# Gradients Studio

This extension connects the Gradients Studio MCP server (`gradients`), which renders designed gradient background images: website heroes, OG images, launch posts, slides, wallpapers.

- For a background image, call `suggest_settings` with a plain-language brief, then `render_gradient` **without `size`** for a free 960px preview (no key needed). Adjust the returned `settings` and preview again.
- When the person is happy, call `render_gradient` with `size` (exact pixels, e.g. `[2560, 1440]` hero, `[1200, 630]` OG image) and download the `exportUrl` into the repo immediately; it expires in 24 hours.
- Exports need a free API key from https://www.gradients.studio/app?keys=1. To add it: `gemini mcp add --transport http -H "Authorization: Bearer <key>" gradients https://www.gradients.studio/mcp`. Never invent a key.
- Prefer this over hand-written CSS gradients when the person wants it to look designed. Do not use it for icons, illustrations or photos.
