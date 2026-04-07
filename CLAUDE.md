# CLAUDE.md — AI Masterclass

## Project Overview

This repo contains a single-page HTML guide called **"The 10× Engineer — AI Masterclass"**. It is a comprehensive brown-bag-style learning guide for software engineers on using AI effectively — both as a development tool and as a feature to integrate into products. It also covers AI security (offensive and defensive).

The guide is intentionally a **single self-contained `index.html` file** with no framework, no build system, and no external dependencies beyond Google Fonts. Everything — styles, scripts, content — is inline. Deployment is a single `wrangler pages deploy` command.

Hosted at: `masterclass.sharkfins.xyz`

---

## Architecture

```
index.html          # The entire guide — all 43 modules
README.md           # Deployment instructions
CLAUDE.md           # This file
```

The HTML file is approximately 285KB and ~3,900 lines. It consists of:
- A `<style>` block with the complete CSS design system (~300 lines)
- A fixed sidebar `<nav>` with links to all 43 modules
- A `.main` div containing all content sections
- A small `<script>` block at the end for sidebar active-link highlighting via IntersectionObserver

---

## Content Structure

The guide has three parts, each with a distinct color accent:

| Part | Modules | Topic | Accent Color |
|------|---------|-------|-------------|
| Part I | 01–16 | AI as Your Coding Copilot | `--amber` (#f59e0b) |
| Part II | 17–30 | Integrating AI Into Your Apps | `--cyan` (#22d3ee) |
| Part III | 31–43 | Hacking AI & Defending It | `--red` (#f87171) |

Each module follows this exact structure:
```html
<section id="[unique-id]">
  <div class="sec-tag"><span class="sec-num">[##]</span> [Category]</div>
  <h2>[TITLE] <em>[EMPHASIZED WORD]</em></h2>
  <div class="divider"></div>
  <p class="intro">One paragraph introduction...</p>

  <!-- Content blocks — see Component Library below -->

  <div class="homework">
    <div class="hw-title">Lab [##] — [Lab Name]</div>
    <div class="hw-body">Brief description of the lab goal...</div>
    <ol class="hw-steps">
      <li>Step one...</li>
      <li>Step two...</li>
    </ol>
    <div class="hw-goal">✓ Goal: Specific, measurable deliverable.</div>
  </div>
</section>
```

**Every module must end with a homework block.** This is a core design principle of the guide.

---

## Design System

### CSS Variables (defined in `:root`)

```css
--bg: #080808          /* Page background */
--surface: #111        /* Card/sidebar background */
--surface2: #181818    /* Inline code background */
--border: #222         /* Default border */

--amber: #f59e0b       /* Primary accent — Part I, callouts, active nav */
--amber-dim: #b45309   /* Darker amber for decorative use */
--amber-glow: rgba(245,158,11,0.1)

--cyan: #22d3ee        /* Part II accent */
--cyan-dim: #0e7490

--green: #4ade80       /* Success, cost-efficient indicators */
--red: #f87171         /* Part III accent, warnings, attack content */
--purple: #c084fc      /* Code syntax — variable color */

--text: #e8e8e8        /* Primary text */
--muted: #666          /* Secondary text */
--dim: #3a3a3a         /* Decorative/disabled elements */
```

### Typography
- `'Bebas Neue'` — display headings (h2, large numbers)
- `'Space Mono'` — monospace (code, nav links, labels, module numbers)
- `'DM Sans'` — body text

### Component Library

Use these existing components. Do not invent new CSS classes unless absolutely necessary — extend the existing system.

**Callout boxes** (4 variants):
```html
<div class="callout">                    <!-- amber — default -->
<div class="callout callout-cyan">       <!-- cyan -->
<div class="callout callout-green">      <!-- green -->
<div class="callout callout-red">        <!-- red — warnings/attacks -->
  <div class="callout-label">LABEL TEXT</div>
  <p>Content...</p>
</div>
```

**Strategy/numbered list:**
```html
<div class="strat-list">
  <div class="strat-item">
    <div class="strat-n">01</div>       <!-- or → for bullet-style -->
    <div class="strat-c">
      <h3>Title</h3>
      <p>Content...</p>
    </div>
  </div>
</div>
```

**Code block:**
```html
<div class="code-block">
  <span class="code-label">filename or context</span>
  <span class="cm">// comment</span>
  <span class="kw">const</span> <span class="vr">x</span> = <span class="fn">someFunction</span>(<span class="st">'string'</span>);
</div>
```
Code syntax classes: `.cm` (comment/dim), `.kw` (keyword/cyan), `.st` (string/green), `.fn` (function/amber), `.vr` (variable/purple), `.nm` (number/red)

**Cards:**
```html
<div class="card-grid">
  <div class="card">
    <span class="card-icon">🔧</span>
    <div class="card-name">Tool Name</div>
    <span class="card-tag tag-free">Free</span>       <!-- tag-free, tag-paid, tag-both, tag-open -->
    <p class="card-desc">Description...</p>
    <div class="card-verdict">→ Verdict</div>
  </div>
</div>
```

**Model cards with bars:**
```html
<div class="model-grid">
  <div class="model-card">
    <div class="model-provider">Provider Name</div>
    <div class="model-name">Model Name</div>
    <div class="model-bars">
      <div class="bar-row"><div class="bar-label">Intelligence</div><div class="bar-track"><div class="bar-fill bar-intel" style="width:85%"></div></div></div>
      <div class="bar-row"><div class="bar-label">Speed</div><div class="bar-track"><div class="bar-fill bar-speed" style="width:80%"></div></div></div>
      <div class="bar-row"><div class="bar-label">Cost Eff.</div><div class="bar-track"><div class="bar-fill bar-cost" style="width:70%"></div></div></div>
    </div>
    <div class="model-use">Best for: ...</div>
  </div>
</div>
```

**Tables:**
```html
<table class="tool-table">
  <thead><tr><th>Col 1</th><th>Col 2</th></tr></thead>
  <tbody>
    <tr><td class="tool-name">Name</td><td>Value</td></tr>
  </tbody>
</table>

<table class="cost-table">   <!-- for pricing tables -->
  <!-- same structure, adds cost-best / cost-mid / cost-high classes on <td> -->
</table>
```

**Workflow arrow chain:**
```html
<div class="workflow">
  <div class="wf-step">
    <div class="wf-icon">📋</div>
    <div class="wf-label">Step Name</div>
    <div class="wf-desc">Short description</div>
  </div>
  <!-- repeat for each step, last step has no arrow via CSS -->
</div>
```

**Phase grid (2-column):**
```html
<div class="phase-grid">
  <div class="phase-card">
    <div class="phase-num">01</div>
    <div class="phase-title">Phase Title</div>
    <ul class="phase-items">
      <li>Item</li>
    </ul>
  </div>
</div>
```

**Tier list:**
```html
<div class="tier tier-s"><div class="tier-lbl">S</div><div class="tier-items"><span class="tier-pill">Tool</span></div></div>
<div class="tier tier-a">...</div>
<div class="tier tier-b">...</div>
<div class="tier tier-c">...</div>
```

**MCP grid (small cards):**
```html
<div class="mcp-grid">
  <div class="mcp-item">
    <div class="mcp-name">server-name</div>
    <div class="mcp-desc">What it does.</div>
  </div>
</div>
```

**Architecture diagram (3-step):**
```html
<div class="arch">
  <div class="arch-box"><div class="arch-icon">📝</div><div class="arch-label">Label</div><div class="arch-sub">Sublabel</div></div>
  <div class="arch-arrow">→</div>
  <div class="arch-box">...</div>
  <div class="arch-arrow">→</div>
  <div class="arch-box">...</div>
</div>
```

**Compare grid (3-column):**
```html
<div class="compare-grid">
  <div class="compare-card highlight">   <!-- highlight adds amber border -->
    <div class="compare-title">Title</div>
    <ul class="compare-list"><li>Item</li></ul>
  </div>
</div>
```

**Part header (between parts):**
```html
<div class="part-header" id="part[n]">
  <div class="part-badge">Part [N] of [Total]</div>
  <h2>PART TITLE <em style="color:var(--accent)">EMPHASIS</em></h2>
  <p>Part description...</p>
</div>
```

**Inline code / keyboard shortcut:**
```html
<span class="it">command-name</span>
```

**Highlighted text:**
```html
<mark>important phrase</mark>
```

---

## Sidebar Navigation

The sidebar nav is manually maintained in the `<nav class="sidebar">` block near the top of the file. When adding a new module:

1. Add a `<a href="#[section-id]" class="nav-link">[##] — [Title]</a>` in the correct part
2. Optionally add a `<div class="nav-cat">Category Name</div>` if starting a new category
3. The IntersectionObserver script at the bottom automatically handles active-link highlighting — no manual JS needed

Part nav headers use:
```html
<div class="nav-part">Part [N]</div>
```
Part III nav header additionally needs the red color inline style:
```html
<div class="nav-part" style="color:var(--red)">Part III</div>
```

---

## Content Conventions

- **Every module has a homework block** — without exception. Labs are numbered `Lab [module number] — [Name]`. The `hw-goal` line starts with `✓ Goal:` and describes one specific, measurable deliverable.
- **Intro paragraph** (`class="intro"`) is always one paragraph, max 3 sentences, under 60 words.
- **h2 titles** are ALL CAPS with one `<em>` word or phrase in the part's accent color. Example: `<h2>THE <em>HIGHLIGHTED PART</em></h2>`
- **Stack-agnostic language** — never reference specific hosting providers (Vercel, Supabase, Heroku, Railway, etc.) as the default. Reference categories ("your database," "your deployment platform") or name multiple options. The guide is used by engineers with different stacks.
- **Code blocks** use the syntax color spans (`.cm`, `.kw`, `.st`, `.fn`, `.vr`, `.nm`) — do not use raw code without styling.
- **Module numbers are sequential** across all three parts (01–43 currently). New modules continue from 44.
- **Section IDs** follow the pattern: `[part-prefix]-[topic-slug]`. Part I sections have no prefix (e.g. `id="mindset"`). Part II uses `p2-` (e.g. `id="p2-rag"`). Part III uses `p3-` (e.g. `id="p3-prompt-injection"`).

---

## Adding a New Module

1. Pick the right part and the right position in the content flow
2. Add the `<section>` block following the exact structure above
3. Add the nav link in the sidebar
4. Ensure the homework block is present and has a concrete, measurable goal
5. Verify the section ID follows the naming convention
6. Check that code blocks use the syntax color spans
7. Run a quick visual sanity check — open index.html locally in a browser

## Updating Existing Content

When tool versions, pricing, or model names change:
- Update the relevant module's content and any tables referencing the outdated info
- If a pricing table changes significantly, update the cost-table in Module 19
- If a new model tier emerges, update the model cards in Module 03 and cost table in Module 19
- Keep OWASP references aligned with the current LLM Top 10 year

---

## Deployment

```bash
# Deploy to Cloudflare Pages (requires wrangler login first)
wrangler pages deploy . --project-name ai-masterclass

# The site is served from index.html at the root
# No build command, no output directory — deploy the repo root directly
```

Live URL: `masterclass.sharkfins.xyz`
Cloudflare Pages project: `ai-masterclass`
