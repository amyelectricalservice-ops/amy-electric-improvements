# Phase 2: Content (High-Priority Issues)

**Timeline**: Week 2  
**Total Effort**: 34 hours  
**Expected Outcome**: Complete blog section, all images optimized, consistent schema markup

---

## Issue #6: Blog Posts Don't Exist

**Priority**: 🟠 HIGH  
**Effort**: 16 hours  
**Dependencies**: Phase 1 (single directory)

### Problem
- `blog/index.html` lists 39 blog article links
- **No actual blog post HTML files exist**
- All links return 404
- Lost SEO opportunity (33 indexable pages)
- Broken internal link structure

### Solution

Generate all 33 blog posts (1500–2000 words each). Use this template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Complete Guide to EV Charger Installation in LA | AMY Electric</title>
  <meta name="description" content="Step-by-step guide to EV charger installation, costs, permits, and rebates in Los Angeles. EVITP-certified.">
  <link rel="canonical" href="https://amyelectric.com/blog/complete-guide-ev-charger-installation">
  
  <!-- Standard header from other pages -->
  <!-- BlogPosting Schema -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "BlogPosting",
    "headline": "Complete Guide to EV Charger Installation in LA",
    "description": "Step-by-step guide...",
    "image": "https://amyelectric.com/img/blog/ev-charger-guide.jpg",
    "datePublished": "2026-09-13",
    "dateModified": "2026-09-13",
    "author": {
      "@type": "Person",
      "name": "Amram",
      "url": "https://amyelectric.com"
    },
    "publisher": {
      "@type": "Organization",
      "name": "AMY Electric",
      "logo": "https://amyelectric.com/img/logo.png"
    }
  }
  </script>
</head>
<body>
  <!-- Standard header/footer -->
  <main>
    <article>
      <h1>Complete Guide to EV Charger Installation in Los Angeles</h1>
      <p class="byline">By Amram | Published September 13, 2026 | Updated September 13, 2026</p>
      
      <h2>What You'll Learn</h2>
      <p>This guide covers everything homeowners need to know about installing an EV charger...</p>
      
      <!-- 1500–2000 words of content -->
      
      <h2>Related Articles</h2>
      <!-- Link to 3–5 related blog posts -->
      
      <section class="blog-cta">
        <h2>Ready to Install an EV Charger?</h2>
        <p>Get a free estimate from our licensed electricians.</p>
        <a href="/index#estimate" class="btn btn-gold">Request an Estimate →</a>
      </section>
    </article>
  </main>
