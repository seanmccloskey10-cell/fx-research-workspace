# HANDOFF-PROMPT.md — Paste this into Claude Code

The fastest way to set up this workspace: open VS Code, run `claude` in the terminal to start Claude Code CLI, then paste **one** of the two prompts below into the chat. Pick the one matching your OS. The agent enters plan mode first, confirms what's on your machine, asks for one "go," then clones the workspace.

## ⚠ Read this first — install prerequisites before pasting the handoff prompt

This workspace requires:

- **Git**
- **VS Code**
- **Node.js + npm** (for installing Claude Code CLI)
- **Claude Code CLI** (`claude` command in a terminal — *NOT* the VS Code "Claude" extension; they are different products)
- **Authenticated to a Claude plan** (not via `ANTHROPIC_API_KEY` env var)

**The Claude Code CLI is critical for this workspace specifically** — the deep-research feature dispatches sub-agents in parallel, which is a CLI capability. The VS Code extension's chat panel may or may not support the same dispatch behavior; if you're using the extension and the 5-agent fan-out doesn't work, fall back to single-agent research or switch to the CLI.

**If any prerequisites are missing, run [PREREQUISITES.md](PREREQUISITES.md) FIRST.** The prerequisites prompt batches every install into one elevated session (one UAC popup on Windows, one Apple GUI password dialog on Mac) so you don't drown in permission prompts. It also installs the Claude Code CLI and verifies plan auth.

