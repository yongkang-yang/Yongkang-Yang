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

Research lasts months or years. A chat window does not reliably carry the project's history from one task to the next. In my research project template, the `README.md` serves as a map: it explains the purpose of each folder and shows a directory tree that can be updated automatically. Here is a simplified example:

```text
research-project/
├── README.md
├── AGENTS.md
├── PROJECT.md
├── MEASURES.md
├── RESULTS.md
├── compliance/
├── literature/
├── studies/
│   ├── study-01/
│   └── study-02/
├── writing/
├── submission/
├── meetings/
├── presentation/
├── logs/
├── scripts/
└── skills/
```

A few Markdown files at the root give the AI the context it needs:

- **`README.md`** maps the folders and tells people and AI where to find files.
- **`AGENTS.md`** explains what the AI should read first, where to save work, and when to ask for approval.
- **`PROJECT.md`** records the research question, current progress, decisions, and next steps.
- **`MEASURES.md`** records variable definitions, measures, and their sources.
- **`RESULTS.md`** summarizes verified analyses and remaining uncertainties.

The other folders keep research materials, manuscripts, meeting notes, and dated logs in predictable places. Project-specific scripts and skills can stay in the project without having to explain their details in every conversation.

## A concrete example: proofreading the results

Suppose I ask AI to check a manuscript after an analysis has changed. Instead of searching through unfamiliar files, it can follow `README.md` to the relevant study, read the variable definitions in `MEASURES.md`, and compare the manuscript's claims and tables with the checked results in `RESULTS.md`. It can flag differences and suggest edits; I decide which corrections are valid. We then record the accepted changes in `logs/`.

If the project gains a new folder, a small script can refresh the directory map in `README.md`. The next AI session starts with an up-to-date map rather than another long explanation. The same structure also works across different AI tools.

**The goal is not to let AI make research decisions on its own.** The researcher remains responsible for checking references, methods, results, confidential data, and disclosure requirements. AI can help with the work; a clear workspace helps us keep control of it.
