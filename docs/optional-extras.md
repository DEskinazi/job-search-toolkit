# Optional extras

You do not need anything on this page to get value from the toolkit. The core is the two files in the README quick start. Come back here when you want more.

## Claude Code skills

If you're using Claude Code specifically (not just any LLM chat), two ready-to-use Skills live in
`skills/`:

- **`skills/job-fit-analysis/`** — formalizes the "fetch the real posting, check it against my
  facts, give me an honest tier" workflow described in the README quick start, so it triggers automatically whenever
  a job posting comes up in conversation instead of depending on you remembering to ask for it
  every time.
- **`skills/interview-prep-builder/`** — builds likely interview questions, answer structure, and
  personalized talking points from your `career_context_template.md`, triggered automatically
  whenever an upcoming interview or screen is mentioned.

To use either, copy the relevant folder into `~/.claude/skills/` (for every project) or a specific
project's `.claude/skills/` directory, alongside your filled-in `career_context_template.md` and
`application_log_template.md`. Both skills are optional — everything they do can also be done by
hand by following the README quick start, with any LLM.


## Adding the optional layers, in order

Steps 1 to 5 are the README quick start. After them, add layers one at a time, and only when the
last one is working.

| Step | What to do | Notes |
|---|---|---|
| 6 | Copy `skills/job-fit-analysis/` and `skills/interview-prep-builder/` into `~/.claude/skills/`. | Claude Code only. They then trigger automatically instead of needing to be invoked by hand. |
| 7 | Fill in `job_sweep_agent_template.md` and schedule it. | An automated, recurring check of job boards on top of your own manual searching, not a replacement for it. |
| 8 | Once titles stop turning up new matches, fill in `body_text_signals_template.md` and `search_lanes_template.md`, and start a changelog from `sweep_changelog_template.md`. | This makes the sweep read posting bodies, not only titles. |
| 9 | Wire sweep alerts into a messaging API (see the next section). | Weigh the tradeoff described there first. |

## Notification delivery beyond desktop and phone push

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

