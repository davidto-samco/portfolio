# Portfolio

Personal developer portfolio for **crystalmind.academy**.

## Stack

- **Astro** (static output only — `output: 'static'`)
- **Tailwind CSS** for styling
- No SSR, no server runtime, no Docker

## Build & dev

```bash
npm run dev      # local dev server (http://localhost:4321)
npm run build    # produces ./dist (static files)
npm run preview  # preview the built site locally
```

Always run `npm run build` before declaring frontend work done — type errors and broken imports show up at build time, not in dev.

## Deployment

Served by **nginx** directly on this Ubuntu WSL host. There is no CI/CD pipeline.

Build output (`./dist`) is the deployable artifact — it gets copied to nginx's webroot. When changing build output paths, asset prefixes, or `base` in `astro.config.mjs`, also confirm the nginx config still serves them correctly.

## Conventions

- All routes are static — never introduce API routes, server endpoints, or middleware.
- Prefer Astro components (`.astro`) over framework components. Only reach for React/Vue/Svelte islands if interactivity genuinely requires it, and use `client:visible` / `client:idle` rather than `client:load` when possible.
- Use Tailwind utility classes directly; avoid `@apply` and custom CSS unless the utility approach is genuinely worse.
- Images go through Astro's `<Image>` component or `astro:assets` for optimization.
- Content (blog posts, project entries) belongs in content collections under `src/content/`, not hardcoded in pages.

## Constraints

- The domain `crystalmind.academy` is the canonical URL — set `site` in `astro.config.mjs` accordingly so sitemap/canonical/OG URLs are correct.
- Keep the dependency footprint small. This is a static site; resist adding heavy runtime libraries.
