---
layout: post
title: "Is Web Scraping Legal in 2026? A Small Team's Guide (Korea, US, EU)"
lang: en
ref: lawful-web-data-collection-2026
date: 2026-10-21
permalink: /en/lawful-web-data-collection-2026/
---

Scraping public pages is generally not banned by law in Korea, the US or the EU. The risk comes from a site's terms, its robots.txt, and how much you copy. This is not legal advice, and everything below was checked on 2026-10-21 unless a line says otherwise.

> **Verdict:** Public does not mean free to take. Of the scrapers in the cases below, the one criminal defendant won, but most civil outcomes went against the scraper. For a small team, the safe rule is to skip any source whose terms or robots.txt say no.
{: .v-verdict}

Three-line summary:

- Criminal risk looks low for plain public-page reading in Korea, but one acquittal is thin ground to build a business on.
- Civil risk is where the money is lost: contracts, unfair-competition law, and database rights.
- Of the 8 sources we checked, 5 are closed, 1 is conditional, 1 is open and 1 is unclear (my calculation).

## First, "public" is not "anything goes"

A page that loads without a login is visible. That is all it tells you.

Whether you may copy it at scale depends on at least four other things: the site's terms, its robots.txt, copyright and database law, and privacy law if people's names are in the data.

Most "is scraping legal" articles stop at one court case. That is a mistake, because the cases point in different directions. The next section puts them side by side.

## The case map

Here is the short version first. Details follow by country.

