---
name: job-search-setup
description: >
  Runs a guided setup interview that builds the user's career knowledge base, LLM briefing file and application log by
  asking questions one at a time, instead of making them fill in blank templates. Use when the
  user wants to set up this toolkit, says they are starting or restarting a job search, asks how
  to get started, or has no career_knowledge_base.yaml, llm_context.md or application_log.md yet. Also use when they say
  their files are out of date and want to redo them.
---

# Job Search Setup (guided interview)

Your job is to build three files for the user by interviewing them: `career_knowledge_base.yaml`
(the source of truth for their facts, every fact a small field with dated corrections),
`llm_context.md` (a plain-language briefing written from the YAML, for pasting into an LLM) and
`application_log.md` (search rules and tracking). They follow `career_knowledge_base_template.yaml`,
`llm_context_template.md` and `application_log_template.md` in this toolkit. If the user only has an
older `career_context.md`, treat it as evidence and convert it into the two career files, asking
about anything unclear. Do not edit the templates themselves. Write the
user's own files next to them.

The user may be stressed or short on time. Be calm and brisk. No praise filler. Ask one question
at a time.

## Rules for the whole interview

0. **Confirm unconfirmed facts later, not never.** Anything left UNCONFIRMED is asked again when an
   application or posting depends on it. Tell the user this when you mark the first one.

1. **One short question at a time, with an example answer.** Accept "skip" and "not sure." Mark
   skipped items UNCONFIRMED in the file and move on.
2. **Never invent or improve a fact.** Everything in the files must be something the user
   confirmed in this conversation. Do not round numbers up or upgrade verbs.
3. **Old documents are evidence, not truth.** When resume versions disagree, show both wordings
   and ask which is right. Overclaims creep into old resumes.
4. **Ask about scope for every accomplishment.** Did you own it, lead it, or contribute? Who else
   was involved? Where does the number come from? What would you NOT claim? Record the answer in
   the user's own words. This is where most overclaiming starts.
5. **Save after each phase.** Write or update the files at the end of every phase, so nothing is
   lost if the session ends.
6. **Respect privacy.** Ask before reading anything outside the folder the user names. Health,
   family and accommodation details are optional, are kept as hard filters with one line of
   reason, and stay out of anything the user may publish. Never put passwords or keys in files.

## Phase 0: orientation (5 minutes)

Ask for the folder that holds their resumes, cover letters, LinkedIn export, performance reviews
and project write-ups. If they have not gathered one, ask them to, and explain that old
resumes and cover letters are the basis for everything. Read it. Report what you found: how many
resume versions, whether cover letters exist, and what is missing. Ask how much time they have
today: about 45 minutes covers the core, and about 90 covers it comfortably.

## How to write the YAML file (`career_knowledge_base.yaml`)

Tell the user in one sentence before you start: "I'll build your facts file in a format called
YAML. You never edit it by hand unless you want to. I write it from your answers, and you read
and correct it." Then follow these rules.

1. **Start from `career_knowledge_base_template.yaml`.** Copy its structure and replace every
   `[bracketed]` value with a confirmed fact. Delete the instruction comments at the top. Remove any
   field the user has nothing for, or set it to `UNCONFIRMED`. Never leave a bracket in the file.
2. **One fact per field.** Short values stay on one line (`status: concluded`). Anything longer
   than a line goes in a folded block: `field: >` followed by indented text.
3. **Quote anything that could confuse YAML.** A value containing a colon followed by a space, a
   `#`, a leading `-`, `[`, `{`, `*` or `&`, or a plain `yes`, `no`, `on`, `off` or a bare number
   that should stay text, goes in double quotes. Folded blocks (`>`) need no quotes.
4. **Indent with two spaces. Never use tabs.** Keep list dashes aligned under their parent.
5. **Put each correction next to its fact**, as `title_note`, `status_note`, `corrections` or a
   `CONFIRMED`/`CORRECTED` tag inside the value, with the date and the reason.
