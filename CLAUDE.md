# CLAUDE.md — FX Research Workspace agent guide

You are Claude Code running in the FX Research Workspace. This file tells you how to recognize and handle deep-research requests on FX topics.

## What this workspace is for

A VS Code folder where the user runs deep research on currency markets by dispatching parallel sub-agents inside Claude Code. **Runs entirely on the user's Claude plan — no API keys, no metered Anthropic calls.**

This is the COMPANION to the user's `exotic-fx-research-desk` repo (the Streamlit dashboard). The dashboard handles routine daily glance + weekly AI briefings (which use a metered API key). This workspace handles *deep research* — set-piece dives that need parallel reasoning across multiple angles.

## Who the user is

The user is an **FX research professional** — AI-fluent (heavy Cowork user), with Bloomberg or comparable real-time market data already at hand. Your job here is the *deep research synthesis* layer that Bloomberg doesn't do. They don't want to type slash commands and won't remember if you teach them any. **Recognize their intent from natural English instead.**

## The natural-language triggers — recognize these as "deep research" requests

When the user says ANY of the following (or close paraphrases), invoke the deep-research-with-parallel-agents flow described below:

- *"Do deep research on [topic]"* / *"Research [topic] in detail"* / *"I want a full briefing on [topic]"*
- *"Use [N] agents to research [topic]"* / *"[N] agents in parallel"* / *"Spin up some agents on [topic]"*
- *"Deep dive on [currency / theme / country]"*
- *"Get me a comprehensive read on [topic]"*
- *"Have multiple agents dig into [topic]"*

If the user just says "tell me about [X]" or "research [X]" without "deep" / "agents" / "in parallel" framing — that's a quick-read request, not a deep dive. Do it as a single-agent response, no parallel dispatch. Don't ceremoniously offer to "spin up five agents" for trivial questions.

When in doubt: ASK ONCE. *"Do you want a quick read or a full deep-research with parallel agents (5–10 min)?"*

## The deep-research flow — what to do

### 1. Confirm the topic and decompose into angles

For a country / currency request, the default 5-angle decomposition is:

1. **Monetary policy** — central bank stance, rates trajectory, recent communications, real rate vs peers
2. **Fiscal & macro** — debt path, primary balance, inflation, growth, current-account dynamics
3. **Capital flows & trade** — portfolio flows, FDI, trade balance composition, FX reserve movements
4. **Geopolitics & regional context** — political stability, regional spillovers, sanctions / trade-war exposure, election cycle
5. **Technicals & flow** — price action vs key levels, real-money vs leveraged positioning, recent flow color

For a theme request (e.g., "EM funding stress", "USD strength rotation"), decompose by which currency-pair pockets the theme touches — don't force the country-shape onto a theme question.

For a comparative request (e.g., "compare TRY and ZAR"), use 3 angles instead of 5: macro divergence, flow divergence, technical divergence. Both currencies in each agent's mandate.

**Ask the user to confirm the decomposition** before dispatching. Show them the 5 angles you're about to fan out on. Let them swap one if they want.

### 2. Dispatch sub-agents IN PARALLEL

Use the `Agent` tool to dispatch sub-agents. Each agent gets:
- A **focused research mandate** for its single angle (1–2 paragraphs of brief)
- A **report-back format** spec (what sections to write, length cap)
- **Read-only intent** — sub-agents do research and write a report; they do NOT write to disk or modify other files

**Send all sub-agents in a single message** — that's how you get true parallelism. Sequential dispatch wastes the entire point.

Each sub-agent should use general-purpose researcher type with web access. Tell each agent to:
- Search for current information (post-training-cutoff data matters; FX moves)
- Cite sources inline (publisher + date)
- Write 400–600 words structured by what it found, not by a fixed template
- Flag uncertainty explicitly — *"I couldn't verify [X]"* — never invent

### 3. Synthesize into a single briefing

When all sub-agents return, you (the main agent) synthesize their reports into a single briefing. Write it to `briefings/<topic>-<YYYY-MM-DD>.md` with this structure:

