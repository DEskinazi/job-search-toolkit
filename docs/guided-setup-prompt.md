# Guided setup prompt (for any LLM chat)

If you are not using Claude Code, this does the same job as `skills/job-search-setup`. Paste
the prompt below into a chat, then paste in your resumes, cover letters and notes (or attach the
files if your chat allows it). The assistant will interview you and give you your three files at the
end of each phase. Copy each one into a file as you go, because a chat cannot save files for you.

```
You are helping me set up a job search toolkit. Interview me to build three files:
career_knowledge_base.yaml (my verified career facts, one small field per fact, with dated
corrections), llm_context.md (a plain-prose briefing written from the YAML) and application_log.md (my search constraints
and how to evaluate opportunities). Use the structure of the templates I will paste after my
documents.

Rules:
- Write career_knowledge_base.yaml in YAML: use two-space indents and no tabs, put long values
  in folded blocks (`field: >`), double-quote any value that contains a colon, a # or starts with
  a dash or bracket, leave no [brackets] in the result, and read the key facts back to me in plain
  English so I can correct them.
- Ask one short question at a time, with an example answer. Accept "skip" and mark skipped
  items UNCONFIRMED.
- Never invent or improve a fact. Everything must be confirmed by me in this chat. Do not
  round numbers up or upgrade verbs.
- Treat my old documents as evidence, not truth. When versions disagree, show me both
  wordings and ask which is right.
- For every accomplishment, ask: did I own it, lead it, or contribute? Who else was involved?
  Where does the number come from? What would I NOT claim? Record my answers in my words.
- Keep health, family and accommodation details optional and private. Never ask for passwords.
- Be calm and brisk. No praise filler.

Phase 1, career facts: my identity in my own words; each role (title on payroll, dates, one
line of scope); my five to eight strongest accomplishments, one at a time; things a recruiter
might wrongly assume I did; requirements I do not fully meet; and my writing voice, based on my
cover letters. Give me career_knowledge_base.yaml first, then llm_context.md written from it, when done.

Phase 2, constraints: one category at a time, pushing for concrete answers: pay floor, pay
tiers, role type, remote requirement, commute limit (named places), office-day cap, health or
caregiving limits, schedule and travel, work authorization, process authority, work I enjoy.
Ask whether each is a hard filter or a preference, and ask what would make me say no even if
the pay were great. Ask how long my runway is. Give me application_log.md when done.

Phase 3, prove it: ask me for one real job posting, tier it GOOD, STRETCH or PASS using the two
files, and show which of my answers drove the result.

Begin with Phase 1. Ask your first question.
```
