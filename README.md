# FamilyNoteHub — Family Note-Taking App

A responsive family note-taking application for organizing daily activities, nutritional intake, and academic assignments. Built with vanilla HTML, CSS, and JavaScript — no frameworks, no build step. Notes persist in `localStorage` and can be reordered across modules via drag-and-drop.

**Live demo:** [familyhubnotes.vercel.app](https://familyhubnotes.vercel.app/)

---

## Screenshots

<img width="1627" alt="Screenshot 2024-04-26 at 2 05 30 PM" src="https://github.com/shuddha2021/FamilyNoteHub-Note-Taking-App/assets/81951239/97688966-8e6b-4196-acbc-a48530d97bd0">
<img width="1646" alt="Screenshot 2024-04-26 at 2 07 10 PM" src="https://github.com/shuddha2021/FamilyNoteHub-Note-Taking-App/assets/81951239/f1f8475e-6136-442a-ab7a-42bae218ffbb">

---

## Features

| Feature | Description |
|---|---|
| **Three Modules** | Daily activities, nutritional intake, and academic assignments — each with its own panel |
| **Drag & Drop** | Reorder notes within a module or move them across modules by dragging |
| **Add / Edit / Delete** | Full CRUD with inline editing and cancel support |
| **Mark Complete** | Toggle completion status with undo capability |
| **Persistent Storage** | JSON-backed `localStorage` — notes survive refresh and browser restart |
| **Clear All** | Confirmation dialog prevents accidental bulk deletion |
| **Toast Notifications** | Brief feedback on every action (added, deleted, moved, etc.) |
| **Responsive** | Mobile-friendly layout with a sticky header and adaptive grid forms |
| **Accessible** | ARIA roles, keyboard navigation (Escape to cancel), focus management |
| **Relative Timestamps** | "just now", "5m ago", "2h ago" — auto-refreshed every minute |
| **v1 Migration** | Automatically migrates notes saved in the old innerHTML format |

## Architecture

```
index.html          Single-file application
├── <style>         Modern CSS: custom properties, flexbox/grid, responsive breakpoints
└── <script>        Vanilla ES6+ JavaScript
    ├── Data layer  JSON in localStorage (keyed as familynotehub_v2)
    ├── Rendering   DOM-built entries (no innerHTML for user data — XSS-safe)
    ├── DnD         Native HTML5 drag-and-drop with visual drop targets
    ├── Dialog      Custom confirm dialog for destructive actions
    └── Migration   v1 (innerHTML) → v2 (JSON) automatic converter
```

## Bug Fixes from Original

| Bug | Impact | Fix |
|---|---|---|
| **XSS via innerHTML** | User input injected raw into `innerHTML` — script injection possible | All user text set via `textContent`; data stored as JSON |
| **Edit broke nutrition/academic** | `editEntry()` split `<strong>` text on `:` but details were in a separate span | Edit reads structured data from the JSON store, not from DOM |
| **Nav highlight mismatch** | CSS styled `.current a` (class on `<li>`) but JS added `current` to `<a>` | Replaced with ARIA `aria-selected` on `<button>` tabs |
| **Drag-and-drop missing** | README claimed DnD but no implementation existed | Full native DnD: reorder within module + move across modules |
| **No undo for completion** | Once completed, entries could not be reverted | Added ↩ undo button on completed entries |
| **No delete confirmation** | Accidental "Clear All" wiped everything with no recovery | Confirm dialog with cancel for all bulk deletes |

## Tech Stack

- **HTML5** — semantic markup with `<header>`, `<main>`, `<section>`, `<nav>`
- **CSS3** — custom properties, flexbox & grid, `@keyframes`, responsive `@media`
- **JavaScript (ES6+)** — `const`/`let`, template literals, arrow functions, async/await, event delegation, native drag-and-drop API

## Getting Started

```bash
git clone https://github.com/shuddha2021/FamilyNoteHub-Note-Taking-App.git
cd FamilyNoteHub-Note-Taking-App
open index.html          # macOS
# or: xdg-open index.html   # Linux
# or: start index.html       # Windows
```

No dependencies. No build step. Just open in a browser.

## Author

**Shuddha Chowdhury** — [github.com/shuddha2021](https://github.com/shuddha2021)

## License

MIT
