# OptiCRM

A patient-centred practice management workspace for independent optical practices.

## Technology

- SvelteKit 3 and Svelte 5
- Plain JavaScript only — no TypeScript
- Tailwind CSS 4
- Lucide icons for Svelte
- PostgreSQL with Drizzle ORM (database integration to be configured)

## Getting started

Requires a current Node.js LTS release.

```sh
npm install
npm run dev
```

Open the local URL printed by Vite.

## Project structure

```
src/
  app.css
  app.html
  lib/
  routes/
    +layout.svelte
    +page.svelte
```

## Current status

The first commit establishes the SvelteKit application shell and an initial practice dashboard using illustrative data. Authentication, database connectivity, patient records, clinical workflows and audit logging are not yet implemented.

Do not use this starter with real patient information. Clinical and operational data protections must be implemented and reviewed before production use.
