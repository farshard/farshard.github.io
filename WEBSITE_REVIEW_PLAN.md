# Farshard Website Review Plan (ASCII RPG + Security + React Feasibility)

_Last updated: April 21, 2026._

## 1) Current state snapshot

The current Farshard site is a single static `index.html` page hosted on GitHub Pages, with inline CSS and no JavaScript runtime framework. This keeps deployment simple but creates maintainability and governance gaps as content grows.

## 2) ASCII RPG work integration plan

### Content updates
- Add a dedicated **ASCII RPG** mention in Products so visitors can discover the project from the homepage.
- Add a short explanation of why the ASCII RPG matters strategically (rapid prototyping, narrative systems validation, systems-first design).
- Link to the game repo/build/playable page once available.

### Navigation and structure
- Add a top-level nav link for `#ascii-rpg` (or a separate page if details become substantial).
- Add a project detail section with:
  - core gameplay loop,
  - current milestone status,
  - roadmap preview,
  - call-to-action (playtest/signup).

## 3) Security vulnerability catalog (current + likely)

Even as a static site, there are meaningful security and trust issues to address.

### High-priority gaps
1. **No security headers enforced at the edge**  
   Risk: weaker clickjacking/XSS hardening.  
   Improvement: enforce headers (especially CSP, X-Frame-Options/frame-ancestors, Referrer-Policy, Permissions-Policy, HSTS) through a CDN/proxy (e.g., Cloudflare) in front of GitHub Pages.

2. **No explicit Content Security Policy**  
   Risk: increased exposure if future scripts or third-party snippets are added.  
   Improvement: define a restrictive CSP now while the site is still simple.

3. **Placeholder and dead links (`href="#"`)**  
   Risk: trust erosion and phishing-pattern resemblance; accidental misuse later.  
   Improvement: replace with valid targets or remove until ready.

4. **Single-file inline styles**  
   Risk: weak change control/auditability; difficult to scale secure review workflows.  
   Improvement: externalize CSS and adopt linting/pre-commit checks.

### Medium-priority gaps
5. **No visible dependency/update process documentation**  
   Risk: unclear ownership for security maintenance as site grows.  
   Improvement: create a lightweight security maintenance checklist.

6. **No automated link and HTML validation in CI**  
   Risk: regressions and broken references over time.  
   Improvement: GitHub Actions for broken-link checks + HTML linting.

7. **Branding/legal freshness** (`© 2025`)  
   Risk: stale metadata can hurt credibility.  
   Improvement: keep copyright/year and legal links current.

## 4) Potential improvement backlog

### Short-term (1-2 weeks)
- Add ASCII RPG content block and clear CTA.
- Replace placeholder links.
- Externalize CSS into `/assets/styles/main.css`.
- Add `sitemap.xml` and improved `robots.txt` directives.
- Add basic CI checks: HTML lint + link checker.

### Mid-term (2-6 weeks)
- Add analytics with privacy-first configuration.
- Add security and incident contact docs (`SECURITY.md`).
- Add performance budgets (image compression, lazy loading if media grows).
- Add structured data (Organization/Product schema).

### Longer-term (6+ weeks)
- Move to component-based architecture (React or static-site framework).
- Add CMS/content pipeline for non-technical updates.
- Add multi-page docs/blog architecture.

## 5) React migration logistics and practicality

## Is React practical here?
Yes—if Farshard expects frequent updates, reusable components, richer interactions, and a growing product surface (e.g., ASCII RPG devlogs, changelogs, docs, media). For a minimal marketing page, plain static HTML remains cost-effective.

## Tradeoffs
### Benefits
- Reusable UI components and cleaner scaling.
- Better state handling for interactive product demos.
- Easier long-term team collaboration with typed/component workflows.

### Costs
- Build tooling complexity increases.
- More moving parts for CI/CD and dependency patching.
- Potential performance regressions if not optimized.

## Recommended approach
- Prefer **React + static export/build** (e.g., Vite) for GitHub Pages compatibility.
- Keep routing simple at first (single page or hash routing).
- Introduce TypeScript, ESLint, and minimal design tokens from day one.

## 6) GitHub Pages compatibility answer

**Yes — the website can still be hosted on GitHub Pages after moving to React.**

Implementation options:
1. Build React app into static assets (`dist/` or `build/`) and publish that folder via GitHub Actions.
2. Use HashRouter (or correct base path config) for client-side routes under project pages.
3. Keep custom domain via existing `CNAME` file.

Practical note:
- GitHub Pages does not run a Node server. React must be prebuilt to static files before deployment.

## 7) Proposed execution sequence

1. Update homepage with ASCII RPG section and link hygiene.
2. Add CI checks (HTML/link validation).
3. Externalize CSS and clean structure.
4. Add optional CDN/proxy layer for response security headers.
5. Decide on React migration after one milestone of content growth metrics.
