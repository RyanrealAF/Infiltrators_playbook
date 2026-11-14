# The Infiltrator's Playbook

The public edition of *The Infiltrator's Playbook* — a textbook in strategic
reversal — as a single-page web app. The full text: 7 parts, 26 chapters,
4 appendices, plus a searchable lexicon and the case timeline.

The case study is told in the abstract: the two principals appear only as
the Builder and the Partner. No real names or place names anywhere in the
site. That is deliberate — this is the public-facing version.

## Live site

- Direct: `https://infiltrators-playbook.pages.dev/` (live, dashboard-connected)
- On the umbrella: `https://buildwhilebleeding.com/infiltrators-playbook/`
  (once the worker route below is live)

## What's in this repo

- `index.html` — the whole site, self-contained (text, styles, artwork,
  lexicon search, navigation). This is the file Cloudflare Pages serves.
- `wrangler.toml` — the Pages project name and output directory.
- `README.md` — this file.

## Deploy

The repo is connected to Cloudflare Pages in the dashboard (Workers &
Pages > Pages > `infiltrators-playbook`, connected to
`RyanrealAF/Infiltrators_playbook`). Every push to `main` redeploys
automatically. There is no build step and no GitHub Action — the dashboard
connection is the only deploy path.

## Wire it into buildwhilebleeding.com

In `RyanrealAF/buildwhilebleeding`, `public/_worker.js`, add one line to
the `PROJECTS` table:

```js
"/infiltrators-playbook": "https://infiltrators-playbook.pages.dev",
```

and one line to `TRAILING_SLASH_REQUIRED`:

```js
"/infiltrators-playbook",
```

Push to `main` — the umbrella redeploys and
`https://buildwhilebleeding.com/infiltrators-playbook/` serves the book.
Also add a row to `docs/ROUTING.md`:

| `/infiltrators-playbook/*` | The Infiltrator's Playbook | `https://infiltrators-playbook.pages.dev` | `RyanrealAF/Infiltrators_playbook` | Static HTML |

## Updating the site

The site is generated from the public-edition document. To update it,
replace `index.html` with a fresh export. GitHub web upload works for the
~7 MB file — the API push path truncates files near 1 MB, so do not push
`index.html` through the API. Small text files (`wrangler.toml`,
`README.md`) are fine to push normally.

## Notes

- The repo also contains `The Infiltrators Playbook.html` — the same site
  under its original upload name. `index.html` is the file Pages serves;
  the duplicate can be deleted.
- No build step, no dependencies, no backend. The site runs entirely in
  the browser.
