# Forma PDF — Browser PDF Editor

A client-side PDF workspace built with Vite, PDF.js and pdf-lib. The application has no backend and does not upload documents to a server.

## Features

- Local PDF upload and drag-and-drop
- PDF page rendering and page thumbnails
- Click text items to select and replace text
- Add new text at a chosen page position
- Zoom, page navigation, rotate, delete and insert pages
- Undo/redo for editor operations
- Download an edited PDF
- Responsive dark interface for desktop and mobile browsers

## Important editing limitation

PDF is a final-layout format, not a word-processing format. It does not reliably store semantic paragraphs or a guaranteed editable font for every text run. Some documents use subset fonts, custom encodings, outlined glyphs, transparency, clipping paths, or scanned page images.

This project uses PDF.js text extraction to locate text and pdf-lib to write edits. **Replacing an existing text item is currently a visual replacement operation:** the selected text area is covered with a white rectangle and new text is drawn using a standard Helvetica font. It does not rewrite the original PDF content stream or guarantee the original font, kerning, color, background, or layout. Complex backgrounds and non-white page areas may show a patch. Scanned PDFs have no selectable text and need OCR, which is not included.

The UI reports detected PDF font metadata as an estimate. Do not treat that as proof that the font has been embedded or reproduced exactly. Always compare the exported PDF with the original. This is an honest browser-only baseline, not a substitute for a commercial-grade PDF content-stream editor.

## Requirements

- Node.js 18+ (20+ recommended)
- npm

## Run locally

```bash
npm install
npm run dev
```

Open the local URL printed by Vite.

## Build

```bash
npm run build
npm run preview
```

The production site is generated in `dist/`.

## Deploy to GitHub Pages

1. Create a GitHub repository and upload the project files.
2. In `vite.config.js`, set `base` to `'/YOUR-REPOSITORY-NAME/'` (the trailing slash matters). For a custom domain or user site repository, use `'/'`.
3. Push the changes to the `main` branch.
4. In GitHub, open **Settings → Pages** and choose **GitHub Actions** as the build and deployment source.
5. Add the workflow below at `.github/workflows/deploy.yml`.
6. Every push to `main` will build and publish the `dist` folder.

## Privacy

PDF parsing and editing run in the browser. Dependencies are downloaded when the website loads/builds, and the optional Google Fonts stylesheet requests fonts from Google. The PDF file itself is not sent to a server by this app.

## Libraries

- [PDF.js](https://mozilla.github.io/pdf.js/) — PDF rendering and text extraction
- [pdf-lib](https://pdf-lib.js.org/) — PDF document manipulation
- [Vite](https://vite.dev/) — development server and production bundler

## Current limitations / next engineering steps

- Implement safe PDF content-stream rewriting and font resource preservation for supported PDFs.
- Add OCR for scanned documents.
- Add font embedding and font-file import for new text.
- Add non-white/background-aware redaction and visual comparison.
- Implement arbitrary page reordering (the current page sidebar selects pages; insertion appends).
- Add tests with PDFs containing embedded fonts, subset fonts, vector backgrounds, rotated pages, forms, and scans.
