# GitHub Profile README Redesign

**Date:** 2026-03-27
**Goal:** Redesign the 73nko GitHub profile README to look professional, showcase stats, and demonstrate frontend/design skills with a "wow" factor.

## Design Direction

- **Aesthetic:** Dark with gradients (Linear/Vercel/Raycast vibes)
- **Base background:** `#0d1117` (GitHub dark)
- **Accent:** Gradient border — purple → blue → teal
- **Typography:** Clean, minimal, white text with muted grey for secondary content
- **Approach:** Full custom SVG — all sections are hand-crafted SVGs with CSS animations for maximum cohesion and to demonstrate FE craftsmanship

## Sections

### 1. Hero — Figma-style Component Card (custom SVG)

A custom animated SVG that looks like a Figma/design-system component inspector card.

- **Window chrome:** Dark rounded rectangle (`#0d1117` background) with a gradient border (purple → blue → teal)
- **Top bar:** "Component" label with a Figma diamond icon and the name `<AlexPerez />`
- **Left panel — "Preview":** Profile image in a circle, name and title ("Senior Software Engineer") below
- **Right panel — "Props":** Property inspector table:
  - `company`: "Awtomic (YC S20)"
  - `prev`: "Eventbrite"
  - `stack`: ["TypeScript", "React", "Rust"]
- **Bottom bar:** Social link icon buttons (email, LinkedIn, X)
- **Animation:** Blinking cursor next to `<AlexPerez />`, subtle gradient shimmer looping across the border

### 2. Currently Building (custom SVG card)

A smaller card in the same dark style.

- **Same gradient border** as hero but thinner
- **Layout:** Horizontal — Awtomic logo/icon left, text right
- **Content:**
  - "Currently Building" muted grey label
  - **Awtomic** — bold, white
  - "Subscription platform for Shopify brands" — muted grey description
  - "YC S20" badge pill with amber accent
- **No animation** — keeps focus on the hero

### 3. Tech Stack Icons (custom SVG strip)

- **Layout:** Horizontal centered row of technology icons
- **Style:** Monochrome white/grey icons with subtle gradient accent glow underneath each
- **Technologies:** TypeScript, React, Node.js, Rust, Next.js, GraphQL
- **Spacing:** Generous gaps, no labels — icons speak for themselves

### 4. GitHub Stats (existing cards, re-themed)

- **Theme:** Switch from `nord_dark` to `github_dark` to match the `#0d1117` background
- **Layout preserved:**
  - 3 cards in a row (32.5% width each): Stats, repos per language, most commit language
  - Full-width profile details card below

## Files to Create/Modify

- `img/hero-card.svg` — the Figma-style component card (animated)
- `img/currently-building.svg` — the currently building card
- `img/tech-stack.svg` — the tech stack icon strip
- `README.md` — rewritten to reference the new SVGs and re-themed stats cards

## Out of Scope

- Open source / projects showcase section
- GitHub Actions for dynamic content
- External service dependencies (beyond existing GitHub profile summary cards)