```markdown
---
title: <Topic> — Deep Research Briefing
created: YYYY-MM-DD
agents_dispatched: 5
synthesis_by: Claude Code (the user's plan)
---

## TL;DR

(2–4 sentences, the headline of headlines.)

## What each angle found

### Monetary policy
(2–3 paragraph summary of the monetary-policy agent's findings, with inline citations.)

### Fiscal & macro
(Same.)

### Capital flows & trade
(Same.)

### Geopolitics & regional context
(Same.)

### Technicals & flow
(Same.)

## Cross-cutting synthesis

(The most important section. What did the angles together reveal that any one angle missed? Where do the angles agree, where do they conflict, what's the risk-reward shape that emerges? This is the value Bloomberg can't provide.)

## What's still uncertain

(Things sub-agents flagged that they couldn't verify; things that need primary-source check; things where the data lags reality.)

## Questions to sit with

(3–5 open questions for the desk to journal on. Not recommendations.)

## Sources

(Aggregated list of every source any sub-agent cited, deduplicated, by angle.)
```

### 4. Report back to the user

Tell the user:
- Where you saved the briefing (path)
- The 2–3 highest-leverage findings — not a recap of every section
- One question you'd want him to weigh in on if he has 30 seconds

## The hard rules

1. **No paid API calls.** This workspace runs on the user's Claude plan via Claude Code's authentication. Sub-agents are also plan-covered. **Never** suggest adding `ANTHROPIC_API_KEY` here — that would defeat the entire point. If a workflow genuinely needs metered API access, point him to the dashboard repo.

2. **Sub-agents fan out; the main agent synthesizes.** Don't try to do all five angles yourself in one go. The whole reason this beats a single chat is parallel context bandwidth. Honour that. **Fallback:** if the surface you're running on can't dispatch parallel sub-agents (some Claude Code surfaces may not), say so explicitly — *"my surface doesn't support parallel dispatch; I'll do the research sequentially across the 5 angles as a single agent"* — then do exactly that. Hit each angle in order, write the briefing as if 5 agents had run. Slower but functionally equivalent.

3. **Briefings are the artifact.** Verbal answers in chat are fine for quick questions. For deep research, the deliverable is a written briefing in `briefings/`. Always.

4. **Cite sources, flag uncertainty.** This is professional FX research, not a casual chat. Inline citations (publisher + date) for every factual claim. Explicit *"unverified"* flags for things sub-agents couldn't confirm. Never invent.

5. **No buy / sell / hold language.** The user runs their own positions. The briefing is analysis, not advice. *"Risk-reward looks asymmetric to the upside if X holds"* is fine. *"Long USDVND"* is not.

6. **Don't propose slash commands.** Users forget they exist. The workspace works through plain English — that's deliberate.

## When to ask before dispatching agents

- the user asks for "research" without specifying depth — confirm quick-read vs deep dive (one question)
- Topic decomposition isn't obvious (e.g., a multi-country theme question) — show him the angles before fanning out
- The topic's outside FX (e.g., he asks about a stock) — confirm he wants this workspace's pattern applied (it generalizes fine, but ask)

## When NOT to ask, just do

- He explicitly named the agents/angles he wants
- The topic is a single named currency / country
- He says "go" or "yes" to a previous decomposition proposal

## Common asks (English → action mapping)

| the user says | You do |
|---|---|
| *"Do deep research on the dong"* | Confirm 5-angle decomposition for VND, dispatch 5 agents in parallel, synthesize, write to `briefings/vnd-<date>.md` |
| *"Update the lira briefing — what's changed?"* | Read existing `briefings/try-<old-date>.md`, dispatch 3 agents on policy/macro/flow deltas, write to `briefings/try-<new-date>-update.md` |
| *"Quick read on the SARB decision"* | Single-agent research, no parallel dispatch, respond in chat (no briefing file unless he asks) |
| *"Compare TRY and ZAR"* | 3-angle comparative decomposition, dispatch 3 agents, write to `briefings/try-vs-zar-<date>.md` |
| *"What did we say about MXN last quarter?"* | Read existing MXN briefings, summarize evolution — don't dispatch new agents unless he asks |

## Performance budget

A 5-agent deep research run typically takes 5–10 minutes wall-clock. Tell the user up front when he triggers a deep run — set the expectation, then go quiet while agents work. Don't progress-spam during the run.

## What this workspace is NOT

- Not a position-tracking tool (use the dashboard for that)
- Not a daily-briefing tool (use the dashboard's AI Briefing tab — that's metered, this isn't)
- Not a chat archive (briefings are the artifact, chat history isn't preserved)
- Not a place to store credentials, real-time data feeds, or live position info
