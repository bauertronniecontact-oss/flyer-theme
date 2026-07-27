# FLYER

Free Shopify theme by [KIOSK](https://kioskthemes.com). Clean, minimal, fast — built on Online Store 2.0 with fully autonomous sections.

- **Version**: 1.0.0
- **Author**: KIOSK — kioskthemes.com
- **Support**: https://kioskthemes.com/support/

## Structure

Every section is self-contained: its own `{% schema %}`, styles and JS. Add, remove or reorder sections freely in the theme editor without breaking anything.

Design tokens (colors, typography, spacing, radii) are editable in **Theme settings** and applied through CSS custom properties — see [docs/DESIGN.md](docs/DESIGN.md).

## Development

```bash
shopify theme dev --store <your-store>
```

Validation: `theme-check` (CI runs it on every push).

## License

See [LICENSE.md](LICENSE.md).
