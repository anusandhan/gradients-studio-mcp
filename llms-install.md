# Installing the Gradients Studio MCP server

Instructions for an AI agent (Claude Code, Cursor, Codex, Cline, Windsurf, VS Code and others) setting up this server for a person.

Gradients Studio renders gradient background images (website heroes, OG images, launch posts, slides, wallpapers) at exact pixel sizes. It is a remote MCP server; there is nothing to download or run.

- URL: `https://www.gradients.studio/mcp`
- Transport: Streamable HTTP (stateless)
- Tools: `render_gradient`, `list_palettes`, `suggest_settings`

## 1. Install without a key (do this first)

No key, account or sign-up is needed for `list_palettes`, `suggest_settings` or `render_gradient` previews (a 960px image returned inline). Install keyless, then confirm it works by rendering a preview.

### Claude Code

```bash
claude mcp add gradients --transport http https://www.gradients.studio/mcp
```

### Cursor

Add to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (this project):

```json
{
  "mcpServers": {
    "gradients": { "url": "https://www.gradients.studio/mcp" }
  }
}
```

### Codex

```bash
codex mcp add gradients --url https://www.gradients.studio/mcp
```

Or in `~/.codex/config.toml`:

```toml
[mcp_servers.gradients]
url = "https://www.gradients.studio/mcp"
```

### Windsurf

Add to `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "gradients": { "serverUrl": "https://www.gradients.studio/mcp" }
  }
}
```

### VS Code (Copilot agent mode)

```bash
code --add-mcp '{"name":"gradients","type":"http","url":"https://www.gradients.studio/mcp"}'
```

Or in `.vscode/mcp.json`:

```json
{
  "servers": {
    "gradients": { "type": "http", "url": "https://www.gradients.studio/mcp" }
  }
}
```

### Cline, Claude Desktop, Gemini CLI and other clients

Any client that supports remote MCP servers over Streamable HTTP: add a server named `gradients` with the URL `https://www.gradients.studio/mcp`. In Claude Desktop or claude.ai: Settings → Connectors → Add custom connector. In Gemini CLI: `gemini mcp add --transport http gradients https://www.gradients.studio/mcp`.

### Check it works

Call `suggest_settings` with a brief such as `"dark, grainy hero, a bit like Linear"`, then `render_gradient` with one of the returned `settings` and no `size`. You should get an image back.

## 2. Add a key for exports (only when the person wants a file)

`render_gradient` with a `size` (exact pixels, for example `[2560, 1440]` for a hero or `[1200, 630]` for an OG image) returns a download URL. That needs a free API key; without one, the call returns a message saying so, plus the preview.

1. The person creates a key at https://www.gradients.studio/app?keys=1 (sign in, then account menu → API keys). The key starts with `gs_live_` and is shown once. Do not invent or guess one; ask the person to paste it.
2. Send it on every request as the header `Authorization: Bearer <key>` (or `X-API-Key: <key>`).

Claude Code (replace the keyless entry):

```bash
claude mcp remove gradients
claude mcp add gradients --transport http https://www.gradients.studio/mcp --header "Authorization: Bearer <key>"
```

JSON configs (Cursor, Cline and others): add `"headers": { "Authorization": "Bearer <key>" }` next to `"url"`. Windsurf uses the same `headers` field next to `serverUrl`.

Codex: `codex mcp add gradients --url https://www.gradients.studio/mcp --bearer-token-env-var GRADIENTS_STUDIO_KEY`, with the key in that environment variable.

VS Code: add `"headers": { "Authorization": "Bearer ${input:gradients-key}" }` and an input `{ "type": "promptString", "id": "gradients-key", "description": "Gradients Studio API key", "password": true }`.

Keep the key out of committed files: prefer user-level config or an environment variable.

## Limits and costs

- Previews, palettes and suggestions: free. Without a key, 30 calls a minute and 300 a day per address.
- Sized exports: 5 free a month per account, unlimited on Pro. Asking for the same export again within 24 hours returns the same URL and costs nothing. Download URLs are valid for 24 hours, so download the file into the repo right away (for example `curl -o public/hero.jpg "<exportUrl>"`).
- Pixel and dither finishes preview free and export on Pro.

## Using it well

- Start from `suggest_settings` (a plain-language brief) or `list_palettes` (palettes and six tuned starting points).
- Preview without `size`, show the person, adjust the returned `settings`, preview again. Only export once they are happy.
- Every result has a `studioUrl` that opens the same settings in the browser studio.

More: https://www.gradients.studio/mcp · Support: hello@gradients.studio
