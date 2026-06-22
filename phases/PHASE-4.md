# Phase 4 — Publish to Stacklist (the product moment)

**Goal:** turn the judge's selection into a real, published, AI-discoverable
[Stacklist](https://stacklist.app) stack — and show the big idea: **an agent's
tools can be your own product's MCP server.**

## What we added

- `.claude/agents/stack-publisher.md` — takes the approved stack and publishes it.
  Its `tools` are just `Write, WebFetch`, so **out of the box it writes
  `output/<slug>.md`** and the whole workshop runs with no account.
- `/build-stack` step 5 now delegates to `stack-publisher` instead of writing inline.

## Make it publish for real (opt-in)

Two small steps turn the local fallback into a live publish:

1. **Connect the Stacklist MCP server** to Claude Code (project-scoped, via
   `.mcp.json`, so the whole team inherits it). Use Stacklist's MCP setup for the
   URL + auth.
2. **Let the publisher use it.** Add the Stacklist tools to the publisher's
   allowlist — edit the frontmatter in `stack-publisher.md`:

   ```yaml
   tools: Write, WebFetch, mcp__stacklist__create_stack, mcp__stacklist__add_cards,
          mcp__stacklist__auto_tag_cards, mcp__stacklist__generate_summary,
          mcp__stacklist__check_ai_discoverability
   ```
   (Match the exact tool names your registered server exposes.)

Now the same `/build-stack` run ends with a real stack URL and a discoverability
score instead of a local file. The agent didn't change — you just widened its
blast radius to include your product. That allowlist line *is* the security model.

## Try it

```
> /build-stack "the practical starting kit for web accessibility"
```

- No Stacklist connected → you get `output/the-practical-starting-kit-...md`.
- Stacklist connected + tools allowed → you get a published stack + discoverability
  report. (This is the on-stage demo.)

## Note for the workshop

If attendees don't have Stacklist access, they run the local-file path (fully
hands-on); the facilitator runs the connected path for the product showcase. Same
agent, two endings.

## Catch-up

`git checkout phase-4`. Next: Phase 5 — ship it to the team + run it in CI.
