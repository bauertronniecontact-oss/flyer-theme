# FLYER — Design & authoring contract

Free Shopify OS 2.0 theme by KIOSK (kioskthemes.com). Art direction: **clean minimal** — white, airy, sober, mass-appeal. Demo brand: RUE STUDIO.

## Tokens (defined in `snippets/css-variables.liquid`, editable in theme settings)

| Var | Default | Role |
| --- | --- | --- |
| `--color-bg` | `#FFFFFF` | page background |
| `--color-surface` | `#F6F6F5` | cards, inputs, secondary bg |
| `--color-ink` | `#1A1A1A` | text |
| `--color-muted` | `#666666` | secondary text (AA on white) |
| `--color-line` | `#E8E8E8` | borders, rules |
| `--color-accent` | `#1A1A1A` | buttons, highlights |
| `--color-on-accent` | `#FFFFFF` | text on accent |
| `--font-body-family` / `--font-heading-family` | Work Sans | via font_picker |
| `--font-size-base` | 16px | body size |
| `--heading-scale` | 1.25 | type scale ratio |
| `--page-width` | 1280px | max content width |
| `--page-margin` | 24px | min side margin |
| `--section-spacing` | 64px | default vertical rhythm |
| `--radius-btn` / `--radius-input` / `--radius-card` | 4 / 4 / 8px | corners |
| `--card-ratio` | 4 / 5 | product card image ratio |

**Look**: generous whitespace, hairline `1px solid var(--color-line)` separators, no shadows (except overlays: `0 8px 40px rgb(0 0 0 / 12%)` allowed), subtle 0.15–0.4s ease transitions, images on `--color-surface`. Headings sentence case (no uppercase except `.fl-eyebrow`). Never hardcode colors/sizes — tokens only. No `!important` (only pre-approved in critical.css), no ID selectors.

## Shared CSS already in `assets/critical.css` — REUSE, don't redefine

`.fl-btn`, `.fl-btn--secondary`, `.fl-input`, `.fl-select`, `.fl-textarea`, `.fl-label`, `.fl-field`, `.fl-form-status`, `.fl-form-status--error`, `.fl-eyebrow`, `.fl-section-head`, `.fl-section-head--center`, `.fl-badge`, `.fl-badge--soldout`, `.fl-card` (product card), `.fl-price`, `.fl-product-grid` (cols via `--grid-cols`, `--grid-cols-tablet`, `--grid-cols-mobile`), `.shopify-section` grid (constrained by default, `.full-width` child spans viewport), `.fl-overlay` (scrim), `.visually-hidden`, `.skip-link`.

## Shared snippets — REUSE

- `{% render 'product-card', product: product %}` — every product listing. Optional: `show_quick_add`, `sizes`.
- `{% render 'price', product: product %}` — never render prices by hand.
- `{% render 'quick-add', product: product %}` — posts `/cart/add`, works without JS.
- `{% render 'image', image: ..., url: ..., width: ... %}` — generic responsive image.

## Section authoring rules

1. **Autonomous sections**: each `.liquid` section carries its own `{% schema %}`, `{% stylesheet %}` (root level, NEVER nested in if/for — Shopify rejects it), `{% javascript %}` if needed. One of each max per file. `{% stylesheet %}` does NOT interpret Liquid — dynamic values go inline: `style="--x: {{ section.settings.x }}"`.
2. **CSS prefix `fl-`**, BEM (`fl-hero__title`, `fl-hero--full`). Grid/flex items containing images get `min-width: 0`.
3. **Section vertical padding** (content sections only): two range settings `padding_top` / `padding_bottom` (min 0, max 120, step 4, unit px, default 48), applied `style="padding-block: {{ section.settings.padding_top }}px {{ section.settings.padding_bottom }}px"` on the section wrapper.
4. **Schema**: literal English labels (no `t:` in schemas). `name` / preset names / block names **≤ 25 characters**. Ranges: min/max/step/default with **max 1 decimal** (use whole hundredths + `divided_by: 100.0` in Liquid if finer). Content sections need `"presets"`; main template sections (product, collection, cart, search, 404, customers, password, policy) have NO presets.
5. **Never** `"default": ""` (empty string) on any setting — Shopify silently rejects the file. Omit the default instead.
6. **Storefront text** = `{{ 'key' | t }}` from `locales/en.default.json` (read it; add keys if missing — report them). Merchant-editable text = schema settings with English defaults. Apostrophes in Liquid single-quoted strings: use ’ (U+2019), never '.
7. **Liquid limits**: no parentheses/ternaries in conditions; `contains` = strings only; `for` ≤ 50 items → `{% paginate %}`; `{% render %}` only (no `include`); snippets get all data via params; snippets start with `{% doc %}`.
8. **JS**: native only, zero dependencies, custom elements `<fl-*>` defined in `{% javascript %}`. Guard `customElements.define` with `if (!customElements.get(...))`. Re-init safe for the theme editor (`shopify:section:load`). Respect `prefers-reduced-motion`.
9. **A11y**: visible focus (`:focus-visible` inherited), 44px min targets, ARIA on drawers/dialogs (`aria-expanded`, `aria-controls`, focus trap + ESC on modals), `aria-live="polite"` on dynamic updates (cart count, form status), alt text from Liquid objects, one `<h1>` per page (main sections only), buttons vs links used correctly.
10. **Images**: `image_url` + `image_tag` with `widths` and `sizes`, `loading: 'lazy'` below the fold. Placeholders via `placeholder_svg_tag` when empty so sections preview nicely in the editor.

## JS contract (cart)

- Add-to-cart forms carry `data-quick-add` (cards) or `data-product-form` (product page).
- The cart drawer section (`sections/cart-drawer.liquid`, statically rendered from theme.liquid when `settings.cart_type == 'drawer'`) intercepts submits of those forms, POSTs to `routes.cart_add_url` with `Accept: application/javascript`, re-renders itself via Section Rendering API (`?sections=cart-drawer`), opens, and dispatches `document` event **`fl:cart:change`** with `detail: { itemCount }`.
- Header displays the count in `[data-cart-count]` and listens for `fl:cart:change`. Elements with `data-cart-open` open the drawer (fallback: plain link to `routes.cart_url` — everything must work without JS).
- When `settings.cart_type == 'page'`, no drawer is rendered; forms submit natively.

## Validation (mandatory before reporting done)

```bash
export OPT_OUT_INSTRUMENTATION=true
cd ~/Desktop/Claude.code/liquid-tools/validator
node scripts/validate.mjs --theme-path ~/Desktop/Claude.code/flyer-theme --files "sections/<file>.liquid"
```

Zero offenses required. theme-check does not catch everything (nested `{% stylesheet %}`, schema name > 25 chars, empty-string defaults) — respect the rules above regardless.
