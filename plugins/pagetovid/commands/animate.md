---
description: Turn your own content (numbers, notes, a story, a deck) into an animated PageToVid video
argument-hint: <what the video is about, or paste the content>
---

## What this is

PageToVid is connected as the MCP server "pagetovid" (https://pagetovid.com/mcp). The first call opens a sign-in in the browser: run `/mcp` and authenticate "pagetovid" if a tool answers "not authorised". Free tools spend nothing; a tool marked [40 credits] spends credits and has a free preview (dry_run, or confirm=false) — quote the cost and never confirm a spend on the person's behalf. The tool descriptions are the reference: read them before calling.

The person asked for: **$ARGUMENTS**

## Do this

1. `list_motions` to see the 26 visuals (statement, chart, timeline, grid, pricing, quote, message thread…) and the transitions. A deck or a file the person has goes through `create_upload` first: its slides come back as text and pictures, one slide per scene.
2. Write the storyboard for `create_animation`: one idea per scene, narration words set the length (about 149 words a minute at the default tone), every figure exactly as the person gave it. Never invent a number, a quote or a testimonial.
3. Show the scenes as a table (visual · narration · on-screen text) and the cost (`dry_run: true`). On their go, call `create_animation` and poll `get_video` until it ends.
4. Report the link, the length and the warnings.
