---
layout: post
title: "Lemon Squeezy is shutting down on March 31, 2027: what should a solo maker do first?"
lang: en
ref: lemonsqueezy-shutdown-what-to-do
date: 2026-11-20
permalink: /en/lemonsqueezy-shutdown-what-to-do/
---

First, check whether your business can use Stripe Managed Payments, because that decides everything else. Lemon Squeezy points sellers there, and it only accepts businesses based in 37 listed locations that sell fully automated digital products. If you pass that check, start by mid-January, which is Lemon Squeezy's own advice, and no later than Feb 3 if your move will take the full 8 weeks.

Published 2026-11-20. Sources checked on 2026-11-20: [Lemon Squeezy shutdown announcement (2026-11-16)](https://www.lemonsqueezy.com/blog/saying-goodbye-to-lemon-squeezy), [Lemon Squeezy migration guide](https://docs.lemonsqueezy.com/migration), [Lemon Squeezy fees](https://docs.lemonsqueezy.com/help/getting-started/fees), [Stripe Managed Payments overview](https://docs.stripe.com/payments/managed-payments), [Stripe Managed Payments eligibility](https://docs.stripe.com/payments/managed-payments/eligibility), [Stripe pricing](https://stripe.com/pricing), [Stripe Billing pricing](https://stripe.com/billing/pricing), [Paddle pricing](https://www.paddle.com/pricing), [Polar fees](https://polar.sh/docs/merchant-of-record/fees).

## What Lemon Squeezy actually said

From the announcement: "As of today, we've closed new store sign-ups, and Lemon Squeezy will stop processing payments on March 31, 2027." It adds: "Migration tooling will be available on December 2 to make the transition as easy as possible."

The migration guide fills in the rest:

- Nov 16, 2026: no new users or new store sign-ups.
- Dec 2, 2026: migration tooling launches.
- "To finish in time, start your migration no later than mid-January 2027."
- "The full process, including notifying customers, updating your links and integrations, and cleaning up remaining subscriptions, can take up to 8 weeks."
- Mar 31, 2027: Lemon Squeezy stops processing transactions, including subscription renewals.

## The dates, in days

We counted these ourselves from the dates above (the guide says "mid-January", so we used Jan 15 as our assumption):

| From | To | Days |
|---|---|---|
| Publish day (Nov 20) | Migration tool (Dec 2) | 12 |
| Migration tool (Dec 2) | Shutdown (Mar 31) | 119 |
| Mid-January (Jan 15) | Shutdown (Mar 31) | 75 (about 10.7 weeks) |
| Feb 3 (latest start for an 8-week move, Mar 31 minus 56 days) | Shutdown (Mar 31) | 56 |
| Mid-January (Jan 15) | Feb 3 | 19 |

Our read: the 8-week figure is a "can take up to", not a promise. If your move needs a new checkout, new webhooks, and a customer email, treat 8 weeks as the plan. Starting on Dec 2 gives you 119 days for a job that may take 56, which leaves a buffer of 63 days. Starting on Jan 15 leaves 19 days of buffer. That is the whole case for not waiting.

## Step 1: can you even move to Managed Payments?

Stripe's eligibility page says your business "must be based in one of the supported business locations". We counted 37: the US and Canada, 31 European locations (including GB, DE, FR, NL, IE and CH), and AU, HK, JP, SG. If your country is not on that list (for example, it does not list KR, IN or BR), the Stripe path is closed to you, and you need another merchant of record before March 31. In that case, export your data first, then compare Paddle and Polar in the fee table below, and check each one's own country rules before you commit. We did not verify their country lists.

The product has to qualify too. Stripe supports software, games, digital media, online courses, and electronic business services. It does not support physical goods, professional services such as consulting or development, or live in-person events. A product with human work in it, such as live 1-to-1 coaching, does not count as "fully automated".

## Step 2: what you lose by moving

According to Lemon Squeezy's guide, these do not come along: "PayPal: Not currently supported on Managed Payments." and "Storefronts: Not included. You'll need a separate website or storefront tool." The guide also says: "Managed Payments doesn't deliver files, license keys, or download links. You'll need a separate solution", and for affiliates: "Not included. You'll need a separate affiliate platform". Stripe's [overview page](https://docs.stripe.com/payments/managed-payments) lists unsupported setups too: Connect platforms, creating a subscription outside of Checkout or Payment Links, and one-off invoices on a subscription.

Subscribers are affected too. The guide says "PayPal subscriptions can't migrate. Customers will need to start a new subscription using a supported payment method", and customers with India-issued cards "need to reauthorize their payment method once their subscription moves to Stripe." Most other card subscriptions move without customers re-entering details.

If you sell through a Lemon Squeezy-hosted store page, you now need your own page. If a chunk of your buyers pay with PayPal, check how many before you move.

## Step 3: the fee math (our calculation)

Lemon Squeezy's fee page charges 5% plus $0.50 per order (its worked example reads "$0.50 + 5%"), +0.5% for subscription payments, and +1.5% for international or PayPal transactions. Stripe's pricing page says 2.9% + 30¢ for domestic cards, and lists Managed Payments at 3.5% on top. Stripe says subscriptions with Managed Payments are "Available with Billing", and Billing's pay-as-you-go price is "0.7% of Billing volume". Lemon Squeezy's guide says migrating merchants get a 1.5% promotional Managed Payments price through December 1, 2027, on top of standard Stripe fees.

Here is what each costs on one $20 monthly subscription, paid by a US customer with a US card to a US seller. We did the arithmetic:

| Option | Calculation | Fee | Share of $20 |
|---|---|---|---|
| Lemon Squeezy (now) | 5% + $0.50 + 0.5% | $1.60 | 8.0% |
| Stripe Managed Payments, promo, with Billing | 2.9% + $0.30 + 1.5% + 0.7% | $1.32 | 6.6% |
| Stripe Managed Payments, 3.5%, with Billing | 2.9% + $0.30 + 3.5% + 0.7% | $1.72 | 8.6% |
| Paddle | 5% + $0.50 | $1.50 | 7.5% |
| Polar, Starter plan | 5% + $0.50 | $1.50 | 7.5% |

What the table does not include: Polar's payout fees, and extra fees for non-US cards. International cards add 1.5% at Lemon Squeezy and at Polar. We assumed you would pay Billing's 0.7% pay-as-you-go price; your own Stripe plan may differ.

Our read: with the promo, Stripe costs about $0.28 less than Lemon Squeezy per $20 subscription payment ($1.32 vs $1.60), and that holds only until December 1, 2027. After that we found no published price. The nearest number is the 3.5% on Stripe's pricing page, and at that rate Stripe costs $0.12 more than Lemon Squeezy does today ($1.72 vs $1.60). Do not choose a provider on the promo alone. Your fee will likely rise after the promo ends.

## What to do this week

1. Check your business location and product type against Stripe's eligibility page. Ten minutes.
2. Export your customer, order and subscription data using Lemon Squeezy's export guide (linked from the announcement), and keep the files.
3. List what you use that Managed Payments does not cover: PayPal, storefront, file and license-key delivery, affiliates.
4. Put Dec 2 in your calendar for the migration tool, and a hard stop of Feb 3 for starting.

Related: another shutdown with a fixed export window is covered in [Mem is shutting down: how do I export my notes?](https://brightiny9.github.io/en/mem-shutdown-export-notes/).

## What we could not confirm

We did not confirm how Stripe prices Managed Payments after December 1, 2027, or the country rules of Paddle and Polar. We also did not test the migration tool, since it is not out until Dec 2. All prices come from the pages above on 2026-11-20 and may change.
