# Saiko

> The independent beauty price index for India.

Saiko is a price-comparison engine for cosmetics — a Skyscanner for beauty. It pulls live prices across 240+ retailers (Nykaa, Tira, Sephora India, Cult Beauty, Lookfantastic, brand-direct stores, and more), folds in shipping, taxes, and active discount codes, and surfaces the real number you'd pay at checkout.

This repository contains the marketing site and product landing page — a single self-contained HTML prototype demonstrating the full user experience.

---

## Live demo

Open `saiko.html` in any modern browser. No build step, no dependencies beyond a Google Fonts CDN call.

```bash
# macOS
open saiko.html

# Linux
xdg-open saiko.html

# Or just drag the file into your browser
```

---

## What's in the prototype

The single-page prototype demonstrates the full Saiko experience end-to-end:

**Hero & search.** A tool-led landing surface with the search card as the primary element — three input modes (search, paste a link, browse by category), four filter fields (product, category, max budget, action), and trending product chips for one-click queries. A live price ticker scrolls underneath showing real-time deal movement across the index.

**Live comparisons.** Four sample products demonstrate the core comparison pattern — Charlotte Tilbury Pillow Talk, La Roche-Posay Anthelios SPF, Sol de Janeiro Bum Bum Cream, and Olaplex No. 3. Each opens to reveal a full retailer table with stock status, shipping cost, perks, discount codes, side-by-side prices, and a "Best" highlight on the cheapest verified seller.

**Trending categories.** Eight category tiles with custom illustrations, live product counts, and "from ₹" pricing — refreshed every six hours from search and click activity.

**This week's drops.** A numbered leaderboard of the eight biggest verified price drops, with strike-through pricing and the active retailer attached to each.

**Price-drop alerts.** A dark-mode footer section with email signup and three feature blurbs explaining wishlist tracking, target prices, and pre-sale leaks.

---

## Design system

Saiko uses a warm editorial palette inspired by the "modern beauty boutique" direction — Aesop, Necessaire, Glow Recipe — refined for tool-first density.

### Palette

| Token       | Hex       | Usage                                |
|-------------|-----------|--------------------------------------|
| Bone        | `#FAF6F0` | Primary background                   |
| Bone 2      | `#F4ECDD` | Secondary surfaces, image fills      |
| Bone 3      | `#EBE0CB` | Tertiary fills                       |
| Caramel     | `#C7956D` | Accent, decorative gradients         |
| Caramel deep| `#A87850` | Eyebrow text, brand label            |
| Brick       | `#B85C57` | Display italic, primary highlights   |
| Brick deep  | `#8E433F` | Hover states                         |
| Sage        | `#5C6B4F` | Stock-in indicator, positive signals |
| Sage deep   | `#3F4B36` | Savings text                         |
| Cocoa       | `#2B1810` | Primary text, dark sections          |
| Ink dim     | `#6B5A47` | Secondary text                       |
| Ink faint   | `#8B7558` | Tertiary text, disabled              |

### Typography

| Family            | Use                                          |
|-------------------|----------------------------------------------|
| Fraunces          | Display headings, italic accents, brand name |
| Inter             | Body text, UI controls                       |
| JetBrains Mono    | Eyebrows, labels, technical metadata         |

Display sizes scale from `clamp(32px, 4vw, 52px)` for section heads up to `clamp(44px, 6.5vw, 86px)` for the main hero. Body copy holds at 15–17px depending on context.

### Components

The prototype includes production-shape implementations of:

- Sticky topbar with logo, centered nav, and login button
- Search card with tabs, fields, and quick-pick chips
- Live ticker with continuous horizontal scroll
- Expandable product cards with retailer comparison tables
- Retailer logo system (32×32 SVG monograms for each store)
- Stock status pills with color-coded indicators
- Discount code chips and perk badges
- Drop leaderboard with Roman numeral ranking
- Modal system (login)
- Image lightbox with zoom-on-click
- Mobile drawer with backdrop
- Loading bar with shimmer animation and stage-by-stage status

---

## Features

### Login

Top-right login button opens a modal with email/password fields plus Google and Apple SSO options. The mobile drawer also includes a "Log in" link for thumb-reachable access.

### Image lightbox

Hover any product image to reveal a zoom hint icon. Click to open a fullscreen lightbox with the product illustration scaled up, plus brand, name, and metadata. Closes via the × button, clicking outside, or pressing Escape.

### New tab + loading state

Triggering a search (button click, Enter key, or quick-chip tap) or expanding a product card opens results in a new tab and shows a stage-by-stage loading bar above the listings in the current tab. The bar runs through five stages with realistic timing:

1. Querying retailer index
2. Fetching prices
3. Calculating shipping & active codes
4. Verifying stock & authenticity
5. Sorting by best price

### Mobile-first responsive