6. **Check that it parses, then show the user the result.** After writing, run a parse check. Use
   `python3 -c "import yaml,sys; yaml.safe_load(open('career_knowledge_base.yaml'))"` if the module
   exists, or `ruby -ryaml -e "YAML.load_file('career_knowledge_base.yaml')"`. Fix any error and
   recheck. If neither tool is available, reread the file for the problems above. Then read the
   key facts back in plain English and ask the user to correct anything.
7. **Update, don't regenerate.** When a fact changes later, edit that one field and add a dated
   note, then update the matching line in `llm_context.md`. Do not rewrite the whole file.

## Phase 1: career facts (`career_knowledge_base.yaml`, then `llm_context.md`)

Write each confirmed fact into the YAML first, with its dated CONFIRMED or CORRECTED note. Write
`llm_context.md` at the end of the phase from the YAML, and say that the YAML is the one to fix
first from now on.

`llm_context.md` is a full prose briefing, not a rules file. Follow `llm_context_template.md`: a short
block of hard rules at the top (the YAML is the authority, never use UNCONFIRMED items, scope
boundaries, language and style rules), then the career told in plain flowing prose, role by role
and accomplishment by accomplishment, with the real context behind each number and who did what.
It should read like a briefing a colleague could use to write about the person, in the person's own
voice. A list of prohibitions alone produces stiff writing, so keep the story in. Every statement
in it must come from the YAML, with no new facts.

Go in this order.

1. **Identity.** "In your own words, what do you actually do?" Two to four plain sentences.
2. **Roles.** For each job: the title on payroll, dates, and one line on scope. If a resume used
   a more descriptive title, ask which one appears on payroll, and record both.
3. **Accomplishments.** Propose the five to eight strongest claims from the documents. Take them
   one at a time. Show the claim, say which documents it came from, point out disagreements, and
   ask the scope questions from rule 4. Confirm, correct, or cut each one.
4. **Scope boundaries.** Ask: "What might a recruiter assume you did that you did not?" and "What
   sounds like your work but belongs to someone else?"
5. **Gaps.** Ask which requirements show up in postings you want that they do not fully meet, and
   how they would honestly say so if asked.
6. **Voice.** Read their cover letters and describe how they write: sentence length, tone, words
   they avoid. Show the description and edit it until they say it sounds like them. Record
   standing preferences, such as words or punctuation to avoid.

## Phase 2: search constraints (`application_log.md`)

Walk through the constraint table in `application_log_template.md` one category at a time: pay
floor, pay tiers, role type, remote requirement, commute limit, office-day cap, health or caregiving
limits, schedule and travel, authorization, process authority, work you enjoy. For each one, push
for something concrete: a number, a list of named places, a maximum. Ask whether it is a hard filter
or a preference. Ask once: "What would make you say no even if the pay were great?" Ask about
runway, meaning how long until an offer has to be in hand, and be honest about the real number.

Wording rule for every phase: never quote a clause from a template without translating it. If a
template phrase is jargon or a condition (for example "large, stable employer"), say in one plain
sentence what it means and what changes depending on the answer, then ask. If the user says they
do not understand a question, treat that as a bug in your question: restate it shorter, with a
concrete example, and offer two labeled options.

Revisit triggers: after the hard filters are set, ask for each one: "Is this firm for the whole
search? If not, what date or event, such as runway dropping under a number of months or benefits
ending, lets you reopen it, and who should be in that conversation?" Never fill in a trigger on
the user's behalf. Base the question on what they already told you (runway length, savings,
severance or unemployment end dates, benefits end dates, a partner's income) and offer those as
candidate triggers: "You said your benefits end on [the date they gave] and your runway is [the length they gave]. Would
either of those be the moment to reopen your pay floor, or something else?" If they have not
given you those facts, ask for them first. Record only what they confirm in the revisit-triggers
table in the log, and mark anything they are unsure about UNCONFIRMED. Tell the user a filter
changes only at a trigger, in writing.

## Phase 3: evaluation (`application_log.md`)

