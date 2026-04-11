# Blog Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a blog to shaanagara.com with 6 articles, a listing page, a homepage Writing section, and a shared nav bar.

**Architecture:** Hybrid HTML + shared CSS. Extract inline styles from `index.html` into `styles.css`, add nav and blog-card styles. Blog listing and 6 blog post HTML files in `blog/` directory. No build tools, no JS framework, GitHub Pages deploy.

**Tech Stack:** HTML, CSS, GitHub Pages

**Spec:** `docs/superpowers/specs/2026-04-11-blog-design.md`

**Author context:** Shaan Agara is a Director of Product at PointClickCare, Stanford AI student, and open-source builder. Write blog content in first person from his perspective. Concise, opinionated, no filler. Never use em dashes. Do not mention confidential acquisition figures or funding amounts.

---

## File Map

| File | Action | Responsibility |
|------|--------|----------------|
| `styles.css` | Create | Shared styles (extracted from index.html + nav + blog cards + blog article) |
| `index.html` | Modify | Replace inline styles with link to styles.css, add nav bar, add Writing section |
| `blog/index.html` | Create | Blog listing page with card grid |
| `blog/open-source-new-resume.html` | Create | Blog post 1 (Apr 1) |
| `blog/hipaa-ai-agents.html` | Create | Blog post 2 (Apr 3) |
| `blog/shipping-side-projects.html` | Create | Blog post 3 (Apr 5) |
| `blog/pm-new-stack-ai-os.html` | Create | Blog post 4 (Apr 7) |
| `blog/agent-cost-problem.html` | Create | Blog post 5 (Apr 9) |
| `blog/your-product-roadmap-ai-agents.html` | Create | Blog post 6 (Apr 11) |

**Task dependencies:** Tasks 1-3 are sequential (styles first, then homepage update, then listing page). Tasks 4-9 (blog posts) are independent of each other but depend on Task 1 (they reference styles.css).

---

### Task 1: Create shared stylesheet (styles.css)

**Files:**
- Create: `styles.css`

- [ ] **Step 1: Create styles.css with all shared styles**

Create `styles.css` at the repo root. This file contains all the CSS currently inlined in `index.html` (lines 22-589), plus new styles for the nav bar, blog cards, and blog article layout.

The file must include these sections in order:

1. **All existing styles** from `index.html` `<style>` block (reset, layout, hero, about, projects, timeline, credentials, footer, animations, responsive). Copy them exactly.

2. **Nav bar styles** (new):

```css
/* ===== NAV ===== */
.site-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px clamp(1.5rem, 1rem + 4vw, 5rem);
  max-width: 1100px;
  margin: 0 auto;
}
.site-nav a {
  text-decoration: none;
  color: #0f172a;
  transition: color 100ms ease-in-out;
}
.site-nav-brand {
  font-weight: 700;
  font-size: 1rem;
}
.site-nav-links {
  display: flex;
  gap: 24px;
}
.site-nav-link {
  font-weight: 500;
  font-size: 0.9rem;
  color: #475569;
}
.site-nav-link:hover {
  color: #0f172a;
}
```

3. **Blog card styles** (new):

```css
/* ===== BLOG CARDS ===== */
.blog-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 20px;
}
.blog-card {
  background: #f0ede8;
  border-radius: 12px;
  padding: 32px;
  text-decoration: none;
  color: inherit;
  display: flex;
  flex-direction: column;
  transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
}
.blog-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 32px rgba(15, 23, 42, 0.08);
}
.blog-card-date {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.7rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: #94a3b8;
  margin-bottom: 8px;
}
.blog-card-title {
  font-size: clamp(1.15rem, 1rem + 0.3vw, 1.35rem);
  font-weight: 800;
  color: #0f172a;
  letter-spacing: -0.5px;
  line-height: 1.3;
  margin-bottom: 8px;
}
.blog-card-excerpt {
  font-family: 'Source Serif 4', Georgia, serif;
  font-size: 0.9rem;
  color: #475569;
  line-height: 1.7;
  margin-bottom: 16px;
  flex: 1;
}
.blog-card-tags {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
}
.blog-card-tag {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.62rem;
  font-weight: 500;
  color: #475569;
  background: #f8fafc;
  border: 1px solid #e2e8f0;
  border-radius: 999px;
  padding: 4px 10px;
  letter-spacing: 0.3px;
}
.writing-cta {
  text-align: center;
  margin-top: 40px;
}
```

4. **Blog article styles** (new):

