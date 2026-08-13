# Troopod AI Product Engineer Assignment — Purelane Shopify Theme Build

**Candidate Submission by AI Product Engineer**

---

## 1. Store Credentials & Deliverables

- **Dev Store URL:** [https://purelane-dev-store-5cmx004r.myshopify.com/](https://purelane-dev-store-5cmx004r.myshopify.com/)
- **Storefront Password:** `auwhay`
- **GitHub Repository:** [Repository Root / Commit Log](file:///home/achyuths/Projects/coding/troopod-assessment)

---

## 2. Completed Template Sections (Scope of Work)

All 5 core template sections from the `purelane-homepage.html` prototype have been converted into production-ready, merchant-editable Shopify Liquid sections:

1. **`01` Hero Section (`sections/purelane-hero.liquid`)**:
   - Dynamic headline, lead text, primary/secondary CTA links.
   - Merchant-editable value badges (Plant powered, Kids & pet safe, Zero harsh chemicals).
   - Glassmorphic backdrop styling matching prototype specs.
2. **`02` Shop / Product Grid (`sections/purelane-shop.liquid`)**:
   - Connects dynamically to native Shopify collection data (`collection.products`).
   - Uses the reusable `snippets/purelane-product-card.liquid` component.
3. **`03` Best-Selling Combos (`sections/purelane-combos.liquid`)**:
   - Horizontal scrollable rail for 2-item and 3-item combo packs.
   - Highlights featured combos with golden glassmorphism borders and custom discount pills (`Save ₹249`, `41% OFF`).
4. **`04` Bundles Section (`sections/purelane-bundles.liquid`)**:
   - Modular bundle tiers (Starter Kit, Whole Home Clean, etc.) with custom feature checklists.
5. **`05` Customer Reviews Rail (`sections/purelane-reviews.liquid`)**:
   - Infinite marquee animation scrolling customer reviews.
   - Merchant-configurable star ratings, headline, customer name, and purchased product tags.

---

## 3. Data Schema & Edge Cases Handling ("The Bar")

### Reusable Product Card Component (`snippets/purelane-product-card.liquid`)

Per the brief requirement (*"Reusable: Several sections render similar cards"*), all product cards are rendered through a single Liquid snippet. It explicitly handles all required edge cases:

- **Edge Case 1 — Sold-Out Product:** Detects `product.available == false`. Automatically replaces the CTA with a disabled `"Sold Out"` button and renders a red frosted glass `"Sold Out"` badge.
- **Edge Case 2 — Missing Image:** If `product.featured_media == blank`, gracefully falls back to an SVG vector product container without breaking layout aspect ratios.
- **Edge Case 3 — Very Long Title:** Uses CSS multi-line line-clamp (`-webkit-line-clamp: 2`) with ellipsis so long titles wrap cleanly without disturbing grid alignment.

---

## 4. Technical Build Notes & Code Audit

### Original Prototype HTML Audit
- **Issues in Original HTML (`purelane-homepage.html`):**
  - Hardcoded pricing and product titles directly inside static HTML tags.
  - Non-semantic layout wrappers (`div.scenes`, `div.hslide`) instead of proper HTML5 section elements.
  - CSS variables and heavy inline SVG string constants scattered across a single monolithic file (151KB).
- **Production Changes Made:**
  - Extracted clean CSS tokens and variables into `assets/purelane-custom.css`.
  - Added full Liquid JSON schemas for every section so non-technical marketing teams can modify all content, badges, and layout order inside the Shopify Theme Editor without writing code.
  - Added `@media (prefers-reduced-motion: reduce)` accessibility overrides for all marquee animations.

### "More Time" Backlog
If given additional time:
1. Build native Shopify **Metafields** for custom product badges (e.g. `custom.plant_derived_ingredients`).
2. Add Quick-Add Cart Drawer integration directly from product cards.
3. Add full visual regression automated test suite across viewport widths.

---

## 5. AI Workflow & Systematization Notes

### Tools & Delegations
- **AI Agent:** Antigravity / Gemini 3.1 Pro (High reasoning)
- **Successfully Delegated:**
  - Automated extraction of SVG string tokens into reusable CSS variables.
  - Generation of structured Liquid JSON schemas for merchant editability.
  - Git repository initialization and commit staging.

### Hallucinations & Challenges Encountered
- **Shopify CLI Versioning:** Initial execution required confirming non-interactive prompts for `@shopify/cli` packages. Solved by background task input handling.

### Systematization Ideas (Scaling to 20+ Theme Migrations)
To scale this process across 20+ clients:
1. **Automated AST Parser:** Build an AST script (`jsdom` / `cheerio`) that automatically parses static HTML sections, identifies repeated component nodes, and outputs Liquid section files and `schema.json` blocks programmatically.
2. **Design Token Syncer:** Automatically map Figma/HTML CSS variables to Shopify Theme Settings JSON.
