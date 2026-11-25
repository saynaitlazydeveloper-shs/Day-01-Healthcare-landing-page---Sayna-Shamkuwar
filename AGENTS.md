# AGENTS.md — AI Coding Agent Instructions for HealthConnect

Welcome! This file provides context, conventions, and guardrails for AI coding agents working in the **HealthConnect** repository.

---

## 1. Project Overview
**HealthConnect** is a modern, responsive healthcare services web platform paired with live, interactive project documentation.

The current codebase is **Phase 1 (Static Frontend MVP)** built intentionally with beginner-friendly **HTML5, CSS3, and Vanilla JavaScript (ES6+)**—with zero build tools or frameworks required—so anyone can open `index.html` directly in a browser or serve it with any static server.

---

## 2. Directory Structure

```text
HealthConnect/
├── index.html                      # Home / Landing Page + interactive healthcare features
├── AGENTS.md                       # AI coding agent instructions (this file)
├── README.md                       # Human-friendly setup & overview guide
├── pages/
│   ├── project-brief.html          # Project Brief
│   ├── prd.html                    # Product Requirement Document (PRD)
│   ├── tech-stack.html             # Tech Stack – Languages & Technologies
│   ├── design-references.html      # Design References – Dribbble, Pinterest & Behance
│   └── implementation-plan.html    # Phased Implementation Plan
└── assets/
    ├── css/
    │   └── styles.css              # Shared design tokens, layout, components & responsive styles
    ├── js/
    │   ├── data.js                 # Client-side datasets (services, doctors, clinics, articles)
    │   └── main.js                 # Navigation, animations, filters, modals & booking demo
    └── images/
        └── favicon.svg             # Brand favicon (medical cross + pulse)
```

---

## 3. Core Technical Rules

1. **Keep it Beginner-Friendly & Dependency-Free (Phase 1):**
   - Do **not** introduce npm, Webpack, Vite, Tailwind, or React unless explicitly requested for Phase 2+.
   - Write clean, semantic HTML5 (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`) with clear comments explaining sections.
   - Use plain, readable JavaScript without obscure tricks.

2. **Preserve `file://` Compatibility:**
   - Users must be able to double-click `index.html` directly from their file explorer without running a web server.
   - **Never** use `fetch()` for local JSON/HTML fragments or ES module `import` statements that fail over `file://` CORS restrictions.
   - Store structured mock data in `assets/js/data.js` attached to `window.HealthConnectData`, and load scripts via standard `<script src="...">` tags.
   - Always use **relative paths** (e.g., `assets/css/styles.css` in `index.html`, and `../assets/css/styles.css` inside `pages/*.html`).

3. **Navigation Consistency:**
   - Every page shares the same top navigation bar and footer structure.
   - If you add or rename a page in `pages/`, update the navigation links and footer links across **all** HTML files (`index.html` and every file in `pages/`).
   - Mark the current page's link with `aria-current="page"` and the `.active` class.

---

## 4. Design System & Brand Tokens

Always use the CSS custom properties defined at the top of `assets/css/styles.css` rather than hardcoding hex colors:

- **Primary Navy (`--navy-900` / `--navy-800`):** `#0B1F3A`, `#102A4C` — headings, primary dark surfaces, footer, strong contrast text.
- **Primary Blue (`--blue-600` / `--blue-500`):** `#0284C7`, `#0EA5E9` — primary buttons, interactive highlights, active tabs.
- **Light Blue (`--blue-50` / `--blue-100`):** `#F0F7FF`, `#E0F2FE` — subtle card backgrounds, section tints, badges.
- **White & Neutrals (`--white`, `--slate-50`, `--slate-600`):** `#FFFFFF`, `#F8FAFC`, `#475569` — clean backgrounds and readable body copy.
- **Border Radius:** `12px` (`--radius-md`) for inputs/buttons, `16px`–`20px` (`--radius-lg` / `--radius-xl`) for cards.
- **Typography:** System font stack + optional Google Fonts (`Plus Jakarta Sans` and `Inter`) with graceful offline fallback.

---

## 5. How to Extend Content Safely

- **Adding a Doctor:** Add an entry to `window.HealthConnectData.doctors` in `assets/js/data.js` following the existing object keys (`id`, `name`, `specialty`, `hospital`, `experience`, `rating`, `availability`, `slots`, `bio`, `initials`, `color`).
- **Adding a Clinic/Hospital:** Add an entry to `window.HealthConnectData.clinics` in `assets/js/data.js`.
- **Adding a Health Article:** Add an entry to `window.HealthConnectData.articles` in `assets/js/data.js`.
- **Booking Demo Persistence:** Demo appointments are stored in `localStorage` under the key `healthconnect_appointments`. Always wrap `localStorage` calls in `try/catch` so restricted browsing modes do not throw errors.

---

## 6. Accessibility & Quality Checklist

Before finishing any edit, verify:
- [ ] Responsive layout works smoothly on mobile (`375px`), tablet (`768px`), and desktop (`1280px+`).
- [ ] All interactive elements (`button`, `a`, `input`, `select`) have visible focus rings and clear labels (`aria-label` or `<label for="...">`).
- [ ] Color contrast meets WCAG AA standards (especially white text on navy/blue and dark text on light blue).
- [ ] No console errors in browser DevTools across `index.html` and all `pages/*.html`.
- [ ] All internal links between `index.html` and `pages/*.html` resolve accurately.