```css
/* ===== BLOG ARTICLE ===== */
.article-header {
  max-width: 680px;
  margin: 0 auto;
  padding: clamp(3rem, 2rem + 3vw, 5rem) clamp(1.5rem, 1rem + 4vw, 5rem) 0;
}
.article-meta {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.75rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #94a3b8;
  margin-bottom: 16px;
}
.article-title {
  font-size: clamp(1.8rem, 1.5rem + 1vw, 2.5rem);
  font-weight: 800;
  letter-spacing: -1px;
  line-height: 1.15;
  color: #0f172a;
  margin-bottom: 16px;
}
.article-subtitle {
  font-family: 'Source Serif 4', Georgia, serif;
  font-size: clamp(1.05rem, 1rem + 0.2vw, 1.2rem);
  font-style: italic;
  color: #475569;
  line-height: 1.7;
  margin-bottom: 16px;
}
.article-tags {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 32px;
}
.article-divider {
  max-width: 680px;
  margin: 0 auto;
  border: none;
  border-top: 1px solid #e2e8f0;
}
.article-body {
  max-width: 680px;
  margin: 0 auto;
  padding: 40px clamp(1.5rem, 1rem + 4vw, 5rem) clamp(3rem, 2rem + 3vw, 5rem);
}
.article-body p {
  font-family: 'Source Serif 4', Georgia, serif;
  font-size: clamp(1.05rem, 1rem + 0.15vw, 1.125rem);
  color: #475569;
  line-height: 1.85;
  margin-bottom: 24px;
}
.article-body h2 {
  font-family: 'Inter', system-ui, sans-serif;
  font-size: clamp(1.3rem, 1.1rem + 0.5vw, 1.6rem);
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.3px;
  margin-top: 48px;
  margin-bottom: 20px;
}
.article-body h3 {
  font-family: 'Inter', system-ui, sans-serif;
  font-size: clamp(1.1rem, 1rem + 0.3vw, 1.25rem);
  font-weight: 600;
  color: #0f172a;
  margin-top: 36px;
  margin-bottom: 16px;
}
.article-body strong {
  color: #0f172a;
  font-weight: 600;
}
.article-body a {
  color: #0f172a;
  font-weight: 600;
  text-decoration: underline;
  text-underline-offset: 0.2em;
  text-decoration-thickness: 0.06em;
  transition: color 100ms ease-in-out;
}
.article-body a:hover {
  color: #475569;
}
.article-body ul, .article-body ol {
  font-family: 'Source Serif 4', Georgia, serif;
  font-size: clamp(1.05rem, 1rem + 0.15vw, 1.125rem);
  color: #475569;
  line-height: 1.85;
  margin-bottom: 24px;
  padding-left: 24px;
}
.article-body li {
  margin-bottom: 8px;
}

/* Blog visual components */
.visual-comparison {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  margin: 32px 0;
}
.visual-comparison-card {
  background: #f0ede8;
  border-radius: 12px;
  padding: 24px;
}
.visual-comparison-label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.65rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: #94a3b8;
  margin-bottom: 12px;
}
.visual-comparison-title {
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 1rem;
  font-weight: 700;
  color: #0f172a;
  margin-bottom: 8px;
}
.visual-comparison-text {
  font-family: 'Source Serif 4', Georgia, serif;
  font-size: 0.9rem;
  color: #475569;
  line-height: 1.7;
}

.visual-flow {
  display: flex;
  align-items: center;
  gap: 12px;
  margin: 32px 0;
  flex-wrap: wrap;
  justify-content: center;
}
.visual-flow-step {
  background: #f0ede8;
  border-radius: 8px;
  padding: 12px 20px;
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 0.85rem;
  font-weight: 600;
  color: #0f172a;
  text-align: center;
}
.visual-flow-step.active {
  background: #0f172a;
  color: #ffffff;
}
.visual-flow-arrow {
  font-size: 1.2rem;
  color: #94a3b8;
}

.visual-callout {
  border-left: 4px solid #0f172a;
  background: #faf8f5;
  padding: 20px 24px;
  margin: 32px 0;
  border-radius: 0 8px 8px 0;
}
.visual-callout p {
  font-family: 'Source Serif 4', Georgia, serif;
  font-size: 1rem;
  color: #0f172a;
  line-height: 1.7;
  margin-bottom: 0;
  font-weight: 500;
}

.visual-metric {
  display: flex;
  gap: 32px;
  margin: 32px 0;
  flex-wrap: wrap;
}
.visual-metric-item {
  text-align: center;
  flex: 1;
  min-width: 120px;
}
.visual-metric-number {
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 2.5rem;
  font-weight: 800;
  color: #0f172a;
  letter-spacing: -1px;
  line-height: 1.1;
}
.visual-metric-label {
  font-family: 'Source Serif 4', Georgia, serif;
  font-size: 0.85rem;
  color: #94a3b8;
  margin-top: 4px;
}

.visual-code {
  background: #f0ede8;
  border-radius: 12px;
  padding: 24px;
  margin: 32px 0;
  overflow-x: auto;
}
.visual-code-label {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.65rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: #94a3b8;
  margin-bottom: 12px;
}
.visual-code pre {
  font-family: 'JetBrains Mono', monospace;
  font-size: 0.85rem;
  line-height: 1.6;
  color: #0f172a;
  margin: 0;
  white-space: pre;
}

.visual-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 8px;
  margin: 32px 0;
}
.visual-grid-item {
  background: #f0ede8;
  border-radius: 8px;
  padding: 12px 16px;
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 0.8rem;
  font-weight: 500;
  color: #0f172a;
  text-align: center;
}

.visual-framework {
  counter-reset: framework;
  margin: 32px 0;
  list-style: none;
  padding: 0;
}
.visual-framework li {
  counter-increment: framework;
  display: flex;
  gap: 16px;
  align-items: flex-start;
  padding: 16px 0;
  border-bottom: 1px solid #e2e8f0;
}
.visual-framework li:last-child {
  border-bottom: none;
}
.visual-framework li::before {
  content: counter(framework);
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 1.2rem;
  font-weight: 800;
  color: #0f172a;
  min-width: 32px;
}

/* Article footer */
.article-footer {
  max-width: 680px;
  margin: 0 auto;
  padding: 0 clamp(1.5rem, 1rem + 4vw, 5rem) clamp(3rem, 2rem + 3vw, 5rem);
}
.article-author {
  border-top: 1px solid #e2e8f0;
  padding-top: 32px;
  margin-bottom: 32px;
}
.article-author-name {
  font-family: 'Inter', system-ui, sans-serif;
  font-size: 0.9rem;
  font-weight: 700;
  color: #0f172a;
  margin-bottom: 4px;
}
.article-author-bio {
  font-family: 'Source Serif 4', Georgia, serif;
  font-size: 0.85rem;
  color: #94a3b8;
  line-height: 1.6;
}
.article-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 24px;
  border-top: 1px solid #e2e8f0;
}
.article-nav a {
  font-size: 0.85rem;
  font-weight: 600;
  color: #0f172a;
  text-decoration: none;
  transition: color 100ms ease-in-out;
}
.article-nav a:hover {
  color: #475569;
}
.article-back {
  text-align: center;
  margin-bottom: 24px;
}
.article-back a {
  font-size: 0.85rem;
  font-weight: 600;
  color: #475569;
  text-decoration: none;
  transition: color 100ms ease-in-out;
}
.article-back a:hover {
  color: #0f172a;
}

/* Blog listing header */
.blog-header {
  padding: clamp(4rem, 3rem + 3vw, 6rem) 0 clamp(2rem, 1.5rem + 1.5vw, 3rem);
}
.blog-header-subtitle {
  font-family: 'Source Serif 4', Georgia, serif;
  font-size: clamp(1.05rem, 1rem + 0.2vw, 1.175rem);
  color: #475569;
  line-height: 1.7;
}
```

5. **Additional responsive rules** (append to existing responsive section):

```css
@media (max-width: 900px) {
  .blog-grid { grid-template-columns: 1fr; }
  .visual-comparison { grid-template-columns: 1fr; }
}

@media (max-width: 640px) {
  .article-title { letter-spacing: -0.5px; }
  .visual-metric { gap: 16px; }
  .visual-flow { flex-direction: column; }
  .visual-flow-arrow { transform: rotate(90deg); }
}
```

- [ ] **Step 2: Verify styles.css loads correctly**

Run: `cd /tmp/shaan-website && python3 -m http.server 8080 &`

Open `http://localhost:8080` to confirm the homepage still works (it will still use inline styles at this point). Then kill the server.

- [ ] **Step 3: Commit**

```bash
cd /tmp/shaan-website
git add styles.css
git commit -m "feat: create shared stylesheet with nav, blog card, and article styles"
```

---

### Task 2: Update homepage (index.html)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace inline styles with stylesheet link**

In `index.html`, replace the entire `<style>...</style>` block (lines 21-590) with:

```html
<link rel="stylesheet" href="styles.css">
```

- [ ] **Step 2: Add nav bar above the hero section**

Insert this immediately after `<body>` (before the `<!-- HERO -->` comment):

```html
<!-- NAV -->
<nav class="site-nav bg-warm">
  <a href="/" class="site-nav-brand">Shaan Agara</a>
  <div class="site-nav-links">
    <a href="/blog/" class="site-nav-link">Blog</a>
  </div>
</nav>
```

- [ ] **Step 3: Add Writing section between Projects and Footer**

Insert this between the closing `</section>` of the Projects section and the `<!-- FOOTER -->` comment:

