---
layout: post
title: "Does Claude Code send your email address to websites? What the issue shows so far"
lang: en
ref: claude-code-email-issue
date: 2026-11-06
permalink: /en/claude-code-email-issue/
---

Short answer: in the scenario a commenter describes, yes, Claude can put your account email in a request header. That commenter, marked Contributor, says it was not a designed feature, and a built-in check now blocks one specific shape of it. Whether the reporter's own case was that scenario, and whether it caused their spam, is unconfirmed.

Published 2026-11-06. Checked that day against the issue and the public source.

## What was reported

On 2026-11-05, a user opened [issue 107757](https://github.com/anthropics/claude-code/issues/107757). They say Claude Code put their email in the `User-Agent` header while searching the web, and that they now get dozens of scam emails a day. They name version 2.1.318 on macOS. All of this is their own account. The issue gives no request log, and nobody in the thread has reproduced the spam link.

## What the Contributor-labeled commenter says

A commenter writing as "we" (GitHub marks them Contributor; I found no direct proof of who employs them) gave this chain in [two comments](https://github.com/anthropics/claude-code/issues/107757#issuecomment-6672259159) ([second one](https://github.com/anthropics/claude-code/issues/107757#issuecomment-6672827267)): some sites, Wikipedia as the example, ask scripted clients to put a contact email in the User-Agent. A user asks Claude to research on such a site. Claude then puts the user's email in its `curl` call. They say nobody built this as a feature, and that a built-in mod, `cc-plugin-privacy`, blocks it from v2.1.317 on and is on by default.

That is an explanation from one commenter, not a post-mortem. I could not find an official statement outside the thread.

## What the check does, from its own README

The [mod's README](https://github.com/anthropics/claude-code/blob/main/mods/privacy/README.md) is plain about it: "a courtesy, not a boundary." It refuses a Bash, PowerShell or Monitor call when the call contains your account email and also names a User-Agent. Two word matches, no parser.

| Checked | Not checked (per the same README) |
|---|---|
| Bash, PowerShell, Monitor calls that hold your email and name a User-Agent (`curl -A`, `wget -U`, `--user-agent`) | Your email in a URL, request body, `curl -u`, or a `From:` header |
| | WebFetch, WebSearch, and MCP tool calls |
| | Values computed at run time, such as `$(git config user.email)`, or held in a variable or file |
| | Clients the check does not name, a header set another way, and addresses with other encodings or non-ASCII characters (the README lists more) |

The README also says an installed plugin's `tool.check` hook can overrule the refusal, and that repository settings cannot turn the mod off.

One mismatch to watch: the [changelog](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md), under 2.1.317, says the check "asks before" a call sends the email. The README says the refusal "raises no prompt." I could not tell which describes what you will see. Also, [one commenter](https://github.com/anthropics/claude-code/issues/107757#issuecomment-6673441086) on 2.1.318 says the mod does not show up in `/plugins`. Nobody answered that in the thread I read.

## My take

The fix is real but small. It blocks the Bash `curl` shape that the Contributor-labeled commenter describes. The reporter only wrote "while conducting web searches," and the README says WebSearch and WebFetch are not checked, so the issue does not show which path their case took. It does not guarantee the email never leaves: by the README's own list, a different request shape gets through.

## A checklist you can run today

1. Open the plugin list (the README writes `/plugin`, a commenter wrote `/plugins`) and look for `cc-plugin-privacy`. If you do not see it, I would not assume the check is active.
2. Check `enabledPlugins` in your user and managed settings for `"cc-plugin-privacy@builtin": false`.
3. Look at which email your account uses. My opinion: if it is your main personal address, a separate address for agent work is cheap insurance.
4. Add a standing rule to your CLAUDE.md. [One commenter shared one](https://github.com/anthropics/claude-code/issues/107757#issuecomment-6673214275) that allows the email only for approved sites and asks first otherwise. It is a prompt, not a guarantee.
5. To see whether a `curl` call already carried your email, scan the Bash commands Claude ran in your terminal scrollback or your shell history, if you keep them, for your address next to `User-Agent`, `-A` or `-U`. A clean search does not prove nothing was sent through the unchecked paths above. I did not verify where Claude Code stores session transcripts, so I leave that out.

## Still unknown

- Whether the reporter's spam came from this header at all.
- How many users were affected.
- Which versions did it, and since when.
- Whether the mod appears on every 2.1.317 and later install.
- Whether earlier reports of the same behavior exist. I did not search the tracker for them.
- Which tool path the reporter's case used (Bash `curl`, WebSearch, or something else).

I will update this post if the thread or the changelog answers any of these.

Change log: 2026-11-06, first version.

Sources, all checked 2026-11-06:
- [Issue 107757](https://github.com/anthropics/claude-code/issues/107757)
- [Privacy mod README](https://github.com/anthropics/claude-code/blob/main/mods/privacy/README.md)
- [Claude Code CHANGELOG](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md)
