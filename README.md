# ai-project-logos

Logo assets for the [way.space](https://way.space) catalogue.

Logos entered through the way.space admin tool editor — an uploaded/pasted SVG, or a
pasted URL re-fetched server-side — are mirrored here and served through jsDelivr, so
`tools.logo_url` stays a durable URL instead of a rotting external one or an inline
`data:` URI.

## Layout

    logos/{tool-slug}/{sha256[:8]}.{svg|png|jpg|webp|gif}

The path is **content-hashed**, so a changed logo is a new path — jsDelivr's 12 h edge
cache has no purge API, and a new URL is never stale. Commits are idempotent: an
unchanged logo re-resolves to the path already present.

## Why this repo is public

jsDelivr only serves public repositories. The GitHub Contents API will commit to a
private repo perfectly happily, so a private mirror produces successful saves whose
every CDN URL 404s.

## Contents

Third-party project logos, held for catalogue display and attributed to their owners.
Nothing is authored here. Written to only by the way.space worker
(`src/lib/server/logo-mirror.ts`); please don't hand-edit.