```html
<hr class="section-divider">

<!-- WRITING -->
<section class="section bg-cream">
  <div class="container">
    <div class="section-label fade-in">Writing</div>
    <div class="blog-grid">

      <a href="blog/your-product-roadmap-ai-agents.html" class="blog-card fade-in">
        <span class="blog-card-date">April 11, 2026</span>
        <span class="blog-card-title">Your Product Roadmap Doesn't Account for AI Agents</span>
        <span class="blog-card-excerpt">Most product orgs are treating AI as a feature. It's an architecture shift, and your roadmap needs to reflect that.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">AI</span>
          <span class="blog-card-tag">Product</span>
          <span class="blog-card-tag">Leadership</span>
        </span>
      </a>

      <a href="blog/agent-cost-problem.html" class="blog-card fade-in">
        <span class="blog-card-date">April 9, 2026</span>
        <span class="blog-card-title">The Agent Cost Problem Nobody's Talking About</span>
        <span class="blog-card-excerpt">AI agents are powerful but expensive in ways that are hard to predict. Observability is the missing infrastructure layer.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">AI</span>
          <span class="blog-card-tag">Agents</span>
          <span class="blog-card-tag">Observability</span>
        </span>
      </a>

      <a href="blog/pm-new-stack-ai-os.html" class="blog-card fade-in">
        <span class="blog-card-date">April 7, 2026</span>
        <span class="blog-card-title">The PM's New Stack: Why I Built an AI Operating System for Product Managers</span>
        <span class="blog-card-excerpt">PM workflows are ripe for AI augmentation. Here's the story behind PM-OS and why the knowledge system matters most.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">Product</span>
          <span class="blog-card-tag">AI</span>
          <span class="blog-card-tag">Tools</span>
        </span>
      </a>

      <a href="blog/shipping-side-projects.html" class="blog-card fade-in">
        <span class="blog-card-date">April 5, 2026</span>
        <span class="blog-card-title">Shipping Side Projects Made Me a Better Product Leader</span>
        <span class="blog-card-excerpt">Building AI tools outside of work sharpened my product instincts more than any framework or certification ever did.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">Product</span>
          <span class="blog-card-tag">Leadership</span>
          <span class="blog-card-tag">Building</span>
        </span>
      </a>

      <a href="blog/hipaa-ai-agents.html" class="blog-card fade-in">
        <span class="blog-card-date">April 3, 2026</span>
        <span class="blog-card-title">HIPAA and AI Agents: Healthcare's Hardest Unsolved Problem</span>
        <span class="blog-card-excerpt">AI agents in healthcare hit a compliance wall that most builders ignore. Here's what it actually takes.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">Healthcare</span>
          <span class="blog-card-tag">AI</span>
          <span class="blog-card-tag">Compliance</span>
        </span>
      </a>

      <a href="blog/open-source-new-resume.html" class="blog-card fade-in">
        <span class="blog-card-date">April 1, 2026</span>
        <span class="blog-card-title">Open Source Is the New Resume</span>
        <span class="blog-card-excerpt">In the age of AI, shipping real tools in public says more about you than any credential or title ever could.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">Open Source</span>
          <span class="blog-card-tag">Career</span>
          <span class="blog-card-tag">AI</span>
        </span>
      </a>

    </div>
    <div class="writing-cta fade-in">
      <a href="blog/" class="hero-link secondary">View all posts</a>
    </div>
  </div>
</section>
```

- [ ] **Step 4: Verify homepage in browser**

Run: `cd /tmp/shaan-website && python3 -m http.server 8080`

Open `http://localhost:8080`. Verify:
- Nav bar appears at top with "Shaan Agara" left and "Blog" right
- All existing sections (hero, about, projects) render identically to before
- New "Writing" section appears between projects and footer
- 6 blog cards display in a 2-column grid (sorted newest first)
- "View all posts" button appears below the cards
- Footer renders correctly

Kill the server when done.

- [ ] **Step 5: Commit**

```bash
cd /tmp/shaan-website
git add index.html
git commit -m "feat: add nav bar and Writing section to homepage, link shared stylesheet"
```

---

### Task 3: Create blog listing page (blog/index.html)

**Files:**
- Create: `blog/index.html`

- [ ] **Step 1: Create the blog directory**

```bash
mkdir -p /tmp/shaan-website/blog
```

- [ ] **Step 2: Create blog/index.html**

Create the file with this complete content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Blog | Shaan Agara</title>
<meta name="description" content="Articles on AI, product management, and leadership by Shaan Agara.">
<meta property="og:title" content="Blog | Shaan Agara">
<meta property="og:description" content="Articles on AI, product management, and leadership by Shaan Agara.">
<meta property="og:url" content="https://shaanagara.com/blog/">
<meta property="og:type" content="website">
<meta property="og:image" content="https://shaanagara.com/og-image.png">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Blog | Shaan Agara">
<meta name="twitter:description" content="Articles on AI, product management, and leadership by Shaan Agara.">
<meta name="twitter:image" content="https://shaanagara.com/og-image.png">
<link rel="canonical" href="https://shaanagara.com/blog/">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;500&family=Source+Serif+4:ital,opsz,wght@0,8..60,400;0,8..60,500;0,8..60,600;1,8..60,400&display=swap" rel="stylesheet">
<link rel="icon" type="image/svg+xml" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Ctext x='4' y='26' font-size='28'%3E%E2%9A%A1%3C/text%3E%3C/svg%3E">
<link rel="stylesheet" href="../styles.css">
</head>
<body>

<!-- NAV -->
<nav class="site-nav bg-warm">
  <a href="../" class="site-nav-brand">Shaan Agara</a>
  <div class="site-nav-links">
    <a href="./" class="site-nav-link">Blog</a>
  </div>
</nav>

<!-- HEADER -->
<section class="blog-header bg-warm">
  <div class="container">
    <div class="section-label">Writing</div>
    <p class="blog-header-subtitle">Thoughts on AI, product leadership, and building in public.</p>
  </div>
</section>

<!-- POSTS -->
<section class="section">
  <div class="container">
    <div class="blog-grid">

      <a href="your-product-roadmap-ai-agents.html" class="blog-card fade-in">
        <span class="blog-card-date">April 11, 2026</span>
        <span class="blog-card-title">Your Product Roadmap Doesn't Account for AI Agents</span>
        <span class="blog-card-excerpt">Most product orgs are treating AI as a feature. It's an architecture shift, and your roadmap needs to reflect that.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">AI</span>
          <span class="blog-card-tag">Product</span>
          <span class="blog-card-tag">Leadership</span>
        </span>
      </a>

      <a href="agent-cost-problem.html" class="blog-card fade-in">
        <span class="blog-card-date">April 9, 2026</span>
        <span class="blog-card-title">The Agent Cost Problem Nobody's Talking About</span>
        <span class="blog-card-excerpt">AI agents are powerful but expensive in ways that are hard to predict. Observability is the missing infrastructure layer.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">AI</span>
          <span class="blog-card-tag">Agents</span>
          <span class="blog-card-tag">Observability</span>
        </span>
      </a>

      <a href="pm-new-stack-ai-os.html" class="blog-card fade-in">
        <span class="blog-card-date">April 7, 2026</span>
        <span class="blog-card-title">The PM's New Stack: Why I Built an AI Operating System for Product Managers</span>
        <span class="blog-card-excerpt">PM workflows are ripe for AI augmentation. Here's the story behind PM-OS and why the knowledge system matters most.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">Product</span>
          <span class="blog-card-tag">AI</span>
          <span class="blog-card-tag">Tools</span>
        </span>
      </a>

      <a href="shipping-side-projects.html" class="blog-card fade-in">
        <span class="blog-card-date">April 5, 2026</span>
        <span class="blog-card-title">Shipping Side Projects Made Me a Better Product Leader</span>
        <span class="blog-card-excerpt">Building AI tools outside of work sharpened my product instincts more than any framework or certification ever did.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">Product</span>
          <span class="blog-card-tag">Leadership</span>
          <span class="blog-card-tag">Building</span>
        </span>
      </a>

      <a href="hipaa-ai-agents.html" class="blog-card fade-in">
        <span class="blog-card-date">April 3, 2026</span>
        <span class="blog-card-title">HIPAA and AI Agents: Healthcare's Hardest Unsolved Problem</span>
        <span class="blog-card-excerpt">AI agents in healthcare hit a compliance wall that most builders ignore. Here's what it actually takes.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">Healthcare</span>
          <span class="blog-card-tag">AI</span>
          <span class="blog-card-tag">Compliance</span>
        </span>
      </a>

      <a href="open-source-new-resume.html" class="blog-card fade-in">
        <span class="blog-card-date">April 1, 2026</span>
        <span class="blog-card-title">Open Source Is the New Resume</span>
        <span class="blog-card-excerpt">In the age of AI, shipping real tools in public says more about you than any credential or title ever could.</span>
        <span class="blog-card-tags">
          <span class="blog-card-tag">Open Source</span>
          <span class="blog-card-tag">Career</span>
          <span class="blog-card-tag">AI</span>
        </span>
      </a>

    </div>
  </div>
