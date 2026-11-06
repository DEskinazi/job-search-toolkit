# Search Lanes: Template

Your title scan misses roles whose titles do not match your vocabulary, and some job boards
return titles only. These lanes search the text of postings instead. Together with
`body_text_signals_template.md` they make up one lane in your sweep, called "lane 9" below.

**Change methods in this file, not in the sweep prompt.** A prompt change means resending the
whole prompt. A file change is a normal commit, and the sweep reads the file on every full run.

All results go through the same screens as everything else: hard filters first, then the
body-text screen. Report candidates under a heading such as "Title-miss, body-match," and name
the lane that found each one. Skip roles already in your log.

## 9a. Applicant-tracking systems whose search covers the full posting text

Some systems search the whole posting, not only the title. Workday is one. A search for a
phrase on one employer can return postings whose titles do not contain it. Do not filter those
results by title. Read the posting.

For each employer on a Workday-hosted board:

1. POST `https://{host}.myworkdayjobs.com/wday/cxs/{tenant}/{site}/jobs` with JSON
   `{"appliedFacets":{},"limit":20,"offset":0,"searchText":"<phrase>"}`. The results are under
   `jobPostings`.
2. Use one search per strong phrase from your signals file. Page with `offset`, up to about 60.
3. De-duplicate by `externalPath` and drop postings already in your log.
4. Fetch each remaining posting at `https://{host}.myworkdayjobs.com/wday/cxs/{tenant}/{site}{externalPath}`.
   The description is in `jobPostingInfo.jobDescription` (HTML). Read it and apply the
   body-text screen. Cap detail reads at about 30 per employer per run, newest first.
5. Record every working host, tenant and site, one per line, in `workday_sites.txt`, so the
   next run does not rediscover them.

## 9b. Employers on other public job APIs (example: SmartRecruiters)

If a Workday search errors out for an employer, check whether it posts somewhere else with a
public API. SmartRecruiters is one.

1. GET `https://api.smartrecruiters.com/v1/companies/{company}/postings?q=<phrase>&limit=100`.
   The `q` match is loose, so expect noise.
2. GET `https://api.smartrecruiters.com/v1/companies/{company}/postings/{id}`. The text is under
   `jobAd.sections`.
3. Apply your filters, then the body-text screen.
4. Keep a short "already known, do not resurface" list so applied or passed roles stay quiet.

## 9c. A monthly hiring thread (example: Hacker News "Who is hiring")

Startups post full job text in a monthly "Ask HN: Who is hiring?" thread.

1. Find the newest thread: GET `https://hn.algolia.com/api/v1/search_by_date?query=who%20is%20hiring&tags=story,author_whoishiring`.
2. Search its comments: GET `https://hn.algolia.com/api/v1/search?tags=comment,story_{id}&query=<phrase>&hitsPerPage=50`.
3. Read each hit, keep roles that meet your location rules, and apply the body-text screen.
   Early-stage pay can sit below your usual floor, so apply your existing rules for equity and
   for pay as a signal.
4. Run once a month, in the first ten days. On other days, write "9c not due."

## 9d. Adjacent titles and fields

Titles and employer types your sweep did not search before. List them with the phrases that
identify each, run them on every full pass, and report them under their own heading. Apply your
filters plus two extra tests:

- **Pay works.** State your minimum, and say how to treat a role between your usual floor and
  that minimum (STRETCH, and the entry says so). For contract work, convert to a yearly
  equivalent and add a premium for having no benefits.
- **Process authority.** Does the posting say you would design, build or own the process? A role
  that only executes someone else's playbook fails.

Each entry should name the adjacent field, why your skills transfer, and the phrases to search.

## 9e. A third tier, and boards you have not scanned yet

Tier 1 is your main lane. Tier 2 is lane 9d. Tier 3 is work outside your field that your
credentials and skills still fit. List the titles and phrases, and add a "do not log" list of
work that repeats your red flags.

Add every hosted board you find. Two public ones worth knowing:

- **Ashby:** `https://api.ashbyhq.com/posting-api/job-board/{slug}?includeCompensation=true`. The
  results are under `jobs`.
- **Lever:** `https://api.lever.co/v0/postings/{slug}?mode=json`.

Keep one file per platform (`ashby_boards.txt`, `lever_boards.txt`) listing known slugs, and add
a slug whenever a posting URL shows you one.

Two lessons that cost a missed posting each:

- **Do not trust a board's `isRemote` field.** On one platform it was true for in-office and
  hybrid roles. Use the workplace type field and the location, and read the body for office-day
  expectations.
- **Check the employer named in the body.** One slug returned another company's postings.

## Boards that return titles only

Some boards cannot be screened by body. List them in each day's entry as "unscreened" so you can
see the blind spot instead of forgetting it.

## Reporting

In each entry, for every lane, say whether it ran, how many postings were read, and any
employer or board that could not be searched and why. End the coverage line with a "done" or
"skipped" note per lane.
