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

5. **Save.** On approval, write the stack to `output/<slug>.md` (slug = the topic
   lowercased, hyphenated). Use this shape:

   ```
   # <name>

   <summary>

   Tags: tag1, tag2, tag3

   ## Links
   - [Title](url) — reason
   ...
   ```

   Confirm the path you wrote.

(Phase 4 will replace step 5 with publishing to Stacklist + an AI-discoverability
check, falling back to this local file when Stacklist isn't connected.)
