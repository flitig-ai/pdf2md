# pdf2md-ts

Forked from [uniai-lab/pdf2md](https://github.com/uniai-lab/pdf2md) (which itself was forked from [@opendocsg/pdf2md](https://www.npmjs.com/package/@opendocsg/pdf2md)).

Converts PDF files to Markdown. Accepts a Buffer and returns `Promise<string[]>` (one string per page).

## Major Changes

[2025-02-26]

1. Bump `pdfjs-dist` from v3 to v5, fixing CVE for arbitrary JS execution in malicious PDFs.
2. Eliminates the `canvas` → `@mapbox/node-pre-gyp` → `tar` native dependency chain and its associated vulnerabilities.
3. Fix test imports to point at `build/` (this fork has no `lib/` source directory).

[2024-3-2] (upstream, uniai-lab/pdf2md)

1. Add types to the package, typescript needs types!
2. Change to return markdown by pages, return `string[]`.
3. Remove CLI scripts.

## Usage

```bash
npm install --save pdf2md-ts
# or
yarn add pdf2md-ts
```

### Library

**CommonJS**
```js
const fs = require('fs')
const pdf2md = require('pdf2md-ts')

const pdfBuffer = fs.readFileSync(filePath)
pdf2md(pdfBuffer)
  .then(text => {
    console.log(text.join('\n'))
  })
  .catch(err => {
    console.error(err)
  })
```

**ES Modules / TypeScript**
```ts
import pdf2md from 'pdf2md-ts'
import { readFileSync } from 'fs'

const buffer = readFileSync(path)
const pages = await pdf2md(buffer)
console.log(pages) // string[]
```

## Credits

- [@opendocsg/pdf2md](https://www.npmjs.com/package/@opendocsg/pdf2md) - Which is this repo forked from
- [pdf-to-markdown](https://github.com/jzillmann/pdf-to-markdown) - original project by Johannes Zillmann
- [pdf.js](https://mozilla.github.io/pdf.js/) - Mozilla's PDF parsing & rendering platform which is used as a raw parser