</section>

<!-- FOOTER -->
<footer class="footer bg-cream">
  <div class="container">
    <div class="section-label">Connect</div>
    <div class="footer-links">
      <a href="https://www.linkedin.com/in/shaan-agara/" class="footer-link" target="_blank" rel="noopener">
        <svg viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
      <a href="https://github.com/shaan-ad" class="footer-link" target="_blank" rel="noopener">
        <svg viewBox="0 0 24 24"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12" fill="currentColor"/></svg>
        GitHub
      </a>
    </div>
    <p class="footer-quote">"You can't connect the dots looking forward; you can only connect them looking backwards. So you have to trust that the dots will somehow connect in your future."</p>
    <p class="footer-quote-attr">Steve Jobs</p>
    <p class="footer-copy">&copy; 2026 Shaan Agara</p>
  </div>
</footer>

<script>
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });
document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));
</script>

</body>
</html>
```

- [ ] **Step 3: Verify blog listing page in browser**

Open `http://localhost:8080/blog/`. Verify:
- Nav bar shows with "Shaan Agara" and "Blog" links
- "Writing" heading and subtitle display
- 6 blog cards in 2-column grid, sorted newest first
- Footer renders correctly
- "Shaan Agara" nav link navigates to homepage

- [ ] **Step 4: Commit**

```bash
cd /tmp/shaan-website
git add blog/index.html
git commit -m "feat: create blog listing page"
```

---

### Task 4: Write blog post 1 - Open Source Is the New Resume

**Files:**
- Create: `blog/open-source-new-resume.html`

**This task is independent of Tasks 5-9 and can run in parallel with them.**

- [ ] **Step 1: Create the blog post file**

Create `blog/open-source-new-resume.html` as a complete HTML page. The post must follow this exact structure:

**SEO metadata:**
- Title: `Open Source Is the New Resume | Shaan Agara`
- Meta description: `In the age of AI, shipping real tools in public says more than credentials. Why open-source builders are pulling ahead in hiring, investing, and career strategy.`
- Canonical: `https://shaanagara.com/blog/open-source-new-resume.html`
- OG type: `article`
- JSON-LD datePublished: `2026-04-01`

**HTML structure:**
```
<nav> (same as blog listing but with relative paths: href="../" for brand, href="./" for Blog)
<article>
  <header class="article-header">
    <div class="article-meta">APRIL 1, 2026 · 8 MIN READ</div>
    <h1 class="article-title">Open Source Is the New Resume</h1>
    <p class="article-subtitle">In the age of AI, shipping real tools in public says more about you than any credential or title ever could.</p>
    <div class="article-tags"> (pills: Open Source, Career, AI) </div>
  </header>
  <hr class="article-divider">
  <div class="article-body"> ... article content ... </div>
  <footer class="article-footer"> ... author + nav ... </footer>
</article>
<footer> (same site footer as listing page)
<script> (same intersection observer)
```

**Article content (write in first person as Shaan, ~2000 words). Section structure:**

**Section 1: "The Credential Gap" (h2)**
- Open with: the traditional signals (degree, title, years of experience) are losing their predictive value, especially in AI/tech.
- Point: when everyone can use AI to generate code, the differentiator is taste, judgment, and the ability to ship complete solutions.
- Include a `visual-comparison` component:
  - Left card: "THE OLD SIGNAL" / title "Credentials" / items: degree, job title, years of experience, certifications, interview performance
  - Right card: "THE NEW SIGNAL" / title "Shipping History" / items: public repos, users and stars, documentation quality, commit history, problem selection

**Section 2: "What Open Source Actually Proves" (h2)**
- Argument: open source proves four things no resume can: (1) you can identify real problems, (2) you can ship complete solutions, (3) you can communicate technical ideas clearly (via docs/READMEs), (4) you can maintain and iterate.
- Personal example: reference building Agent Watch. You noticed that agent cost observability was a gap. Solving it publicly proved you could identify the problem, build the solution, write docs that others could follow, and iterate based on feedback.
- Include a `visual-callout`: "A GitHub repo with a clear README, a solved problem, and active maintenance tells me more in five minutes than a 30-minute interview."

**Section 3: "The Compounding Effect" (h2)**
- Point: open source compounds. Each project builds on the last. Agent Watch informed Health Agents, which informed PM-OS. The public history of that evolution is itself a signal.
- Include a `visual-flow` component: Agent Watch -> Health Agents -> The Cabinet -> PM-OS (mark PM-OS as `.active`)
- Discuss how this public trail creates inbound: people find your work, reach out, collaborate, hire. The resume becomes a pull mechanism instead of a push document.

**Section 4: "What This Means for Hiring and Investing" (h2)**
- For hiring managers: look at what candidates have shipped, not just what they claim. A well-maintained open source project is a better signal than a take-home assignment.
- For angel investors (reference your interest in angel investing): the founder's GitHub tells you about execution speed, taste, and follow-through.
- Include a `visual-framework` (numbered list, 4 items):
  1. **Problem Selection**: Did they pick a real problem or a toy one?
  2. **Solution Quality**: Is the code clean? Is the architecture sound?
  3. **Communication**: Is the README clear? Could a stranger use it?
  4. **Maintenance**: Do they respond to issues? Ship updates?

**Section 5: "How to Start" (h2)**
- Practical advice: start with a tool you wish existed. Build the minimum version. Write a clear README. Ship it. Iterate based on real feedback.
- Point: the bar is lower than people think. You do not need a viral repo. You need one project that shows you can think clearly and ship.
- Close with a strong opinion: the builders who win in the next decade are the ones who build in public now.

**Article footer:**
- Author: "Written by Shaan Agara"
- Bio: "Director of Product at PointClickCare. Stanford AI. Building open-source AI tools for product leaders and decision-makers."
- "Back to all posts" link: `<a href="./">` with left arrow
- Prev/Next nav: Prev = none (first post), Next = "HIPAA and AI Agents" linking to `hipaa-ai-agents.html`

- [ ] **Step 2: Verify in browser**

