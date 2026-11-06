# AI-Assisted Job Search Kit for Germany

Four Claude skills that run most of a job search with you:

| Skill | What it does | How you start it |
|---|---|---|
| `job-search-intake` | Interviews you about your goals, limits and experience; writes your **Job Search Profile** (a Google Doc) | "Set up my job search" |
| `job-hunt` | Searches German job boards and company career pages on a schedule, filters out anything that breaks your limits, checks the job is still open, emails you a ranked list, never repeats a job | "Run my job search" / "Set up my job search schedule" |
| `cv-builder` | Builds 2–4 base CVs (German format, with photo, ATS-friendly), plus optional quick per-job versions | "Build my base CVs" |
| `interview-prep` | Researches the company, drafts questions to ask, rehearses your answers, runs mock questions | "Prep me for this interview" + job link |

All four read the same profile, so you describe yourself once.

## What you need

- About **90 minutes** for setup, plus about an hour to build your CVs
- A **personal** Claude account on a paid plan (Pro is enough). Scheduled tasks, Gmail sending
  and custom skills need a paid plan. Do not use an account provided by an employer.
- A **new Gmail account** used only by Claude (step 2)
- Your current CV and/or your LinkedIn profile as PDF
  (LinkedIn: your profile → "More" → "Save to PDF")
- A recent professional photo (for the CV)

## 1. Create your Claude account

1. Go to claude.ai and sign up with your personal email.
2. Subscribe to **Pro** (Settings → Billing). You can cancel when you have signed a contract.
3. Install the Claude desktop or mobile app if you like. Everything also works in the browser.

## 2. Create a Gmail account just for Claude

Create a new Gmail account, e.g. `firstname.lastname.jobsearch@gmail.com`.

This account sends your job digests and stores your profile and CVs in its Google Drive. Your
private inbox stays private, and you can delete the account when your search is over.

## 3. Turn on file creation

In Claude: **Settings → Capabilities**, and switch on **Code execution and file creation**
(called **Create and edit files** in some versions). Skills do not work without it.

## 4. Upload the four skills

1. Find the four `.zip` files in the `zips` folder of this kit. **Do not unzip them.**
2. In Claude: **Customize → Skills** (in some versions: Settings → Capabilities → Skills).
3. Click **+** / **Upload skill** and upload each zip, one at a time.
4. Check that all four are listed and switched on.

## 5. Connect Gmail and Google Drive

1. In Claude: **Settings → Connectors** (or the connectors menu in the chat box).
2. Connect **Gmail** and **Google Drive**.
3. When Google asks you to sign in, choose the **new Claude Gmail account** from step 2,
   **not** your personal one. This is the most common setup mistake.

## 6. Run the intake (30–45 minutes)

Open a new chat and type: **Set up my job search**

Claude will ask for your CV, then interview you topic by topic: target roles, location and
commute, home office, salary floor, sectors you rule out, companies to block, language,
anything personal the job must fit around, and your real skills and gaps.

Be specific. "Munich, max 45 minutes by train, at least 2 home-office days, €70k floor" gives a
far better search than "Munich-ish, flexible".

At the end Claude saves **Job Search Profile** as a Google Doc in the new account's Drive.
Share that folder with your personal Google account (Share → your address → Editor) so you
can edit it easily.

## 7. Build your base CVs (45–60 minutes)

New chat: **Build my base CVs**

Upload your photo when asked. Claude builds one CV per role family from your profile, shows
you every fact to check, and saves Word files to the Drive folder **Job Search/CVs**. Open them
with Google Docs to edit; download as PDF to apply.

Read every line before you use a CV. You are the final fact-checker.

## 8. Switch on the scheduled search

New chat: **Set up my job search schedule**

Claude runs one search immediately so you see a real digest, then creates a scheduled task
(default: every 2 days, early morning). Scheduled tasks run in Anthropic's cloud, so your
computer can be off.

One setting matters: in **Settings → Connectors → Gmail**, allow sending **without asking
each time**. Otherwise every scheduled run stops and waits for an approval nobody gives. This
is safe because the account belongs to Claude and only emails you.

You can see, pause or edit the task under **Scheduled** in the left sidebar.

## 9. Before each interview

New chat: **Prep me for this interview** + the job link (or paste the posting text).

Claude asks who will interview you and which skills you feel least sure about, researches the
company, rehearses your answers with you and gives you a one-page prep sheet.

## Privacy

- Everything stays in your own Claude account and the Claude Gmail/Drive account. Nothing in
  this kit sends data anywhere else.
- The skills are told not to save personal details (address, salary, health, permit status)
  into Claude's memory. Check **Settings → Privacy** for whether your chats may be used to
  improve models, and to manage memory.
- When your search is over: pause or delete the scheduled task, then delete the Claude
  Gmail account if you want everything gone.

## Fixes for common problems

| Problem | Fix |
|---|---|
| Upload fails | Upload the `.zip` as it is. Do not unzip and re-zip it. |
| Claude does not use a skill | Name it: "Use the job-hunt skill to…". Check it is switched on under Skills. |
| "Profile not found" | The Google Doc must be named exactly **Job Search Profile** and live in the **Claude** Gmail account's Drive. |
| No digest arrived | Sidebar → **Scheduled** → open the last run. Usually the Gmail "ask before sending" setting (step 8) or a disconnected connector. |
| Same job twice | It appeared under a very different title. Tell Claude, and it will tighten the duplicate check. Repeats should be rare. |
| A job link will not open for Claude | LinkedIn often blocks it. Paste the job text into the chat. |
| You want German | Ask Claude: "Work in German from now on" or "Translate this guide into German". |

See **PLAYBOOK.md** for how to use the kit week to week.
