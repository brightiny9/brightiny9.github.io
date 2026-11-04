---
layout: post
title: "Postman and AI plugins: what two bug reports show, and how to check your own machine"
lang: en
ref: postman-ai-plugins-issue
date: 2026-11-04
permalink: /en/postman-ai-plugins-issue/
---

**Did Postman install plugins into my Claude Code and Codex?** Two users say yes, in the same GitHub issue on Postman's app repo. We did not run Postman ourselves, so this is what their logs show, not a test of ours. Published 2026-11-04, based on the issue as we read it that day.

## What the reports say

The first report was opened on 2026-10-25. The reporter's log is from 2026-10-24 and shows Postman desktop 12.33.4 running an "auto-existing-upgrade" step (the app's own name for upgrading a machine that already has Postman). The next line says "claude-code:installed,codex:installed" ([issue #14370](https://github.com/postmanlabs/postman-app-support/issues/14370)).

The reporter lists what they found afterwards:

- A Codex plugin (v1.1.0), a Claude Code plugin (v2.0.1) and the Postman CLI in `~/.local/bin`.
- Postman marketplace entries in `~/.codex/config.toml`, and the Postman plugin marked "enabled" in `~/.claude/settings.json`.
- A Codex start-up file that tells the agent to treat Postman as the default for non-trivial API work. (We only saw this file described for Codex, not for Claude Code.)
- A remote tool connection (MCP) to `https://mcp.postman.com/mcp` that asked for login and failed.

A second user added a log from 2026-11-03 (22:58 UTC) that shows the same "auto-existing-upgrade" step. In a comment, they say it happened while updating from 12.31.3 to 12.35.1.

## What we can and cannot say

| Question | Our read |
|---|---|
| Does the same install path show up on two builds? | Yes, in two separate users' reports (12.33.4, and an update to 12.35.1). |
| Does the issue show data being sent out? | No. The reporter says the report does not claim to show data theft. They say the installer *attempts* to approve its own hooks, and that a trust record alone does not prove who made it. |
| Is this confirmed by Postman? | Partly. See below. |

## What Postman replied

A commenter (account zecoquit; we could not confirm they work at Postman) answered on the issue. The reply is dated 2026-11-04 08:36 in GMT+9, which is 2026-11-03 23:36 UTC ([comment](https://github.com/postmanlabs/postman-app-support/issues/14370#issuecomment-6618267843)). It says: "we bundle the Postman CLI and the agent plugins with the desktop app because many users had trouble installing and wiring them up separately."

The same reply says opt-in will be made clearer for existing users, that hook approval and session-start behavior are under review, that the parts can be removed inside the app, and that "We'll post an update in this thread as changes land." When we checked on 2026-11-04 (afternoon, Korea time), no fixed version was listed.

## How to check your own machine

1. Open `~/.claude/settings.json` and `~/.codex/config.toml`. Look for Postman entries you did not add. Back up each file first.
2. Look for Postman files in `~/.local/bin`.
3. Postman's docs describe a status command, `npx @postman/postman-plugin status`, and a `remove` command with a `--dry-run` option ([docs](https://learning.postman.com/docs/postman-plugin/install/detected-agents)). Run `status` first. Use `--dry-run` before you remove anything.

Those paths and commands come from the report and Postman's docs. Your setup may differ.

## Our opinion

A start-up hook is a small command your agent runs each time a session begins. Any desktop app that can write to your agent's settings can change what that agent does. For Codex, Postman's docs say: "The installer approves the hook for you." We think a short look at those two settings files, every month or so, is cheap. Treat it like checking your shell config.

## Sources (read 2026-11-04)

- [postman-app-support issue #14370](https://github.com/postmanlabs/postman-app-support/issues/14370)
- [Postman reply in the issue](https://github.com/postmanlabs/postman-app-support/issues/14370#issuecomment-6618267843)
- [Postman docs: install the plugin into detected agents](https://learning.postman.com/docs/postman-plugin/install/detected-agents)
