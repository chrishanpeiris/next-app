# Progress Tracker

Update this file whenever the current phase, active feature, or implementation state changes.

Every completed feature gets a log entry under Completed in the form: `Feature NN: Name — what was added and where. Verification status.`

## Current Phase

- Phase 2: Editor chrome (navbar, project sidebar, dialog pattern)

## Current Goal

- Build editor navbar, floating project sidebar, and reusable dialog pattern (spec: `context/feature-specs/02-editor.md`).

## Completed

- Feature 01: Design System — shadcn/ui (base-nova) installed with Button, Card, Dialog, Input, Tabs, Textarea, and ScrollArea added to components/ui/. lucide-react and the `cn()` helper in lib/utils.ts added. Dark theme forced via `dark` class on `<html>`. TypeScript and ESLint clean.
- Feature 02: Editor Chrome — EditorNavbar (fixed top bar with PanelLeftOpen/PanelLeftClose toggle) and ProjectSidebar (floating overlay, slides from left, Projects title + close button, My Projects/Shared tabs with empty states, New Project button) added to components/editor/. Both are rendered by the client layout `app/(editor)/layout.tsx`, which holds the sidebar open/closed state. Dialog pattern confirmed ready via existing components/ui/dialog.tsx and the color tokens in globals.css; no actual dialogs built. TypeScript and ESLint clean.

## In Progress

- None.

## Next Up

- Feature 03: TBD

## Open Questions

- Add unresolved product or implementation questions here.

## Architecture Decisions

- UI primitives come from shadcn/ui (style `base-nova`, built on `@base-ui/react`); generated files in `components/ui/*` must not be modified.
- `cn()` lives in `lib/utils.ts` and re-exports from the `cn` package (shadcn's clsx + tailwind-merge replacement).
- Dark theme only: `dark` class is set on `<html>` in `app/layout.tsx`; theme tokens (oklch CSS variables) live in `app/globals.css` under `:root` / `.dark`, plus `color-scheme: dark`.
- Fonts: Geist Sans/Mono via `next/font`, mapped through `--font-sans` / `--font-mono` in `globals.css`.
- Styling uses Tailwind v4 via `@tailwindcss/turbopack` configured in `next.config.ts`.

## Session Notes

- Boilerplate cleaned up: `public/` SVGs removed; `app/(editor)/page.tsx` is an empty placeholder for the future canvas.
- Editor routes live in the `(editor)` route group; its client layout owns sidebar state and renders the navbar and sidebar around `children`.
- shadcn init generated a circular `--font-sans: var(--font-sans)`; fixed to point at `--font-geist-sans`.
- The dev server can serve stale CSS after `globals.css` edits; restart `npm run dev` (and clear `.next`) if styles look wrong.
- `layout.tsx` metadata still says "Create Next App"; update when the app has a real name.
- Feature 03 is not yet specified; add a spec under `context/feature-specs/` before starting.
