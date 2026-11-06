# Why this works

The reasoning behind the toolkit, for anyone who wants it before or after setting up.

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


## How the files work together

`career_context_template.md` answers "what's actually true about me." `application_log_template.md`
answers "given what's true about me, does this specific opportunity make sense." `job_sweep_agent_template.md`
reads both of the above and automates the ongoing search itself. Keep company-specific tailoring
notes out of the first file, and keep your core facts out of the second — duplicating them risks
drift, where a correction made in one place never makes it to the other.

