# PROFESSIONAL CONTEXT: [YOUR NAME]

This document is a structured, fact-checked representation of your professional experience,
scope, and boundaries. Feed this to an LLM as authoritative context for any generation task
(resumes, cover letters, blurbs, interview prep, positioning). The core rule this file exists to
enforce: **the LLM should never write a claim about you that isn't traceable back to this file.**
If a resume draft says something this file doesn't support, that's a bug in the resume, not a
gap in the file — fix the file first (after verifying the fact with yourself), then regenerate.

Fill in every `[bracketed]` section. Delete this instructions block once you've read it.

---

## HOW TO SET THIS UP (read once, then delete)

1. **Do not start from a blank page. Gather everything you have written about your work into
   one folder.** Every resume version (not just the current one), every cover letter, LinkedIn
   exports, performance reviews, project write-ups, and the job descriptions for roles you held.
   Old resumes catch stale or duplicate facts, and a resume written for a different target role
   often describes the *same* underlying work through a genuinely different lens. Those
   alternate framings are useful raw material, even from roles that feel dated. Cover letters
   matter just as much: they show your voice, and they hold context that never fit on a resume.
   Give the whole folder to the LLM in one sitting and ask it to extract every distinct claim,
   achievement, framing and number into a single list, and to describe how you write. **Treat
   old documents as evidence, not as truth.** They often contain overclaims, and versions
   disagree with each other. That is what step 2 is for.
2. **Reconcile that list with yourself, not with the LLM.** For each claim: is it still true, is
   it worded accurately, is the number right, did you actually own that work or just touch it?
   The LLM cannot verify these — only you can. This step is slow and that's the point.
3. **Write the reconciled, correct version into this file**, organized by section (see the
   skeleton below). Prefer plain, specific language over resume-speak. Include things that
   *aren't* resume-ready yet (half-formed accomplishments, context behind a number) — this file
   is your working memory, not the resume itself. The resume gets generated *from* this file.
4. **Keep it updated in place.** Every time you catch an LLM-generated draft overclaiming,
   underclaiming, or getting a fact wrong, that's a signal this file is incomplete or unclear —
   fix it here immediately, in the same session, before touching the resume draft again. Don't
   let corrections live only in your resume; if they don't make it back into this file, you'll
   have the same argument with the LLM again next time.

   **Where the correction actually goes:** inline, directly inside the section the fact
   belongs to — not in a separate changelog at the bottom of the file, which gets skipped and
   drifts out of sync with the sections it's supposedly tracking. Attach a short, dated tag
   right next to the fact itself:

   ```
   Managed a 2-person technical writing team. CORRECTED [date]: earlier drafts said this team
   was "built from the ground up" — inaccurate, the team was inherited plus one hire I made
   later. Use "manage two technical writers, including hiring, mentoring, and performance
   management" instead.
   ```

   or, for a fact you double-checked and are now confident in:

   ```
   CONFIRMED [date]: this is the correct payroll title — an earlier, more descriptive framing
   was misleading about actual scope. Use this exact title on any resume/application.
   ```

   The date and the *why* both matter, not just the corrected value — a bare fix invites the
   same wrong version to quietly resurface later; the annotation is what stops that.
