# Changelog

All notable changes to this project are documented in this file.

## [v1.0.1] - 2026-05-21

### Fixed
- Sidebar (`components/Sidebar.vue`): Implemented Progressive Loading in `setAccordionItems` to render basic layout instantly and defer heavy cache checks (50ms debounce) to avoid blocking Safari/WebKit main thread. This resolves a ~1s UI freeze when switching header categories.
- Sidebar: Stop using direct `pkg` references in components; version is now read from runtime config and displayed as `v{{ version }}`.

### Changed
- `nuxt.config.ts`: Read values from `package.json` for `VERSION` and `UPDATE` (falling back to env vars). Ensures build-time version is available in `runtimeConfig.public`.
- Sidebar styling: version text centered horizontally at the bottom of the sidebar.

### Performance & Impact
- Safari/WebKit: Category switching response time improved from ~1000ms to near-instant.

### Notes for reviewers / QA
- Verify in Safari (macOS or iOS simulator) that switching categories shows no noticeable UI freeze.
- Verify the app version is available at runtime: open console and check `useRuntimeConfig().public.VERSION` or observe `v{{ version }}` in the sidebar.
- If TypeScript complains about importing JSON, the config uses `fs` to read `package.json` at runtime in `nuxt.config.ts`. An alternative is enabling `resolveJsonModule` and importing `package.json` directly.

### Developer tips
- To run a quick dev build and test locally:

```bash
npm install
npm run dev
```

- To verify the runtime config value in a component:

```js
const config = useRuntimeConfig();
console.log(config.public.VERSION);
```

---

*Generated for branch `fix/sidemenu`.*
