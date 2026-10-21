---
description: Plan and make how-to videos for this product's documentation
argument-hint: [a feature, a doc page, or "all"]
---

## What this is

PageToVid is connected as the MCP server "pagetovid" (https://pagetovid.com/mcp). The first call opens a sign-in in the browser: run `/mcp` and authenticate "pagetovid" if a tool answers "not authorised". Free tools spend nothing; a tool marked [40 credits] spends credits and has a free preview (dry_run, or confirm=false) — quote the cost and never confirm a spend on the person's behalf. The tool descriptions are the reference: read them before calling.

How-to videos: one short film per task a user must learn, filmed on the real product, narrated and captioned. The person asked for: **$ARGUMENTS**

## Do this

1. Read this repository's docs (docs/, a /docs route, README sections) and its routes. List the 3–8 tasks a new user must learn, each with the public page where it happens.
2. `inspect_page` each page in 16:9. Prefer pages whose ranked subjects are the product itself (a form, a table, a listing) over a marketing hero.
3. Write each brief for `create_video`: goal `tutorial`, 45–75 s, the task in the first sentence, the exact steps as facts.
4. Present the plan as a table (task · page · length · cost) and ask before every `create_video`. Never start more renders than the person approved.
