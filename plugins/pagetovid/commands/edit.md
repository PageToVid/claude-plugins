---
description: Edit a PageToVid video's storyboard, re-render it, or translate it
argument-hint: [video id or "last"] <what to change>
---

## What this is

PageToVid is connected as the MCP server "pagetovid" (https://pagetovid.com/mcp). The first call opens a sign-in in the browser: run `/mcp` and authenticate "pagetovid" if a tool answers "not authorised". Free tools spend nothing; a tool marked [40 credits] spends credits and has a free preview (dry_run, or confirm=false) — quote the cost and never confirm a spend on the person's behalf. The tool descriptions are the reference: read them before calling.

The person asked for: **$ARGUMENTS**

## Do this

1. Find the video: the id given, or `list_videos` (newest first) for "last".
2. `get_storyboard` and show the scenes briefly. Make the change with `update_storyboard` (words, captions, visuals, shots, transitions, voice, music, look) — every edit is snapshotted and `restore_revision` undoes it.
3. `quote_cost` the next `rerender_video`, say the price (a caption-only fix is free once per paid render), and re-render on the person's go. For another language, `translate_video` makes a new video per language.
4. Poll `get_video` and report the new link and its warnings.
