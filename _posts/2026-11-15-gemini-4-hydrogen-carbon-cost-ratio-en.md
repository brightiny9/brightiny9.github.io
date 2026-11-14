---
layout: post
title: "Gemini 4 Hydrogen or Carbon: what does each cost per month, before and after Dec 1?"
lang: en
ref: gemini-4-hydrogen-carbon-cost-ratio
date: 2026-11-15
permalink: /en/gemini-4-hydrogen-carbon-cost-ratio/
---

**Gemini 4 Hydrogen costs 25% less than Carbon until Nov 30, 2026, and 62.5% less from Dec 1. Hydrogen is $1.50 input and $7.50 output per million tokens. Carbon is $2 and $10 until Nov 30, then $4 and $20.**

That gap is the same on every per-token line I compared, so the monthly gap is the same for any mix of input, cached input and output. In my three example bills, Hydrogen costs 75% of Carbon in November and 37.5% of Carbon from Dec 1. The real question is not the price per token. It is whether Carbon finishes your job with fewer tokens.

The dollar figures below are my arithmetic on published prices. I did not run either model.

## What Google published

Google's [Hydrogen announcement](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/) is dated Nov 12, 2026. I opened it on Nov 15, 2026. It says:

- Hydrogen is "priced flat across its entire 1 million-token context window at $1.50 per million input tokens and $7.50 per million output tokens."
- Hydrogen is "our daily driver for agentic workflows."
- On the Artificial Analysis Intelligence Index at default high thinking, Hydrogen scores 51 and Argon scores 50, according to Google.

Google's [Carbon announcement](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-4-carbon-now-available/) is dated Nov 10, 2026 (opened Nov 15, 2026). It gives "$2 per million input tokens and $10 per million output tokens" as an introductory price, and says "$4 per 1M input tokens and $20 per 1M output tokens will apply" after Nov 30, 2026. It also says Argon is the ideal choice for most software engineering and knowledge work, while Carbon is built for tasks that test the limits of a model's intelligence.

## The price list side by side

From Google's [pricing page](https://aistudio.google.com/docs/pricing), opened Nov 15, 2026. Prices are per 1M tokens.

| Price per 1M tokens | Hydrogen | Carbon until Nov 30 | Carbon from Dec 1 |
|---|---|---|---|
| Standard input | $1.50 | $2.00 | $4.00 |
| Standard output | $7.50 | $10.00 | $20.00 |
| Standard cached input | $0.075 | $0.10 | $0.20 |
| Batch input | $0.75 | $1.00 | $2.00 |
| Batch output | $3.75 | $5.00 | $10.00 |
| Batch cached input | $0.0375 | $0.05 | $0.10 |
| Free tier (API) | yes | none | none |

The page lists a free tier for Hydrogen and says Carbon is not available on the free tier. I did not check the free tier's rate limits.

## My calculation: three monthly bills (standard tier)

Assumptions, not measurements: made-up token counts, standard tier only (Batch is half of Standard for both models, so the ratio is the same), and the same token counts on both models. I count only the per-token prices in the table, not any other cache fee.

| Scenario | Hydrogen | Carbon until Nov 30 | Carbon from Dec 1 |
|---|---|---|---|
| A. Light: 5M input, 1M output | 5 × $1.50 + 1 × $7.50 = $15 | $20 | $40 |
| B. Medium: 20M input, 4M output | 20 × $1.50 + 4 × $7.50 = $60 | $80 | $160 |
| C. Cache-heavy: 10M fresh input, 85M cache reads, 8M output | 10 × $1.50 + 85 × $0.075 + 8 × $7.50 = $81.38 | $108.50 | $217 |

Hydrogen's price is exactly 75% of Carbon's November price on every line ($1.50 / $2, $7.50 / $10, $0.075 / $0.10). Against the Dec 1 price it is exactly 37.5% ($1.50 / $4, $7.50 / $20, $0.075 / $0.20). That is why all three scenarios show the same ratio.

## The number that decides it: break-even tokens

Because the ratio is fixed, you can turn the price into one rule:

- Until Nov 30, Carbon is cheaper only if it finishes the job using less than 75% of the tokens Hydrogen needs (a 25% cut).
- From Dec 1, Carbon is cheaper only if it uses less than 37.5% of Hydrogen's tokens, meaning it must use about 2.7 times fewer tokens.

Google says Carbon uses "more tokens than Argon" to reason deeply and run verification loops, and thinking tokens count as output. I found no token comparison between Carbon and Hydrogen in the text I read. So on price alone, Hydrogen is the cheaper default. Carbon has to earn its price with results, such as fewer retries on a hard coding task.

## What I could not check

- Token use of Carbon versus Hydrogen on a real job. Google gives no number in the pages I read.
- Whether either price will change. Google calls Carbon's current price "introductory," so I would not assume either price is final.
- Free tier rate limits for Hydrogen.
- Cache storage fees for either model. The pricing page's caching rows were unclear to me, so I left them out of the three bills. If you keep large caches, check that line on the page yourself.
- Quality on your own task. The Index score above is Google's claim about Hydrogen and Argon, not Carbon.

## My take

For a small budget, start with Hydrogen. It is cheaper on every per-token line, it has a free API tier, and Google positions it for everyday agent work. Switch a specific hard job to Carbon only after you count the tokens on both models for that job and see Carbon finish in under 37.5% of Hydrogen's tokens (from Dec 1). Budget with the Dec 1 Carbon price, not the November one.

Related: our earlier post on [Carbon vs Argon pricing and the Dec 1 change](https://brightiny9.github.io/en/gemini-4-carbon-price-vs-argon-dec-1/).

*Sources, opened Nov 15, 2026: [Hydrogen announcement](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-hydrogen/), [Carbon announcement](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-4-carbon-now-available/), [Gemini pricing](https://aistudio.google.com/docs/pricing).*
