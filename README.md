# PDF Markup

A single-file, in-browser tool for drawing on PDFs, replacing text, redacting sensitive content and splitting documents. Everything runs locally in your browser — your files are never uploaded.

## Features

### Markup
- **Shapes:** rectangle, square, ellipse, line, arrow and freehand pen
- **Styling:** 8 preset colors plus a rainbow custom-color picker, adjustable stroke width, and three fill modes (none, translucent, solid)
- **Line opacity:** lines, arrows, pen strokes and shape outlines can be solid or translucent. Translucent arrows are drawn as a single stroke, so they don't darken where the head meets the shaft
- **Highlighter:** use the pen with translucent opacity
- **Editing:** select, move, resize (bottom-right handle) and delete any markup; full undo and redo

### Text
- **Text tool:** add text anywhere, with 17 fonts, sizes from 8 to 72 pt and bold
- **Replace tool:** click a line of existing PDF text (or drag across several words) to replace it. The tool reads the original position and size from the PDF, samples the background and text colors from the page, and picks the closest matching font automatically (Latin text is always matched to a Latin font)
- **Live styling:** while you type, the sidebar shows the detected text color, background color, font, size and bold. Change any of them and the text box updates instantly, without closing
- **Background control:** set the cover color yourself, switch to white, or use **Match page** to sample it again
- **Reset to detected style:** undo your style changes in one click
- Leave the replacement empty to erase the original text

### Redaction
- **Redact tool:** draws boxes that permanently remove whatever is underneath when you save or split
- **Any color:** black by default; pick white for a clean cover-up, or any other color
- **Easy to tell apart:** redaction boxes show a dashed inner outline while you edit (not included in the saved PDF), so they're never confused with ordinary solid shapes
- **Safety prompt:** if you've drawn solid shapes that aren't redactions, you're offered to convert them before saving, so nothing you meant to hide stays copyable

### Split
- Five methods: pick cut points (click between pages), every page, every N pages, custom ranges, and extract pages
- Real page thumbnails with color-coded groups and markup indicators
- Download files individually or as a single ZIP
- Splits use the same processing as Save, so removed text never reappears in split files. Splitting the original pages is disabled while the document has redactions or replaced text

### Convenience
- **Settings sidebar:** tool settings (color, stroke, fill, font, size) appear in a left sidebar and only show what's relevant to the current tool or selection. On phones it becomes a floating panel at the bottom
- **Autosave:** markup is saved in your browser and can be restored the next time you open the same PDF
- **Light and dark mode:** a soft, low-saturation blue “jelly” look that follows your system setting

## Getting started

1. Open `pdf-markup.html` in a modern browser (Chrome, Edge, Firefox or Safari).
2. Drag a PDF onto the page, or click **Open PDF**.
3. Pick a tool from the toolbar, adjust it in the left sidebar, and draw on the page.
4. Click **Save PDF** to download the marked-up copy (saved as `<name>-marked.pdf`), or **Split** to break it into several files.

An internet connection is needed so the page can load its libraries and fonts from CDNs.

## Hosting

The app is a single static file with no server-side code, so you can:

- **Open it directly** from your computer by double-clicking `pdf-markup.html`
- **Host it** on any static host such as GitHub Pages, Netlify, Cloudflare Pages or an S3 bucket. Rename it to `index.html` if you want it served at the site root

Files are saved through your browser's normal download flow.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| H | Pan |
| V | Select |
| P | Pen |
| R | Rectangle |
| S | Square |
| O | Ellipse |
| L | Line |
| A | Arrow |
| T | Text |
| E | Replace |
| X | Redact |
| Shift + drag | Constrain to square / circle, or snap lines to 45° |
| Ctrl/⌘ + Z | Undo |
| Ctrl/⌘ + Shift + Z, Ctrl/⌘ + Y | Redo |
| Delete / Backspace | Delete the selected markup |
| Enter | Finish editing text (Shift + Enter for a new line) |
| Esc | Cancel text editing, clear the selection, or close the split panel |

Double-click text with the Select tool to edit it.

## How saving works

Each page is handled according to what's on it:

- **Pages with redactions or replaced text are flattened.** The page is rebuilt as a single 200 dpi image with your markup burned in, so the covered text is truly gone and can't be copied or searched.
- **Pages with other markup get an overlay.** Your drawings are added as an image layer on top, and the page's original text stays selectable and searchable.
- **Pages without markup are copied unchanged.**

When any page is flattened, the output is assembled into a brand-new document, so no leftover data from the original pages remains in the file. In that case the new file doesn't keep bookmarks, outlines or form fields from the original.

## Fonts

| Group | Fonts |
| --- | --- |
| Office look-alikes | Arial / Helvetica (Arimo), Times New Roman (Tinos), Calibri (Carlito), Cambria (Caladea), Georgia (Gelasio), Courier New (Cousine) |
| Modern | Roboto, Open Sans, Lato, Montserrat, Noto Sans Mono |
| Display & handwriting | Merriweather, Playfair Display, Caveat |
| Chinese | Noto Sans TC (黑體), Noto Serif TC (明體), LXGW WenKai TC (楷體) |

New text uses Arial / Helvetica (Arimo) by default.

The Office look-alikes are metric-compatible open fonts: each character has the same width as the original, so replaced text lines up with the surrounding layout. When a Latin font is selected, Chinese characters fall back to a matching Chinese font. The interface itself uses Nunito.

## Limitations

- **Scanned PDFs** have no text layer, so Replace can't detect text. Use the Redact tool (white works well) plus the Text tool instead.
- **Replace** covers text with a single background color, so it works best on plain backgrounds. Gradients, photos and watermarks will show the patch. Longer replacement text does not reflow surrounding content.
- **Font matching** is approximate. Custom or brand fonts are mapped to the closest available style.
- **Password-protected PDFs** cannot be opened.
- **Some Chinese PDFs** that don't embed their fonts may display text incompletely.
- **Autosave** is stored per browser and device. Clearing browser data removes it, and it is matched by file name, size and page count.
- **Rotated or vertical text** is skipped by the Replace tool.

## Privacy

PDFs are read, rendered and processed entirely in your browser. Nothing is sent to a server. Autosaved markup is kept in your browser's local storage and never leaves your device.

## Built with

- [PDF.js](https://mozilla.github.io/pdf.js/) 3.11.174 — rendering and text extraction
- [pdf-lib](https://pdf-lib.js.org/) 1.17.1 — writing, flattening and splitting PDFs
- [JSZip](https://stuk.github.io/jszip/) 3.10.1 — ZIP downloads for split files
- [Google Fonts](https://fonts.google.com/) — interface and text fonts

The whole app is a single HTML file with inline CSS and JavaScript and no build step.
