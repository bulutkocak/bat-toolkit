# bat-toolkit

A simple toolkit for obfuscating and restoring Windows .bat files using multiple methods. Includes both an obfuscator and deobfuscator as a single-page web tool — no install, no upload, runs entirely in the browser.

## Demo

[https://bat-toolkit.netlify.app](https://bat-toolkit.netlify.app)

## Features

- **4 obfuscation methods** — prefix injection, base64 encoding, junk line insertion, variable name scrambling
- **Auto-detect deobfuscation** — automatically identifies and reverses the method used
- No server, no upload — everything runs client-side in the browser
- Drag & drop or click to browse

## Methods

### Method 1 — Prefix Injection
Prepends a fixed 8-byte payload to the beginning of the file:

| Field | Value |
|---|---|
| Payload (base64) | `//4mY2xzDQo=` |
| Decoded (hex) | `FF FE 26 63 6C 73 0D 0A` |
| Prefix content | UTF-16LE BOM + `&cls\r\n` |
| Prefix size | 8 bytes |

### Method 2 — Base64 Encoding
Encodes the entire file as base64 and wraps it in a `certutil` self-decoding stub. The stub decodes and executes the original file at runtime.

### Method 3 — Junk Line Insertion
Scatters random `REM` comment lines and blank lines between every real line of the script. The original logic is preserved but buried in noise.

### Method 4 — Variable Name Scrambling
Replaces all `%variable%` names with random tokens (e.g. `%_xA3k9f%`). A reverse map is embedded in the file header so the deobfuscator can restore all original names.

## Usage

1. Open `index.html` in any modern browser
2. **Obfuscate** — select a method, drop your `.bat` file, downloads as `filename_obfuscated.bat`
3. **Deobfuscate** — select the matching method (or use auto-detect), drop the file, downloads as `filename_deobfuscated.bat`

## Compatibility

- Any modern browser (Chrome, Firefox, Edge, Safari)
- No dependencies, no build step — just open `index.html`

## License

MIT