| Case | Outcome | The catch | Source |
|---|---|---|---|
| Yanolja v Goodchoice, Korea, criminal | Acquitted (Supreme Court, 2022-05-12) | Facts were narrow: no API protection, 3 to 8 items copied, vague terms | [Shin & Kim newsletter](https://www.shinkim.com/kor/media/newsletter/1843) |
| Yanolja v Goodchoice, Korea, civil | Scraping ruled unlawful: 1 billion won damages (first-instance court, 2021-08-19) | Appeal court also found it unlawful (reported 2022-08-26) | [Shin & Kim](https://www.shinkim.com/kor/media/newsletter/1843), [appeal report](https://v.daum.net/v/20220826110606958) |
| Jobkorea v Saramin, Korea | Unfair-competition liability (Seoul Central District Court, 2016-02-17) | Court awarded 500,000 won per copied listing | [NEPLA wiki summary](https://www.nepla.ai/wiki/지식재산/부정경쟁/데이터-부정사용-rv5n72p1g8zm) |
| hiQ v LinkedIn, US | LinkedIn won on breach of contract | Consent judgment approved 2022-12-08, $500,000 | [Proskauer, 2022-12-08](https://newmedialaw.proskauer.com/2022/12/08/hiq-and-linkedin-reach-proposed-settlement-in-landmark-scraping-case/) |
| Meta v Bright Data, US | Court said logged-out scraping did not breach Meta's terms (2024-01-23) | Meta dropped the remaining claims in 2024-02 | [TechCrunch, 2024-02-26](https://techcrunch.com/2024/02/26/meta-drops-lawsuit-against-web-scraping-firm-bright-data-that-sold-millions-of-instagram-records), [Frankfurt Kurnit analysis](https://www.fbm.com/data-analytics/publications/major-decision-affects-law-of-scraping-and-online-data-collection-meta-platforms-v-bright-data/) |

### Korea

**Yanolja v Goodchoice (the "Yeogi Eottae" case).** Start with the good news. On 2022-05-12 the Supreme Court of Korea (2021도1533) found the scraper not guilty. That covered intrusion under the Information and Communications Network Act (§48), violation of database-maker rights, and obstruction of business. [Shin & Kim](https://www.shinkim.com/kor/media/newsletter/1843) summarizes the ruling.

Now the turn. The same dispute has a civil track, and it went the other way. On 2021-08-19 the first-instance court ordered damages of 1 billion won. The appeal court also called the crawling unlawful, as [reported on 2022-08-26](https://v.daum.net/v/20220826110606958).

This is the most useful fact in the whole article. A criminal "not guilty" answers one question: did the state have grounds to punish this? A civil ruling answers another: did you wrongfully harm a competitor? Same facts, two questions, two answers (our reading of the two tracks).

The criminal ruling was also tied to its facts. The site had no technical protection on its API, the scraper copied only 3 to 8 items, and the terms were vague. Change those facts and you cannot assume the same result.

**Jobkorea v Saramin.** On 2016-02-17 the Seoul Central District Court (2015가합517982) held that Saramin's mechanical copying of Jobkorea's job listings was unfair competition. It awarded 500,000 won per copied listing ([NEPLA summary](https://www.nepla.ai/wiki/지식재산/부정경쟁/데이터-부정사용-rv5n72p1g8zm)). We could not find a source we could open for later steps in this dispute, so we say nothing about appeals or settlement.

**The statutes behind these cases.** We could not load the article text on law.go.kr with our tools, so the article numbers below come from our research file. Check them before you rely on them.

- Unfair Competition Prevention Act, Article 2(1), item (ka) ([act page](https://www.law.go.kr/법령/부정경쟁방지및영업비밀보호에관한법률/제2조)). It targets data obtained without access rights or by bypassing protection measures. Our research file dates it to 2022-04-20.
- Copyright Act §93 ([article page](https://www.law.go.kr/법령/저작권법/제93조)), database maker's rights. Copying a substantial part, or copying systematically and repeatedly, can infringe. Quoting under §28 works only if your own writing is the main content and you name the source (§37). A review is also a copyrighted work.
- Korea has no text-and-data-mining (TDM) exception as of 2026-10. This comes from our research file. The January 2026 copyright amendment, as [Shin & Kim describes it](https://shinkim.com/kor/media/newsletter/3154), dealt with pirated copies, and that newsletter does not mention TDM.
- Personal Information Protection Act ([Article 15](https://www.law.go.kr/법령/개인정보보호법/제15조)). Usernames and review text can count as personal information. In the AI development and service context, the Personal Information Protection Commission's guide on processing public personal information for AI (2024-07-17) allows processing on a "legitimate interest" basis, with safeguards in place, as [this news report](https://newsseoul.co.kr/news/view/1065606019743236) describes it. That guide is about AI, not about collecting data in general.

Guidance: [pipc.go.kr](https://www.pipc.go.kr).

### United States

**hiQ v LinkedIn.** You may have read that hiQ won. It did win a famous ruling: on 2022-04-18 the Ninth Circuit held that scraping public pages did not break the hacking statute, the CFAA ([Fenwick summary](https://www.fenwick.com/insights/publications/hiq-labs-scrapes-by-again-the-ninth-circuit-reaffirms-that-data-scraping-does-not-violate-the-cfaa-1)). But that was a different question from the contract claim, and the case did not end there.

LinkedIn won on breach of contract. The parties filed the settlement on 2022-12-06 and the court approved it on 2022-12-08, with $500,000 attached ([Proskauer](https://newmedialaw.proskauer.com/2022/12/08/hiq-and-linkedin-reach-proposed-settlement-in-landmark-scraping-case/)). So the final result: the scraper lost on the terms of service.

**Meta v Bright Data.** On 2024-01-23 a federal court in the Northern District of California found that logged-out scraping did not violate Meta's terms. On 2024-02-23 Meta dropped its remaining claims without prejudice and gave up its right to appeal the contract ruling ([TechCrunch](https://techcrunch.com/2024/02/26/meta-drops-lawsuit-against-web-scraping-firm-bright-data-that-sold-millions-of-instagram-records), [analysis](https://www.fbm.com/data-analytics/publications/major-decision-affects-law-of-scraping-and-online-data-collection-meta-platforms-v-bright-data/)). That is a dismissal by the plaintiff, not a settlement as some summaries say. We found no settlement terms, so we do not claim one.

One case with a clear lesson, one with a narrow one. Logged-out versus logged-in matters. Once you accept a site's terms by creating an account, you are in contract territory.

### European Union

Two things matter for a small team.

- **Copyright (DSM Directive 2019/790, Article 4).** Commercial text-and-data mining is allowed, but not if the rights holder opted out in a machine-readable way, such as robots.txt or TDMRep. Text: [EUR-Lex](https://eur-lex.europa.eu/eli/dir/2019/790/oj).
- **GDPR.** A reviewer's name is personal data. Text: [EUR-Lex](https://eur-lex.europa.eu/eli/reg/2016/679/oj).

We leave out GDPR fine amounts and enforcement examples. We did not verify them against primary sources for this article.

### What the map says (my calculation)

Count the outcomes in the table. The scraper won 1 of 1 criminal case. In civil matters, the scraper lost 3 of 4 (hiQ final, Yanolja civil, Jobkorea; Meta v Bright Data went the scraper's way before it was dropped).

Four civil cases is a tiny sample, and we would not stretch it into a statistic. But the direction is clear enough to plan around: prison is a remote risk for most small teams, a lawsuit from the site you scraped is the likelier one.

## Which sources are open and which are closed

We read each policy page directly where our tools allowed. On 2026-10-21 we opened Trustpilot's robots.txt, Product Hunt's API terms, the Hacker News API docs, G2's terms of use, the dev.to API page and dev.to's terms. Reddit, Naver Blog and Naver Cafe are rows from our same-day research check (2026-10-21); our tools could not open their robots.txt files during writing, so those rows rest on that earlier read.

We did not crawl any closed platform for this article. We only read their policy pages.

| Source | What the policy says | Status |
|---|---|---|
| [Reddit](https://www.reddit.com/robots.txt) | robots.txt: `User-agent: *` then `Disallow: /`. Commercial API use needs a separate agreement (not re-opened) | Closed |
| G2 | [Terms of use](https://legal.g2.com/terms-of-use), section 9, forbid you to "access, collect, copy, scrape, harvest" content or data from the site | Closed |
| [Trustpilot](https://www.trustpilot.com/robots.txt) | robots.txt: `User-agent: *` then `Disallow: /` (named search and AI bots get their own rules) | Closed |
| [Product Hunt](https://api.producthunt.com/v2/docs) | API docs: "must not be used for commercial purposes"; contact them for business use | Conditional |
| [Hacker News](https://github.com/HackerNews/API) | Official Firebase API, no key, docs say "There is currently no rate limit" | Open |
| dev.to | The [API page](https://developers.forem.com/api) says many endpoints (not all) need an API key and lists no rate limit or commercial rule. The [terms](https://dev.to/terms) do not mention scraping, but bar commercial use of site "materials" under the download license. We got a 403 when the User-Agent was empty (our own test) | Unclear |
| [Naver Blog](https://blog.naver.com/robots.txt) | robots.txt blocks post paths and says AI training and RAG are banned (not re-opened) | Closed |
| [Naver Cafe](https://cafe.naver.com/robots.txt) | robots.txt: `Disallow: /`, AI training and RAG banned (not re-opened) | Closed |

What this table shows (my calculation): robots.txt or terms stop you first in 5 of 8 cases, long before any court does. Only one source, Hacker News, is both official-API and free of any stated limit. dev.to is the cautionary row: no explicit ban, but also no clear permission.

"Open" is not "unlimited." Hacker News says it has no rate limit today. That is a statement of the present, not a promise, and you should still back off when you see errors.

My opinion: if you are a small team, drop every closed source from your list on day one. Do not spend your scarce hours arguing that the terms are unenforceable. A big company can afford that fight. You cannot.

## The 10-point checklist

This is the list we wrote for our own collector. Each line has a reason.

1. **Keep an allowlist.** Write the terms URL and the date you read it next to every source. Terms change, and a dated record shows good faith.
2. **Obey robots.txt and Crawl-delay.** It is also the opt-out signal the EU copyright exception looks at.
3. **Identify yourself.** Use a clear User-Agent with a contact address. Anonymous crawlers look like attackers.
4. **Use the official API or RSS first.** It is the one route the site has openly offered.
5. **Go slow: at most one request per 5–10 seconds per host, and back off on 429 or 5xx.** That is 360 to 720 requests an hour per host (my calculation), plenty for a small project.
6. **Never log in. Never bypass paywalls or CAPTCHAs. Never rotate proxies.** Accepting terms by logging in, or defeating protection, is exactly where the contract and Korean item (ka) risks begin.
7. **Drop or hash usernames at collection time.** Names are personal data in Korea and the EU. Data you never keep cannot leak.
8. **Keep raw copies internal.** Do not republish the stored pages. Copying a substantial part is the §93 risk.
9. **Publish facts with source and date.** Turn reviews into pro-and-con summaries; quote only briefly and name the source (Korean Copyright Act §28, §37).
10. **Publish a deletion contact and answer within 72 hours.** Keep a fetch log so you can show what you took and when.

Where the numbers come from: items 5 and 10 are our own operating rules, not legal requirements. Nothing in the statutes says "5 seconds" or "72 hours." They are conservative choices.

## What we did with this

We are building a collector that follows these ten rules, and this article is the list we wrote down while doing that. We have not published the product, and this is not a review of other tools.

## FAQ

**Can I collect Reddit posts if they are public?**
Not on our list. Reddit's robots.txt disallows generic crawlers and commercial API use needs a separate agreement (per our 2026-10-21 research read). Public visibility does not change either of those.

**Does a criminal acquittal mean I am safe?**
No. The Yanolja criminal case ended in acquittal while the civil case went against the scraper. Different questions, different answers.

**Can I use the data for AI training in Korea?**
Korea has no TDM exception as of 2026-10, so you cannot lean on one. JoongAng Ilbo [reported on 2025-08-20](https://v.daum.net/v/20250820050157767) that Naver applied code blocking AI crawlers across its services in June and July 2025, and our research read of its robots.txt says AI training and RAG are banned (not re-opened for this article). In the EU, a TDM exception exists but yields to a machine-readable opt-out.

**Is Hacker News really free to use?**
Its official API needs no key and states no rate limit today. Read the terms yourself before building a product on it, and keep your requests polite.

## One more time: this is not legal advice

We are not lawyers, and court outcomes depend on exact facts. If a source is central to your business, pay a lawyer before you scale.

Then do one thing today. Paste the checklist above at the top of your source list, and write the date you last read each source's terms next to it. Re-read them on a schedule.

## Sources and check dates

All checked 2026-10-21 unless stated.

- Supreme Court of Korea, 2022-05-12, 2021도1533 (Yanolja criminal), and first-instance civil ruling, 2021-08-19: [Shin & Kim newsletter](https://www.shinkim.com/kor/media/newsletter/1843); appeal report, 2022-08-26: [Daum](https://v.daum.net/v/20220826110606958)
- Seoul Central District Court, 2016-02-17, 2015가합517982 (Jobkorea v Saramin): [NEPLA wiki summary](https://www.nepla.ai/wiki/지식재산/부정경쟁/데이터-부정사용-rv5n72p1g8zm)
- Korean statutes, article text not readable with our tools; numbers from our research file: [Unfair Competition Prevention Act Art. 2](https://www.law.go.kr/법령/부정경쟁방지및영업비밀보호에관한법률/제2조), [Copyright Act Art. 93](https://www.law.go.kr/법령/저작권법/제93조), [Personal Information Protection Act Art. 15](https://www.law.go.kr/법령/개인정보보호법/제15조). §48 of the Information and Communications Network Act is as summarized by Shin & Kim above.
- Korean 2026-01 copyright amendment: [Shin & Kim](https://shinkim.com/kor/media/newsletter/3154)
- Personal Information Protection Commission, guide on processing public personal information for AI development and services (2024-07-17): [news report](https://newsseoul.co.kr/news/view/1065606019743236); [pipc.go.kr](https://www.pipc.go.kr)
- hiQ Labs v. LinkedIn, Ninth Circuit, 2022-04-18: [Fenwick](https://www.fenwick.com/insights/publications/hiq-labs-scrapes-by-again-the-ninth-circuit-reaffirms-that-data-scraping-does-not-violate-the-cfaa-1); N.D. Cal. consent judgment 2022-12-08: [Proskauer](https://newmedialaw.proskauer.com/2022/12/08/hiq-and-linkedin-reach-proposed-settlement-in-landmark-scraping-case/)
- Meta Platforms v. Bright Data, N.D. Cal., ruling 2024-01-23, claims dropped 2024-02-23: [TechCrunch, 2024-02-26](https://techcrunch.com/2024/02/26/meta-drops-lawsuit-against-web-scraping-firm-bright-data-that-sold-millions-of-instagram-records); [Frankfurt Kurnit](https://www.fbm.com/data-analytics/publications/major-decision-affects-law-of-scraping-and-online-data-collection-meta-platforms-v-bright-data/)
- EU Directive 2019/790, Art. 4: [EUR-Lex](https://eur-lex.europa.eu/eli/dir/2019/790/oj); GDPR: [EUR-Lex](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [Trustpilot robots.txt](https://www.trustpilot.com/robots.txt), [Product Hunt API docs](https://api.producthunt.com/v2/docs), [Hacker News API](https://github.com/HackerNews/API), [dev.to / Forem API](https://developers.forem.com/api), [dev.to terms](https://dev.to/terms), [G2 terms of use](https://legal.g2.com/terms-of-use)
- Naver AI-crawler blocking report, JoongAng Ilbo via Daum, 2025-08-20: [link](https://v.daum.net/v/20250820050157767)
- Reddit robots.txt and Data API terms, Naver Blog and Naver Cafe robots.txt: read by our team on 2026-10-21; links above are to the files, not re-opened during writing.
