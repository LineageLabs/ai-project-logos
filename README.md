# ai-project-logos

Logo assets for the AI-agent tools catalogued on **[way.space](https://way.space)**, mirrored
here and served over jsDelivr's CDN.

The catalogue needs each tool's logo to still load in a year. Hotlinking doesn't survive that:
favicons move, GitHub avatars break, project sites redesign. Nor is it fair on the hosts —
`raw.githubusercontent.com` is not a CDN, and a project's own asset server never agreed to
serve our traffic. So the logos the catalogue uses are copied here, and the catalogue stores
the CDN URL.

Two sources feed this repo, both written by the way.space worker
([`logo-mirror.ts`](https://github.com/LineageLabs/way-space/blob/main/src/lib/server/logo-mirror.ts)):

- logos entered through the way.space admin editor (a pasted URL or an uploaded SVG), and
- square icons found in a catalogued project's own README by the icon scraper.

Two things are deliberately **not** mirrored: [Lobehub](https://github.com/lobehub/lobe-icons)
icons, which are already served as a pinned npm package over jsDelivr — that CDN's actual
purpose — and GitHub owner avatars, which are a live link to an account's own image and change
over time.

## Using a logo

Every file is served from jsDelivr, free and CORS-enabled:

```
https://cdn.jsdelivr.net/gh/LineageLabs/ai-project-logos@main/logos/{slug}/{filename}
```

```html
<img src="https://cdn.jsdelivr.net/gh/LineageLabs/ai-project-logos@main/logos/ecc/ecc-ea500226.svg"
     alt="ECC" width="48" height="48">
```

**Paths are immutable.** A file is named for the SHA-256 of its own bytes, so a URL that
works today keeps serving the exact image it served on day one — nothing is ever overwritten
in place. Pinning to a commit SHA instead of `@main` is supported by jsDelivr but unnecessary
here.

Note what that does and does not give you: a stable URL, and no rights in the image behind it.
See **Provenance and attribution** below before using one of these marks for anything other
than identifying the same project this catalogue identifies.

## Layout

```
logos/{tool-slug}/{tool-slug}-{sha256[:8]}.{svg|png|jpg|webp|gif}
```

- **One folder per catalogued tool**, named for its way.space slug — so
  `way.space/tool/ecc` ↔ `logos/ecc/`.
- **The filename is content-addressed.** A changed logo hashes differently and lands at a
  new path, which is what keeps jsDelivr's 12 h edge cache from ever serving a stale image
  (it has no purge API). An unchanged logo re-resolves to the path already here, so nothing
  is duplicated no matter how often a tool is edited or re-scraped.
- **The slug is repeated in the filename** so a file downloaded on its own still says what
  it is. It's decoration — the hash alone determines the path.
- **No dates in filenames.** A date is mutable by construction: re-saving a corrected logo
  the same day would reuse the name for different bytes and serve the stale one for up to
  12 hours. Dates live in the git history, where they belong — `git log -- logos/ecc/`.

More than one file in a folder simply means that tool's logo has been updated; the older
files stay so previously issued URLs keep resolving.

## Why this repo is public

jsDelivr serves public repositories only. The GitHub Contents API will commit to a private
repo perfectly happily, so a private mirror would produce successful saves whose every CDN
URL 404s.

## Provenance and attribution

These are **third-party logos**, held for identification of the projects they belong to in a
catalogue. Each remains the property of its owner and may be a registered trademark. Nothing
here is authored by Lineage Labs, and inclusion implies no affiliation with, sponsorship by,
or endorsement from the projects shown.

They are used **nominatively** — to identify the tool a catalogue entry is about. way.space
shows a logo on that tool's own card and page, at the size needed to recognise it, and nowhere
else; it does not use them in its own promotional material or imply any project has endorsed
it.

**This repository grants no licence to these marks, and deliberately carries no `LICENSE`
file.** We hold no rights to grant. An open-source licence on a project's *code* does not
convey rights to its name or logo — the Apache-2.0 licence excludes trademarks explicitly
(§6), and permissive licences that are silent on the point are not read as trademark grants
either. Anyone reusing a file from here is responsible for their own basis for doing so.

**If you own a logo here and want it changed, attributed differently, or removed**, open an
issue on this repository and we will act on it — no explanation needed, and we will not ask
you to justify the request.

## Safety

Files are written by the worker, never by hand. SVGs — whether uploaded by an admin or found
in a project README — are sanitized before they are committed: no scripts, event handlers,
`foreignObject`, external references, or DOCTYPE/ENTITY declarations. Once bytes are served
from this repo over our CDN path, anything active in them would be ours.
