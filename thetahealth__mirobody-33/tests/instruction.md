# Issue

**Title:** fix: replace hardcoded CORS with configurable CORSMiddleware

## Description

## Summary

This PR replaces the hardcoded `Access-Control-Allow-Origin: *` CORS headers in the MCP service with a proper, configurable `CORSMiddleware` that reads from the existing `HTTP_HEADERS` config.

### Problem

The MCP service (`mirobody/mcp/service.py`) had hardcoded permissive CORS headers:

- **OPTIONS response**: `Access-Control-Allow-Origin: *`, `Access-Control-Allow-Methods: *`, `Access-Control-Allow-Headers: *`
- **405 response**: `Access-Control-Allow-Origin: *`

For a platform handling sensitive health and genetic data, this is a security risk. Users who deploy without modifying these defaults expose their data to cross-origin attacks. Additionally, `Access-Control-Allow-Origin: *` combined with `Access-Control-Allow-Credentials: true` is invalid per the CORS spec — browsers will reject it.

### Fix

1. **Removed hardcoded CORS headers** from `mirobody/mcp/service.py` OPTIONS and 405 responses.

2. **Configured `CORSMiddleware`** in `mirobody/server/server.py` from the existing `HTTP_HEADERS` config section. The middleware now handles CORS globally for all routes (including the MCP endpoint).

3. **Added startup warning** when `Access-Control-Allow-Origin: *` is configured with `Access-Control-Allow-Credentials: true` — this combination is invalid per the CORS spec.

4. **Updated `config.yaml`** example with secure defaults:
   - `Access-Control-Allow-Origin: 'http://localhost:18080'` (specific origin, not `*`)
   - `Access-Control-Allow-Methods: 'GET, POST, PUT, DELETE, OPTIONS'` (explicit, not `*`)
   - `Access-Control-Allow-Headers: 'Authorization, Content-Type'` (explicit, not `*`)
   - `Access-Control-Max-Age: '600'` (reduced from 86400)

### How it works

When `HTTP_HEADERS` is configured in `config.yaml`, the server extracts CORS-related headers and creates a `CORSMiddleware` instance. When `HTTP_HEADERS` is not configured (default), no CORS middleware is added — the server doesn't send any CORS headers, which is the secure default.

### Verification

- Syntax verified with Python 3.11 (codebase requires ≥3.11)
- No new pre-existing syntax errors introduced
- The `CORSMiddleware` import is from Starlette's built-in middleware (already a dependency)
- No tests exist in this repo, but the change follows Starlette's documented CORS middleware pattern

---

**About the Author:** Raphael Malikian — Clinical AI Solutions Architect. I specialise in building and fixing AI/ML systems for healthcare, including vector databases, RAG pipelines, and clinical NLP. If you need help with your project or think I can add value to your organisation, feel free to reach out — I'd love to connect.

📧 rtmalikian@gmail.com
🔗 GitHub: https://github.com/rtmalikian
🔗 LinkedIn: http://www.linkedin.com/in/raphael-t-malikian-mbbs-bsc-hons-71075436a

---

**Disclosure:** This code was developed with assistance from **mimo-2.5-pro** (Xiaomi) via **Hermes Agent** (Nous Research). All changes were reviewed, tested against the actual codebase, and verified for correctness.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b76bc5a546a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.