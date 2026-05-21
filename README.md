# Diamond Clinic — Frontend (Nuxt)

This repository contains the Nuxt-based frontend for Diamond Clinic.

Purpose: provide a small, clear developer guide using `npm` to get contributors productive quickly.

## Requirements
- Node.js 18+ (LTS recommended)
- npm 8+ (bundled with Node.js)

## Quick start (npm)
Install dependencies and run the app locally:

```bash
npm install
npm run dev
```

Open http://localhost:3004

## Important npm scripts
- `npm run dev` — start dev server
- `npm run build` — build production assets
- `npm run preview` — preview production build locally
- `npm run lint` — run ESLint (if configured)
- `npm run format` — run code formatter (if configured)

If any script is missing, check `package.json` and add it consistently.

## Environment / Runtime config
- Environment variables are read through Nuxt runtime config.
- The important public variables are set in `runtimeConfig.public` — see `nuxt.config.ts`.
- `VERSION` is sourced from `package.json` during config build and exposed via `useRuntimeConfig().public.VERSION` (displayed in `components/Sidebar.vue`).

To set env variables locally, create a `.env` file at project root with keys like:
```
API_URL=https://api.example.com
```

## Development notes and tips
- Progressive loading: `components/Sidebar.vue` implements progressive loading in `setAccordionItems` to avoid blocking Safari/WebKit when switching categories. If you are modifying that code, ensure heavy image/cache checks remain off the main render path.
- Versioning: update `package.json` `version` field to change the runtime `VERSION` exposed to the app.
- If TypeScript complains about JSON imports, this project reads `package.json` from `nuxt.config.ts` using `fs` — no extra compiler options required.

## Testing & QA checklist
- Verify the Safari/WebKit fix: on Safari (or iOS simulator) switch header categories and confirm there is no ~1s freeze.
- Verify version display: open the sidebar and confirm `v<version>` matches `package.json`.

## PWA / Service Worker
- Service worker is configured via `@vite-pwa/nuxt` with `injectManifest` using `service-worker/sw.ts`.
- When modifying caching or asset globs, test both dev and production builds.

## Building & deploying
```bash
npm run build
npm run preview
```

For deployment, follow Nuxt deployment guides for your platform. The app outputs static and server assets depending on your target.

## Contributing
- Branch naming: use descriptive branch names, e.g. `fix/sidemenu`, `feature/auth`, `chore/deps`.
- Update `CHANGELOG.md` for any user-visible changes and reference the branch/PR.
- Open a Pull Request against `develop` (default branch) with a clear description and QA steps.

## Troubleshooting
- If the runtime `VERSION` is missing, ensure `nuxt.config.ts` successfully reads `package.json` and that environment variables don't override it.
- If Safari shows UI freezes when switching categories, review `setAccordionItems` in `components/Sidebar.vue` and ensure heavy image/cache checks are performed asynchronously.

## Useful commands
```bash
# install
npm install

# dev
npm run dev

# build
npm run build
npm run preview

# lint / format (if configured)
npm run lint
npm run format
```

---
Last updated: 2026-05-21 — branch `fix/sidemenu`.
