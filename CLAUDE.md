# CLAUDE.md — AI Assistant Guide

This is a **prototype template** for PMs and designers. It is not a production app.
Your job is to help non-technical users vibe-code working UI prototypes quickly.

---

## What This Is

A Next.js + Mantine UI prototype starter. No backend, no database, no auth, no API routes.
Pure front-of-frontend: pages, components, and ephemeral session state. Ship fast, look good.

---

## Data Architecture

```
src/data/*.json   →   src/stores/*.ts (Zustand)   →   UI components
  (seed/defaults)        (session state)
```

- **JSON files** are the source of truth for default/seed data. They are read-only at runtime.
- **Zustand stores** hydrate from JSON on page load and hold all read/write state for the session.
- **Refreshing the page resets state** to JSON defaults. This is intentional — great for demos.
- Do not use `localStorage`, cookies, or any persistence. Prototypes reset. That's the point.

### Adding a new data entity

1. Create `src/data/things.json` with your seed data array.
2. Create `src/stores/thingsStore.ts` — import the JSON, initialize Zustand state from it, expose actions.
3. Use the store in components via `useThingsStore()`.

---

## Folder Conventions

| Folder | Purpose |
|---|---|
| `src/app/` | Next.js App Router pages and layouts. One folder per route. |
| `src/components/` | Shared UI components. Co-locate `.module.css` next to each component. |
| `src/stores/` | Zustand stores. One file per domain entity. |
| `src/data/` | JSON seed data. One file per entity type. |
| `src/styles/` | Global CSS custom properties, design tokens, Mantine theme overrides. |

---

## Adding a New Page

1. Create `src/app/my-page/page.tsx`
2. Export a default React component
3. Navigate to `/my-page` in the browser

No routing config needed — Next.js App Router handles it automatically.

---

## Mantine Usage

- Mantine is the primary UI component library. Use it for everything: layout, forms, modals, tables.
- Import components from `@mantine/core`: `Button`, `Stack`, `Group`, `Text`, `Title`, `Card`, etc.
- For charts use `@mantine/charts` (built on Recharts). For date pickers use `@mantine/dates`.
- `MantineProvider` is already set up in `layout.tsx`. Do not add it again.
- For theming, pass a `theme` prop to `<MantineProvider>` in `layout.tsx`.
- Design tokens and global overrides go in `src/styles/` as CSS custom properties.

---

## Zustand Store Pattern

```ts
// src/stores/exampleStore.ts
import { create } from 'zustand';
import seedData from '../data/example.json';

interface Item {
  id: string;
  name: string;
}

interface ExampleStore {
  items: Item[];
  addItem: (item: Item) => void;
  removeItem: (id: string) => void;
}

export const useExampleStore = create<ExampleStore>((set) => ({
  items: seedData,
  addItem: (item) => set((state) => ({ items: [...state.items, item] })),
  removeItem: (id) => set((state) => ({ items: state.items.filter((i) => i.id !== id) })),
}));
```

---

## What NOT To Do

- **No API routes** — do not create `src/app/api/` routes
- **No server actions** — do not use `'use server'` or `next/server`
- **No external databases** — no Prisma, Supabase, Firebase, etc.
- **No authentication** — no NextAuth, Clerk, or session management
- **No localStorage/sessionStorage** — state resets on refresh by design
- **No environment variables for secrets** — there are no secrets; this is a prototype
- **No SSR data fetching** — no `getServerSideProps`, no `fetch` in server components for real APIs
- **Do not add a backend** — if the PM asks for "real data", use JSON files

---

## Quick Reference

```bash
npm run dev      # Start dev server at localhost:3000
npm run build    # Type-check and build
npm run lint     # Run ESLint
```
