# File formats

Exact schemas for the three state files. Follow them so that every future session (and every future version of this skill) can parse what past sessions wrote.

## career-corpus.md

One file, one source of truth. Far richer than any resume — resumes are *views* over this corpus. Rules:

- Every role and project gets a **stable anchor heading** (kebab-case, never renamed once created) so edits merge into the right place instead of duplicating.
- Every quantified claim carries **provenance** — where the number came from and when. This is what makes the no-fabrication guarantee auditable.
- Unresolved weaknesses stay visibly annotated (`[NO METRIC]`, `[VAGUE]`, `[THIN]`) until an interview resolves them. Do not delete annotations without evidence; they are the to-do list.
- Newer information wins. When the user corrects a fact, update in place and note the correction in `changelog.md` — don't keep both versions in the corpus.

```markdown
# Career Corpus — <Name>
Updated: YYYY-MM-DD

## profile
Contact: email · phone · city · linkedin-url · portfolio/github
Targeting: role families, seniority, geography/remote, constraints (visa etc.)
Narrative: 2–4 sentences — the through-line of their career and the story of the next move.

## role: acme-senior-pm            <!-- anchor: company-title, stable forever -->
Company: Acme Corp — B2B logistics SaaS, ~200 employees
Title: Senior Product Manager | Dates: Mar 2022 – Present | Location: Bangalore
Scope: owned pricing + billing pod; 2 PMs, 8 engineers; reported to VP Product
Source: resume-v3.pdf, 2024 perf review, interview 2026-07-21

### project: usage-based-pricing   <!-- anchor, stable forever -->
- Led migration from seat-based to usage-based pricing across 400 accounts
  - metric: +23% net revenue retention in 2 quarters {source: 2024 perf review}
  - metric: churn on migrated accounts 4% vs 9% control {source: user interview 2026-07-21}
- Story (interview answers, verbatim-ish): <what happened, obstacles, their specific contribution>
- Skills: pricing strategy, SQL, stakeholder management
- [VAGUE] their contribution vs the RevOps team's on the billing rebuild

### project: ...

## education
## certifications
## extras                          <!-- talks, publications, awards, volunteering, interests -->
## parking-lot                     <!-- material that fits no current role/project; review during BUILD -->
```

## style-rules.md

A lint file, not a diary. Small (~30 rules max), imperative, dated. Applied to **every** output the skill produces. On contradiction, the new rule replaces the old; log the supersession in `changelog.md`.

```markdown
# Style Rules
<!-- Every rule: one line, imperative, with date + trigger. Newest wins on conflict. -->

## never
- Use em dashes anywhere. (2026-07-21, user correction)
- Open a bullet with "Spearheaded" or "Responsible for". (2026-07-21)

## always
- Sentence case for section headings. (2026-07-21)
- State team size in leadership bullets. (2026-07-21)

## framing
- Frame platform/infra work as business outcomes, not technical outputs. (2026-07-21)
- De-emphasize the 2019 consulting stint unless the JD is strategy-heavy. (2026-07-21)

## format-profile
<!-- Rendering contract for every TAILOR. Only present if the user chose non-defaults.
     Consented risks are recorded with dates so the skill never re-warns about them. -->
- Template: user's two-column docx (templates/priya-template.docx). (2026-07-21)
- Font: Georgia 11pt; margins 0.8". (2026-07-21)
- RISK ACCEPTED: two-column layout; warned re Workday/Taleo parsing, kept for design-studio applications. (2026-07-21)
```

## changelog.md

Append-only, newest first. One line per learning event — enough to reconstruct *why* the corpus/rules look the way they do, and to spot recurring corrections (a recurring correction = a skill bug, not a preference).

```markdown
# Changelog
- 2026-07-22 [style] Added "never: em dashes" (user correction during acme-pm tailor)
- 2026-07-22 [corpus] acme-senior-pm/usage-based-pricing: churn metric added (interview)
- 2026-07-21 [corpus] Initial build from resume-v3.pdf + LinkedIn + 40-min interview
- 2026-07-21 [style] SUPERSEDED "always: one page" → "always: one page except academic roles"
```

## applications/<slug>/

Slug: `YYYY-MM-company-role` (e.g. `2026-07-stripe-senior-pm`). Contents are described in SKILL.md. `resume.md` is the master; regenerate rendered files from it after any edit. `delta-report.md` must exist for every delivered resume — it is the trust artifact.