Open `http://localhost:8080/blog/open-source-new-resume.html`. Verify:
- Nav bar renders correctly with working links
- Article header: date, title, subtitle, tags all display
- Article body: all 5 sections render with correct typography
- Visual components: comparison cards, callout, flow diagram, framework list all render
- Article footer: author line, back link, next post link
- Site footer renders
- Mobile responsive: resize browser to verify single-column layout

- [ ] **Step 3: Commit**

```bash
cd /tmp/shaan-website
git add blog/open-source-new-resume.html
git commit -m "feat: add blog post - Open Source Is the New Resume"
```

---

### Task 5: Write blog post 2 - HIPAA and AI Agents

**Files:**
- Create: `blog/hipaa-ai-agents.html`

**This task is independent of Tasks 4, 6-9 and can run in parallel with them.**

- [ ] **Step 1: Create the blog post file**

Create `blog/hipaa-ai-agents.html` as a complete HTML page. Same structural template as Task 4.

**SEO metadata:**
- Title: `HIPAA and AI Agents: Healthcare's Hardest Unsolved Problem | Shaan Agara`
- Meta description: `AI agents in healthcare hit a compliance wall most builders ignore. The 18 Safe Harbor identifiers, why current frameworks fail, and what compliant agent orchestration requires.`
- Canonical: `https://shaanagara.com/blog/hipaa-ai-agents.html`
- OG type: `article`
- JSON-LD datePublished: `2026-04-03`

**Article header:**
- Meta: `APRIL 3, 2026 · 10 MIN READ`
- Title: `HIPAA and AI Agents: Healthcare's Hardest Unsolved Problem`
- Subtitle: `Everyone is building AI agents. Almost nobody is thinking about what happens when those agents touch patient data.`
- Tags: Healthcare, AI, Compliance

**Article content (~2000 words). Section structure:**

**Section 1: "The Agent Explosion Meets Healthcare" (h2)**
- AI agents are proliferating across industries. In healthcare, the potential is enormous: clinical decision support, prior authorization automation, patient communication, care coordination.
- But healthcare has HIPAA. And HIPAA was written for a world where humans handle data, not autonomous agents that can loop, branch, and make API calls without human oversight.
- The gap between what agents can do and what compliance allows is where most healthcare AI projects die.

**Section 2: "The 18 Identifiers Nobody Remembers" (h2)**
- HIPAA's Safe Harbor method defines 18 types of Protected Health Information (PHI) that must be de-identified.
- Include a `visual-grid` component showing all 18 identifiers: Names, Geographic data, Dates, Phone numbers, Fax numbers, Email addresses, SSN, Medical record numbers, Health plan beneficiary numbers, Account numbers, Certificate/license numbers, Vehicle identifiers, Device identifiers, Web URLs, IP addresses, Biometric identifiers, Full-face photos, Any other unique identifier
- Point: most AI developers know about names and SSNs. Few realize that dates, geographic data smaller than a state, and device identifiers all count. An agent that logs a patient's zip code in a debug trace just created a HIPAA violation.

**Section 3: "Why Current Frameworks Fail" (h2)**
- Most agent frameworks (LangChain, CrewAI, AutoGen) are general-purpose. They have no concept of PHI, no built-in detection, no audit logging that meets HIPAA's requirements.
- Include a `visual-comparison`:
  - Left: "GENERAL-PURPOSE AGENTS" / No PHI awareness, Logs may contain PHI, No access control on data, Audit trails optional, Compliance is the developer's problem
  - Right: "HIPAA-COMPLIANT AGENTS" / PHI detection at every boundary, Redacted logging by default, Role-based data access, Immutable audit trails, Compliance is built into the framework
- The result: developers build agents, deploy them in healthcare settings, and only discover the compliance gaps after a breach or audit.

**Section 4: "What Compliant Agent Orchestration Looks Like" (h2)**
- Reference Health Agents (your open-source project). Describe the three pillars: PHI detection, role-based access control, and immutable audit logging.
- Include a `visual-flow`: Data Input -> PHI Detection (18 identifiers) -> Access Control (role check) -> Agent Processing -> Audit Log -> Output (mark PHI Detection as `.active`)
- Explain: PHI detection runs at every boundary, not just input. If an agent generates text that contains PHI, it gets caught before it reaches a log, an API call, or another agent.
- Point: this is not a nice-to-have. It is the minimum bar for any agent touching healthcare data.

**Section 5: "The Path Forward" (h2)**
- Healthcare needs agent frameworks built with compliance as a first principle, not an afterthought.
- Include a `visual-callout`: "The question is not whether AI agents will transform healthcare. They will. The question is whether we build the compliance infrastructure before or after the first major breach."
- Close: the builders who solve this problem, who make compliant agent orchestration as easy as spinning up a general-purpose agent, will define the next era of healthcare technology. That is why Health Agents exists as an open-source project. The problem is too important to be proprietary.

**Article footer:**
- Same author block as Task 4
- Prev: "Open Source Is the New Resume" linking to `open-source-new-resume.html`
- Next: "Shipping Side Projects Made Me a Better Product Leader" linking to `shipping-side-projects.html`

- [ ] **Step 2: Verify in browser**

Open `http://localhost:8080/blog/hipaa-ai-agents.html`. Verify all sections, visuals (grid of 18 identifiers, comparison, flow diagram, callout), nav, and footer render correctly. Check mobile responsiveness.

- [ ] **Step 3: Commit**

```bash
cd /tmp/shaan-website
git add blog/hipaa-ai-agents.html
git commit -m "feat: add blog post - HIPAA and AI Agents"
```

---

### Task 6: Write blog post 3 - Shipping Side Projects Made Me a Better Product Leader

**Files:**
- Create: `blog/shipping-side-projects.html`

**This task is independent of Tasks 4-5, 7-9 and can run in parallel with them.**

- [ ] **Step 1: Create the blog post file**

Create `blog/shipping-side-projects.html` as a complete HTML page. Same structural template as Task 4.

**SEO metadata:**
- Title: `Shipping Side Projects Made Me a Better Product Leader | Shaan Agara`
- Meta description: `Building open-source AI tools outside of work sharpened my product instincts more than any framework. The build-ship-learn loop applied to career growth.`
- Canonical: `https://shaanagara.com/blog/shipping-side-projects.html`
- OG type: `article`
- JSON-LD datePublished: `2026-04-05`

**Article header:**
- Meta: `APRIL 5, 2026 · 8 MIN READ`
- Title: `Shipping Side Projects Made Me a Better Product Leader`
- Subtitle: `The best product lessons I've learned didn't come from a framework, a book, or a meeting. They came from building things on my own.`
- Tags: Product, Leadership, Building

**Article content (~2000 words). Section structure:**

**Section 1: "The Build-Ship-Learn Loop" (h2)**
- As a product leader by day, you live in the world of roadmaps, prioritization, and stakeholder alignment. These are real skills. But they can create a distance from the act of building.
- Side projects collapse that distance. You are the PM, the engineer, the designer, and the user. Every decision is yours, and every consequence is immediate.
- Include a `visual-flow` (circular feel): Build -> Ship -> Learn -> Build (mark all as regular, show the loop nature)
- This loop, running fast and on your own terms, teaches product intuition in a way that no amount of strategy work can replicate.