This workspace itself is much lighter than the [dashboard's handoff](https://github.com/seanmccloskey10-cell/exotic-fx-research-desk/blob/main/HANDOFF-PROMPT.md) — there's nothing to install in the workspace itself, just clone and start. The handoff prompts below check prerequisites at the top; if they're missing, the agent will tell you to go run PREREQUISITES.md first.

The prompts include:

- **Plan mode FIRST** — propose what it'll do before running anything
- **Prerequisites check** — verify the CLI + auth before doing anything else
- **OS-aware adjustments** — paths and commands that match your machine
- **Read CLAUDE.md** — to understand the deep-research workflow before the first request
- **Confirm `claude login` (not API key)** — this workspace runs on your Claude plan; an `ANTHROPIC_API_KEY` here would defeat the entire point

---

## Mac variant — paste this if you're on macOS

```
Someone built me a small VS Code project they want me to clone to my
Mac. It's not a tool to install — it's a folder I'll talk to via
Claude Code CLI to do deep currency research on my Claude plan (no
API key, no metered calls). I work in FX research and I'm AI-fluent
(heavy Claude user) but not a developer.

I want you to clone this for me:

    https://github.com/seanmccloskey10-cell/fx-research-workspace

It's literally just a folder with a CLAUDE.md and a README.md inside.
There's nothing to build. Setup should take 2 minutes IF prerequisites
are already in place.

OS HANDOFF — IMPORTANT
This was built and tested on Windows 11. I'm on macOS. The CLAUDE.md
in the repo doesn't have any OS-specific code, so the workspace
itself is OS-agnostic. But the way you (the agent) interact with the
file system might differ — use macOS path conventions (~/Projects,
forward slashes) and macOS-native commands where it matters.

PREREQUISITES CHECK — DO THIS FIRST
Before anything else, verify I have the prerequisites installed:
- Git: `git --version`
- VS Code: `which code` (NOT bare `code` in some setups — use the
  full PATH lookup)
- Node.js + npm: `node --version` and `npm --version`
- Claude Code CLI: `which claude`
- Plan auth (NOT API key): `echo $ANTHROPIC_API_KEY` should return
  empty / unset

DISAMBIGUATION — IMPORTANT FOR THIS WORKSPACE
"Claude Code CLI" (the `claude` command in Terminal) is a separate
product from the "Claude" VS Code extension. This workspace is
designed for the CLI specifically because deep-research uses
sub-agent dispatch, which is a CLI capability. If I'm currently
talking to you through the VS Code extension chat panel, that's
fine for setting up — but the actual deep-research feature may not
work the same way through the extension. Confirm `which claude`
returns a real path before proceeding.

If ANY prerequisites are missing, STOP and tell me. I'll go run
the prerequisites prompt at PREREQUISITES.md in this same repo
(https://github.com/seanmccloskey10-cell/fx-research-workspace/blob/main/PREREQUISITES.md)
to install them properly in one batch — then come back here.

If all prerequisites are good, proceed:

I'll say "go" once when you ask. Don't ask again per command.

Please follow this flow:

1. ENTER PLAN MODE FIRST. After confirming prerequisites, tell me
   what you propose to do (clone path + which docs you'll read).
   Don't start running anything until I say "go".

2. Clone the repo into ~/Projects/fx-research-workspace.

3. Read README.md and CLAUDE.md end-to-end. CLAUDE.md is the agent
   guide for this workspace — it explains the natural-language
   triggers I'll use ("do deep research on X", "use 5 agents in
   parallel"), the 5-angle decomposition default, and the briefing
   template you'll write to. Read it ALL before I ask anything.

   FOR REFERENCE — when I say "deep research on [currency]", the
   default 5-agent fan-out is:
   1. MONETARY POLICY — central bank stance, rates trajectory,
      recent communications, real rate vs peers
   2. FISCAL & MACRO — debt path, primary balance, inflation,
      growth, current-account dynamics
   3. CAPITAL FLOWS & TRADE — portfolio flows, FDI, trade balance
      composition, FX reserve movements
   4. GEOPOLITICS & REGIONAL CONTEXT — political stability, regional
      spillovers, sanctions / trade-war exposure, election cycle
   5. TECHNICALS & FLOW — price action vs key levels, real-money
      vs leveraged positioning, recent flow color
   Each agent runs in parallel with web access. You collect their
   reports and synthesize one briefing into `briefings/<topic>-<date>.md`.

   For theme questions (e.g. "EM funding stress") — decompose by
   which currency-pair pockets the theme touches, not the country
   shape. For comparative questions (e.g. "TRY vs ZAR") — drop to
   3 agents: macro divergence, flow divergence, technical divergence.

   Always show me the proposed decomposition before dispatching.
   I should be able to swap an angle if I want.

4. Open the folder in VS Code.

5. Stop. Don't dispatch any sub-agents proactively. The workspace is
   ready when the folder exists, the docs are read, and Claude Code
   is running in the folder. I'll trigger my first deep research
   when I'm ready.

WHAT "DONE" LOOKS LIKE — tell me ONLY when you've verified ALL of these:
- All prerequisites confirmed (git, vscode, node, claude CLI, plan auth)
- The folder ~/Projects/fx-research-workspace/ exists with CLAUDE.md,
  README.md, briefings/, .gitignore
- VS Code can open the folder without errors
- I'm authenticated via my plan, not an API key

If any of those aren't right, don't say "it's working" — stop and
tell me exactly what's off.

WHAT YOU SHOULD KNOW ABOUT THIS WORKSPACE
This is the COMPANION to a dashboard repo (exotic-fx-research-desk).
The dashboard is a Streamlit website — when its AI Briefing button
fires, it uses an Anthropic API key (metered, separate bill). This
workspace is the opposite: every deep-research run dispatches
sub-agents inside Claude Code, all of which share my Claude plan
auth. No API key, no second bill. The contrast is intentional —
please don't muddy it by suggesting I add an API key here. There's
no .env in this repo for a reason.

If you hit anything unexpected — STOP and ask me. Don't silently
skip or work around anything.

Report back at each major step. Keep me in the loop.

Let's begin — please run the prerequisites check and tell me what
you find.
```

---

## Windows variant — paste this if you're on Windows

```
Someone built me a small VS Code project they want me to clone to my
Windows PC. It's not a tool to install — it's a folder I'll talk to
via Claude Code CLI to do deep currency research on my Claude plan
(no API key, no metered calls). I work in FX research and I'm
AI-fluent (heavy Claude user) but not a developer.

I want you to clone this for me:

    https://github.com/seanmccloskey10-cell/fx-research-workspace

It's literally just a folder with a CLAUDE.md and a README.md inside.
There's nothing to build. Setup should take 2 minutes IF prerequisites
are already in place.

OS HANDOFF — IMPORTANT
This was built and tested on Windows 11. Use Windows path conventions
(%USERPROFILE%\Projects\..., backslashes in paths). USE POWERSHELL
for the prerequisite version checks (NOT bash / git-bash — bash on
Windows resolves some commands differently and gives confusing
output).

PREREQUISITES CHECK — DO THIS FIRST
Before anything else, verify I have the prerequisites installed.
USE POWERSHELL for these checks:

- Git: `git --version`
- VS Code: `where.exe code` (NOT bare `code --version` — on Windows
  in bash, `code` may resolve to a Node.js binary inside VS Code's
  bundled folder and return a Node version like v22.x. Use
  `where.exe code` to see all candidates and pick the one ending
  in `code.cmd`. Or run `code.cmd --version` directly in PowerShell.)
- Node.js + npm: `node --version` and `npm --version`
- Claude Code CLI: `where.exe claude` (returns a path if installed,
  empty if not; bare `claude --version` will throw "command not
  recognized" if missing but won't tell you whether it's a missing
  binary or a PATH issue).
- Plan auth (NOT API key):
  `Get-Item Env:\ANTHROPIC_API_KEY -ErrorAction SilentlyContinue`
  (should return empty)

DISAMBIGUATION — IMPORTANT FOR THIS WORKSPACE
"Claude Code CLI" (the `claude` command in a terminal) is a separate
product from the "Claude" VS Code extension. This workspace is
designed for the CLI specifically because deep-research uses
sub-agent dispatch, which is a CLI capability. If I'm currently
talking to you through the VS Code extension chat panel, that's
fine for setting up — but the actual deep-research feature may not
work the same way through the extension. Confirm `where.exe claude`
returns a real path before proceeding.

If ANY prerequisites are missing, STOP and tell me. I'll go run
the prerequisites prompt at PREREQUISITES.md in this same repo
(https://github.com/seanmccloskey10-cell/fx-research-workspace/blob/main/PREREQUISITES.md)
to install them properly in one batched session — then come back
here.

If all prerequisites are good, proceed:

I'll say "go" once when you ask. Don't ask again per command.

Please follow this flow:

1. ENTER PLAN MODE FIRST. After confirming prerequisites, tell me
   what you propose to do (clone path + which docs you'll read).
   Don't start running anything until I say "go".

2. Clone the repo into %USERPROFILE%\Projects\fx-research-workspace.

3. Read README.md and CLAUDE.md end-to-end. CLAUDE.md is the agent
   guide for this workspace — it explains the natural-language
   triggers I'll use ("do deep research on X", "use 5 agents in
   parallel"), the 5-angle decomposition default, and the briefing
   template you'll write to. Read it ALL before I ask anything.

   FOR REFERENCE — when I say "deep research on [currency]", the
   default 5-agent fan-out is:
   1. MONETARY POLICY — central bank stance, rates trajectory,
      recent communications, real rate vs peers
   2. FISCAL & MACRO — debt path, primary balance, inflation,
      growth, current-account dynamics
   3. CAPITAL FLOWS & TRADE — portfolio flows, FDI, trade balance
      composition, FX reserve movements
   4. GEOPOLITICS & REGIONAL CONTEXT — political stability, regional
      spillovers, sanctions / trade-war exposure, election cycle
   5. TECHNICALS & FLOW — price action vs key levels, real-money
      vs leveraged positioning, recent flow color
   Each agent runs in parallel with web access. You collect their
   reports and synthesize one briefing into `briefings/<topic>-<date>.md`.

   For theme questions (e.g. "EM funding stress") — decompose by
   which currency-pair pockets the theme touches, not the country
   shape. For comparative questions (e.g. "TRY vs ZAR") — drop to
   3 agents: macro divergence, flow divergence, technical divergence.

   Always show me the proposed decomposition before dispatching.
   I should be able to swap an angle if I want.

4. Open the folder in VS Code.

5. Stop. Don't dispatch any sub-agents proactively. The workspace is
   ready when the folder exists, the docs are read, and Claude Code
   is running in the folder. I'll trigger my first deep research
   when I'm ready.

WHAT "DONE" LOOKS LIKE — tell me ONLY when you've verified ALL of these:
- All prerequisites confirmed (git, vscode, node, claude CLI, plan auth)
- The folder C:\Users\<me>\Projects\fx-research-workspace\ exists
  with CLAUDE.md, README.md, briefings\, .gitignore
- VS Code can open the folder without errors
- I'm authenticated via my plan, not an API key

If any of those aren't right, don't say "it's working" — stop and
tell me exactly what's off.

WHAT YOU SHOULD KNOW ABOUT THIS WORKSPACE
This is the COMPANION to a dashboard repo (exotic-fx-research-desk).
The dashboard is a Streamlit website — when its AI Briefing button
fires, it uses an Anthropic API key (metered, separate bill). This
workspace is the opposite: every deep-research run dispatches
sub-agents inside Claude Code, all of which share my Claude plan
auth. No API key, no second bill. The contrast is intentional —
please don't muddy it by suggesting I add an API key here. There's
no .env in this repo for a reason.

If you hit anything unexpected — STOP and ask me. Don't silently
skip or work around anything.

Report back at each major step. Keep me in the loop.

Let's begin — please run the prerequisites check (in PowerShell, not
bash) and tell me what you find.
```

---

## Cross-references

- Prerequisites prompt: [PREREQUISITES.md](PREREQUISITES.md) — run this FIRST if you don't already have Claude Code CLI installed
- Sibling repo: [`exotic-fx-research-desk`](https://github.com/seanmccloskey10-cell/exotic-fx-research-desk) — companion dashboard with its own handoff prompt
