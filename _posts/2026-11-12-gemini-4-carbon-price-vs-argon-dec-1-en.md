---
layout: post
title: "Is Gemini 4 Carbon priced the same as Argon, and what happens to the bill on Dec 1?"
lang: en
ref: gemini-4-carbon-price-vs-argon-dec-1
date: 2026-11-12
permalink: /en/gemini-4-carbon-price-vs-argon-dec-1/
---

**Is Gemini 4 Carbon priced the same as Gemini 4 Argon? Yes, on Google's pricing page the standard prices are identical. Both cost $2 input and $10 output per million tokens until Nov 30, 2026, then $4 and $20 from Dec 1.**

So the Dec 1 change doubles the bill on either model. In my example of 20M input and 4M output tokens a month, the bill goes from $80 to $160. The difference between the two models is not the price per token. Google describes Carbon as "using more tokens than Argon to explore thoroughly, reason deeply, and run extended verification loops," so the same job can cost more on Carbon.

The dollar figures below are my arithmetic on published prices. I did not run either model.

## What Google announced

Google's [Gemini 4 Carbon announcement](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-4-carbon-now-available/) is dated Nov 10, 2026. I opened it on Nov 12, 2026. It says:

- Carbon is available through the API in Google AI Studio and Gemini for Business, among other places.
- The price is "$2 per million input tokens and $10 per million output tokens" at an introductory rate.
- "After the introductory period expires on November 30, 2026, the price of $4 per 1M input tokens and $20 per 1M output tokens will apply."
- Carbon is described as "using more tokens than Argon" to reason deeply and run extended verification loops.

Google's [pricing page](https://aistudio.google.com/docs/pricing) (opened Nov 12, 2026) lists the same Standard and Batch prices for both models. Here is the side-by-side, per million tokens (the page labels output "including thinking tokens"):

| Price per 1M tokens | Carbon until Nov 30 | Argon until Nov 30 | Both from Dec 1 |
|---|---|---|---|
| Standard input | $2 | $2 | $4 |
| Standard output | $10 | $10 | $20 |
| Standard cached input | $0.10 | $0.10 | $0.20 |
| Batch input | $1 | $1 | $2 |
| Batch output | $5 | $5 | $10 |
| Batch cached input | $0.05 | $0.05 | $0.10 |
| Free tier | none | none | none |

Batch is half the standard price, but it also doubles on Dec 1.

## My calculation: three monthly bills (standard tier)

Assumptions, not measurements: made-up token counts, standard tier only (no batch), and I leave out any cache storage fee because I did not read one.

| Scenario | Until Nov 30 | From Dec 1 |
|---|---|---|
| A. Light: 5M input, 1M output | 5 × $2 + 1 × $10 = $20 | 5 × $4 + 1 × $20 = $40 |
| B. Medium: 20M input, 4M output | 20 × $2 + 4 × $10 = $80 | 20 × $4 + 4 × $20 = $160 |
| C. Cache-heavy: 10M fresh input, 85M cache reads, 8M output | 10 × $2 + 85 × $0.10 + 8 × $10 = $108.50 | 10 × $4 + 85 × $0.20 + 8 × $20 = $217 |

Every line doubles exactly, so the cache does not soften it. Output is the biggest part of the bill only in scenario C ($80 of $108.50). In A and B, input and output cost the same. Because thinking tokens count as output, a model that thinks longer costs more even at the same price.

## What I could not check

- The context window and token limits for Carbon. The announcement does not state them.
- How many more tokens Carbon uses than Argon on a real job. Google gives no number in the text I read.
- Whether the Dec 1 price is final. Google calls the current price "introductory."
- Cache storage fees. The pricing page also lists Flex and Priority tiers; I did not compare them for both models, so the table above covers Standard and Batch only.

## My take

If you are planning a Gemini 4 budget, use the Dec 1 prices ($4 and $20), not the November ones. Test one real job on both models and count the output tokens before you choose Carbon over Argon. Same price per token can still mean a different bill.

Related: our earlier post on [Gemini 4 Argon's Dec 1 price change](https://brightiny9.github.io/en/gemini-4-argon-price-doubles-dec-1/).

*Sources, opened Nov 12, 2026: [Google announcement](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-4-carbon-now-available/), [Gemini pricing](https://aistudio.google.com/docs/pricing).*
