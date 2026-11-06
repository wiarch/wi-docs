# Roadmap

This roadmap distinguishes the current baseline from proposed work. Items are not complete until implemented, tested and documented.

## Phase 0 — Product and engineering foundation

- [x] Identify current React + Express + Puppeteer baseline.
- [x] Document current import and export behavior.
- [ ] Remove obsolete ProGanadero documentation.
- [ ] Define supported format/operation matrix.
- [ ] Add automated frontend and API test foundations.
- [ ] Establish secure upload and HTML rendering rules.

## Phase 1 — Reliable document core

- [ ] Server-side file signature and content validation.
- [ ] Configurable upload size and request limits.
- [ ] HTML sanitization and safe resource policy.
- [ ] CORS allowlist and production configuration.
- [ ] Centralized error handling and structured operational logs.
- [ ] Temporary file lifecycle and cleanup policy.
- [ ] Conversion regression fixtures.

## Phase 2 — Core formats and conversions

- [ ] Native DOCX generation.
- [ ] RTF import/export.
- [ ] ODT import/export.
- [ ] PDF-to-text extraction.
- [ ] PDF/DOCX/ODT/RTF/TXT/MD/HTML conversion adapters.
- [ ] Per-conversion fidelity warnings and compatibility tests.

## Phase 3 — PDF toolkit

- [ ] Merge PDF files.
- [ ] Split by page range.
- [ ] Reorder and rotate pages.
- [ ] Extract selected pages.
- [ ] Compress and optimize PDF.
- [ ] Add/remove page numbers and watermarks.

## Phase 4 — Office and productivity tools

- [ ] Batch processing.
- [ ] Document templates and reusable presets.
- [ ] Metadata inspection and editing where safe.
- [ ] Spreadsheet conversion tools.
- [ ] Presentation conversion tools.
- [ ] Image-to-document and document-to-image tools.

## Phase 5 — Advanced capabilities

- [ ] OCR for scanned documents.
- [ ] Searchable PDF generation.
- [ ] Extract embedded images and attachments.
- [ ] Background job queue and worker isolation.
- [ ] Optional accounts and private history, subject to a privacy review.

## Release gates

A tool is ready only when it has:
- Explicit input/output format support.
- Validated limits and error handling.
- Tests for representative and malformed files.
- Security review appropriate to its parser/engine.
- Documented fidelity limitations.
- A user-facing description that matches actual behavior.
