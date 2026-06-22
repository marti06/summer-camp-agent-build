# Phase 0 — Setup & orientation

**Goal:** everyone in the same known-good state, and clear on what we're building.

## Check you're ready

```bash
claude --version     # Claude Code is installed
git --version        # git is installed
```

Your Anthropic key/login is provided at the summit. Open Claude Code in this repo:

```bash
claude
```

Ask it something trivial to confirm it's alive (`what files are in this repo?`).

## The mental model (2 minutes)

- An **agent** = an LLM calling tools in a loop until the task is done. Claude Code
  *is* that loop — you don't write it, you configure it.
- A **subagent** = a markdown file in `.claude/agents/` with its own role, tools,
  and context window. The main agent can hand work to it.
- A **slash command** = a markdown file in `.claude/commands/` that gives the main
  agent a repeatable plan — including "spawn these subagents."
- **Sharing** = commit `.claude/` to the repo. Everyone who clones it gets the agent.

## What we'll build

`/build-stack "<topic>"` → research → a panel vets the links → a judge picks →
publish a curated Stacklist stack. See the diagram in `CLAUDE.md`.

## Why this task (and not a calculator)

A good agent task is **open-ended** (no fixed decision tree), **verifiable** (you
can look at the stack and judge it), and **worth the tokens**. Curating the best
links on a topic is all three. Arithmetic is none of them — that's a function call,
not an agent.

## Catch-up

You're at the start. `git checkout phase-0` is here. Next: Phase 1.
