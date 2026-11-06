# Contributing

Thank you for helping improve WI Docs.

## Before changing code

1. Read the README, product definition and architecture notes.
2. Inspect the current implementation and identify the actual behavior.
3. Confirm whether the task concerns an existing feature or a roadmap capability.
4. Preserve unrelated behavior and keep changes focused.

## Development

Backend dependencies are installed from the repository root:

```bash
npm install
npm run dev
```

Frontend dependencies and scripts are in `client/`:

```bash
cd client
npm install
npm run dev
npm run build
```

The API defaults to port 3000 and can be configured with `PORT`.

## Pull requests

A pull request should include:
- Problem and motivation.
- Summary of implementation.
- Supported input and output formats.
- User-visible limitations or fidelity changes.
- Security considerations for parsers, uploads and renderers.
- Tests executed and their actual results.
- Screenshots for meaningful UI changes.

## Quality expectations

- Add regression tests for document parsing and conversion.
- Include malformed and boundary-case inputs.
- Do not commit private documents, credentials, generated outputs or temporary files.
- Avoid logging document content.
- Update the capability matrix and documentation when format support changes.
- Never label a conversion lossless without evidence.
