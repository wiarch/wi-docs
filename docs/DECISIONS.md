# Architecture Decision Records

## ADR-001 — Position WI Docs as a multi-format document toolkit

**Status:** Accepted

WI Docs will be developed as a universal document toolkit inspired by iLovePDF, but not limited to PDF. The product should organize operations around user tasks and expose only verified format/operation combinations.

## ADR-002 — Preserve the existing React and Express baseline

**Status:** Accepted

The current React 18, Vite 6 and Tailwind CSS 3 frontend with Node.js/Express 4 API remains the baseline. New capabilities should be introduced incrementally rather than forcing an unnecessary rewrite.

## ADR-003 — Treat format support as operation-specific

**Status:** Accepted

A format being importable does not mean it can be exported, edited, compressed or converted to every other format. Maintain a capability matrix per operation and test each combination.

## ADR-004 — Separate current capabilities from roadmap

**Status:** Accepted

Documentation and UI must distinguish implemented, experimental and planned functionality. In particular, the current Word-compatible endpoint returns HTML labelled as MS Word and must not be represented as native DOCX generation.

## ADR-005 — Uploaded documents are untrusted

**Status:** Accepted

All parsers and renderers must be protected with validation, sanitization, resource limits, isolation and cleanup. Document contents must not be logged or sent to third parties without an explicit product decision and user disclosure.

## ADR-006 — Preserve original inputs

**Status:** Accepted

Document operations should create new outputs by default. The original upload remains unchanged during processing, subject to the product's retention and deletion policy.
