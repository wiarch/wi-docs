# Claude Code — WI Docs

## Project mission

Build WI Docs as a universal document toolkit inspired by iLovePDF, with support for many document formats and workflows—not a PDF-only utility.

The long-term product may include conversion, merge/split, compression, page organization, editing, OCR, extraction, templates, batch processing and document export. These are roadmap goals unless explicitly implemented and verified in source.

## Non-negotiable rules

1. Inspect the existing implementation before changing it.
2. Preserve existing behavior unless the task explicitly requests a change.
3. Do not claim a format or operation is supported until its implementation and output have been tested.
4. Keep the format/operation compatibility matrix up to date.
5. Treat uploaded documents as untrusted input.
6. Do not send document contents to external services without an explicit product decision and user disclosure.
7. Never expose server secrets in frontend code or `VITE_*` variables.
8. Use isolated, resource-limited processing for expensive or risky conversions.
9. Keep temporary files private and clean them up on success, failure and cancellation.
10. Prefer small, reviewable changes and add tests for conversion fidelity and security-sensitive behavior.

## Current stack

- Frontend: React 18, JavaScript, Vite 6, Tailwind CSS 3.
- Backend: Node.js, Express 4.
- PDF rendering: Puppeteer.
- Markdown parsing: markdown-it.
- DOCX import: Mammoth.

Root `package.json` contains API scripts. `client/package.json` contains frontend scripts.

## Current implementation boundaries

The current code imports Markdown, TXT and DOCX; converts DOCX to HTML with Mammoth; provides a live document editor/preview; and exposes HTML/PDF plus legacy Word-compatible HTML output routes.

Important limitation: `POST /api/generate-docx` currently sends HTML with an MS Word MIME type. It does not create a standards-compliant DOCX archive.

## Engineering workflow

- Read relevant components, utilities and server routes before editing.
- Keep document parsing, conversion, rendering and download responsibilities separated.
- Validate inputs on the server, even if the client validates them too.
- Add unit/integration tests for parsers and conversion adapters.
- Test malformed files, oversized files, unsupported formats and conversion failures.
- Run the frontend production build and API checks when relevant.
- Report exactly what was and was not tested.

## Security checklist

- HTML sanitization before browser rendering.
- Safe URL/resource handling; prevent SSRF and local-file access.
- CORS allowlist in production.
- Request and upload limits.
- Per-job timeouts and concurrency limits.
- Safe temporary directories and cleanup.
- No sensitive document content in logs.
- Dependency and Chromium updates.

See `docs/SECURITY.md` and `docs/ARCHITECTURE.md`.
