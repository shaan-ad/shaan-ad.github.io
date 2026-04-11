# Blog Pages Design Spec

## Overview

Add a blog to shaanagara.com with 6 initial posts, a blog listing page, and a homepage "Writing" section. No build tools. Static HTML + shared CSS on GitHub Pages.

## File Structure

```
shaanagara.com/
  index.html                                    (updated: nav bar, Writing section)
  styles.css                                    (new: shared styles extracted from index.html)
  blog/
    index.html                                  (blog listing page)
    open-source-new-resume.html                 (Apr 1)
    hipaa-ai-agents.html                        (Apr 3)
    shipping-side-projects.html                 (Apr 5)
    pm-new-stack-ai-os.html                     (Apr 7)
    agent-cost-problem.html                     (Apr 9)
    your-product-roadmap-ai-agents.html         (Apr 11)
```

## Architecture

**Approach:** Hybrid HTML + shared CSS file. All pages reference `styles.css` for base styles (reset, typography, colors, layout, nav, cards, footer, animations, responsive). Blog-specific styles (article typography, reading width, visual components) are inlined in blog pages since they only apply there.

**No build tools.** No JS framework. Plain HTML/CSS. GitHub Pages deploys on push.

## Shared CSS (`styles.css`)

Extract all existing styles from `index.html` into `styles.css`. Add nav bar styles. All pages (homepage, blog listing, blog posts) reference this file.

**Color tokens:**
- Dark: `#0f172a`
- Text: `#475569`
- Light text: `#94a3b8`
- Warm bg: `#faf8f5`
- Cream bg: `#f5f2ed`
- Card bg: `#f0ede8`
- Border: `#e2e8f0`
- Light border: `#f1f5f9`

**Fonts:**
- Headings: Inter (400, 500, 600, 700, 800)
- Body: Source Serif 4 (400, 500, 600, italic)
- Mono: JetBrains Mono (400, 500)

## Nav Bar (All Pages)

- Static (not sticky/fixed) bar at the top of every page
- Left: "Shaan Agara" (font-weight: 700, links to `/`). From blog pages, use relative path `../`
- Right: "Blog" (font-weight: 500, links to `/blog/`). From blog posts, use relative path `./` or `../blog/`
- Background: `#faf8f5`
- No border, no shadow
- Padding: `16px` vertical, same horizontal as `.container`

## Homepage Changes (`index.html`)

**Add nav bar** above the hero section.

**Add "Writing" section** between Projects and Footer:
- Background: `bg-cream` (`#f5f2ed`)
- Section label: "Writing" (same style as "What I build")
- 2-column card grid showing all 6 posts
- Each card contains:
  - Date: JetBrains Mono, small, uppercase, `#94a3b8`
  - Title: font-weight 800, `#0f172a`, letter-spacing -0.5px
  - Excerpt: Source Serif 4, `#475569`, 1-2 lines
  - Tags: pill-style spans (same as hero pills)
- Cards link to the individual blog post
- Below grid: centered "View all posts" button (`hero-link secondary` style), links to `/blog/`

**Update `index.html`** to reference `styles.css` instead of inline `<style>` block.

## Blog Listing Page (`blog/index.html`)

**Layout:**
- Nav bar at top
- Page header area (`bg-warm`):
  - Heading: "Writing" (same section-label style)
  - Subtitle: "Thoughts on AI, product leadership, and building in public." (Source Serif 4, `#475569`)
- Card grid area (white background):
  - 2-column grid, same card design as homepage Writing section
  - Sorted newest first
  - Each card links to the full blog post
- Footer: same as homepage

**SEO:**
- Title: `Blog | Shaan Agara`
- Meta description: `Articles on AI, product management, and leadership by Shaan Agara.`
- Canonical: `https://shaanagara.com/blog/`
- OG tags: title, description, url, type (website), image
- Twitter card tags

## Individual Blog Post Pages

**Layout (left-aligned editorial):**
- Nav bar at top
- Article header (max-width: 680px, centered on page, text left-aligned):
  - Date + reading time: JetBrains Mono, small, `#94a3b8` (e.g., "APRIL 11, 2026 . 8 MIN READ")
  - Title: font-size clamp(1.8rem, 1.5rem + 1vw, 2.5rem), font-weight 800, letter-spacing -1px, `#0f172a`
  - Subtitle: Source Serif 4, italic, `#475569`
  - Tags: pill-style spans
- Full-width divider: 1px `#e2e8f0`
- Article body (max-width: 680px, centered):
  - Body text: Source Serif 4, ~1.1rem, line-height 1.85, `#475569`
  - `<h2>` section headers: Inter, font-weight 700
  - `<h3>` sub-headers: Inter, font-weight 600
  - Rich HTML visuals (see Visual Components below)
- Article footer:
  - Author line: "Written by Shaan Agara" with one-line bio
  - "Back to all posts" link to `/blog/`
  - Previous/Next post navigation

**Semantic HTML:** `<article>`, `<header>`, `<section>`, `<time datetime="">`, `<footer>`

