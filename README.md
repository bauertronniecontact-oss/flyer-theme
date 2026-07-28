# FLYER

A free Shopify theme by **[KIOSK](https://kioskthemes.com)** — clean, minimal and fast. Built on Online Store 2.0 with fully autonomous sections.

**[kioskthemes.com](https://kioskthemes.com)** · [Browse all themes](https://kioskthemes.com) · [Support](https://kioskthemes.com/support/)

- **Version**: 1.0.0
- **Author**: KIOSK
- **License**: see [LICENSE.md](LICENSE.md)

## What's inside

Everything a store needs, nothing it doesn't:

| Area | Sections |
| --- | --- |
| Storefront | image banner, featured collection, image with text, multicolumn, rich text, newsletter, custom Liquid |
| Shopping | product page with block-based layout, collection with filters and sorting, cart drawer, cart page, predictive search |
| Content | blog, article with comments, page, contact form, policies |
| Account | login, register, password reset, activation, order history, addresses, order detail |
| Chrome | header with dropdown navigation, announcement bar, footer, 404, password page |

## Design tokens

Colors, typography, spacing, corner radii and product-card ratios are all editable in **Theme settings** and applied through CSS custom properties. Nothing is hardcoded — see [docs/DESIGN.md](docs/DESIGN.md) for the full token table and the section authoring contract.

## Development

```bash
shopify theme dev --store your-store
```

Every push runs `theme-check` in CI.

## Structure

Each section is self-contained: its own `{% schema %}`, styles and JavaScript. Add, remove or reorder sections in the theme editor without breaking anything. JavaScript is native and dependency-free; the storefront works without it.
