---
layout: post
title: "Zirelia lands on Meta: Autonomous Posts on Instagram and Facebook"
date: 2025-01-09 10:00:00 +0100
categories: [updates, guides]
lang: en
description: "The Zirelia engine is now entirely configurable for automating content on Instagram and Facebook Pages. Discover the power of the free and permissive Graph API v26.0."
image: /assets/images/blog/meta-integration.png
---

As previously announced, the Zirelia ecosystem has embraced Meta as the primary platform for growing your AI Virtual Influencer. By abandoning a punitive and restricted ecosystem, we dive into a platform that rewards visual aesthetics and consistency.

## Why Meta (Instagram and Facebook)?

Unlike the original text-heavy limitations, Instagram perfectly aligns with Zirelia's genetic strengths.

*   **Visual Priority:** The scheduler no longer needs to "hide" partial image usage. Instagram *is* images. FLUX.1 (combined with your LoRA) becomes the anchor of your presence, guaranteeing a stunning level of professionalism.
*   **Creator-Based Trust:** You won't be immediately shadowbanned for automation. By using the Facebook for Developers portal linked to your real account, Meta automatically accepts that your Persona's Instagram Account is "covered" by your personal credibility.
*   **APIs are Free:** While other platforms enforce prohibitive fees for write access, Meta's Graph API (currently version `v26.0`) is entirely free for "Development" accounts.

## Multi-Platform Architecture

In the core Zirelia module, we've introduced the `--platform` parameter. The Python script `main.py` now utilizes a dynamic *PlatformFactory*:

```bash
docker compose run --rm app python main.py --platform instagram --mode hybrid
```

This command triggers both the LangChain brain (text generation) and the FLUX.1 engine. After generating the media locally, it calls Instagram's REST APIs to publish directly to the feed.

Zirelia strictly checks data integrity: for instance, it will proactively block execution if you try to publish to Instagram with `--mode text` set (since Instagram natively rejects posts without images).

Get comfortable, forget the paralyzing shadowbans, and prepare your Influencer's Professional Instagram Account. In the next article, we'll see exactly how to set up Meta Developer step by step!
