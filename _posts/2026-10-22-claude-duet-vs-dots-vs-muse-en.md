---
layout: post
title: "Claude Duet vs OpenAI Dots vs Meta Muse: Who Can Use It Today, and What the Docs Say About Price and Limits"
lang: en
ref: claude-duet-vs-dots-vs-muse
date: 2026-10-22
permalink: /en/claude-duet-vs-dots-vs-muse/
---

Claude Duet is a research preview you can only join by waitlist today, and only if you are a US Pro or Max subscriber ([Anthropic help article](https://claude.com/resources/articles/claude-duet), checked Oct 22, 2026). Anthropic's pages show no separate price and no usage-limit number. Duet is "included in Pro and Max plans" and shares your plan's limits. We have not used Duet. This post is built from the official pages and public articles only.

> **Verdict:** If you are a solo builder outside the US, you cannot use Duet yet, and nobody can price it for you. The one cost fact Anthropic gives is that Duet draws on the same usage limits as the rest of Claude, and it gives no number for them. We would not plan a budget around it until that number exists.
{: .v-verdict}

**Short version**

- Who: US Pro and Max subscribers, by waitlist. Team and Enterprise plans are not included yet.
- Cost: no extra price in the official text, and no published limit number.
- Known limits: Anthropic itself says Duet "may misread a thread or miscalibrate what's urgent."
- Dots and Muse: we could not read OpenAI's Dots page today (HTTP 403), and we did not check Meta's Muse pricing for this post.

## What is Claude Duet?

Anthropic's product page calls it "a proactive agent that understands what needs your attention" ([product page](https://claude.com/product/claude-duet), Oct 22, 2026). It watches your connected accounts, then drafts or does the next step. The help article says it "checks your connected accounts every few hours" and was "designed around Claude Opus 5.5" ([help article](https://claude.com/resources/articles/claude-duet), Oct 22, 2026).

The connector list is large. Anthropic says Duet can use "the over 6,000 connectors and plugins in the Claude Marketplace."

{% include stat.html value="6,000+" label="Connectors and plugins Duet can use, per Anthropic" source="Anthropic, Claude Duet help article" url="https://claude.com/resources/articles/claude-duet" date="Oct 22, 2026" %}

That is a count of what exists, not of what works well. We have no way to judge quality without using it.

## What the official pages say

Here is every price, limit and safety fact we found on Anthropic's two pages. Blank rows are blank on purpose.

| Item | Official wording | Source | Checked |
|---|---|---|---|
| Status | "A research preview is available by waitlist today, starting with US Pro and Max subscribers." | [Help article](https://claude.com/resources/articles/claude-duet) | Oct 22, 2026 |
| Region | "Available in Pro and Max plans in the US." | [Product page](https://claude.com/product/claude-duet) | Oct 22, 2026 |
| Not included | "Team and Enterprise plans are not included yet." | [Product page](https://claude.com/product/claude-duet) | Oct 22, 2026 |
| Price | "included in Pro and Max plans and uses the same usage limits as the rest of Claude." No separate amount | [Help article](https://claude.com/resources/articles/claude-duet) | Oct 22, 2026 |
| Usage limit | During the research preview, Duet "shares your plan's usage limits with the rest of Claude, and it uses them differently than a typical conversation does." Official limit number: none | [Help article](https://claude.com/resources/articles/claude-duet) | Oct 22, 2026 |
| Known limits | "It may misread a thread or miscalibrate what's urgent, and it can miss something that arrives between checking in with you." | [Product page FAQ](https://claude.com/product/claude-duet) | Oct 22, 2026 |
| Needs your approval | "sends a message, makes a payment, signs a document, or deletes anything" | [Help article](https://claude.com/resources/articles/claude-duet) | Oct 22, 2026 |
| Never allowed | "trading securities or moving money between accounts" | [Help article](https://claude.com/resources/articles/claude-duet) | Oct 22, 2026 |
| Passwords | "it never directly sees your passwords or sign-in tokens" | [Help article](https://claude.com/resources/articles/claude-duet) | Oct 22, 2026 |
| Where logins run | "Approvals, logins, and safety checks run in your own cloud computer" | [Product page](https://claude.com/product/claude-duet) | Oct 22, 2026 |

The help article is dated October 21, 2026. It links a "See pricing" page, and the link goes to the API pricing section. The Duet text itself names no amount.

## What Anthropic says is not ready yet

Most launch coverage skips this, but Anthropic writes its own limits down. The product page FAQ says Duet is a research preview that "may misread a thread or miscalibrate what's urgent, and it can miss something that arrives between checking in with you." The help article repeats that it "still might misread a thread or miscalibrate what's urgent" ([product page](https://claude.com/product/claude-duet) and [help article](https://claude.com/resources/articles/claude-duet), Oct 22, 2026). The help article also says Duet "can't yet show you its browser" (same help article, same date).

Our interpretation: put the quote next to the "every few hours" check schedule and you get a plain reading. Duet is built for slow-moving inbox and calendar work, not for things that must be caught within minutes. If a customer email or a failed payment needs a reply fast, do not count on Duet being the one to see it. This is our reading of two official lines, not a test result.

## Where the news articles differ

A Korean outlet reports that Duet comes with Pro at $20 a month, that OpenAI's Dots needs a Pro plan of $100 or more, and that Meta's Muse has more than 14 million installs as of Oct 21, per the article ([Digital Today](https://www.digitaltoday.co.kr/news/articleView.html?idxno=709007), shared Oct 22, 2026). These are the article's claims.

We could not confirm any of the three from a first-party page:

- **$20 for Pro:** not on the Duet pages we read. They say "included in Pro and Max plans" and nothing about dollars.
- **Dots at $100 or more:** OpenAI's [Dots page](https://openai.com/index/introducing-dots/) returned HTTP 403 for us on Oct 22, 2026. We cannot check it.
- **Muse at 14 million installs:** we found no first-party source.

So the headline most readers will see, a price, is not in Anthropic's own text. That gap is the main finding of this post. Also, the 9to5Google launch story ([Oct 21, 2026](https://9to5google.com/2026/10/21/claude-duet-anthropic-ai-agent-waitlist/)) does not mention price or region in what we read, which is why we built the table above.

## Approval and login handling (our interpretation)

Two different things are being handed over, and they carry different risks. One is your accounts. The other is your actions.

**Accounts.** Anthropic says Duet "never directly sees your passwords or sign-in tokens", and that logins run in a cloud computer set up for you. We cannot test that claim. We can say it is a specific, checkable promise, and that it is stronger than a vague "we take privacy seriously."

**Actions.** Anthropic splits them into two lists.

- Needs approval: send a message, make a payment, sign a document, delete anything. That is 4.
- Never, even with approval: trade securities, move money between accounts. That is 2.

{% include stat.html value="4 vs 2" label="Action types that need your approval versus action types that are blocked even with approval, per Anthropic" source="Anthropic, Claude Duet help article" url="https://claude.com/resources/articles/claude-duet" date="Oct 22, 2026" %}

For a solo builder with Stripe and a business bank account connected, the second list matters more than the first. A payment needs your click. A transfer between your own accounts is not possible at all. That is a hard wall, and it is a design choice we like.

How do Dots and Muse compare? Less is known. Our [earlier post](https://brightiny9.github.io/en/muse-vs-dots-confirmed-and-blank/) (Oct 16, 2026) found that Meta says Muse checks with you before sensitive actions like sending an email or making a purchase, and shows "a complete audit trail." For Dots, we could read only a 28-word summary that says users "stay in control." The Dots detail is blank, so we make no comparison on it.

## The cost question (our interpretation)

Here is the logic, and it is ours, not Anthropic's. Duet is "included," which means no new line on your bill. But in the preview it "uses them differently than a typical conversation does," and it checks your accounts every few hours. So background work can spend the same limit you use for chat and coding.

Anthropic gives no limit number. So the real cost to you, in lost chat capacity, cannot be calculated today. We think that uncertainty is the actual risk for a small maker: "free" with an unknown meter is not the same as free. Limits may also change after the preview ends. Our advice is to treat this as unpriced until Anthropic publishes a figure.

## What a solo builder can do now

| Your situation | What you can do today | Why |
|---|---|---|
| US, on Pro or Max | Join the waitlist on the [official page](https://claude.com/product/claude-duet) | Stated eligibility, Oct 22, 2026 |
| US, on Team or Enterprise | Wait. These plans are "not included yet" | [Product page](https://claude.com/product/claude-duet) |
| Outside the US | Read and watch the pages. Duet is US-only in this preview. We could not confirm whether any other region is planned | Help article, Oct 22, 2026 |
| Budgeting | Do not budget yet. Limits are shared and no number is published | Help article, Oct 22, 2026 |
| Time-critical alerts | Do not rely on it yet. It checks every few hours and can miss items between check-ins | [Product page FAQ](https://claude.com/product/claude-duet), Oct 22, 2026 |
| Choosing between Duet, Dots, Muse | Wait for price pages. Dots: page unreadable (HTTP 403, Oct 22). Muse: pricing not checked for this post | [Our Muse vs Dots post](https://brightiny9.github.io/en/muse-vs-dots-confirmed-and-blank/) |

## FAQ

**Is Claude Duet free?**
Anthropic's text shows no separate price. Duet is "included in Pro and Max plans," so you need one of those paid plans, and it shares their usage limits ([help article](https://claude.com/resources/articles/claude-duet), Oct 22, 2026).

**Can I use Claude Duet in Korea or outside the US?**
Not today, as far as the official pages say. The preview starts with US Pro and Max subscribers ([product page](https://claude.com/product/claude-duet), Oct 22, 2026). We could not confirm any plan for other regions.

**Can Duet move money between my accounts?**
No. Anthropic lists "trading securities or moving money between accounts" as never allowed, even with your approval ([help article](https://claude.com/resources/articles/claude-duet), Oct 22, 2026). Payments are different: those need your approval.

**What does Anthropic say Duet gets wrong?**
That it "may misread a thread or miscalibrate what's urgent" and can miss something that arrives between check-ins ([product page FAQ](https://claude.com/product/claude-duet), Oct 22, 2026).

## Interest

On Hacker News the Duet announcement had 306 points and 267 comments when we checked on Oct 22, 2026 ([HN item](https://news.ycombinator.com/item?id=50186037)). That tells you people care. It does not tell you the product is good.

{% include stat.html value="306 points" label="Hacker News score for the Claude Duet thread at check time, with 267 comments" source="Hacker News" url="https://news.ycombinator.com/item?id=50186037" date="Oct 22, 2026" %}

For the Muse side, see our post on [Muse Spark Open and small makers](https://brightiny9.github.io/en/muse-spark-open-small-makers/).

**Corrections:** none so far. We will update the table when Anthropic publishes limits, a price, or new regions. Last checked: Oct 22, 2026.
