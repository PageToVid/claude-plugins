# PageToVid plugins for coding agents

[PageToVid](https://pagetovid.com) turns a public web page into a narrated, captioned MP4 by filming the real site. This repository packages it for coding agents: an MCP server, a one-line **film this** skill, and slash commands.

## Film this in one line

Install once, then say **"film this"** (or "make a launch video of my site") in the project you are working on. The skill finds the project's public URL in `package.json`, the README or the Vercel/Netlify config (or asks), makes a **free draft** first, then offers the full render at the price your account shows, and drafts a post to share it.

**Claude Code**

```
/plugin marketplace add PageToVid/claude-plugins
/plugin install pagetovid@pagetovid
```

Then run `/mcp`, choose **pagetovid** and sign in (free sign-up).

**Codex**

```
codex plugin marketplace add PageToVid/claude-plugins
codex plugin add pagetovid@pagetovid
```

If the PageToVid tools do not show up, add the server directly: `codex mcp add pagetovid --url https://pagetovid.com/mcp`, then `codex mcp login pagetovid`.

**Any agent the [skills CLI](https://github.com/vercel-labs/skills) supports** (Cursor, Copilot, Gemini CLI, opencode, Codex and more)

```
npx skills add PageToVid/claude-plugins --skill film-this
```

Add `-g` to install it for every project. The skill needs the MCP server: add `https://pagetovid.com/mcp` as a remote (streamable HTTP) MCP server in your agent. It signs in with OAuth; an agent without OAuth can send an API key from your PageToVid account as `Authorization: Bearer cp_live_xxx`.

**What to know**

- MCP server: `https://pagetovid.com/mcp`.
- The draft is free. The full film costs credits; the skill reads your account and quotes the price before asking.
- Public URLs only. A project that runs only on `localhost` needs a preview deploy (Vercel, Netlify) or a tunnel first. Pages behind a login need the [VS Code](https://marketplace.visualstudio.com/items?itemName=pagetovid.pagetovid-capture) or [Chrome](https://chromewebstore.google.com/detail/pagetovid-%E2%80%94-capture/oaiajdabfjpklohkinnacldlojbnjemd) extension (Scale plan and up).
- Say "9:16" or "for Reels" for a vertical film of the mobile layout, or name a language for the voice-over.
- The skill's single source is [`plugins/pagetovid/skills/film-this/SKILL.md`](plugins/pagetovid/skills/film-this/SKILL.md). No installer? Paste that file into your agent's instructions.

## The plugin

| Plugin | What it does |
|---|---|
| [pagetovid](plugins/pagetovid) | The PageToVid MCP server, the `film-this` and `pagetovid-video` skills, and `/pagetovid:video`, `/pagetovid:animate`, `/pagetovid:edit`, `/pagetovid:howto` and `/pagetovid:show` |

Using Claude.ai, Claude Desktop or ChatGPT instead? Add `https://pagetovid.com/mcp` as a custom connector — see https://pagetovid.com/assistants.

## Try it

```
film this
/pagetovid:video https://pagetovid.com a 30-second vertical ad, bold look, draft first
/pagetovid:animate our launch post as a 45-second explainer, no website
/pagetovid:edit last shorten scene 3 and end on "Start free"
```

Drafts are free; nothing is charged until you render the full film. See the
[examples](https://pagetovid.github.io/docs/examples) for what comes out, and the
[tips](https://pagetovid.github.io/docs/tips) for a better film first time.

## More

- [Documentation](https://pagetovid.github.io/docs/) · [MCP tool reference](https://pagetovid.github.io/docs/mcp/tools)
- [VS Code extension](https://marketplace.visualstudio.com/items?itemName=pagetovid.pagetovid-capture) — Claude Code plans the flows worth filming from your code
- [Chrome extension](https://chromewebstore.google.com/detail/pagetovid-%E2%80%94-capture/oaiajdabfjpklohkinnacldlojbnjemd) — capture pages and film your app behind its login
- Bugs and ideas: [open an issue](https://github.com/PageToVid/docs/issues/new/choose) · Follow [@PageToVid on X](https://x.com/PageToVid)

MIT licence.
