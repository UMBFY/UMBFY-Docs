# UMBFY Documentation Assets

!!! note
    **Screenshots belong under `docs/assets/`, not here.**

MkDocs publishes only what is inside `docs_dir`, which is `docs/`. A file placed in this top-level
`assets/` folder is never copied into the built site, so an image referenced from a page would 404.
The site's own stylesheets already live at `docs/assets/stylesheets/` for that reason.

## Layout

```text
docs/assets/<package>/<shot>.png
```

For example:

```text
docs/assets/hub/dashboard.png
docs/assets/content-guard/content-health.png
docs/assets/media-order/collections.png
docs/assets/environment-manager/sync-deploy.png
docs/assets/shared/backoffice-sections.png
```

Reference them from a page with a path relative to that page:

```markdown
![The Hub dashboard](../assets/hub/dashboard.png)
```

## Capturing

Screenshots are generated rather than taken by hand, so they can be regenerated when the UI moves —
see `docs/shared/screenshot-guide.md` for the states each feature needs, and
`scripts/docs-screenshots.mjs` in the UMBFY.Umbraco.Ecosystem repository for the capture itself.

## Rules

- Only assets that are safe for public distribution.
- No customer or private data: no real names, e-mail addresses, domains, secrets, licence keys or
  confidential content.
- Give every image alt text that describes what it shows, not just the feature name.
