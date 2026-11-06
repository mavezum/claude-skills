---
name: job-search-intake
description: Interview the user about their job search goals, constraints and experience, then write their "Job Search Profile" Google Doc that the job-hunt, cv-builder and interview-prep skills all read. Use when the user says "set up my job search", "start the intake", "interview me about my job search", "update my profile", "change my job search criteria", "add a company to my blocklist", or is starting a job search and has no profile yet. Medium-depth interview (about 30–45 minutes), one topic at a time, with pushback on vague answers.
---

# Job Search Intake

Run a structured interview and turn the answers into one document: the **Job Search
Profile**. Every other skill in this kit depends on it, so precision here saves hours later.
A vague profile produces a noisy job digest and generic CVs.

The template is in `assets/profile-template.md`. Read it before starting. Keep its section
headings exactly; the other skills find sections by heading name.

## How to interview

- **One topic per message, 3–6 questions per topic.** Use the AskUserQuestion tool (or the
  multiple-choice input tool, whichever is available) for questions with clear options;
  ask open questions in plain chat.
- **Push back on vague answers.** "Anything in tech" or "flexible on salary" gives the
  search nothing to work with. Ask for the number, the city, the title. Offer examples to
  choose from when the user is stuck.
- **Challenge contradictions politely and immediately.** Examples: a salary floor far above
  what the target titles pay in that city; "fully remote" plus "only Munich companies";
  "part-time" plus "Head of" roles. Name the trade-off, let the user decide, record the
  decision.
- **Separate hard limits from preferences.** For every constraint ask: "If a job were great
  in every other way, would this alone make you say no?" Yes → Hard limits. No →
  Preferences. Most people put too much in Hard limits; that hides good jobs.
- **Never pressure anyone to share personal context.** Childcare, health, caregiving, permit
  status: ask once, gently, say it is optional and only used to filter jobs. Record only what
  the user volunteers, in their words.
- **Be warm and brief.** Many users are job hunting after an involuntary exit. Do not dwell
  on it, do not cheerlead. Be practical.
- Write in the user's language. Default to English.

## Interview topics, in order

1. **Starting material.** Ask the user to upload their current CV and/or their LinkedIn
   profile as PDF (LinkedIn: profile → "More" → "Save to PDF"). Read them first, so later
   questions confirm facts instead of asking from zero.
2. **Target roles.** What roles, which 2–4 role families, seniority range, people
   leadership yes/no. Suggest families based on the CV if the user is unsure. For each family
   collect English and German search titles (e.g. "Project Manager / Projektleiter").
   More than 4 families is a sign of an unfocused search: say so, and help merge or drop.
3. **Location and working model.** City, maximum commute (in minutes, door to door) and how
   they commute (do not assume a car), relocation, minimum home-office days, fully remote
   acceptable or wanted.
4. **Money and contract.** Salary floor as gross EUR per year. If the user does not know
   their market value, offer to look up ranges for the target titles and city (StepStone
   Gehaltsreport, kununu, Glassdoor, Entgeltatlas der Bundesagentur für Arbeit) and
   show the range with sources. Full-time / part-time and hours. Contract types accepted.
   Earliest start date.
5. **Sectors and companies.** Sectors ruled out (ask about common ones: defence, gambling,
   tobacco, fossil fuels, adult, crypto), sectors loved, company size/stage. Blocklist:
   ask explicitly whether to add the former employer and any companies they already applied
   to and were rejected by recently.
6. **Language and permit.** Workplace language they can work in, with honest German and
   English levels (CEFR A1–C2). Work permit situation, framed as: "Do you need the new
   employer to sponsor or approve a work permit?" If the user's permit depends on their
   employment, recommend once that they check their deadlines with the Ausländerbehörde or
   an advisor. Give no legal advice.
7. **Personal constraints (optional).** Anything the job must fit around. Record verbatim.
8. **Experience and skills.** Walk through each role from the CV: confirm dates, scope,
   one or two results with numbers where honest. Then build two lists: **Confirmed skills**
   (used for real, could discuss in an interview) and **Gaps** (things the target roles
   often ask for that the user does not have). Gaps matter as much as skills; they stop
   the other skills from overclaiming.
9. **Delivery.** The personal email address for job digests, and how often to search
   (default: every 2 days in the morning). Daily is often noise; weekly is too slow in an
   active market.

## Write the profile

1. Fill the template with the answers. Remove all `<!-- -->` comments and example text.
   Write "none" in empty sections instead of deleting them. Set "Last updated" to today.
2. Show the full profile in chat and ask the user to correct anything. Iterate until they
   confirm.
3. Save it to Google Drive with the Google Drive connector as a Google Doc named exactly
   **Job Search Profile**, in a folder named **Job Search**. The Drive connector is the
   dedicated Claude Google account, which is also where the job digests come from.
   - If the connector cannot create a Google Doc directly, save it as a file in that folder
     and tell the user: open it in Google Drive, then **File → Save as Google Docs**, and
     delete the original file. The final name must be exactly "Job Search Profile".
   - If no Drive connector is connected, give the profile in one copyable block and
     tell the user to create a Google Doc named "Job Search Profile" in the Claude Google
     account's Drive and paste it in.
4. Recommend sharing the folder with the user's personal Google account (Share → their
   personal address → Editor), so they can edit it from wherever they normally work.

## Updating an existing profile

If a profile already exists, read it from Drive first. Ask only about what the user wants
to change, confirm the edited sections, update "Last updated", and save over the same
document. When a hard limit changes, mention that the next scheduled job search will use
it automatically.

## Hand-off

End with the next steps, briefly:
1. Build the base CVs: "build my base CVs" (cv-builder skill), one per role family.
2. Set up the scheduled search: "set up my job search schedule" (job-hunt skill).
3. Before each interview: "prep me for this interview" plus the job link (interview-prep
   skill).

## Rules

- Never invent experience, numbers, or skills. If the CV and the user disagree, ask.
- Never add a skill to "Confirmed" because it seems likely. Only what the user confirms.
- Do not save the profile's personal details (address, family, health, permit, salary)
  into Claude's memory. They belong in the profile document only.
