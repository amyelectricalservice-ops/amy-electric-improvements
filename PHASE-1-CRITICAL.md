# Phase 1: Foundation (Critical Issues)

**Timeline**: Week 1  
**Total Effort**: 12 hours  
**Expected Outcome**: Single directory structure, working form, clean git history, valid SEO metadata

---

## Issue #1: Duplicate/Fragmented Site Structure

**Priority**: 🔴 CRITICAL  
**Effort**: 4 hours  
**Dependencies**: None

### Problem
- **Root files**: `index.html`, `ev-charger-installation.html`, etc.
- **Duplicate folder**: `amyelectric-site/index.html`, `amyelectric-site/ev-charger-installation.html`, etc.
- **Blog separate**: `blog/index.html`
- **Impact**: Duplicate content, maintenance burden, SEO confusion, unclear deployment target

### Solution
1. Identify which tree is production (likely root-level)
2. Backup `amyelectric-site/` folder (as archive branch)
3. Delete `amyelectric-site/` folder completely
4. Consolidate blog: move posts to `blog/post-name.html` (already correct structure)
5. Update `.gitignore`: Add `amyelectric-site/` to prevent accidental re-creation
6. Verify all links work after deletion
7. Test site locally

### Acceptance Criteria
- [ ] `amyelectric-site/` folder deleted from main branch
- [ ] All root-level files intact and functional
- [ ] `.gitignore` updated
- [ ] No broken links (run broken-link-checker)
- [ ] Site renders correctly at root domain

---

## Issue #2: Conflicting robots.txt

**Priority**: 🔴 CRITICAL  
**Effort**: 1 hour  
**Dependencies**: Issue #1 (delete amyelectric-site/)

### Problem
- **Root `robots.txt`** (50 lines): Comprehensive, blocks training crawlers (CCBot, Bytespider)
- **`amyelectric-site/robots.txt`** (11 lines): Minimal, allows all crawlers
- **Risk**: Training crawlers could use `amyelectric-site/*` paths for data harvesting

