# Resume Skill — Resume Builder & Beautifier

> 🌐 **English** · [中文](./README.zh.md)

> A Claude / Copilot **skill** that turns *"I need a good-looking resume"* into a stable, repeatable workflow. Every input flows into **one standardized data schema**, then renders through a swappable template — switching templates is just a skin change, content is never lost.

![Seven print-ready resume templates rendered from one data schema](docs/preview.png)

---

## Three entry points

| What the user says | Flow | Script |
|---|---|---|
| *"Beautify my resume"* / uploads a PDF/docx/txt | **A. Beautify an existing resume** | [`prompts/beautify.md`](prompts/beautify.md) |
| *"Here's my LinkedIn"* / pastes a linkedin.com link | **B. LinkedIn import** | [`prompts/linkedin-import.md`](prompts/linkedin-import.md) |
| *"Build me one from scratch"* / *"let's chat"* | **C. Conversational build** | [`prompts/interview.md`](prompts/interview.md) |

All three funnel into [`schema/resume-data.md`](schema/resume-data.md), then render through a template.

## Seven templates

| Preview | Template | Best for |
|:---:|---|---|
| <img src="docs/templates/classic-ats.png" width="200"> | **Classic / ATS**<br>[`classic-ats.html`](templates/classic-ats.html) | Single-column, machine-parseable, safest for mass applications |
| <img src="docs/templates/ledger.png" width="200"> | **Ledger**<br>[`ledger.html`](templates/ledger.html) | LaTeX-style serif, justified, nested bullets — SWE / data / eng |
| <img src="docs/templates/tech-compact.png" width="200"> | **Tech Compact**<br>[`tech-compact.html`](templates/tech-compact.html) | High density + mono accents, fits many projects on one page |
| <img src="docs/templates/modern-sidebar.png" width="200"> | **Modern Sidebar**<br>[`modern-sidebar.html`](templates/modern-sidebar.html) | Two-column with dark sidebar, modern feel |
| <img src="docs/templates/pillar.png" width="200"> | **Pillar**<br>[`pillar.html`](templates/pillar.html) | Enhancv-style, blue accents + skill chips + icon achievements — PM / marketing |
| <img src="docs/templates/elegant-serif.png" width="200"> | **Elegant Serif**<br>[`elegant-serif.html`](templates/elegant-serif.html) | Centered editorial serif — design / consulting / marketing |
| <img src="docs/templates/atelier.png" width="200"> | **Atelier**<br>[`atelier.html`](templates/atelier.html) | Whitespace-heavy minimal — design / creative roles |

**Picking one:** mass-applying / passing the bots → Classic-ATS or Ledger; a human reads it / referral / portfolio-facing → the others stand out more.

## Three first principles

1. **Never fabricate.** Every experience, responsibility and number comes from what the user actually provided. Guide, probe, sharpen weak bullets — but never invent a company, title, result, or metric. Verify every number; mark unknowns `[to confirm]`.
2. **One question at a time.** Building a resume by conversation is an interview, not a questionnaire.
3. **Structure first, render second.** Whatever the entry point, organize content into the `schema/resume-data.md` fields and confirm it before rendering HTML.

## Usage

Drop the whole `resume-skill/` folder into your skills directory (e.g. `~/.claude/skills/resume-skill/`) and just say *"beautify this resume"* (attach a PDF), *"I have no resume, let's build one"*, or *"here's my LinkedIn, make me one."* Claude reads `SKILL.md` and runs the matching flow.

**Output:** a self-contained single-file HTML (`<name>-resume-<template>.html`). Open in a browser → `Cmd+P` → Save as PDF (margins None/Default, enable background graphics).

## Layout
```
resume-skill/
├── SKILL.md                       # Flow entry point (read first)
├── schema/resume-data.md          # Standardized fields — the hub format for every entry point
├── prompts/
│   ├── beautify.md                # Entry A: beautify an existing resume
│   ├── linkedin-import.md         # Entry B: LinkedIn import + fallback
│   └── interview.md               # Entry C: conversational collection
├── guides/writing-tips.md         # Bullet craft, quantification, ATS keywords, common mistakes
└── templates/                     # 7 print-optimized HTML templates
```

## Related skills
- [job-description-skill](https://github.com/yanliudesign/job-description-skill) — JD Decoder & Offer Strategy OS
- [Behavior-question-skill](https://github.com/yanliudesign/Behavior-question-skill) — Behavioral interview / Career Story OS

## License
MIT
