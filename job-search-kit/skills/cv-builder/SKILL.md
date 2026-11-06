---
name: cv-builder
description: Build 2–4 reusable base CVs (German Lebenslauf conventions, with photo, ATS-friendly) from the user's "Job Search Profile" and old CV, one per target role family, delivered as Word files that open in Google Docs. Optionally make a quick per-job version that changes only the title line, summary and key competencies. Use when the user says "build my base CVs", "make my CV", "update my CV", "which CV should I use for this job", "tailor my CV to this job", "Lebenslauf", or pastes a job link and asks about their CV. Never invents experience.
---

# CV Builder

Earlier versions of this workflow rewrote the CV for every application. It produced good CVs
but took too long per job. This skill does the heavy work **once**: 2–4 strong base CVs, one
per role family. Per application the user picks one of two paths:

- **Path 1 — Use a base CV as-is.** Fastest. The job-hunt digest already names the best base
  CV for each job. Good enough for most applications.
- **Path 2 — Quick per-job version (about 10–15 minutes).** Copy the closest base CV and change
  only three blocks: title line, profile summary, key competencies. Worth it for jobs the user
  really wants.

Let the user choose each time. Do not push Path 2 by default.

## Inputs

1. **Job Search Profile** Google Doc (Drive connector). Use: Target roles (families),
   Experience summary, Confirmed skills, Gaps, Contact details, Languages.
   If missing, ask the user to run the intake first, or to paste their details.
2. **Current CV and/or LinkedIn PDF**: ask the user to upload them if they are not in the
   conversation.
3. **Photo**: ask the user to upload a recent professional headshot (neutral background,
   shoulders up). If they do not have one, the CV can be built with a placeholder and the
   photo added later.

## Before writing anything: ask

Use AskUserQuestion (max 4 questions per round) to settle:
- **Language** of each base CV: English or German. Default: the language most target postings
  use. A second language version can be produced afterwards.
- **Personal details in the header.** German CVs traditionally include photo, address, phone,
  email, LinkedIn; date of birth and nationality are optional and increasingly left out.
  Ask which to include.
- **Which experience to foreground** for each role family, if the profile does not make it
  obvious.
- **Anything in the old CV the user wants dropped** (very old roles, side jobs).

Challenge the plan if it looks wrong. Examples: five role families (too many; merge), a target
family the experience does not support at all (say so and offer an honest stretch
positioning), or gaps in the timeline the user has not addressed (suggest one honest line,
e.g. "Career break: family care" or "Sabbatical", if the user wants it).

## CV structure (same for every base CV)

1. **Header:** name; title line (2–3 short segments separated by " | ", under ~65
   characters); contact details; photo top-right.
2. **Profile:** 3–5 lines of plain prose: who the user is professionally, what they are
   strongest at, what they are looking for. Tuned per role family.
3. **Key competencies:** 4 items, each one real sentence (max 2 lines), most relevant to the
   role family first.
4. **Professional experience:** reverse chronological. Per role: title, company, city, dates
   (MM/YYYY), 3–5 bullets with concrete results. Older roles (10+ years) get 1–2 bullets.
5. **Education:** reverse chronological.
6. **Skills:** grouped (e.g. Tools, Methods, Domains). Only Confirmed skills from the profile.
7. **Languages:** with CEFR levels (e.g. German C1, English C2).
8. Optional: certifications, publications, volunteering. Keep it short.

**Length:** 1 page for under ~5 years of experience, max 2 pages otherwise. Never shrink the
font or margins to fit; cut content.

Only blocks 1–3 change between base CVs and in per-job versions. Blocks 4–8 are identical
across all of the user's CVs. This keeps facts consistent and makes Path 2 fast.

## Format: ATS-friendly with photo

Applicant-tracking systems parse text. They fail on clever layouts.
- Single column. Standard headings ("Professional Experience", "Education", "Skills";
  German: "Berufserfahrung", "Ausbildung", "Kenntnisse", "Sprachen").
