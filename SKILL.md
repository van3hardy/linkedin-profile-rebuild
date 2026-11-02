---
name: linkedin-profile-rebuild
description: Reference-led rebuild of a whole LinkedIn profile. Compare the owner's profile with a strong reference profile, rebuild several sections in that structure, show a mockup, then (only after the owner approves) type the approved text into LinkedIn's edit forms in the built-in browser. Use when the user says "use this profile as a guide", "make mine look like this one", "rebuild my LinkedIn from this", or wants a mockup plus live entry across headline, About, Experience, licenses or honors. Not for a profile audit or an isolated About, banner or headline rewrite (use linkedin-profile-optimizer), feed posts (use linkedin-post-writer), or de-AI editing of a post (use linkedin-humanizer).
---

# LinkedIn profile rebuild

Compare a strong reference profile, rebuild the owner's profile in that structure, show a mockup, let the owner pick changes, then enter the approved text on LinkedIn in the built-in browser.

Work in four phases. Do not start the next phase until the owner has approved the one before. Edits on a public profile are visible at once, so putting anything live needs an explicit "put it live" from the owner.

## Inputs to collect first
Ask once, in one short list, before Phase 1. Anything unknown becomes a `[NEED: ...]` flag, not a guess.
- The owner's profile URL and the reference profile URL (or a capture of it).
- Where the evidence lives (source files, confirmed owner statements) and any confidentiality file.
- Target sections, and which are off limits.
- Owner-specific constraints, for example a profile frame or banner that must stay as it is. Take these from the owner or the project task. Never assume one, and never override a change the owner asked for.
- Unresolved facts that block copy: certification issuer, an ambiguous honor or date, award counts, whether an internal award may be named. Collect these now so the owner answers once.

## Rules that apply throughout
- **Truth only.** Every claim gets an evidence row (a source file, a confirmed owner statement, or the live profile). No invented titles, numbers or dates. If evidence is missing, leave the item out and say so, or mark `[NEED: ...]`.
- **Public-safe.** Public copy describes the kind of problem solved and the kind of result. Leave out: internal metrics, headcounts, availability percentages; site names and codes; equipment names; internal processes, workflows, station procedures and detailed operational steps; safety incidents; manager, coworker and personnel records; internal program or course names; internal documents. If the project has a confidentiality file, read it first and follow it over anything here.
- **Owner counts are the owner's.** If the owner states a count ("7 times"), use it and label it in the evidence table as the owner's own count.
- **Never share or publish.** Do not post anything, including the "share your certification" prompts LinkedIn shows after saves.
- **Never authenticate.** Do not type passwords, MFA or recovery codes, or complete "verify work email" or other identity checks. If LinkedIn asks for any of them, stop and ask the owner to do it. Why: the credentials are the owner's, and a mistyped or automated attempt can lock the account.
- **Deletes belong to the owner.** The app's safety check blocks them anyway, and they cannot be undone.
- **Owner reply style:** plain, short, results rather than process.
- Log the owner's verbatim decisions in the project's confirmation log if it has one, one numbered item each, so later sessions do not re-ask.

## Phase 1: Reference compare
1. Capture the reference profile read-only, sections only (headline, About, Top skills, Experience, Licenses, Courses, Honors). Drop other people's suggestions and sidebars.
2. Take **structure, depth and tone only**. Never copy a sentence, and never name or quote the reference person in any deliverable. Why: the profile must be the owner's own voice, and naming a third party is a privacy problem.
3. Write a short "reference does X -> our version" table covering: headline pattern, About shape, Top skills, how the current role is split, how older roles read, which sections exist, what is left out. Add a row for anything skipped for lack of evidence (for example Languages, Volunteering, Financial Management).
4. State the gaps up front: titles the owner never held, sections with no evidence. Show growth through scope, not an invented rank.

## Phase 2: Build the profile in that structure
- **Headline:** `<Title> @ <Company> | <Field> | <keywords> | <years>`. Use the real current title. Offer 2-3 lengths if the owner wants more; LinkedIn allows 220 characters. Count characters.
- **About:** first person, two dense paragraphs. The first two sentences show before "see more", so they carry years and scope. Paragraph two covers what I manage, standards I keep, a people-first close, and awards in one clause. Follow with five Top skills.
- **Current role:** labeled sub-sections, each a short paragraph starting "I ...": Operations Management, People Management, Relationship Management, Safety & Quality Management. Skip Self-Management and Financial Management unless evidence exists. If the owner started recently and no duties are on record, build the sections only from duties in earlier roles and flag that to the owner.
- **Most recent earlier role:** the same labels.
- **Older roles:** one first-person paragraph or 3-5 "I ..." bullets each, showing growth in scope.
- **Licenses & certifications:** generic names from evidence only. LinkedIn requires an issuing organization, so put the issuer on the unresolved-facts list. Never list a failed assessment.
- **Honors & awards:** list every one, with counts the owner confirms.
- **Projects:** lower on the page. Keep one story: side interests (music, AI) stay in Projects or Featured, not in the About.
- **Copy pass:** run copy-editing's AI-tell check and linkedin-humanizer's audit. Repeating "I" is fine because the reference shape does it, but each sentence must add a new fact.
- **Evidence table** under every section, in the paste-ready .md.

## Phase 3: Mockup
1. Produce one self-contained LinkedIn-look HTML file with images inlined (base64), so it opens anywhere. Also produce a paste-ready .md with Before / After / Reason / Evidence per section. Put the owner flags and the unresolved-facts list at the top.
2. Render to check it, using headless Edge or the built-in browser (if one is unavailable, use the other). Use an iframe-offset wrapper at 1024px wide, capture in 800px vertical steps at 1.5 scale, and drop any capture whose file size shows it is blank. Then look at the header (does the headline wrap?) and the longest sections.
3. Show the owner and wait for picks. Log their verbatim words. Revise as many times as asked. Nothing is posted at this stage.

## Phase 4: Put it live in the built-in browser
Only after the owner says to put it live. Read [references/live-entry.md](references/live-entry.md) before the first edit: it has the edit URLs, how to find profile and item ids, how to enter each field type, the add-position flow (opened through the Experience "+" button, never a guessed URL), and the redirects you will meet.

**Say these limits to the owner first:**
- Deleting skills and other deletes are blocked by the app's safety check, so the owner does them.
- LinkedIn has no skill pin or reorder. The newest-added skill shows first. The workaround is deleting and re-adding in reverse order, which loses endorsements, so only do it if the owner accepts that.
- Honors shows two entries, then "Show all". That is normal.
- File uploads (banner, photo, Featured images) need the owner to pick files.

**Per-section loop** (one section at a time, never batch several unverified edits):
1. Open the section's edit form and note the current value (for the headline, snapshot it in full).
2. Enter the approved text.
3. **Read the value back with JS before Save** and compare it to the approved .md: plain inputs, selects, typeaheads, dates and rich text alike. A stale screenshot can look right while the submitted value is wrong, so trust the JS read.
4. Save, then confirm the page is the one you expect. After any redirect, return to the profile and check the section before moving on (see the live-entry reference).
5. Reload and read the saved section back. If it differs from the approved text, stop and fix it before the next section. When an edit changes anything near the headline (adding a position), re-read the headline too.

## Verify live
1. After the last save, reload the profile and read every edited section with JS; compare to the approved .md word for word.
2. Send the owner top-to-bottom screenshots.
3. List what was not done (deletes, uploads, reorder) and who does it.

## Reporting
Say what changed, what the owner still has to do by hand, and anything flagged but undecided. Keep it short.
