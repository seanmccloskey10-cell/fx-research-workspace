# FX Research Workspace

A VS Code project for deep research on currency markets, powered by parallel sub-agents inside Claude Code. **Runs on your Claude plan — no API key, no second bill.**

This is a companion repo to [`exotic-fx-research-desk`](https://github.com/seanmccloskey10-cell/exotic-fx-research-desk) — the dashboard. They have different jobs:

| | **`exotic-fx-research-desk`** (the dashboard) | **`fx-research-workspace`** (this repo) |
|---|---|---|
| **What it is** | Streamlit web app — live FX prices, charts, AI Briefing tab | A VS Code folder you talk to via Claude Code |
| **Surface** | Browser at `localhost:8501` | The Claude Code chat in VS Code |
| **AI calls** | Optional Anthropic API key (metered, you pay per token) | Your existing Claude plan (no second bill) |
| **Best for** | Daily glance at watchlist, weekly AI briefing on the same pairs | Deep-dive research on a specific currency, market theme, or country |
| **What's saved** | Live data + cached briefings under `briefings/` (gitignored) | Long-form research briefings under `briefings/` (committed) |

## What this workspace does

You open this folder in VS Code, run `claude`, and ask in plain English:

- *"Do deep research on Vietnamese currency markets — get five agents to work in parallel."*
- *"I want a full briefing on Turkish lira: monetary policy, fiscal trajectory, capital flows, geopolitics, and trade. Five angles, five agents, then synthesize."*
- *"Research the Brazilian real outlook for the next quarter."*

Claude (the agent reading this folder's `CLAUDE.md`) recognizes the request, dispatches several sub-agents in parallel — each with its own research mandate — and synthesizes their findings into a single briefing saved to `briefings/<currency-or-topic>-<date>.md`.

**No slash commands. No API key. Just ask.**

## Why this works without an API key

This is the trick worth understanding:

- **Your Claude plan covers exactly three surfaces**: Claude.ai chat, Claude Cowork (a tab in the same app), and Claude Code (the CLI you're running in VS Code right now).
- **All sub-agents Claude Code dispatches share that same plan auth.** When Claude spins up five parallel research agents from inside this workspace, every one of them runs on your subscription. No separate bills.
- **Compare to the dashboard repo:** that's a Streamlit *website* you're running. Websites can't log in to your subscription — there's no mechanism for it. So when the dashboard's "Generate Briefing" button calls Claude, it has to use a metered API key.

Same Claude. Two completely different bill structures, depending on *where* the call happens.

## Setup (~5 minutes)

You need: VS Code, Claude Code CLI, Git. If you cloned the dashboard repo first, you have all three already.

```bash
# Clone into your Projects folder
mkdir -p ~/Projects && cd ~/Projects
git clone https://github.com/seanmccloskey10-cell/fx-research-workspace
cd fx-research-workspace

# Open in VS Code
code .

# Inside VS Code's terminal:
claude login   # if you haven't already — uses your plan, NOT an API key
claude         # start Claude Code
```

That's it. There's nothing to install, nothing to build. Claude reads `CLAUDE.md` automatically and knows the workspace's purpose.

## Your first deep research

In the Claude Code chat, try:

> *"I want deep research on the Vietnamese dong. Five agents in parallel — one on monetary policy, one on fiscal & macro, one on capital flows & trade, one on geopolitics & regional context, one on technicals & flow. Then synthesize."*

Claude will:
1. Dispatch five sub-agents in parallel (you'll see them spin up as separate research tasks)
2. Each agent does focused research on its angle
3. Claude collects all five findings and synthesizes a single briefing
4. The briefing is saved to `briefings/vnd-2026-04-26.md` (or whatever date it is)

Takes 5–10 minutes for the agents to finish. You can do something else while they work — the synthesis is the wow moment.

## What "deep research" means here

Sub-agents inside Claude Code can use:
- **Web search and fetch** to read current sources
- **Their full thinking budget** to reason through what they read
- **Each their own clean context** — no token contamination from the main conversation

Each agent produces a focused report on its assigned angle. The main agent (the one you're talking to) reads all five reports and writes the synthesis. The synthesis is what hits `briefings/`.

This is significantly more powerful than a single chat asking "tell me about VND." A single chat fights for context bandwidth across all the angles at once and degrades. Five focused agents in parallel each get full bandwidth on their narrow piece, then the synthesis brings them together.

## The briefings folder

Anything Claude writes for you lands in `briefings/`. It's committed by default — you'll build a personal research archive over time. If you want a briefing kept private, tell Claude to add it to `.gitignore` after writing.

## Common asks

| You say | Claude does |
|---|---|
| *"Deep research on [currency]"* | 5 parallel agents on the standard angles → synthesis briefing |
| *"Research [theme] across these pairs"* | Theme-shaped research instead of country-shaped |
| *"Update the [currency] briefing — what's changed in the last month?"* | Reads existing briefing, dispatches agents to find what's new, writes a delta |
| *"Compare [X] and [Y]"* | Two-currency comparative research |
| *"Just give me a quick read on [topic] — don't dispatch agents"* | Single-agent research, no parallelism, faster turnaround |

Plain English is the interface. If you're not sure how to phrase a request, just say what you want — Claude figures it out.

## What this is NOT

- Not a replacement for Bloomberg or your real-time data feeds — this is a deep-research and synthesis layer
- Not a position-tracking tool (use the dashboard repo for that, or your existing tools)
- Not a daily-briefing tool — for that, use the dashboard's AI Briefing tab. This workspace is for set-piece deep dives, not routine pulses.
- Not a place to store credentials or live API keys (no `.env` here — there's nothing to authenticate against)

## Cross-reference

- Dashboard repo: <https://github.com/seanmccloskey10-cell/exotic-fx-research-desk>
- The two repos work well together: dashboard for daily glance + routine briefings, workspace for deep dives that don't fit a daily rhythm.
