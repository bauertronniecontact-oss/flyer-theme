# Changelog

## 1.4.0 — 2026-08-20

### Added
- Payment method logos in the footer, taken from the methods your store
  actually accepts. New setting: **Show payment method logos**.
- Unit price on the product page and on product cards — required in the EU
  (Directive 98/6/EC) for anything sold by weight, volume or length. It appears
  only when you have set a unit of measure on the variant, and follows the
  selected variant.
- Complementary product recommendations. The product recommendations section
  now has a **Recommendation type** setting — *Related* (automatic) or
  *Complementary*, the ones you pair by hand in the free Shopify Search &
  Discovery app. Add the section twice to show both.

### Added
- The product recommendations section can now be added from the editor, and
  only on the product template. It had no preset, so a second instance — the one
  you need for complementary products — could not be added at all.

## 1.3.0 — 2026-08-20

### Added
- Shop Pay Installments banner on the product page, shown automatically when
  the store is eligible.
- New setting, **Show express payment buttons**, on both the product and
  featured product sections, enabled by default. The express buttons
  themselves shipped in 1.2.0; they can now be turned off.

## 1.2.0 — 2026-08-11

First public release.

### Added
- Colour schemes: five editable schemes, selectable per section.
- 130 theme settings across 21 groups — typography, layout, animations,
  buttons, inputs, variant pills, product/collection/blog cards, content
  containers, media, popups, drawers, badges, brand information, search,
  currency format, cart.
- 22 addable sections, including slideshow, video, collage, multirow,
  collapsible content, collection list, featured blog, featured product,
  email signup banner, page content, quick order list, and app blocks.
- Scroll reveal, configurable hover effect, LCP-aware image loading on the
  first row of product grids.

### Fixed
- Variant selection now posts correctly with JavaScript disabled: a `noscript`
  select carries the variant id, so the chosen variant is what reaches the cart.
- Product pages show the price of the selected variant, not the product minimum.
- Slideshow set to "adapt to first image" no longer exceeds the viewport width
  on phones.
- Secondary text and control borders stay above WCAG AA contrast on every
  shipped colour scheme.
- Shadow colour follows the active colour scheme instead of the first one.
- Price filter no longer multiplies values by 100 in comma-decimal currencies.
- Cart drawer refreshes after a bulk add, and the "Added to cart" confirmation
  stays visible.
- Product card buttons align across a row regardless of title length.

### Notes
- No external dependencies, no tracking, no CDN calls.
- Every purchase path works without JavaScript.
