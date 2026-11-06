# Job Search Toolkit

Template files, plus two optional Claude Code Skills, for job-searching with an LLM without it
overclaiming, underclaiming, or quietly drifting away from what's actually true about your career.

## The problem this solves

Ask an LLM to write you a resume bullet, and it will happily generate something plausible,
polished, and occasionally wrong — not because it's trying to deceive anyone, but because it
has no way to distinguish "what you told me once, loosely" from "what's actually verified true."
Left unmanaged, this produces resumes that overclaim (implying sole ownership of a team effort),
underclaim (missing a real qualification because it wasn't phrased using the posting's exact
buzzword), or just drift inconsistent across five different tailored versions.

The fix isn't a smarter prompt. It's a **single source-of-truth file you maintain deliberately**,
that every generation task is required to draw from — plus a **separate log for evaluating
opportunities**, kept apart so career facts and application-specific notes don't get tangled
together.

## What's in here

- **`career_context_template.md`** — a structured file for your actual career facts: identity,
  work history, scope boundaries (what you do vs. what merely sounds like what you do), detailed
  accomplishment write-ups, a framework for handling job-posting requirements that look unmet but
  might not be, and a language glossary so every generated document uses consistent, accurate
  verbs. Read the setup instructions at the top of the file before filling it in — the most
  important step is feeding an LLM *every* old resume version you have, not just your current
  one, so nothing gets lost in the reconciliation.
- **`application_log_template.md`** — a log for tracking and comparing opportunities against each
  other: your real constraints (comp anchor, runway, non-negotiables), a reusable
  GOOD/STRETCH/PASS evaluation framework with hard filters that never flex regardless of time
  pressure, and a phase-based structure for deciding, on purpose, when to widen your criteria as
  a timeline compresses — instead of that happening unconsciously as pressure builds.
- **`body_text_signals_template.md`**, **`search_lanes_template.md`** and
  **`sweep_changelog_template.md`** — the body-text layer for the sweep. Titles in most fields are
  unreliable, so these files tell the agent which phrases to look for inside a posting (and which
  red flags to downgrade for), how to search posting text on boards where that is possible, and
  how to keep a changelog of why the search methods changed. Optional, but this is where most of
  the real matches turned up once the title scan stopped finding new ones.
- **`job_sweep_agent_template.md`** — a prompt template for a scheduled agent that reads the
  other two files and checks job boards for you on a recurring basis, applying your evaluation
  framework consistently instead of you re-deciding it under pressure at 11pm. Includes guidance
  on avoiding scope creep as you widen what it searches for over time.

## Optional: Claude Code Skills

If you're using Claude Code specifically (not just any LLM chat), two ready-to-use Skills live in
`skills/`:

- **`skills/job-fit-analysis/`** — formalizes the "fetch the real posting, check it against my
  facts, give me an honest tier" workflow described below, so it triggers automatically whenever
  a job posting comes up in conversation instead of depending on you remembering to ask for it
  every time.
- **`skills/interview-prep-builder/`** — builds likely interview questions, answer structure, and
  personalized talking points from your `career_context_template.md`, triggered automatically
  whenever an upcoming interview or screen is mentioned.

To use either, copy the relevant folder into `~/.claude/skills/` (for every project) or a specific
project's `.claude/skills/` directory, alongside your filled-in `career_context_template.md` and
`application_log_template.md`. Both skills are optional — everything they do can also be done by
hand using the workflow in the next section, with any LLM.

## Optional: notification delivery beyond desktop/phone push

If you want the sweep agent to alert you somewhere more reliable than a generic push notification
— especially useful if you want it to reach you even when you're not at your computer — you can
have it call any messaging API you already control directly, with no extra infrastructure. A
personal Telegram bot is a good fit: create one (a few messages to @BotFather gets you a token in
under a minute), send yourself one message manually to get your chat ID, then add a line to your
sweep agent's instructions telling it to `curl` a POST to
`https://api.telegram.org/bot<TOKEN>/sendMessage` with your chat ID and the alert text whenever it
finds something worth surfacing. This was built and verified end-to-end this way — confirmed via
a direct API call (`getMe`) that the token works, then a real test message delivered to a phone
before wiring it into the actual scheduled agent.

