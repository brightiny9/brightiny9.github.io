---
layout: post
title: "Mem is shutting down: how do I export my notes? (read-only Dec 18, shutdown Jan 15)"
lang: en
ref: mem-shutdown-export-notes
date: 2026-11-18
permalink: /en/mem-shutdown-export-notes/
---

If you use Mem, your notes become read-only on December 18, 2026, and you should have your copy saved before January 15, 2027. Mem's own announcement says notes become read-only on December 18 and the service shuts down on January 15. The export is one ZIP file with one Markdown file per note, started from Settings, then Exports (steps below). The part that is easy to get wrong is what to do with the ZIP afterward. This guide covers both.

Sources checked on 2026-11-18: [Mem's announcement (2026-11-16)](https://get.mem.ai/blog/mem-is-shutting-down), [Mem's migration page](https://help.mem.ai/migration), [Save a copy](https://help.mem.ai/migration/save-a-copy.md), [Check your move](https://help.mem.ai/migration/check-your-move.md), [Move to Obsidian](https://help.mem.ai/migration/obsidian.md).

## The dates, in days

Mem posted the news on November 16. We counted the gaps ourselves from the dates in the announcement:

- Announcement (Nov 16) to read-only (Dec 18): 32 days.
- Read-only (Dec 18) to shutdown (Jan 15, 2027): 28 days.
- Announcement to shutdown: 60 days.
- As of Nov 18, 2026, to read-only: 30 days.

Mem also says "You won't be charged again. All charging has been paused," and that paid features stay available through the shutdown date. So there is no billing pressure. The only clock is the export.

## Export steps (from Mem's guide)

1. Open Settings, then Exports, in Mem on your computer.
2. Click "Start new export" and choose "My Computer", then Next.
3. Review the options and click "Start export".
4. Come back to Exports when it is ready and download the ZIP.
5. Unzip it (double-click on Mac, right-click and Extract All on Windows).
6. Keep both the original ZIP and the unzipped folder until you have checked the move.

One rule from the [same guide](https://help.mem.ai/migration/save-a-copy.md): if another export is already preparing, let it finish before you start a new one.

## What is inside the ZIP

According to Mem's guide, the ZIP has these parts:

| Folder or file | What it holds |
|---|---|
| notes/ | One Markdown (.md) file per exported note |
| collections/ | An index for each collection, with links to its notes |
| attachments/ | The files your notes point to, where available |
| export-report.md | A list of items Mem could not include, if there are any |

Meeting transcripts are included by default where they exist. Audio recordings are optional, and Mem says audio can make the download much larger. Mem also warns that a written meeting note, a transcript, and a recording are three separate things. Keeping one does not mean you have the other two.

## Moving to Obsidian (the one path we read in full)

Mem's Obsidian guide says both "Obsidian" and "My Computer" in the destination picker give you Markdown files. Then:

1. Open Obsidian's vault switcher and pick Open folder as vault.
2. Select the folder that contains notes/, collections/, and your attachments.
3. Open a note you know well, then open one file in collections/ and follow a link.

The easy mistake is choosing only notes/. Mem's guide says that leaves the other files outside your vault, and it tells you to keep the folders together while you check images and links. Select the parent folder. (Our inference: a vault without attachments/ would show broken images.)

Mem also has guides for Apple Notes, Notion, Google Docs or Drive, Microsoft OneNote, and Bear or Evernote, plus a short list of other apps. We did not read those in full, so check the one for your app on the [migration page](https://help.mem.ai/migration).

## What to check after the move

Mem's own checklist is short:

- Collections: a note that belonged to two collections may show up in both indexes, pointing at the same file.
- Files: open a photo or PDF from inside a note. If the link fails, find the file in the unzipped folder. Moving only the note can break the link to its attachment.
- Meetings: find a meeting by title, open its transcript, and play the audio if you included recordings.
- Missing items: Mem's troubleshooting section says to open export-report.md if you find something missing. It lists what Mem could not include. Our suggestion: read it right after the first export, not only when something looks wrong.

## Our read: export twice

This part is our reasoning, not Mem's advice. Mem's [migration page](https://help.mem.ai/migration) says to export again if you edit notes after your first copy. Notes become read-only on December 18, so no edits can happen after that day. That gives a simple plan:

1. Export now. This is your safety copy, and it also tells you early whether export-report.md lists anything you care about.
2. Export once more after December 18. Nothing can change after that, so this copy is final. You still have 28 days before shutdown to fix a bad export.

If you do not edit your notes between now and December 18, the second export will be identical, and that is fine. One more thing worth doing: put the ZIP somewhere other than the laptop you export from.

## What we could not confirm

Mem's pages do not say how large an export can get, how long a big library takes to prepare, or how note properties and tags come out in each destination. If your library is large, start the export early and keep the first ZIP until the second one checks out. We have not run the export ourselves. Everything above comes from Mem's published pages on the date shown.
