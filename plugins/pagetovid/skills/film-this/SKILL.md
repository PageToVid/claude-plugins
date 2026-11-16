---
name: film-this
description: Film the project you are working on with PageToVid, in one line. Use when someone says "film this", "film my site", "make a video of my site", "make a launch video", "a demo video of this app", "/pagetovid" or "/film-this", or wants a short video to show what they built. Finds the public URL from the project (package.json, README, Vercel/Netlify config) or asks for it, makes a free draft first, then offers the full render and drafts the post to share it. Needs the PageToVid MCP server (https://pagetovid.com/mcp).
---

# Film this

The person built something and wants a video of it. PageToVid films the real, public website in a browser, writes the script, voices and captions it, and returns an MP4. You drive it through the PageToVid MCP server. Keep it short: one question at most before the free draft.

## 0. Check the connection

The tools come from the MCP server `pagetovid` (https://pagetovid.com/mcp). If no PageToVid tool is available, stop and tell the person how to connect it, then continue once they have:

- Claude Code: `/plugin marketplace add PageToVid/claude-plugins` then `/plugin install pagetovid@pagetovid`, then `/mcp` and sign in to `pagetovid`.
- Codex: `codex mcp add pagetovid --url https://pagetovid.com/mcp` then `codex mcp login pagetovid`.
- Any other agent: add `https://pagetovid.com/mcp` as a remote (streamable HTTP) MCP server. It signs in with OAuth; an agent that cannot do OAuth can send an API key from pagetovid.com as `Authorization: Bearer cp_live_xxx` (never write a real key into a file that gets committed).

If a tool answers "not authorised", the person has to sign in again (`/mcp` in Claude Code).

## 1. Find the URL to film

PageToVid films **public** pages only. Look, in this order, and stop at the first public `https://` URL that is the product itself (not a docs host, a badge, a CDN or a package registry):

1. What the person said.
2. `package.json`: `homepage`.
3. `README.md` (and `README.*`): a "Live", "Demo", "Website" or "Try it" link near the top.
4. Deploy config: `vercel.json` / `.vercel/project.json` (project name, aliases), `netlify.toml` (or `.netlify/state.json`), `CNAME` (GitHub Pages), `fly.toml` (`app` → `https://<app>.fly.dev`), `wrangler.toml` / `wrangler.jsonc` (routes), `app.json` / `render.yaml`. Only use a host the file actually names; never guess a domain.
5. Otherwise ask one question: "Which public URL should I film?"

Say which URL you picked and where you found it.

**Only on localhost?** Say it plainly: PageToVid films public URLs and cannot reach `localhost`, `127.0.0.1` or a private network. Offer the ways round, and let the person choose:

- deploy a preview (`vercel` gives a preview URL, `netlify deploy` a draft URL, or a branch preview from their host), and check the preview is not behind the host's own login protection;
- open a public tunnel to the dev server (for example `cloudflared tunnel --url http://localhost:3000` or `ngrok http 3000`) for the length of the render;
- or, with no URL at all, `create_animation` makes a video from scenes written from the README.

**Behind a login?** A page behind a sign-in is filmed only through a capture session from the PageToVid VS Code or Chrome extension (Scale plan and up). Say so, and suggest filming the public landing page instead.

## 2. Look at the page (free)

Call `inspect_page` with the URL, in the shape you will film:

- 16:9 by default (a launch or demo video, the desktop layout);
- `9:16` when the person mentions Reels, Shorts, TikTok, a story or a phone: it films the page's mobile layout;
- `1:1` or `4:5` for a feed post.

If the reply says `blocked` (a robot check, a sign-in, a missing page), tell the person what stood in the way and stop or switch to `create_animation`. Otherwise note the two or three strongest candidates: they tell you what the film can show.

## 3. Make the free draft

Call `create_video` with `draft: true`. A draft is free: no credits, a third of the resolution, a DRAFT mark, no AI visuals, a few an hour.

- `url`, `aspect_ratio`, `goal` (`demo` for a product walkthrough, `ad` for a launch, `explainer` otherwise), `target_seconds` (30 to 45 is a good launch length).
- `focus`: what the page cannot show, written from the project: who it is for, the one thing it does, the call to action. Take it from the README, never invent a feature, a number, a customer or a quote. A line in quotation marks is said word for word.
- `language` only when the person asks for one or the page is in one they did not want; it defaults to the page's own. The script and voice can be in English, French, Spanish, German, Italian, Portuguese, Dutch, Arabic, Hindi, Korean, Polish, Turkish or Swedish.

The call returns a `video_id` at once. Poll `get_video` after `poll_after_seconds` until `status` is `done`, `held` or `error` (a render takes minutes). While it runs, say the phase in one line, not every poll.

Then show: the draft's link, its length, and every item in `warnings`. If it ended in `error`, give the reason from `error` and what to change.

## 4. Offer the full film

Ask before anything that costs. Call `get_account` (plan, credits left, what the plan can do) and `quote_cost` with the `video_id` (the price of the next `rerender_video`). Tell the person what the full render costs on their account and what they have, in the figures those tools return. Never state a price from memory and never invent one.

On their go, call `rerender_video` with the `video_id` and no `draft`. It renders the full-resolution film from the same storyboard, with no re-plan. Poll `get_video` the same way and report the MP4 link, the share page, the length and every warning. A failed render is refunded automatically. If the result carries `upgrade`, relay its message and link once.

Changes before or after the full render: `get_storyboard`, then `update_storyboard` (free, every edit undoable with `restore_revision`), then `rerender_video`. The same film in another language: `translate_video`. Another shape of the same film: `rerender_video` with `outputs` (each shape is its own render).

## 5. Draft the post to share it

Once a film is done, offer a post. Read `get_storyboard` and write from what the film actually says, nothing more:

- **X**: one or two sentences under 280 characters, the link, no hashtag wall.
- **LinkedIn**: three to five short lines: the problem, what was built, what the video shows, the link.
- **Product Hunt**: a tagline under 60 characters and a two-sentence description.

Label it clearly as **Draft, edit before posting**. Use the person's own product name and claims from the storyboard and README only; no invented metrics, users or quotes, no exclamation marks. PageToVid posts nowhere: the person publishes it themselves.

## What not to do

- Never claim PageToVid can film `localhost`, a private network, a page behind a login (without the extension) or past a robot check.
- Never start a paid render, or confirm a spend, without the person's yes.
- Never type a name, email or password into the site, or ask PageToVid to.
- Never commit an API key.

For anything beyond this quick path (animations, AI clips, recurring shows, how-to series), the `pagetovid-video` skill and the prompts `make_an_ad`, `make_a_vertical`, `make_a_demo` and `fix_this_film` go further.
