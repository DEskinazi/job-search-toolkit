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
3. **Run the guided setup.** It interviews you one question at a time and writes your three files.
   One of them, `career_knowledge_base.yaml`, is in a plain-text format called YAML. You don't need to
   know it. The assistant writes it from your answers, checks that it is valid, and reads the facts
   back to you in plain English. You correct it by telling the assistant, or by editing a line.
   - **Claude Code:** copy `skills/job-search-setup/` into `~/.claude/skills/`, then say "set up my
     job search" and point it at your folder.
   - **Any other chat:** open [`docs/guided-setup-prompt.md`](docs/guided-setup-prompt.md), paste the
     prompt, then paste in your documents.
   - **Prefer to fill in the templates yourself?** Open `career_knowledge_base_template.yaml`,
     `llm_context_template.md` and `application_log_template.md` and follow the instructions at the top of each.
4. **Try it on one posting.** The setup ends with this. Later, give your LLM your files and any
   posting, and ask it to tier the role (GOOD, STRETCH or PASS) and to say which requirements you
   meet, which are a stretch, and which are gaps.
5. **Fix errors at the source.** When a draft gets a fact wrong, correct it in your career file
   right away, so the same mistake does not come back.

That is the whole core toolkit.

## Before you set up a daily search

The setup can end with a search that runs every day on its own. Know these things first:

| What to know | Details |
|---|---|
| **It needs a tool with scheduled cloud agents.** | Claude Code has them. Other assistants may not. If yours cannot run a schedule, you can still run the search by hand, as often as you like. See [`docs/using-a-different-tool.md`](docs/using-a-different-tool.md). |
| **Your files go in a private repository.** | A cloud agent can only read files it can reach. Use a **private** repository that you own. Never put your files in a public one. |
| **Private details stay out.** | The assistant makes a search-safe copy. Family, health, finances and names are removed or generalized. You approve what goes in before anything is created. |
| **It keeps running until you stop it.** | There is no expiry. Say "stop my search" and the assistant deletes it. It can also change the time or pause it. |
| **It uses your plan's usage.** | Each run counts. Check your plan's limits before choosing more than one run a day. |
| **A timer inside an open window is not the same thing.** | It stops when you close the window and expires after about a week. The assistant must tell you before creating one. |
| **It only reads public postings.** | It cannot see roles filled by referral, roles behind a login or boards that block automated reading. It supports your own searching and does not replace it. |

## What's in here

| File | What it is | Needed? |
|---|---|---|
| `career_knowledge_base_template.yaml` | The source of truth for your career facts, one small field per fact: roles, scope, accomplishments with who did what, gaps, and dated corrections. | Core |
| `llm_context_template.md` | The briefing version, written from the YAML in plain prose, plus scope boundaries and a glossary so generated documents stay consistent. Paste it into any LLM. | Core |
| `application_log_template.md` | Your search constraints, a GOOD / STRETCH / PASS framework with hard filters, and a log for comparing opportunities. | Core |
| `job_sweep_agent_template.md` | A prompt for a scheduled agent that checks job boards for you on a recurring basis. | Optional |
| `body_text_signals_template.md` | The phrases and red flags that tell your sweep what a posting is really about, so it reads bodies and not only titles. | Optional, with the sweep |
| `search_lanes_template.md` | Methods for searching posting text directly, and for boards that return titles only. | Optional, with the sweep |
| `sweep_changelog_template.md` | A format for recording why your search methods changed, with examples. | Optional, with the sweep |
| `skills/job-search-setup/` | A Claude Code skill that interviews you, builds your three files, and can then run a first search from your rules. The paste-in version for other chats is `docs/guided-setup-prompt.md`. | Recommended |
| `skills/job-fit-analysis/` | A Claude Code skill: fetch the real posting, check it against your facts, give an honest tier. | Optional, Claude Code |
| `skills/interview-prep-builder/` | A Claude Code skill: build interview questions and talking points from your career file. | Optional, Claude Code |

## Go further

Not using Claude, or want a search to run while you are away? See
[`docs/using-a-different-tool.md`](docs/using-a-different-tool.md) for what each part needs, why
things fail on other tools, and how to adapt them.

See [`docs/optional-extras.md`](docs/optional-extras.md) for installing the Claude Code skills,
the order for adding a scheduled sweep, and notification delivery. See
[`docs/why-it-works.md`](docs/why-it-works.md) for the reasoning behind the design.

## License

CC BY-NC 4.0: free to use, share and adapt for non-commercial purposes with credit. Commercial use
(selling it, coaching, outplacement or a skill marketplace) needs permission: contact the author
through GitHub at https://github.com/DEskinazi. See `LICENSE`. Earlier versions were released under MIT.
