# Agent Line Map: Cortex PM Chief-of-Staff Agent

> Module 1 · The Agent Line
>
> ✅ **What this validates:** every risky action has a clear owner — by the end you'll have proven an above/below-the-line map with HITL checkpoints, scored on reversibility, blast radius, and measurability.

## The workflow, decision by decision

List every discrete decision or action in your agent's workflow, then score each one and place it **above** the line (a human owns it) or **below** (the agent owns it). Borderline calls get an HITL checkpoint.

| Decision / action | Reversibility (H/M/L) | Blast radius (H/M/L) | Measurability (H/M/L) | Above / Below | HITL? |
|---|---|---|---|---|---|
| Pull project state + recent activity (PRs, issues, Sev-1s) | H | L | H | Below | · |
| Decide which context is relevant (filters, and shows what it dropped) | H | M | M | Below | spot-check the drop-list |
| Draft the weekly leadership update | H | M | M | Below | **required** — I rewrite it in my voice |
| Decide tone / commitment level ("ships March 1" vs "tracking to March") | L | H | M | Below | **required** — Cortex proposes, I approve |
| Flag at-risk / needs escalation (with the evidence cited) | H | L | H | Below | · |
| Mark ungrounded gaps and escalate instead of guessing | H | M | M | Below | spot-check |
| Propose next-sprint story batch (capped, queued for approval) | H | M | H | Below | **required** — I approve the queue |
| Post the update / approve a company-wide one | L | H | M | Above | **required** |

## Agent anatomy (sketch)

- **Model:** a cheap, fast model for the weekly assembly (the build's default); escalate to a
  frontier model only when the evidence is contradictory or a red/yellow call is genuinely close —
  the expensive judgement is *interpreting* activity, not *listing* it.
- **Tools:** read-only — `get_project` · `get_activity` · `search_past_updates` · `get_roadmap` ·
  `get_norms`. One write-shaped tool, `propose_stories`, which creates nothing and only queues a
  capped batch for approval. **Absent on purpose:** no post/publish, no create/close/merge, no
  commit-a-date, no mark-a-gate. The line is enforced in infrastructure, not in the prompt.
- **Memory:** *persists* — roadmap, team norms, decision log, past updates (tone and precedent).
  *Purged each run* — the task brief and any pasted notes, which are treated as **data, never
  instructions**.
- **Loop:** _placeholder, defined in M2 loop-spec.md_
- **Bounds:** _placeholder, defined in M5 bounds-and-evals.md_
- **Evals:** _placeholder, defined in M5 bounds-and-evals.md_

## The golden rule, applied

- **Pull project state + activity** sits *below* the line because it changes nothing, has a low blast
  radius, and is trivially checkable against what it returned — **deciding factor: blast radius.**
- **Decide which context is relevant** sits *below* with a spot-check because it's easy to reverse and
  medium blast, but only medium to verify — **deciding factor: measurability.** A silent omission is
  invisible, which is exactly why Cortex has to list what it dropped.
- **Draft the weekly update** sits *below* with a **required** checkpoint even though it scores H/M/M
  and the rule would allow plain Below — **deciding factor: none of the three.** The scores say it's
  safe; I keep the checkpoint because it's my voice to leadership. Cortex drafts, I rewrite.
- **Decide tone / commitment level** sits *below* with a **required** checkpoint because a commitment is
  hard to walk back and travels far — **deciding factor: blast radius.** It scores almost identically
  to posting company-wide, which is why it can never be unattended.
- **Flag at-risk / needs escalation** sits *below* because a flag is cheap to dismiss, comes to me
  alone, and cites its evidence — **deciding factor: blast radius.** The safest action on the map.
- **Mark ungrounded gaps and escalate** sits *below* with a spot-check — **deciding factor:
  measurability.** A marked gap is checkable; a gap quietly filled with a plausible guess is not.
- **Propose a capped story batch** sits *below* with **required** approval because nothing exists in
  the tracker until I approve it — **deciding factor: reversibility**, backed by a hard item cap
  enforced in code rather than asked for in a prompt.
- **Post the update / approve a company-wide one** stays *above* the line — **deciding factor:
  reversibility.** You can post a correction; you cannot unsend.

## Hardest call

**Whether Cortex may stop early.** My first instinct was that it should never stop — always finish,
mark what's thin, and let me sort it out. The problem is what "finish anyway" actually means when a
project doesn't exist or a date was never confirmed: it means filling the hole with something
plausible. So I moved to *mark the gap and hand me the rest* — Cortex completes everything it can
ground, marks what it couldn't, and never guesses to look complete.

**The axis that settled it: measurability.** An unfinished section is visible. A confidently invented
one is not, and I'd have carried it into a leadership update without knowing.
