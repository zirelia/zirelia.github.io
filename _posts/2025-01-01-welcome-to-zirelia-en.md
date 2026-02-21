---
layout: post
title: "Welcome to Zirelia — The Autonomous AI Virtual Influencer Engine"
date: 2025-01-01 10:00:00 +0100
categories: [announcement, vision]
lang: en
description: "What if your social media ran itself — generating content, creating images, and posting 24/7 — while you sleep? That's Zirelia."
image: /assets/images/blog/welcome.png
---

## The Influencer Paradox

Building a social media presence is a full-time job. Creating content every day, staying consistent with your visual identity, posting at the right time, engaging with followers — it never stops.

But what if the "influencer" didn't need to sleep, eat, or take a day off?

That's the idea behind **Zirelia**: a fully autonomous AI engine that creates and manages a virtual influencer persona from end to end, without manual intervention.

## What Zirelia Does

Zirelia is built around three core capabilities:

**The Brain** — Powered by GPT-4 and LangChain, Zirelia generates authentic thoughts, opinions, and content ideas based on a configurable persona. It knows the persona's backstory, interests, tone of voice, and daily routine. It even has memory — using ChromaDB to recall past posts and avoid repetition.

**The Imagination** — Every post can include an AI-generated image, created by FLUX.1 via the Replicate API. Images are generated to match the persona's visual identity, with a quality control loop that retries if the output doesn't meet the standard.

**The Hands** — Zirelia automatically posts to Twitter/X using the official API. It uploads media, writes captions, and schedules posts based on optimal time windows — no human needed.

## The Architecture

The system is fully self-hosted and runs via Docker Compose:

```
docker compose up -d
```

This starts five services: the FastAPI REST server, the Celery task queue, Redis, PostgreSQL for post history, and the SmartScheduler daemon that runs 24/7.

## Define a Persona, Get an Influencer

Everything starts with a YAML file. Here's a minimal example:

```yaml
name: "Sienna Fox"
age: 23
occupation: "Digital Creator & Lifestyle Model"
voice:
  tone: "Playful, confident, relatable"
  style: "Short sentences, emojis, conversational"
interests:
  - "Fitness & wellness"
  - "Tech & AI"
  - "Travel"
```

From this definition, Zirelia builds a complete persona — and starts generating content that sounds genuinely human.

## Open Source, Self-Hosted

Zirelia is **open source** under the Elastic License 2.0. You bring your own API keys (OpenAI, Replicate, Twitter/X), your own server, and your own persona definition. The Author has zero access to your data or generated content.

This is the first release. The roadmap includes Instagram support, voice synthesis, and a visual control dashboard.

**Star the project on GitHub and join the experiment.**
