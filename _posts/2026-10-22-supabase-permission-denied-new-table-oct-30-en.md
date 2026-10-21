---
layout: post
title: "Supabase \"permission denied\" on a new table after Oct 30: what AI-written migrations miss"
lang: en
ref: supabase-permission-denied-new-table-oct-30
date: 2026-10-22
permalink: /en/supabase-permission-denied-new-table-oct-30/
---

From October 30, 2026, a new table in the `public` schema of an existing Supabase project is no longer exposed to the Data API automatically. A migration that creates a table without a `GRANT` will return `permission denied` (Postgres code 42501) when you call that table through the API. The fix is to add the `GRANT` statements to the same migration, and the error message already shows you the first one.

Our reading: the grant is the first gate, and RLS (Row Level Security) comes after it. Supabase's docs say "A table isn't reachable through the Data API unless you have granted a role privileges on it." ([Supabase docs](https://supabase.com/docs/guides/database/hardening-data-api), checked Oct 21, 2026). We take that to mean a table without a grant is blocked before your RLS policies matter. The docs do not spell it out in those words, so treat it as our interpretation of how Postgres permissions work.

{% include stat.html value="Oct 30, 2026" label="Date the new behavior applies to all existing Supabase projects" source="Supabase changelog, Breaking Change: Tables Not Exposed to Data and GraphQL API Automatically" url="https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically" date="2026-10-21" %}

> **Verdict:** Existing tables keep working. The break comes the first time a migration, a CLI script, or an AI tool adds a new table without a grant. Check your last few migrations before Oct 30 and add grants to your template.
{: .v-verdict}

## The short answer

Add grants for the roles that should reach the table, in the same migration that creates it. This is the example from the official discussion post, copied as published:

```sql
-- 1. Grant the privileges the role needs
grant select on public.your_table to anon;
grant select, insert, update, delete on public.your_table to authenticated;
grant select, insert, update, delete on public.your_table to service_role;

-- 2. Enable RLS
alter table public.your_table enable row level security;

-- 3. Add the policies you need
create policy "users can read their own rows"
  on public.your_table
  for select
  to authenticated
  using (auth.uid() = user_id);
```

