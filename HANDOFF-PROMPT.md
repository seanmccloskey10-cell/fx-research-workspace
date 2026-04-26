# HANDOFF-PROMPT.md — Paste this into Claude Code

The fastest way to set up this workspace: open VS Code, run `claude` in the terminal to start Claude Code, then paste **one** of the two prompts below into the chat. Pick the one matching your OS. The agent enters plan mode first, confirms what's on your machine, asks for one "go," then clones the workspace.

This is much lighter than the [dashboard's handoff](https://github.com/seanmccloskey10-cell/exotic-fx-research-desk/blob/main/HANDOFF-PROMPT.md) — there's nothing to install here, just clone and start. The prompts include:

- **Plan mode FIRST** — propose what it'll do before running anything
- **OS-aware adjustments** — paths and commands that match your machine
- **Read CLAUDE.md** — to understand the deep-research workflow before the first request
- **Confirm `claude login` (not API key)** — this workspace runs on your Claude plan; an `ANTHROPIC_API_KEY` here would defeat the entire point of the workspace

---

## Mac variant — paste this if you're on macOS

```
Someone built me a small VS Code project they want me to clone to my
Mac. It's not a tool to install — it's a folder I'll talk to via
Claude Code to do deep currency research on my Claude plan (no API
key, no metered calls). I work in FX research and I'm AI-fluent
(heavy Claude user) but not a developer.

I want you to clone this for me:

    https://github.com/seanmccloskey10-cell/fx-research-workspace

It's literally just a folder with a CLAUDE.md and a README.md inside.
There's nothing to build, nothing to install (assuming I already have
VS Code, Claude Code, and Git on my machine). Setup should take 2
minutes.

OS HANDOFF — IMPORTANT
This was built and tested on Windows 11. I'm on macOS. The CLAUDE.md
in the repo doesn't have any OS-specific code, so the workspace
itself is OS-agnostic. But the way you (the agent) interact with the
file system might differ — use macOS path conventions (~/Projects,
forward slashes) and macOS-native commands where it matters.

I'll say "go" once when you ask. Don't ask again per command.

Please follow this flow:

1. ENTER PLAN MODE FIRST. Tell me:
   - Whether I already have VS Code, Claude Code, and Git installed
     (run version checks; report what you find)
   - What you propose to do
   Don't start running anything until I say "go".

2. If VS Code or Claude Code or Git are missing, STOP and tell me.
   I'd rather install them deliberately than have you install them
   silently in the middle of cloning.

3. Verify I'm logged into Claude Code via `claude login` (uses my
   Claude plan), NOT an API key. Run `claude --version` or check the
   auth status however you can. If I'm somehow on an API key instead
   of my plan, STOP and tell me — using an API key here would defeat
   the entire point of this workspace.

4. Clone the repo into ~/Projects/fx-research-workspace.

5. Read README.md and CLAUDE.md end-to-end. CLAUDE.md is the agent
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

6. Open the folder in VS Code.

7. Stop. Don't dispatch any sub-agents proactively. The workspace is
   ready when the folder exists, the docs are read, and Claude Code
   is running in the folder. I'll trigger my first deep research
   when I'm ready.

WHAT "DONE" LOOKS LIKE — tell me ONLY when you've verified ALL of these:
- The folder ~/Projects/fx-research-workspace/ exists with CLAUDE.md,
  README.md, briefings/, .gitignore.
- VS Code can open the folder without errors.
- Claude Code (`claude` in the folder's terminal) starts cleanly and
  has loaded CLAUDE.md as the project instructions.
- I'm authenticated via my plan, not an API key.

If any of those aren't right, don't say "it's working" — stop and
tell me exactly what's off.

WHAT YOU SHOULD KNOW ABOUT THIS WORKSPACE
This is the COMPANION to my dashboard repo. The dashboard is a
Streamlit website — when its AI Briefing button fires, it uses an
Anthropic API key (metered, separate bill). This workspace is the
opposite: every deep-research run dispatches sub-agents inside
Claude Code, all of which share my Claude plan auth. No API key,
no second bill. The contrast is intentional — please don't muddy it
by suggesting I add an API key here. There's no .env in this repo
for a reason.

If you hit anything unexpected — STOP and ask me. Don't silently
skip or work around anything.

Report back at each major step. Keep me in the loop.

Let's begin — please enter plan mode and tell me what's on my machine.
```

---

## Windows variant — paste this if you're on Windows

```
Someone built me a small VS Code project they want me to clone to my
Windows PC. It's not a tool to install — it's a folder I'll talk to
via Claude Code to do deep currency research on my Claude plan (no
API key, no metered calls). I work in FX research and I'm AI-fluent
(heavy Claude user) but not a developer.

I want you to clone this for me:

    https://github.com/seanmccloskey10-cell/fx-research-workspace

It's literally just a folder with a CLAUDE.md and a README.md inside.
There's nothing to build, nothing to install (assuming I already have
VS Code, Claude Code, and Git on my machine). Setup should take 2
minutes.

OS HANDOFF — IMPORTANT
This was built and tested on Windows 11 and is OS-agnostic in
content. Use Windows path conventions
(%USERPROFILE%\Projects\..., backslashes in paths) where appropriate.

I'll say "go" once when you ask. Don't ask again per command.

Please follow this flow:

1. ENTER PLAN MODE FIRST. Tell me:
   - Whether I already have VS Code, Claude Code, and Git installed
     (run version checks; report what you find)
   - What you propose to do
   Don't start running anything until I say "go".

2. If VS Code or Claude Code or Git are missing, STOP and tell me.
   I'd rather install them deliberately than have you install them
   silently in the middle of cloning.

3. Verify I'm logged into Claude Code via `claude login` (uses my
   Claude plan), NOT an API key. Run `claude --version` or check the
   auth status however you can. If I'm somehow on an API key instead
   of my plan, STOP and tell me — using an API key here would defeat
   the entire point of this workspace.

4. Clone the repo into %USERPROFILE%\Projects\fx-research-workspace.

5. Read README.md and CLAUDE.md end-to-end. CLAUDE.md is the agent
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

6. Open the folder in VS Code.

7. Stop. Don't dispatch any sub-agents proactively. The workspace is
   ready when the folder exists, the docs are read, and Claude Code
   is running in the folder. I'll trigger my first deep research
   when I'm ready.

WHAT "DONE" LOOKS LIKE — tell me ONLY when you've verified ALL of these:
- The folder C:\Users\<me>\Projects\fx-research-workspace\ exists
  with CLAUDE.md, README.md, briefings\, .gitignore.
- VS Code can open the folder without errors.
- Claude Code (`claude` in the folder's terminal) starts cleanly and
  has loaded CLAUDE.md as the project instructions.
- I'm authenticated via my plan, not an API key.

If any of those aren't right, don't say "it's working" — stop and
tell me exactly what's off.

WHAT YOU SHOULD KNOW ABOUT THIS WORKSPACE
This is the COMPANION to my dashboard repo. The dashboard is a
Streamlit website — when its AI Briefing button fires, it uses an
Anthropic API key (metered, separate bill). This workspace is the
opposite: every deep-research run dispatches sub-agents inside
Claude Code, all of which share my Claude plan auth. No API key,
no second bill. The contrast is intentional — please don't muddy it
by suggesting I add an API key here. There's no .env in this repo
for a reason.

If you hit anything unexpected — STOP and ask me. Don't silently
skip or work around anything.

Report back at each major step. Keep me in the loop.

Let's begin — please enter plan mode and tell me what's on my machine.
```

---

## Cross-references

- Sibling repo: [`exotic-fx-research-desk`](https://github.com/seanmccloskey10-cell/exotic-fx-research-desk) — companion dashboard with its own (longer) handoff prompt
