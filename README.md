# bat-toolkit

A simple toolkit for obfuscating and restoring Windows .bat files using prefix injection. Includes both an obfuscator and deobfuscator as a single-page web tool — no install, no upload, runs entirely in the browser.

## Features

- **Obfuscator** — injects an 8-byte prefix into any `.bat` file
- **Deobfuscator** — detects and strips the prefix, restoring the original file
- No server, no upload — everything runs client-side in the browser
- Drag & drop or click to browse

## How it works

The obfuscator prepends a fixed 8-byte payload to the beginning of your `.bat` file:

| Field | Value |
|---|---|
| Payload (base64) | `//4mY2xzDQo=` |
| Decoded (hex) | `FF FE 26 63 6C 73 0D 0A` |
| Prefix content | UTF-16LE BOM + `&cls\r\n` |
| Prefix size | 8 bytes |

The deobfuscator checks for this exact prefix and slices it off, producing a clean restored file.

## Demo

[https://bat-toolkit.netlify.app](https://bat-toolkit.netlify.app)

## Usage

1. Open `index.html` in any modern browser
2. Use the **Obfuscator** card to encode a `.bat` file — downloads as `filename_obfuscated.bat`
3. Use the **Deobfuscator** card to restore an obfuscated file — downloads as `filename_deobfuscated.bat`

> **Note:** The deobfuscator only works with files using the prefix injection method (`//4mY2xzDQo=`). Files from other obfuscators will not be recognized.

## Compatibility

- Any modern browser (Chrome, Firefox, Edge, Safari)
- No dependencies, no build step — just open `index.html`

## License

MIT
