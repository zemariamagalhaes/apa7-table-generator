# APA Table Generator

A free, single-file tool that turns data pasted from Excel, Google Sheets, SPSS or a CSV into an **APA 7** formatted table, ready to copy into Word or download as a real `.docx`.

Everything runs in your browser. No server, no account, no tracking, no data leaves your computer, and it works offline.

**Live demo:** `https://<your-username>.github.io/apa-table-generator/` *(enable GitHub Pages, see below)*

## Features

- **Paste and go:** copy cells from Excel, Google Sheets or SPSS and paste. Tab-, comma-, semicolon- and pipe-separated data are detected automatically.
- **Open files:** load a `.csv`, `.tsv` or `.txt` file directly.
- **Two outputs:**
  - **Copy for Word:** puts a formatted table on the clipboard (paste with *Keep Source Formatting*).
  - **Download .docx:** generates a real Word file (A4, 1-inch margins), more reliable than pasting.
- **APA 7 layout:** bold table number, italic title, horizontal rules only (above and below the header, below the last row), Times New Roman 12pt, double-spaced title and note.
- **Statistical italics:** *M*, *SD*, *N*, *n*, *p*, *t*, *F*, *r*, *SE*, *df*, *B* in headers, and in notes or cells when followed by `=`, `<` or `>`. Also sets η<sub>p</sub><sup>2</sup>, χ<sup>2</sup> and *R*<sup>2</sup>.
- **Heading capitalisation:** sentence case (APA 7), Title Case, or as typed.
- **Optional leading-zero removal:** `0.05` → `.05`.
- **Smart alignment:** first column left-aligned; other columns centred when all values are numeric.
- **Robust parsing:** quoted cells, ragged rows, Windows line endings, and an empty top-left header cell are handled.
- **Light and dark mode.**

## Usage

1. Open `index.html` in any modern browser (double-click it, or use the live demo).
2. Enter a table number, a title and, optionally, a note.
3. Paste your data. The **first row must be the column headings**.
4. Click **Generate APA table**.
5. Click **Copy for Word** or **Download .docx**.

### Example files

Two ready-made files in [`examples/`](examples/) show everything, including the table number, title and note:

- [`examples/example.csv`](examples/example.csv): comma-separated, with quoted cells (descriptive statistics and group comparisons).
- [`examples/example.txt`](examples/example.txt): tab-separated, as copied from Excel or SPSS (regression results with confidence intervals).

Click **Open CSV/TSV file...** and pick one, then click **Generate APA table**.

### Title and note inside the data (optional)

Put these lines at the top of a file, or at the top of pasted text, and the tool moves them into the form fields for you:

```
# Table: 1
# Title: Descriptive Statistics for Study Variables
# Note: Note. N = 120. M = mean; SD = standard deviation.
Group,N,M,SD
Control,42,25.4,4.1
```

### Minimal example input

```
Group	N	M	SD
Control	42	25.4	4.1
Treatment A	40	24.9	3.8
Treatment B	41	26.1	4.3
```

(Tab-separated. Copying cells straight from a spreadsheet gives you this automatically.)

## Run or host it

It is a single static file with no build step and no dependencies.

- **Locally:** open `index.html` in your browser.
- **GitHub Pages:** *Settings → Pages → Deploy from a branch → `main` / root*. The file must be named `index.html`.
- **Any static host** (Netlify, Cloudflare Pages, Vercel, ...): upload the file.

## How it works

- A small RFC 4180-style parser handles delimiter detection and quoted fields.
- The table is rendered as HTML with inline styles (including Word-specific `mso-border-*` properties), which is what lets Word keep the APA borders when you paste.
- The `.docx` is built by hand: the OOXML parts are written as strings and packed into a store-only ZIP with a CRC-32 implementation, so no libraries are needed.

## Limitations

- Numbers are centred, not decimal-aligned.
- No merged cells or spanner headings yet.
- One table per document.
- "Copy for Word" depends on how Word handles clipboard HTML. Word for the web ignores some styling, so use **Download .docx** if the paste looks off.
- The tool formats; it does not check your statistics or round your numbers. Check values against the APA 7 manual before submitting.

## Roadmap ideas

- Round numbers to *N* decimals and strip trailing `.0`
- Spanner headings and merged cells
- Multiple tables in one `.docx`
- Decimal alignment

## License

MIT, see [LICENSE](LICENSE).

## Author

Developed by **José Maria Magalhães**.
