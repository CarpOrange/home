# Repository Guidelines

## Project Structure & Module Organization
This repository is a Vue 3 + Vite single-page site. Application code lives in `src/`: components in `src/components`, views in `src/views`, state in `src/store`, API helpers in `src/api`, utilities in `src/utils`, and static data in `src/assets/*.json`. Global styles are in `src/style`. Public icons, fonts, and background images belong in `public/`. Build output is generated into `dist/` and should not be edited by hand.

## Build, Test, and Development Commands
Prefer `pnpm`; the repo includes `pnpm-lock.yaml`.

- `pnpm install`: install dependencies.
- `pnpm dev`: start the Vite dev server on port `3000`.
- `pnpm build`: create the production bundle in `dist/`.
- `pnpm preview`: serve the built app locally for a final check.
- `pnpm lint`: run ESLint across `.js`, `.ts`, and `.vue` files with autofix.
- `pnpm format`: run Prettier on `src/`.

## Coding Style & Naming Conventions
Follow the existing Vue SFC pattern and ES modules. Prettier enforces 2-space indentation, double quotes, semicolons, trailing commas, and a 100-character print width. ESLint uses `eslint:recommended` plus `plugin:vue/vue3-essential`; keep files lint-clean before opening a PR.

Use `PascalCase` for shared component filenames such as `Background.vue` and `Footer.vue`. Keep view entry files as `src/views/<Feature>/index.vue` when extending an existing section. Use `camelCase` for utility modules such as `getTime.js`. Import app-local modules through the `@` alias.

## Testing Guidelines
There is no dedicated unit-test suite today. Treat `pnpm lint` and `pnpm build` as the minimum validation gate before submitting changes. For UI changes, verify desktop and mobile layouts and include screenshots when the visible result changes. When editing `.env`-driven features, test with a local `.env` copied from `.env.example`.

## Configuration Notes
Branding is branch-sensitive. This project can serve personal or company variants, and `VITE_SITE_NAME` plus related `VITE_SITE_*` values may intentionally differ by branch. Do not normalize these values across branches unless the change is meant for every deployment target. When changing branding, document which branch or environment the update belongs to.

## Commit & Pull Request Guidelines
Keep commits small and focused. Recent history uses short, imperative subjects tied to the change, for example `Create test.yml` or `Delete .github/workflows/main.yml`. Follow that pattern: one concern per commit, clear action verb first.

PRs should include a concise summary, required environment/config changes, linked issues when applicable, and screenshots for visual updates. Call out changes to `src/assets/*.json`, `.env.example`, branch-specific branding, or deployment workflows because they affect downstream setup.
