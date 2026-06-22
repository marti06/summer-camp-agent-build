# Phase 2 — The review panel

**Goal:** three subagents that each judge the candidates from a different angle.
This is the heart of the orchestration: independent perspectives beat one agent
deciding alone.

## What we added

Three reviewer subagents in `.claude/agents/`:

- `reviewer-credibility` — is the source trustworthy?
- `reviewer-freshness` — is it current?
- `reviewer-fit` — does it fit the topic and the set?

Each one:
- has the **same narrow toolset** (`WebFetch` for spot-checks) and runs on a
  **cheap, fast model** (`haiku`) — because we'll run three of them, in parallel;
- judges **only its lens** ("do not consider freshness — another reviewer owns
  that"). Narrow roles give sharper, more independent signals;
- returns the **same structured shape** (`score | URL | reason`, then a `DROP:`
  line) so the judge can combine them mechanically.

## Why three agents instead of one prompt

You *could* ask a single agent to "consider credibility, freshness, and fit." But
then the three concerns blur together in one context and one model's bias. Three
isolated agents each commit to a position; the judge sees genuine disagreement to
resolve. That independence is exactly why a panel is worth the extra calls.

## Try it (manually, for now)

Run the researcher, copy its list, then:

```
> Give this candidate list to reviewer-credibility, reviewer-freshness, and
  reviewer-fit, and show me their three score sets.
  <paste the list>
```

Next phase wires this fan-out into one command so you never paste by hand.

## Catch-up

`git checkout phase-2`. Next: Phase 3 — the orchestrator + the judge.
