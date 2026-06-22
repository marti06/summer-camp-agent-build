---
description: Curate a topic into a ranked, reasoned stack — research, panel review, judge.
argument-hint: "<topic>"
---

The user wants to build a curated stack on this topic:

**$ARGUMENTS**

Run this orchestration. You are the lead agent and, at the end, the judge.

1. **Research.** Launch the `link-researcher` subagent on the topic. It returns a
   candidate list (`- [Title](url) — reason`).

2. **Review — in parallel.** Launch all THREE reviewers in a single step so they
   run concurrently, each given the topic and the full candidate list:
   `reviewer-credibility`, `reviewer-freshness`, `reviewer-fit`.
   Each returns a `score | URL | reason` line per candidate plus a `DROP:` line.

3. **Judge.** This is your job, not a subagent's. Combine the three score sets:
   - Sum each link's three scores. Honour `DROP` votes — a link dropped by two or
     more reviewers is out.
   - Remove near-duplicates (keep the stronger one).
   - Select the best **8–12** links. Quality over quantity.
   - Where the reviewers sharply disagreed on a link, make a call and say so in
     one line — don't hide the tension.

4. **Propose the stack.** Present:
   - a **name** (specific, front-loaded, 30–48 chars),
   - a **one-paragraph summary** a stranger could understand,
   - **3–6 tags**,
   - the **final ranked list** with each link's one-line reason, and a short note
     on any contested picks.
   Ask the user for a quick OK or edits before saving.

5. **Publish.** On approval, launch the `stack-publisher` subagent with the approved
   name, summary, tags, and ranked links. It publishes to Stacklist (via the
   Stacklist MCP) when connected — and reports the stack URL and the
   AI-discoverability check — or writes `output/<slug>.md` when it isn't. Relay
   exactly what it reports back; don't claim a publish that didn't happen.
