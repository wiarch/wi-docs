# Security Policy and Engineering Requirements

## Data sensitivity

Documents may contain personal, financial, legal, educational, medical or business information. Treat every uploaded file and its contents as confidential and untrusted.

## Findings in the current baseline

The inspected API currently:
- Enables CORS without an origin allowlist.
- Accepts JSON and URL-encoded bodies up to 50 MB.
- Configures markdown-it with raw HTML enabled.
- Passes generated HTML to Puppeteer.
- Launches Puppeteer with Chromium sandbox flags disabled.

These choices require hardening before public production use. This document records code-level observations, not a penetration-test result.

## Required controls

### Upload and parsing
- Validate file signatures and actual content, not only extensions or client MIME types.
- Enforce file size, page count, archive expansion, image dimensions and processing limits.
- Reject malformed, encrypted or unsupported files with safe errors.
- Defend against archive bombs and parser vulnerabilities.
- Keep parsers and conversion libraries updated.

### HTML and rendering
- Sanitize user-provided and converted HTML with a maintained allowlist sanitizer.
- Disable arbitrary remote resource loading.
- Prevent access to local files, internal services, cloud metadata endpoints and loopback addresses.
- Avoid interpolating untrusted strings into CSS, HTML, URLs or Puppeteer configuration.
- Run Chromium in a properly isolated environment; do not rely on disabling sandbox protections as a production default.

### API
- Restrict CORS to trusted origins.
- Add rate limits, concurrency limits and request timeouts.
- Validate all numeric and color configuration values.
- Avoid returning internal exception details to clients.
- Add authentication/authorization if private job history or persistent files are introduced.

### Storage and privacy
- Use private temporary storage and unpredictable identifiers.
- Clean up files on success, failure, cancellation and expiration.
- Define retention periods and deletion behavior.
- Do not log document bodies, extracted text, secrets or sensitive filenames.
- Encrypt data in transit and protect stored files if persistence is introduced.
- Do not transmit documents to third-party conversion or AI services without clear disclosure and consent.

### Operations
- Run workers with least privilege and restricted network/filesystem access.
- Monitor resource use and conversion failures without collecting document content.
- Maintain dependency and container update processes.
- Back up only data that the product intentionally retains.

## Incident response

If a security issue is discovered, stop the affected processing path, preserve relevant operational evidence without copying sensitive document contents, assess exposure, rotate affected credentials and notify impacted users as required.

## Reporting

Report vulnerabilities privately to the repository maintainers. Do not publish exploit details before maintainers have had a reasonable opportunity to investigate and release a fix.