**SEO per post:**
- Title: `{Post Title} | Shaan Agara`
- Meta description: custom 150-160 char summary per post
- Canonical: `https://shaanagara.com/blog/{slug}.html`
- OG tags: title, description, url, type (article), image
- Twitter card: summary_large_image
- JSON-LD Article structured data:
  ```json
  {
    "@context": "https://schema.org",
    "@type": "Article",
    "headline": "Post Title",
    "author": { "@type": "Person", "name": "Shaan Agara" },
    "datePublished": "2026-04-01",
    "description": "Custom 150-160 char summary",
    "url": "https://shaanagara.com/blog/open-source-new-resume.html"
  }
  ```

## Visual Components (Blog Posts)

All visuals are pure HTML/CSS. No images, no JavaScript, no external dependencies.

**Comparison cards:** Side-by-side boxes contrasting two concepts. Grid layout, `#f0ede8` background, rounded corners.

**Flow diagrams:** Horizontal step progressions using flexbox. Styled boxes connected by arrows (`&#8594;`). Used for process or evolution sequences.

**Callout boxes:** Key insight or quote highlighted with a left border accent (`4px solid #0f172a`), light background, slightly indented.

**Data/metric highlights:** Large bold numbers (2-3rem) with descriptive labels below. Used for stats that anchor an argument.

**Code snippets:** `<pre><code>` blocks with `#f0ede8` background, JetBrains Mono font, rounded corners, horizontal scroll on overflow.

**Numbered frameworks:** Styled `<ol>` with custom counter styling for actionable takeaway lists.

**Section dividers:** Centered thin line or extra spacing between major sections.

## Blog Posts

### Post 1: Open Source Is the New Resume
- **Date:** April 1, 2026
- **Tags:** Open Source, Career, AI
- **Category:** AI Landscape
- **Angle:** In the age of AI, shipping real tools in public says more than credentials. Why builders who open-source are pulling ahead, and what that means for hiring, investing, and career strategy.
- **Visuals:** Comparison (old resume vs new resume), framework for evaluating open source projects, metric highlights on GitHub trends

### Post 2: HIPAA and AI Agents: Healthcare's Hardest Unsolved Problem
- **Date:** April 3, 2026
- **Tags:** Healthcare, AI, Compliance
- **Category:** AI Landscape
- **Angle:** AI agents in healthcare hit a compliance wall that most builders ignore. The 18 Safe Harbor identifiers, why current frameworks fail, and what it actually takes to build compliant agent orchestration.
- **Visuals:** The 18 Safe Harbor identifiers as a styled grid, flow diagram of PHI detection pipeline, comparison of compliant vs non-compliant approaches

### Post 3: Shipping Side Projects Made Me a Better Product Leader
- **Date:** April 5, 2026
- **Tags:** Product, Leadership, Building
- **Category:** AI + PM
- **Angle:** Building Agent Watch, Health Agents, and PM-OS outside of work sharpened product instincts more than any framework. The build-ship-learn loop applied to your own career.
- **Visuals:** Build-ship-learn loop diagram, timeline of side projects and lessons, callout boxes with specific product lessons

### Post 4: The PM's New Stack: Why I Built an AI Operating System for Product Managers
- **Date:** April 7, 2026
- **Tags:** Product, AI, Tools
- **Category:** AI + PM
- **Angle:** The story behind PM-OS. How PM workflows are ripe for AI augmentation, what 27 skills actually looks like in practice, and why the knowledge system matters more than any single skill.
- **Visuals:** PM workflow map (before/after AI), PM-OS skill categories as a visual grid, knowledge system architecture diagram

### Post 5: The Agent Cost Problem Nobody's Talking About
- **Date:** April 9, 2026
- **Tags:** AI, Agents, Observability
- **Category:** AI Landscape
- **Angle:** AI agents are getting powerful but expensive in ways that are hard to predict. Why observability for agents is the next critical infrastructure layer.
- **Visuals:** Cost comparison chart (single call vs agent loop), Agent Watch code snippet, metric highlights on cost variance, flow diagram of agent execution costs

### Post 6: Your Product Roadmap Doesn't Account for AI Agents
- **Date:** April 11, 2026
- **Tags:** AI, Product, Leadership
- **Category:** AI + PM
- **Angle:** Most product orgs are treating AI as a feature, not an architecture shift. How product leaders should rethink roadmaps when agents can do the work that features used to automate.
- **Visuals:** "AI as Feature" vs "AI as Architecture" comparison, roadmap evolution flow diagram (Features > Workflows > Agents), framework for agent-aware product planning

## Responsive Behavior

- Blog card grid: 2 columns above 900px, 1 column below
- Article body: max-width 680px, centered, with comfortable side padding on mobile
- Nav bar: stacks gracefully, maintains padding
- Visual components: stack vertically on mobile, comparison cards go single-column
- All existing responsive breakpoints from the current site carry over via `styles.css`

## What Does NOT Change

- Hero section content, layout, and links
- About section
- Projects section
- Footer content and layout (only gains consistent nav bar above)
- `shaan-agara.jpeg` and `CNAME`