- **Below 1024px:** topbar collapses to logo + hamburger + login icon, search fields stack, comparison tables hide secondary columns
- **Below 768px:** retailer tables convert from rows to stacked cards (every retailer becomes a self-contained card with logo, name, stock, shipping, perks, price, and CTA)
- **Below 380px:** type sizes step down further for narrow phones

### Keyboard support

- `Escape` closes any open modal, lightbox, or drawer
- `Enter` in the search field triggers a search
- All interactive elements are keyboard-focusable

---

## Project structure

```
.
├── saiko.html         # The complete prototype — HTML, CSS, JS in one file
└── README.md          # This file
```

The prototype is intentionally a single file. For a production codebase you'd split this into a Next.js or Astro app with components, a real search index, retailer crawlers, and a database — see "Roadmap" below.

---

## Brand

**Name:** Saiko
**Wordmark:** Fraunces italic, set in cocoa (`#2B1810`)
**Tagline:** *Every shade. Every retailer. One honest price.*

The brand voice is editorial and confident — adjacent to a beauty magazine, not a coupon site. Copy stays direct, free of cringe slang, and trusts the reader to want a clear answer over a hyped one. Trend signals and category pages get a touch of warmth; the comparison engine itself stays clinical.

---

## How Saiko makes money (proposed)

Saiko does **not** take a cut from the retailer when a user clicks through. The price the user sees is the price the user pays. Revenue comes from:

1. **Retailer subscriptions** — featured placement, analytics dashboards, restock alerts to retailers when their competitors run out
2. **Brand intelligence** — anonymized pricing data sold to brands to help them spot grey-market activity and retailer pricing violations
3. **Affiliate links to brand-direct stores only** — when buying direct from the brand wins, that's a clean affiliate link with no markup; when a third-party retailer wins, it's a clean unaffiliated link

This protects the integrity of the comparison — Saiko has no incentive to surface a more expensive retailer.

---

## Roadmap

A non-exhaustive list of what would come next if this graduated from prototype to product:

**Search & discovery**
- Real product search index with shade/size variant matching
- Image search ("find this lipstick from a screenshot")
- Dupe finder powered by ingredient overlap
- Routine builder with bundled price comparison

**Comparison engine**
- True checkout-cost calculation with live tax/customs lookup
- Active code validation (test codes against retailer carts every 4 hours)
- Authentic stock verification (batch code check against brand databases)
- Shade-level pricing where retailers vary by shade

**User accounts**
- Wishlist with target-price alerts
- Price history charts per product
- "Notify when in stock" for sold-out products
- Pre-sale leak notifications 12 hours before public launch

**Editorial layer**
- Weekly drops newsletter
- Category guides with comparison embeds
- Brand-direct vs retailer breakdowns
- Authenticator partner integrations

**Retailer coverage (India launch)**
- Tier 1: Nykaa, Tira, Sephora India, Myntra Beauty, Tata CLiQ Luxury
- Tier 2: Smytten, Purplle, Boddess, Foxy, Shoppers Stop Beauty
- Brand-direct: Charlotte Tilbury, MAC, Estée Lauder, Clinique, La Mer, Dior Beauty, YSL Beauty, Maison Margiela, Sol de Janeiro, Rare Beauty, Olaplex, Drunk Elephant, La Roche-Posay
- International with India shipping: Cult Beauty, Lookfantastic, Selfridges, Space NK

---

## Tech notes

The prototype uses zero frameworks deliberately — every interaction is hand-written so it's easy to lift patterns into whatever stack you choose. Some specifics worth flagging:

- **Custom SVG illustrations** for product images and retailer logos. Each is hand-coded as inline SVG with brand-correct colors, gradients, and typography. They render crisp at every size including the 3x lightbox view.
- **CSS Grid + Flex** throughout. No layout libraries.
- **IntersectionObserver** drives the reveal-on-scroll animations.
- **No browser storage** is used (no `localStorage`, no `sessionStorage`) — all state is in-memory React-style via vanilla JS variables. Wishlist persistence would arrive with the real account system.
- **Google Fonts CDN** is the only external dependency. Replace with self-hosted woff2 if you need offline-first.

---

## Browser support

| Browser           | Tested |
|-------------------|--------|
| Chrome / Edge 100+ | ✓      |
| Safari 15+         | ✓      |
| Firefox 100+       | ✓      |
| Mobile Safari iOS 15+ | ✓   |
| Chrome Android        | ✓   |

`backdrop-filter` is used for the modal/lightbox blur — degrades gracefully to a solid overlay on browsers without support.

---

## License

This prototype is shared as a design and code reference. The Saiko name, wordmark, and brand identity are not licensed for reuse. Code patterns, layouts, and design system tokens are free to learn from and adapt.

---

## Credits

- Brand direction: Saiko team
- Type: Fraunces (Undercase Type), Inter (Rasmus Andersson), JetBrains Mono (JetBrains)
- Sample products are real but pricing is illustrative and was accurate at time of prototype build
- Retailer logos are simplified monogram representations — not official brand assets
