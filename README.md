# The 10× Engineer — AI Masterclass

A comprehensive, self-contained HTML guide for software engineers on leveraging AI — from coding assistants and autonomous agents to integrating AI into products, training models, and securing AI systems against attack.

**Live at:** `masterclass.sharkfins.xyz` (or your configured subdomain)

---

## What's Inside

The guide is a single `index.html` file — no framework, no build step, no dependencies. Everything is inline: styles, scripts, and content. It renders fully offline.

### Part I — AI as Your Coding Copilot (Modules 01–16)
How to use AI tools to write code faster, run autonomous agents, manage side projects, and operate like a one-person engineering team. Covers the full tool landscape, Claude Code, MCP servers, prompt engineering, agentic workflows, security hygiene, team adoption, and staying current.

### Part II — Integrating AI Into Your Apps (Modules 17–30)
How to add AI capabilities to the products you build. Covers API providers and pricing, integration patterns (zero-shot, RAG, streaming, agents), embeddings and vector databases, fine-tuning, training custom models, self-hosting with Ollama and vLLM, and running AI in production with observability and guardrails.

### Part III — Hacking AI & Defending It (Modules 31–43)
The complete attacker and defender's guide to AI security. Covers the OWASP LLM Top 10, prompt injection (all six attack families), jailbreaking, system prompt extraction, data poisoning, RAG poisoning, agent hijacking, adversarial examples, model theft, AI red teaming, defense-in-depth architecture, and compliance/governance.

**43 modules. 43 homework labs. 60+ tools covered. 40+ working code examples.**

---

## Deployment

The guide deploys to Cloudflare Pages as a static site. No build step required.

### Prerequisites

```bash
npm install -g wrangler
wrangler login
```

### First Deploy

```bash
# Clone the repo
git clone <your-repo-url>
cd <repo-name>

# Deploy to Cloudflare Pages
wrangler pages deploy . --project-name ai-masterclass
```

Your guide will be live at `ai-masterclass.pages.dev` immediately.

### Connect a Custom Subdomain

1. Go to [dash.cloudflare.com](https://dash.cloudflare.com) → **Workers & Pages** → `ai-masterclass`
2. Click **Custom domains → Set up a custom domain**
3. Enter your subdomain (e.g. `masterclass.sharkfins.xyz`)
4. Cloudflare automatically creates the CNAME — no manual DNS edits needed since sharkfins.xyz is already managed by Cloudflare
5. Propagates in ~2 minutes

### Subsequent Deploys

```bash
wrangler pages deploy . --project-name ai-masterclass
```

Cloudflare Pages keeps a full deployment history. Roll back to any previous version from the dashboard if needed.

### GitHub-Connected Auto Deploy (Optional)

If you prefer automatic deploys on every `git push`:

1. Go to your Pages project → **Settings → Git connections**
2. Connect this repository
3. Set build command to *(none)* and output directory to `/`
4. Every push to `main` auto-deploys — no manual `wrangler` command needed

---

## Project Structure

```
/
├── index.html      # The entire guide — all 43 modules, inline styles and scripts
├── README.md       # This file
└── CLAUDE.md       # Context file for Claude Code sessions
```

---

## Making Changes

The guide is intentionally a single file to keep deployment trivial. When editing:

- **Adding a module:** Follow the existing section pattern — `<section id="...">` with `.sec-tag`, `<h2>`, `.divider`, `.intro`, content blocks, and a `.homework` block at the end
- **Design system:** All CSS variables are defined in the `:root` block at the top of `<style>`. Colors: `--amber` (primary), `--cyan` (Part II accent), `--red` (Part III accent), `--green` (success/cost)
- **Navigation:** The sidebar `<nav>` is manually maintained — add a `.nav-link` entry for any new section
- **Part colors:** Part I uses amber (`var(--amber)`), Part II uses cyan (`var(--cyan)`), Part III uses red (`var(--red)`)

See `CLAUDE.md` for the full context used in Claude Code sessions.

---

## Contributing

This guide is intentionally opinionated and reflects a specific point of view on what matters for engineers building with AI in 2026. If you want to add a module, the bar is: would this have saved me significant time or prevented a real mistake? If yes, open a PR.
