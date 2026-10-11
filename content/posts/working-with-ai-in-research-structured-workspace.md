---
title: "Working with AI in Research: Start with a Structured Workspace"
date: 2026-07-09T18:51:00+02:00
author: Yongkang Yang
description: "A simple project workspace helps researchers work with AI while keeping decisions, files, and results clear."
tags:
  - AI
  - research
  - research workflow
  - OpenClaw
categories:
  - Research
draft: false
---

Artificial intelligence (AI) is already part of everyday research. Avoiding it entirely is becoming unrealistic. Rather than trying to keep AI out of academic work, I think we should ask how to work with it more effectively. AI is particularly useful for tasks that demand patience and attention to detail: proofreading manuscripts, checking consistency across drafts, and flagging possible errors in text or tables. We still need to verify its suggestions, but it can save us considerable time.

So how can we make AI work better for us? Inspired partly by my experience with [OpenClaw](https://github.com/openclaw/openclaw), I have been exploring a simple idea: **make the research project itself AI-friendly**. A clear folder structure and a few short Markdown files can help an AI assistant understand what the project is about, where things belong, and what has already been done.

## A small, shared workspace

Research lasts months or years. A chat window does not reliably carry the project's history from one task to the next. Instead, I keep a few plain Markdown files at the project root:

```text
research-project/
├── README.md
├── AGENTS.md
├── PROJECT.md
├── MEASURES.md
├── RESULTS.md
├── literature/
├── data/
├── scripts/
├── results/
├── writing/
├── logs/
└── skills/
```

Each root file has one job:

- **`README.md`** maps the folders and tells people where to find files. A small script can update its directory tree when files are added or moved.
- **`AGENTS.md`** tells the AI what to read first, where to save work, how to name files, and when to ask for approval.
- **`PROJECT.md`** records the research question, current progress, key decisions, and next steps.
- **`MEASURES.md`** records variable definitions, measures, sources, and changes.
- **`RESULTS.md`** summarizes checked analyses, findings, and remaining uncertainties.

The folders keep source material, scripts, outputs, drafts, and dated work logs separate. I keep project-specific instructions in `skills/` only when a task needs them. There is no need to install every available AI tool or extension.

## How I work with AI

At the start of a task, the AI reads `AGENTS.md`, `PROJECT.md`, and the latest entry in `logs/`. If I ask it to revisit an analysis, it can check `MEASURES.md`, put code in `scripts/`, and save outputs in `results/`. After I verify the output, we update `RESULTS.md` and record what changed in the log. When the folder structure changes, a small local script refreshes the directory map in `README.md`.

This makes the process easier to inspect and repeat. It also makes it easier to switch between tools without losing the project's rules.

**The goal is not to let AI make research decisions on its own.** The researcher remains responsible for checking references, methods, results, confidential data, and disclosure requirements. AI can help with the work; a clear workspace helps us keep control of it.
