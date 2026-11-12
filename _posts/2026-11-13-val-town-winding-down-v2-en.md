---
layout: post
title: "Val Town is winding down: when do my vals stop working, and where can I move?"
lang: en
ref: val-town-winding-down-v2
date: 2026-11-13
permalink: /en/val-town-winding-down-v2/
---

**Val Town is shutting down. Its code goes read-only on Dec 10, 2026. Apps (called "vals") keep running until Jan 10, 2027. So you have until Jan 10 to move running apps, and until Dec 10 to edit code. SQLite and blob storage are listed as outside the Dec 10 read-only step, so export them early anyway.**

Val Town's [announcement](https://blog.val.town/winding-down) is dated Nov 10, 2026. Its [migration docs](https://docs.val.town/migration) were last updated Nov 7, 2026. I opened both on Nov 11, 2026, and checked again on Nov 13, 2026. The dates and mappings below come from those pages. The checklist and the take are my own.

## The dates

| Date | What happens (Val Town's words, short) |
|---|---|
| Nov 10, 2026 | New signups and upgrades end. Billing pauses. |
| Dec 10, 2026 | Read-only mode begins, "not including sqlite and blob storage". |
| Jan 10, 2027 | All other services end. |
| Feb 1, 2027 | Open-sourcing is planned. |

The docs say it more plainly: "Code on Val Town will become read-only on December 10, 2026. Apps on Val Town ("vals") will continue running until January 10, 2027."

Counting from Nov 13, that is 27 days to Dec 10 and 58 days to Jan 10.

What this means in practice:

- After Dec 10 you cannot edit your code on Val Town. A bug in a live val will stay a bug.
- A val that is already running keeps running until Jan 10. A webhook or cron job does not stop on Dec 10 just because the code is read-only.
- Plan to have the new copy working before Dec 10. That is the last day you can still fix things in place.

## Why, and what about money

The announcement says the business "couldn't compete in the cloud computing space". Billing is paused, and existing subscriptions are served for free. For annual plans, the post says: "If you pre-paid for our annual plan, we will issue you a partial refund." It does not say how the partial refund is calculated.

## Where to move

The post says "We have guides for migrating to Cloudflare, Vercel, Netlify, and Render." The docs list those plus GitHub and Redirects.

The docs also say Deno itself is winding down: "The core maintainers won't support Deno beyond October 2027". They suggest Node, Bun, Cloudflare Workers, or Vercel Functions. So if your code is Deno-based, the runtime is on a clock too.

Val Town's own "where to migrate" page calls Cloudflare the most complete feature match, and says some Val Town team members have decided to move their own vals there, including the Val Town blog and docs. That is Val Town's view, not an independent test.

Here is part of the Cloudflare mapping from the docs (the [full page](https://docs.val.town/migration/cloudflare) has more rows):

| In Val Town | On Cloudflare |
|---|---|
| std/sqlite | D1 |
| std/blob | R2 |
| cron vals | Cron Triggers |
| email vals | Email Routing |
| std/email (sending) | Email Service |
| std/openai | AI Gateway |
| Val Town Access | Cloudflare Access |
| custom domains | Worker Custom Domains |

The Cloudflare guide has nine sub-guides: secrets transfer, SQLite export, blob export, email setup, access controls, domain migration, AI integration, code refactoring, and cron conversion.

If you do not want Cloudflare, the "where to migrate" page lists options for the parts that are not code: Turso or D1 for SQLite, Cloudflare R2, AWS S3, or Vercel Blob for files, Resend, Postmark, or SendGrid for sending email, and Cloudflare Email Routing or Mailgun for receiving (examples, not the full list). It also lists Lovable, Replit, v0, ChatGPT Sites, and Claude Artifacts as alternatives for quick vibe-coded apps.

## My checklist (not from Val Town)

1. List everything that still runs: HTTP vals, cron vals, email vals, anything other services call by URL.
2. Copy the code out now. Do not wait for the Feb 1 open-source plan, because the post does not say what will be released.
3. Export SQLite data and blobs next. Both have export guides in the Cloudflare docs. Do this first among the data tasks, and keep a second copy.
4. Rebuild on the new host and test it with real inputs.
5. Change the URLs that other services call (webhooks, forms, bots) once the new host works.
6. Keep the old val running until the new one has handled a day of traffic. This works until Jan 10, but remember you cannot edit the old one after Dec 10.

## What I could not check

- I did not run any of the migration guides, so I cannot say how well they work.
- The docs say SQLite and blob storage are not part of the Dec 10 read-only step. They do not say whether you can still write to them between Dec 10 and Jan 10, so do not rely on that.
- Who runs the code after Feb 1, and under what license. The post does not say.
- How the partial refund is calculated.

If you are stuck, the post gives support@val.town and Discord.

## My take

A shutdown has two deadlines, and they are about different things. Dec 10 is the deadline for changing your code. Jan 10 is the deadline for everything still running, data included. Start with the data export, because data you forgot to export is gone, and code is easy to copy. Then move the code before Dec 10, so the last month is only for watching traffic and fixing the small things you missed.

*Sources, opened Nov 11, 2026 and checked again Nov 13, 2026: [Val Town, "winding down"](https://blog.val.town/winding-down); [Val Town docs, migration](https://docs.val.town/migration); [Migrate to Cloudflare](https://docs.val.town/migration/cloudflare); [Where to migrate](https://docs.val.town/migration/where-to-migrate).*
