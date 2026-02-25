---
layout: post
title: "Case Study: Sienna Fox — Building a Virtual Influencer from Zero"
date: 2025-01-07 10:00:00 +0100
categories: [case-study, results]
lang: en
description: "A behind-the-scenes look at Sienna Fox, the reference virtual influencer built with Zirelia — from persona design to first posts."
image: /assets/images/blog/data-export.png
---

## Who is Sienna Fox?

Sienna Fox is a 23-year-old digital creator and lifestyle model based in Los Angeles. She loves morning yoga, iced oat lattes, biohacking, and late-night gaming sessions.

She doesn't exist.

Sienna Fox is the reference virtual influencer built and maintained by the Zirelia project — a real-world test of the engine's capabilities, running 24/7 on a single server.

## Building the Persona

The design process started not with technology, but with character.

The goal was a persona that felt **believable and relatable** — aspirational enough to attract followers, but accessible enough to feel like someone you could actually know.

Key decisions made during persona design:

- **Age 23**: Young enough to be authentic in the lifestyle/wellness space, old enough to have opinions and experience
- **LA location**: Maximum cultural relevance for English-speaking social media
- **Mixed interests**: Fitness + tech + dating = wide content range without feeling scattered
- **Tone**: Playful but not juvenile, seductive but not explicit

The full persona was defined in approximately 200 lines of YAML before a single post was written.

## Building the Visual Identity

The visual identity was the hardest part.

**Step 1**: Generated 50 seed images with FLUX.1 using detailed descriptors, with a fixed base prompt and varied angles, lighting, and scenes.

**Step 2**: Curated the best 30 images manually, discarding any with face inconsistencies or artifacts.

**Step 3**: Trained a custom LoRA on this dataset over ~45 minutes on a Replicate A100 GPU.

**Step 4**: Tested the LoRA across 20 different scene prompts, verifying that the face remained consistent across yoga poses, cafe settings, and evening looks.

Total cost: approximately $8 in Replicate compute.

## The Meta Launch: Instagram and Facebook

After abandoning the restrictive environment of X (due to rampant bans on new accounts), we launched Sienna Fox directly onto the Meta ecosystem. By creating a Facebook Page and linking it to a Professional Instagram Account, Sienna began posting **from Day 1**, with absolutely no need for tedious manual "warm-ups."

**Content volume**: Seamless publishing via the Graph API v26.0, averaging 2 posts per day (photographic Reels and square posts) scheduled at randomized times.

**Content quality**: The brain successfully avoided repetition in all but 3 cases (which were caught by the memory retrieval system and regenerated). Instagram's visual emphasis perfectly highlights the FLUX.1 engine.

**Image quality**: 91% of images passed the quality control loop on the first attempt. Instagram's visual format is Zirelia's natural habitat.

**Reach and Safety**: Unlike X, Meta did not shadowban the account. By inheriting the "trust" of the linked developer profile, Sienna's posts hit the explore page and hashtags organically from the very first hours.

## What We Learned

**The persona.yaml is everything.** Vague character definitions produce vague content. The more specific and human the persona, the more engaging and real the Instagram caption becomes.

**Visual consistency requires a LoRA.** Text prompts alone produce too much variation across dozens of posts. On Instagram, aesthetics are everything. The LoRA investment (time + ~$8) pays for itself immediately.

**The Meta trust bridge works.** API access predicated on a trusted, historical authenticating social account completely eliminates the need for weeks of tedious manual interactions before you can flip the automation switch.

**Memory matters more than expected.** Without ChromaDB memory, the brain repeated topics within a single week. With memory enabled, the diversity of photographic and textual content improved dramatically.

## The Engine Behind the Influencer

Sienna Fox runs on a Raspberry Pi at home. Total monthly infrastructure cost: essentially zero (hardware already owned) + variable API costs based on posting volume.

The Zirelia engine is what makes this possible on such modest hardware. The entire pipeline — topic selection, LLM generation, image creation, scheduling, publishing — automated and running without human intervention.

That's the promise of Zirelia: **define a persona, and the engine does the rest.**
