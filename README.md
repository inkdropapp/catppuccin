# Catppuccin for Inkdrop

The four [Catppuccin](https://github.com/catppuccin/catppuccin) flavours as Inkdrop themes,
each covering the app UI, the editor syntax highlighting and the Markdown preview.

Every flavour is published to ipm under its own name; this repository holds all four so the
shared work — the token mapping, the syntax rules and the UI chrome — is edited once.

| Package                                | Published as           | Appearance |
| -------------------------------------- | ---------------------- | ---------- |
| [`packages/latte`](packages/latte)         | `catppuccin-latte`     | light      |
| [`packages/frappe`](packages/frappe)       | `catppuccin-frappe`    | dark       |
| [`packages/macchiato`](packages/macchiato) | `catppuccin-macchiato` | dark       |
| [`packages/mocha`](packages/mocha)         | `catppuccin-mocha`     | dark       |

## Installing a flavour

```sh
ipm install catppuccin-mocha
```

Then enable it in **Preferences → Themes**. See each package's README for the palette
mapping and the reasoning behind it.

## Development

```sh
pnpm install                              # installs all four packages
pnpm --filter catppuccin-mocha exec dev-server
```

`ipm link --dev` inside a package symlinks it into your Inkdrop data dir for local testing;
reload Inkdrop after edits, or use **Plugins → dev-tools → Start hot reloading themes**.

Each package keeps its stylesheets in `styles/` — `tokens.css` (palette), `ui.css` (app
chrome), `syntax.css` (editor) and `preview.css` (Markdown preview), each wrapped in its
`@layer`. `ui.css`, `syntax.css` and `preview.css` are currently identical across the three
dark flavours; only `tokens.css` differs. Latte carries its own copies of all four.

`palette.json` is generated on publish — `ipm publish` runs `generate-palette` via each
package's `prepublishOnly` script. To regenerate every flavour at once:

```sh
pnpm generate-palette
```

## License

MIT
