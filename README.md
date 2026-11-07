# English Reader

A local-first, installable PWA for reading **English books** and learning vocabulary with **French** translations.
Import an EPUB or PDF, read it page by page, tap any word for its base form, French translation and English definitions,
long-press and slide over several words to translate a phrase or sentence, and keep a vocabulary notebook.

Everything (books, vocabulary, reading position, settings) stays on the device. No backend, no accounts, no API keys.

## Deploy on GitHub Pages (new repository)
1. On GitHub create a **new** public repository, e.g. `english-reader`. Do not use the Hojas repository.
2. Unzip this package. In the new repository choose **Add file → Upload files** and drag in the *contents* of the unzipped
   folder (so that `index.html` is at the top level, next to the `vendor` and `icons` folders). Commit.
3. **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)` → Save.**
4. After a minute the app is at `https://<your-username>.github.io/english-reader/`.
5. On Android open that address in Chrome → menu → **Install app**.
6. If anything seems off, open `…/english-reader/check.html`. It reads (never changes) what the website serves,
   what is saved for offline use, and which service worker runs.

## Where things are
| File | Purpose |
|---|---|
| `index.html`, `style.css` | page and the dusty-pink design |
| `app.js` | the app (library, paginated reader, word/phrase lookup, vocabulary, chapters) |
| `lex.js` | dictionary + translation: English Wiktionary, Lingva, MyMemory (English → French) |
| `paginate.js`, `chapters.js` | page layout engine, chapter list logic |
| `sw.js` | service worker (offline copy; app files are network-first so updates show up) |
| `manifest.webmanifest`, `icons/` | PWA identity and icons |
| `vendor/` | pdf.js and JSZip (EPUB/PDF reading) |
| `check.html` | installation check |

## Storage identity (nothing shared with other apps)
IndexedDB database `english-reader` · localStorage key `english-reader.settings` · Cache Storage `english-reader-<build>` ·
its own manifest, icons and service worker.

## Updating
Upload the new files and open the app twice (the first load fetches the update; a "Reload" prompt appears when it is ready).
Raise `BUILD` in `sw.js` and `APP_BUILD` in `app.js` and the `app-build` meta tag in `index.html` together when you release.

## Services (no keys)
English Wiktionary (definitions, base forms, grammar) · Lingva then MyMemory (French). A new word or sentence needs internet;
words you have looked up are cached on the device. MyMemory allows a limited number of free translations per day;
you can put your e-mail address in `MYMEMORY_EMAIL` at the top of `lex.js` to raise it.

## Credits
pdf.js (Apache-2.0), JSZip (MIT / GPLv3), English Wiktionary (CC BY-SA).
