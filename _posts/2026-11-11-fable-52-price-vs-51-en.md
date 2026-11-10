---
layout: post
title: "Is Claude Fable 5.2 cheaper than 5.1, and what does it save on a month of coding?"
lang: en
ref: fable-52-price-vs-51
date: 2026-11-11
permalink: /en/fable-52-price-vs-51/
---

**Is Claude Fable 5.2 cheaper than Fable 5.1? Yes. Every per-token price on Anthropic's pricing page is 20% lower.**

Input is $8 per million tokens (was $10), output is $40 (was $50), and cache reads are $0.20 (was $0.25). In my example of 20M input and 4M output tokens a month, the bill goes from $400 to $320. That is $80 a month saved, and the old model is not going away soon.

The dollar figures below are my arithmetic on Anthropic's published prices. I did not run either model, so I can't tell you which one answers your prompts better.

## What Anthropic announced

Anthropic's [announcement of Fable 5.2 and Mythos 5.2](https://www.anthropic.com/claude-fable-and-mythos-5-2) is dated Nov 9, 2026. I opened it on Nov 10, 2026. It says:

- Standard price for Fable 5.2: $8 input, $40 output, per million tokens.
- Fast mode: $16 input, $80 output.
- The model ID is `claude-fable-5-2`.
- Anthropic says Fable 5.2 can "generate outputs up to 30% faster" than Fable 5.1, and that it has about 55% fewer blocks than Fable 5.1 (about 60% fewer in cybersecurity and 40% fewer in biology). Both are Anthropic's own claims. I did not test either.
- Mythos 5.2 is sold at the same prices, but it is limited availability.

## The price table, side by side

From Anthropic's [pricing page](https://platform.claude.com/docs/en/about-claude/pricing), per million tokens, opened Nov 10, 2026:

| Price type | Fable 5.1 | Fable 5.2 | Change |
|---|---|---|---|
| Input | $10 | $8 | -20% |
| Cache write, 5 minutes | $12.50 | $10 | -20% |
| Cache write, 1 hour | $20 | $16 | -20% |
| Cache read | $0.25 | $0.20 | -20% |
| Output | $50 | $40 | -20% |
| Batch input / output | $5 / $25 | $4 / $20 | -20% |

The change is the same 20% on every line (for example 8 ÷ 10 = 0.8 and 40 ÷ 50 = 0.8). That matters for the next section.

## My calculation: three monthly bills

Assumptions, not measurements: standard mode, no batch discount, prompts that fit the normal pricing, and the token counts are made up for illustration. Your counts will differ. Check them in your own usage export.

| Scenario | Math on Fable 5.1 | Math on Fable 5.2 | 5.1 bill | 5.2 bill | Saved |
|---|---|---|---|---|---|
| A. Light: 5M input, 1M output | 5 × $10 + 1 × $50 | 5 × $8 + 1 × $40 | $100.00 | $80.00 | $20.00 |
| B. Medium: 20M input, 4M output | 20 × $10 + 4 × $50 | 20 × $8 + 4 × $40 | $400.00 | $320.00 | $80.00 |
| C. Cache-heavy agent work: 10M fresh input, 5M cache writes (5 min), 85M cache reads, 8M output | 10 × $10 + 5 × $12.50 + 85 × $0.25 + 8 × $50 | 10 × $8 + 5 × $10 + 85 × $0.20 + 8 × $40 | $583.75 | $467.00 | $116.75 |

Two things stand out.

First, **the cache mix does not change the percentage.** Because every price fell by exactly 20%, scenario C saves 20% too ($116.75 of $583.75). A cache-heavy workflow doesn't get a bigger discount. It just has a bigger bill to take 20% off.

Second, **output is the biggest line.** In scenario C, 8M output tokens cost $400 on 5.1, which is 69% of the $583.75 bill. The 85M cache-read tokens cost $21.25, about 4%. If you want to cut the bill further, the number of output tokens you generate matters more than how many tokens you read from cache. That is my reading of the table, not Anthropic's advice.

## What fast mode costs

