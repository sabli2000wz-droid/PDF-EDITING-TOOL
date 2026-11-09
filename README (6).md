# PDF Markup

A single-file, in-browser tool for drawing on PDFs, replacing text, redacting sensitive content and splitting documents. Everything runs locally in your browser — your files are never uploaded.

## Features

### Markup
- **Shapes:** rectangle, square, ellipse, line, arrow and freehand pen
- **Styling:** 8 preset colors plus a custom picker, adjustable stroke width, and three fill modes (none, translucent, solid)
- **Highlighter:** use the pen with a translucent fill
- **Editing:** select, move, resize (bottom-right handle) and delete any markup; full undo and redo

### Text
- **Text tool:** add text anywhere, with 17 fonts, sizes from 8 to 72 pt and bold
- **Replace tool:** click a line of existing PDF text (or drag across several words) to replace it. The tool reads the original position and size from the PDF, samples the background and text colors from the page, and picks the closest matching font automatically
- Leave the replacement empty to erase the original text

### Redaction
- **Redact tool:** draws solid black boxes
- **Remove covered text:** flattens marked pages into images so covered content is permanently removed and cannot be copied or searched
- This option is forced on whenever the document contains redactions or replaced text, and you are warned if you have solid boxes but haven't enabled it

### Split
- Five methods: pick cut points (click between pages), every page, every N pages, custom ranges, and extract pages
- Real page thumbnails with color-coded groups and markup indicators
- Download files individually or as a single ZIP
- Splits use the same processing as Save, so removed text never reappears in split files

### Convenience
- **Autosave:** markup is saved in your browser and can be restored the next time you open the same PDF
- **Context-aware toolbar:** shows only the settings relevant to the current tool or selection
- **Light and dark mode:** follows your system setting

## Getting started

1. Open `pdf-markup.html` in a modern browser (Chrome, Edge, Firefox or Safari).
2. Drag a PDF onto the page, or click **Open PDF**.
3. Pick a tool and draw on the page.
4. Click **Save PDF** to download the marked-up copy (saved as `<name>-marked.pdf`).

An internet connection is needed the first time so the page can load its libraries and fonts from CDNs.

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
| Esc | Cancel text editing or clear the selection |

Double-click text with the Select tool to edit it.

## How saving works

There are two ways the tool writes your markup into the PDF:

- **Overlay (default):** markup is added as an image layer on top of each marked page. The original text stays selectable and searchable — including any text under your shapes.
- **Flatten (Remove covered text):** each marked page is rebuilt as a single 200 dpi image with your markup burned in. Covered text is truly gone. Pages without markup are copied unchanged. The output is assembled into a new document, so no leftover data from the original pages remains in the file.

Flattened pages are no longer selectable or searchable, and the new file does not keep bookmarks, outlines or form fields from the original.

## Fonts

| Group | Fonts |
| --- | --- |
| Chinese | Noto Sans TC (黑體), Noto Serif TC (明體), LXGW WenKai TC (楷體) |
| Office look-alikes | Arial / Helvetica (Arimo), Times New Roman (Tinos), Calibri (Carlito), Cambria (Caladea), Georgia (Gelasio), Courier New (Cousine) |
| Modern | Roboto, Open Sans, Lato, Montserrat, Noto Sans Mono |
| Display & handwriting | Merriweather, Playfair Display, Caveat |

The Office look-alikes are metric-compatible open fonts: each character has the same width as the original, so replaced text lines up with the surrounding layout. When a Latin font is selected, Chinese characters fall back to a matching Chinese font.

## Limitations

- **Scanned PDFs** have no text layer, so Replace can't detect text. Use a Rectangle with a solid fill plus the Text tool instead.
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
