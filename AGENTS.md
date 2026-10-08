# Repository Guidelines

## Project Structure & Module Organization

This repository contains two independent TypeScript packages:

- `frontend/`: React application built with Vite. `src/main.tsx` mounts `src/App.tsx`; styles live in `src/*.css`, imported images in `src/assets/`, and public files in `public/`.
- `backend/`: Hono API targeting Cloudflare Workers. Routes currently live in `src/index.ts`; Worker settings and bindings belong in `wrangler.jsonc`.

Each package has its own `package.json`, `package-lock.json`, and TypeScript configuration. There is no root package or shared build command, and no test directory currently exists.

## Build, Test, and Development Commands

Run commands from the relevant package directory. Install dependencies with `npm ci` in both `frontend/` and `backend/`.

- Frontend `npm run dev`: start Vite with hot reload.
- Frontend `npm run build`: run TypeScript checks and generate production assets in `dist/`.
- Frontend `npm run lint`: run Oxlint.
- Frontend `npm run preview`: serve the production build locally.
- Backend `npm run dev`: run the Worker locally through Wrangler.
- Backend `npm run cf-typegen`: regenerate `CloudflareBindings` types after changing Worker bindings.
- Backend `npm run deploy`: publish the Worker to Cloudflare; use only for an intended deployment.

## Coding Style & Naming Conventions

Follow existing code: two-space indentation, single-quoted TypeScript strings, no semicolons, and ES module imports. Use PascalCase for React components, camelCase for functions and variables, and descriptive asset names. Keep frontend UI code and backend routes in their respective packages. Oxlint is configured as a frontend command; no dedicated formatter is configured.

## Testing Guidelines

Neither package currently defines a test runner, test script, or coverage threshold. Before submitting changes, run the frontend build and lint commands, exercise affected UI behavior locally, and verify changed API routes with Wrangler running, for example `curl http://localhost:8787/`. If adding automated tests, document the chosen framework and runnable command; use descriptive names such as `App.test.tsx` or `routes.test.ts`.

## Commit & Pull Request Guidelines

Git history currently contains only `react hono init`, so no established commit convention exists. Use concise, imperative commit subjects describing the change. Pull requests should explain the behavior changed, identify affected packages, list validation performed, link relevant issues, and include screenshots for visible UI changes.