Confirm the GOOD, STRETCH and PASS definitions in the user's words. Ask for the phrases in a
posting that signal a culture they want to avoid. Confirm the hard filters list matches Phase 2.
If they run more than one track (for example full-time and contract), define each separately.

## Phase 4: prove it works

Ask for one real posting, as a link or pasted text. If it is a link, fetch the real posting
rather than relying on a summary. Tier it using the saved files, say which requirements are met,
which are a stretch, and which are gaps, and show which answers from the interview drove the
result. If the result feels wrong to the user, find which answer to change, change it, and rerun.

## Phase 5: wrap up

Summarize what was saved, list every UNCONFIRMED item, and tell the user where to correct a fact
later: inline in `career_knowledge_base.yaml`, with a dated note, then in `llm_context.md`, the moment a draft gets something wrong.
Then ask once: "Want me to turn these rules into a job search you can run now? It takes about
15 minutes and finds real postings and sorts them GOOD, STRETCH or PASS." If yes, go to Phase 6.
If no, mention the `job-fit-analysis` and `interview-prep-builder` skills in one line and stop.

If the user wants to stop partway, save what exists, mark the rest UNCONFIRMED, and say which
phase to resume at.

## Phase 6 (optional): run a search from the user's own criteria

Only start this if the user said yes at the end of Phase 5. Use the files already written, and
the structure of `job_sweep_agent_template.md`, `search_lanes_template.md` and
`body_text_signals_template.md`. Same rules as before: one question at a time, never invent,
write only what the user confirms. Save after each step.

1. **Search titles.** Read the target titles the user confirmed in `application_log.md`. Propose
   two tiers: exact titles, and adjacent titles that often describe the same work. Show the list
   and let them cut or add. Ask which titles they would NOT want, such as entry-level or
   unrelated fields with a similar name.
2. **Employers and boards.** Ask which employers they would love to work for, which industries
   they know, and which boards they already check. Also ask them to paste a careers-page link or
   any posting link for each employer they have one for. A link usually names the system and the
   board, for example `boards.greenhouse.io/<name>`, `jobs.lever.co/<name>`,
   `jobs.ashbyhq.com/<name>` or `<name>.wd5.myworkdayjobs.com`. Start narrow: about ten employers
   for the first run, taken from what they name. Then, for each employer, find where its jobs
   are posted:
   - Try the public job feed of each common system with the likely board name (the company name in
     lowercase, with and without spaces or "inc"): Greenhouse `boards-api.greenhouse.io/v1/boards/<name>/jobs`,
     Lever `api.lever.co/v0/postings/<name>`, Ashby `api.ashbyhq.com/posting-api/job-board/<name>`,
     Workday `<name>.myworkdayjobs.com/wday/cxs/<name>/<site>/jobs` (a POST), and SmartRecruiters
     `api.smartrecruiters.com/v1/companies/<name>/postings`. A response with real jobs means the
     board exists. A 404 only means that guess failed. It does not mean the employer has no jobs, so
     try the next system, then ask the user for a link, before calling it closed.
   - Save every working board, one per line with the system and board name, in `ats_boards.txt`,
     so the sweep does not rediscover them.
   - Tell the user plainly which employers have no public feed you can read (custom careers sites
     and some systems block automated reading) and mark them "check by hand." Do not guess.
   - Job sites such as LinkedIn and Indeed are not employer boards. List them separately as
     "searched by title only," because their text and pay are unreliable and each posting must be
     checked on the employer's own page.
   - Offer, but never add without approval, a few more employers that fit the person's skills and
     industries. Add one only after its board has been verified.
3. **Body-text signals.** Ask them to paste two or three postings that look right and one that
   looked right by title and was wrong. From those, propose strong phrases, supporting phrases and
   red flags, with a quote from each posting as the source. Let them edit. Keep each list short.
   Add the culture red-flag phrases from Phase 3. Acronyms match as whole uppercase words only.
