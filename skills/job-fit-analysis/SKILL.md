---
name: job-fit-analysis
description: >
  Structured fit analysis for a specific job posting against your verified career facts. Invoke
  whenever a job posting, job URL, req ID, or job title enters the conversation and the question
  is some version of "how does this fit," "is this a good fit," "should I apply," or "what about
  this role" — invoke proactively even if the user doesn't name the skill by name, any time a
  specific posting comes up. Also covers side-by-side comparison when multiple postings are
  shared at once. Do NOT use for generic career-direction questions with no specific posting
  attached, and do NOT use to draft a resume/cover letter directly (that's a separate, downstream
  step once the fit is established).
---

# Job Fit Analysis

Part of the [Job Search Toolkit](../../README.md). Formalizes the fit-check the rest of the
toolkit assumes happens manually every time a posting comes up, so it happens the same rigorous
way whether or not you remember the checklist that day.

## Step 0 — read your source-of-truth file fresh

Read your filled-in `career_context_template.md` **fresh, every time** — never reconstruct facts
from an earlier conversation's summary or from a resume file found on disk. If you haven't filled
that file in yet, do that first; this skill has nothing to check a posting against without it.

## Step 1 — never analyze a pasted or summarized JD. Fetch the real one.

A job-sweep log's GOOD/STRETCH tag, a LinkedIn preview, or a third-party aggregator's summary is a
lead, not source material. Before doing anything else:

- If given a URL, fetch it. Treat any displayed location on an aggregator site with real
  suspicion — these have been observed showing an identical fake placeholder location across
  completely unrelated companies. Cross-verify location, remote status, pay, and the actual
  requirement list against the employer's own applicant tracking system directly — most companies
  run one of a small number of platforms with a fetchable JSON API (Greenhouse:
  `boards-api.greenhouse.io/v1/boards/{company}/jobs?content=true`; Lever:
  `api.lever.co/v0/postings/{company}?mode=json`; Ashby:
  `api.ashbyhq.com/posting-api/job-board/{company}`; Workday's CXS API is fetchable too, though it
  usually needs a POST request) — before trusting anything from an aggregator.
- If given only a company + title with no link, search for the live posting and verify it
  actually exists before analyzing it — a title alone circulating on a job board isn't evidence a
  role is real; stale and even entirely fabricated-sounding listings do turn up.
- If the JD can't be verified against a primary source, say so explicitly rather than analyzing
  the secondhand summary as if it were confirmed.

## Step 2 — build the fit table

Once the real JD is in hand, produce:

- **Matched requirements** — specific, named facts from `career_context_template.md` that map
  directly to specific JD requirements. Cite the actual achievement, not a generic paraphrase.
- **Real gaps** — named plainly, not softened. Distinguish a genuine capability gap from a "same
  skill, different context" reframe (built internal operational systems repeatedly but never an
  audience-facing one, say — that's a context gap, not a skill gap).
- **ATS keyword gaps** — terms the JD uses that the current resume doesn't, where the underlying
  experience already supports adding the term honestly. Never add a keyword the substance behind
  it doesn't actually support — that's exactly the overclaiming this toolkit exists to prevent.
- **Tier: GOOD / STRETCH / PASS**, using whatever framework is defined in your
  `application_log_template.md`, with the one or two reasons that actually drive the call.

## Step 3 — no false precision

Never produce a numeric score (no "73/100," no 1-10 ratings across invented categories). A
confident-sounding number implies a rigor the analysis doesn't have — there's no ground truth for
what such a score would predict, and it invites treating an unfounded number as a real signal.
Give the qualitative fit table instead; that's the actual information.

## Step 4 — location and comp verification is not optional

Confirm remote/hybrid/onsite status and pay range directly from the primary source, same as Step
1. Aggregators and third-party "AI resume tools" have been observed both misstating locations and
inflating or fabricating pay figures — verify independently rather than trusting either.

## When "why am I not getting interviews" comes up

Don't default to "your resume needs work." Check the actual application history in
`application_log_template.md` first — recruiter screens, hiring-manager rounds, or team interviews
that already happened are evidence the materials *are* working to get through the door; a dry
spell in *new matches found* is usually a market/niche-scarcity signal, not a materials-quality
one. Real structural factors worth checking before blaming the resume: whether experience sits
right at a stated threshold (e.g. "5+ years management" against real tenure of 4.5-5), how much of
the recent pipeline is honest stretch/atypical-title applications (which convert at a structurally
lower rate by design, not by flaw), and current employment status (an active "doing this work
right now" signal some hiring managers weight that a between-jobs candidate doesn't have).
