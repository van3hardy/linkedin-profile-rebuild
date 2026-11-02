# Live entry on LinkedIn (Phase 4 mechanics)

Read this before the first live edit. All of it assumes the owner has said "put it live" and is signed in already. Never enter credentials or verification codes (see SKILL.md); if a sign-in or identity prompt appears, stop and hand control to the owner.

## Finding ids
- **Profile id:** the part after `/in/` in the owner's profile URL. Ask the owner for the URL first.
- **Position and skill ids:** open the profile read-only, then read the `href` of each Experience item's edit (pencil) link and each skill's edit link. The ids are in those URLs. This method has not been verified end to end in this repo; if a link does not expose an id, ask the owner to open the form and send you the URL rather than guessing a number.
- **Items with no id yet** (new About, honor, certification) use the `/new/` forms below.

## Edit URLs
Prefix with `https://www.linkedin.com` and open in the built-in browser.
- Intro / headline: `/in/<id>/edit/intro/` (the headline is a contenteditable DIV: click it, Ctrl+A, type)
- About and Top skills: `/in/<id>/edit/forms/summary/new/`
- Experience entry: `/in/<id>/details/experience/edit/forms/<positionId>/`
- Honor: `/in/<id>/edit/forms/honor/new/`
- Certification: `/in/<id>/edit/forms/certification/new/`
- Skill: `/in/<id>/details/skills/edit/forms/<skillId>/`

## Entering text
- **Plain textareas and inputs:** focus, select all, `document.execCommand('delete')`, then `document.execCommand('insertText', false, text)`.
- **Selects:** set the value with the native `HTMLSelectElement` value setter, then dispatch a `change` event.
- **Rich text (About, Experience descriptions):** focus via JS, then keyboard Ctrl+A, Delete, and type. Return makes a new line, Return Return a blank line. Read `innerText` back and compare before Save.
- **Typeaheads (Top skills, certification issuer):** type with the keyboard, then pick the `[role=option]` result (or a `find` result). Never leave free text. Typing twice doubles the text, so read the value before typing again.
- **Save:** click the last enabled button whose text is "Save".
- **Readback before Save, every field type:** read the value with JS and compare it to the approved text. This is not only for rich text. A wrong value caught here costs nothing; one caught after Save is already public.

## Adding a position
Adding a new Experience position has been reported to overwrite the profile headline with the new title. There is no known add-position URL, so open the form through the UI and never invent a route.
1. Snapshot the full headline from the intro form before anything else.
2. Open the profile page, find the Experience section, click its "+" (Add) button, then choose "Add position". Find the button by its accessible name or label, not by position on the page.
3. Read `location.href` once the form is open and record it in your notes. That is the verified add-form URL for this owner; reuse it instead of retyping a route.
4. If the "+" button or the "Add position" choice is not found, stop and ask the owner to open the add-position form and send you its URL. Do not guess a path.
5. Fill the form, read every field back before Save, save, then re-open the intro form and read the headline back.
6. If the headline changed, restore the approved headline and read it back again before continuing.

## Dates
Honors with a year but no month save as January. Ask the owner for the month, or tell them what will be saved.

## After Save: redirects and prompts
After saves LinkedIn may redirect to an upsell, "people you may know", a "verify work email" page, or a "share your certification" prompt.
- Do not click Share, Post or Verify, and do not type anything into them.
- Navigate back to the profile or edit URL directly (do not rely on the browser Back button), then reload and read the section you just saved. A redirect does not prove the save happened, and it does not prove it failed.
- If the work-email page appears when opening the Experience form, treat it as an identity check: stop and ask the owner to complete or dismiss it, then re-open the form.
- If a saved value is missing or wrong, re-enter it once. If it fails again, stop and report to the owner instead of retrying.

## Environment gotchas
- Screenshots in the pane can lag. Trust JS reads of field values over what a screenshot shows.
- The profile page scrolls inside `main#workspace`, not the window. Scroll that element before taking screenshots.
- The app's safety check blocks deletes, so the owner handles them.
