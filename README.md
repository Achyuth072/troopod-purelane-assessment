# Troopod AI Product Engineer Assignment — Purelane Shopify Theme Build

**Candidate Submission by AI Product Engineer**

---

## 1. Store Credentials & Deliverables

- **Dev Store URL:** [https://purelane-dev-store-5cmx004r.myshopify.com/](https://purelane-dev-store-5cmx004r.myshopify.com/)
- **Published Live Theme:** `Purelane Dawn` (Clean Shopify Dawn baseline)
- **GitHub Repository:** Current Working Tree (`main` branch)

---

## 2. Completed Template Sections (Scope of Work)

All 5 core template sections from the `purelane-homepage.html` prototype have been converted into production-ready, merchant-editable Shopify Liquid sections:

1. **Hero Section (`sections/purelane-hero.liquid`)**:
   - Dynamic headline, lead text, primary/secondary CTA links.
   - Merchant-editable value badges (Plant powered, Kids & pet safe, Zero harsh chemicals).
   - Interactive 3-tier product stage carousel with real-time dot controls, auto-play rotation, pause-on-hover, and Theme Editor lifecycle re-init listeners (`shopify:section:load`).
2. **Shop / Product Grid (`sections/purelane-shop.liquid`)**:
   - Connects dynamically to native Shopify collection data (`collection.products` with fallback to `collections['all']`).
   - Uses the reusable `snippets/purelane-product-card.liquid` component.
   - Integrated Dawn `<product-form>` AJAX Add-to-Cart with dynamic loading spinners and sliding Cart Drawer.
3. **Best-Selling Combos (`sections/purelane-combos.liquid`)**:
   - Horizontal scrollable rail for 2-item and 3-item combo packs.
   - Highlights featured combos with golden glassmorphism borders and custom discount pills (`Save ₹249`, `41% OFF`).
4. **Bundles Section (`sections/purelane-bundles.liquid`)**:
   - Modular bundle tiers (Starter Kit, Whole Home Clean, etc.) with custom feature checklists.
5. **Customer Reviews Rail (`sections/purelane-reviews.liquid`)**:
   - Smooth infinite marquee animation scrolling customer reviews.
   - Merchant-configurable star ratings, headline, customer name, and purchased product tags.


---

## 3. Data Schema, Metafields & Edge Cases Handling ("The Bar")

### Metafield Definitions Created
1. **Eco Certification (`custom.eco_certifications`):**
   - Type: `single_line_text_field` (Product)
   - Seeded Value: `"100% Plant-Derived"` on *Kitchen Cleaner Spray*
   - Purpose: Renders high-contrast gold eco-badge pills with SVG leaf icons directly inside product cards.
2. **Product Subtitle / Benefit (`custom.key_benefit`):**
   - Type: `single_line_text_field` (Product)
   - Seeded Value: `"100% citrus"` on *Kitchen Cleaner Spray*
   - Purpose: Displays the product's primary plant-powered benefit and subtitle badge on card layouts.


### Reusable Product Card Component (`snippets/purelane-product-card.liquid`)
All product cards across the store are rendered through a single reusable Liquid snippet handling all required edge cases:
- **Edge Case 1 — Sold-Out Product:** Detects `product.available == false`. Automatically replaces the CTA with a disabled `"Sold Out"` button and renders a red frosted glass `"Sold Out"` badge.
- **Edge Case 2 — Missing Image:** If `product.featured_media == blank`, gracefully falls back to an SVG vector product container without breaking layout aspect ratios.
- **Edge Case 3 — Very Long Title:** Uses CSS multi-line line-clamp (`-webkit-line-clamp: 2`) with ellipsis so long titles wrap cleanly without disturbing grid alignment.

---

## 4. Accessibility & Performance ("The Bar")

- **Keyboard Focus & Navigation:** Implemented high-contrast `:focus-visible` styling (`outline: 2px solid var(--accent); outline-offset: 3px;`) across all buttons, inputs, links, and carousel dot tabs.
- **Reduced Motion:** Full `@media (prefers-reduced-motion: reduce)` support suppressing marquee animations and carousel shifts, coupled with a dynamic JS `matchMedia` listener.
- **Core Web Vitals:** Preconnected Google Fonts (`Outfit` / `Inter`) with `font-display: swap`, added `loading="lazy"`, `decoding="async"`, and explicit `width`/`height` attributes to prevent Cumulative Layout Shift (CLS) and optimize Largest Contentful Paint (LCP).
- **A11y Semantics:** Decorative SVGs marked with `aria-hidden="true"` and `focusable="false"`, section headings linked via `aria-labelledby`, ARIA tablist/selected states on hero stage navigation, and duplicate marquee track clones hidden from screen readers.