- No tables, text boxes, columns, icons, skill-rating bars or charts for content.
- **Photo as a floating image** anchored top-right of page 1, square text wrapping. Not inside
  a table or text box, so the header text stays readable to an ATS.
- One clean font (e.g. Calibri, Arial or Source Sans), 10–11 pt body, consistent dates.
- Real text everywhere: no text inside images.

## Writing rules

The CV must read as written by a careful person, not by AI. These rules beat keyword density.

**Never write:**
- Self-labels: "seasoned leader", "results-driven professional", "passionate about".
- Filler words: seamlessly, robust, cutting-edge, world-class, proven track record,
  leveraging, spearheaded, synergy, holistic, best-in-class, dynamic, drive impact.
- Keyword runs separated by semicolons. Competencies are sentences. A short list of tool
  names at the end of a sentence is fine.
- Ten near-identical bullets in a row. Compress to the two or three that matter.
- The same number repeated in summary, competencies and experience. A metric appears once in
  the top half; the experience section keeps its own.
- "Not just X, but Y" constructions and dramatic dashes.

**Do write:**
- Plain sentences: subject, verb, object. Present tense for the current role, past tense for
  the rest.
- Concrete nouns: tools, standards, team sizes, budgets, customers, systems. These are also what
  ATS and recruiters search for.
- Results with honest numbers where the user can back them up in an interview.

## Honesty rules (non-negotiable)

- Only facts from the profile, the old CV, or confirmed by the user in this conversation.
- Never add a skill that is not under "Confirmed skills". If a posting needs it, ask; if the
  user has it, add it to the profile first.
- Phrase stretches truthfully: "supported", "contributed to", not "owned" or "led".
- If a posting's must-have requirement is genuinely unmet, say so plainly and offer honest
  positioning options. Never paper over it.
- Never inflate tenure, titles or team sizes.

## Workflow: base CVs (Mode A)

1. Read the profile, old CV, LinkedIn PDF. Ask the questions above.
2. Draft blocks 4–8 once (shared). Show them in chat for fact-checking. Fix until confirmed.
3. For each role family, draft blocks 1–3. Show all versions side by side so the user sees the
   differences.
4. Build each CV as a **.docx** (use the docx skill). Name files
   `CV_<LastName>_<Family>_<EN|DE>.docx`, e.g. `CV_Mueller_A-DataAnalytics_EN.docx`.
5. Verify every file: convert to PDF and render the pages to images; check page count, that the
   photo sits top-right without covering text, no broken characters (ä ö ü ß), and that the
   text extracts cleanly in reading order (a quick ATS check). Re-read blocks 1–3 against the
   writing rules: if a sentence could describe any other candidate, rewrite it.
6. Deliver the files in chat. Then save them to Google Drive in **Job Search/CVs** (Drive
   connector) if available. Tell the user: open each file in Google Drive with Google
   Docs to edit, and **export as PDF** (File → Download → PDF) when applying. Most portals
   want PDF.
7. Update the profile's "Target roles" section so each family points to its CV file name.

## Workflow: per-job version (Mode B, optional)

1. Fetch the job posting. If the fetch fails (LinkedIn often blocks it), ask the user to paste
   the text.
2. Pick the closest base CV and say which and why. If it fits well already, tell the user
   Path 1 is enough. Do not edit for the sake of editing.
3. Map the posting's must-haves to Confirmed skills and Gaps. Ask (max 4 questions) about
   anything unclear, especially required tools that are not in Confirmed skills.
4. Change **only** title line, profile and key competencies. Mirror the posting's key terms
   where they are true for the user.
5. Build the .docx as `CV_<LastName>_<Company>_<Role>.docx`. Never overwrite a base CV.
   Verify as in Mode A step 5, and confirm that blocks 4–8 are unchanged from the base.
6. Deliver, save to **Job Search/CVs/Applications**, and list any honest gaps the user should
   prepare to talk about.

## Rules

- Do not save personal details (address, birth date, photo) into Claude's memory.
- Do not write cover letters unless asked. If asked, apply the same writing and honesty rules,
  max one page, and address the specific posting.
