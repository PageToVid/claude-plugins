---
description: Create a recurring PageToVid show (one video per new item of a feed)
argument-hint: [site] [what should recur, e.g. "weekly changelog" or "each blog post"]
---

## What this is

PageToVid is connected as the MCP server "pagetovid" (https://pagetovid.com/mcp). The first call opens a sign-in in the browser: run `/mcp` and authenticate "pagetovid" if a tool answers "not authorised". Free tools spend nothing; a tool marked [40 credits] spends credits and has a free preview (dry_run, or confirm=false) — quote the cost and never confirm a spend on the person's behalf. The tool descriptions are the reference: read them before calling.

A show makes one video per new item, on a cadence, from a format. The person asked for: **$ARGUMENTS**

## Do this

1. Find the source: a public feed on the site (feed.xml, rss.xml, atom.xml, a JSON feed, a changelog) — read this repository for one if it is the site's code.
2. `create_format` for the show (free, validated against a sample item), then `create_show` on it with `max_episodes_per_run` 1 and a low `max_credits_per_day` unless the person says otherwise.
3. `run_show` with confirm=false and show what the first run would make and cost. A new show is HELD until its owner confirms once: do NOT confirm for them.
4. Report the format id, the show id, the source, the cadence and the first run's preview.
