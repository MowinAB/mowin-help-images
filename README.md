# Mowin help images

Public host for screenshots embedded in Mowin's [Intercom help articles](https://github.com/MowinAB/mowin/tree/development/frontend/docs/articles).

This repo exists because Intercom's Articles API has no file-upload endpoint — it only accepts publicly fetchable image URLs, which it then rehosts on its own CDN. We point article markdown at `raw.githubusercontent.com` URLs in this repo; Intercom fetches them on push and serves the rehosted copy to end users from `intercomcdn.com`.

## Folder convention

```
<helpTopicId>/<descriptive-name>.png
```

Example: `order-list/filters.png`, used in the article from `frontend/docs/articles/order-list.md` as:

```markdown
![](https://raw.githubusercontent.com/MowinAB/mowin-help-images/main/order-list/filters.png)
```

`helpTopicId` matches the camelCase id in `frontend/app/config/help.ts`. Use kebab-case for the file name.

## When to add a screenshot

By default, articles are screenshot-free — Fin AI reads text, screenshots drift faster than prose, and the existing pull pipeline strips Intercom CDN images on every pull. Only commit a screenshot here when it carries information the prose can't, and prefer one good screenshot over a series.

## Workflow

1. Drop the PNG/SVG into `<topic>/<name>.png` in this repo and push to `main`.
2. Reference the `raw.githubusercontent.com` URL from the article markdown in the main repo.
3. Run `yarn intercom:sync --topic <topic>` (or merge to `development` to let CI sync). Intercom downloads from this repo and rehosts.

The `inverse.ts` strip rule only matches `intercomcdn.com`, so `raw.githubusercontent.com` URLs survive a pull. A forced re-pull of an article still loses the original URL though — keep that in mind before running `intercom:pull --force` on a wired article with screenshots.

## Don't delete

Once a screenshot is referenced from a live article, the URL must keep working — every CI sync re-pushes the article body, and Intercom re-fetches the source URL. If the source URL 404s at sync time, the image disappears from the live article.

If a screenshot becomes obsolete: remove the reference from the article markdown first (and let the next sync land), then delete the file here.
