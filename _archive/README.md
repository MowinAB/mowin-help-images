# `_archive/`

Recovery bin for screenshots that lived only in Intercom. Two batches so far:

- **2026-06** — the screenshots embedded in the 49 repo-managed articles, archived when the screenshots-default-no policy landed in [`MowinAB/mowin@b7e5cd59b`](https://github.com/MowinAB/mowin/commit/b7e5cd59b).
- **2026-09-16** — 255 images across 78 articles, pulled during the help-centre audit in [`MowinAB/mowin#5546`](https://github.com/MowinAB/mowin/issues/5546). Mostly articles not yet migrated into `frontend/docs/articles/`.

**Every Intercom image URL is signed and short-lived.** The 2026-09 batch was fetched hours before expiry, and re-requesting the article from the Articles API returns the *same* signature rather than a fresh one — there is no re-minting to wait for. Anything still only on Intercom is one expiry away from being unrecoverable, so archive first and decide later.

## Layout

```
_archive/<article-kebab-name>/<NN>.png
```

`<article-kebab-name>` matches the source markdown file in `frontend/docs/articles/` where one exists. Articles not yet migrated have no markdown file, so those folders are `<kebab-title>-<intercomArticleId>` instead — the id is what ties the folder back to Intercom.

`<NN>` is a 2-digit zero-padded index reflecting the order the image appeared in the article body (top to bottom). No filename hints — these are unlabelled raw captures.

## What this is *not*

These are not the canonical place for new screenshots. The canonical layout is `<helpTopicId>/<descriptive-name>.png` at the repo root. `_archive/` is a recovery bin: if a future article edit reveals that one of the original screenshots was actually carrying meaning, copy it out of here, rename it to the proper convention, and delete the archived copy.

If a screenshot looks stale against today's UI, recapture rather than reuse — most of these date from the legacy Intercom UI editor and reflect older states of the product.

## Provenance

For the 2026-06 batch, source URLs are recoverable from the strip commit's diff in the main repo:

```bash
git show b7e5cd59b -- frontend/docs/articles/ | grep intercomcdn.com
```

The 2026-09 batch records its own provenance in `manifest-2026-09.json` beside this file — article id, title, archived path, and the original CDN path with the signature stripped.
