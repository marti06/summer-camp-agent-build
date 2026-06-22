# Phase 5 — Deploy & share

**Goal:** the whole reason we built it in Claude Code instead of a script — ship it
to the team with `git`, and run it unattended in CI. Nobody installs anything.

## Share it with the team (this is "deploy")

Everything the agent needs is already in `.claude/`. So:

```bash
git add .claude CLAUDE.md
git commit -m "Add the /build-stack agent"
git push
```

A teammate:

```bash
git pull
claude
> /build-stack "self-hosting your analytics"
```

They have the full agent — researcher, panel, judge, publisher — with zero setup.
That's the payoff: **the repo *is* the distribution mechanism.** Update an agent,
commit, and the whole team gets the new behaviour on their next pull.

Scope recap:
- `.claude/` in the **repo** = shared with everyone who clones it (what we used).
- `~/.claude/` = your personal agents, not shared.

## Run it headless (CI)

`.github/workflows/weekly-stack.yml` runs the same command with `claude -p` (print
mode) on a schedule — e.g. a fresh "trending" stack every Monday. Add
`ANTHROPIC_API_KEY` as a repo secret; add your Stacklist MCP secrets too if you
want CI to publish for real. Trigger it manually from the Actions tab to test.

Same agent, three ways to run it: interactive (`claude`), headless (`claude -p`),
scheduled (CI). You wrote it once.

## When to reach for the SDK instead

`claude -p` is perfect for scripts and CI. If you need to *embed* the agent in a
product — structured outputs, custom tool callbacks, hosted as a service — that's
the **Claude Agent SDK** (Python/TypeScript). Same idea, programmatic control.

## You're done

`main` is the finished workshop. You built a real, reusable, team-shared agent in
Claude Code, gave it your product's tools, orchestrated a panel + judge, and
deployed it by committing it. `git checkout phase-5` is here.
