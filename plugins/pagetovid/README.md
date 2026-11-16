# PageToVid for Claude Code

Turn any web page into a narrated video without leaving the terminal. PageToVid opens the page in a real browser, picks what is worth filming, writes the script, records the site, adds an AI voice-over with captions and music, and renders an MP4 in 16:9, 9:16 or 1:1. It also animates content you give it — numbers, notes, a story, a slide deck — with no page at all.

## What this plugin adds

- **The PageToVid MCP server** (`https://pagetovid.com/mcp`): the tools to make, edit, translate and publish videos. You sign in with your PageToVid account in the browser the first time (OAuth); no API key is stored in any file.
- **Skills**
  - `film-this` — say "film this" or "make a launch video of my site": finds the project's public URL, makes a free draft, offers the full render at your account's price, drafts a post to share it
  - `pagetovid-video` — which PageToVid tool to call for every other kind of video
- **Slash commands**
  - `/pagetovid:video <url>` — a narrated video of a web page
  - `/pagetovid:animate <content>` — an animated video from your own content
  - `/pagetovid:edit [video] <change>` — edit the storyboard, re-render, translate
  - `/pagetovid:howto [feature]` — plan how-to videos from this repository's docs
  - `/pagetovid:show [site] [what recurs]` — a recurring video for each new item of a feed

## What it sends and spends

The MCP server is PageToVid's own service at pagetovid.com. When you ask for a video, the page URL and the brief you approve are sent there; the video is rendered on PageToVid's servers and stored on your account. Tools that spend credits say so, have a free preview, and the commands ask before every spend. A failed render is refunded automatically. Free accounts make watermarked videos; paid plans remove the watermark and unlock AI clips and stills. Privacy policy: https://pagetovid.com/privacy

## Install

```
/plugin marketplace add PageToVid/claude-plugins
/plugin install pagetovid@pagetovid
```

Then run `/mcp`, choose **pagetovid** and sign in.

Codex reads the same plugin (`.codex-plugin/plugin.json`):

```
codex plugin marketplace add PageToVid/claude-plugins
codex plugin add pagetovid@pagetovid
```

Any agent the skills CLI supports:

```
npx skills add PageToVid/claude-plugins --skill film-this
```

then add `https://pagetovid.com/mcp` as a remote MCP server in that agent.

Docs: https://pagetovid.com/assistants · Support: hello@pagetovid.com
