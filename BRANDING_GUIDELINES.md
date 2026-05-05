# BlackOps docs — branding guidelines

Working rules for the Mintlify branding settings. These match the live site's brand tokens (`src/app/globals.css`). When in doubt, the website is the source of truth.

## Source of truth (from the web)

These are the brand tokens defined in `src/app/globals.css`. Anything in the docs branding should be derived from one of these.

| Token | Hex | Used for |
|---|---|---|
| `--color-black-bg` | `#070709` | Page background (the actual web background — not pure black) |
| `--color-black-primary` | `#000000` | True black, deepest fills |
| `--color-black-soft` | `#050505` | Slightly elevated black surfaces |
| `--color-gray-xdark` | `#1c1b20` | Card surfaces, raised elements |
| `--color-gray-dark` | `#3d3c41` | Borders, grid lines, dividers (this is the recurring "line" color across the site) |
| `--color-gray-medium` | `#7f7e83` | De-emphasized secondary text |
| `--color-gray-light` | `#d6d5da` | Light text on dark surfaces |
| `--color-gray-xlight` | `#e6e6e6` | Lightest gray |
| `--color-text-primary` | `#ffffff` | Primary text |
| `--color-text-secondary` | `#a1a0a5` | Secondary text |

**The brand is monochrome.** There is no accent color on the website. No green, no blue, no purple. If a docs setting demands an "accent", use white (#ffffff) or a gray.

## Mintlify settings — what to put in each field

These map to the panels you screenshot.

### Theme

`luma`. Already correct. Luma's dark-with-glow aesthetic matches the site.

### Colors → Primary / Light / Dark

This is the brand color set used for links, button backgrounds, and accents.

| Field | Current value | Correct value | Why |
|---|---|---|---|
| Primary color | `#ffffff` | `#ffffff` | Keep. Matches web `--color-text-primary`. |
| Light | `#07C983` (green) | `#ffffff` | **Replace.** The green is not a brand color. The web has no accent; primary action color is white. |
| Dark | `#000000` | `#ffffff` | **Replace.** Mintlify's "Dark" here is the brand color used in dark mode (not the background). For our brand this should be white, same as light, since the brand is monochrome. |

Result: links and primary highlights will be white in both modes, which matches how the website handles emphasis (white text against the dark backdrop).

### Logo → Light logo / Dark logo

| Field | Recommended value | Why |
|---|---|---|
| Light logo (shown on light/white background) | The black-on-transparent variant of the logo (or `logomark.svg` if a wordmark version doesn't exist) | A white-on-transparent SVG vanishes on a white background. |
| Dark logo (shown on dark background) | `logo.svg` from `/public/logo.svg` | This is the white-on-transparent version used on the live site. |
| Logo link | `https://blackops-theta.vercel.app/` (or the production URL when it lands) | Clicking the logo should return readers to the marketing site, not the docs index. |

**Note on the current `media.brand.dev/...` URLs.** Both the light and dark logo are pointing to the same SVG, which means one of the two will be invisible. Replace with the local `logo.svg` (and a black-on-transparent version for the light slot, if the design system has one). If only a white logo exists, set the light-mode background dark enough that it stays visible, or accept that light mode is not supported and disable it (see below).

### Background → Light color / Dark color

| Field | Current value | Correct value | Why |
|---|---|---|---|
| Light color | `#FFFFFF` | `#FFFFFF` | Keep if supporting light mode. |
| Dark color | `#000000` | `#070709` | **Replace.** This is `--color-black-bg` from the site. The site is not pure black; it has a slight blue-purple lift. |

If you choose to ship dark-only docs (recommended for brand consistency, since the site has no light mode), Mintlify supports a dark-only setting. Saves the trouble of producing a black logo.

### Background image / Background decoration

Leave blank for now. The site uses subtle vertical "grid lines" as decoration — those are section-specific (rendered via gradients in components like `SpanningLines` and `Comparison.tsx`). Reproducing them in docs is not worth the effort and would make docs feel busier than the marketing site, which is the opposite of the intent. Plain dark background is correct.

### Navbar links

Suggested entries:

- **App** → link to the running app or early-access flow.
- **Site** → link back to `https://blackops-theta.vercel.app/`.

Keep to two. Nav-bar links over three start to feel like marketing nav.

### Banner content

Leave empty unless there is something time-sensitive to communicate (e.g. "V1.0 access requests open"). Banners shipped permanently become noise.

## Fonts

The site uses three fonts. Mintlify supports custom Google Fonts via the JSON config; if the branding panel exposes a font picker, set it to match.

| Role | Family (web) | Mintlify field |
|---|---|---|
| Headings | **Roboto Flex** | Heading font |
| Body | **Mona Sans** | Body font |
| Code | Geist Mono | Code font (or accept Mintlify default — body of docs is more navigable with a familiar mono) |

Both Roboto Flex and Mona Sans are on Google Fonts. If the Mintlify settings UI doesn't expose font picking, this requires editing `docs.json` directly:

```json
"fonts": {
  "heading": { "family": "Roboto Flex", "weight": 450 },
  "body":    { "family": "Mona Sans", "weight": 400 }
}
```

The site uses Roboto Flex at weight 450 (not the Google default 400) for headings — important for matching the visual weight.

## What not to add

- **No accent color** beyond white. The brand is monochrome on purpose.
- **No emoji icons** on cards or in the sidebar. Lucide icons (`shield`, `route`, `cube`, etc.) are fine; they match the linear, geometric feel of the site.
- **No gradients** in the body. The site uses gradients only for the dissolving line effect, which is decorative and section-bound.
- **No screenshots of the marketing site** in the docs. Docs should not look like a sales surface.
- **No hero images** at the top of pages. The site has them; docs do not need them.

## Quick check before publishing branding changes

- [ ] Logo is visible on the chosen background (white logo on dark bg, or dark logo on light bg).
- [ ] Dark mode background is `#070709`, not pure `#000000`.
- [ ] No green, blue, or purple accent anywhere.
- [ ] Font families match the site (Roboto Flex headings, Mona Sans body).
- [ ] Logo click destination is the marketing site, not the docs root.
- [ ] Banner is empty (or genuinely time-sensitive).
