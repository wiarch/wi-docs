# WI Docs

**A universal document toolkit — beyond PDF.**

WI Docs is envisioned as a web-based workspace for working with document files across formats. Inspired by the convenience of iLovePDF, it aims to bring conversion, editing, organization and document utilities together in one place—not just for PDF, but for a broad range of document formats.

> **Project status:** The current codebase is an early document-to-output application. The broader multi-format toolkit described here is the product direction, not a claim that every planned tool is already implemented.

## Current implementation

The repository currently contains a React interface and an Express API focused on document composition and export.

- Import Markdown (`.md`), plain text (`.txt`) and Word Open XML (`.docx`) files.
- Edit content in a text editor and preview the rendered document.
- Convert DOCX input to HTML using Mammoth.
- Customize page size, margins, page/content colors, typography and background imagery.
- Generate PDF output using Puppeteer.
- Generate HTML output.
- Generate legacy Word-compatible `.doc` output from HTML.
- Undo and redo recent content changes in the editor.

These capabilities describe the inspected code paths; they should not be interpreted as a guarantee of production readiness or complete format fidelity.

## Product vision

WI Docs aims to become a unified collection of document tools, including:

### Convert
Convert supported document formats between PDF, DOCX, DOC, TXT, Markdown, RTF, ODT and other formats as compatible engines are introduced.

### Organize
Merge, split, reorder, extract, rotate and rearrange pages or document sections where the format supports those operations.

### Optimize
Compress files, optimize embedded images, reduce document size and prepare files for sharing.

### Edit and prepare
Edit document content, adjust layouts, apply templates, add headers/footers, page numbers, watermarks and branding.

### Extract and transform
Extract text and images, convert scans through OCR, and transform content into reusable formats.

### Batch workflows
Process multiple files in one operation, with clear per-file status and downloadable results.

The supported format matrix and tool availability must be documented as each capability is implemented and tested.

## Technology stack

| Area | Current technology |
|---|---|
| Frontend | React 18, JavaScript, Vite 6 |
| Styling | Tailwind CSS 3 |
| Backend | Node.js, Express 4 |
| PDF rendering | Puppeteer |
| Markdown | markdown-it |
| DOCX import | Mammoth |
| HTTP middleware | CORS |

The client and API have separate package manifests: `client/package.json` and root `package.json`.

## Repository layout

```text
.
├── client/                 # React + Vite application
│   └── src/
│       ├── components/     # Editor, upload, preview and UI components
│       └── utils/          # Document conversion utilities
├── server.js               # Express API and document rendering endpoints
├── package.json            # Backend dependencies and scripts
├── DOCUMENTACION.md        # Legacy documentation (not authoritative)
└── docs/                   # Product and engineering documentation
```

## Development setup

### Requirements

- Node.js compatible with the installed dependencies.
- npm.
- Chromium dependencies required by Puppeteer on your operating system.

### Install dependencies

From the repository root:

```bash
npm install
cd client
npm install
```

### Run the API

In the repository root:

```bash
npm run dev
```

The API listens on port `3000` by default. Set `PORT` to override it.

### Run the frontend

In a second terminal:

```bash
cd client
npm run dev
```

Vite serves the frontend. The API proxy configuration and deployment routing should be checked for the active environment before connecting the client to a separately hosted API.

### Production build

```bash
cd client
npm run build
```

The current root package exposes `start` and `dev` scripts for the Express API. There is no root-level orchestrated build script in the inspected package manifest.

## API endpoints currently present

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/` | API health/status response |
| POST | `/api/generate-pdf` | Render document content to PDF |
| POST | `/api/generate-html` | Return generated HTML |
| POST | `/api/generate-docx` | Return HTML with a legacy Word MIME type |

The `generate-docx` endpoint currently returns HTML content labelled as `application/msword`; it is not a full DOCX package generator. Do not describe it as native DOCX export.

## Security and privacy

Document processing can involve sensitive personal, business or legal information. Before exposing the service publicly:

- Validate file type using content inspection, not only filename extensions or browser MIME values.
- Enforce upload size, page count, processing time and resource limits.
- Sanitize HTML and validate URLs and embedded resources before rendering.
- Restrict CORS to trusted origins.
- Avoid logging document content or sensitive metadata.
- Use temporary storage with cleanup if file-based processing is introduced.
- Isolate conversion workers and restrict network access where possible.
- Define retention and deletion behavior for uploaded and generated files.
- Never expose secrets in frontend environment variables or client bundles.

See [Security](docs/SECURITY.md).

## Documentation

- [Product definition](docs/PRODUCT.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Roadmap](docs/ROADMAP.md)
- [Architecture decisions](docs/DECISIONS.md)
- [Security](docs/SECURITY.md)
- [Contributing](docs/CONTRIBUTING.md)
- [Claude Code instructions](CLAUDE.md)
- [Project implementation prompt](PROMPT.md)

## License

Released under the [MIT License](LICENSE).

---

Part of the **[WI Arch](https://github.com/wiarch)** ecosystem.
