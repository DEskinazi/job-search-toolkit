# Sweep Changelog: Template

Keep a changelog for how your sweep searches, not only for what it finds. When a result looks
off weeks later, you want to know what changed and why. Newest entries first. Each entry has
four parts:

- **What changed.** The file or prompt paragraph, in one or two sentences.
- **Why.** The specific miss or false hit that prompted it. Use real examples.
- **How it was checked.** For a prompt change: the stored text matched the intended text, the
  sweep's repo source was attached, and a test run ran. Say what the test did not cover.
- **Lesson.** One sentence you would give your past self.

## Example entries (from a real sweep, with specifics removed)

### Body-text screen added
**What changed.** Added a signals file and a prompt paragraph: read the body of every posting
fetched, whatever the title says. A posting with enough strong phrases and no hard red flag is a
candidate and is reported under its own heading. Title matches whose bodies show red flags are
downgraded.
**Why.** In one week, five postings with on-vocabulary titles turned out to be a learning
workshop, customer marketing, data-center procedures, conversion-focused onboarding content and
brand marketing. The reverse also happens: a plain title can be exactly the work.
**How it was checked.** A test run flagged postings for a short acronym that appeared inside
other words. The signals file now says to match whole words only.
**Lesson.** Titles are a hint. The body is the evidence.

### Search lanes for boards that return titles only
**What changed.** Added a lanes file: search by body phrase through the applicant-tracking
system, scan a second employer through a different public API, and search a monthly hiring
thread in the first ten days of the month.
**Why.** The body-text screen only works on postings whose bodies are fetched, and several
boards had been scanned by title only. A probe showed one system's search covers full posting
text, so a phrase returned postings whose titles did not contain it.
**How it was checked.** The stored prompt matched the intended text, the repo source was
attached, and a lighter test run exercised each new lane at low depth. The first full-depth run
was the next scheduled one.
**Lesson.** Put method detail in a repo file the run reads, not in the prompt. A prompt change
means resending the whole prompt. A file change is a normal commit.

### Boards that were never scanned
**What changed.** Added a list of hosted boards for two more platforms, and a rule not to trust
an `isRemote` flag.
**Why.** A strong match was posted by an employer on a platform the sweep did not scan, and was
found by hand.
**Lesson.** When a human finds a posting the sweep missed, ask which blind spot let it through
before you add the posting to a list.

### A constraint turned into a rule
**What changed.** A schedule cap (maximum office days per week) was added to the criteria file
and the signals file. An unstated schedule is labeled "cadence unconfirmed" and reported, not
passed silently.
**Why.** A real constraint was being applied inconsistently by hand.
**Lesson.** A constraint you apply by memory will drift. Write it down where the sweep reads it.
