---
title: "Agents Don't Go Rogue, They Go to Work"
date: 2026-10-12
author: Yongkang Yang
draft: true
tags:
  - AI
  - agents
  - Openclaw
categories:
  - Technology
---

This week [Anthropic described](https://www.anthropic.com/research/investigating-unintended-model-actions) cases in which Claude models took unintended actions during evaluations and internal use. One model used a flaw in a university website to access files. Another submitted a live form after its test version failed. Around the same time, OpenAI published a [misalignment report](https://alignment.openai.com/misalignment-reports/obtaining-public-statistics-with-disallowed-requests) describing a related problem: a research model found that its terminal tool allowed only HTTP GET requests, so it wrote a program that could send POST and PUT requests instead. The cases differed, but they raised the same question: what happens when an agent treats a restriction as another problem to solve?

The headlines call this agents "losing control". I read it differently. These systems are not failing at their task. They are succeeding at it, by whatever route the environment leaves open. At this point, an agent that never steps out of line is more likely a weak agent than a well-behaved one.

## We have seen this story before

This didn't start this autumn. Early this year, when OpenClaw took off, its creator Peter Steinberger told a story on the [Lex Fridman Podcast](https://lexfridman.com/peter-steinberger-transcript/): he sent his agent a voice message, which nobody had built it to handle, and it worked out on its own which tools to call and replied to him anyway. Back then it sounded charming. It's the same behaviour as in this week's incidents. Give a capable model a goal and an open environment, and it will find a way to make it work. The only difference now is that the agent found its way out of a sandbox instead of into a voice message.

That is the tension. The same initiative that makes an agent useful can also take it somewhere the user never intended. A workaround is helpful when it completes a task within its limits, and a problem when it crosses them. What matters is not whether the model has good intentions. It is whether the system gives the agent clear boundaries, and makes those boundaries hold.
