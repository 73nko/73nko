# GitHub Profile README Redesign — Sunset Pool Splash

## Goal

Redesign the GitHub profile README (`73nko/73nko`) to match the "Sunset · Pool Splash" style guide. Consolidate three SVG cards into one hero card, keep existing GitHub stats cards unchanged.

## Style Guide Tokens (reference)

| Token           | Value       | Role                              |
| --------------- | ----------- | --------------------------------- |
| dusk            | `#1A0A28`   | Card background                   |
| magenta         | `#FF3D8A`   | Section numbers, keywords         |
| magenta-hi      | `#FFB8D5`   | Bold/highlighted names            |
| tangerine       | `#FF8A3D`   | Functions, accents                |
| turquoise-hi    | `#7FE0EB`   | Eyebrow, pills, structural       |
| aqua            | `#8FE3E8`   | Types, quieter blue               |
| rosegold        | `#FFC6A0`   | Default foreground text           |
| gold            | `#FFD67A`   | Numbers, booleans                 |
| inkLine         | `rgba(255,198,160,0.14)` | Card border             |
| ink             | `#1F1630`   | Surface background                |

## Deliverables

1. **`img/hero-card.svg`** — new hero card (replaces old hero-card, currently-building, and tech-stack)
2. **`README.md`** — updated to reference single hero card + existing GitHub stats
3. **Delete** `img/currently-building.svg` and `img/tech-stack.svg`

## Hero Card Design

### Dimensions & Frame

- **Width:** 840px, **Height:** ~280px
- **Background:** solid `#1A0A28` (dusk)
- **Border radius:** 14px
- **Border:** 1px `rgba(255,198,160,0.14)` (inkLine)
- **Top accent stripe:** 3px gradient across the full top edge — `#FF3D8A` (magenta) left, `#FF8A3D` (tangerine) center, `#7FE0EB` (turquoise-hi) right. Sits inside the border radius.

### Content Layout

**Top-right corner:**
- Section number `01` in magenta `#FF3D8A`, JetBrains Mono, 11px, letter-spacing 2px

**Top-left area (y ~50-60):**
- Eyebrow: `SENIOR SOFTWARE ENGINEER` in JetBrains Mono, 11px, uppercase, letter-spacing 2px, color `#7FE0EB` (turquoise-hi)

**Below eyebrow (y ~90-110):**
- Name: `Alex Pérez` in Inter/sans-serif, 36-40px, font-weight 800, gradient fill using linearGradient: magenta-hi `#FFB8D5` 0%, magenta `#FF3D8A` 30%, tangerine `#FF8A3D` 55%, turquoise-hi `#7FE0EB` 95%

**Below name (y ~140-150):**
- Tagline: "Building subscriptions at **Awtomic** (YC S20) · Previously **Eventbrite**"
- Base text: rosegold `#FFC6A0`, 14px, opacity 0.88
- Bold words ("Awtomic", "Eventbrite"): magenta-hi `#FFB8D5`, font-weight 600

**Bottom-left area (y ~190-210):**
- Tech stack pills in a horizontal row, 10-12px gap between pills
- Each pill: `rgba(127,224,235,0.08)` background, 1px `rgba(127,224,235,0.22)` border, rounded 999px (full pill shape), horizontal padding ~10px, vertical padding ~4px
- Pill text: turquoise-hi `#7FE0EB`, JetBrains Mono, 11px
- Technologies: TypeScript, React, Rust, Next.js, Node.js, GraphQL

**Bottom-right area (y ~190-210):**
- Social icons: email (envelope), LinkedIn, X/Twitter
- Icon color: `rgba(255,198,160,0.6)` (muted rosegold)
- Size: ~16px, spaced 20px apart

### Fonts in SVG

SVGs on GitHub can't load external fonts. Use system font stacks:
- Headings/body: `'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`
- Monospace (eyebrow, pills, section number): `'JetBrains Mono', 'SF Mono', 'Cascadia Code', monospace`

Note: Inter and JetBrains Mono won't render for users who don't have them installed. The fallbacks will handle this gracefully.

### Animations

- Optional: shimmer animation on the top gradient stripe (stroke-dasharray trick from current hero card). Keep it subtle.
- Blinking cursor removed (doesn't fit the new aesthetic).

## README Structure

```markdown
<div align="center">
  <img src="./img/hero-card.svg" alt="Alex Pérez — Senior Software Engineer" width="840" />
</div>

<br />

<div align="center">
  <a href="https://github.com/73nko">
    <img src="https://raw.githubusercontent.com/73nko/github-profile-summary-cards/master/profile-summary-card-output/github_dark/3-stats.svg" width="32.5%" />
    <img src="https://raw.githubusercontent.com/73nko/github-profile-summary-cards/master/profile-summary-card-output/github_dark/1-repos-per-language.svg" width="32.5%" />
    <img src="https://raw.githubusercontent.com/73nko/github-profile-summary-cards/master/profile-summary-card-output/github_dark/2-most-commit-language.svg" width="32.5%" />
  </a>
</div>

<br />

<div align="center">
  <img src="https://raw.githubusercontent.com/73nko/github-profile-summary-cards/master/profile-summary-card-output/github_dark/0-profile-details.svg" />
</div>
```

## Files to Delete

- `img/currently-building.svg`
- `img/tech-stack.svg`

## Out of Scope

- Changing the GitHub stats card theme (kept as `github_dark`)
- Profile photo (explicitly removed)
- Any server-side or dynamic content
