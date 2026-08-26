# ai-project-logos

Logo assets for the AI-agent tools catalogued on **[way.space](https://way.space)**, mirrored
here and served over jsDelivr's CDN.

The catalogue needs each tool's logo to still load in a year. Hotlinking doesn't survive that:
favicons move, GitHub avatars break, project sites redesign. So logos entered through the
way.space admin editor are copied here, and the catalogue stores the CDN URL.

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
in place. Hotlink these with confidence; pinning to a commit SHA instead of `@main` is
supported by jsDelivr but unnecessary here.

## Layout

```
logos/{tool-slug}/{tool-slug}-{sha256[:8]}.{svg|png|jpg|webp|gif}
```

- **One folder per catalogued tool**, named for its way.space slug — so
  `way.space/tool/ecc` ↔ `logos/ecc/`.
- **The filename is content-addressed.** A changed logo hashes differently and lands at a
  new path, which is what keeps jsDelivr's 12 h edge cache from ever serving a stale image
  (it has no purge API). An unchanged logo re-resolves to the path already here, so nothing
  is duplicated no matter how often a tool is edited.
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
here is authored by Lineage Labs, and inclusion implies no affiliation with or endorsement by
the projects shown.

Files are written by the way.space worker
([`logo-mirror.ts`](https://github.com/LineageLabs/way-space/blob/main/src/lib/server/logo-mirror.ts)),
not by hand — uploaded SVGs are sanitized first (no scripts, event handlers,
`foreignObject`, external references, or DOCTYPE/ENTITY declarations).

**If you own a logo here and want it changed or removed**, open an issue on this repository
and we'll take care of it.