Source: [Supabase discussion #45329](https://github.com/orgs/supabase/discussions/45329), checked Oct 21, 2026. The changelog shows the same statements. Replace `your_table` with your table name. The `anon` line is only there as an example. Whether `anon` should see anything is your call, and we come back to that near the end.

## What changes on Oct 30, and when

Supabase has rolled this out in steps since April. Here are the dates from the official changelog.

| Date | What happens | Source (checked Oct 21, 2026) |
|---|---|---|
| Apr 28, 2026 | Opt-in toggle available when you create a project | [Changelog](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically) |
| May 18, 2026 | `pg_graphql` not enabled by default | [Changelog](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically) |
| May 30, 2026 | New behavior is the default for all new projects | [Changelog](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically) |
| Oct 30, 2026 | Applied to all existing projects | [Changelog](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically) |

The practical point for most readers is the last row. If your project is older than May 30, nothing changed for you yet. On Oct 30 it does.

## Who is affected, who is not

The line is not "old project versus new project". It is how you reach the table.

| Situation | Affected? | Why |
|---|---|---|
| Your app reads or writes `public` tables through `supabase-js`, PostgREST, GraphQL, or direct HTTP to `/rest/v1/` or `/graphql/v1` | Yes, for new tables | These all go through the Data API |
| A migration creates a table with no `GRANT` | Yes, for that table | The table is not exposed by default |
| An AI tool or script creates tables and expects them to appear in the API | Yes | Same reason |
| Tables that already exist on Oct 30 | No | The discussion says existing objects keep their current grants |
| An app that connects with a direct Postgres connection (psql, an ORM, a connection string) | No | The changelog lists direct Postgres connections as not affected |

Sources: [changelog](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically) and [official discussion](https://github.com/orgs/supabase/discussions/45329), checked Oct 21, 2026.

The discussion post says that after October 30, a new table created in `public` without an explicit grant will return a "permission denied for table" error through the Data API.

Our reading: this is why a clean check today does not protect you. The risk is not in the tables you have. It is in the next table anyone adds, whether a person, a script, or an AI tool.

## Why AI-written migrations hit this

Supabase gives its reason directly. The changelog says that "agents, CLI scripts, and AI platforms create tables too, and many of those operations do not have a human reviewing the diff." Making access "a deliberate, code-level decision" is the stated goal.

Now the interpretation. This part is ours, not Supabase's.

Our reading: before this change, creating a table in `public` was enough to make it reachable. A migration that only said `create table` and `enable row level security` worked end to end. Code written in that style is everywhere, in docs, tutorials, and open repositories. An AI model that learned from that code may well leave the grants out, because for years leaving them out was correct. We have not tested any specific model, so read this as a likely pattern and not as a measurement.

The result is a failure that looks like a bug. The migration runs without errors. The table exists. The Supabase dashboard shows it. Then the first API call fails with `permission denied`, and the natural next step is to look at your RLS policies, which are probably not the problem.

The docs separate the two jobs. Per the [Supabase docs](https://supabase.com/docs/guides/database/hardening-data-api) (checked Oct 21, 2026), "Grants determine which Postgres roles can reach a table, view, or function over the Data API," while RLS policies "determine which rows those roles can read or modify." The grant answers "can this role reach the table at all". The policy answers "which rows". Our reading: if the first answer is no, the second never comes up. The docs do not state that order in so many words.

One caution. Supabase's [42501 troubleshooting page](https://supabase.com/docs/guides/troubleshooting/database-api-42501-errors) (checked Oct 21, 2026) says 42501 also appears when "the anon or authenticated roles attempt to UPDATE or INSERT values without the necessary RLS permissions." Our reading: so a 42501 on a brand-new table is not proof that a grant is missing, but it is the first thing to check, because a new table with no grant fails every request.

## The error message already tells you the fix

When a role has no grant, PostgREST returns `permission denied for table your_table`. The official changelog shows a hint field in the response:

> "Grant the required privileges to the current role with: GRANT SELECT ON public.your_table TO anon;"

([Supabase changelog](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically), checked Oct 21, 2026)

So the command is right there. What you do not get from the error is the decision behind it. The hint names the role that made the failing request. It cannot know which roles you want to allow.

Our reading: this changes what you need to learn. You do not need new syntax. You need to answer one question for every new table: which of `anon`, `authenticated`, and `service_role` should reach it, and with which operations? A signed-in-users-only table usually needs `authenticated` and not `anon`. A table that only server code touches may need only `service_role`. Copying the hint verbatim answers the question in the most open way possible, which is not always the right one.

## A migration review checklist

Run this on any migration that creates a table, especially one you did not write line by line.

1. **Does it create a table in `public`?** If yes, continue. The Supabase pages we read only describe the `public` schema, so we do not make claims about other schemas.
2. **Is there a `GRANT` in the same migration?** The discussion post says to bundle grants with your RLS and policy statements in the same migration.
3. **Does each grant name a role on purpose?** Look for `anon`, `authenticated`, and `service_role`, and ask whether each one should be there.
4. **Are the operations narrow?** `select` alone is different from `select, insert, update, delete`.
5. **Is RLS enabled and is there a policy?** The grant lets a role reach the table. The policy decides which rows it can touch. You need both.
6. **Is the `anon` grant really needed?** If not, delete it.

Before Oct 30, run this list on your last five migrations. Then run it on whatever template or prompt creates your next ones.

## One line to give your AI coding tool

The official discussion post says: "If you use an AI coding tool to create tables, update its system prompt or adopt the Supabase agent skill, which includes the grants step, and which we keep updated as the platform changes." ([Official discussion](https://github.com/orgs/supabase/discussions/45329), checked Oct 21, 2026)

If you would rather add one line yourself, here is an example. This is our example, not official wording:

```
When you create a table in the public schema, add explicit GRANT statements for the roles that need access, plus RLS and policies, in the same migration, and tell me which roles you chose and why.
```

The last clause matters. It forces the tool to show its choice, which brings back the human review that Supabase says is often missing.

## What this does not fix

The easy way out is to grant everything to `anon` and move on. It works. The error goes away. It also reopens exactly the exposure this change was designed to close: any table you create becomes reachable by anyone holding your public key, limited only by whatever RLS you remembered to write.

Our reading: that is the real trade. The change moves a safe default into your code, and the fastest fix quietly undoes it. A grant is a decision, so make it deliberately for each table. We are not quoting outside security numbers here, because we could not confirm them against original sources.

## FAQ

**Do existing tables need anything before October 30?**
No. According to the [official discussion](https://github.com/orgs/supabase/discussions/45329), existing objects keep their current grants. Your running app stays reachable. Only tables created after the cutover are affected.

**Does a direct Postgres connection (psql, ORM) change?**
The [changelog](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically) lists direct Postgres connections as not affected. The change is about Data API exposure, not about Postgres permissions in general.

**Does this apply to local `db reset` and preview branches?**
The discussion says to bundle grants with RLS and policy statements in the same migration. A maintainer comment in the thread discusses `db reset`, and we did not verify its details. Our reading: if your grants live in your migration files, a reset replays them, and if they live only in a dashboard click, a reset will not. We did not test a reset.

## Sources and last checked

All checked on Oct 21, 2026.

- [Supabase changelog: Breaking Change, Tables Not Exposed to Data and GraphQL API Automatically](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically) (published Apr 28, 2026)
- [Supabase docs: Data API hardening](https://supabase.com/docs/guides/database/hardening-data-api) (no publication date shown on the page)
- [Supabase docs: Database API 42501 errors](https://supabase.com/docs/guides/troubleshooting/database-api-42501-errors) (no publication date shown on the page)
- [Supabase discussion #45329](https://github.com/orgs/supabase/discussions/45329) (reactions and comment counts change over time)

Everything labeled "Our reading" is our interpretation, not Supabase's. We did not run these migrations against a live project.

**Before October 30, run the checklist on your last five migrations.**
