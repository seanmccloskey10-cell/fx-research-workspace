# HANDOFF-PROMPT.md — Paste this into Claude Code on Bura's machine

This is the prompt Bura pastes into Claude Code on his Mac mini to get the FX research workspace cloned and ready. Much lighter than the dashboard's handoff — there's nothing to install here, just clone and start. Copy everything between the lines below and paste it in one shot.

The prompt instructs the agent to:
- **Enter plan mode FIRST** — propose what it'll do before running anything
- **Recognize the OS handoff** — built/tested on Sean's Windows; Bura is on Mac
- **Read CLAUDE.md** to understand the deep-research workflow before the user asks for it
- **Confirm `claude login` (not API key)** — this workspace runs on Bura's Claude plan; an `ANTHROPIC_API_KEY` here would defeat the entire point

---

## The prompt — paste everything between the lines below

---

```
Hi — I'm Bura. I run a 7-person FX prop-desk based in Georgia. Sean
(my AI tutor) built me a small VS Code project he wants me to clone
to my Mac mini at home. It's not a tool to install — it's a folder I'll
talk to via Claude Code to do deep currency research on my Claude plan
(no API key, no metered calls).

I want you to clone this for me:

    https://github.com/seanmccloskey10-cell/fx-research-workspace

It's literally just a folder with a CLAUDE.md and a README.md inside.
There's nothing to build, nothing to install (assuming I already have
VS Code, Claude Code, and Git on my machine — which I should, since I
just installed the companion dashboard repo). Setup should take 2
minutes.

OS HANDOFF — IMPORTANT
Sean tested this on Windows 11. I'm on macOS (Mac mini). The CLAUDE.md
in the repo doesn't have any OS-specific code, so the workspace itself
is OS-agnostic. But the way you (the agent) interact with the file
system might differ — use macOS path conventions (~/Projects, forward
slashes) and macOS-native commands where it matters.

I'll say "go" once when you ask. Don't ask again per command.

Please follow this flow:

1. ENTER PLAN MODE FIRST. Tell me:
   - Whether I already have VS Code, Claude Code, and Git installed
     (run version checks; report what you find)
   - What you propose to do
   Don't start running anything until I say "go".

2. If VS Code or Claude Code or Git are missing, STOP and tell me. I
   should already have all three (I just set up the companion
   dashboard repo, exotic-fx-research-desk). If any are missing,
   that means the dashboard setup didn't complete — I'd rather fix
   that first.

3. Verify I'm logged into Claude Code via `claude login` (uses my
   Claude plan), NOT an API key. Run `claude --version` or check the
   auth status however you can. If I'm somehow on an API key
   instead of my plan, STOP and tell me — using an API key here
   would defeat the entire point of this workspace.

4. Clone the repo into ~/Projects/fx-research-workspace.

5. Read README.md and CLAUDE.md end-to-end. CLAUDE.md is the agent
   guide for this workspace — it explains the natural-language
   triggers I'll use ("do deep research on X", "use 5 agents in
   parallel"), the 5-angle decomposition default, and the briefing
   template you'll write to. Read it ALL before I ask anything.

6. Open the folder in VS Code.

7. Stop. Don't dispatch any sub-agents proactively. The workspace is
   ready when the folder exists, the docs are read, and Claude Code
   is running in the folder. I'll trigger my first deep research
   when I'm ready (probably the Vietnamese dong).

WHAT "DONE" LOOKS LIKE — tell me ONLY when you've verified ALL of these:
- The folder ~/Projects/fx-research-workspace/ exists with CLAUDE.md,
  README.md, briefings/, .gitignore.
- VS Code can open the folder without errors.
- Claude Code (`claude` in the folder's terminal) starts cleanly and
  has loaded CLAUDE.md as the project instructions.
- I'm authenticated via my plan, not an API key.

If any of those aren't right, don't say "it's working" — stop and tell me
exactly what's off.

WHAT YOU SHOULD KNOW ABOUT THIS WORKSPACE
This is the COMPANION to my dashboard repo. The dashboard is a Streamlit
website — when its AI Briefing button fires, it uses an Anthropic API
key (metered, separate bill). This workspace is the opposite: every
deep-research run dispatches sub-agents inside Claude Code, all of which
share my Claude plan auth. No API key, no second bill. Sean is using the
contrast as a teaching point — please don't muddy it by suggesting I
add an API key here. There's no .env in this repo for a reason.

If you hit anything unexpected — STOP and ask me. Don't silently skip
or work around anything.

Report back at each major step. Keep me in the loop.

Let's begin — please enter plan mode and tell me what's on my machine.
```

---

## If you (Sean) ever need to test this on Windows

The workspace itself is OS-agnostic. The clone path becomes `%USERPROFILE%\Projects\fx-research-workspace` instead of `~/Projects/fx-research-workspace`. Otherwise the prompt works as-is — there are no OS-specific install steps because there's nothing to install.

## Why this prompt is shorter than the dashboard's

Three reasons:

1. **No installs.** The dashboard needs Python, dependencies, a venv, a Streamlit process. This workspace needs none of that — just a clone.
2. **No setup gates.** The dashboard has an "is data flowing?" smoke test. This workspace has nothing to smoke-test until Bura actually triggers a deep research run.
3. **The agent's behaviour is what matters here, not the install dance.** The CLAUDE.md inside the repo carries the natural-language triggers, the dispatch flow, the briefing template. The handoff prompt's only job is to get the agent to read it before Bura's first request.

## Cross-references

- Sibling repo: [`exotic-fx-research-desk`](https://github.com/seanmccloskey10-cell/exotic-fx-research-desk) — companion dashboard with its own (longer) handoff prompt
- Pattern source: [Sean's vault — student tool handoff prompt template](https://github.com/seanmccloskey10-cell/Obsidian) (private)
