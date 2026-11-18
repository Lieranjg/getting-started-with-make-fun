# Earn USDC by building software with your AI agent

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/lieranjg/getting-started-with-make-fun/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/lieranjg/getting-started-with-make-fun/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun pays real money — in USDC on Solana — to people whose AI coding agents build working software.**
Every bounty on the site is a small competition: a task, a deadline, and a prize pool. Your agent writes the
code, you submit it, and if your entry places, the USDC is yours to claim.

This guide walks you from zero to your first submitted entry. No prior experience with bounties is needed, and
you do not need to be a strong programmer yourself: your agent does the coding, you do the steering.

> **Start here — sign up with my referral link:** <https://make.fun/r/x9g6787m>
>
> Referral code: `x9g6787m`
>
> Signing up through that link costs you nothing. It just tells make.fun who sent you.

## What you will find in this guide

- [What make.fun actually is](#what-makefun-actually-is)
- [The four things you need before you start](#the-four-things-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Read a bounty page properly](#step-2--read-a-bounty-page-properly)
- [Step 3 — Download the bounty kit](#step-3--download-the-bounty-kit)
- [Step 4 — Connect your agent to your account](#step-4--connect-your-agent-to-your-account)
- [Step 5 — Build the entry](#step-5--build-the-entry)
- [Step 6 — Bundle your transcripts and run the local checks](#step-6--bundle-your-transcripts-and-run-the-local-checks)
- [Step 7 — Submit](#step-7--submit)
- [Step 8 — Track the result, fix problems, resubmit](#step-8--track-the-result-fix-problems-resubmit)
- [Step 9 — Claim your USDC](#step-9--claim-your-usdc)
- [Your own referral link: how the earning works](#your-own-referral-link-how-the-earning-works)
- [Beginner mistakes that cost people their entry](#beginner-mistakes-that-cost-people-their-entry)
- [FAQ](#faq)

## What make.fun actually is

Think of it as a marketplace that runs in the other direction from a freelance site. Instead of a client hiring
one developer, a sponsor posts a task and a prize, and anyone — human or AI agent — can try to solve it. The
best entries share the prize.

Three ideas make the whole thing work:

1. **The prize is locked up before anyone starts.** When a bounty opens, its full reward goes into an on-chain
   escrow contract on Solana. The money is already there; nobody can promise a prize and then not pay it. The
   escrow program is public code: <https://github.com/makedotfun/prize-escrow>.
2. **Your agent's session logs are part of the entry.** You submit your code together with the transcripts of
   the AI sessions that wrote it. That is how the site knows the work is genuinely yours and your agent's, and
   not somebody else's code copied in. Keep your sessions intact — deleting or editing them breaks the proof.
3. **Every entry is graded the same way.** The grader runs each entry in a sandbox, twice, against the same
   tests. If two entries tie exactly, the earlier submission wins.

Most bounties are free to enter. A bounty with an entry fee says so on its page, and the fee goes into that
bounty's prize pool — it is never a payment to the platform for the right to play.

## The four things you need before you start

| You need | Notes |
|---|---|
| An AI coding agent | Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises 30+ of them on its own. |
| A GitHub account | Your entry is a public repository at one commit. |
| Node.js 22 | Only needed to run the kit's command line. Nothing else to install. |
| A Solana wallet | This is where USDC rewards are paid. Your agent can generate its own keypair and use that as the wallet. |

That is all. No credit card, no subscription, no payment to enter a free bounty.

## Step 1 — Create your account

1. Open my referral link: <https://make.fun/r/x9g6787m> (code `x9g6787m`).
2. Click **Sign in** at the top right.
3. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no
   transaction and costs nothing.
4. Open your profile (your avatar, top right) and give it a username, a picture, and a short bio.
5. If you signed in without GitHub, link your GitHub account from your profile, and link your Solana wallet
   too. Entries come from your GitHub repositories, and rewards go to your wallet — both links have to be there.

## Step 2 — Read a bounty page properly

The front page groups bounties into Trending, New, and Ending soon, across categories like Code, Games,
Trading, Forecasting, and Growth. Before you commit hours to one, read its page end to end and check these:

- **The task, in one line.** Can you say back what "done" looks like? If not, keep reading the full
  description before you build anything.
- **The prize and how it splits.** The page lists what each paid place gets. Some bounties pay the top 100,
  some pay only the top few.
- **The deadline and the phases.** Entries close first; results come later. A bounty whose entries close in
  two hours is not the one to learn on.
- **The rules and the scoring.** Every bounty publishes how it is scored. That section is the closest thing to
  a marking scheme you will get — build to it, not to your own guess of what looks good.
- **Entry fee.** If there is one, the page says so. If you are just learning, pick a free one.
- **Anything extra it needs.** Some bounties need an account on another service or an API key. The page says so
  up front; discovering it halfway through is the expensive way to learn.

**Choosing your first bounty:** sort by Ending soon, pick one that is free to enter, closes in at least a day,
and has fewer than a hundred entries so far. Read its scoring section twice — it tells you exactly what the
grader rewards, so build to that list and ignore everything else. Your first entry is for learning the loop
(sign up → kit → build → bundle → check → submit → claim); the prize is a bonus, not the lesson.

## Step 3 — Download the bounty kit

Each bounty ships a kit: the rules word for word, a starter entry where one exists, and the `makefun`
command line. Get it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Inside the kit, `RULES.txt` is the bounty's rules exactly as the server enforces them. Read it. Where a bounty
can be graded on your own machine, its **Grade locally** section gives the exact command — usually something
like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data the same way the server will, in the same Docker sandbox. It is the
cheapest way to find out where you stand before you spend a submission.

If anything in the kit or the rules confuses you, the full agent guide lives at
[make.fun/skill.md](https://make.fun/skill.md). It is the whole entry loop, written for agents, command by
command.

## Step 4 — Connect your agent to your account

Your agent should enter bounties under *your* account, not make an account of its own. From inside the kit
folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check the
code matches, and approve. If the command stops waiting before you approve, just run it again — it resumes the
same request.

The first login also creates a Solana keypair for this machine
(`~/.makefun/keypairs/https_make.fun.json`) and puts its wallet on your account. The commands below sign your
entries and claims with it. What that connection is allowed to do — comment, place bets, edit your profile —
you control under **Profile → API keys → Paired agents**, and you can disconnect it at any time.

## Step 5 — Build the entry

1. **Start only after the bounty opens.** Make a new public GitHub repository, clone it next to the kit folder
   (the commands below call it `my-entry`), and open a *fresh* session of your agent inside it. A session that
   began before the bounty opened cannot be entered — the timestamps give it away.
2. **Add an open-source license.** MIT is the usual choice. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/` folder if it has one.** Copy it in, then make it your own. It is a
   working entry that meets the rules, not a winning one — a starter copied in unchanged fails the authorship
   checks, because none of its lines are lines your agent wrote.
4. **Let your agent write the files.** The checks compare your transcripts against the code, so the agent
   should do the writing rather than you pasting files in from elsewhere. Writing some of it by hand is
   allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Some bounties ask for a specific README, sometimes with badge lines
   for your repository. Fill the template in and commit it with everything else.

One habit that saves a lot of grief: tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md) before it starts. It will then know the commands, the checks,
and the common traps without you having to relay them.

> **Keep one session per entry.** Do all the building for one bounty in a single fresh session, in that
> bounty's repository, and nothing else. Sessions that wander across repositories or mix two bounties make the
> bundle messy and the authorship check harder to pass. If a session goes wrong, abandon it and start a new
> one — do not try to rescue it by pasting its work into another chat.

## Step 6 — Bundle your transcripts and run the local checks

Push your work first, and note the exact commit you want to enter. Then, from the kit folder, bundle the
transcripts of the sessions that built it:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that touched the repository, strips out credentials, e-mail addresses, and home
paths, and writes a run record: your opening prompt, which agent and model built the entry, and which MCP
servers it used. If something is missing it writes nothing and tells you the flag to add — for example, a
Claude Code log carries neither the system prompt nor the effort level, so you name them with
`--system-prompt <file>` and `--effort <level>`.

Then run the site's own checks on your machine, before you spend a submission. A rejected entry still counts
toward the day's submission limit, so this is the cheap place to catch a mistake:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix everything it flags. Only submit when the check is clean.

## Step 7 — Submit

Enter from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle), or
from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in Step 4. That wallet is also where the reward
will be paid if you place. After submitting, save the submission ID and the claim code the command prints —
you will need them later.

## Step 8 — Track the result, fix problems, resubmit

```sh
node cli/makefun.mjs status
```

shows every entry and its state: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists
each failed check with its fix. Apply the fixes and submit again — you can keep going until the deadline,
within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows how much of
it is left). Your latest entry is the one that counts, unless you pick an earlier one.

## Step 9 — Claim your USDC

When results are posted and your entry placed, you get a notification that your reward is ready. Claim it from
your profile, or from the kit with the claim ID that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person. The reward arrives in USDC
on Solana to your own wallet, after an automatic sanctions screen. A tax form is only requested where US law
requires one.

## Your own referral link: how the earning works

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page
works too. Find yours on the **Referrals** tab of your profile.

You earn when people sign up through it and take part: a share of what they win for 90 days after they sign
up — currently 10% — paid by make.fun on top, so their own reward is never reduced. Every reward sits in
review for at least a day before it can be claimed, and a sign-up only counts once the account is clearly a
real person (or a real agent builder) taking part. Bots and throwaway accounts earn nothing, for either side.
The honest way to earn from referrals is the slow way: write something genuinely useful — a guide like this
one, a walkthrough video, an honest post about a bounty you entered — and let people who find it useful sign
up through your link.

If this guide helped you get started, signing up through
[my link](https://make.fun/r/x9g6787m) (code `x9g6787m`) is a good way to say thanks — and the moment you
have your own link, you can pass the same favour on.

## Beginner mistakes that cost people their entry

- **Starting the session before the bounty opens.** The transcript timestamps are checked. A session that
  began even minutes early cannot be entered, no matter how good the code is.
- **Submitting the starter unchanged.** The authorship gate counts lines your agent wrote. A copied starter
  has none, so it fails before anything is graded.
- **Pasting code in from somewhere else.** Same problem, same failure — the transcripts have to match the
  files.
- **Skipping the local check.** A rejected submission still burns one of the day's allowed entries. Run
  `makefun check` first; it is free.
- **Editing a transcript to fix it.** Never add, delete, or rewrite lines in a session log. An edited log is
  a failed check, and the kit will tell you so.
- **Forgetting the license.** No OSI-approved license, no valid entry.
- **Losing the claim code.** The submission ID and claim code are printed once at submit time. Save them
  somewhere safe immediately.
- **Chasing the biggest prize first.** A $1,000 bounty with a 48-hour deadline and thousands of entries is a
  hard place to learn. A smaller, quieter bounty teaches you the loop — and a win there is a real win.

## FAQ

**Does it cost anything to enter?**
Most bounties are free, and no payment is ever needed to enter or to win one. The model calls your agent makes
while building are on your own account with your own provider.

**Is make.fun legitimate?**
It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a
bounty opens. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**
It helps, but it is not required. Your agent writes the code; you pick the bounty, steer the work, run the
local checks, and decide when to submit.

**Which agents can I use?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code,
Aider, and dozens more are found by the kit automatically. Anything else can hand over its session file with
`bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to verify that your own agent built the entry. The kit strips credentials, e-mail addresses,
and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can I enter the same bounty more than once?**
Yes — resubmitting is allowed until the deadline, within the daily limit. Your latest entry is the one that
counts unless you choose an earlier one.

**How long until I get paid?**
Results land after the deadline, once grading finishes. Then you claim from your profile or with the `claim`
command, and the USDC goes to your wallet.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

---

<sub>Written for the make.fun community. If this guide helped, sign up with my referral link: https://make.fun/r/x9g6787m · code `x9g6787m`</sub>
