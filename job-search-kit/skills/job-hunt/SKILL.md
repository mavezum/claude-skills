---
name: job-hunt
description: Search German job boards and company career pages for roles that match the user's "Job Search Profile" Google Doc, reject anything that breaks their hard limits, verify each posting is still open, rank what survives, skip anything already sent in earlier digests, and email the results from the connected Gmail account. Also sets up the recurring scheduled search. Use when the user says "run my job search", "find me jobs", "any new roles", "job hunt", "set up my job search schedule", "change my search schedule", when a scheduled task fires for the job search, or when the user pastes a single job link and asks whether it fits.
---

# Job Hunt

Find roles the user would not have found on their own, filter them hard, and deliver a
short, ranked, verified list by email. Each run reads the profile fresh and checks the sent
digests in Gmail so nothing is repeated.

This skill screens and ranks. It never applies, never contacts employers, never drafts
outreach. Once the user picks a role, hand off to cv-builder and interview-prep.

## Setup assumptions

- **Google Drive connector** and **Gmail connector** are connected to the same dedicated
  Google account created for Claude (not the user's personal account).
- The profile is a Google Doc named **Job Search Profile** in that account's Drive.
- Digests are sent **from** the dedicated account **to** the address under
  "Contact and delivery → Email for job digests" in the profile.

If the profile cannot be found, stop and tell the user to run the intake ("set up my job
search"). In an interactive session, offer to paste the profile into chat instead.

## Modes

| The user says / trigger | Mode |
|---|---|
| "run my job search", scheduled task fires | Full run (steps 1–9) |
| pastes one job link, "does this fit?" | Single check: steps 3–5 for that link, answer in chat, no email |
| "set up my job search schedule", "change the schedule" | Schedule setup (see the end) |

## Full run

### 1. Load the profile
Read the **Job Search Profile** Google Doc. Extract: target role families and search titles,
seniority range, Hard limits, Blocklist, Preferences, Personal constraints, Confirmed skills,
Gaps, digest email address.

### 2. Load what was already sent
Search the connected Gmail account's **sent mail** for earlier digests:
`in:sent subject:"Job hunt —" newer_than:120d`

From each digest, collect every job URL and every **company + job title** pair. A job counts
as already sent if **either** matches:
- the same URL (ignore tracking parameters like `?utm_...`, `refId`, `trk`), or
- the same company and a near-identical title, even on a different site (the same job often
  appears on StepStone, LinkedIn and the company's own page).

Already-sent jobs are excluded from this run entirely. If Gmail search fails, say so at the top
of the digest ("could not check earlier digests — some repeats possible") rather than
silently sending repeats.

### 3. Search broadly
Run **many separate searches**: one per role family × location × source type. One combined
query returns thin results. Search in **English and German** (e.g. "Projektleiter" finds jobs
"Project Manager" misses). Use the search titles from the profile.

**Job boards (Germany):**
StepStone, LinkedIn Jobs, Indeed DE, Xing, Glassdoor DE, **Jobbörse der Bundesagentur für
Arbeit** (very large and often overlooked), Get in IT, GermanTechJobs, Berlin Startup Jobs
(lists startups across Germany), Wellfound, Arbeitnow, and sector boards that fit the
profile (e.g. public sector: interamt.de, bund.de; academia: academics.de; NGOs:
GoodJobs, Talents4Good).

**Applicant-tracking systems: this is where most "hidden" jobs are.** Many companies post on
their own careers page long before (or instead of) the big boards. Search these directly:
- `site:jobs.personio.de` or `site:jobs.personio.com` + title + city
- `site:join.com` + title + city
- `site:boards.greenhouse.io` + title + Germany/city
- `site:jobs.lever.co` + title + Germany/city
- `site:jobs.ashbyhq.com` + title + Germany/city
- `site:*.softgarden.io` + title, `site:*.recruitee.com` + title, `site:smartrecruiters.com` + title

**Company career pages:** for companies in the user's preferred sectors, check their own
careers page.

If you find a new credible source, use it. Prefer more sources over exhausting one.

### 4. Screen against hard limits: reject fast
Fetch each candidate posting's full text (snippets are too thin). Check in this order and stop
at the first failure:
1. **Blocklist** — case-insensitive company name match, including obvious variants and
   subsidiaries. Instant reject.
2. **Location / commute / relocation / home office** — as stated in the profile. "Remote
   (Germany)" passes a remote requirement; "remote, but 3 days in Hamburg" does not pass a
   Munich-only limit.
3. **Sector ruled out** — including companies whose main customer is a ruled-out sector.
4. **Hours and contract type.**
5. **Workplace language** — reject if the posting requires a level the user does not have
   (e.g. "verhandlungssicheres Deutsch" for a B1 speaker).
6. **Salary floor** — if salary is disclosed, compare. If not, estimate from title, level,
   city and company size (kununu, Glassdoor, StepStone Gehaltsreport, levels.fyi for tech)
   and mark it **"estimated — verify"**. Reject only when the estimate is clearly below the
   floor; when unsure, keep it and flag it.
7. **Work permit** — if the profile says sponsorship is needed and the posting explicitly
   excludes it, reject.

### 5. Verify it is still open
Only verified-open jobs may be recommended.
- Fetch the posting on the **company's own careers page or ATS** whenever you can find it.
  Aggregators (Indeed, Glassdoor, LinkedIn reposts) often show closed jobs.
- **Closed / "no longer accepting applications" / 404** → drop silently.
- **Cannot confirm** (aggregator only, page will not load) → may go in the separate
  "Could not verify" note, never in the main list or the apply list.
- **Confirmed open** → eligible.

### 6. Score and research
For each eligible job:
- **Fit:** compare requirements with Confirmed skills and Experience. Name the strongest
  genuine match and the most important genuine gap from the Gaps list. Be honest:
  "no SAP experience", not "opportunity to grow into SAP".
- **Best base CV:** which role family (CV_A, CV_B, …) fits this posting best.
- **Company health** (skip for large established companies and public sector): funding stage
  and date of last round, recent layoffs (search for them explicitly), revenue or customer
  traction, headcount trend. Give a rating, **Strong / Moderate / Weak / Can't assess**,
  plus one line of evidence. Never invent a survival probability.
- **Preferences:** rank up for "Things that rank a job up", rank down (but keep) for
  "Things that rank a job down" and for seniority outside the preferred range.

### 7. Rank
One list, best first:
1. Matches target family and seniority, no rank-down flags: ordered by fit, then company health.
2. Matches, with one rank-down flag (labelled).
3. Stretch roles: one level above or below the preferred seniority, or an adjacent role
   family (labelled "stretch").

Cap the main list at **15**. If more qualify, keep the best 15 and say how many more there
were. If nothing passes, say so plainly. Never pad the list with rejects.

### 8. Write the digest
Subject: `Job hunt — {N} new roles — {DD Mon YYYY}`
Keep the prefix `Job hunt —` exactly. Step 2 relies on it to find earlier digests.

Body:
1. One line: "{N} new verified-open roles since the last digest."
   (Add the Gmail-check warning here if step 2 failed.)
2. The ranked list, one block per job:
   **{Rank}. {Company} · {Job title}**
   {City / remote} · {salary or "est. €X–Y — verify"} · Company health: {rating}
   Match: {strongest genuine match} · Gap: {most important gap or "none major"}
   Use: {CV_A / CV_B …} · Flags: {any labels}
   {URL}
3. **Apply to these:** a numbered list of URLs only, each with a 3–5 word company + role
   tag, in ranked order, verified-open jobs only.
4. **Could not verify:** short, clearly separated, only if any. Not recommended.

Write plainly. No hype, no "exciting opportunity".

### 9. Send
Send the digest with the Gmail connector from the dedicated account to the digest address in
the profile. **Send it; do not just create a draft.** Scheduled runs have nobody watching.
If sending fails, put the full digest in the session output and state clearly that the
email was not sent and why.

Also show the digest in the session.

If zero new jobs qualify, still send a one-line email ("No new verified-open roles today.
Searched: {list of sources}.") so the user knows the run happened. Use the same subject
format with N = 0.

## Schedule setup

When the user asks to set up or change the schedule:

1. Confirm the profile exists in Drive and both connectors are connected. Run one full search
   now so the user sees a real digest before automating. Fix problems first.
2. Make sure the Gmail connector is allowed to **send without asking each time**. By default
   Claude asks for approval before sending, and a scheduled run cannot get that approval.
   Tell the user to open the Gmail connector's settings in Claude and set sending to
   "always allow". This is safe because the account is dedicated to Claude and only emails
   the user.
3. Create the scheduled task. If a scheduling tool is available in this session, create it
   directly. Otherwise walk the user through: left sidebar **Scheduled → New task**, or type
   `/schedule` in a chat. Use:
   - **Name:** Job search digest
   - **Frequency:** from the profile (default: every 2 days, early morning)
   - **Prompt:**
     > Use the job-hunt skill to run a full job search. Read my "Job Search Profile" Google
     > Doc from Google Drive, check earlier "Job hunt —" digests in sent mail so nothing
     > repeats, and email the new digest to the address in my profile. Send the email
     > without waiting for approval.
4. Tell the user: scheduled tasks run in the cloud even when the computer is off. They can
   see past runs under **Scheduled** in the sidebar, and pause or edit the task there.
5. To change what is searched, edit the profile, not the task. The next run picks it up.

## Rules

- Hard limits are hard. Never show a job that breaks one, however good it looks.
- Never recommend an unverified job in the main list or the apply list.
- Never overstate fit. A gap the user listed is a gap.
- Never apply, contact anyone, or create accounts on job sites.
- Do not save the user's personal details into Claude's memory.
