# TaskBoard

A browser-based visual desktop (windows, files, jobs, network, music, settings, terminal) that is assembled from HTML markup. There are no first-party `.js` or `.css` files: capabilities are mounted with `<script src>` and `<link href>`, and behavior is bound through `id`, `class` and the attribute vocabularies of htmx, Alpine.js and _hyperscript.

## Files

```
TaskBoard/
├── index.html
├── README.md
└── partials/
    └── apps/
        ├── terminal.html
        ├── files.html
        ├── jobs.html
        ├── network.html
        ├── music.html
        └── settings.html
```

## Run

The apps are HTML fragments fetched with htmx, so serve the folder over HTTP (opening `index.html` from `file://` will not work).

```
cd TaskBoard
python3 -m http.server 8000
```

Open http://localhost:8000. Any static host works (GitHub Pages, Vercel, Render static site).

## Modes

All three modes launch the same fragments through one `launch()` definition in `index.html`.

- GUI: icon launcher (footer, first button)
- CUI: numbered text menu, keys 1 to 6 (second button)
- CLI: terminal window; type `help`, then an app name such as `files` (third button)

## Mounted components (exact pinned versions)

htmx 4.0.1 with hx-alpine-compat, Alpine.js 3.17.5 with Anchor, Collapse, Focus, Intersect, Mask, Morph, Persist, Resize and Sort plugins, _hyperscript 0.9.94, Tailwind CSS Browser 4.3.5, daisyUI 5.7.50 with its theme pack, Animate.css 4.1.1, Iconify Icon 3.0.5, Tone.js 15.1.22.

Used by the apps today: htmx (window loading), Alpine (state, Persist for language, theme and background, Sort for job and note order, Collapse for minimize), _hyperscript (footer clock), Tone.js (Music), Iconify (icons), daisyUI and Tailwind (styling), Animate.css (window entrance, which Animate.css disables under reduced motion). Focus, Intersect, Mask, Morph and Resize are loaded but not yet used by an app.

## Apps

- Terminal: command routing to apps
- Files: pick files or a folder and list names and sizes (File System Access API not used yet)
- Jobs: drag-sortable queue with progress, runs only while the tab is open
- Network: online state, connection type (where the browser reports it) and a latency probe against this host
- Music: four-step melody, drag to reorder, pick notes, play with Tone.js
- Settings: language (English, Japanese, Spanish, Arabic with right-to-left), theme, background gradient or picture, keep screen on (Wake Lock, where supported)

## Decisions taken

- "Code-free" is read as: no hand-written `.js` or `.css` files. Behavior is declared as attribute expressions (`x-data`, `@click`, `_`).
- No project-owned adapter bundle. Features that would need one are not included yet.

## Not included yet

Gesture recognition (MediaPipe), p5.js, Processing.js, Three.js and WebGL scenes, sql.js, PyScript, php.js, supercollider.js, Datastar, Unpoly, Stimulus, Turbo, Vue.js, Petite-Vue, the remaining CSS frameworks and animation packs, the other htmx extensions, video, image and poetry studios.

## Status and caveats

- Static checks only; not yet run in Chrome, Firefox and Safari. Report console errors as issues.
- Subresource Integrity hashes are not set. Generate them for every `<script>` and `<link>` before production use.
- Pinned versions are at least two weeks old at the time of writing. Review licenses of every component before publishing.
- Iconify fetches icon data from the Iconify API at runtime, so icons need a network connection.
- Tailwind Browser and the Alpine standard build need `unsafe-eval`-style permissions, so a strict CSP is not possible with this build.
