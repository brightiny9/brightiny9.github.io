---
layout: post
title: "What changes on Dec 1 if your app calls gemini-2.5-pro, and what it costs"
lang: en
ref: gemini-25-deprecation-dec1
date: 2026-11-03
permalink: /en/gemini-25-deprecation-dec1/
---

**Your app calls gemini-2.5-pro. What changes on December 1 and what will it cost?**

From Dec 1, 2026, requests to `gemini-2.5-pro` are routed to `gemini-3.8-flash` and billed at Gemini 3.8 Flash rates. In my example (10M input and 2M output tokens a month) the bill falls from $32.50 to $15.00 in December, then rises to $30.00 on Jan 1, 2027. The same changelog entry also lists API changes that can break code, so read the section on that below.

Those dollar figures are my arithmetic on Google's published prices. I did not run any model. I can't tell you whether the new model answers your prompts as well.

## What Google says

Google's [Gemini API changelog](https://aistudio.google.com/docs/changelog) has a Nov 2, 2026 entry. I opened it on Nov 3, 2026.

- Starting Dec 1, 2026, all API requests to `gemini-2.5-pro` automatically route to `gemini-3.8-flash`, charged at Gemini 3.8 Flash rates.
- Starting Dec 1, 2026, all API requests to `gemini-2.5-flash` automatically route to `gemini-3.5-flash-lite`, charged at Gemini 3.5 Flash-Lite rates.

The switch happens on Google's side. But the same entry tells developers to update the model string before Dec 1, and it lists changes that can break existing code:

- Function calling and `thought_signature` validation changes.
- `thinking_level` replaces `thinking_budget`.
- Sampling parameters are removed.
- Prefilled model turns are removed.

The same breaking changes apply to `gemini-2.5-flash` users moving to `gemini-3.5-flash-lite`. I did not test any of these. Check the changelog entry for the exact wording before you change code.

## The prices

From Google's [pricing page](https://aistudio.google.com/docs/pricing), per 1M tokens, standard paid tier, opened Nov 3, 2026:

| Model ID | Input | Output |
|---|---|---|
| gemini-2.5-pro | $1.25 (prompts up to 200k tokens), $2.50 (over 200k) | $10.00 (up to 200k), $15.00 (over 200k) |
| gemini-3.8-flash | $0.75 through Dec 31, 2026; $1.50 from Jan 1, 2027 | $3.75 through Dec 31, 2026; $7.50 from Jan 1, 2027 |
| gemini-2.5-flash | $0.30 (text, image, video); $1.00 (audio) | $2.50 |
| gemini-3.5-flash-lite | $0.30 (text, image, video, audio) | $2.50 |

Note the 3.8 Flash price has a date on it. The Dec price is the lower one.

## My calculation: 10M input, 2M output tokens a month

Assumption, not a measurement: all prompts are 200k tokens or shorter, and no caching or batch discounts.

| Path | Math | Monthly bill |
|---|---|---|
| gemini-2.5-pro today | 10 × $1.25 + 2 × $10 | $32.50 |
| Routed to 3.8 Flash, December 2026 | 10 × $0.75 + 2 × $3.75 | $15.00 |
| Routed to 3.8 Flash, from Jan 1, 2027 | 10 × $1.50 + 2 × $7.50 | $30.00 |
| gemini-2.5-flash today | 10 × $0.30 + 2 × $2.50 | $8.00 |
| Routed to 3.5 Flash-Lite | 10 × $0.30 + 2 × $2.50 | $8.00 |

What stands out:

- December is 54% cheaper than today ($17.50 less). January cuts that to $2.50 less, about 8%.
- With prompts over 200k tokens, 2.5 Pro costs 10 × $2.50 + 2 × $15 = $55.00. Against that, $30.00 in January is still a drop.
- If you call `gemini-2.5-flash` with text, the bill doesn't change on paper. Audio input gets cheaper, from $1.00 to $0.30.

## My opinion

The cheap December is a short window. If you budget on the December number, you will be wrong a month later. I'd plan on the January price.

The price per token is only half the bill. Google's pricing page lists the output price as including thinking tokens, and a different model can write more or fewer of them for the same task. I haven't measured this for 3.8 Flash, so test a few of your real prompts before Dec 1 and compare output tokens per request, not just quality.

Google's [deprecations page](https://aistudio.google.com/docs/deprecations) says calls to the old IDs after Dec 1 are routed to the new model. It also says AI Studio no longer lets you select the old models, and API access is limited to users who have used them before. So the old name keeps working for existing users, but it points at a different model.

## What I don't know

- How `gemini-3.8-flash` compares to `gemini-2.5-pro` on your tasks. I have no quality data.
- How many output tokens 3.8 Flash uses for the same job.
- Whether context caching or batch prices change with the reroute. I did not check them.
- Whether the Jan 1, 2027 price is final.
- Whether any option exists to opt out of the reroute. Neither the changelog entry nor the deprecations page mentions one.
- How long the old IDs keep routing after Dec 1. I did not find an end date.
- Vertex AI prices. The pricing page I used covers the Gemini Developer API and AI Studio only.

## Related

- Another Google price change, different model: [Gemini 4 Argon's price doubles on Dec 1](https://brightiny9.github.io/en/gemini-4-argon-price-doubles-dec-1/).
- Same changelog, nearby entries: Computer Use tool GA (Oct 30, 2026) and the Gemini API CLI `gemini-api` release (Oct 27, 2026). I did not cover them here.

## Sources (opened Nov 3, 2026)

- [Gemini API changelog](https://aistudio.google.com/docs/changelog)
- [Gemini API pricing](https://aistudio.google.com/docs/pricing)
- [Gemini API deprecations](https://aistudio.google.com/docs/deprecations)
