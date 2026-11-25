# 2. Rebranding

All colours, fonts, spacing and shapes come from CSS custom properties, so a rebrand is a handful of edits.

## Where the values live

- `css/tokens.css` holds the defaults for every page.
- `css/pages/<name>.css` overrides the tokens for one page. Most of those files start with that page's colour tokens; `saas.css` only changes the hero background and corner radius, so it uses the defaults.
- Change a token once and every section that uses it follows.

## The colour tokens

| Token | Use |
|---|---|
| `--bg`, `--surface`, `--surface-2` | page, cards and sections, tinted areas and footer |
| `--text`, `--text-muted` | normal and secondary text |
| `--accent` / `--accent-ink` | button background and the text on it |
| `--accent-text` | links and accent-coloured text on `--bg` and `--surface` |
| `--accent-soft` | tinted background behind `--text` |
| `--border`, `--input-border` | decorative lines and the edge of form controls |
| `--focus` | the keyboard focus ring |
| `--danger`, `--success` | error text, success marker |
| `--hero-bg`, `--hero-text`, `--hero-muted` | the hero band (can differ from the page, as on the launch page) |
| `--footer-bg`, `--footer-text`, `--footer-muted` | footer |

## Light and dark themes

`css/tokens.css`, and every page file that changes colours, has the light values in a `:root` block and the dark values twice: once inside `@media (prefers-color-scheme: dark)` for visitors whose system is dark, and once under `:root[data-theme="dark"]` for the toggle button. CSS cannot share one block between the two conditions, so **edit both copies the same way**. A visitor who never touches the toggle follows their system setting.

## Check contrast every time you change a colour

For each pair, text needs a contrast ratio of at least 4.5:1 against its background (3:1 for large text, icons and the edges of controls). Use any contrast checker with these pairs:

- `--text` on `--bg`, `--surface`, `--surface-2`, `--accent-soft`
- `--text-muted` on `--bg`, `--surface`, `--surface-2`
- `--accent-text` on `--bg` and `--surface`
- `--accent-ink` on `--accent`
- `--hero-text` and `--hero-muted` on `--hero-bg`
- `--danger` on `--surface` and `--bg`
- `--input-border` and `--focus` against the surface they sit on (3:1)

Do this in both themes. A contrast checker is one tool: it does not replace testing with real people and assistive technology.

## Fonts

The kit uses system font stacks (`--font-body`, `--font-heading`), so nothing is downloaded and there is nothing to license. To use a web font, add the font files to your own folder, declare them with `@font-face` in `css/tokens.css` and put the family first in the stack. Keep the system fonts after it as a fallback, and check the font's licence allows web use.

## Logo, favicon and artwork

- The logo in the header is an inline `<svg>` next to the brand name inside `<a class="brand">`. Replace the `<svg>` with your own, or with `<img src="../assets/your-logo.svg" alt="">` next to the text.
- `assets/favicon.svg` is the browser-tab icon shared by all pages.
- The hero and section artwork in `assets/*.svg` is original and made of simple shapes. Replace any of it with your own images (give each `<img>` real `alt` text and `width`/`height`), or delete the `<img>` if you do not need it.

## Shape and spacing

`--radius`, `--radius-sm`, `--radius-lg` and `--radius-pill` control corners. The `--step-*` and `--space-*` tokens are fluid: they grow smoothly with the screen width using `clamp()`, so you rarely need media queries.

Made by The Diamond Empire, https://thedempire.shop/