**Section 2: "What Each Project Taught Me" (h2)**
- Walk through specific lessons from each project:

**Agent Watch** (h3):
- Lesson: Start with the smallest useful thing. Agent Watch is two decorators and a CLI. No dashboard, no cloud service, no config files. The constraint of "what is the absolute minimum?" forced better product decisions than any prioritization framework.
- Include a `visual-callout`: "The best V1 is the one that makes the user say 'finally' instead of 'interesting.'"

**Health Agents** (h3):
- Lesson: Compliance is a product feature, not a roadblock. Building HIPAA-compliant agent orchestration taught you that the hardest constraints produce the clearest product decisions. When you cannot store PHI in logs, the architecture designs itself.

**PM-OS** (h3):
- Lesson: Systems beat features. PM-OS is 27 skills, but the real product is the knowledge system that compounds over time. Building it taught you that the most valuable product work is often invisible: the connections between features, not the features themselves.

**Section 3: "Why This Makes You Better at Your Day Job" (h2)**
- Three specific ways side projects improve product leadership:
- Include a `visual-framework` (numbered list, 3 items):
  1. **Speed of judgment**: When you ship your own products, you develop intuition for what works before you have data. This translates directly to faster, better prioritization at work.
  2. **Technical empathy**: Building forces you to understand the real cost of decisions. "Can we just add a small feature?" lands differently when you have recently been the one implementing it.
  3. **User obsession**: When your side project has zero marketing budget, the only growth channel is building something people actually want. That discipline carries over.

**Section 4: "How to Start Shipping" (h2)**
- Practical advice: find a problem you personally experience. Build the smallest possible solution. Ship it publicly. Write about what you learned. Repeat.
- Point: the goal is not to build a startup. The goal is to stay in the builder's seat often enough that your product instincts stay sharp.
- Include a `visual-metric` component:
  - "6" / "Projects shipped in 12 months"
  - "2" / "Decorators (Agent Watch's entire API)"
  - "27" / "Skills in PM-OS"
- Close: the best product leaders I know are the ones who still build. Not because they have to, but because the loop of building, shipping, and learning is the fastest way to get better at the thing they do every day.

**Article footer:**
- Same author block as Task 4
- Prev: "HIPAA and AI Agents" linking to `hipaa-ai-agents.html`
- Next: "The PM's New Stack" linking to `pm-new-stack-ai-os.html`

- [ ] **Step 2: Verify in browser**

Open `http://localhost:8080/blog/shipping-side-projects.html`. Verify all sections, visuals (flow diagram, callout, framework, metrics), nav, and footer render correctly. Check mobile responsiveness.

- [ ] **Step 3: Commit**

```bash
cd /tmp/shaan-website
git add blog/shipping-side-projects.html
git commit -m "feat: add blog post - Shipping Side Projects Made Me a Better Product Leader"
```

---

### Task 7: Write blog post 4 - The PM's New Stack

**Files:**
- Create: `blog/pm-new-stack-ai-os.html`

**This task is independent of Tasks 4-6, 8-9 and can run in parallel with them.**

- [ ] **Step 1: Create the blog post file**

Create `blog/pm-new-stack-ai-os.html` as a complete HTML page. Same structural template as Task 4.

**SEO metadata:**
- Title: `The PM's New Stack: Why I Built an AI Operating System for Product Managers | Shaan Agara`
- Meta description: `PM workflows are ripe for AI augmentation. The story behind PM-OS: 27 AI skills, a compounding knowledge system, and why it changes how product managers work.`
- Canonical: `https://shaanagara.com/blog/pm-new-stack-ai-os.html`
- OG type: `article`
- JSON-LD datePublished: `2026-04-07`

**Article header:**
- Meta: `APRIL 7, 2026 · 10 MIN READ`
- Title: `The PM's New Stack: Why I Built an AI Operating System for Product Managers`
- Subtitle: `PM workflows are ripe for AI augmentation. Here's the story behind PM-OS and why the knowledge system matters more than any single skill.`
- Tags: Product, AI, Tools

**Article content (~2200 words). Section structure:**

**Section 1: "The Tool Fragmentation Problem" (h2)**
- PMs use dozens of tools: Jira for tickets, Notion for specs, Linear for sprints, Figma for designs, Google Slides for presentations, Slack for communication, spreadsheets for prioritization.
- None of them talk to each other. Every workflow starts from scratch. Context is lost between tools. The PM's job is increasingly about moving information between systems rather than making product decisions.
- Include a `visual-metric`:
  - "12+" / "Tools in the average PM's stack"
  - "0" / "That share context with each other"
  - "40%" / "Time spent on information transfer"

**Section 2: "What If the Stack Was One System?" (h2)**
- That question led to PM-OS. Not a single tool to replace them all, but an AI layer that sits on top and connects the workflows.
- PM-OS is a Claude Code plugin with 27 skills covering the full PM lifecycle: discovery, strategy, user research, spec writing, prioritization, roadmapping, sprint planning, launch, measurement, and communication.
- Include a `visual-grid` component showing skill categories: Discovery (3), Strategy (3), User Research (3), Define (3), Plan (3), Deliver (2), Communicate (3), Measure (2), Present (1), Cadence (1)
- Each number represents the count of skills in that category.

**Section 3: "The Knowledge System Is the Product" (h2)**
- The 27 skills are useful on their own. But the real product is the knowledge directory that every skill reads from and writes to.
- When you run competitive intel, the output feeds into strategy. Strategy feeds into OKRs. OKRs feed into prioritization. Prioritization feeds into roadmaps. Each skill compounds on the last.
- Include a `visual-flow`: Competitive Intel -> Strategy -> OKRs -> Prioritization -> Roadmap -> Sprint Scope (mark "Strategy" and "Roadmap" as `.active`)
- Point: most AI tools are stateless. You prompt, you get output, and the context vanishes. PM-OS is stateful. The knowledge system means every skill gets smarter as you use the system. That is the difference between a tool and an operating system.

**Section 4: "How It Works in Practice" (h2)**
- Walk through a real workflow: You are planning Q3.
- You run `/competitive-intel` on three competitors. The outputs land in `knowledge/competitors/`.
- You run `/write-strategy`. It reads the competitor data, your current OKRs, and your product context. It produces a strategy doc in `knowledge/strategy.md`.
- You run `/prioritize`. It reads the strategy, pulls in your backlog, and runs RICE scoring aligned to your OKRs. Output goes to `knowledge/priorities/`.
- You run `/quarterly-plan`. It reads strategy, priorities, and team capacity. It produces a quarter plan.
- Include a `visual-code` component showing a terminal session:
  ```
  $ /competitive-intel Linear
  > Analyzing linear.app...
  > Battlecard saved to knowledge/competitors/linear.md

  $ /write-strategy
  > Reading competitors, OKRs, product context...
  > Strategy draft saved to knowledge/strategy.md

  $ /prioritize
  > Running RICE scoring against strategy...
  > Ranked priorities saved to knowledge/priorities/q3-2026.md
  ```

**Section 5: "Why I Open-Sourced It" (h2)**
- PM-OS is free and MIT-licensed.
- The product management discipline has been underserved by AI. Most PM tools add a chatbot. PM-OS rethinks the entire workflow around AI-native primitives: skills that chain together, a knowledge system that compounds, and integrations that pull real data from your existing tools.
- Include a `visual-callout`: "The goal is not to replace product managers. It is to remove the busywork so PMs can focus on the decisions that actually matter."
- Close: if you are a PM, try it. If you build PM tools, study the knowledge system architecture. The future of PM tooling is not better features. It is better systems.

