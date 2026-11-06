# Job Sweep Agent — Sample Config

A template for a scheduled, recurring agent that reads your two files
(`career_context_template.md` and `application_log_template.md`, both filled in) and checks job
boards for you on its own, instead of you doing this search by hand every day.

This is written as a prompt you'd hand to a scheduled agent — if you're using Claude Code, that's
a [scheduled trigger](https://docs.claude.com) you set up to run this prompt on a cron schedule
against a git repo it can read/write. If you're using something else, adapt the structure below
to whatever recurring-agent mechanism you have; the structure is the reusable part, not the
specific platform.

Fill in every `[bracketed]` section. Delete this instructions block once you've read it.

---

## HOW TO SET THIS UP (read once, then delete)

1. **Create a git repo** the agent can read from and write to — this is where it keeps its own
   memory of what it already found, so it doesn't re-report the same unchanged listing every
   run. A single markdown log file (dated entries, newest at the bottom) is enough.
2. **Point the agent at your two filled-in template files** (or paste their contents directly
   into this prompt — either works, but keeping them as separate files you can update
   independently is cleaner, since your evaluation framework will change less often than your
   target companies).
3. **Start narrow, then widen deliberately.** Don't try to cover every possible employer or
   title on day one — pick a handful of companies/platforms you know how to check reliably, get
   the log-and-diff mechanism working, then expand. Every time you widen scope (a new title, a
   new adjacent domain, a new industry), log *why*, so a future you (or the agent) understands
   the reasoning, not just the current rule.
4. **Give it a real notification rule**, and make it strict. An agent that pings you every run
   regardless of whether anything changed trains you to ignore it. Only notify on a genuinely
   new match, a tracked opportunity's status changing, or something breaking (see NETWORK CHECK
   below).
5. **Review its decisions periodically, not just its findings.** The most useful thing an agent
   like this can do isn't finding jobs — job boards do that. It's applying your evaluation
   framework *consistently*, every single run, without getting tired or making an exception
   under pressure the way a person might late in a search. Spot-check its PASS/STRETCH/GOOD
   calls against your own framework occasionally to make sure it's still calibrated.

---

## WHERE TO LOOK: BUILDING YOUR TARGET COMPANY LIST

The agent needs somewhere to start. Don't leave this to "search broadly" — hand it an actual
list, built from a few different kinds of reasoning, and expect to keep adding to it over time:

1. **Obvious-fit employers in your named field.** The companies you'd list if someone asked
   "who hires for what you do." Start here, but don't stop here — this list alone tends to be
   tech-company-biased and misses entire adjacent industries.
2. **A structured, complete directory, worked through exhaustively rather than sampled.** If
   there's a public list you can pull programmatically — a startup accelerator's portfolio
   (Y Combinator publishes one), a VC firm's portfolio page, a professional association's
   member directory — treat it as a finite backlog to clear systematically (see the tracking-
   file note in METHOD below), not a place to spot-check a few names from occasionally. This
   catches real matches that pure brand-recognition search misses.
3. **Cross-industry expansion, deliberately reasoned, not just "more tech companies."** Ask: what
   *function* do I actually do, and which industries need that function even though they're not
   obviously in my field? A knowledge-governance/content-strategy skill set is needed at law
   firms, insurance companies, healthcare orgs, and fintechs, not just SaaS companies — none of
   which show up if you only search companies that "feel like" your industry.
4. **Company categories built from your specific skill *combination*, not just your title.** If
   your real value is two skills together (say, mechanical/hands-on expertise plus geospatial
   data), search for the employer categories where *that combination* is the actual value
   proposition — fleet telematics, autonomous-vehicle prototyping, EV-charging network planning
   — rather than only searching for your job title in isolation, which will mostly surface
   employers who only need one half of what you bring.
