# AMY Electric Website Improvement Plan

**Repository**: [amy-electric-site](https://github.com/amyelectricalservice-ops/amy-electric-site)  
**Status**: Active Audit & Remediation  
**Last Updated**: September 14, 2026

---

## 📊 Executive Summary

The AMY Electric website is a well-designed static HTML site with strong SEO fundamentals (schema markup, responsive design, accessibility). However, **20 critical and medium-priority issues** prevent it from achieving full SEO potential and operational efficiency.

### Key Findings:
- ✅ **76 pages** (services, cities, blog) — comprehensive coverage
- ✅ **Rich schema markup** (LocalBusiness, Service, FAQPage)
- ✅ **Professional design** (navy + gold, responsive)
- ❌ **Duplicate file structure** (root + `amyelectric-site/` folder)
- ❌ **Blog posts don't exist** (39 links to non-existent pages)
- ❌ **Form backend broken** (Formspree ID never configured)
- ❌ **Sitemap stale** (only 2 pages listed)
- ❌ **No CI/CD pipeline** (3 unmerged PRs from automation bots)

**Estimated Impact**: Fixing these issues could increase organic traffic by **40–60%** and lead capture by **30–50%**.

---

## 📋 Quick Stats

| Category | Count | Status |
|----------|-------|--------|
| **Critical Issues** | 5 | 🔴 In Progress |
| **High-Priority Issues** | 6 | 🟠 Backlog |
| **Medium-Priority Issues** | 4 | 🟡 Backlog |
| **Low-Priority Issues** | 5 | 🟢 Backlog |
| **Total Work Items** | 20 | - |
| **Estimated Effort** | 80 hours | 4 weeks |

---

## 🎯 Improvement Roadmap

### Phase 1: Foundation (Week 1) — **Critical Issues**
- [ ] Resolve directory structure (consolidate root + `amyelectric-site/` folder)
- [ ] Fix form backend (configure Formspree or Pages Function)
- [ ] Merge/close pending PRs (resolve Workers configuration)
- [ ] Update robots.txt and regenerate sitemap.xml

**Deliverable**: Single source-of-truth directory; working contact form; clean git history  
**Lead Time**: 5 work days

---

### Phase 2: Content (Week 2) — **High-Priority Issues**
- [ ] Verify/generate all blog post HTML files (33 posts)
- [ ] Add image assets to `img/` directory (5 hero + 30 gallery)
- [ ] Audit and standardize schema markup across all pages
- [ ] Fix build automation scripts (commit CSS/JS build pipeline)

**Deliverable**: Complete blog section; all images indexed; consistent schema  
**Lead Time**: 5 work days

---

### Phase 3: Quality (Week 3) — **Medium-Priority Issues**
- [ ] Accessibility audit & WCAG 2.1 AA compliance
- [ ] Citation cleanup (Google Business, Yelp, CALeVIP, etc.)
- [ ] Analytics setup (Cloudflare + GA4)
- [ ] NAP consistency across all schema & directories

**Deliverable**: Accessible site; consistent local SEO signals; visitor tracking  
**Lead Time**: 5 work days

---

### Phase 4: Automation (Week 4) — **Low-Priority Issues**
- [ ] Set up CI/CD pipeline (GitHub Actions)
- [ ] Add automated testing (HTML validation, link checker, schema validator)
- [ ] Create deployment runbook and documentation
- [ ] Set up automated license verification

**Deliverable**: Zero-touch deployments; automated quality gates; runbooks  
**Lead Time**: 5 work days

---

## 🔴 Phase 1: Foundation Issues

### Issue #1: Duplicate/Fragmented Site Structure
**Priority**: CRITICAL  
**Effort**: 4 hours  
**Impact**: SEO, maintenance burden  

**Problem**:
- Root-level files: `index.html`, `ev-charger-installation.html`, etc.
- Parallel folder: `amyelectric-site/index.html`, `amyelectric-site/ev-charger-installation.html`, etc.
- Blog separate: `blog/index.html`

**Solution**:
1. Determine which tree is production (likely root-level)
2. Delete or archive `amyelectric-site/` folder
3. Consolidate blog posts into root structure: `blog/post-name.html`
4. Update `.gitignore` to prevent accidental re-creation

---

### Issue #2: Conflicting robots.txt
**Priority**: CRITICAL  
**Effort**: 1 hour  
**Impact**: AI crawlers, duplicate content  

**Problem**:
- Root `robots.txt`: Comprehensive (50 lines)
- `amyelectric-site/robots.txt`: Minimal (11 lines)
- Training crawlers may be allowed on `amyelectric-site/*`

**Solution**:
```robots
User-agent: *
Allow: /
Disallow: /api/
Disallow: /reports/
Disallow: /amyelectric-site/
Disallow: /partials/
Disallow: /~

# Allow AI indexing crawlers
User-agent: GPTBot
Allow: /

User-agent: ClaudeBot
Allow: /

# Block training crawlers
User-agent: CCBot
Disallow: /

User-agent: Bytespider
Disallow: /
```

---

### Issue #3: Stale sitemap.xml
**Priority**: CRITICAL  
**Effort**: 2 hours  
**Impact**: Search indexation  

**Problem**:
- Root `sitemap.xml`: Only 2 pages listed, many blank lines
- `amyelectric-site/sitemap.xml`: Old `.html` extensions, 2025 dates
- Current site uses clean URLs (no `.html`)

**Solution**:
1. Generate complete sitemap with all 76+ pages
2. Use correct URLs without `.html` extension
3. Update `lastmod` to current dates based on Git history
4. Set priorities: homepage (1.0), service pages (0.9), city pages (0.7), blog (0.6)
5. Submit to Google Search Console

---

### Issue #4: Unresolved Pull Requests
**Priority**: CRITICAL  
**Effort**: 3 hours  
**Impact**: CI/CD, deployment reliability  

**Problem**:
- PR #4 (7 days old): "Audit and improve site SEO, schema, and audit scripts" — 3 comments, unreviewed
- PR #3 (47 days old): "Update name in Wrangler configuration" — Cloudflare bot, stale
- PR #2 (21 May 2026): "Add Cloudflare Workers configuration" — not merged

**Solution**:
1. Review PR #4 → merge if approved, close if superseded
2. Review PR #2 & #3 → merge Cloudflare config or clarify Workers deprecation
3. Establish PR review SLA (24–48 hours)
4. Add branch protection rules requiring 1 approval before merge

---

### Issue #5: Form Backend Not Configured
**Priority**: CRITICAL  
**Effort**: 2 hours  
**Impact**: Lead capture  

**Problem**:
- Form points to `https://formspree.io/f/YOUR_FORM_ID` but `YOUR_FORM_ID` never replaced
- Form submissions fail silently; leads lost

**Solution - Option A (Recommended: Cloudflare Pages Function)**:
```javascript
// functions/api/contact.ts
export async function onRequest(context) {
  const { request } = context;
  
  if (request.method !== 'POST') {
    return new Response('Method not allowed', { status: 405 });
  }

  const formData = await request.formData();
  const name = formData.get('name');
  const phone = formData.get('phone');
  const email = formData.get('email') || 'no-reply@amyelectric.com';
  const service = formData.get('service');
  const message = formData.get('message');

  // Send email via SendGrid or Mailgun
  const emailResponse = await fetch('https://api.sendgrid.com/v3/mail/send', {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${context.env.SENDGRID_API_KEY}`,
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      personalizations: [
        {
          to: [{ email: 'info@amyelectric.com' }],
        },
      ],
      from: { email: 'noreply@amyelectric.com' },
      subject: `New Contact Form: ${name}`,
      html: `<p><strong>${name}</strong></p><p>Phone: ${phone}</p><p>Email: ${email}</p><p>Service: ${service}</p><p>${message}</p>`,
    }),
  });

  if (emailResponse.ok) {
    return new Response(JSON.stringify({ success: true }), {
      headers: { 'Content-Type': 'application/json' },
    });
  }

  return new Response(JSON.stringify({ error: 'Failed to send' }), {
    status: 500,
    headers: { 'Content-Type': 'application/json' },
  });
}
```

**Solution - Option B (Fallback: Formspree)**:
1. Sign up at https://formspree.io (free tier: 50 submissions/month)
2. Create new form → get form ID (e.g., `f_abc123xyz`)
3. Replace `YOUR_FORM_ID` in all forms: `action="https://formspree.io/f_abc123xyz"`

---

## See full detailed plan in [GitHub Issues](https://github.com/amyelectricalservice-ops/amy-electric-improvements/issues)