5. **Pair this file with `application_log_template.md`** (see that file's own instructions) —
   this file is about *you*; the other file is about *the opportunities you're evaluating*.
   Keep them separate. Don't let company-specific tailoring notes creep into this file, and
   don't let your core facts get duplicated/drift out of sync across multiple application logs.

---

## CORE IDENTITY

[2-4 sentences. Not a resume summary — a plain description of what you actually do and what
your real expertise is, in your own words. Example shape: "X leader focused on Y, working
primarily in Z." Avoid buzzwords you can't back up with a specific example.]

---

## WORK CONTEXT

List every role, most recent first. For your current or most recent role, note its status
(current / concluded, with an end date if concluded — this matters for keeping resume tense
consistent). For each role, a short list of real focus areas — not bullet points copied from a
job description, but what you actually spent your time on.

### [Most Recent Role] — [Company] ([status], [dates])
Focus areas:
- [...]
- [...]

### [Previous Role] — [Company] ([dates])
Focus areas:
- [...]

[Repeat for every role worth including. Don't skip older roles just because they feel dated —
a skill or pattern from 8 years ago is often the cleanest evidence for an "adjacent domain"
argument later. See KEY ACCOMPLISHMENTS below for where the detail actually lives.]

---

## IMPORTANT SCOPE BOUNDARIES

This is the single highest-leverage section in the whole file. Most overclaiming happens at the
boundary between "what I actually did" and "what's adjacent to what I did." Be explicit about
both sides.

**You do NOT:**
- [thing that sounds adjacent to your work but isn't actually yours — be specific]
- [...]

**You DO:**
- [the real, narrower version of the adjacent-sounding claim above]
- [...]

[Example of the pattern this section exists to prevent: someone who designs *content*
governance for AI-ready data is adjacent to, but not the same as, someone who designs *AI
governance policy*. Both use the words "AI" and "governance." Only one is true of them. Spell
out every boundary like that one, for your own domain.]

---

## KEY ACCOMPLISHMENTS / SYSTEMS

For each substantial piece of work worth citing on a resume, give it its own numbered
sub-section with real detail — not a polished bullet, the underlying story:

### 1. [Accomplishment name]
[What it was, in plain language. Include:]
- The real scope (how many people/teams/pages/dollars — with the caveat if a number is an
  estimate vs. confirmed)
- What you specifically did vs. what a team did around you (be precise about sole ownership
  vs. collaboration vs. handoff — see the note below)
- Before/after or mechanism, if there is one (what was broken, what you built, how it actually
  worked)
- Any correction history worth keeping ("earlier drafts said X, that was wrong because Y,
  correct version is Z") — future-you will thank present-you for this

**On collaboration vs. sole ownership:** be exact about who did what. "I built X" when a
teammate set up the underlying infrastructure and you configured it on top is a real
overclaim, even if it feels like a technicality. The accurate version ("working with an
engineer who set up Y, I built Z on top of it") is *still a strong resume line* — don't
default to inflating it out of fear that precision reads as weak.

---

## HANDLING A CRITERION THAT LOOKS UNMET (gap-scrutiny guidance)

When a job posting lists a requirement you're not sure you meet, don't reflexively treat it as
either "I have this" or "I don't have this." Most real gaps are actually one of these:

1. **You have it, just not under that exact label.** A posting asks for "Agile/SDLC
   experience" — you've never used that phrase, but you've spent your whole career embedded
   with engineering teams shipping on release cycles. That's real experience, described with
   different words. Don't flag this as a gap just because the term itself doesn't appear
   verbatim in your history — but also don't claim a *specific* sub-practice (e.g., "ran sprint
   retros") unless you actually did that specific thing.
2. **You have an adjacent, narrower version of it.** A posting wants "life sciences
   experience" — you don't have a pharma job, but you did a competitive-intelligence contract
   researching drugs in development. That's a real, honest bridge — name it as what it is,
   don't round it up to the full requirement.
3. **You genuinely don't have it, and that's worth saying plainly.** Not every gap needs a
   bridge. Naming a real gap directly, in one honest sentence, usually reads better than
   straining to imply you have something you don't.

The scrutiny level should scale with how *specific* and *verifiable* the requirement is. "5+
years of people management" is a hard, checkable number — don't round up. "Experience with
change management" is a soft, narrative claim — a real example of leading a process change
without formal authority genuinely satisfies it, even if you'd never called it "change
management" before.

---

## LANGUAGE RULES FOR GENERATION

A short verb/phrase glossary keeps every generated document consistent instead of re-litigating
word choice every time. Example shape (replace with your own):

**Use:**
- "designed" → you owned the system-level decisions
- "led" → you directed people or a cross-functional initiative
- "built" → you personally did the hands-on work (see the collaboration note above before using
  this one)
- "partnered with" / "worked with" → real collaboration, not sole ownership

**Avoid:**
- [any phrase that implies authority, scope, or ownership you don't actually have — list your
  own specific danger-phrases here as you catch them]

---

## STANDING STYLE PREFERENCES

[Anything true across every document generated from this file — e.g., "no em dashes," "avoid
[specific clichés]," "keep paragraphs under N sentences," "always use [specific font]." Small
things, but repeating them here means you only have to say them once.]

*(Tip: your own cover letters are the best source for these. Ask the LLM to read them and describe your sentence length, tone, and the words you avoid, then edit that description until it sounds like you.)*
