# GitHub Profile Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Redesign the GitHub profile README to match the Sunset · Pool Splash style guide, consolidating three SVG cards into one hero card.

**Architecture:** Single SVG hero card built with inline styles (GitHub strips external CSS). All colors from the style guide token reference. README simplified to hero card + existing GitHub stats cards.

**Tech Stack:** SVG, Markdown

**Spec:** `docs/superpowers/specs/2026-04-22-profile-redesign-design.md`

---

### File Structure

| Action | Path | Responsibility |
| ------ | ---- | -------------- |
| Rewrite | `img/hero-card.svg` | New hero card with Sunset · Pool Splash styling |
| Rewrite | `README.md` | Updated layout: hero card + GitHub stats |
| Delete | `img/currently-building.svg` | No longer needed |
| Delete | `img/tech-stack.svg` | No longer needed |

---

### Task 1: Build the hero card SVG

**Files:**
- Rewrite: `img/hero-card.svg`

- [ ] **Step 1: Create the SVG frame**

Write the outer SVG element, defs (gradients, animations), background rect, border, and top accent stripe.

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 840 280" width="840">
  <defs>
    <!-- Title gradient: magenta-hi → magenta → tangerine → turquoise-hi -->
    <linearGradient id="titleGrad" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#FFB8D5"/>
      <stop offset="30%" stop-color="#FF3D8A"/>
      <stop offset="55%" stop-color="#FF8A3D"/>
      <stop offset="95%" stop-color="#7FE0EB"/>
    </linearGradient>
    <!-- Top accent stripe gradient -->
    <linearGradient id="accentGrad" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#FF3D8A"/>
      <stop offset="50%" stop-color="#FF8A3D"/>
      <stop offset="100%" stop-color="#7FE0EB"/>
    </linearGradient>
    <!-- Clip for top stripe inside rounded rect -->
    <clipPath id="cardClip">
      <rect x="0" y="0" width="840" height="280" rx="14" ry="14"/>
    </clipPath>
  </defs>

  <!-- Background -->
  <rect x="0" y="0" width="840" height="280" rx="14" ry="14" fill="#1A0A28"/>

  <!-- Border -->
  <rect x="0.5" y="0.5" width="839" height="279" rx="14" ry="14"
        fill="none" stroke="rgba(255,198,160,0.14)" stroke-width="1"/>

  <!-- Top accent stripe (3px, clipped to card radius) -->
  <rect x="0" y="0" width="840" height="3" fill="url(#accentGrad)"
        clip-path="url(#cardClip)"/>
</svg>
```

- [ ] **Step 2: Add the section number and eyebrow**

Inside the SVG, after the background elements, add the `01` section number (top-right) and the eyebrow label (top-left).

```xml
  <!-- Section number -->
  <text x="800" y="40" fill="#FF3D8A"
        font-family="'JetBrains Mono','SF Mono','Cascadia Code',monospace"
        font-size="11" font-weight="500" letter-spacing="2" text-anchor="end">01</text>

  <!-- Eyebrow -->
  <text x="40" y="44" fill="#7FE0EB"
        font-family="'JetBrains Mono','SF Mono','Cascadia Code',monospace"
        font-size="11" font-weight="500" letter-spacing="2">SENIOR SOFTWARE ENGINEER</text>
```

- [ ] **Step 3: Add the name with gradient fill**

```xml
  <!-- Name -->
  <text x="40" y="96" fill="url(#titleGrad)"
        font-family="'Inter',-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif"
        font-size="40" font-weight="800" letter-spacing="-1">Alex P&#233;rez</text>
```

- [ ] **Step 4: Add the tagline**

Two tspan elements for the tagline — base rosegold, bold names in magenta-hi.

```xml
  <!-- Tagline -->
  <text x="40" y="132"
        font-family="'Inter',-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif"
        font-size="14" fill="#FFC6A0" opacity="0.88">
    <tspan>Building subscriptions at </tspan>
    <tspan fill="#FFB8D5" font-weight="600">Awtomic</tspan>
    <tspan> (YC S20) &#183; Previously </tspan>
    <tspan fill="#FFB8D5" font-weight="600">Eventbrite</tspan>
  </text>
