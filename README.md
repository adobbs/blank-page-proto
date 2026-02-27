# blank-page-proto

A reusable prototype template for PMs and designers. Clone this repo as a starting point for each new prototype.

No backend. No database. No auth. Pure front-of-frontend.

---

## Stack

| Tool | Role | Why |
|---|---|---|
| **Next.js 15** | App framework | File-based routing, fast dev server, easy deploys |
| **Mantine v8** | UI component library | Rich, accessible components out of the box — great for rapid prototyping |
| **Zustand** | Session state | Minimal boilerplate, works great with JSON seed data |
| **TypeScript** | Language | Catches mistakes early; AI assistants work better with typed code |

Also included: `@mantine/charts` (Recharts), `@mantine/dates` (Day.js) — ready to use, no extra setup.

---

## Getting Started

```bash
git clone <this-repo> my-prototype
cd my-prototype
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000). You should see a blank white page — that's intentional.

---

## Folder Structure

```
src/
  app/          # Next.js routes — one folder per page
  components/   # Shared UI components (co-locate .module.css here)
  stores/       # Zustand stores — initialized from data/ at session start
  data/         # JSON files — seed/default data (the "database")
  styles/       # Global CSS custom properties and design tokens
```

---

## The JSON → Zustand Data Pattern

JSON files are the source of truth for default data. Zustand stores hydrate from JSON on page load and hold all read/write state for the browser session. **Refreshing the page resets everything to JSON defaults.**

This is intentional. Prototypes demo better when they're predictable.

```
src/data/users.json       ← define your seed data here
src/stores/usersStore.ts  ← import JSON, expose state + actions
src/app/page.tsx          ← call useUsersStore() to read/write
```

See [CLAUDE.md](./CLAUDE.md) for the full Zustand store pattern and code examples.

---

## Working with AI Assistants

This repo includes a `CLAUDE.md` file that primes Claude (or any AI coding assistant) with the architecture, conventions, and guardrails for this template. When you open a chat in Claude Code, it will read `CLAUDE.md` automatically.

Ask it things like:
- "Add a page that lists users from the seed data"
- "Create a Zustand store for tasks with add and complete actions"
- "Add a Mantine DataTable showing the products from data/products.json"
