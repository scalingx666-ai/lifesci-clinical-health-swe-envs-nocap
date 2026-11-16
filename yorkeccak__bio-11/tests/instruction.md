# Issue

**Title:** Add comprehensive SEO improvements

## Description

## Summary

- Add `robots.ts` with crawling rules that block `/api/` and `/auth/` paths
- Add `sitemap.ts` for core pages (home, privacy, terms)
- Add `manifest.json` for PWA support
- Update `layout.tsx` with comprehensive SEO metadata:
  - Improved title: "Bio AI Agent - Biomedical Deep Research | Valyu"
  - Keywords targeting: biomedical research AI, PubMed alternative, clinical trial search, FDA drug search, medical literature AI, drug discovery AI, ChEMBL, DrugBank, bioRxiv, medRxiv
  - JSON-LD SoftwareApplication schema for rich search results
  - Canonical URL configuration
  - Enhanced robots config with googleBot settings
  - Multi-size icon configuration
  - OpenGraph and Twitter card improvements with bio-screenshot.png

## Test plan

- [ ] Verify robots.txt is accessible at /robots.txt
- [ ] Verify sitemap.xml is accessible at /sitemap.xml
- [ ] Verify manifest.json is accessible at /manifest.json
- [ ] Check meta tags in page source
- [ ] Validate JSON-LD schema with Google Rich Results Test

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e7f2429a742`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.