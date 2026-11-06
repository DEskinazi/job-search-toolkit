# Job Search Toolkit

Template files for job-searching with an LLM without it overclaiming, underclaiming, or drifting
away from what is actually true about your career. Everything here works with any LLM chat. Two
optional Claude Code skills are included.

## Quick start

Do these in order. The first two steps take real time, because they are the part everything
else depends on. Expect an hour or two.

1. **Get the files.** Clone this repo or download it. You need two files to start:
   `career_context_template.md` and `application_log_template.md`.
2. **Build your career file with your LLM.** Paste all your resume versions into a chat and use
   this prompt:

   ```
   I am job searching and want a source-of-truth file about my career, so that nothing you
   write for me overclaims. Below are all my resume versions and notes. Draft my career file
   using the structure in career_context_template.md. Then go through every accomplishment
   claim one at a time: show me the claim, say where it came from, and ask me to confirm it,
   correct it, or cut it. Do not add anything I have not confirmed.
   ```

   Save the result as your own `career_context.md`.
3. **Fill in your search constraints.** Open `application_log_template.md` and complete the
   constraint table: pay floor, location, schedule, and the rest.
4. **Try it on one posting.** Give your LLM both files and a job posting. Ask it to tier the role
   (GOOD, STRETCH or PASS) and to say which requirements you meet, which are a real stretch, and
   which are gaps.
5. **Fix errors at the source.** When a draft gets a fact wrong, correct it in your career file
   right away, so the same mistake does not come back.

That is the whole core toolkit.

## What's in here

| File | What it is | Needed? |
|---|---|---|
| `career_context_template.md` | The source of truth for your career facts: work history, scope boundaries, accomplishment write-ups, how to handle requirements that look unmet, and a glossary so generated documents use accurate verbs. | Core |
| `application_log_template.md` | Your search constraints, a GOOD / STRETCH / PASS framework with hard filters, and a log for comparing opportunities. | Core |
| `job_sweep_agent_template.md` | A prompt for a scheduled agent that checks job boards for you on a recurring basis. | Optional |
| `body_text_signals_template.md` | The phrases and red flags that tell your sweep what a posting is really about, so it reads bodies and not only titles. | Optional, with the sweep |
| `search_lanes_template.md` | Methods for searching posting text directly, and for boards that return titles only. | Optional, with the sweep |
| `sweep_changelog_template.md` | A format for recording why your search methods changed, with examples. | Optional, with the sweep |
| `skills/job-fit-analysis/` | A Claude Code skill: fetch the real posting, check it against your facts, give an honest tier. | Optional, Claude Code |
| `skills/interview-prep-builder/` | A Claude Code skill: build interview questions and talking points from your career file. | Optional, Claude Code |

## Go further

See [`docs/optional-extras.md`](docs/optional-extras.md) for installing the Claude Code skills,
the full step-by-step path to a scheduled sweep, and notification delivery.

## License

MIT. See `LICENSE`.