```

- [ ] **Step 5: Add tech stack pills**

Each pill is a `<rect>` + `<text>` pair. Position them in a horizontal row starting at y ~185. Calculate x positions based on approximate text widths (pill padding ~10px each side).

Approximate pill widths (text + 20px padding): TypeScript ~90px, React ~60px, Rust ~50px, Next.js ~65px, Node.js ~65px, GraphQL ~72px. Gap between pills: 10px.

```xml
  <!-- Tech stack pills -->
  <!-- TypeScript -->
  <rect x="40" y="170" width="90" height="26" rx="13" fill="rgba(127,224,235,0.08)"
        stroke="rgba(127,224,235,0.22)" stroke-width="1"/>
  <text x="85" y="187" text-anchor="middle" fill="#7FE0EB"
        font-family="'JetBrains Mono','SF Mono','Cascadia Code',monospace"
        font-size="11">TypeScript</text>

  <!-- React -->
  <rect x="140" y="170" width="60" height="26" rx="13" fill="rgba(127,224,235,0.08)"
        stroke="rgba(127,224,235,0.22)" stroke-width="1"/>
  <text x="170" y="187" text-anchor="middle" fill="#7FE0EB"
        font-family="'JetBrains Mono','SF Mono','Cascadia Code',monospace"
        font-size="11">React</text>

  <!-- Rust -->
  <rect x="210" y="170" width="50" height="26" rx="13" fill="rgba(127,224,235,0.08)"
        stroke="rgba(127,224,235,0.22)" stroke-width="1"/>
  <text x="235" y="187" text-anchor="middle" fill="#7FE0EB"
        font-family="'JetBrains Mono','SF Mono','Cascadia Code',monospace"
        font-size="11">Rust</text>

  <!-- Next.js -->
  <rect x="270" y="170" width="65" height="26" rx="13" fill="rgba(127,224,235,0.08)"
        stroke="rgba(127,224,235,0.22)" stroke-width="1"/>
  <text x="302" y="187" text-anchor="middle" fill="#7FE0EB"
        font-family="'JetBrains Mono','SF Mono','Cascadia Code',monospace"
        font-size="11">Next.js</text>

  <!-- Node.js -->
  <rect x="345" y="170" width="65" height="26" rx="13" fill="rgba(127,224,235,0.08)"
        stroke="rgba(127,224,235,0.22)" stroke-width="1"/>
  <text x="377" y="187" text-anchor="middle" fill="#7FE0EB"
        font-family="'JetBrains Mono','SF Mono','Cascadia Code',monospace"
        font-size="11">Node.js</text>

  <!-- GraphQL -->
  <rect x="420" y="170" width="72" height="26" rx="13" fill="rgba(127,224,235,0.08)"
        stroke="rgba(127,224,235,0.22)" stroke-width="1"/>
  <text x="456" y="187" text-anchor="middle" fill="#7FE0EB"
        font-family="'JetBrains Mono','SF Mono','Cascadia Code',monospace"
        font-size="11">GraphQL</text>
