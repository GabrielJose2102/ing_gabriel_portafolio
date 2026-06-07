# AGENTS.md

High-signal guidance for OpenCode agents working in this repository.

---

## 1. Project Overview
- **Purpose:** Personal portfolio for Gabriel José Torrealba Luque
  (Senior Odoo Consultant & Software Engineer, Barquisimeto, Venezuela).
- **Type:** Static site (single-page).
- **Deploy target:** Vercel (per owner's CV).
- **Stack:** Astro ^6.3.7 + Tailwind CSS ^4.3.0 (via @tailwindcss/vite).
- **Runtime:** Node.js >= 22.12.0.
- **Language config:** TypeScript strict (extends astro/tsconfigs/strict).

---

## 2. Key Developer Commands
- `npm install`          Install dependencies
- `npm run dev`          Dev server (localhost:4321)
- `npm run build`        Production build to ./dist/
- `npm run preview`      Preview production build

---

## 3. Project Structure (real, not template)
- `src/pages/index.astro`           ONLY route; composes the full page
- `src/layouts/MainLayout.astro`    Active layout (dark theme, Inter, OG
                                    tags). Imports `global.css`; root
                                    wrapper has `overflow-x-hidden` to
                                    prevent child overflow from breaking
                                    `mx-auto` centering.
- `src/layouts/Layout.astro`        UNUSED — default Astro template, safe to delete
- `src/components/`                 Active: Navbar, Hero, ServiceCard,
                                    CaseStudyCard, Footer
                                    UNUSED: Welcome.astro (delete candidate)
- `src/components/Footer.astro`    Three-column layout (Contacto | Ubicación
                                    | Conectar). Uses an INNER wrapper
                                    `<div class="mx-auto max-w-5xl …">` to
                                    constrain width to 1024px while the
                                    outer `<footer>` spans the parent.
- `src/styles/global.css`           Tailwind import only (`@import "tailwindcss";`)
- `src/assets/`                     astro.svg + background.svg (UNUSED)
- `public/`                         favicon.svg, favicon.ico,
                                    Curriculum_Gabriel_Torrealba.pdf
- `CONTEXTO_GABRIEL.md.md`          Source of truth for owner's bio/experience

---

## 4. Navigation Map (anchor targets in index.astro)
| Navbar link   | Section id        | Source component       | Status   |
|---------------|-------------------|------------------------|----------|
| #servicios    | servicios         | ServiceCard.astro      | OK       |
| #proyectos    | proyectos         | CaseStudyCard.astro    | OK       |
| #trayectoria  | trayectoria       | — (MISSING)            | BROKEN   |
| #contacto     | contacto          | Footer.astro           | OK       |

---

## 5. Owner Profile (canonical data)
- **Name:** Gabriel José Torrealba Luque
- **Role:** Consultor Senior Odoo & Desarrollador Full-Stack
- **Location:** Barquisimeto, Lara, Venezuela
- **Phone:** +58 0424-578-56-08
- **Email:** gabrieltorrealba09@gmail.com
- **LinkedIn:** linkedin.com/in/gabriel-torrealba-1a5059209/
- **GitHub:**   github.com/GabrielJose2102

### Tech stack (per CV)
- **ERP:** Odoo 17/18 (consulting, custom modules, migrations)
- **Mobile:** Flutter, Dart
- **Web/Backend:** Node.js, Express, Astro, Java, TypeScript, JavaScript
- **UI:** Tailwind CSS, Bootstrap
- **Architecture:** Clean Architecture
- **AI tooling:** Claude Code, Gemini Code Assist, GitHub Copilot,
  NotebookLM, AI agents
- **Infra:** Git/GitHub, Vercel, PostgreSQL, MySQL, REST APIs (BCV)
- **Fiscal domain:** Venezuela localization, SENIAT retentions,
  multi-currency, exchange differential
- **Methodology:** Scrum, requirements analysis

### Featured companies in CV
Transportes GyR · Casagri de Lara · Velas3N · Grupo Supply · Amacorp · Help-Des.CA

---

## 6. Known Issues / Tech Debt
1. `Navbar.astro:5` links to `#trayectoria` but no such section
   exists in `index.astro`.
2. `MainLayout.astro:27` references `/og-image.png` which is missing
   from `public/`.
3. Unused files: `src/components/Welcome.astro`,
   `src/layouts/Layout.astro`, `src/assets/astro.svg`,
   `src/assets/background.svg`.
4. `CaseStudyCard.astro` only shows 3 of the 6 projects listed
   in `CONTEXTO_GABRIEL.md.md`.
5. Skills and Education sections from the CV are not yet rendered
   in the site.
6. Content is hardcoded inside components (no `src/data/` layer).

### Resolved in recent sessions
- ~~`Footer.astro` "Descargar CV" link pointed to `#`~~ → now
  `href="/Curriculum_Gabriel_Torrealba.pdf"` (target="_blank").
- `MainLayout.astro` was missing `import '../styles/global.css';` —
  Tailwind v4 silently produced no utility classes. Fixed by adding
  the import in the frontmatter.
- `MainLayout.astro` root wrapper gained `overflow-x-hidden` to
  prevent child overflow from breaking `mx-auto` layout.
- `Footer.astro` reorganized from a 2-column `lg:items-end` grid
  (visually unbalanced) into 3 labeled columns with an inner
  `max-w-5xl` wrapper for explicit centering.

---

## 7. Conventions
- **Theme:** dark base (slate-950) + emerald-500 accent.
  Preserve this palette in any new section.
- **Components:** Astro (`.astro`) only; no client framework.
- **Data:** currently inlined in components — moving to a
  `src/data/*.ts` module is the preferred refactor path.
- **Comments in code:** DO NOT add comments unless explicitly asked.
- **Commits:** NEVER commit unless the user explicitly asks.
- **Bilingual:** site copy is Spanish; UI labels and code in English.

### Layout pattern: contained blocks inside the page
For section footers/cards that need to look centered and contained
on wide screens, use an inner wrapper:
```astro
<section class="bg-slate-950">
  <div class="mx-auto max-w-5xl px-6 lg:px-8">
    <!-- content -->
  </div>
</section>
```
This decouples background extent (outer) from content width
(inner), avoiding the "glued-to-edge" feel of `max-w-7xl` on
>1280px viewports.

---

## 8. When asked about the site
The single source of truth for biographical and project content is
`CONTEXTO_GABRIEL.md.md`. The site currently exposes a subset of that
content. If asked to "add a section" or "show X from the CV", first
read CONTEXTO_GABRIEL.md.md to extract canonical data, then render
it in the established style.