---
description: Make a narrated video of a web page with PageToVid
argument-hint: <url> [goal, length, aspect, language, anything to say word for word]
---

## What this is

PageToVid is connected as the MCP server "pagetovid" (https://pagetovid.com/mcp). The first call opens a sign-in in the browser: run `/mcp` and authenticate "pagetovid" if a tool answers "not authorised". Free tools spend nothing; a tool marked [40 credits] spends credits and has a free preview (dry_run, or confirm=false) — quote the cost and never confirm a spend on the person's behalf. The tool descriptions are the reference: read them before calling.

The person asked for: **$ARGUMENTS**

## Do this

1. `get_account`: plan, credits, watermark. Say what a film costs on this plan.
2. `inspect_page` the URL in the aspect ratio the person wants (16:9 by default; 9:16 films the page's mobile layout). If the page is behind a login or a robot check, say so and suggest a public page that shows the product instead.
3. Write the brief for `create_video`: the goal, the length, the facts and the offer in `focus`, one idea per scene, and any line that must be said word for word in quotation marks. Show it to the person with the cost (`dry_run: true` quotes it free).
4. On their go, call `create_video`. Poll `get_video` every `poll_after_seconds` until the status is done, held or error.
5. Report the video link, its length, and every item in `warnings`. Offer `/pagetovid:edit` if anything should change.
