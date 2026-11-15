---
layout: post
title: "Is my Lovable or Supabase app leaking user data? How to check in 10 minutes"
lang: en
ref: lovable-supabase-exposure-check
date: 2026-11-15
permalink: /en/lovable-supabase-exposure-check/
---

You built an app with Lovable, it uses Supabase, and you just read the headlines. Short answer: your app is exposed if a Supabase table in the `public` schema has Row Level Security (RLS) switched off, or if a table still gives the `anon` role grants you never meant to give. Supabase's own checker, the Security Advisor, flags the first case. For a small project with a few tables, the steps below take about ten minutes (steps 3 and 5 are timed per table). They come from Supabase's docs.

This is a checklist built from public research and public docs. We did not scan anyone's app, and nothing here replaces an expert review if you hold passports, payments, or private chats.

## What the research found (a claim by researchers)

Crissy Field, a German security firm, published a study on Lovable apps. It was reported together with the business daily Handelsblatt. The study page says it carries newer figures than Handelsblatt's 2026-11-02 article, and the numbers below are the page's. HN posted the study on 2026-11-14 ([Hacker News, 679 points when we checked on 2026-11-15](https://news.ycombinator.com/item?id=50499017)).

Numbers from [the study](https://www.crissyfield.de/research/lovable-en/) (checked 2026-11-15):

- 159,041 Lovable projects analysed, from Common Crawl archives, December 2025 to September 2026.
- 34,545 of them used Supabase.
- 24,664 websites sent database records "as soon as they loaded, without requiring a login or any other interaction."
- With extra read-only requests, the researchers found email addresses in 10,560 tables across 7,403 of those sites. That is 7,403 of the 24,664 websites (30%).
- Examples they list: 80,000+ profiles from one forum, 200,000+ chat messages, 1,000+ identity records with passport data, 280,000 customer emails.

The researchers add their own warning: email addresses "may also be public contact addresses or test data," so the 30% is not a confirmed leak rate. They also say the sample does not represent all Lovable apps. Treat the findings as one research team's measurement, not as an audit that anyone else has repeated.

**What did Lovable say?** The study page only says Handelsblatt contacted Lovable with the findings; it prints no reply. We found no Lovable statement on Lovable's own site. One article from 2026-11-14 ([Trending Topics](https://www.trendingtopics.eu/lovable-apps-sensitive-data-exposed/)) reports that the company calls it "a known, industrywide configuration problem with Supabase." That is a news outlet's report, second-hand, and we could not check it against a Lovable page. The same article says Lovable added security tools after a similar 2025 problem. Lovable's [docs](https://docs.lovable.dev/features/security) describe two built-in scans, Quick scan and Deep scan, and say they "cannot guarantee complete security." The same page says you are responsible for making sure your app meets the security requirements of its use case.

## Our own arithmetic on the study's numbers

These are our calculations from the figures above, not new data:

| Ratio | Calculation | Result |
|---|---|---|
| Supabase share of the sample | 34,545 / 159,041 | 21.7% |
| Supabase sites sending records on load | 24,664 / 34,545 | 71.4% |
| Same sites as a share of the whole sample | 24,664 / 159,041 | 15.5% |
| Sites with emails among those | 7,403 / 24,664 | 30.0% |
| Email tables per such site | 10,560 / 7,403 | 1.4 |

Two cautions. First, "sent records on load" is not the same as "sent private records." A public blog's post list should load without login. The researchers' email check is a rough way to find personal data, and they say so. Second, Common Crawl only holds pages that a crawler reached, so 159,041 is not the number of all Lovable apps. Read 71.4% as "of Supabase-backed apps in this sample, seven in ten sent some records to a signed-out visitor," and no more than that.

## How Supabase is built: the key is public on purpose

A Supabase app in the browser holds a publishable key (older projects call it the anon key). Supabase's [API keys page](https://supabase.com/docs/guides/api/api-keys) says this key is "Safe to expose online: web page, mobile or desktop app, GitHub actions, CLIs, source code." The reason it is safe is that "Row Level Security decides what this client can reach, so enable it on every table before you deploy."

That sentence is the core of how Supabase works. The key being public is normal. Supabase's protection is RLS plus the database grants. The study does not say which setting failed on the exposed sites, so what follows is our reading of the docs: if those protections are missing, anyone who opens your site and reads its network requests can use the same key to ask for rows.

Supabase's [RLS guide](https://supabase.com/docs/guides/database/postgres/row-level-security) states the risk plainly: "A table in an exposed schema without RLS is readable and writable by any role with a grant on it." It also says that on existing projects "a new table in `public` starts with every privilege already granted to all three roles," and adds that "Not every project grants these automatically." So check your own project instead of assuming either way.

## The 10-minute check

Do this in your Supabase dashboard. Work on a copy or a staging project first if you can.

**Step 1: Run the Security Advisor (2 minutes).**
Supabase's [linter docs](https://supabase.com/docs/guides/database/database-linter?lint=0013_rls_disabled_in_public) describe a lint called "RLS Disabled in Public." The docs say that without RLS on a `public` table, "anyone with the project's URL can CREATE/READ/UPDATE/DELETE (CRUD) rows in the impacted table" (the lint is listed as 0013). Open the [Security Advisor](https://supabase.com/docs/guides/database/database-advisors) in the dashboard (or run `supabase db advisors` in the CLI) and read every warning. Any hit on a table with user data is urgent.

**Step 2: List your tables and look for RLS (3 minutes).**
Open the Table Editor and go through each table in `public`. For each one, write down: does it hold anything personal (emails, names, messages, files, payments)? Is RLS enabled? A table with personal data and RLS off is what Supabase's docs describe as open to anyone. The study itself does not name RLS as the cause; linking the two is our inference from the docs.

**Optional (our addition, standard Postgres, not a Supabase step): list tables with RLS off.**

```sql
select schemaname, tablename, rowsecurity
from pg_tables
where schemaname = 'public' and rowsecurity = false;
```

Run it in the SQL editor. Every row returned is a `public` table with RLS off.

**Step 3: Turn RLS on (1 minute per table).**
The documented command is:

```sql
alter table public.reports enable row level security;
```

Replace `reports` with your table name. Supabase warns that "Once RLS is enabled, no data is accessible through the API when using a publishable key, until you create policies." Your app may look broken right after this. That is the protection working, and it is why you test on a copy first.

**Step 4: Add the smallest policy that works (3 minutes).**
Supabase's example lets a signed-in user read only their own row:

```sql
create policy "Users can view their own profile."
on profiles for select
to authenticated
using ( (select auth.uid()) = user_id );
```

Adapt the column name to your table. Write one policy per need (read, insert, update, delete) and keep each one narrow. Do not write a policy that lets everyone through, such as `using (true)`; that gives back what you just removed. (Our addition: Lovable's own docs say its database review flags "rules that let everyone through," which is the same trap.)

**Step 5: Revoke grants you do not want (1 minute per table).**
Supabase's RLS guide says to revoke existing grants from the client roles and then give back only what each role needs:

```sql
revoke all on table public.reports from anon, authenticated;
```

The docs add a point many guides skip: adding policies does not take those grants back, so a table protected only by policies can still hand `anon` an insert path if you never revoke the grant. Use RLS and grants together. Supabase's [Data API guide](https://supabase.com/docs/guides/api/securing-your-api) says the same: "Use both controls for every exposed object."

**Step 6: Check where the secret key lives (1 minute).**
The `service_role`/secret key skips RLS. The API keys page says "Never put one in a browser, a shipped application, or source control," and lists places it must never appear: a web page, public document, source code, or a bundled app. Search your front-end code for it. If it ever shipped, rotate it.

**Step 7: Check your database functions.**
Supabase's [Data API guide](https://supabase.com/docs/guides/api/securing-your-api) says "RLS doesn't apply to functions, so grant `execute` only to the roles that need to call them," and asks you to review every `security definer` function carefully. If Lovable generated functions for your app, read them and check who can call them.

**A signed-out look (our addition, not a Supabase step).** The study counted sites that send records on first load without login. You can imitate that test: open your app in a private browser window and see what appears before you sign in. If you can see other people's data, treat it as confirmed exposure. If you see nothing, that is encouraging but not proof. A table can still be reachable by a direct request.

## What this does not tell you

- It cannot tell you whether anyone already read your data. Supabase's docs we read describe no log of what an anonymous reader fetched, so we do not claim you can find out. If personal data was exposed, check your local legal duties on breach notice.
- It does not prove Lovable or Supabase is "at fault." The study shows apps with open data. Lovable (second-hand) points to Supabase configuration; the study's recommendation is that "an easy-to-use development platform does not remove the need for an expert review of access permissions before an application handles confidential data." Both can be true at once.
- We have not tested these steps on a live app. They are the documented commands.

## Our take

If you ship anything with logins, fix RLS before you add features. Steps 1 to 5 are cheap compared with the cost of leaking user data. This is our opinion, based on the docs, not a measured result. We have no related posts to link yet.

*Sources and check dates: all pages above were read on 2026-11-15. Supabase docs and Lovable docs change, so recheck before you rely on a command.*
