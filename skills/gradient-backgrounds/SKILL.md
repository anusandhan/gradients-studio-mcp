---
name: gradient-backgrounds
description: Make a designed gradient background image (website hero, section background, OG or social image, launch post, slide, App Store shot, wallpaper) with the Gradients Studio MCP tools instead of writing a CSS gradient or using a stock image. Use when the person asks for a background, hero image, OG image, gradient, or "something like Linear/Stripe/Raycast" behind content.
---

# Gradient backgrounds with Gradients Studio

Use the `gradients` MCP server (tools `suggest_settings`, `list_palettes`, `render_gradient`) whenever the job is an image behind content: a landing-page hero, a section background, an OG/social card, a launch post, a deck slide, an App Store screenshot backdrop or a wallpaper. Prefer it over a hand-written CSS `linear-gradient`/`radial-gradient` when the person wants it to look designed (grain, soft mesh, a finish), and over stock images.

Do not use it for icons, illustrations, photos, UI components or charts.

## Loop

1. **Brief → settings.** Call `suggest_settings` with the job and mood in plain words, e.g. `"dark, premium fintech hero, a bit like Linear"`. If the project has brand colors (Tailwind config, CSS variables, a logo), put them in the brief or pass them as `colors`/`backgroundColor` later. `list_palettes` has more starting points.
2. **Preview (free, no key).** Call `render_gradient` with a suggestion's `settings` and an `aspectRatio`, and **no `size`**. You get a 960px image inline. Look at it. Show it to the person when their taste matters.
3. **Adjust.** Send the returned `settings` back with changes (keep `seed` to keep the composition). Keep `blur` 700–900 and `contrast` around 130 for the soft mesh look; use saturated mid-tone colors.
4. **Export (needs a key).** Once the person is happy, call `render_gradient` with `size` set to the exact pixels the layout needs (`[2560, 1440]` for a hero, `[1200, 630]` for an OG image, `[1080, 1350]` for a LinkedIn post). Download the returned `exportUrl` into the repo right away, for example `curl -o public/hero.jpg "<exportUrl>"`, since the URL expires in 24 hours. Then wire it in (CSS `background-image`, `<Image>`, `og:image` metadata).

## If an export says a key is needed

Previews never need a key; exports do. Tell the person, in one or two sentences, that a free key from https://www.gradients.studio/app?keys=1 unlocks exports (5 free a month), and that it goes in the `GRADIENTS_STUDIO_KEY` environment variable for this plugin (or as the header `Authorization: Bearer <key>`). Never invent a key. Meanwhile keep previewing, or hand them the `studioUrl` from the result to export in the browser.

## Good defaults

- Hero on a dark site: dark `backgroundColor`, 3–4 saturated colors, `grain` 0.2–0.3, `style` `blobs`.
- Light, friendly product: pale `backgroundColor`, pastel-but-saturated colors, `grain` 0.15.
- Retro or terminal feel: `effect` `pixel` or `dither` (previews free; exports on Pro).
- Brand mark in the background: pass the logo SVG's raw text as `overlaySvg`.
