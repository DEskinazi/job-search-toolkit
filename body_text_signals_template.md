# Body-Text Screen: Template

Job titles are unreliable in both directions. A posting titled "AI Enablement Manager" can turn
out to be a learning-workshop job. "Content and Operations" can be customer marketing. A plain
title can be exactly your work. If your sweep only reads titles, it will miss real matches and
pass along false ones.

This file tells your sweep what to look for in the body of a posting. You edit it. The sweep
reads it on every full run. Phrases here are examples of the idea, not exact strings, so match
close variants.

**Match whole words only.** Short acronyms cause false hits. A sweep once flagged a posting for
"RAG" because the letters appear inside "leverage" and "coverage." Say in this file that an
acronym must appear as its own uppercase word.

## How to fill this in

1. Read five or six postings that are close to your real work and write down the phrases they
   share. Do the same for five or six postings that looked right by title and were wrong.
2. Sort the phrases into the lists below. Strong phrases describe the work you want to own.
   Supporting phrases show up around that work. Red flags describe work you do not want or
   cannot credibly do.
3. Keep the lists short. A list of 80 phrases matches everything and tells you nothing.

## How the sweep uses it

1. For every posting it fetches with a full body, read the body whatever the title says. Never
   skip a posting because its title is off-vocabulary.
2. Apply your normal hard filters first (location, pay floor, anything marked non-negotiable).
3. Record the first three responsibility bullets in your own words. They show what the job
   really is.
4. Note the reporting line if the posting names one. Some lines fit your work and some do not.
5. Count the phrases. Suggested rule: two or more strong phrases, or one strong plus three
   supporting, and no hard red flag, makes a body-match candidate. Do not give numeric scores.
   List which phrases matched and quote them.
6. Report body-match candidates in the log under their own heading, separate from the
   title-based list, with the tier (GOOD / STRETCH / PASS) and the one or two reasons that
   drive it.
7. For a title match whose body shows red flags, say so and downgrade it.

## Strong phrases (the work you want to own)

[List 8 to 12. Example for a knowledge-management field: content governance, content lifecycle,
content ownership, taxonomy, metadata standards, single source of truth, stale content.
Example for a fleet-telematics field: route optimization, vehicle diagnostics, telematics data,
geofencing.]

## Supporting phrases

[List 6 to 10: tools you use, processes that surround the work, kinds of collaboration.]

## Red flags

Group them so you can see why each one is there.

- **Work in the wrong family** (example: marketing campaigns when you want operations).
- **The wrong main activity** (example: training programs when you want systems work).
- **Requirements you do not meet.** Be honest. If a posting makes a skill the core of the job
  and you lack it, that is a PASS, not a stretch.
- **Domain expertise you cannot fake** (regulated fields, specialized equipment, clinical work).
- **Level and authority mismatches** (managing managers, executive presence required, years of
  experience in a domain you lack).

## Process authority (optional, but it catches a lot)

If you want license over how the work is done, look for evidence in the body.

Green phrases: "design the process," "build from scratch," "first hire," "greenfield," "stand
up," "define standards," "own the framework," "own the roadmap."

Red phrases: "execute the playbook," "follow established processes," "support the team's,"
"work the ticket queue," "administer," "carry out the strategy set by."

A posting that matches your field but shows only red process phrases is a downgrade. Say why in
one line.

## Location and schedule notes (optional)

If your constraints include a commute limit or a cap on office days (see the constraint
categories in `application_log_template.md`), write them here so the screen applies them. Two habits help:

- Treat a stated office schedule above your cap as a location PASS.
- If the schedule is not stated, label the posting "cadence unconfirmed." Do not pass it
  silently, and do not assume it is fine.

## Query phrases for web search

Write 6 to 8 searches built from your strong phrases, combined with remote or your region.
Run them alongside your title searches, not instead of them.

## Misleading titles you have seen

Keep a running list in this format: title, employer, what the body showed. It trains your own
eye and tells the sweep which title patterns deserve a second look.
