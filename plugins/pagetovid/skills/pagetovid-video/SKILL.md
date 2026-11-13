---
name: pagetovid-video
description: Use when the person wants a video of a website, a web page, a product or an app (a demo, an ad, a launch or explainer video, a vertical reel for TikTok/Shorts/Reels, a how-to or walkthrough), a narrated screencast, an animated video from data, a script or slides, a short AI clip or still for a video, or wants to edit, translate or re-render a video they made with PageToVid. Covers which PageToVid tool to call, in what order, and how to quote the cost before any paid call.
---

# Making videos with PageToVid

PageToVid is connected as the MCP server `pagetovid` (https://pagetovid.com/mcp). The first call opens a sign-in in the browser; if a tool answers "not authorised", run `/mcp` and authenticate `pagetovid`. The tool descriptions are the reference for every parameter: read them before calling.

## Money first

- Tools whose description starts with `[Free]` spend nothing.
- A tool marked with a credit price spends credits. Before calling it, quote the cost with `dry_run: true` (or `quote_cost`) and ask the person. Never confirm a spend on their behalf.
- `get_account` says the plan, the credits left and whether AI visuals are available. Call it before the first paid call of a conversation.

## Pick the path

| The person wants | Do |
|---|---|
| A video of a public web page | `inspect_page` (in the aspect ratio to film) → `create_video` with `draft: true` (free preview) → `get_storyboard` → edits with `update_storyboard` → `rerender_video` for the full film |
| A video without a web page (data, a story, slides, a script) | `create_animation` with scenes written from what they gave you |
| A vertical reel (9:16) | the same, with `aspect_ratio: "9:16"`: it films the page's mobile layout |
| One AI clip or still, not a video | `generate_asset` (`dry_run: true` first); for a clip, keep the `job_id` and follow it with `get_asset_job` if the call answers `generating` |
| Change a finished video | `get_storyboard` → `update_storyboard` (free, undoable) → `rerender_video` |
| The same video in another language | `translate_video` |

## Follow a render

Every start returns a `video_id` at once. Poll `get_video` after `poll_after_seconds` until the status is `done`, `held` or `error`. Before saying it is finished, read `warnings` and tell the person every one of them.

## Things PageToVid does not do

- Pages behind a sign-in are filmed only through a capture session from the PageToVid browser or VS Code extension; a robot check cannot be filmed past (use `create_animation` instead).
- It never types personal data into a site, never posts anywhere, never clones a voice.

When the person is unsure what to make, the prompts `make_an_ad`, `make_a_vertical`, `make_a_demo` and `fix_this_film` walk through each case.
