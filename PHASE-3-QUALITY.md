# Phase 3: Quality (Medium-Priority Issues)

**Timeline**: Week 3
**Total Effort**: 16 hours
**Expected Outcome**: Accessible website (WCAG 2.1 AA), consistent NAP across all pages, visitor analytics configured, updated citations

---

## Issue #10: Accessibility (WCAG 2.1 AA Compliance)

**Priority**: 🟡 MEDIUM
**Effort**: 6 hours
**Dependencies**: Phase 1 & Phase 2

### Problem
- Color contrast ratios on gold buttons and light gray backgrounds do not meet WCAG AA standards (minimum 4.5:1 for normal text).
- Interactive elements (buttons, links, form fields) lack proper focus states or aria-labels.
- Screen readers encounter missing `alt` attributes or non-semantic HTML structures on service/city pages.

### Solution
1. **Color Contrast**:
   - Adjust primary gold accent (`#D4AF37` / `#C5A028`) on white/light backgrounds to darker tones (`#997A15` or dark text) to ensure >4.5:1 contrast.
   - Maintain dark navy background (`#0A192F`) with light text for high contrast header/footer.
2. **Keyboard Navigation & Focus**:
   - Add explicit focus indicators (`:focus-visible` outline in CSS).
   - Ensure all modal elements, mobile navigation menus, and form inputs are fully accessible via Keyboard (`Tab` / `Shift+Tab` / `Enter` / `Space`).
3. **ARIA & Semantics**:
   - Add `aria-label` to icon-only buttons (phone links, social icons, mobile menu toggle).
   - Ensure header hierarchy follows logical order (`H1` -> `H2` -> `H3`) on every page without skipping levels.
4. **Validation**:
   - Run automated audits using axe-core / Lighthouse / WAVE tool.

### Acceptance Criteria
- [ ] 0 WCAG 2.1 AA errors on Lighthouse accessibility audit (score >= 95)
- [ ] Color contrast ratio >= 4.5:1 for standard text and >= 3:1 for large text
- [ ] Visible focus outlines on all interactive elements
- [ ] All forms and inputs labeled correctly with `<label>` and `id` bindings

---

## Issue #11: Fix NAP (Name, Address, Phone) Inconsistencies

**Priority**: 🟡 MEDIUM
**Effort**: 5 hours
**Dependencies**: Phase 1

### Problem
- Inconsistent NAP citations across pages:
  - Name variations: "AMY Electric", "A.M.Y. Electrical Service", "AMY Electrical Service"
  - Address variations: Winnetka, CA 91306 vs Los Angeles, CA
  - Phone format variations: `(818) 302-5614`, `818-302-5614`, `+18183025614`
- Impact: Confuses local search algorithms (Google Local Pack / Maps) and reduces local ranking signals.

### Solution
1. **Define Canonical NAP**:
   - **Business Name**: AMY Electric
   - **Address**: 20628 Londelius St, Winnetka, CA 91306
   - **Phone**: (818) 302-5614 (Tel link format: `tel:+18183025614`)
   - **Email**: info@amyelectric.com
   - **License**: C-10 #981578
2. **Audit & Standardize Site Header/Footer**:
   - Update standard header and footer partials/templates across all 76+ HTML pages.
3. **LocalBusiness Schema Alignment**:
   - Ensure `PostalAddress` in LocalBusiness JSON-LD schema matches canonical address precisely.

### Acceptance Criteria
- [ ] 100% of pages display identical canonical NAP details in header and footer
- [ ] Phone number formatted consistently `(818) 302-5614` with valid `tel:+18183025614` hrefs
- [ ] LocalBusiness JSON-LD schema on all pages matches exact canonical address and phone

---

## Issue #12: Analytics & Performance Tracking Setup

**Priority**: 🟡 MEDIUM
**Effort**: 2 hours
**Dependencies**: None

### Problem
- No visitor analytics or conversion tracking configured.
- Incapable of measuring organic landing page performance, form submission conversion rates, or bounce rates.

### Solution
1. **Cloudflare Web Analytics**:
   - Enable privacy-first Cloudflare Web Analytics token in site layout.
2. **Google Analytics 4 (GA4)**:
   - Add GA4 tracking snippet (`G-XXXXXXXXXX`) to header with privacy/cookie-consent considerations.
   - Configure custom conversion events:
     - `generate_lead` (on contact/estimate form submission)
     - `click_to_call` (on phone link clicks)
3. **Google Search Console**:
   - Verify domain ownership via DNS TXT record or HTML tag.

### Acceptance Criteria
- [ ] Cloudflare Web Analytics script tag active across all pages
- [ ] GA4 script loaded with active real-time tracking
- [ ] Lead submission & click-to-call custom events firing in GA4
- [ ] Google Search Console property verified and active

---

## Issue #13: Citation & Directory Links Update

**Priority**: 🟡 MEDIUM
**Effort**: 3 hours
**Dependencies**: Issue #11

### Problem
- External citations (Yelp, Google Business Profile, CSLB license lookup, BBB) link to old domain or inconsistent NAP details.

### Solution
1. Audit top citation platforms:
   - Google Business Profile
   - Yelp for Business
   - CSLB License Verification (License #981578)
   - Angi / HomeAdvisor / Houzz profiles
2. Update website URL in directory listings to canonical HTTPS domain (`https://amyelectric.com`).
3. Standardize NAP details across directory accounts.

### Acceptance Criteria
- [ ] Top local directories reflect unified canonical NAP
- [ ] Website links point directly to `https://amyelectric.com` without extra redirects
- [ ] CSLB license link verified and active on website footer

---

## Summary

**Phase 3 Completion Checklist**:
- [ ] WCAG 2.1 AA accessibility pass achieved (Lighthouse >= 95)
- [ ] Canonical NAP enforced across 100% of pages and schema
- [ ] GA4 & Cloudflare Web Analytics active with lead tracking
- [ ] External directory citations updated and verified

**Expected Outcome**: Fully accessible, local-SEO optimized website with active traffic and lead analytics.
