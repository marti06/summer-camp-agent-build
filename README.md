# Build a team agent in Claude Code — *Stack Builder*

A 2.5-hour, hands-on workshop. You build a real, reusable agent **inside Claude
Code** — not a script on your laptop — and **ship it to your whole team by
committing it to this repo**. Pull the repo, open Claude Code, type `/build-stack
"<topic>"`, and watch a panel of agents research, vet, and publish a curated
[Stacklist](https://stacklist.app) stack.

The point isn't the toy. The point is the pattern you'll use forever:

- An **agent** in Claude Code is a markdown file (`.claude/agents/*.md`).
- An **orchestration** is one agent fanning out to several and judging the results.
- An agent's **tools can be your own product's MCP server.**
- **Deploy = `git commit`.** Whoever clones the repo gets the agent. CI runs it headless.

---

## Prerequisites (have these before we start)

- **Claude Code** installed and working (`claude --version`). You already use it.
- **An Anthropic API key / login** — provided at the summit.
- **git** — you have it.
- That's it. No Python, no framework.

---

## The phases

We build in phases. **Each phase is a git tag** holding a complete, working state,
so nobody gets stuck:

| Phase | You build | Catch-up tag |
|---|---|---|
| 0 | Setup + orientation (you're here) | `phase-0` |
| 1 | Your first subagent — `link-researcher` | `phase-1` |
| 2 | The review panel — three perspective subagents | `phase-2` |
| 3 | The orchestrator — `/build-stack` fans out + judges | `phase-3` |
| 4 | Publish to Stacklist + AI-discoverability check | `phase-4` |
| 5 | Deploy & share — commit, teammate pulls, CI headless | `phase-5` |

Walkthrough for each phase is in `phases/PHASE-N.md`. `main` is the finished
workshop.

### If you fall behind

Each phase starts from the previous phase's finished state. To jump to a known-good
checkpoint:

```bash
git stash            # park anything unfinished
git checkout phase-2 # grab the completed Phase 2, then keep going with Phase 3
```

To follow from scratch instead of reading the finished `main`:

```bash
git checkout phase-0
```

---

## What "done" looks like

```bash
claude            # open Claude Code in this repo
> /build-stack "best resources for shipping AI agents in 2026"
```

You'll watch the researcher gather links, three reviewers score them in parallel,
the judge pick the final set, and the publisher produce a tagged, summarized stack
— in Stacklist if it's connected, otherwise as `output/<slug>.md`.

See `examples.md` for good topics to try. Facilitator notes: `FACILITATOR.md`.
