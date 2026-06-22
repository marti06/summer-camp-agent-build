# Phase 3 — The orchestrator + the judge

**Goal:** one command that runs the whole pipeline — research → parallel review →
judge → a saved stack. This is the "Scout" move: fan out, then synthesize.

## What we added

`.claude/commands/build-stack.md` → the `/build-stack` slash command. Its body is
a plan the lead agent follows:

1. Launch `link-researcher`.
2. Launch the three reviewers **in parallel** (one step, three subagents).
3. **Be the judge** — combine the scores, honour drops, kill duplicates, pick 8–12,
   and surface any disagreement instead of hiding it.
4. Propose name + summary + tags + the ranked list, and ask for an OK.
5. Save to `output/<slug>.md`.

Two design choices worth calling out:
- **The judge is the lead agent, not another subagent.** Subagents report back to
  whoever spawned them; the lead already holds all three score sets, so it's the
  natural place to synthesize. (You *could* make the judge its own subagent — try
  it as a stretch.)
- **Parallel fan-out** — launching the three reviewers in a single step runs them
  concurrently. Three opinions cost about the latency of one.

## Try it — the whole thing, one command

```
> /build-stack "best resources for shipping AI agents in 2026"
```

Watch: researcher → three reviewers at once → the judge's ranked pick with reasons
→ a saved `output/best-resources-for-shipping-ai-agents-in-2026.md`.

**This is the checkpoint that matters.** You typed one line; a panel of agents
produced a curated, reasoned artifact. You never hard-coded which links win.

## Exercise

Run the same topic twice and compare the judge's notes on contested links. Then
add a 4th reviewer (e.g. `reviewer-beginner-friendliness`) and see the verdict
shift — the behaviour lives in the roles, not the plumbing.

## Catch-up

`git checkout phase-3`. Next: Phase 4 — publish to Stacklist for real.