```

- [ ] **Step 6: Add social icons**

Three small SVG icon paths (envelope, LinkedIn, X) positioned bottom-right.

```xml
  <!-- Social icons (bottom-right) -->
  <!-- Email envelope -->
  <g transform="translate(720, 232)" fill="none" stroke="rgba(255,198,160,0.6)"
     stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
    <rect x="0" y="0" width="18" height="14" rx="2"/>
    <path d="M0 0L9 7L18 0"/>
  </g>

  <!-- LinkedIn -->
  <g transform="translate(750, 232)" fill="rgba(255,198,160,0.6)">
    <path d="M4 2a1.5 1.5 0 11-3 0 1.5 1.5 0 013 0zM1 5h3v9h-3zM7 5h2.5v1.2c.5-.8 1.5-1.4 2.7-1.4 2.8 0 3.3 1.8 3.3 4.2V14h-3v-4.3c0-1 0-2.3-1.4-2.3s-1.7 1.1-1.7 2.2V14H7z"/>
  </g>

  <!-- X/Twitter -->
  <g transform="translate(782, 232)" fill="rgba(255,198,160,0.6)">
    <path d="M1 1l6.5 8L1 16h1.5l5.5-6 4.5 6H16L9.5 7.5 15.5 1H14L9 6.5 5 1zm2 1.2h2.2l9.2 12.6h-2.2z"/>
  </g>
```

- [ ] **Step 7: Verify the SVG renders correctly**

Open the SVG in a browser to check layout, colors, and alignment:

Run: `open /Users/73nko/Projects/73nko/img/hero-card.svg`

Verify:
- Dusk background with 14px rounded corners
- 3px gradient stripe visible at top (magenta → tangerine → turquoise)
- `01` in magenta top-right
- `SENIOR SOFTWARE ENGINEER` eyebrow in turquoise
- `Alex Pérez` in gradient text, large
- Tagline in rosegold with magenta-hi bold names
- 6 tech pills in turquoise with subtle borders
- 3 social icons bottom-right in muted rosegold

Adjust positions/sizes as needed until layout looks balanced.

- [ ] **Step 8: Commit**

```bash
git add img/hero-card.svg
git commit -m "Redesign hero card with Sunset Pool Splash style"
```

---

### Task 2: Update README and clean up old files

**Files:**
- Rewrite: `README.md`
- Delete: `img/currently-building.svg`
- Delete: `img/tech-stack.svg`

- [ ] **Step 1: Rewrite README.md**

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

- [ ] **Step 2: Delete old SVG files**

```bash
rm img/currently-building.svg img/tech-stack.svg
```

- [ ] **Step 3: Verify README renders on GitHub**

Check that `README.md` references the correct hero card path and the GitHub stats URLs are unchanged.

Run: `cat README.md` and confirm the structure matches the spec.

- [ ] **Step 4: Commit**

```bash
git add README.md
git rm img/currently-building.svg img/tech-stack.svg
git commit -m "Update README layout and remove old SVG cards"
```

---

### Task 3: Visual QA and final adjustments

- [ ] **Step 1: Open the hero SVG in browser and compare against style guide**

Run: `open /Users/73nko/Projects/73nko/img/hero-card.svg`

Check:
- Colors match the style guide tokens exactly
- Text hierarchy reads well (eyebrow → name → tagline → pills)
- Spacing is balanced — not cramped, not too spread
- Pills are evenly spaced and readable
- Social icons are visible but not dominant

- [ ] **Step 2: Fix any alignment or spacing issues found in QA**

Adjust x/y positions, font sizes, or pill widths as needed. Common issues:
- Pills overlapping (increase gaps)
- Name too close to eyebrow (increase y offset)
- Social icons misaligned (adjust translate values)

- [ ] **Step 3: Commit any fixes**

```bash
git add img/hero-card.svg
git commit -m "Fix hero card spacing and alignment"
```

(Skip this step if no fixes were needed.)

---

### Task 4: Generate QA test plan

- [ ] **Step 1: Use the `qa-test-planner` skill to generate a manual QA plan**

Save to `~/awtomic/docs/superpowers/qa/2026-04-22-profile-redesign-qa-plan.md`.

The QA plan should cover:
- Hero card renders in Chrome, Firefox, Safari
- Hero card renders on GitHub (push to a branch, check)
- All colors match style guide tokens
- GitHub stats cards still display correctly
- No broken image references in README
- Old SVG files are gone
- Card is responsive (width="840" with viewBox scales)