[Fast mode](https://platform.claude.com/docs/en/about-claude/pricing) for Fable 5.2 is $16 input and $80 output, exactly 2x standard. Anthropic says it speeds up token generation by up to 2.5 times (company claim, not tested by me).

On scenario B (20M input, 4M output), fast mode costs 20 × $16 + 4 × $80 = $640. That is double the $320 standard bill. It is also 60% more than the $400 you paid on Fable 5.1 in standard mode.

So the 20% cut does not make fast mode cheap. Fast mode on 5.2 costs more than standard on 5.1. I did not find a fast mode price for Fable 5.1 in the pricing page's fast mode table, which lists Fable 5.2, Mythos 5.2, Opus 5.5, Opus 5 and Opus 4.8.

Fast mode can't be used with the Batch API, according to the same page. The pricing page also says fast mode multipliers stack with prompt caching, so I would not assume cache reads stay at $0.20 in fast mode. I did not calculate that case.

## Is there a reason to stay on Fable 5.1?

On price alone, no. 5.2 is cheaper on every line.

Reasons to wait that are about risk, not price (my opinion):

- You have prompts tuned for 5.1 and have not re-tested them. A cheaper model that gives different output can cost more in review time.
- You pin a model ID in production. Switching means changing `claude-fable-5-1` to `claude-fable-5-2` and testing.
- Output length can change. The bill is price times tokens, and I have no data on whether 5.2 writes more or fewer tokens than 5.1 on the same job.

There is no deadline forcing a move. Anthropic's [model deprecations page](https://platform.claude.com/docs/en/about-claude/model-deprecations), opened Nov 10, 2026, lists `claude-fable-5-1` as Active, with a tentative retirement date of "Not sooner than September 1, 2027". `claude-fable-5-2` is listed as Active, "Not sooner than November 9, 2027". "Not sooner than" is a floor, not a promise of the exact date. The page says Anthropic gives at least 60 days' notice before retiring a publicly released model.

{% include bars.html title="Monthly bill for 20M input + 4M output tokens, standard mode unless noted (USD)" items="Opus 5.5, standard|160;Fable 5.2, standard|320;Fable 5.1, standard|400;Fable 5.2, fast mode|640" prefix="$" source="Anthropic pricing page (platform.claude.com/docs/en/about-claude/pricing), my arithmetic" date="Nov 10, 2026" note="Fable 5.2 standard costs 2x Opus 5.5 standard on the same tokens. Example token counts are my assumption. Lower is cheaper, not better." %}

## How does it compare with Opus 5.5?

The same pricing page lists Opus 5.5 at $4 input and $20 output, with cache reads at $0.20. On scenario B that is 20 × $4 + 4 × $20 = $160. So Fable 5.2 at $320 is still twice the price of Opus 5.5 on the same tokens.

Anthropic's announcement says Fable 5.2 and Mythos 5.2 are "a step above Opus 5.5 in almost all the capabilities we evaluated". That is Anthropic's claim from its own evaluations. Whether the gap is worth 2x for your tasks is something only your own test can show.

One detail I noticed: the cache read price is the same $0.20 for Fable 5.2 and Opus 5.5. For cache-heavy work, the gap between those two models is mostly in the output price, fresh input and cache writes, not in reads.

## My opinion

If you were already paying for Fable 5.1, switch your test environment to 5.2 this week and compare output tokens per task on a handful of real prompts. If the token counts and quality hold, you keep the 20% for free. If you were not using Fable because of the price, the new price does not change the picture much: it is still the premium tier, at twice Opus 5.5.

## What I don't know

- Whether Fable 5.2 writes the same number of output tokens as 5.1 on your tasks. Only that would show your real saving.
- Whether the 30% speed and 55% fewer blocks claims hold in your use. I did not test them.
- Whether rate limits changed. The announcement doesn't mention rate limits, and I did not find them on the pages I opened.
- What fast mode costs on Fable 5.1, or whether it exists. It is not in the pricing page's fast mode table.
- What cache reads cost in fast mode. The page says caching multipliers apply on top of fast mode, and I did not work through that math.
- Whether prices on Amazon Bedrock or Google Cloud match. I only checked Anthropic's own pricing page.

## Related

- Another model price change with a date on it: [What changes on Dec 1 if your app calls gemini-2.5-pro, and what it costs](https://brightiny9.github.io/en/gemini-25-deprecation-dec1/).

## Sources (opened Nov 10, 2026)

- [Anthropic: Claude Fable 5.2 and Claude Mythos 5.2 (Nov 9, 2026)](https://www.anthropic.com/claude-fable-and-mythos-5-2)
- [Anthropic API pricing](https://platform.claude.com/docs/en/about-claude/pricing)
- [Anthropic model deprecations](https://platform.claude.com/docs/en/about-claude/model-deprecations)
