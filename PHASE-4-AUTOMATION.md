# Phase 4: Automation (Low-Priority Issues)

**Timeline**: Week 4
**Total Effort**: 15 hours
**Expected Outcome**: Automated CI/CD deployment pipeline, automated code quality & validation gates, photo redaction workflow, automated license verification

---

## Issue #14: CI/CD Pipeline (GitHub Actions)

**Priority**: 🟢 LOW
**Effort**: 8 hours
**Dependencies**: Phase 1 & Phase 2 (build scripts)

### Problem
- Deployment is manual or ad-hoc.
- Pull requests are not automatically validated for broken links, minification, schema validity, or HTML syntax.

### Solution
1. **GitHub Actions Workflow** (`.github/workflows/ci.yml`):
```yaml
name: CI & Deployment Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - name: Validate HTML & Build Assets
        run: |
          npm run build
          npm run validate
      - name: Check for Broken Links
        run: npx lychee --offline "*.html" "blog/*.html"

  deploy:
    needs: validate
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to Cloudflare Pages
        uses: cloudflare/pages-action@v1
        with:
          apiToken: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          accountId: ${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
          projectName: amy-electric-site
          directory: .
          gitBranch: main
```

### Acceptance Criteria
- [ ] GitHub Actions workflow triggers on PRs and pushes to `main`
- [ ] HTML validation and link checking run automatically on PRs
- [ ] Direct deployment to Cloudflare Pages on `main` merge
- [ ] Build status badge added to `README.md`

---

## Issue #15: Job Photo Redaction Workflow

**Priority**: 🟢 LOW
**Effort**: 4 hours
**Dependencies**: None

### Problem
- Worksite photos uploaded to gallery/blog may inadvertently contain customer address details, license plates, or private property details.

### Solution
1. **Script Workflow** (`scripts/redact-photos.py` or `.sh`):
   - Automatic metadata/EXIF stripping using `exiftool` or Python `Pillow`.
   - Inspection utility to auto-blur detected license plates/text boxes prior to WebP compression.
2. **Pre-commit Hook / Image Guidelines**:
   - Add image upload documentation in `docs/IMAGE-WORKFLOW.md`.
   - Run EXIF cleaner automatically during `npm run build`.

### Acceptance Criteria
- [ ] All gallery and hero images are stripped of EXIF geotags/metadata
- [ ] Photo submission guide published in `docs/IMAGE-WORKFLOW.md`
- [ ] Automated EXIF cleaning integrated into image build process

---

## Issue #16: Automated License Verification

**Priority**: 01 LOW
**Effort**: 3 hours
**Dependencies**: None

### Problem
- Contractor license status (California C-10 #981578) must remain active and in good standing on CSLB (Contractors State License Board).

### Solution
1. **License Verification Script** (`scripts/check-license.py`):
```python
import sys
import requests

def check_cslb_license(license_number):
    url = f"https://www.cslb.ca.gov/OnlineServices/CheckLicForm/LicenseDetail.aspx?LicNum={license_number}"
    response = requests.get(url, timeout=10)
    if "CLEAR" in response.text or "ACTIVE" in response.text:
        print(f"✅ License #{license_number} is ACTIVE and in good standing.")
        return True
    else:
        print(f"⚠️ Warning: Check license status for #{license_number}")
        sys.exit(1)

if __name__ == "__main__":
    check_cslb_license("981578")
```
2. **Weekly GitHub Action Cron Job**:
   - Schedule weekly run (`0 0 * * 1`) to query CSLB status and create an issue/alert if status changes.

### Acceptance Criteria
- [ ] `scripts/check-license.py` created and tested
- [ ] Weekly scheduled GitHub Action configured to monitor license status
- [ ] Automated notification configured upon status change

---

## Summary

**Phase 4 Completion Checklist**:
- [ ] GitHub Actions CI/CD pipeline active
- [ ] Automated HTML validation and link check on every PR
- [ ] Automated EXIF metadata removal on image assets
- [ ] Weekly CSLB license verification workflow active

**Expected Outcome**: Zero-touch deployment, automated quality gates, and automated monitoring for operational compliance.
