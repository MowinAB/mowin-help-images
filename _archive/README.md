# `_archive/`

One-shot archive of the screenshots that were embedded in Intercom help articles before the screenshots-default-no policy landed in [`MowinAB/mowin@b7e5cd59b`](https://github.com/MowinAB/mowin/commit/b7e5cd59b). Fetched while the original `downloads.intercomcdn.com` signed URLs were still resolving (signatures expire end of June 2026).

## Layout

```
_archive/<article-kebab-name>/<NN>.png
```

`<article-kebab-name>` matches the source markdown file in `frontend/docs/articles/`. `<NN>` is a 2-digit zero-padded index reflecting the order the image appeared in the article body (top to bottom). No filename hints — these are unlabelled raw captures.

## What this is *not*

These are not the canonical place for new screenshots. The canonical layout is `<helpTopicId>/<descriptive-name>.png` at the repo root. `_archive/` is a recovery bin: if a future article edit reveals that one of the original screenshots was actually carrying meaning, copy it out of here, rename it to the proper convention, and delete the archived copy.

If a screenshot looks stale against today's UI, recapture rather than reuse — most of these date from the legacy Intercom UI editor and reflect older states of the product.

## Provenance

Source URLs are recoverable from the strip commit's diff in the main repo:

```bash
git show b7e5cd59b -- frontend/docs/articles/ | grep intercomcdn.com
```
