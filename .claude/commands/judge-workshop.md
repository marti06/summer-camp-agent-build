---
description: Judge submitted workshop stacks (integrity, curation, craft) and rank a winner.
argument-hint: "<pasted submissions, one per line: name - stack URL - topic>"
---

The facilitator has collected workshop stack submissions to judge:

**$ARGUMENTS**

Run this orchestration. You are the lead agent and, at the end, the judge.

1. **Parse.** Read the submissions, one per line. Each line has, in some
   order, a name or handle and a Stacklist stack URL, and usually a topic. A
   bare URL with no name or topic is fine too, infer what you can from the
   stack itself.

2. **Judge each stack, in parallel.** For EVERY submitted stack, launch all
   THREE judges in a single step so they run concurrently: `judge-integrity`,
   `judge-curation`, `judge-craft`, each given that stack's URL and topic.
   Judge different stacks concurrently too, don't go one at a time if you
   don't have to. (If there are more than ~15 submissions, batch them in
   groups so you don't overload a single turn.)

   **Don't assume first-try compliance.** A judge may ignore the required
   output format, or wander into another judge's lane. Before using a
   result, check it actually has a `SCORE: <1-5>` line. If it doesn't, or if
   it references another judge's verdict, send it back once with the exact
   format required, then use that reply. Never invent a score yourself, and
   never trust a judge's claim about what another judge found, only trust
   what that other judge told you directly.

3. **Rank.** This is your job, not a subagent's:
   - Sum each stack's three scores (max 15).
   - **Confirmed-dead links cap the ceiling:** a stack with any card the
     integrity judge lists under `DEAD` cannot take 1st place, regardless of
     its total. State plainly if this changed the outcome.
   - **`UNVERIFIED` is not `DEAD`.** Don't penalize a stack for links the
     judge couldn't confirm either way. But if a stack's placement, especially
     1st, hinges on the outcome (would the ranking change if an unverified
     link turned out dead?), fetch that one link yourself before finalizing.
     Trust but verify, the same rule the workshop's own reviewers live by.
   - Break ties on curation score, then craft score.
   - Produce a full ranked leaderboard, not just a single winner: name/handle,
     the three scores, the total, and one line on why it landed there.

4. **Announce.** Present:
   - the **leaderboard**, ranked, with each entry's three scores and total,
   - the **winner**, with a two-sentence case for why (quote the strongest
     judge note),
   - **one honest callout** if the winner had any weakness anyway, don't hide
     the tension, the same rule the panel used on itself all workshop.
   Ask the facilitator to eyeball the winning stack before announcing it to
   the room, this ranks candidates, it doesn't replace a human's final call.
