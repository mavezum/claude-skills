---
name: interview-prep
description: Prepare the user for a specific job interview from the job posting. Researches the company (recent news, funding, layoffs, leadership, culture signals), drafts sharp questions to ask the interviewer, rehearses the answers the user will certainly need (why this company, why are you looking, salary expectation), and runs mock questions on the skills the user is least sure of, with honest feedback. Use when the user says "help me prep for this interview", "I have an interview at [company]", "interview next week", "Vorstellungsgespräch", or pastes a job link while job hunting and mentions an interview. Always asks which skills to focus on and who the interviewer is before generating questions.
---

# Interview Prep

The user walks into the interview with four things: a current, accurate read on the company;
questions worth asking; rehearsed answers to the questions every interview contains; and
practice on the topics they are least sure of.

Generic advice ("research the company", "prepare questions") is useless. Everyone knows it.
The value is doing the research **for this posting** and spending prep time where the user
is weak.

## Step 1: Get the posting and context

- Ask for the job link (preferred) or the pasted text. Try fetching the link. If it fails or
  returns a login wall (common with LinkedIn), say so and ask for the text. Never fill gaps
  from the company name alone.
- Read the **Job Search Profile** Google Doc (Drive connector) if available: Confirmed skills,
  Gaps, Experience, salary floor, constraints. Without it, ask the user for their CV.
- Ask, in one round (AskUserQuestion, max 4 questions):
  - **Interview stage and interviewer:** HR / recruiter screen, hiring manager, technical
    or case interview, executive / C-level, panel, or unknown. Names and roles if known.
  - **Date and format** (video / on site, length).
  - **Which hard skills to focus on**: list the hard skills from the posting and let the user
    multi-select the ones they feel least sure about.
  - **What worries them most** about this interview (optional, free text).

Interviewer type changes everything:
- **HR / recruiter:** motivation, salary, notice period, start date, working model, culture
  fit. Few technical details.
- **Hiring manager:** concrete past examples, how you would approach the first 90 days, team fit.
- **Technical / case:** depth on tools and methods; expect to solve or explain something live.
- **Executive:** explain decisions in business terms (cost, risk, speed, customers), not
  implementation detail. Strategy and market questions.
- **Panel / unknown:** blend, and suggest the user asks at the start who they are speaking with.

## Step 2: Research the company

Use web search and fetch. Recency is the point. The user can read "About us" themselves.
- What the company does, how it makes money, size and stage (startup / scale-up / Mittelstand
  / corporate / public).
- Last 12 months: funding rounds, acquisitions, product launches, **layoffs or restructuring**
  (search for them explicitly), leadership changes, major customers, press coverage.
- Signals about the team or role: why it might be open (growth, replacement, new unit),
  related open roles, the hiring manager's public profile or talks if named.
- Culture signals: kununu and Glassdoor ratings and recurring themes in reviews (treat as
  signals, not facts), stated values, working model.
- Anything specific enough to mention naturally in the interview.

If there is little recent news, say so. Do not invent substance. Cite sources.

## Step 3: Rehearse the answers every interview needs

Draft, then refine with the user in chat:
1. **"Tell me about yourself."** 60–90 seconds: current/last role, two relevant strengths with
   one proof each, why this role now.
2. **"Why are you looking?" / "Why did you leave?"** Many users have left involuntarily. Help
   them build a short, true, neutral answer: what happened in one sentence (e.g. "My role was
   one of many affected by a restructuring"), no blame, no over-explaining, then pivot to
   what they want next. Practise until it sounds calm and finished. Never coach them to lie.
3. **"Why us?"** Built from Step 2: two specific reasons tied to real facts about the company.
4. **Salary expectation (Gehaltsvorstellung).** Gross per year in EUR. Use the profile floor
   and current market ranges for this title, city and company size (kununu, Glassdoor,
   StepStone Gehaltsreport, levels.fyi for tech). Give the user a range with their target
   in the lower third, and a one-sentence way to say it.
5. **Practical questions:** notice period / earliest start, working model, travel.
6. **The weak spot.** The most important gap between the posting and the profile. Prepare an
   honest answer: what they have that is adjacent, how they would close the gap, how fast.

## Step 4: Mock questions in chat

- Ask questions on the skills the user selected, calibrated to the interviewer type. Ask in
  batches of 3–5, not 15 at once.
- Use behavioural questions too ("Tell me about a time…") and expect STAR-structured answers
  (situation, task, action, result).
- After each answer, give **honest** feedback: what worked, what was vague, what was
  missing (usually: concrete numbers, the user's own role vs. the team's, the result).
  Push back on answers that dodge the substance. That is the value of rehearsing.
- Offer a second attempt at weak answers.

## Step 5: Deliver the prep sheet

Create a markdown file the user takes into the interview. Scannable, not a wall of text:

```markdown
# Interview prep: [Role] at [Company]
[Date] · [Format] · [Interviewer names and roles]

## Company summary
[4–6 sentences: what they do, stage, last-12-month news, anything to reference. Sources.]

## Answers to have ready
- Tell me about yourself: [bullet version]
- Why I'm looking: [one or two sentences]
- Why this company: [two reasons]
- Salary expectation: [range and sentence]
- Earliest start / notice period: [answer]
- My gap and how I address it: [two lines]

## Stories to use
- [Story name]: [situation → action → result, one line] — fits questions about [...]

## Questions to ask them
[5–8 questions, tailored to the interviewer type. Mix: 2–3 that show real research
(referencing something specific from the company summary) and 3–4 that get information
the user needs to decide: why the role is open, what success looks like after 90 days and
after a year, team structure and who they'd work with most, biggest current challenge,
how decisions get made, next steps and timeline.]

## Notes during the interview
-
```

Save it as `Interview_<Company>_<Role>.md`, share it in chat, and save it to Google Drive
in **Job Search/Interviews** if the Drive connector is available.

## Honesty

Do not inflate the research or write questions that sound impressive but are not grounded in
the posting or the sources. The user will use these live with another person. One wrong
reference costs more than a plain, accurate question.

Do not save personal details (salary, reasons for leaving) into Claude's memory.
