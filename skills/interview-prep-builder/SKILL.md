---
name: interview-prep-builder
description: >
  Builds interview prep (likely questions, answer structure, personalized talking points) for an
  upcoming interview, screen, or call for a specific role. Invoke proactively whenever an
  interview, recruiter screen, hiring-manager call, or team round is mentioned as scheduled or
  upcoming — don't wait to be asked for "prep," treat a mentioned interview date as the trigger.
  Also use when asked directly for interview questions, talking points, or STAR stories for a
  role. Pairs with the job-fit-analysis skill, which should run first if the fit for this specific
  role hasn't already been established.
---

# Interview Prep Builder

Part of the [Job Search Toolkit](../../README.md).

## Step 1 — read your source-of-truth file fresh

Same file as job-fit-analysis: your filled-in `career_knowledge_base_template.yaml`. Read it fresh every
time, not from memory of an earlier session — corrections land in this file as you catch them
(a misattributed "led" vs. "participated in," a dropped collaborator credit, a corrected
ownership story), and prep built on a stale understanding can put an inaccurate claim in your own
mouth right before you say it out loud to an interviewer.

## Step 2 — generate questions grounded in the actual JD

Pull the real JD (fetch/verify it the same way job-fit-analysis does, if that hasn't already
happened this conversation). For each likely question, produce:

- **What it's actually testing** — the underlying concern behind the question, not just a label.
- **Answer structure** — a shape (e.g. situation → the no-authority problem → the specific system
  built → the adoption result), not a script to memorize word for word.
- **A personalized talking point sourced only from your verified facts** — if the real experience
  is a genuine stretch or an honest gap, say so plainly and suggest naming the gap directly rather
  than papering over it, then bridging it with the closest real evidence — that's the same
  honesty principle the rest of this toolkit runs on, applied out loud in the room.
- **A common mistake to avoid** specific to a known real tendency on this topic (e.g. overstating
  solo ownership of collaborative work), not a generic interview tip.

## Step 3 — output format: short cue bullets, not paragraphs

Compress each talking point into a short cue you can glance at, not a full written-out paragraph
to memorize or read from. A prep doc full of paragraphs isn't actually "interview ready" yet — it
needs a compression pass, turning every story into a cue, before it counts as done. Do that
compression as part of building the prep; don't treat it as a separate step someone has to
remember to ask for.

## Step 4 — never invent a personalized answer beyond what's verified

If a likely question doesn't have real, verified supporting experience behind it, say so directly
instead of writing a plausible-sounding sample answer. The honest answer — "this is a real gap,
here's the closest true story to bridge it with" — holds up better in the room than a fabricated
one that falls apart under a follow-up question.


## Clarify unconfirmed facts as you go

If the posting or application depends on anything marked UNCONFIRMED in the user's files (a number,
a date, a skill level, a title, who owned a piece of work), stop and ask only about that item
before you tier, draft or advise. Say which item, why this application needs it, and offer
"still not sure" as an answer. After they answer, update the one field in
`career_knowledge_base.yaml` with a dated CONFIRMED note, then update the matching line in
`llm_context.md`, then continue. If they are still unsure, leave it UNCONFIRMED and leave the claim
out of anything you write. Never fill the gap with a guess or a rounded number.
