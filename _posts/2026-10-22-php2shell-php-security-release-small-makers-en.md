---
layout: post
title: "PHP2Shell: Is Your Site Affected? Versions, Who Patches, and What to Do Today"
lang: en
ref: php2shell-php-security-release-small-makers
date: 2026-10-22
permalink: /en/php2shell-php-security-release-small-makers/
---

PHP shipped security releases on Oct 21, 2026: 8.5.12, 8.4.27, 8.3.36 and 8.2.35. They fix two critical bugs that can allow remote code execution without logging in ([PHP Foundation](https://thephp.foundation/blog/2026/10/21/todays-php-security-release-and-how-were-strengthening-php-security/), checked Oct 22, 2026). Whether your site needs action today depends on two things: who runs your PHP, and which version it runs. This post also checks a few popular claims against official sources.

> **Verdict:** If you run your own PHP, update to a fixed version and restart. If a managed host runs it, read that host's notice. PHP 8.1 and older get no official release, so plan a move to a supported branch. Attacks have already been reported, so do not wait for the weekend.
{: .v-verdict}

{% include stat.html value="4 versions" label="Fixed releases: 8.5.12, 8.4.27, 8.3.36, 8.2.35" source="PHP Foundation announcement, thephp.foundation" date="Oct 22, 2026" %}

## Short answer

- Self-managed PHP (VPS, your own Docker image, your own server): you must update.
- Managed hosts: five Automattic-run platforms say they already protected you. For any other host, read that host's own notice.
- PHP 8.1 or older: the PHP project issues no updates for these branches. Move to a supported branch.
- Is anyone attacking? Yes. Amazon says its MadPot honeypot sensors saw an attempt dating to Oct. 17, four days before public disclosure, and that the bug is now "being broadly exploited in the wild" ([Amazon Threat Intelligence](https://aws.amazon.com/blogs/security/amazon-threat-intelligence-identifies-php2shell-exploitation-prior-to-public-disclosure-in-madpot/), published Oct 21, checked Oct 22, 2026). Cloudflare also says it saw attack traffic after the leak ([Cloudflare](https://blog.cloudflare.com/php-vulnerabilities-waf-protection/), Oct 22, 2026). Details are in the exploitation section below.

The "70% of the internet" line is about how many websites use PHP. It is not the share of sites that are vulnerable. Cloudflare says PHP is used by ["almost 70% of websites"](https://blog.cloudflare.com/php-vulnerabilities-waf-protection/) (Oct 22, 2026).

## Affected range vs. fix range

These are two different questions, and mixing them up causes most of the confusion in the write-ups.

- Affected range: how far back the flawed code goes. Cloudflare says "all web servers running PHP 5.4 or later." Wiz, the firm that reported the bugs, says every PHP version of the last decade is affected by at least one bug, "going back to version 5.4" ([Wiz](https://www.wiz.io/blog/php2shell-php-rce), Oct 22, 2026). Note that Wiz counts four bug instances grouped under the two CVEs, so that range covers all four, not one CVE alone. Automattic says the same ([Automattic](https://automattic.com/2026/10/21/your-sites-are-protected-against-the-php2shell-vulnerabilities/), Oct 22, 2026). Tenable cites a technical write-up by Calif for the earliest affected code path, PHP 5.4.0 ([Tenable](https://www.tenable.com/blog/php2shell-cve-2026-109618-cve-2026-109619-frequently-asked-questions-about-critical-php-remote), Oct 22, 2026).
- Fix range: which branches get a release. Only the four supported ones. The PHP announcement says: "PHP 8.1 and older no longer receive updates from the PHP project. Some distributions and LTS vendors provide backported fixes, so contact your vendor for details, or upgrade to a supported version" ([php.net](https://www.php.net/archive/2026.php), Oct 22, 2026).

Put together:

| Your branch | Affected? | Official fix | Support status |
|---|---|---|---|
| 8.5 | Yes, below 8.5.12 | 8.5.12 | Security support until Dec 31, 2029 |
| 8.4 | Yes, below 8.4.27 | 8.4.27 | Security support until Dec 31, 2028 |
| 8.3 | Yes, below 8.3.36 | 8.3.36 | Security support until Dec 31, 2027 |
| 8.2 | Yes, below 8.2.35 | 8.2.35 | Security support ends Dec 31, 2026 |
| 7.4, 8.0, 8.1 | Per Tenable, minimal source backports exist. Our reading: affected | No release. Minimal source backports only | End of life |
| 5.4 to 7.3 | Yes, per Tenable | None from the PHP project | End of life |

Sources: [php.net archive](https://www.php.net/archive/2026.php), [php.net supported versions](https://www.php.net/supported-versions.php), [Tenable](https://www.tenable.com/blog/php2shell-cve-2026-109618-cve-2026-109619-frequently-asked-questions-about-critical-php-remote), all checked Oct 22, 2026. The "Affected?" cell for 7.4 to 8.1 is our reading: the PHP security team would not backport a fix to branches that were not affected. Tenable says 7.4.x through 8.1.x get minimal source backports, and that 5.4 through 7.3 are end of life with no fix.

Is 5.4 really the floor? It is the floor that Wiz, Cloudflare and Tenable (citing Calif) give. Alexandre Daubois, a member of the PHP security team, writes that "the mechanism goes back further than the rumor, since the same jump sits in the PHP-5.3 allocator." He adds that he has not seen an exploit shown on those old versions either ([Daubois](https://daubois.dev/blog/cve-2026-109618-php2shell-rumors/), posted Oct 21, checked Oct 22, 2026). So the honest summary is: 5.4 is the commonly cited lower bound, older code may share the mechanism, and nobody has shown a working attack on it.

The safe rule: if you run any PHP version below the fixed numbers, treat yourself as exposed until a primary source says otherwise.

Note on 8.2. It has a fix today, but support ends in about two months. Automattic says ["8.3 or newer is the better target"](https://automattic.com/2026/10/21/your-sites-are-protected-against-the-php2shell-vulnerabilities/). We agree: if you are touching the server anyway, jump past 8.2.

{% include stat.html value="Dec 31, 2026" label="PHP 8.2 security support ends" source="php.net supported versions" date="Oct 22, 2026" %}

## Claims you may see, checked against official text

These are claims that float around social posts and summaries. They are not tied to one source, so treat the left column as our wording. Each one sits next to the official text.

| Claim to check | What sources say | Verdict |
|---|---|---|
| The bug is hidden in 70% of the internet | PHP is used by almost 70% of websites (Cloudflare). Not the share that is vulnerable. | Wording misleads |
| It takes over a server without login | Foundation: on Apache with mod_php, "an unauthenticated request can trigger this before any application code runs." | Largely right for mod_php. Takeover depends on setup. |
| The code is a specific number of years old (for example 14) | "Affected releases go back more than a decade, to PHP 5.4" ([Automattic](https://automattic.com/2026/10/21/your-sites-are-protected-against-the-php2shell-vulnerabilities/)) | "Over a decade" confirmed. An exact age is not |
| Memory fills up, cleanup is skipped | Foundation: at the wrong moment of hitting memory_limit, PHP "could leave partially initialized internal data behind" | Right in spirit |
| Only version 8.1.1 or below needs a version jump | The whole 8.1 branch is end of life ([php.net](https://www.php.net/archive/2026.php)) | Wrong. The whole branch is out |
| Attacks started before the patch | Amazon's MadPot sensors saw an attempt dating to Oct. 17, four days before disclosure. Cloudflare says it saw attack traffic after the leak, and shipped WAF rules about 9 hours ahead of public disclosure. | Confirmed by Amazon. Cloudflare does not state the hour of its traffic |
| A government took a service offline over it | We found no official source | Not confirmed. Treat as rumor |

The leak itself is on record. The PHP Foundation says the two CVE IDs began circulating on Oct 20, around 15:00 UTC, with a wrong release time and a wrong score ([Foundation](https://thephp.foundation/blog/2026/10/21/todays-php-security-release-and-how-were-strengthening-php-security/), Oct 22, 2026).

## Is it being exploited?

Three kinds of evidence, all from first-hand observers:

| Claim | Who says it | How close to the source |
|---|---|---|
| An exploitation attempt dating to Oct. 17 in MadPot telemetry, four days before public disclosure. Now "being broadly exploited in the wild," with several PoCs and attempts seen "almost immediately" after the Oct 21 14:00 UTC embargo lift | Amazon Threat Intelligence, "[Amazon Threat Intelligence identifies PHP2Shell exploitation prior to public disclosure in MadPot](https://aws.amazon.com/blogs/security/amazon-threat-intelligence-identifies-php2shell-exploitation-prior-to-public-disclosure-in-madpot/)" (Oct 21, checked Oct 22, 2026) | First-hand, from its own honeypot sensors |
| Attack traffic targeting customers after the leak. Cloudflare says the bug "was leaked before the official release date and we observed attack traffic targeting our customers." It does not state the hour. | Cloudflare, in its own post ([Cloudflare](https://blog.cloudflare.com/php-vulnerabilities-waf-protection/), Oct 22, 2026) | First-hand |
| Exploitation seen on watchTowr's honeypot network as of Oct 21 | watchTowr FAQ, "through watchTowr's Attacker Eye global honeypot network" ([watchTowr](https://watchtowr.com/intelligence/php-cve-2026-109618-faq/), Oct 22, 2026) | First-hand, from a security vendor |

The Foundation says something that looks different but is about a different moment. Its security team "closely monitored and inspected appearing PoCs after the leak but did not identify any functional exploits at the time of release/public disclosure." Amazon describes several PoCs appearing after the embargo lifted. So the two do not conflict: the Foundation describes the moment of release, and Amazon describes what came right after. The Foundation also describes full remote code execution for CVE-2026-109618 as demonstrated, and says the reporter demonstrated CVE-2026-109619 ([Foundation](https://thephp.foundation/blog/2026/10/21/todays-php-security-release-and-how-were-strengthening-php-security/), Oct 22, 2026).

Our reading: a bug that leaked about a day early, was probed on a honeypot four days before disclosure, and is now reported as broadly exploited is a bad candidate for "I'll patch next week."

## Which server setups are in scope?

The PHP announcement is blunt: "all PHP installations serving web requests, including PHP-FPM, Apache with mod_php, php-cgi, FrankenPHP and LiteSpeed. We consider the risk highest for mod_php" ([php.net](https://www.php.net/archive/2026.php), Oct 22, 2026). The Foundation names two bugs, and the split matters:

| CVE | What Foundation describes |
|---|---|
| CVE-2026-109618 | Apache with mod_php: an unauthenticated request can trigger it before any application code runs. Also confirmed on PHP-FPM "through application-level code paths." |
| CVE-2026-109619 | Remote code execution against a real application on Apache with mod_php, demonstrated by the reporter. |

The PHP announcement gives one CVSS v4.0 score, 9.2, for the two critical bugs. Some people posted 10.0. The Foundation says the early CVE records "came with a wrong release time and a wrong CVSS score of 10.0 (the actual score is 9.2)." Daubois traces the 10.0 number to a post by Florian Roth (as relayed by Phoenix Security) and to Cyber Daily's report of watchTowr ([Daubois](https://daubois.dev/blog/cve-2026-109618-php2shell-rumors/), Oct 22, 2026).

{% include stat.html value="9.2" label="Official CVSS v4.0 score. The 10.0 that circulated was wrong" source="PHP announcement, php.net, and PHP Foundation" date="Oct 22, 2026" %}

If you do not know which setup you run, assume you are in scope. Do not read "mod_php is highest risk" as "FPM is safe."

## Who patches your PHP?

This table is our reading of the sources, not an official list.

| Where your site runs | Who updates PHP | What you do |
|---|---|---|
| WordPress.com, WordPress VIP, WP Cloud, Pressable, Tumblr | The platform. Automattic says these are "already protected." | Nothing, per Automattic. |
| Other managed WordPress host | Unknown. Read your host's notice. | Look for a security notice. If none, ask support. |
| Shared hosting | Usually the host, but you may choose the PHP version in a control panel | Check the version, then ask the host if it is fixed |
| VPS or your own server | You | Update the PHP package, restart |
| Docker | You | Update the base image, rebuild, redeploy |

For the first row, the source is [Automattic](https://automattic.com/2026/10/21/your-sites-are-protected-against-the-php2shell-vulnerabilities/) (Oct 22, 2026). The other rows are our reasoning. We did not verify any other host's response.

One pattern stands out. The people most at risk are probably not on the big managed platforms. They are on a cheap VPS or a Docker image built once and forgotten, because nobody pushes updates to them. That is our inference, not a measured number.

## Check your version

- Command line: run `php -v`. Careful: the command line PHP can differ from the PHP your web server uses. Check both if you can.
- WordPress: go to Tools > Site Health > Info > Server. The [WordPress docs](https://wordpress.org/documentation/article/site-health-screen/) (updated July 12, 2026) say this section lists your server and PHP setup. The Status tab also warns when PHP is outdated. If you cannot find a PHP version line, ask your host.
- Container: check the image tag in your Dockerfile, then confirm inside the running container.
- Linux distribution packages: distributions may backport the fix without changing the PHP version number. The PHP announcement says to contact your vendor. In that case compare the CVE numbers in your distribution's security notice, not the version string.

For upstream builds, match the number against the table. 8.3.35 is not fixed. 8.3.36 is.

## Running 8.1 or older?

An update will not come from the PHP project, so the answer is migration. The project did publish minimal source backports for 7.4, 8.0 and 8.1, meant for people who build from source or lack an LTS vendor ([php.net](https://www.php.net/archive/2026.php), Oct 22, 2026).

Our take: for a small team, building PHP from source is a heavy plan. Moving to 8.3 or newer is usually less work than it sounds, and it ends the problem for the next several years instead of this week. If you buy LTS support from a vendor, ask them in writing whether they ship these CVE fixes.

## Today's checklist

1. **Check.** Run `php -v`, or look in Site Health. Write down the number.
2. **Patch.** Move to 8.5.12, 8.4.27, 8.3.36 or 8.2.35 (or newer). On managed hosting, confirm the host did it.
3. **Restart.** Restart PHP-FPM, Apache or your containers. The old process keeps running until you do.
4. **Verify.** Check `php -v` again, in the web context too.
5. **Add a firewall layer.** Cloudflare says free and paid WAF customers have been protected by default since Oct 21, 3:02 am UTC. It also says to patch anyway: the WAF is "defense-in-depth" ([Cloudflare](https://blog.cloudflare.com/php-vulnerabilities-waf-protection/), Oct 22, 2026).

About rumor fixes. The setting `session.upload_progress.enabled = Off` was the most repeated advice. It applies only to the second bug, not the first ([Daubois](https://daubois.dev/blog/cve-2026-109618-php2shell-rumors/)). It is not a substitute for patching.

Daubois also relays the advisory's own stopgaps. He writes that the first one it lists, enforcing `memory_limit=-1` and never `RLIMIT_AS`, "appeared in none of the write-ups I read, and it looks like the opposite of hardening until you see the bug underneath." For apps that take no uploads, he says the advisory recommends blocking multipart/form-data at the web server. Read his post for the reasoning before you touch any setting. These are stopgaps until you patch, not replacements for patching.

## Sources and what we couldn't verify

All checked Oct 22, 2026.

- [PHP Foundation announcement](https://thephp.foundation/blog/2026/10/21/todays-php-security-release-and-how-were-strengthening-php-security/): versions, CVE IDs, setups, leak timing, the wrong 10.0 score, the monitoring and demonstration statements
- [php.net 2026 news archive](https://www.php.net/archive/2026.php): release dates, CVSS v4.0 9.2, all-SAPI risk statement, 8.1 and older backports
- [php.net supported versions](https://www.php.net/supported-versions.php): EOL dates
- [Amazon Threat Intelligence](https://aws.amazon.com/blogs/security/amazon-threat-intelligence-identifies-php2shell-exploitation-prior-to-public-disclosure-in-madpot/): the Oct. 17 MadPot observation, "broadly exploited" statement, PoCs after the embargo lift
- [Automattic](https://automattic.com/2026/10/21/your-sites-are-protected-against-the-php2shell-vulnerabilities/): managed hosts, "more than a decade" range, EOL advice
- [Cloudflare](https://blog.cloudflare.com/php-vulnerabilities-waf-protection/): 70% figure, attack traffic after the leak, WAF coverage
- [Wiz](https://www.wiz.io/blog/php2shell-php-rce): reporter's view on the 5.4 range, four bug instances
- [Tenable FAQ](https://www.tenable.com/blog/php2shell-cve-2026-109618-cve-2026-109619-frequently-asked-questions-about-critical-php-remote): earliest affected code path, EOL branches
- [watchTowr FAQ](https://watchtowr.com/intelligence/php-cve-2026-109618-faq/): honeypot exploitation as of Oct 21
- [Daubois, PHP security team](https://daubois.dev/blog/cve-2026-109618-php2shell-rumors/): the 5.3 allocator remark, the 10.0 attribution, the session setting, the advisory's stopgaps
- [WordPress Site Health docs](https://wordpress.org/documentation/article/site-health-screen/)

Not verified: the NVD records (page returned no data), any host other than the five Automattic names, an exact "age of the bug" figure, the hour of Cloudflare's observed traffic, and the claim that a government took a service offline. We left out exploit details on purpose. This post is for defense. If official guidance changes, we will update it and say so here.

Patch PHP. Restart. Verify.
