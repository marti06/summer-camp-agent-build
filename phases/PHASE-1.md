# Phase 1 — Your first subagent

**Goal:** create one real subagent and watch Claude Code hand work to it.

A subagent is just a markdown file: YAML frontmatter (who it is, what tools it may
use, which model) + a system prompt (how it behaves). That's the whole format.

## What we added

`.claude/agents/link-researcher.md`:

```yaml
---
name: link-researcher
description: Finds strong candidate links for a topic... Use this first.
tools: WebSearch, WebFetch     # this agent can ONLY search & fetch — nothing else
model: sonnet
---
You are a research specialist...
```

Two things to notice:
- **`description`** is how the main agent decides to delegate. Write it like a job
  posting — when should this agent be used, and what does it hand back?
- **`tools`** is the agent's blast radius. The researcher can search and fetch; it
  can't write files or run commands. Least privilege, by default.

## Try it

In Claude Code:

```
> Use the link-researcher subagent to find candidates for
  "learning Rust coming from TypeScript".
```

You should see Claude spawn the subagent, watch it run its own searches in its own
context window, and hand back a clean candidate list. Note that *your* main context
stayed clean — that isolation is the point of a subagent.

## Exercise

Tighten the `description` so it's unambiguous, then ask a vague question and see if
Claude delegates correctly. The description is a prompt — vague in, vague out.

## Catch-up

`git checkout phase-1`. Next: Phase 2 — give the researcher's output to a panel.
