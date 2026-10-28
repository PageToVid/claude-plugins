# PageToVid plugins for Claude Code

A Claude Code plugin marketplace from [PageToVid](https://pagetovid.com): make narrated videos of web pages, and animated videos of your own content, from the terminal.

```
/plugin marketplace add PageToVid/claude-plugins
/plugin install pagetovid@pagetovid
```

Then run `/mcp`, choose **pagetovid** and sign in with your PageToVid account (free sign-up).

| Plugin | What it does |
|---|---|
| [pagetovid](plugins/pagetovid) | The PageToVid MCP server plus `/pagetovid:video`, `/pagetovid:animate`, `/pagetovid:edit`, `/pagetovid:howto` and `/pagetovid:show` |

Using Claude.ai, Claude Desktop or ChatGPT instead? Add `https://pagetovid.com/mcp` as a custom connector — see https://pagetovid.com/assistants.

## Try it

```
/pagetovid:video https://example.com a 30-second vertical ad, bold look, draft first
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
