# Product Definition

## Vision

WI Docs is a universal document toolkit that makes common file operations accessible through one consistent web experience. It takes inspiration from the simplicity and task-oriented model of iLovePDF, while expanding beyond PDF into a broader ecosystem of document formats.

## Problem

People routinely move between disconnected tools to convert, edit, combine, optimize and prepare documents. WI Docs aims to centralize these workflows and make format compatibility and output quality understandable.

## Target users

- Students and educators managing assignments and study materials.
- Professionals preparing reports, proposals and business documents.
- Administrative teams handling forms, records and office files.
- Freelancers and small businesses exchanging documents with clients.
- Developers and knowledge workers transforming text and structured documents.

## Product pillars

### 1. Convert
Convert files between supported document formats while communicating possible layout, font, table, image and metadata changes.

### 2. Organize
Merge, split, reorder, rotate, extract or rearrange document pages and sections when the source format permits it.

### 3. Optimize
Compress documents, optimize embedded media and prepare files for storage or sharing.

### 4. Edit and design
Edit document content, page setup, styles, headers, footers, page numbering, watermarks and reusable templates.

### 5. Extract and transform
Extract text, images and metadata; support OCR for scanned documents as a separately tested capability.

### 6. Batch process
Apply compatible operations to multiple files and provide clear progress, errors and output downloads.

## Format strategy

Candidate formats:

- PDF
- Microsoft Word: DOCX and legacy DOC
- OpenDocument Text: ODT
- Rich Text Format: RTF
- Plain text: TXT
- Markdown: MD
- HTML
- Microsoft Excel: XLSX and legacy XLS
- Microsoft PowerPoint: PPTX and legacy PPT
- Images used as document input/output: PNG, JPEG, TIFF and WebP

This list is a product target, not a statement of current support. Every format must be mapped to individual operations with tested input/output fidelity.

## Current implemented baseline

The inspected code currently provides:

- Browser import of MD, TXT and DOCX.
- DOCX-to-HTML conversion using Mammoth.
- Markdown rendering using markdown-it.
- Text editing and live preview with page layout controls.
- Custom background images, page dimensions, margins, colors and font size.
- PDF rendering through Puppeteer.
- HTML output.
- A legacy Word-compatible output route that returns HTML labelled as MS Word, not a native DOCX package.

## Not yet established as implemented

The following remain product goals until source implementation and tests prove otherwise:

- PDF merge, split, compression, rotation and page extraction.
- Native DOCX/ODT/RTF/XLSX/PPTX export.
- OCR.
- Spreadsheet and presentation editing.
- Batch processing.
- Cloud storage, accounts, subscriptions or collaboration.
- Guaranteed offline processing.

## Experience principles

- Tool discovery should be simple and categorized by task.
- Uploads should show supported formats and limits before processing.
- Preserve originals and create a separate output.
- Show progress and actionable errors.
- Explain when a conversion may alter formatting.
- Provide privacy and retention information at the point of upload.
- Make accessibility, responsive layouts and localization first-class concerns.

## Success measures

- Successful conversion rate by operation and format pair.
- Output fidelity and document integrity.
- Median processing time and failure rate.
- User completion rate per tool.
- Upload-to-download conversion.
- Security incidents and unexpected retention events.
