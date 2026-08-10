# catppuccin-latte

The light [Catppuccin](https://github.com/catppuccin/catppuccin) flavour — Latte — for
Inkdrop. A single theme covering the app UI, the editor syntax highlighting and the
Markdown preview.

![Screenshot of catppuccin-latte](./docs/screenshot.png)

Other flavours: [Frappé](../frappe) · [Macchiato](../macchiato) · [Mocha](../mocha)

## How to install

```sh
ipm install catppuccin-latte
```

Then enable it in **Preferences → Themes**.

## Palette

The 12-step greyscale becomes Inkdrop's `neutral` ramp, and twelve Latte accents each take
over the Inkdrop ramp closest to their hue:

| Inkdrop ramp     | Latte       |     | Inkdrop ramp | Latte    |
| ---------------- | ----------- | --- | ------------ | -------- |
| `neutral-50…950` | base → text |     | `sky`        | sky      |
| `red`            | red         |     | `cyan`       | sapphire |
| `rose`           | maroon      |     | `teal`       | teal     |
| `pink`           | pink        |     | `green`      | green    |
| `purple`         | mauve       |     | `yellow`     | yellow   |
| `violet`         | lavender    |     | `orange`     | peach    |
| `blue`           | blue        |     |              |          |

Latte ships one intensity per accent, so each is anchored at its ramp's **500** stop and the
remaining ten stops are extrapolated in HSL — tints toward a 96% lightness ceiling, shades
toward a 20% floor, with saturation easing off at both ends. Every anchor round-trips to its
exact Latte hex, each ramp is monotonic in lightness, and no two tokens carry the same value.

`rosewater`, `flamingo` and `subtext1` have no ramp of their own and are exposed as
`--ctp-rosewater`, `--ctp-flamingo` and `--ctp-subtext1`.

Surfaces follow Catppuccin's own layering: **base** for the page, editor and modal content,
**mantle** for panels, menus, popups and the note list, **crust** for the sidebar and inputs.

### Colors Latte doesn't have

Inkdrop's token set includes `amber`, `lime` and `emerald` ramps with no Latte counterpart.
Rather than invent colors, the semantics that reached for them are repointed:

- **Warnings** use yellow, per the Catppuccin style guide (was amber).
- **Olive** — the `olive` tag and the `--olive*` aliases — takes green's darker shades, the
  same trick the app itself uses to derive `--brown` from `--color-yellow-800`.
- **Note statuses** are sapphire / yellow / green / maroon for active / on hold / completed /
  dropped.

The `default`, `grey` and `black` tags take the greyscale, and `brown` takes yellow's shades.
With those in place, all 1581 variables Inkdrop resolves land inside the Latte palette.

### Syntax

Token colors follow the "Code Editors" table of the
[Catppuccin style guide](https://github.com/catppuccin/catppuccin/blob/main/docs/style-guide.md):
keywords mauve, strings green, constants and numbers peach, operators sky, comments and
delimiters overlay2, types and attributes yellow, functions and properties blue, parameters
maroon, macros rosewater, and the cursor rosewater. Headings — in both the editor and the
preview — take the rainbow-highlight sequence: red, peach, yellow, green, sapphire, lavender.

The theme deliberately sets no `font-family`, so your **Font Family** preference is respected.

## Development

```sh
pnpm install           # once, from the workspace root
ipm link --dev         # symlink into your Inkdrop data dir for local testing
pnpm exec dev-server   # browse every available variable + live component preview
```

Edit the stylesheets in `styles/` — `tokens.css` (palette), `ui.css` (app chrome),
`syntax.css` (editor) and `preview.css` (Markdown preview), each wrapped in its `@layer` —
then reload Inkdrop, or use **Plugins → dev-tools → Start hot reloading themes**.

`palette.json` is generated automatically on publish — `ipm publish` runs `generate-palette`
via the `prepublishOnly` script, so you don't commit it by hand.