</body>
</html>
```

### Blog Posts to Create

**From sitemap.xml** (priority 0.8 posts first):
1. Complete Guide to EV Charger Installation
2. Complete Guide to Electrical Panel Upgrades
3. Electrical Safety Checklist for Older LA Homes
4. Knob and Tube Wiring Replacement Guide
5. Electrical Permit Process in Los Angeles
6. How to Choose an LA Electrician
7. EV Charger Installation Cost in LA
8. Panel Upgrade Cost in Los Angeles
9. Whole-Home Rewiring Cost in LA
10. LADWP EV Charger Rebate Guide 2026

**Then fill in remaining 23 posts** (priority 0.6):
11. EV Charging Benefits
12. Panel Upgrade Signs
13. EV Charging in Los Angeles
14. EV Charger Installation Cost LA
15. Panel Upgrade Cost Los Angeles
16. EV vs Gas Vehicle Cost Los Angeles
17. Breaker Keeps Tripping Causes
18. ... (and 16 more)

### Content Guidelines
- **Length**: 1500–2000 words
- **Structure**: H1 title, intro, H2 sections (4–5), conclusion, CTA
- **Internal links**: 3–5 links to related service pages
- **FAQ section**: 3–5 Q&A in FAQPage schema
- **Images**: At least 1 relevant image
- **Schema**: BlogPosting + FAQPage
- **Call-to-action**: Link to estimate form

### Acceptance Criteria
- [ ] All 33 blog post files created
- [ ] Each post is 1500–2000 words
- [ ] All posts have BlogPosting schema (validated)
- [ ] All posts have internal links to service pages
- [ ] All posts have CTA footer
- [ ] All links in blog index are live (no 404s)
- [ ] Blog posts indexed in Google (check GSC after 2–3 days)

---

## Issue #7: Missing Image Assets

**Priority**: 🟠 HIGH  
**Effort**: 8 hours  
**Dependencies**: Phase 1 (directory structure)

### Problem
- HTML references: `img/hero-electrician.webp`, `img/og-home.jpg`, `img/gallery/*`
- **No images in repository**
- Pages render without hero images
- Social shares have no preview images
- Core Web Vitals impacted (LCP, CLS)

### Solution

1. **Create `img/` directory structure**:
```
img/
├── hero-electrician.jpg (1200×900)
├── hero-electrician.webp (1200×900)
├── hero-electrician-560x420.jpg (560×420)
├── hero-electrician-560x420.webp (560×420)
├── og-home.jpg (1200×630)
├── og-home.webp (1200×630)
└── gallery/
    ├── ev-charger-install-1.jpg
    ├── ev-charger-install-1.webp
    ├── panel-upgrade-1.jpg
    ├── panel-upgrade-1.webp
    ... (30 total gallery images)
```

2. **Image specifications**:
   - **Hero image**: Professional electrician working on panel (1200×900px, high-quality)
   - **OG image**: Company logo + branding (1200×630px, for social sharing)
   - **Gallery**: 30 photos of actual work (EV chargers, panel upgrades, lighting, commercial)
   - **Formats**: Both JPEG and WebP (Cloudflare Polish can convert, but include both)
   - **Optimization**: Use Squoosh.app or ImageOptim; target <100KB per image
   - **Alt text**: Descriptive, includes keywords (e.g., "Licensed electrician installing Tesla Wall Connector in Los Angeles garage")

3. **Implementation**:
   - Create all image files
   - Add to git
   - Verify paths in HTML match
   - Test responsive images with `srcset`
   - Verify Cloudflare Image Optimization enabled

### Image Checklist
- [ ] Hero images exist (JPEG + WebP, both sizes)
- [ ] OG images exist (JPEG + WebP)
- [ ] 30 gallery images added
- [ ] All images optimized (<100KB each)
- [ ] All alt text descriptive and keyword-rich
- [ ] Responsive images tested on mobile/desktop
- [ ] Cloudflare Image Optimization enabled
- [ ] Core Web Vitals improved (verify in Lighthouse)

---

## Issue #8: Build Automation Missing

**Priority**: 🟠 HIGH  
**Effort**: 4 hours  
**Dependencies**: None (parallel work)

### Problem
- `css/style.min.css` and `js/site.min.js` exist but no build scripts in git
- Instructions reference `scripts/build-css.py` and `scripts/build-js.py` but missing
- Can't validate or reproduce CSS/JS minification
- Changes to source files can't be built

### Solution

1. **Create `scripts/build-css.sh`**:
```bash
#!/bin/bash
set -e
echo "Building CSS..."
npx cleancss \
  -o css/style.min.css \
  css/style.css
echo "✅ CSS build complete: css/style.min.css"
```

2. **Create `scripts/build-js.sh`**:
```bash
#!/bin/bash
set -e
echo "Building JavaScript..."
npx terser \
  js/site.js \
  -o js/site.min.js \
  --compress \
  --mangle
echo "✅ JS build complete: js/site.min.js"
```

3. **Create `scripts/build.sh`** (master):
```bash
#!/bin/bash
set -e
echo "Running full build pipeline..."
bash scripts/build-css.sh
bash scripts/build-js.sh
echo "✅ Build complete!"
```

4. **Create `scripts/validate-html.sh`**:
```bash
#!/bin/bash
set -e
echo "Validating HTML..."
for file in *.html blog/*.html; do
  echo "Checking $file..."
  npx html-validate "$file" || exit 1
done
echo "✅ HTML validation complete!"
```

5. **Update `package.json`**:
```json
{
  "scripts": {
    "build": "bash scripts/build.sh",
    "build:css": "bash scripts/build-css.sh",
    "build:js": "bash scripts/build-js.sh",
    "validate": "bash scripts/validate-html.sh",
    "dev": "npm run build && npm run validate"
  },
  "devDependencies": {
    "clean-css-cli": "^5.6.2",
    "terser": "^5.19.2",
    "html-validator": "^7.2.0"
  }
}
```

6. **Commit to git**:
   - Add all scripts to `scripts/` directory
   - Add `package.json` with dependencies
   - Create `.gitignore` entry for `node_modules/`
   - Run locally to verify builds work

### Acceptance Criteria
- [ ] All scripts created in `scripts/`
- [ ] `package.json` has build scripts
- [ ] `npm install` runs without errors
- [ ] `npm run build` produces minified files
- [ ] `npm run validate` validates HTML
- [ ] Scripts are committed to git
- [ ] Documentation added to README

---

## Issue #9: Schema Markup Inconsistencies

**Priority**: 🟠 HIGH  
**Effort**: 6 hours  
**Dependencies**: Phase 1 (single directory)

### Problem
- Root `index.html`: Comprehensive LocalBusiness + Person + FAQPage schema (350+ lines)
- `amyelectric-site/index.html`: Simplified Electrician schema
- No BlogPosting schema on blog posts
- No HowTo schema on how-to content
- Inconsistent schema across pages confuses search engines

### Solution

Standardize schema on all pages:

**Homepage** (`index.html`):
```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "AMY Electric",
  "image": "https://amyelectric.com/img/og-home.jpg",
  "url": "https://amyelectric.com",
  "telephone": "+18183025614",
  "email": "info@amyelectric.com",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "20628 Londelius St",
    "addressLocality": "Winnetka",
    "addressRegion": "CA",
    "postalCode": "91306",
    "addressCountry": "US"
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.9",
    "reviewCount": "87"
  },
  "hasCredential": [
    {
      "@type": "EducationalOccupationalCredential",
      "name": "California C-10 License",
      "identifier": "981578"
    }
  ]
}
```

**Service pages** (e.g., `ev-charger-installation.html`):
```json
{
  "@context": "https://schema.org",
  "@type": "Service",
  "name": "EV Charger Installation",
  "provider": {
    "@type": "LocalBusiness",
    "name": "AMY Electric"
  },
  "areaServed": "Los Angeles, CA",
  "offers": {
    "@type": "Offer",
    "priceCurrency": "USD",
    "price": "500-1200"
  }
}
```

**Blog posts** (e.g., `blog/ev-charger-installation-guide.html`):
```json
{
  "@context": "https://schema.org",
  "@type": "BlogPosting",
  "headline": "Complete Guide to EV Charger Installation",
  "datePublished": "2026-09-13",
  "author": {
    "@type": "Person",
    "name": "Amram"
  },
  "publisher": {
    "@type": "Organization",
    "name": "AMY Electric"
  }
}
```

### Validation
- Run all pages through [Google Structured Data Tester](https://search.google.com/test/rich-results)
- Aim for: 0 errors, 0 warnings
- Test both desktop and mobile versions

### Acceptance Criteria
- [ ] All pages have appropriate schema markup
- [ ] Homepage: LocalBusiness schema complete
- [ ] Service pages: Service + Offer schema
- [ ] Blog posts: BlogPosting schema
- [ ] All city pages: LocalBusiness with geo coordinates
- [ ] All schema validates (0 errors, 0 warnings)
- [ ] Rich snippets appear in search results (2–3 weeks after)

---

## Summary

**Phase 2 Completion Checklist**:
- [ ] All 33 blog posts created and published
- [ ] All blog links live (0 404s)
- [ ] All images optimized and uploaded
- [ ] Hero/OG images displaying correctly
- [ ] Build scripts working (npm run build)
- [ ] All schema validated (0 errors)
- [ ] 76+ pages indexed in Google Search Console
- [ ] Sitemap shows all 76+ pages

**Expected Outcome**: Complete blog section, all visual content optimized, consistent schema across entire site. Ready for Phase 3 quality improvements.
