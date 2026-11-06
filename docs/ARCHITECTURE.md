# Architecture

## Current repository architecture

The current application has two main parts:

1. React/Vite client in `client/`.
2. Express API in root `server.js`.

### Client

- React 18 components compose the upload, editing, customization and preview experience.
- Vite 6 provides development and production bundling.
- Tailwind CSS 3 provides styling.
- Mammoth converts uploaded DOCX files to HTML in the browser.
- markdown-it renders Markdown for preview.

### API

- Express 4 exposes a health endpoint and document-generation routes.
- markdown-it renders Markdown.
- Puppeteer launches Chromium to render HTML and produce PDF.
- HTML output is returned directly.
- The current Word-compatible route returns HTML under an MS Word content type; it is not a native OOXML DOCX generator.

## Current request flow

1. User imports MD, TXT or DOCX in the client.
2. DOCX is converted to HTML using Mammoth; MD/TXT content is read as text.
3. User edits content and adjusts page presentation.
4. Client sends content and presentation settings to the API.
5. API builds HTML and, for PDF, renders it with Puppeteer.
6. Browser receives a generated file for download.

## Target architecture

As the product expands, separate the application into explicit layers:

- **Web client:** tool catalog, upload experience, operation configuration, progress, preview and downloads.
- **API gateway:** authentication if introduced, validation, rate limiting and job creation.
- **Tool registry:** declares each operation, accepted formats, output formats, limits and engine.
- **Conversion adapters:** isolated integrations for PDF, office, text, image and OCR engines.
- **Job workers:** process long-running tasks asynchronously with bounded resources.
- **Temporary file service:** private storage, random identifiers, retention and cleanup.
- **Result delivery:** authorized, expiring downloads and clear lifecycle states.
- **Observability:** operational metrics without logging document contents.

## Conversion adapter contract

Each adapter should declare:

- Supported input formats.
- Supported output formats.
- Operations supported.
- Required binaries/libraries.
- Maximum file size and resource requirements.
- Whether conversion is lossless or may alter layout.
- Timeout and cleanup behavior.
- Test fixtures and known limitations.

A central capability registry should drive both backend validation and frontend tool availability. Do not duplicate format support rules in multiple UI components.

## Processing lifecycle

Recommended job states:

`queued → validating → processing → completed | failed | cancelled | expired`

Every job should have:
- An opaque identifier.
- An owner or scoped access token if accounts exist.
- Input validation result.
- Operation and adapter version.
- Bounded execution time and resources.
- Output metadata.
- Expiration and cleanup timestamp.

## Security boundaries

Uploaded documents are untrusted. Conversion engines may parse complex archives, images, fonts, XML and HTML. Run them with least privilege, no unnecessary network access, restricted filesystem access, memory/CPU limits and timeouts.

Never pass user-controlled HTML directly to a browser renderer without sanitization and safe resource policies. Do not allow arbitrary URLs, local file paths or remote resource fetching from user content.

## Architectural evolution

Keep the existing React/Express baseline while extracting responsibilities incrementally. Avoid a full rewrite solely to add new formats. Introduce a job queue and worker isolation when processing duration, concurrency or engine risk justifies it.