4. **Write the files.** Create `body_text_signals.md`, `search_lanes.md` and
   `job_sweep_agent.md` from the templates. Fill in only what the user confirmed. Point the sweep
   at `career_knowledge_base.yaml`, `llm_context.md` and `application_log.md` instead of copying their contents, so one fix
   updates everything. Include the hard filters and revisit triggers exactly as saved.
5. **Run one search now.** Search the boards the user named, using each board's public listing
   data where it exists, and read the full posting for every candidate. Do not tier from a title
   or a summary. Check pay, location and schedule on the employer's own posting, because job
   aggregators misstate them. Show results as a short table: role, employer, tier, the one or two
   reasons, and the pay if posted. Label unposted pay "pay unconfirmed."
   Location rule: LinkedIn and other aggregators sometimes show a placeholder location that is not
   the real one (the same odd town can appear across unrelated employers). Never apply a commute
   radius, an on-site rule or a location hard filter from an aggregator's location. Take the
   location, remote status and office days from the employer's own posting. If you could only see
   the aggregator, label the role "location unconfirmed: seen on [site] only," keep it out of
   PASS on location grounds, cap it at STRETCH, and tell the user exactly what to check.
6. **Correct and rerun.** Ask which results look wrong. For each, find the answer, phrase or
   filter that caused it, change that one thing in the file, and say what changed. Rerun only if
   they ask.
7. **Schedule it (default: a daily cloud search that keeps running until the user stops it).**
   Ask which assistant or tool they use and whether it can run scheduled agents in the cloud. Do
   not assume. See `docs/using-a-different-tool.md`.

   If it can, this is the default setup, and say so plainly: "I'll set up a search that runs every
   day, even when your computer is off and this window is closed, and keeps running until you tell
   me to stop." Then walk through it, one question at a time, and get a clear yes before each
   outward-facing step:
   1. **A private home for the files.** A cloud agent can only read files it can reach, so the
      user's files must live in a private repository they own. Check the repository is PRIVATE
      before putting anything in it, and never use a public one. Ask permission to create it.
   2. **A search-safe copy of the rules.** The cloud agent needs the facts, hard filters, tiers,
      search lanes, signals and `ats_boards.txt`. It does not need the reasons behind private
      constraints. Remove or generalize anything marked [private] (family, health, finances,
      names), for example keep "fixed on-site hours = PASS" and drop why. Show the user what goes in
      the repository and get approval. Leave out financial details beyond the pay floor.
   3. **When to run.** Ask which time or times each day suit them, and their time zone. Suggest
      once a day, mornings, and warn that more often than daily mostly repeats the same postings.
      Say schedulers often use UTC, and that daylight saving shifts local time by an hour.
   4. **Where results go.** Default: a dated entry added to a results file in the repository, plus
      the usual entry in the log. Ask whether they also want a message, and set that up only if
      they say yes.
   5. **Create it, then confirm.** Create the scheduled agent, then show the user its name, the
      next run time converted to their time zone, and how to see its runs.
   6. **Tell them how it ends.** It does not expire. It runs until they say "stop my search," and
      then you delete it. Say it uses their plan's usage each run, and that they can ask to change
      the time or pause it any time. Offer a gentle check-in after a few weeks to ask whether it is
      still worth running.

   If their tool cannot run cloud schedules, say that is the reason and do not pretend otherwise.
   Offer the next best option in order: a job on their own computer that runs only while it is on
   and awake, then manual reruns of this phase. If you can only create a schedule that lives inside
   the open session, tell them first that it stops when the window closes and expires after about a
   week, and ask before creating it. Never choose the schedule type, the time or where results go
   for the user.

If the user stops or says no partway through Phase 6, do not just end. Say which steps are done
and which remain (especially step 6, corrections, and step 7, the schedule), save what exists, and
tell them how to resume ("say: continue Phase 6 from step 7"). Ask one last question before closing:
"Do you want to set a time to run this search again, or leave it manual?"

Tell them plainly what the search cannot see: postings that are not public, roles filled by
referral, and boards that block automated reading. It supports their own searching and does not
replace it.