### Solution
1. Delete `amyelectric-site/robots.txt` (after issue #1)
2. Keep root `robots.txt` with comprehensive rules
3. Verify rules are correct:
   - Allow: `/` (default)
   - Disallow: `/api/`, `/reports/`, `/partials/`, `/~`
   - Allow AI indexing: GPTBot, ClaudeBot, OAI-SearchBot
   - Block training crawlers: CCBot, Bytespider, cohere-ai

### Acceptance Criteria
- [ ] Only root `robots.txt` exists
- [ ] `amyelectric-site/robots.txt` deleted
- [ ] Root robots.txt validated with Google robots.txt tester
- [ ] No errors or warnings in tester

---

## Issue #3: Stale sitemap.xml

**Priority**: 🔴 CRITICAL  
**Effort**: 2 hours  
**Dependencies**: Issue #1 (single directory)

### Problem
- **Root `sitemap.xml`**: Only 2 pages listed (200-amp-panel-upgrade, about), many blank lines
- **`amyelectric-site/sitemap.xml`**: Old `.html` extensions, 2025 dates
- **Current site**: Uses clean URLs (e.g., `/ev-charger-installation`, no `.html`)
- **Impact**: Google won't index modern pages; missed organic traffic

### Solution
1. Delete `amyelectric-site/sitemap.xml` (after issue #1)
2. Generate new root `sitemap.xml` with:
   - All 76+ pages (root + blog + cities)
   - Clean URLs (no `.html` extension)
   - Current `lastmod` dates (from git history)
   - Priority levels:
     - Homepage: 1.0
     - Service pages: 0.9
     - City pages: 0.7
     - Blog posts: 0.6
3. Validate at https://www.xml-sitemaps.com/validate-xml-sitemap.html
4. Submit to Google Search Console
5. Test with `curl https://amyelectric.com/sitemap.xml | head -20`

### Acceptance Criteria
- [ ] `sitemap.xml` contains all 76+ URLs
- [ ] URLs use clean paths (no `.html`)
- [ ] All `lastmod` dates are current (2026-09-13 or later)
- [ ] XML validates without errors
- [ ] Submitted to Google Search Console
- [ ] `robots.txt` references correct sitemap

---

## Issue #4: Unresolved Pull Requests

**Priority**: 🔴 CRITICAL  
**Effort**: 3 hours  
**Dependencies**: None (parallel work)

### Problem
- **PR #4** (7 days old): "Audit and improve site SEO, schema, and audit scripts" — 3 comments, unreviewed
- **PR #3** (47 days old): "Update name in Wrangler configuration" — Cloudflare bot, stale
- **PR #2** (21 May 2026): "Add Cloudflare Workers configuration" — not merged
- **Impact**: Unclear deployment pipeline, stale automation configurations

### Solution
1. **Review PR #4**:
   - Read all comments
   - If approved and no conflicts: Merge
   - If issues: Request changes or close
   - If superseded by this plan: Close with explanation

2. **Review PR #2 & #3**:
   - Confirm if Cloudflare Workers deployment is still needed
   - If yes and no conflicts: Merge both
   - If no: Close with explanation
   - Clarify deployment target (Cloudflare Pages vs. Workers)

3. **Establish PR review SLA**:
   - Minimum 24–48 hour review window
   - At least 1 approval before merge
   - Add branch protection rule to GitHub

### Acceptance Criteria
- [ ] PR #4 merged or closed (with explanation)
- [ ] PR #3 merged or closed
- [ ] PR #2 merged or closed
- [ ] Branch protection rule added (1 approval required)
- [ ] Clear deployment documentation in README

---

## Issue #5: Form Backend Not Configured

**Priority**: 🔴 CRITICAL  
**Effort**: 2 hours  
**Dependencies**: None (can be parallel)

### Problem
- **Form action**: `https://formspree.io/f/YOUR_FORM_ID` (placeholder never replaced)
- **Result**: All form submissions fail silently; leads are lost
- **Locations**: Multiple forms in `index.html` and service pages
- **Impact**: 0% lead capture from web forms

### Solution (Option A - Recommended: Cloudflare Pages Function)

1. Create `/functions/api/contact.ts`:
```typescript
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

  // Send email via SendGrid
  const emailResponse = await fetch('https://api.sendgrid.com/v3/mail/send', {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${context.env.SENDGRID_API_KEY}`,
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      personalizations: [
        { to: [{ email: 'info@amyelectric.com' }] },
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

2. Set up SendGrid (free tier available):
   - Sign up at https://sendgrid.com
   - Get API key
   - Add to Cloudflare Pages environment variables: `SENDGRID_API_KEY`

3. Update forms to post to `/api/contact`

### Solution (Option B - Quick: Formspree)

1. Sign up at https://formspree.io (free: 50 submissions/month)
2. Create new form → get form ID (e.g., `f_abc123xyz`)
3. Find/replace all form actions:
   ```html
   <!-- Before -->
   action="https://formspree.io/f/YOUR_FORM_ID"
   
   <!-- After -->
   action="https://formspree.io/f_abc123xyz"
   ```
4. Update all occurrences in:
   - `index.html` (line 284) — Quick form
   - `index.html` (line 821) — Estimate form
   - All service pages (similar pattern)
5. Test with test submission

### Acceptance Criteria
- [ ] Form backend configured (Cloudflare or Formspree)
- [ ] All form actions updated (no `YOUR_FORM_ID` placeholders)
- [ ] Test submissions received in info@amyelectric.com
- [ ] Form validation working (required fields)
- [ ] Success message displayed after submission
- [ ] No errors in browser console

---

## Summary

**Phase 1 Completion Checklist**:
- [ ] Directory consolidated (amyelectric-site/ deleted)
- [ ] robots.txt standardized
- [ ] sitemap.xml regenerated and submitted to GSC
- [ ] All PRs merged or closed
- [ ] Form backend working (5+ test submissions successful)
- [ ] No broken links (run link checker)
- [ ] Site renders correctly at root domain
- [ ] All SEO metadata valid (Google Search Console shows 0 errors)

**Expected Outcome**: Clean, consolidated site structure with working lead capture and valid SEO metadata. Ready for Phase 2 content creation.
