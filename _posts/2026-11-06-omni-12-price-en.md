---
layout: post
title: "Gemini Omni 1.1 Flash moves to 1.2 prices on Dec 3. What changes on your bill?"
lang: en
ref: omni-12-price
date: 2026-11-06
permalink: /en/omni-12-price/
---

If you call gemini-omni-1.1-flash, Google says your requests route to gemini-omni-1.2-flash on December 3 and are billed at 1.2 rates. Video output drops from $17.50 to $12.00 per 1M tokens, about 31% less (Google pricing page, checked 2026-11-06).

## What Google says

- Nov 5, 2026: Google released Gemini Omni 1.2 Flash (gemini-omni-1.2-flash), with up to 15-second video generation, 30% lower video output pricing ($12.00 per 1M tokens) and doubled paid-tier rate limits (changelog, checked 2026-11-06: https://aistudio.google.com/docs/changelog).
- Dec 3, 2026: API requests to gemini-omni-1.1-flash automatically route to gemini-omni-1.2-flash at 1.2 rates (same changelog).

## Price table (paid tier, per 1M tokens)

| | Omni 1.1 Flash | Omni 1.2 Flash |
|---|---|---|
| Input (text/image/video) | $1.50 | $1.50 |
| Text output | $9.00 | $9.00 |
| Video output | $17.50 | $12.00 |

Source: https://aistudio.google.com/docs/pricing, checked 2026-11-06. Only video output changes. Neither model has a free tier.

## Our math: cost per clip

The pricing page says 720p video is billed at 5,792 tokens per second on 1.2. That gives:

- 1.1: 5,792 x $17.50 / 1M = about $0.101 per second (the page says roughly $0.10)
- 1.2: 5,792 x $12.00 / 1M = about $0.070 per second (the page says roughly $0.07)
- A 15-second 720p clip: about $1.52 on 1.1 rates, about $1.04 on 1.2 rates

The 1.1 clip figure is our calculation. We assumed 1.1 uses the same 5,792 tokens per second. The page's "roughly $0.10 per second" for 1.1 matches that assumption, but our reads of the page were not consistent on whether Google states the 1.1 token rate, so we treat it as an assumption.

Google says 30% cheaper; our arithmetic gives 31.4% (5.50 / 17.50).

## Other resolutions on 1.2

Google lists these effective prices for 1.2 (pricing page, checked 2026-11-06). The 15-second column is our math (price per second x 15).

| Resolution | Tokens per second | Price per second | 15-second clip |
|---|---|---|---|
| 360p | 1,931 | $0.023 | about $0.35 |
| 720p | 5,792 | about $0.07 | about $1.04 |
| 1080p | 8,688 | $0.104 | about $1.56 |
| 4K | 17,376 | $0.209 | about $3.13 |

Google notes that 1080p and 4K use upsampling. We did not find matching per-resolution prices for 1.1 on that page, so we did not compare them.

## What a month looks like

At 1,000 clips of 15 seconds at 720p, that is about $1,520 on 1.1 rates versus $1,043 on 1.2 rates. The gap is about $478 a month. At 100 clips it is about $48. If you only draft at 360p, the whole 1,000 clips cost about $350 on 1.2, so the change matters most for finished 720p and higher output.

Our view: if you generate under 100 clips a month, the change is lunch money, and you do not need to touch anything. Above 1,000 clips, it is worth a calendar reminder.

## What to check before Dec 3

1. Look for the model name in your code. If it says gemini-omni-1.1-flash, Google says you will be billed at 1.2 rates after Dec 3 without changing anything.
2. Budget alerts: if you set a spend cap from the old price, your cap now buys about 46% more video seconds ($17.50 / $12.00 = 1.46).
3. Quality: 1.2 is a different model. Rerun your own prompts, because auto-routing may change outputs on the same model name. This is our inference from the routing notice, not a Google claim.
4. Rate limits: Google says paid-tier limits doubled for 1.2 (changelog). We did not find the exact new numbers in the text we read.

## What we did not verify

- Whether 1.2 outputs stay compatible with your existing prompts and pipelines after routing. Google's notice covers routing and billing only.
- Per-resolution prices for 1.1.
- The exact new rate-limit numbers.

Sources
- https://aistudio.google.com/docs/changelog (checked 2026-11-06)
- https://aistudio.google.com/docs/pricing (checked 2026-11-06)
