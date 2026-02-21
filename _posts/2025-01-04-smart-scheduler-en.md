---
layout: post
title: "The SmartScheduler: How Zirelia Posts Like a Human, Not a Bot"
date: 2025-01-04 10:00:00 +0100
categories: [architecture, automation]
lang: en
description: "Posting at fixed intervals is the fastest way to get flagged. Here's how Zirelia's SmartScheduler mimics human behavior to stay under the radar."
image: /assets/images/blog/smart-scheduler.png
---

## The Bot Detection Problem

Social media platforms are getting better at detecting automated accounts. One of the clearest signals: **mechanical regularity**.

A real person doesn't post at exactly 09:00, 13:00, and 18:00 every single day. They post when they feel like it, skip a day when they're busy, post twice on a lazy Sunday, and stay quiet on holidays.

A naive automation script that posts on a fixed cron schedule looks nothing like this — and platforms notice.

Zirelia's **SmartScheduler** is designed to solve exactly this problem.

## How the SmartScheduler Works

### Time Windows, Not Fixed Times

Instead of posting at exact times, the scheduler defines posting *windows* based on the persona's daily routine:

```python
TIME_WINDOWS = {
    "morning":   (8, 10),   # 8:00–10:00
    "afternoon": (12, 15),  # 12:00–15:00
    "evening":   (17, 20),  # 17:00–20:00
    "night":     (21, 23),  # 21:00–23:00
}
```

Within each window, the actual post time is **randomized** with a Gaussian distribution around the midpoint. The result looks human because it *is* statistically human-like.

### Daily Post Volume Variation

The scheduler doesn't post the same number of times every day. It draws from a configurable range:

```env
MAX_DAILY_POSTS=3
MIN_DAILY_POSTS=1
```

Some days it posts once. Some days three times. Occasionally it skips a day entirely — just like a real creator who "went off the grid."

### Holiday & Event Awareness

The SmartScheduler is aware of holidays (configurable per locale) and reduces posting frequency during them. It can also be configured to post *more* during trending events.

```python
HOLIDAYS = ["2025-12-25", "2025-01-01", "2025-07-04"]
```

On holidays, the scheduler reduces posts to 0–1 and adjusts content topics to match the occasion.

### Timezone Support

Everything runs in the persona's local timezone (default: `America/Los_Angeles`), so posts appear at natural local times:

```env
TIMEZONE=America/Los_Angeles
```

## Safety Rate Limiting

On top of scheduling randomization, the `SafetyManager` enforces hard limits to prevent accidental API abuse:

- Maximum N posts per rolling 24-hour window
- Minimum gap between consecutive posts (configurable)
- Automatic pause if Twitter/X returns rate limit errors

## Running the Scheduler

```bash
# Via Docker (recommended)
docker compose up scheduler -d

# Or directly
python run_scheduler.py
```

The scheduler runs as a persistent daemon, waking up periodically to check whether it's time to generate and post. It logs every decision — post time, topic selection, publish result — to a local log file.

The outcome: a feed that looks organic, grows steadily, and doesn't trigger platform detection algorithms.
