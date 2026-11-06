# Job Search Toolkit

Template files for job-searching with an LLM without it overclaiming, underclaiming, or drifting
away from what is actually true about your career. Everything here works with any LLM chat. Three
Claude Code skills are included.

## Why this exists

Ask an LLM to write you a resume bullet and it will give you something plausible, polished, and
occasionally wrong. It cannot tell "what you mentioned once, loosely" from "what is actually
verified true," so it overclaims, underclaims, or drifts across five tailored versions of the
same resume. The fix is not a smarter prompt. It is one source-of-truth file you maintain on
purpose, plus a separate log for judging opportunities against it.
[Read the full reasoning.](docs/why-it-works.md)

## Quick start

Do these in order. Expect about an hour. The setup interview is the part everything else
depends on.

1. **Get the files.** Clone this repo or download it.
2. **Gather everything you have written about your work into one folder.** Every resume version,
   every cover letter, your LinkedIn export, performance reviews, project write-ups. Do not start
   from a blank page. Cover letters count, because they show your voice. Old documents are
   evidence, not truth: they often overclaim and disagree with each other, which is why the next
   step makes you confirm every claim.
3. **Run the guided setup.** It interviews you one question at a time and writes your two files.
   - **Claude Code:** copy `skills/job-search-setup/` into `~/.claude/skills/`, then say "set up my
     job search" and point it at your folder.
   - **Any other chat:** open [`docs/guided-setup-prompt.md`](docs/guided-setup-prompt.md), paste the
     prompt, then paste in your documents.
   - **Prefer to fill in the templates yourself?** Open `career_context_template.md` and
     `application_log_template.md` and follow the instructions at the top of each.
4. **Try it on one posting.** The setup ends with this. Later, give your LLM both files and any
   posting, and ask it to tier the role (GOOD, STRETCH or PASS) and to say which requirements you
   meet, which are a stretch, and which are gaps.
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
| `skills/job-search-setup/` | A Claude Code skill that interviews you and builds your two files. The paste-in version for other chats is `docs/guided-setup-prompt.md`. | Recommended |
| `skills/job-fit-analysis/` | A Claude Code skill: fetch the real posting, check it against your facts, give an honest tier. | Optional, Claude Code |
| `skills/interview-prep-builder/` | A Claude Code skill: build interview questions and talking points from your career file. | Optional, Claude Code |

## Go further

See [`docs/optional-extras.md`](docs/optional-extras.md) for installing the Claude Code skills,
the order for adding a scheduled sweep, and notification delivery. See
[`docs/why-it-works.md`](docs/why-it-works.md) for the reasoning behind the design.

## License

MIT. See `LICENSE`.
