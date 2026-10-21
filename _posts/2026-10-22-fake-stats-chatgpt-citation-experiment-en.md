---
layout: post
title: "Did ChatGPT really cite 50,000 fake stats? What a Peec AI researcher claims, and what we can check"
lang: en
ref: fake-stats-chatgpt-citation-experiment
date: 2026-10-22
permalink: /en/fake-stats-chatgpt-citation-experiment/
---

A Peec AI researcher says ChatGPT kept pulling from a site of 50,000 invented statistics for seven months. Nobody outside the company has verified that yet.

The numbers come from the author's own analytics accounts, so we split what was measured from what was interpreted. A three-line check for your own numbers is at the end. We read the source on Oct 22, 2026. Our checks are listed in the limits section.

> **Verdict:** The claim is plausible and matches independent research on AI search. But the key numbers are one vendor's own count, and "cited" does not mean "trusted." Treat it as a strong lead, not a measured fact.
{: .v-verdict}

Other researchers see something similar. An Oct 2026 paper from a university team tested 10 AI search platforms. [Its abstract](https://arxiv.org/abs/2610.11932) says "8 of 10 platforms cited a fabricated concept within seven days" (checked Oct 22, 2026). That backs the direction of the claim. It does not back Peec's specific numbers.

## What the Peec AI researcher says happened

The [Peec AI post](https://peec.ai/blog/publish-stats-get-cited-the-tactic-that-put-my-data-all-over-the-web) is dated Oct 21, 2026. It opens bluntly. About seven months ago, it says, the author launched a website with 50,000 statistics, and "Every one of them was fake." (Quote from the page, checked Oct 22, 2026.)

Here are the headline claims, each with the tool the author names:

- **50,000 invented statistics** on one site, written with GPT-4.1. These were made up in the experiment. We do not repeat any of them.
- **More than 10,000 ChatGPT sessions** since launch, from the author's GA4 account. The post also uses the broader phrase "AI sessions" in places.
- **More than 330 referring domains** linking to the site, from Ahrefs and Semrush.
- **More than 600,000 bot requests** in 30 days, with around 72,000 from ChatGPT-User, from Cloudflare.
- **Google deindexed the pages.** In the author's words, "ChatGPT hasn't."

The author also says the invented numbers showed up in an academic paper, an investment research note from a large Qatari financial group, an Indian economics outlet and a Canadian influencer community report. We could not check any of those.

{% include stat.html value="330+" label="Linked domains the author counts for the fake-stats site (author's own count, unverified)" source="Peec AI blog post, Ahrefs and Semrush per the author" url="https://peec.ai/blog/publish-stats-get-cited-the-tactic-that-put-my-data-all-over-the-web" date="Oct 22, 2026" %}

One detail matters for how you read the post. It ends on a product pitch: the author says Peec uses its own tool for this kind of tracking. Peec AI sells tracking for how brands appear in AI answers. That is not a crime. It is a reason to ask who benefits when the number is large.

## What is measured vs. what is interpreted

Not every sentence in the post is the same kind of claim. Our reading, sorted:

| Claim | Tool named | Checked by a third party? | Our verdict |
|---|---|---|---|
| 10,000+ ChatGPT sessions (GA4, author's account) | GA4 (author's account) | No | Plausible, unverified |
| 330+ referring domains | Ahrefs, Semrush | No | Plausible, unverified. Anyone with access can re-count |
| 72,000 ChatGPT-User requests in 30 days | Cloudflare | No | Plausible, unverified |
| Fake stats appeared in a paper and a financial note | Not stated | No | Unchecked |
| "Retrieval is not ranking" (why it works) | None, it is an explanation | No | Interpretation |
| Google deindexed it, ChatGPT kept fetching | Search Console, Cloudflare | No | Plausible, unverified |

The last two rows are the weakest. A bot fetching a page is a measurement. Why it fetches is a guess. The post does not isolate the cause with a control site, and one site cannot show what ChatGPT does in general.

## Other experiments point the same way, with caveats

This is not the first fake-content test, and the earlier ones show how much interpretation matters.

In Dec 2025, [Ahrefs ran a made-up brand experiment](https://ahrefs.com/blog/ai-vs-made-up-brand-experiment/) and concluded that the most detailed story wins, even if it is false. Weeks later, [Search Engine Journal replied](https://www.searchenginejournal.com/ahrefs-tested-ai-misinformation-but-proved-something-else/564124/) (Dec 28, 2025). Its main point: of 56 prompts, 49 were leading questions and only 7 were neutral. SEJ's reading was that AI systems favor content that matches the question's wording, not that they pick lies over truth.

Same data, two stories. That is the best argument for separating measurement from interpretation.

The newer paper adds hard numbers, though we got them through SEJ. [SEJ's Oct 19, 2026 report](https://searchenginejournal.com/ai-search-tools-cited-a-made-up-concept-within-a-week-paper-finds/593472) lists how often each tool cited the invented concept. We checked the paper's abstract for the "8 of 10" line only. The per-tool counts below are SEJ's, not ours:

{% include bars.html title="Share of answers citing the made-up concept (my calculation from SEJ counts)" items="Grok|94;Google AI|45;Perplexity|37;ChatGPT|35" unit="%" highlight="4" source="Search Engine Journal report on arXiv 2610.11932, per SEJ counts 30/32, 15/33, 13/35, 7/20" url="https://searchenginejournal.com/ai-search-tools-cited-a-made-up-concept-within-a-week-paper-finds/593472" date="Oct 22, 2026" note="Percentages are our division of SEJ's counts. Small samples. Not verified against the paper's tables." %}

Look at the ChatGPT bar. In that study ChatGPT cited the fake concept in 7 of 20 answers. That is the lowest rate of the four. So "ChatGPT cites fake stats" is true in the sense that it happens. It is not true in the sense that ChatGPT is the worst offender. One vendor's experiment aimed at one tool should not be read as a ranking.

Two more details keep this from turning into "AI believes anything." SEJ's summary of the paper says invented concepts got cited, while fake products and opinion pieces were rarely cited (SEJ, Oct 19, 2026, a secondary summary we did not check against the paper). And per Ahrefs' write-up of its own experiment, ChatGPT cited the official FAQ in most responses (Ahrefs, Dec 10, 2025, read through a summary, so we do not state it as settled). Both point the same way: the models pick up some kinds of fake content, not all of it.

Evidence strength: medium on direction (two independent teams, different methods), weak on size (small samples, one site, one summary layer).

## Our reading: what this does and doesn't tell a small maker

Everything in this section is our interpretation, not a finding from either source.

**1. "Fetched" is not "verified."** The Peec numbers describe retrieval: bots requested pages, and links appeared. Nothing in the post shows ChatGPT believed the data. It shows a pipeline that fetches pages matching a query like "statistics 2026." The post gives that kind of explanation itself. For a maker, the lesson is narrow. Being quoted tells you a model found your page. It does not tell you the model trusts you.

**2. The cost of reach looks tiny, which is the risk.** Our calculation: the post says it spent about $50 in total, $30 on the stats pages plus about $20 on 15,000 listicles added later. Divide by 10,000 sessions: 50 ÷ 10,000 = $0.005 per session. This assumes the author's numbers are right, and "cost per session" is our own metric, not theirs. Since March 2026, about seven months, 10,000 sessions averages roughly 50 a day. That is small traffic. The real story may be the 330 links, not the visits. Cheap attention for fake data also means cheap noise for everyone else, and honest numbers have to stand out from it.

**3. Vendors measure what their product sells.** The 72,000 ChatGPT-User requests are about 12% of 600,000 total bot requests (72,000 ÷ 600,000, our division). That is a useful detail. It also appears in a post by a company that tracks AI visibility. We are not saying the numbers are wrong. We are saying the post cannot be read as neutral.

The post's author says plainly that no one should publish fake content, and that sentence is fair to include. The experiment also had a disclaimer on the live site, per the page. We take the stated intent at face value.

## A 3-line check before you trust or publish a number

This is our own check, built from the table above. It is a rule of thumb, not a tested method, and the evidence for it is weak. It is the product of two sources and our reading.

1. **Who measured it?** Your own analytics, or a third party you can name?
2. **Is there a date and a method?** Which tool, what period, what was counted?
3. **Does the writer sell something the number supports?** Is that said in the text?

Run the Peec post through it. Line 1 fails: the author's own accounts. Line 2 half-passes: tools named, dates given, no outside check. Line 3 is disclosed, but late and softly.

Now run your own numbers through it before you publish them. Say "our GA4, Oct 1–21, 2026, sessions with a ChatGPT referrer" instead of "lots of AI traffic." Name the vendor interest if you have one. Proadcast, our product, lists maker products and has the same bias, so we apply the same check to our own claims.

Use these three lines before you cite any number, ours included.

## Disclosure and limits

- **Interest.** Peec AI sells AI visibility tracking. We have no relationship with them. We have our own product (Proadcast) in a nearby space.
- **How we read the source.** We opened the Peec page, the arXiv abstract, and the SEJ pages on Oct 22, 2026. We could not check the claimed citations in the paper or the financial note, or the paper's own per-tool tables.
- **Not tested here.** Whether publishing statistics pages helps a real site get cited. The post says its real-data rerun worked. We have not seen that data.

If you spot an error, tell us and we will fix it and say so here.