**Article footer:**
- Same author block as Task 4
- Prev: "Shipping Side Projects" linking to `shipping-side-projects.html`
- Next: "The Agent Cost Problem" linking to `agent-cost-problem.html`

- [ ] **Step 2: Verify in browser**

Open `http://localhost:8080/blog/pm-new-stack-ai-os.html`. Verify all sections, visuals (metrics, grid, flow, code block, callout), nav, and footer render correctly. Check mobile responsiveness.

- [ ] **Step 3: Commit**

```bash
cd /tmp/shaan-website
git add blog/pm-new-stack-ai-os.html
git commit -m "feat: add blog post - The PM's New Stack"
```

---

### Task 8: Write blog post 5 - The Agent Cost Problem

**Files:**
- Create: `blog/agent-cost-problem.html`

**This task is independent of Tasks 4-7, 9 and can run in parallel with them.**

- [ ] **Step 1: Create the blog post file**

Create `blog/agent-cost-problem.html` as a complete HTML page. Same structural template as Task 4.

**SEO metadata:**
- Title: `The Agent Cost Problem Nobody's Talking About | Shaan Agara`
- Meta description: `AI agents are powerful but expensive in unpredictable ways. Why observability for AI agents is the next critical infrastructure layer, and how Agent Watch solves it.`
- Canonical: `https://shaanagara.com/blog/agent-cost-problem.html`
- OG type: `article`
- JSON-LD datePublished: `2026-04-09`

**Article header:**
- Meta: `APRIL 9, 2026 · 9 MIN READ`
- Title: `The Agent Cost Problem Nobody's Talking About`
- Subtitle: `AI agents are getting powerful. They are also getting expensive in ways that are nearly impossible to predict without the right tools.`
- Tags: AI, Agents, Observability

**Article content (~2000 words). Section structure:**

**Section 1: "The Hidden Cost Curve" (h2)**
- A single API call to Claude or GPT-4 is cheap. Maybe $0.01 to $0.10. But an agent is not a single call.
- An agent loops. It reasons, calls tools, evaluates results, retries, branches. A simple "research this topic" task might make 15-40 API calls before it finishes. A complex multi-agent workflow can make hundreds.
- Include a `visual-comparison`:
  - Left: "SINGLE API CALL" / One request, one response / Cost: predictable / $0.01 to $0.10 per call / Linear scaling
  - Right: "AGENT WORKFLOW" / 15-40+ chained calls / Cost: unpredictable / $0.50 to $8.00+ per task / Exponential variance
- The cost of a single task is not the issue. The issue is that you have no idea what a task will cost until it is done.

**Section 2: "Why Existing Tools Don't Help" (h2)**
- Cloud provider dashboards show aggregate spend. Helpful for budget tracking, useless for debugging a specific agent run.
- LLM observability platforms (LangSmith, Helicone, etc.) focus on traces and latency. They can tell you what happened, but they are enterprise tools with complex setup and ongoing costs.
- What is missing: a simple, local-first way to see exactly what each agent run costs at the function level. No dashboard to deploy. No API keys to manage. No monthly bill for the observability tool itself.

**Section 3: "Agent Watch: Two Decorators, Zero Config" (h2)**
- This gap is why Agent Watch exists.
- Include a `visual-code` component:
  ```python
  from agent_watch import track_usage, monitor_agent

  @monitor_agent
  def research_agent(topic):
      # Your agent logic here
      result = call_llm(f"Research {topic}")
      sources = call_llm(f"Find sources for {result}")
      summary = call_llm(f"Summarize {sources}")
      return summary

  @track_usage
  def call_llm(prompt):
      return client.messages.create(
          model="claude-sonnet-4-20250514",
          messages=[{"role": "user", "content": prompt}]
      )
  ```
- Two decorators: `@track_usage` on your LLM calls, `@monitor_agent` on your agent function. That is the entire API.
- Agent Watch logs every call locally as JSONL. No data leaves your machine. No cloud service. No config files.
- Include a `visual-code` component showing output:
  ```
  $ agent-watch report

  Agent: research_agent
  Total runs: 47
  Avg cost per run: $1.23
  Max cost: $4.87
  Min cost: $0.34
  Total spend: $57.81

  Top cost drivers:
    call_llm (summarize): $23.40 (40.4%)
    call_llm (sources):   $19.12 (33.1%)
    call_llm (research):  $15.29 (26.4%)
  ```

**Section 4: "What Observability Reveals" (h2)**
- Once you can see costs at the function level, patterns emerge:
- Include a `visual-metric`:
  - "14x" / "Cost variance between cheapest and most expensive run"
  - "40%" / "Of total cost from a single function"
  - "3" / "Lines of code to add full observability"
- Discovery 1: Most agent cost is concentrated in 1-2 functions. Optimizing those functions (better prompts, caching, smaller models for simpler steps) can cut total cost by 50-70%.
- Discovery 2: The most expensive runs are usually the ones that loop. An agent that retries a failed tool call five times costs 5x more, but the failure is silent without observability.
- Discovery 3: Cost and quality are not correlated. The cheapest runs often produce the best results because they indicate the agent found the right path quickly.

**Section 5: "The Infrastructure Layer We Need" (h2)**
- Agent observability is going to be as essential as application monitoring.
- As agents move from demos to production, the question shifts from "can it work?" to "can it work within a cost envelope we can predict and control?"
- Include a `visual-callout`: "You would never deploy a web application without monitoring. We should not deploy agents without cost observability."
- Close: Agent Watch is open source and takes three lines to add to any Python project. But beyond this specific tool, the industry needs to treat agent cost observability as infrastructure, not an afterthought. The builders who instrument early will be the ones who can actually afford to run agents at scale.

**Article footer:**
- Same author block as Task 4
- Prev: "The PM's New Stack" linking to `pm-new-stack-ai-os.html`
- Next: "Your Product Roadmap Doesn't Account for AI Agents" linking to `your-product-roadmap-ai-agents.html`

- [ ] **Step 2: Verify in browser**

Open `http://localhost:8080/blog/agent-cost-problem.html`. Verify all sections, visuals (comparison, code blocks, metrics, callout), nav, and footer render correctly. Check mobile responsiveness.

- [ ] **Step 3: Commit**

```bash
cd /tmp/shaan-website
git add blog/agent-cost-problem.html
git commit -m "feat: add blog post - The Agent Cost Problem Nobody's Talking About"
```

---

### Task 9: Write blog post 6 - Your Product Roadmap Doesn't Account for AI Agents

**Files:**
- Create: `blog/your-product-roadmap-ai-agents.html`

**This task is independent of Tasks 4-8 and can run in parallel with them.**

- [ ] **Step 1: Create the blog post file**

Create `blog/your-product-roadmap-ai-agents.html` as a complete HTML page. Same structural template as Task 4.