5. **Be honest about what this method structurally can't reach.** Direct-ATS-API checking only
   finds postings on an employer's own careers page. It won't find agency/recruiter-posted
   listings, and it can't replicate a platform's own personalized recommendation feed (e.g.
   LinkedIn's job suggestions to you specifically) — note this limitation explicitly rather than
   letting the automated sweep quietly become your only channel. Keep checking those by hand.

Expect this list to grow over time as you notice gaps — see the SCOPE CREEP note at the bottom
of this file for how to widen it without letting it sprawl unmanaged.

---

## BUILDING YOUR TARGET TITLE LIST (in two tiers)

Your target titles are not one flat list. Some titles are a clean match for your work — anyone
using that title is doing something you can do. Others are titles your field *shares* with a
genuinely different field: the words line up, but half the postings under that title are
someone else's job. An automated sweep that treats both kinds the same will either flood you
with false positives or, if you tell it to be strict, quietly drop the real matches along with
the fake ones. Split the list.

**Tier 1 — clean-match titles.** The title reliably means the work you do. Match on the title
alone (still read the posting before applying, but the sweep can surface it without a domain
check). These are the titles from your own field and its close neighbors, plus any that a
current or former colleague would immediately agree describe your job.

**Tier 2 — shared-vocabulary titles.** The title is used by your field *and* by a different
field that isn't yours. The classic pattern: one word in the title is a real skill of yours
and the other word points somewhere adjacent but distinct — so a posting can carry the exact
title and still be the wrong job. For a Tier 2 title, tell the sweep to **read the full job
description and confirm the actual subject matches your work before surfacing it**, and to
**label why it came through** (e.g. "matched on title X — flagged for you to confirm it's not
really about Y") so a false positive stays visible as a judgment call rather than blending in
with the solid matches. Write the dividing line explicitly in the prompt, anchored to your
real accomplishments: *this title is a match when the posting is about [the thing you actually
did]; it is not a match when the posting is about [the adjacent thing that isn't yours], even
though the title is identical.*

How you find your Tier 2 titles: the most reliable source is someone already working in the
adjacent field telling you your experience would transfer. When that happens, don't take it at
face value and don't dismiss it — pressure-test it. List what you'd actually claim under that
field's vocabulary, check each claim against a real thing you did (not a thing that sounds
close), and keep only the titles where the honest answer is "yes, and here's the project."
Those become Tier 2 entries — real enough to search for, close enough to a different job that
every hit needs a look. See your career-context file's scope-boundary section for the same
distinction applied to individual resume claims.

---

## SEARCHING FOR WORK THAT DOESN'T HAVE A SETTLED NAME YET

Some of the work you're qualified for may not have a settled title at all — this shows up most
often with fractional/interim/advisory engagements, and with genuinely new or emerging functions
(AI enablement, AI governance, knowledge operations are current examples). The company that needs
this work may not even know a formal name for the role exists yet, let alone use it in a posting.
A title-based search — even a well-built Tier 1/Tier 2 list — will systematically miss this
category, because there's nothing consistent on the other end to match against.

The fix is to search by the **problem the company is trying to solve**, not the title of the
person who'd solve it. Build a second query list, phrased as the outcome or pain point a company
would actually describe, not a job title. For example, if your title-based search includes
"Fractional Chief Knowledge Officer," add problem-framed variants alongside it: "AI readiness
audit consultant," "knowledge base cleanup consultant," "documentation debt consultant." The
general move: take a title in your niche, ask what specific mess or gap that title exists to fix,
and search for that instead.

Two things to build into the sweep if you use this approach:

1. **Run both title-framed and problem-framed queries every time, not one or the other.** They
   surface different postings entirely — a company describing "we need someone to fix our messy
   Confluence before we roll out AI search" and a company posting "Fractional Chief Knowledge
   Officer" are two different populations of postings, not overlapping phrasings of the same one.
2. **If you're checking fractional/consulting marketplaces specifically, don't rely on their
   keyword search alone.** Many of these platforms organize open engagements as short client
   problem-statements grouped into loose categories (e.g. "Knowledge Management," "AI Strategy,"
   "Change Management") rather than as formal job-title postings a keyword search would catch.
   Browse the relevant categories directly, in addition to searching — a real match can sit right
   there without ever surfacing in a title search.

---

## SCREENING THE POSTING BODY, NOT JUST THE TITLE

Titles in most fields are unreliable, and a title-only sweep fails in both directions. It misses
real matches with off-vocabulary titles, and it passes along postings whose titles look right and
whose bodies describe something else. Fix this by reading the body of every posting the sweep
fetches.

Two companion files do the work. Fill them in and keep them in the sweep's repo:

- `body_text_signals_template.md` lists the phrases that mean your work (strong and supporting),
  your red flags, and the rule for turning a phrase count into a candidate.
- `search_lanes_template.md` lists methods for searching posting text directly, on boards whose
  search covers full text, and for boards that return titles only.

Two habits make this hold up. Match short acronyms as whole words only. Put method detail in
those repo files, not in the prompt, so that changing a method is a commit and not a resend of the
whole prompt. Record each change, with the reason, in your sweep changelog
(`sweep_changelog_template.md`).

---

## THE PROMPT

```
You are running a [daily/weekly] automated job-search sweep for [your name], [one-line role
description]. You have a git repo cloned ([repo URL]) that persists results across runs — use it
to avoid re-reporting the same unchanged findings every time.

STEP 0 — READ HISTORY FIRST: Check the log file at the repo root. Read the most recent dated
entry (if any) to classify today's findings as NEW, STILL OPEN, or CLOSED relative to what was
already found.

STEP 0.5 — CHECK YOUR OWN URGENCY PHASE: [reference the phase-based timeline from your
application_log — e.g., "compare today's date against the phases defined there; escalate
STRETCH-tier engagement once Phase 2 begins."]

STEP 0.75 — NETWORK CONNECTIVITY CHECK: Before doing anything else, test direct external
connectivity to a couple of plain URLs. If blocked, flag "NETWORK BLOCKED" prominently at the
top of today's log entry, fall back to a broader web search, and mark every finding
lower-confidence rather than treating this as a normal run.

GOAL: Find currently LIVE postings matching the criteria in [career_context_template.md] and
[application_log_template.md] (attach or paste both). Specifically:

1. TITLE MATCHING — don't rely on exact keyword matching alone, in either direction:
   - A title that doesn't use the expected words can still be your job — read the description
     body, check the real day-to-day work against the context file, and flag a hit as
     "skills match, atypical title" with the specific experience the role calls for.
   - A title that *does* use the expected words can still be someone else's job — for the
     Tier 2 / shared-vocabulary titles in [your title list], confirm the posting's actual
     subject matches your work before surfacing it, and label why it came through so a false
     positive stays visible: "[matched on title, flagged to confirm it's not really about X]".
   [Paste your Tier 1 and Tier 2 title lists here, with the dividing line for each Tier 2
   title written out — "a match when the posting is about A, not when it's about B."]
2. HARD FILTERS — apply the hard filters defined in the evaluation framework (location, pay
   floor, or whatever else is marked non-negotiable) with zero exceptions, regardless of how
   good a match otherwise looks.
3. TIER EVERY MATCH using the GOOD/STRETCH/PASS framework already defined in the application log
   — don't invent a new evaluation standard per posting.
4. DON'T RE-LITIGATE SETTLED DECISIONS — maintain a running "known false positive / already
   passed / declined" list in the log so a posting that's already been reviewed and rejected
   doesn't get re-surfaced as new just because it's still technically live.
5. BODY-TEXT SCREEN — for every posting fetched with a full body, read the body whatever the
   title says, using [your body_text_signals file]. Report body-match candidates under their own
   heading, apply the tier framework, and downgrade title matches whose bodies show red flags.
   On each full pass also run the search lanes in [your search_lanes file], and list every board
   that could only be scanned by title as "unscreened" in the day's entry.

METHOD — prefer direct, structured sources over generic web search where possible:

Most companies don't build their own careers page from scratch — they run it on top of an
applicant-tracking system (ATS), a piece of shared software several employers all use. The
useful part: a lot of these systems expose a plain, public, read-only JSON endpoint behind the
pretty page — the same data the webpage displays, but structured and queryable directly, with no
login and no scraping needed. That's far more reliable than parsing rendered HTML, and cheap
enough to re-check "is this specific posting still open" every single run. A few common ones,
with `{company}` as the placeholder you swap for each employer's own slug (usually visible in
their careers-page URL):

- **Greenhouse:** `https://boards-api.greenhouse.io/v1/boards/{company}/jobs?content=true`
- **Lever:** `https://api.lever.co/v0/postings/{company}?mode=json`
- **Ashby:** `https://api.ashbyhq.com/posting-api/job-board/{company}`
- **Workday:** `https://{company}.wd{N}.myworkdayjobs.com/wday/cxs/{company}/{site}/jobs` — the
  one common exception: this one usually requires a POST request with a small JSON search
  payload rather than a plain GET, and the `{N}` and `{site}` values vary per company, so expect
  to spend a little more effort confirming the exact URL the first time you check a given
  employer.

You won't know which platform a given employer uses in advance — the practical approach is to
just try the company's slug against each pattern above in turn (they fail fast and safely with a
404 if wrong) and note which one worked. Build up your own running list of `{company} → platform`
as you go, so you're not re-discovering it every run.

- For platforms without a clean public API (many use something custom, or a platform that
  requires a rendered page), fall back to a direct fetch of the employer's own careers page, and
  treat anything that resists verification as "unresolved," not as a negative result — don't
  silently drop a lead just because it was hard to check.
- For a broad company-directory sweep (e.g., every company in a startup accelerator's public
  portfolio), keep a separate tracking file listing which companies/slugs have already been
  checked, so a large backlog gets worked through incrementally across many runs instead of
  being re-attempted from scratch every time.
- These are public endpoints meant to be checked by job seekers and their tools, but be a
  reasonable citizen about it — a scheduled run once or twice a day is plenty; there's no need to
  poll aggressively.

STEP FINAL — WRITE, COMMIT, PUSH: Append a dated section to the log file with: connectivity
status, new matches per the framework above (with tier + reasoning), anything that closed,
and a one-line summary of what's unchanged. Commit with a descriptive message and push.

NOTIFICATION RULE: Send exactly one notification only if there's a new GOOD/STRETCH match, a
tracked opportunity's status changed, or the network was blocked. Do not notify if nothing
changed. Keep it under 200 characters.
```

---

## A NOTE ON SCOPE CREEP

It's tempting to keep adding new titles, industries, and platforms to this prompt indefinitely.
Each addition makes the agent slower and the prompt harder to maintain. When you do widen scope,
treat it as an experiment with a review checkpoint, not a permanent addition by default — note
the date you added it, why, and a date to come back and check whether it actually surfaced
anything worth having versus just adding noise. If it didn't earn its keep, narrow back down.
Tier 2 / shared-vocabulary titles (see BUILDING YOUR TARGET TITLE LIST) are the likeliest to
add noise rather than matches — put a firm review date on each one and be willing to cut it.
