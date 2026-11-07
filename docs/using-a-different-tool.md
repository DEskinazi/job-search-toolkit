# Using a different tool, or running when you are away

The toolkit was built and tested with Claude Code. You do not need a Claude account to use most
of it. This page explains what each part needs, what breaks without it and why, and how to adapt
the pieces for another assistant.

## What each part needs from your tool

| Part | What the tool must be able to do | Works in a plain chat? |
|---|---|---|
| Your facts files (`career_knowledge_base.yaml`, `llm_context.md`) | Ask you questions and give you text back. You save the files yourself. | Yes. Use `docs/guided-setup-prompt.md` and copy each file into your folder as you go. |
| Search rules (`application_log.md`) | Same as above. | Yes. |
| Tiering one posting you paste in | Read text you paste. | Yes. |
| Tiering a posting from a link | Open web pages. Many chats cannot, or return a summary instead of the real page. | Only if your chat has web access. Otherwise paste the posting text. |
| Setup skills (`skills/`) | A tool that loads skill folders, such as Claude Code. | No. Paste the prompt instead. The skill text is the same interview. |
| Running a first search (Phase 6) | Read files in your folder, fetch web pages and public job feeds, write files back. | No. A plain chat cannot do this. |
| A search that runs while you are away | A scheduler that starts an agent on a timer, with its own web access and a place to save results. | No. See below. |

## Why things fail on another tool

- **"I can't open that link" or a vague summary.** The tool has no web access, or it blocks
  automated reading. Paste the posting text. Never trust a summary of a posting, because summaries
  get pay and location wrong.
- **It forgets your files.** A plain chat cannot read your folder. Paste `llm_context.md` at the
  start of each session, and `application_log.md` when you want a posting judged.
- **It cannot save files.** Copy each file out of the chat yourself, or the next session starts
  from nothing.
- **The skill does not load.** Skills are a Claude Code feature. Other tools ignore the folder.
  Paste `docs/guided-setup-prompt.md` instead.
- **The search finds nothing, or says "blocked."** The tool may not be allowed to reach job
  boards. Public feeds from systems such as Greenhouse, Lever, Ashby and Workday are plain web
  addresses, so any agent that can fetch URLs can read them. A tool that cannot fetch URLs cannot
  run the search.
- **A different model reads the rules differently.** Smaller or older models skip steps, mix up
  tiers or invent facts. If results look wrong, shorten the prompt, ask one step at a time, and
  check each claim against your YAML.

## Running a search when you are not at your computer

The toolkit's default is a daily search in the cloud that keeps running, with your computer off,
until you tell it to stop. It needs a tool with scheduled cloud agents and a **private** repository
for your files, because a cloud agent can only read what it can reach. Your private details stay
out of that repository (the setup skill makes a search-safe copy). If your tool cannot do this, the
other options below are the fallbacks.

Nothing runs by itself. A search runs unattended only if something starts it on a schedule. Pick
the option your tool supports.

| Option | Needs | Works with your computer off? | Notes |
|---|---|---|---|
| In-session schedule (a timer inside your open assistant window) | An open session | No. It stops when you close the window and expires after about a week. | Good for a short test. It is easy to mistake for a real unattended search. |
| Scheduled agent in your assistant (for example Claude Code's scheduled routines) | An account with that feature | Yes | It runs in the provider's cloud. Give it the sweep prompt, your three files in a repo it can read, and a place to write results. Each run starts fresh, so the repo is its memory. |
| A script on your own computer (cron on Mac or Linux, Task Scheduler on Windows) that calls your assistant's command line or API | A tool or API you can call from a script | No. The computer must be on and awake. | You write the script. |
| A scheduled GitHub Action that calls an LLM API | A GitHub account and an API key | Yes | The most setup. Store the key as a secret, never in the repo. |
| Manual | Nothing | No | Rerun the search when you want one. Works with any tool that can fetch web pages. |

Times are in UTC on most schedulers. Convert from your time zone, and remember that daylight
saving shifts the local time by an hour twice a year.

## Adapting the prompts for another LLM

1. **The files are plain text.** Markdown and YAML work in any tool. Nothing in them is specific
   to Claude.
2. **The sweep prompt** (`job_sweep_agent_template.md`) is a normal written instruction. Paste it
   into any agent that can read files, fetch URLs and write files. Replace any tool names in it
   with what your tool calls them.
3. **The job feeds** are ordinary web addresses. The tool only needs to fetch a URL and read JSON
   or HTML. Check that it can, with one test posting, before you build on it.
4. **Test on one posting you already know the answer to.** If the tool tiers it the way you
   would, it is reading your rules. If not, the cause is almost always missing web access, a
   missing file or a model that skips steps.

## If something does not work

Ask your assistant: "Which of these can you do here: read files in my folder, fetch a web page,
save a file, run on a schedule?" Then match the answers to the first table. What it cannot do is
the reason.