**SEO metadata:**
- Title: `Your Product Roadmap Doesn't Account for AI Agents | Shaan Agara`
- Meta description: `Most product orgs treat AI as a feature, not an architecture shift. How product leaders should rethink roadmaps when agents can do the work features used to automate.`
- Canonical: `https://shaanagara.com/blog/your-product-roadmap-ai-agents.html`
- OG type: `article`
- JSON-LD datePublished: `2026-04-11`

**Article header:**
- Meta: `APRIL 11, 2026 · 9 MIN READ`
- Title: `Your Product Roadmap Doesn't Account for AI Agents`
- Subtitle: `Most product orgs are treating AI as a feature. It's an architecture shift, and your roadmap needs to reflect that.`
- Tags: AI, Product, Leadership

**Article content (~2000 words). Section structure:**

**Section 1: "The Feature Trap" (h2)**
- Every product roadmap I see has "AI" on it. Add a chatbot. Add auto-suggestions. Add a summarization feature. These are legitimate product decisions. But they are also incremental.
- The real shift is not adding AI features to existing products. It is rethinking what your product does when autonomous agents can handle entire workflows end-to-end.
- Include a `visual-comparison`:
  - Left: "AI AS FEATURE" / Bolt-on to existing UI / User-triggered / Single-step automation / Incremental improvement / Same product architecture
  - Right: "AI AS ARCHITECTURE" / Rethinks the workflow / Agent-triggered / Multi-step orchestration / Fundamental shift / New product architecture
- Most product teams are on the left. The market is moving to the right.

**Section 2: "What Agents Change About Products" (h2)**
- When agents can complete multi-step workflows autonomously, three things change about how products work:
- **Interfaces shrink.** If an agent can research, draft, review, and publish a report, the user does not need a 40-field form. They need a prompt and an approval step.
- **Workflows collapse.** A process that currently requires three different tools and manual handoffs becomes a single agent run. Products that exist primarily to bridge workflow gaps are at risk.
- **Value moves upstream.** The product's value shifts from executing the workflow to defining the goal and evaluating the output. Products that help users set objectives and judge results become more valuable than products that help users execute steps.
- Include a `visual-flow`: Features -> Workflows -> Agents -> Outcomes (mark "Agents" as `.active`)
- This is the evolution. Features automate steps. Workflows automate sequences. Agents automate goals. Outcomes are what users actually want.

**Section 3: "The Roadmap Rethink" (h2)**
- Here is how to update your product roadmap for an agent-first world:
- Include a `visual-framework` (numbered list, 4 items):
  1. **Audit for automation risk**: Which features on your roadmap exist to help users do something that an agent could do instead? If the answer is "most of them," your roadmap is building for a shrinking use case.
  2. **Identify the orchestration layer**: Where do users currently stitch together multiple steps manually? Those are your highest-value agent opportunities. Build the orchestration, not more features.
  3. **Design for delegation**: Every new feature should answer the question: "Can a user delegate this to an agent?" If yes, build the agent-friendly interface (APIs, structured inputs, clear evaluation criteria) alongside the human interface.
  4. **Build evaluation into the product**: As agents handle execution, users need better tools to evaluate output. Invest in comparison views, quality metrics, and approval workflows.

**Section 4: "A Real Example" (h2)**
- Consider a product management tool (something you know well).
- The traditional roadmap: add a better kanban board, improve sprint velocity charts, build a reporting dashboard.
- The agent-aware roadmap: build an agent that can scope a sprint from the backlog based on team capacity and OKR alignment. Build an agent that drafts a PRD from a one-paragraph brief. Build evaluation views where the PM reviews and approves agent-generated outputs.
- Include a `visual-comparison`:
  - Left: "TRADITIONAL PM TOOL ROADMAP" / Better kanban board / Sprint velocity charts / Reporting dashboard / Template library / Notification improvements
  - Right: "AGENT-AWARE PM TOOL ROADMAP" / Sprint scoping agent / PRD generation from briefs / Agent output evaluation views / Knowledge system for context / Approval and delegation workflows
- The second roadmap builds a fundamentally different product. One that gets more valuable as agents get more capable.

**Section 5: "Start Now" (h2)**
- You do not need to rewrite your entire roadmap today. Start with one exercise: look at every item on your current roadmap and ask, "Does this build something a user does, or something an agent could do?"
- If most of your roadmap is building things agents will do within 18 months, you have a problem. Not because the work is wasted, but because the half-life of that work just got much shorter.
- Include a `visual-callout`: "The best product roadmaps do not just plan for what users need today. They plan for a world where agents handle the execution and users focus on the decisions."
- Close: AI agents are not a future possibility. They are a present reality. The product leaders who adjust their roadmaps now, who build for an agent-first world, will define the next generation of software. The ones who keep adding AI features to existing architectures will be building for a market that no longer exists.

**Article footer:**
- Same author block as Task 4
- Prev: "The Agent Cost Problem" linking to `agent-cost-problem.html`
- Next: none (last post)

- [ ] **Step 2: Verify in browser**

Open `http://localhost:8080/blog/your-product-roadmap-ai-agents.html`. Verify all sections, visuals (comparisons, flow, framework, callout), nav, and footer render correctly. Check mobile responsiveness.

- [ ] **Step 3: Commit**

```bash
cd /tmp/shaan-website
git add blog/your-product-roadmap-ai-agents.html
git commit -m "feat: add blog post - Your Product Roadmap Doesn't Account for AI Agents"
```

---

### Task 10: Final verification and push

**Files:**
- All files created/modified in Tasks 1-9

- [ ] **Step 1: Run full site verification**

Start local server: `cd /tmp/shaan-website && python3 -m http.server 8080`

Verify the following pages load and render correctly:
1. `http://localhost:8080/` (homepage with nav, writing section, all existing content)
2. `http://localhost:8080/blog/` (listing page with 6 cards)
3. `http://localhost:8080/blog/open-source-new-resume.html`
4. `http://localhost:8080/blog/hipaa-ai-agents.html`
5. `http://localhost:8080/blog/shipping-side-projects.html`
6. `http://localhost:8080/blog/pm-new-stack-ai-os.html`
7. `http://localhost:8080/blog/agent-cost-problem.html`
8. `http://localhost:8080/blog/your-product-roadmap-ai-agents.html`

For each page verify:
- Nav bar renders with working links (brand links to homepage, Blog links to listing)
- Content displays correctly
- Visual components render (comparisons, flows, callouts, metrics, code, grids, frameworks)
- Footer renders
- Mobile responsive (resize to 375px width)

- [ ] **Step 2: Verify all internal links work**

Check every link on every page:
- Homepage "Blog" nav link -> blog listing
- Homepage blog cards -> individual posts
- Homepage "View all posts" -> blog listing
- Blog listing nav links -> homepage and blog listing
- Blog listing cards -> individual posts
- Blog post nav links -> homepage and blog listing
- Blog post "Back to all posts" -> blog listing
- Blog post prev/next links -> correct adjacent posts

- [ ] **Step 3: Validate HTML structure**

For each blog post, confirm:
- Correct `<title>` tag
- Meta description present and under 160 chars
- Canonical URL set correctly
- OG tags present (og:title, og:description, og:url, og:type, og:image)
- Twitter card tags present
- JSON-LD structured data block present with correct datePublished
- Semantic HTML used: `<article>`, `<header>`, `<time>`, `<footer>`

- [ ] **Step 4: Push to remote**

```bash
cd /tmp/shaan-website
git push origin master
```
