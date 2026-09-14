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

## 🎯 Improvement Roadmap - 4 Phases

### Phase 1: Foundation (Week 1) — **Critical Issues**
- Issue #1: Resolve directory structure
- Issue #2: Fix conflicting robots.txt
- Issue #3: Regenerate sitemap.xml
- Issue #4: Merge/close pending PRs
- Issue #5: Configure form backend

**Deliverable**: Single source-of-truth directory; working contact form; clean git history  
**Lead Time**: 5 work days

---

### Phase 2: Content (Week 2) — **High-Priority Issues**
- Issue #6: Generate blog posts (33 posts)
- Issue #7: Add image assets (5 hero + 30 gallery)
- Issue #8: Fix build automation scripts
- Issue #9: Standardize schema markup

**Deliverable**: Complete blog section; all images indexed; consistent schema  
**Lead Time**: 5 work days

---

### Phase 3: Quality (Week 3) — **Medium-Priority Issues**
- Issue #10: WCAG 2.1 AA compliance
- Issue #11: Fix NAP inconsistencies
- Issue #12: Set up analytics (Cloudflare + GA4)
- Issue #13: Update citations

**Deliverable**: Accessible site; consistent local SEO signals; visitor tracking  
**Lead Time**: 5 work days

---

### Phase 4: Automation (Week 4) — **Low-Priority Issues**
- Issue #14: Set up CI/CD pipeline (GitHub Actions)
- Issue #15: Create photo redaction workflow
- Issue #16: Automated license verification

**Deliverable**: Zero-touch deployments; automated quality gates; runbooks  
**Lead Time**: 5 work days

---

## 📊 Issue Tracking Matrix

| # | Title | Priority | Effort | Phase | Status |
|---|-------|----------|--------|-------|--------|
| 1 | Duplicate directory structure | 🔴 CRITICAL | 4 hrs | 1 | 📋 |
| 2 | Conflicting robots.txt | 🔴 CRITICAL | 1 hr | 1 | 📋 |
| 3 | Stale sitemap.xml | 🔴 CRITICAL | 2 hrs | 1 | 📋 |
| 4 | Unresolved PRs | 🔴 CRITICAL | 3 hrs | 1 | 📋 |
| 5 | Form backend | 🔴 CRITICAL | 2 hrs | 1 | 📋 |
| 6 | Blog posts missing | 🟠 HIGH | 16 hrs | 2 | 📋 |
| 7 | Image assets | 🟠 HIGH | 8 hrs | 2 | 📋 |
| 8 | Build automation | 🟠 HIGH | 4 hrs | 2 | 📋 |
| 9 | Schema inconsistencies | 🟠 HIGH | 6 hrs | 2 | 📋 |
| 10 | Accessibility (WCAG) | 🟡 MEDIUM | 6 hrs | 3 | 📋 |
| 11 | NAP inconsistency | 🟡 MEDIUM | 5 hrs | 3 | 📋 |
| 12 | Analytics missing | 🟡 MEDIUM | 2 hrs | 3 | 📋 |
| 13 | Citation URLs | 🟡 MEDIUM | 3 hrs | 3 | 📋 |
| 14 | CI/CD pipeline | 🟢 LOW | 8 hrs | 4 | 📋 |
| 15 | Photo redaction | 🟢 LOW | 4 hrs | 4 | 📋 |
| 16 | License verification | 🟢 LOW | 3 hrs | 4 | 📋 |
| **TOTAL** | | | **80 hrs** | **4 weeks** | |

---

## 🎯 Success Criteria

### After Phase 1 (Week 1):
- ✅ Single directory structure (root only)
- ✅ Form submissions working (5+ test submissions)
- ✅ Merged/closed all pending PRs
- ✅ Sitemap indexed in Google Search Console

### After Phase 2 (Week 2):
- ✅ All 76+ pages indexed in Google
- ✅ 33 blog posts published and linked
- ✅ All images loaded and optimized (<100KB each)
- ✅ Schema validation: 0 errors, 0 warnings

### After Phase 3 (Week 3):
- ✅ WCAG 2.1 AA compliant (Axe/WAVE pass)
- ✅ NAP consistent on 100% of pages
- ✅ Analytics tracking active (Cloudflare + GA4)
- ✅ All citations updated to new domain

### After Phase 4 (Week 4):
- ✅ GitHub Actions CI/CD deployed
- ✅ Automated tests running on every PR
- ✅ License verification running weekly
- ✅ Deployment runbook documented

---

## 📈 Expected Business Impact

| Metric | Current | Target | Improvement |
|--------|---------|--------|-------------|
| Indexed pages | 40 | 76+ | +90% |
| Organic traffic | Baseline | +40–60% | 3–5 new leads/week |
| Lead capture rate | ~30% (broken) | 85% (working) | +180% |
| Local pack visibility | Low | High | Top 3 ranking |
| Citation consistency | Poor | 100% | Better trust |
| Cost per lead | N/A | ~$2–5 | ROI >500% |

---

## 🚀 Getting Started

1. **Create GitHub Issues** from this plan (see [Issues tab](https://github.com/amyelectricalservice-ops/amy-electric-improvements/issues))
2. **Assign team members** and set deadlines
3. **Start Phase 1 immediately** (critical issues this week)
4. **Daily standup** to track progress
5. **Weekly review** with stakeholder

See individual GitHub Issues for detailed implementation guidance, code examples, and acceptance criteria.

---

**Last Updated**: September 14, 2026  
**Repository**: [amy-electric-site](https://github.com/amyelectricalservice-ops/amy-electric-site)  
**Plan Repo**: [amy-electric-improvements](https://github.com/amyelectricalservice-ops/amy-electric-improvements)
