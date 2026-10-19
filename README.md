# Gradients Studio MCP

Gradient backgrounds for coding agents. Describe the background in plain words ("dark, grainy, a bit like Linear") and your agent previews it, adjusts it, and drops the finished file into your repo at the exact size the layout needs: a website hero, an OG image, a launch post, a slide.

![Gradients Studio MCP](https://www.gradients.studio/landing/og-mcp-hero.jpg)

- **Server:** `https://www.gradients.studio/mcp` (remote, Streamable HTTP, stateless)
- **No key to start:** previews, palettes and suggestions work without an account.
- **Exports:** exact-size files with a download URL need a free API key; 5 free a month, unlimited on Pro.
- **Docs:** https://www.gradients.studio/mcp · agent install guide: [llms-install.md](llms-install.md)

This repository holds the server's public listing files and docs only. The service itself is hosted; there is nothing to build or run.

## Install

**Claude Code**

```bash
claude mcp add gradients --transport http https://www.gradients.studio/mcp
```

Or as a plugin, which adds a skill that tells Claude when to reach for it:

```bash
/plugin marketplace add anusandhan/gradients-studio-mcp
/plugin install gradients-studio@gradients-studio
```

**Cursor:** [Add to Cursor](https://www.gradients.studio/mcp#install), or add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "gradients": { "url": "https://www.gradients.studio/mcp" }
  }
}
```

**Codex**

```bash
codex mcp add gradients --url https://www.gradients.studio/mcp
```

**VS Code**

```bash
code --add-mcp '{"name":"gradients","type":"http","url":"https://www.gradients.studio/mcp"}'
```

**Gemini CLI**

```bash
gemini extensions install https://github.com/anusandhan/gradients-studio-mcp
```

**Windsurf, Cline, Claude Desktop and others:** add a remote server named `gradients` with the URL above. Per-client details are in [llms-install.md](llms-install.md).

### Add a key for exports

1. Create a key at https://www.gradients.studio/app?keys=1 (sign in, then account menu → API keys). It is shown once.
2. Send it as `Authorization: Bearer <key>`:

```bash
claude mcp remove gradients
claude mcp add gradients --transport http https://www.gradients.studio/mcp --header "Authorization: Bearer <key>"
```

In JSON configs, add `"headers": { "Authorization": "Bearer <key>" }` next to `"url"`. With the Claude Code plugin, set `GRADIENTS_STUDIO_KEY` in your environment instead.

## Tools

| Tool | What it does | Key |
| --- | --- | --- |
| `suggest_settings` | Turns a brief ("dark, premium fintech hero, a bit retro") into two or three starting settings. Understands jobs, moods, colors, product names, styles and finishes. | No |
| `list_palettes` | The studio's sixteen palettes, palettes behind sites people admire (Linear, Stripe, Raycast…), and six tuned starting points for common jobs. Your saved palettes too, with a key. | No |
| `render_gradient` | Renders with every dial the studio has: blobs, stripes, clouds or rays; grain; pixel and dither finishes; shape overlays or your logo SVG. Without `size`: a free 960px preview inline. With `size`: an exact-size export and a download URL valid for 24 hours. | Only for `size` |

Every result includes the settings (send them back to iterate) and a studio link to take over in the browser. Asking for the same export again within 24 hours returns the same URL and costs nothing.

## Example prompts

- "Add a dark, grainy hero background to the landing page, 2560×1440, something like Linear."
- "Make a 1200×630 OG image background in our brand colors from `tailwind.config.ts`."
- "Give the pricing section a soft pastel gradient background; preview three options first."
- "Make a LinkedIn launch post background, 1080×1350, with our logo as a subtle outline."
- "Generate a retro pixel-finish wallpaper for the 404 page."

## What it makes

| Website hero | Launch post | Deck slide |
| --- | --- | --- |
| ![Website hero](https://www.gradients.studio/landing/in-use/website-hero.jpg) | ![Launch post](https://www.gradients.studio/landing/in-use/launch-post.jpg) | ![Deck slide](https://www.gradients.studio/landing/in-use/deck-slide.jpg) |

## Limits

- Without a key: 30 calls a minute and 300 a day per address.
- With a key: previews are free; sized exports use the account's monthly pool (5 free, unlimited on Pro), with a cap of 200 sized exports a day on every plan.
- Pixel and dither finishes preview free and export on Pro.

## Files in this repo

- `server.json`: the [MCP Registry](https://registry.modelcontextprotocol.io) entry
- `.claude-plugin/`, `.mcp.json`, `skills/`: the Claude Code plugin and its marketplace
- `.codex-plugin/`: the Codex plugin
- `gemini-extension.json`, `GEMINI.md`: the Gemini CLI extension
- `glama.json`: the Glama listing
- `llms-install.md`: install instructions written for agents

## Support

hello@gradients.studio · [Privacy](https://www.gradients.studio/privacy) · [Terms](https://www.gradients.studio/terms)

The files in this repository are MIT licensed; see [LICENSE](LICENSE).
