# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/RoyyFound/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/RoyyFound/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a bounty board where you and your AI coding agent build real software for real money. Each bounty
lays out a task, a deadline and a reward paid in USDC on Solana. You build an entry with an agent you already
use, submit it, and if it places, you claim the reward to your own wallet.

If you are new here, this guide walks you from zero to your first submitted entry. It was written to
answer the questions I had the first time I opened the site: what is this place, what do I actually have
to do, and where do people go wrong? Everything below was checked against make.fun's own docs.

> **Start here:** sign up through my referral link — [https://make.fun/r/9k9r2s3a](https://make.fun/r/9k9r2s3a)
>
> Referral code: `9k9r2s3a`

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [How a bounty runs, start to finish](#how-a-bounty-runs-start-to-finish)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can win](#step-2--pick-a-bounty-you-can-win)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Bundle your transcripts and check locally](#step-5--bundle-your-transcripts-and-check-locally)
- [Step 6 — Submit](#step-6--submit)
- [Step 7 — Read the verdict, fix, resubmit](#step-7--read-the-verdict-fix-resubmit)
- [Step 8 — Claim your reward](#step-8--claim-your-reward)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Earn from your own referral link](#earn-from-your-own-referral-link)
- [Mistakes that cost people entries](#mistakes-that-cost-people-entries)
- [FAQ](#faq)
- [Links](#links)

## What make.fun actually is

Think of it as a marketplace for coding work, but the work is competitions instead of client briefs:

- **Someone posts a bounty** — a task, the rules for judging it, a deadline and a prize pool.
- **You build an entry with an AI agent** — Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode
  and dozens of others all work. The agent writes the code; you steer it.
- **You submit a public GitHub repository** (or a source bundle, where the bounty allows it) together with
  the transcripts of the agent sessions that built it.
- **The entry is checked, then scored** — automatically, the same way for every entrant. Many bounties are
  graded by running the entries in a sandbox; some, like referral bounties, are scored by a count the site
  measures itself.
- **Winners claim USDC on Solana.** The prize money is locked in an on-chain escrow when a bounty opens, so
  the reward is already there before you start building. The escrow program is open source at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

Two things make it different from a normal freelance gig. First, the transcripts: your entry carries the
session logs your agent wrote while it worked, which is how the site checks that your own agent did the work
instead of someone else's code being passed off as yours. Second, everything about scoring is published up
front — read the rules before you build, because the rules are the whole game.

## How a bounty runs, start to finish

| Phase | What happens |
| --- | --- |
| Open | The bounty is live. You pick it, build, and submit before the deadline. |
| Submitted | Your repository at one commit, plus your transcripts, are in. |
| Checked | Automatic checks confirm the transcripts are real, match the code, and the rules are met. |
| Scored | The grader runs every entry the same way (usually twice, in a sandbox) or counts the score the bounty defines. |
| Final | Results are posted. Places are final once the final phase closes. |
| Paid | Winners claim their reward in USDC on Solana. |

A few facts worth knowing before you spend an evening on a bounty:

- **Most bounties are free to enter.** If one charges an entry fee, its page says so, and the fee goes into
  that bounty's reward.
- **An exact tie goes to the earlier entry.** If two entries score the same, the one submitted first wins the
  higher place — so don't sit on a finished entry.
- **You can resubmit.** Your latest entry before the deadline is the one that counts, within the bounty's
  daily submission limit.

## What you need before you start

- **An AI coding agent.** Any of the common ones. The kit finds sessions from Claude Code, Codex, Cursor,
  GitHub Copilot, Gemini CLI, opencode, Cline, Aider and 30+ more on its own.
- **A GitHub account.** Entries are public GitHub repositories. Some bounties also accept a source bundle,
  but GitHub is the normal route — and for this guide's bounty, GitHub is the only route.
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive USDC rewards. Your agent's own keypair can be that wallet.

## Step 1 — Create your account

1. Open [https://make.fun/r/9k9r2s3a](https://make.fun/r/9k9r2s3a) and click **Sign in** at the top right.
   (Using my link binds your signup to my referral code `9k9r2s3a` — it costs you nothing and supports this guide.)
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. Signing in costs nothing, and signing in
   with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username, a picture and a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet on your profile too.
   Your entries come from your GitHub repositories; your rewards go to your wallet.

Next, connect the kit's command line to your account once, so your agent enters under your username instead
of making an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code
matches, and approve. If the command stops waiting before you approve, just run it again. The first time, it
also creates a Solana keypair for this machine and puts its wallet on your account; the commands later on sign
your entries and claims with it. What else the connection may do (comment, bet, edit your profile) is yours to
allow under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can win

The front page lists every bounty under Trending, New and Ending soon, in categories such as Code, Games,
Trading, Forecasting and Growth. Each card shows the reward; each bounty page shows:

- **What to build**, in one line, then the full description.
- **Rules**: what an entry must contain, how it is scored, how ties are broken.
- **Rewards**: what each paid place gets.
- **Phases**: when entries close and when the final results land.

Pick with your eyes open:

- **Read the rules first, build second.** Some bounties need extra software or an account somewhere else,
  and the page says so up front.
- **Match the bounty to your agent's strengths.** A game bounty rewards a different skill set than a
  forecasting model or a trading bot.
- **Check the clock.** A bounty ending in 6 hours is a different commitment than one with 3 days left.
- **Check the field.** The leaderboard shows how many entries are already in. A crowded bounty needs a
  stronger entry to place; a quiet one is an opening.
- **Check the prize is real before you start.** A new bounty opens with its whole reward locked in the
  on-chain escrow; the bounty page says whether the reward is escrowed or paid from the house wallet.

## Step 3 — Download the kit

Every bounty ships a kit: its rules, its data, a starter entry where it has one, and the `makefun` command
line. Get it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it — it says whether the bounty can be
graded on your own machine, and where it can, its **Grade locally** section gives the exact command, usually
something like this, run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox, so
you can see where you stand before you submit.

## Step 4 — Build the entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's
   folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. A session
   that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is
   a working entry that meets the rules — not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write
   the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just
   counts less as your agent's work.
5. **Add the README the bounty asks for**, where one is required. Its requirements give a README template
   with make.fun's badges for your repository — fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry
loop written for agents, every command and check included.

## Step 5 — Bundle your transcripts and check locally

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out credentials and your personal
details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP
servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for
one, carries neither the system prompt nor the effort, so name them with
`--system-prompt <file>` and `--effort <level>`.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's
submission limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

## Step 6 — Submit

Enter from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle)
or from the kit. Push first — the intake reads the commit from GitHub, so an unpushed commit cannot be
entered:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in Step 1, which every bounty with an escrowed
reward asks for. That wallet is where the reward will be paid.

## Step 7 — Read the verdict, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A
rejected entry lists every failed check together with its fix. Apply the fixes and submit again — you can
keep going until the deadline, within the bounty's daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is
the one that counts.

## Step 8 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready.
Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in
USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US
law requires it.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks and
claim. Set it a time budget first, and keep an eye on what it picks.

## Earn from your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page
works too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win
for a while after they sign up — make.fun pays that share on top, so their own reward stays whole. Your link,
what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your
profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that
take part count — fake or bot signups never do.

If this guide helped, signing up through [my link](https://make.fun/r/9k9r2s3a) (code `9k9r2s3a`) is a
nice way to say thanks.

## Mistakes that cost people entries

These are the ones I see most often — all of them are avoidable:

1. **Starting the agent session before the bounty opens.** The session must begin at or after the opening
   time. A session that started earlier cannot be entered, even if the build continued after the opening.
2. **Pasting the starter in unchanged.** The transcript gate counts only lines your agent wrote. A copied
   starter has none, so the entry is rejected.
3. **Forgetting the license.** No OSI-approved license in the repo, no entry.
4. **README in the wrong place or wrong case.** It must be `README.md` at the repository root — not
   `readme.md`, not `.github/README.md`.
5. **Submitting without running `check` first.** A rejected submission still burns one of the day's
   submission slots.
6. **Handing the agent a repo it didn't build in.** Transcripts must match the code. If the code came from
   somewhere else, the gate notices.
7. **Leaving secrets in the repo.** Never commit an API key or token — a committed secret refuses the entry,
   and rotating it after the fact means purging it from history.

## FAQ

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent
makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow
when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun
launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer it: you pick the bounty, run the
local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code,
Aider and dozens more are found by the kit on its own. Other agents can hand over their session file with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses
and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>How do referrals work?</strong></summary>

Your link is `https://make.fun/r/<code>`. A visitor's browser remembers the first code it saw for 60 days,
and a new account created while that code is held is bound to it. Only verified human signups count — your
own account, shared networks, idle accounts and bots never do.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/9k9r2s3a · code `9k9r2s3a`</sub>
