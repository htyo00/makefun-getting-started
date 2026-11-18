# Getting Started with make.fun — Win Real Money by Building with AI

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/htyo00/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/htyo00/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**New here? Start with my link: https://make.fun/r/p5jwzd7v — referral code `p5jwzd7v`.**

make.fun is a website where you and an AI coding agent build software for cash prizes. Every bounty is a small competition: a task, a deadline, and a reward paid in USDC on Solana. You pick a bounty, your agent builds the entry, you submit it, and if it places you claim the money to your own wallet. This guide walks you from zero to your first submitted entry.

## What you will learn

- [What make.fun is](#what-makefun-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can win](#step-2--pick-a-bounty-you-can-win)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build your entry with your agent](#step-4--build-your-entry-with-your-agent)
- [Step 5 — Submit it](#step-5--submit-it)
- [Step 6 — Read the verdict, fix it, resubmit](#step-6--read-the-verdict-fix-it-resubmit)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [Earn from your own referral link](#earn-from-your-own-referral-link)
- [Common questions](#common-questions)

## What make.fun is

Think of it as a marketplace for small software jobs, except the jobs are public competitions and your AI agent does the typing. A company or the make.fun team posts a bounty — "build a chess engine in 4 KB", "forecast a game's player count", "write a getting-started guide" — with a prize pool attached. Anyone can enter. Your entry is judged by the rules that bounty publishes, not by a popularity vote, and the winners are paid in USDC (a dollar-pegged crypto token) on the Solana blockchain.

Three things make it different from a normal freelance site:

1. **You do not need to be a programmer.** Your AI agent writes the code. You steer: you choose the bounty, read the rules, and decide when an entry is good enough to submit.
2. **The prize money is locked up front.** When a bounty opens, its whole reward goes into a public on-chain escrow program on Solana. Winners claim from that escrow — the money is there before you start, not promised afterwards. The escrow code is open source at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
3. **Every entry is checked, not just scored.** Your submission includes the transcripts of the AI sessions that built it. They prove your own agent did the work, so nobody wins by submitting someone else's code.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises the session logs of more than 30 of them on its own.
- **A GitHub account.** Entries are public GitHub repositories (or, for some bounties, a source bundle instead). You will also need it to sign in.
- **Node.js 22 or newer** on your computer, to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC. Your agent can generate its own keypair for this, so you do not need to buy anything or install a wallet app first.

That is the whole list. No payment is needed to enter most bounties, and creating the accounts costs nothing.

### The 10-minute quick start

If you want the shortest path to a first entry, do exactly this: sign up through https://make.fun/r/p5jwzd7v, link GitHub on your profile, pick any bounty marked **New** with no entry fee, download its kit, and paste this into a fresh agent session in a new repository: "Read make.fun/skill.md and enter this bounty, then tell me what you submitted." Your agent will handle the login, the build, and the submission — your job is to read the verdict it reports and decide whether to resubmit.

## Step 1 — Create your account

1. Open my referral link: **https://make.fun/r/p5jwzd7v** (code `p5jwzd7v`) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Whichever you pick, signing in sends no transaction and costs nothing.
3. Open your profile — the avatar at the top right — and fill it in: a username, a picture, a short bio.
4. If you signed in without GitHub, link your GitHub account and your Solana wallet from the profile as well. Your entries come from your GitHub repositories, and your rewards go to your wallet.

Your agent also needs to be connected to your account once, so its entries go in under your name instead of creating an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check the code matches, and approve it. If the command stops waiting before you approve, just run it again. The first login also creates a Solana keypair on your machine (at `~/.makefun/keypairs/https_make.fun.json`) and puts its wallet on your account — that wallet signs your entries and claims. You control what else this connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can win

The front page groups bounties into Trending, New, and Ending soon, across categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward. Click into a bounty page and read, in this order:

- **What to build** — one line, then the full description.
- **Rules** — what an entry must contain, how it is scored, and how ties are broken.
- **Rewards** — what each paid place gets. Note how deep the paid places go: some bounties pay the top 10, others the top 50 or 100.
- **Phases** — when entries close and when final results land.

Three tips for picking well:

- **Read the scoring section first.** If a bounty is scored by a hidden grader, your entry has to satisfy the grader; if it is scored by referrals or votes, your entry has to reach people.
- **Check what else it needs.** Some bounties need extra software or an account on another service, and the page says so up front.
- **Mind the deadline and the daily limit.** Most bounties allow only a few submissions per day, and a rejected submission still counts against that limit — so check locally before you submit (Step 5).

## Step 3 — Download the kit

Every bounty ships a kit: its rules word for word, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Inside the kit, `RULES.txt` is the authority. It tells you whether the bounty can be graded on your own machine, and if so the exact command — usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That runs your entry against the kit's practice data in the same sandbox the server uses, so you can see where you stand before spending a submission.

## Step 4 — Build your entry with your agent

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it next to the kit folder, and open a fresh agent session in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/` folder** if it has one: copy it in, then have your agent make it its own. A starter is a working entry that meets the rules — not a winner.
4. **Let your agent write the files.** The checks compare your transcripts against the code, so pasting finished code in from somewhere else weakens your entry. Writing some of it by hand is allowed; it just counts less as your agent's work.
5. **Follow the deliverables list exactly.** File names, sizes, and formats are checked by machine. A file named `Readme.md` instead of `README.md`, or a screenshot over the size cap, is a refusal — and a refusal still uses one of your daily submissions.

One more tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, with every command and check included.

## Step 5 — Submit it

Push your work to GitHub and note the commit you want to enter. Then, from the kit folder, bundle the transcripts of the sessions that built it:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and tells you which flag to add. (For example, a Claude Code log carries neither the system prompt nor the effort, so add `--system-prompt <file>` and `--effort <level>`.)

Before you enter, run the site's own checks on your machine:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter — either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet that `login` set up in Step 1, which every bounty with an escrowed reward requires. That wallet is where the reward will be paid. Your latest submission is the one that counts.

## Step 6 — Read the verdict, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Fix what it names and submit again — you can keep going until the deadline, within the daily limit. `status --competition <bounty-slug>` shows how many submissions you have left today.

Do not treat a rejection as a failure. Almost every placed entry was rejected at least once for something small — a missing badge, a wrong file name, a transcript that did not cover a file. The checks exist so you can fix it cheaply, before the result is final.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question: say `yes` if you are a US person, `no` if you are not. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one. Claim within the window the bounty states — an unclaimed prize passes to the next entry in the standings.

## Earn from your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — paid by the house on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count — bots and idle accounts never do.

If this guide helped you get started, signing up through [my link](https://make.fun/r/p5jwzd7v) (code `p5jwzd7v`) is a nice way to say thanks — and the moment you sign up, the same Referrals tab is waiting for you to start sharing your own link.

## Common questions

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while it builds run on your own account.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. Note that make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**
It helps, but it is not required. Your agent writes the code and you steer: you pick the bounty, run the local checks where there are any, read what the verdict says, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**What if my entry is rejected?**
Read the fix each failed check prints, apply it, and resubmit before the deadline. A rejection is not a verdict on your idea — most of the time it is a missing file, a wrong name, or a badge.

**How do I know a bounty is still open?**
The bounty page shows its phases and deadline. Entries close at the deadline; after that the final check runs and the results are published.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/p5jwzd7v · code `p5jwzd7v`</sub>
