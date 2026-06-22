# Facilitator runbook — Build a team agent in Claude Code (2.5h)

**Audience:** developers who already use Claude Code and Git. **Outcome:** everyone
leaves with `/build-stack` committed in a repo — a real, reusable, team-shared
agent — plus the knowledge to build their own.

**Spine:** what makes a real agent task → one subagent → a panel → the orchestrator
+ judge → publish via your product's MCP → ship it to the team + CI.

**The load-bearing message, repeated:** an agent in Claude Code is config you
commit, not a script. Multi-agent is composition. Deploy = `git commit`.

The phase tags ARE your safety net: anyone behind runs `git checkout phase-N` and
rejoins instantly.

---

## Timing at a glance

| Time | Block | Phase |
|---|---|---|
| 0:00–0:10 | Welcome + setup check + show the end state | — |
| 0:10–0:25 | Concept: what makes a real agent task; subagents/commands/sharing | 0 |
| 0:25–0:50 | Build the first subagent | 1 |
| 0:50–1:20 | The review panel (+ start the orchestrator) | 2 → 3 |
| 1:20–1:30 | Break | — |
| 1:30–1:55 | Finish the orchestrator + judge — first full run | 3 |
| 1:55–2:20 | Publish to Stacklist + the deploy/CI payoff | 4 → 5 |
| 2:20–2:30 | Best practices + Q&A | — |

---

## 0:00–0:10 — Welcome + the end state
- One line: *you'll leave with an agent your whole team can use — committed, not a
  script on your laptop.*
- Triage setup (key/login works, `claude --version`, repo cloned). The phase tags
  rescue anyone who's stuck — say so now so nobody panics.
- **Show the finish (45s):** `/build-stack "best resources for shipping AI agents in
  2026"` on your machine, wired to Stacklist. Let them see the published stack.

## 0:10–0:25 — Concept (Phase 0)
- A good agent task is open-ended + verifiable + worth the tokens. Curation is;
  arithmetic isn't (head off "why not a calculator").
- Claude Code *is* the agent loop — you configure it, you don't write it.
- Three primitives: **subagent** (`.claude/agents/`), **slash command**
  (`.claude/commands/`), **sharing** (commit `.claude/`).
- War story: how Scout works at Stacklist — judge + panel — and why a panel beats
  one model on a judgment call. This is what we're about to build, simplified.

## 0:25–0:50 — First subagent (Phase 1)
- Everyone opens `.claude/agents/link-researcher.md`. Walk the frontmatter:
  `description` = how the lead delegates; `tools` = blast radius.
- Run it live: *"Use the link-researcher subagent to find candidates for <topic>."*
- Point out the isolated context — the main chat stayed clean.
- **CHECKPOINT:** everyone gets a candidate list back from the subagent.

## 0:50–1:20 — The panel (Phase 2 → start Phase 3)
- Open the three reviewers. Hammer: each owns ONE lens, same model (cheap, parallel),
  same output shape. Independence is the point.
- Run all three on a candidate list. Then introduce `/build-stack` and let them read
  the command body — the plan the lead follows.

## 1:20–1:30 — Break

## 1:30–1:55 — Orchestrator + judge, full run (Phase 3)
- Walk `/build-stack`: research → 3 reviewers **in parallel** → the lead **as judge**.
- **THE CHECKPOINT THAT MATTERS:** crowd-source a topic, run `/build-stack`, watch
  research → parallel review → ranked verdict → saved stack. *You typed one line; a
  panel produced a reasoned artifact you never hard-coded.*
- Exercise: add a 4th reviewer; watch the verdict shift. Behaviour lives in roles.

## 1:55–2:20 — Publish + deploy (Phase 4 → 5)
- **Product moment (Phase 4):** show the publisher. Default = local file (works for
  everyone). Then the opt-in: connect Stacklist MCP + add its tools to the allowlist
  → the same run publishes a real, discoverable stack. *An agent's tools can be your
  own product.* Run it live on your account.
- **The payoff (Phase 5):** `git commit` the `.claude/` dir → a teammate pulls and
  runs `/build-stack` with zero setup. Show `weekly-stack.yml` — the same agent
  headless in CI. *Wrote it once; runs interactive, headless, scheduled.*

## 2:20–2:30 — Best practices + Q&A
- Four that bite: tool sprawl; context rot; vague `description`s (the delegation
  prompt); cost — orchestration multiplies tokens, so tier your models (Haiku
  panel, stronger judge) and don't loop forever.
- Where next: give panelists more tools, the Agent SDK for embedding, agent teams
  for inter-agent debate.

---

## Fallbacks
- **Behind?** `git stash && git checkout phase-N` — the whole reason for the phase
  tags. Use them shamelessly; nobody falls off.
- **No Stacklist access for attendees:** they run the local-file path (fully
  hands-on); you run the connected path for the showcase. Same agent.
- **Running behind:** protect the two checkpoints (subagent returns a list; full
  `/build-stack` returns a stack). Compress the panel exercise and the CI bit first.
- **API/network flakey:** the concept + file walkthroughs work offline; demo the
  live runs once it's back.
- **Subagent didn't get delegated to:** the `description` is the delegation prompt —
  tighten it, or name the subagent explicitly in the request.

## Cost
- Standard per-token billing. One `/build-stack` run ≈ 1 researcher + 3 Haiku
  reviewers + judge + publisher — cents per run on the tiered models. Fine on the
  summit key; just don't leave a room looping the judge on Opus.

## Accuracy note
- Claude Code's exact frontmatter fields and `claude -p` flags can shift between
  versions. Do a full dry run on the venue machine with the provided key before the
  session, and adjust `weekly-stack.yml` flags / the publisher allowlist to match
  your installed version.
