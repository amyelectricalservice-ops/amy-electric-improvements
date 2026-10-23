# AMY Electric Website Improvement Plan

**Repository**: [amy-electric-site](https://github.com/amyelectricalservice-ops/amy-electric-site)  
**Status**: Active Audit & Remediation  
**Last Updated**: September 14, 2026

---

## 📊 Executive Summary

The AMY Electric website improvement plan addresses critical technical, SEO, content, quality, and deployment pipeline issues across the codebase.

### Key Findings:
- ✅ **76 pages** (services, cities, blog) — comprehensive coverage
- ✅ **Rich schema markup** (LocalBusiness, Service, FAQPage)
- ✅ **Professional design** (navy + gold, responsive)
- ❌ **Duplicate file structure** (root + `amyelectric-site/` folder)
- ❌ **Blog posts don't exist** (39 links to non-existent pages)
- ❌ **Form backend broken** (Formspree ID never configured)
- ❌ **Sitemap stale** (only 2 pages listed)
- ❌ **No CI/CD pipeline** (3 unmerged PRs from automation bots)

---

## 📋 Documentation Map

Detailed technical requirements, step-by-step implementation guidelines, and acceptance criteria are organized into 4 phase documents:

1. **[Phase 1: Foundation (Critical Issues)](./PHASE-1-CRITICAL.md)**
   - Issue #1: Duplicate directory structure resolution
   - Issue #2: Conflicting robots.txt cleanup
   - Issue #3: Sitemap.xml regeneration
   - Issue #4: Unresolved PRs triage
   - Issue #5: Form backend integration

2. **[Phase 2: Content (High-Priority Issues)](./PHASE-2-CONTENT.md)**
   - Issue #6: Blog posts generation (33 articles)
   - Issue #7: Missing image assets & gallery
   - Issue #8: Build automation scripts
   - Issue #9: Standardize JSON-LD schema markup

3. **[Phase 3: Quality (Medium-Priority Issues)](./PHASE-3-QUALITY.md)**
   - Issue #10: WCAG 2.1 AA accessibility compliance
   - Issue #11: Canonical NAP (Name, Address, Phone) consistency
   - Issue #12: Analytics setup (Cloudflare + GA4)
   - Issue #13: Citation updates & directory listings

4. **[Phase 4: Automation (Low-Priority Issues)](./PHASE-4-AUTOMATION.md)**
   - Issue #14: GitHub Actions CI/CD pipeline
   - Issue #15: Job photo redaction workflow & EXIF stripping
   - Issue #16: Automated CSLB license verification cron job

---

## 📊 Issue Tracking Matrix

| # | Title | Priority | Effort | Phase | Document |
|---|-------|----------|--------|-------|----------|
| 1 | Duplicate directory structure | 🔴 CRITICAL | 4 hrs | 1 | [PHASE-1-CRITICAL.md](./PHASE-1-CRITICAL.md) |
| 2 | Conflicting robots.txt | 🔴 CRITICAL | 1 hr | 1 | [PHASE-1-CRITICAL.md](./PHASE-1-CRITICAL.md) |
| 3 | Stale sitemap.xml | 🔴 CRITICAL | 2 hrs | 1 | [PHASE-1-CRITICAL.md](./PHASE-1-CRITICAL.md) |
| 4 | Unresolved PRs | 🔴 CRITICAL | 3 hrs | 1 | [PHASE-1-CRITICAL.md](./PHASE-1-CRITICAL.md) |
| 5 | Form backend | 🔴 CRITICAL | 2 hrs | 1 | [PHASE-1-CRITICAL.md](./PHASE-1-CRITICAL.md) |
| 6 | Blog posts missing | 🟠 HIGH | 16 hrs | 2 | [PHASE-2-CONTENT.md](./PHASE-2-CONTENT.md) |
| 7 | Image assets | 🟠 HIGH | 8 hrs | 2 | [PHASE-2-CONTENT.md](./PHASE-2-CONTENT.md) |
| 8 | Build automation | 🟠 HIGH | 4 hrs | 2 | [PHASE-2-CONTENT.md](./PHASE-2-CONTENT.md) |
| 9 | Schema inconsistencies | 🟠 HIGH | 6 hrs | 2 | [PHASE-2-CONTENT.md](./PHASE-2-CONTENT.md) |
| 10 | Accessibility (WCAG) | 🟡 MEDIUM | 6 hrs | 3 | [PHASE-3-QUALITY.md](./PHASE-3-QUALITY.md) |
| 11 | NAP inconsistency | 🟡 MEDIUM | 5 hrs | 3 | [PHASE-3-QUALITY.md](./PHASE-3-QUALITY.md) |
| 12 | Analytics missing | 🟡 MEDIUM | 2 hrs | 3 | [PHASE-3-QUALITY.md](./PHASE-3-QUALITY.md) |
| 13 | Citation URLs | 🟡 MEDIUM | 3 hrs | 3 | [PHASE-3-QUALITY.md](./PHASE-3-QUALITY.md) |
| 14 | CI/CD pipeline | 🟢 LOW | 8 hrs | 4 | [PHASE-4-AUTOMATION.md](./PHASE-4-AUTOMATION.md) |
| 15 | Photo redaction | 🟢 LOW | 4 hrs | 4 | [PHASE-4-AUTOMATION.md](./PHASE-4-AUTOMATION.md) |
| 16 | License verification | 🟢 LOW | 3 hrs | 4 | [PHASE-4-AUTOMATION.md](./PHASE-4-AUTOMATION.md) |
| **TOTAL** | | | **77 hrs** | **4 weeks** | |

---

## 🎯 Overall Success Criteria

- ✅ All 16 identified audit issues resolved across Phases 1 through 4.
- ✅ Site passes automated HTML validation, broken link checks, and schema validation.
- ✅ WCAG 2.1 AA accessibility compliance score >= 95 on Lighthouse.
- ✅ Direct deployment via GitHub Actions CI/CD to Cloudflare Pages.
