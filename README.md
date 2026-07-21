# resume-studio

**A Claude skill that turns everything you've ever done at work into resumes that win interviews.**

Most resume tools polish words. This one fixes the real problem: you don't remember half of what you achieved, and a generic resume gets ignored. resume-studio builds a permanent memory of your career, digs out the achievements you forgot, and tailors a fresh resume for every job you apply to.

## What it does

**1. Remembers your career.** Feed it anything — old resumes, your LinkedIn, performance reviews, or just messy notes. It builds a `career-corpus.md` file: your full professional history, with every number tied to where it came from. This file is yours, it's plain text, and it grows every time you use the skill.

**2. Interviews you like a great recruiter.** It drafts first, then asks a few sharp questions about the weak spots: *"What was the number before you improved it?" "What did your manager praise you in your last review?"* A few answers at a time, never a long form.

**3. Tailors a resume for each job.** Paste a job description. It researches the company, maps your history against what the role actually needs, and produces a clean, ATS-safe resume (`.md` + `.docx`) — plus a report that explains every change and honestly lists what the job wants that you don't have. No hiding, no padding.

**4. Never makes things up.** Every number on your resume traces back to something you said or shared. If there's no evidence, it asks you — it doesn't invent.

**5. Learns your taste, permanently.** Say "never use em dashes" or "that number was actually 3.8%" once — it's saved and applied to every future resume. Corrections never need repeating.

## Set it up — 2 clicks

1. Download **[`resume-studio.skill`](./resume-studio.skill)** from this repo *(click the file, then the download icon)*.
2. Drop it into any Claude chat and click **Save skill**.

**Even lazier:** paste this into Claude and let it set itself up:

> Set up the resume-studio skill from https://github.com/Sidgit11/resume-studio — follow the repo's AGENT_SETUP.md.

## Start — 1 message

> Build my professional profile. Here's my old resume and some notes about what I actually did: …

That's it. Claude takes over from there.

## How a typical journey goes

1. **Dump everything.** Old resumes, LinkedIn PDF, performance reviews, appraisal letters, even a rambling voice note about your proudest project. The messier the better — more raw material means a better resume.
2. **Get your career file.** Claude drafts `career-corpus.md` immediately, with weak spots visibly marked, and asks you a handful of questions to fill them. Answer what you can, skip what you want.
3. **Apply to a job.** Paste the JD (plus the hiring manager's LinkedIn post if there is one) and say *"tailor my resume for this."* You get the resume, the Word file, and the change report.
4. **Correct anything, once.** Style, facts, framing — every correction is remembered for all future resumes.
5. **Next application takes minutes,** because your career file already exists and keeps getting richer.

## Tips for the best results

- **Share performance reviews and self-assessments** — they're the single best input, and the one nobody thinks of.
- **Keep your `resume-studio/` folder somewhere permanent** (a connected local folder, a synced drive). That folder *is* your career memory — as long as Claude can see it, everything carries over between sessions.
- The resume rules inside are research-backed (ATS parsing mechanics, recruiter surveys, role-specific norms — see `references/resume-playbook.md`), including the myth-busting: ATS systems almost never auto-reject resumes; humans do.

## What's inside

| Path | What it is |
|---|---|
| `SKILL.md` | The skill's logic: modes, protocols, guardrails |
| `references/resume-playbook.md` | The research: ATS mechanics, formatting rules, role-specific playbooks, debunked myths |
| `references/corpus-schema.md` | File formats for your career memory |
| `references/question-bank.md` | How the interview questions work |
| `scripts/build_docx.py` | Renders your resume to an ATS-safe Word file |
| `resume-studio.skill` | The one-click install file |
| `AGENT_SETUP.md` | Instructions for a Claude agent to install this automatically |
| `evals/` | Test cases used to benchmark the skill |

## License

MIT. Contributions welcome — especially role-specific additions to the playbook. If Claude keeps repeating a mistake your style rules should prevent, that's a bug: open an issue.