**One real tradeoff worth knowing before you do this:** wherever your scheduled agent's
instructions live, that's also where the bot token would live — in plaintext, since the agent
needs to use it directly. That's a genuine, if usually small, increase in where the credential
could leak from (anyone who could read your agent's stored configuration could also read the
token). Weigh that against how the token is already stored elsewhere (a config file on a personal
device, say) — if it's already sitting in plaintext somewhere, adding a second plaintext copy
mostly just adds "one more place it could leak from" rather than introducing plaintext storage for
the first time. Decide deliberately rather than skipping this consideration because the technical
setup itself is easy.

## You don't need the automated agent to get value from this

The first two files are useful entirely on their own, with zero automation. A common real case:
you find a role yourself — scrolling LinkedIn, a friend sends a link, whatever — and want to
tailor your resume to it quickly and accurately. Hand the LLM `career_context_template.md`
(filled in) plus the job posting, and ask it to draft a tailored version and flag which stated
requirements you genuinely meet, which are a real stretch worth naming honestly, and which don't
apply. That's the whole workflow — no scheduled agent required. `job_sweep_agent_template.md` is
for when you want that same discipline applied automatically, at scale, across roles you didn't
go looking for yourself; it's an addition, not a prerequisite — and not a replacement for
searching yourself, either. The real pattern this toolkit is built around is both running at
once: the agent works on a schedule (checking boards overnight, say, while you're not looking),
and you keep searching manually too, on platforms and through channels (a recommendation feed,
a friend's link, your own browsing) that an automated sweep structurally can't reach. Both feed
the same two files, so either way, everything gets evaluated against the same standard.

## Getting started, start to finish

This is the full path from having nothing to having the whole system running, in order. Steps
1-5 are the core toolkit and work with any LLM; 6-8 are optional and Claude-Code-specific.

1. Read the instructions block at the top of `career_context_template.md` and follow it —
   gather every resume version you have, reconcile the claims with yourself, and write the
   corrected version into the file. Budget real time for this step; it's the one thing everything
   else depends on, and rushing it defeats the point.
2. Read the instructions block at the top of `application_log_template.md`, and fill in your
   real search constraints and evaluation framework — your actual pay floor, non-negotiables, and
   the GOOD/STRETCH/PASS criteria you want applied consistently.
3. When you ask an LLM to draft a resume, cover letter, or blurb, give it `career_context_template.md`
   (filled in) as context and tell it explicitly: don't write anything this file doesn't support.
4. When you're deciding whether to pursue a specific opportunity, give it `application_log_template.md`
   (filled in) plus the job posting, and ask it to slot the posting into a tier using the
   framework already defined there.
5. Whenever a generated draft gets a fact wrong — overclaims, underclaims, or just phrases
   something inaccurately — fix it in `career_context_template.md` immediately, in the same
   session. Corrections that only live in a resume draft will resurface as the same argument
   next time. **Steps 1-5 are the whole toolkit already working — everything below is optional.**
6. *(Optional, Claude Code only)* Copy `skills/job-fit-analysis/` and `skills/interview-prep-builder/`
   into `~/.claude/skills/` so they trigger automatically instead of needing to be invoked by hand
   each time.
7. *(Optional)* Fill in `job_sweep_agent_template.md` and schedule it if you want an automated,
   recurring check of job boards on top of your own manual searching — not a replacement for it.
8. *(Optional)* Once the sweep is running and titles stop turning up new matches, fill in
   `body_text_signals_template.md` and `search_lanes_template.md` so it reads posting bodies, and
   start a changelog from `sweep_changelog_template.md`.
9. *(Optional)* If you want sweep alerts delivered somewhere more reliable than a generic push
   notification, wire in a messaging API per the notification-delivery section above — after
   weighing the tradeoff described there.

## How the files work together

`career_context_template.md` answers "what's actually true about me." `application_log_template.md`
answers "given what's true about me, does this specific opportunity make sense." `job_sweep_agent_template.md`
reads both of the above and automates the ongoing search itself. Keep company-specific tailoring
notes out of the first file, and keep your core facts out of the second — duplicating them risks
drift, where a correction made in one place never makes it to the other.

## License

MIT — see `LICENSE`.
