---
name: start-from-scratch
description: Interview-driven skill for scaffolding a brand-new frontend website or web app project from zero. Always use this skill whenever the user wants to start a new website, web app, or frontend project "from scratch," asks to scaffold/bootstrap/initialize a new project, or wants help setting up a brand-new repo for a site or app — even if they haven't said what framework or language yet. Runs a short live interview (project type, framework, language, exact versions, build approach, styling), gives best-practice advisory notes based on the picked stack, then always shows the full plan and exact commands and waits for explicit user confirmation before creating any files, folders, or running any install commands. Do not scaffold anything without running this interview and getting confirmation first, even if the user seems to have already stated their stack.
license: MIT
metadata:
  version: 1.0.0
  author: Leong
  repository: https://github.com/zunleong/start-from-scratch
---

# Start From Scratch

A skill for kicking off a brand-new frontend website/web app project the right way: ask the right questions, apply current best practices for whatever stack gets picked, and never touch the filesystem without explicit sign-off.

## Core rule

**Never skip the interview. Never skip the confirmation.** Even if the user's request already mentions a framework ("build me a React site"), still run the interview to fill in the rest (language, version, styling, folder, etc.) and still show the final plan for a yes before creating anything. The only exception: if the user has clearly already answered a question earlier in the same conversation, don't re-ask it — carry that answer into the plan.

## Workflow

1. Run the live interview (all questions below, in order)
2. Generate best-practice advisory notes based on the combination of answers
3. Present the full plan (stack, versions, folder, commands) and advisory notes — **wait for explicit "yes"**
4. If approved, execute; if not, revise based on feedback and re-confirm
5. Wrap up with a short summary of what was created and suggested next steps

---

## Step 1: The interview

Ask these in order. Use whatever question/option UI is available (e.g. quick-select buttons); fall back to plain chat questions if not. Keep it conversational — don't dump all 9 at once if a lighter-weight back-and-forth reads better, but don't skip any.

| # | Question | Notes |
|---|---|---|
| 1 | What kind of site/app is this? | Options: Marketing/landing (mostly static), Web app/dashboard (interactive, data-driven), Blog/CMS-driven, General purpose |
| 2 | Framework? | Options: React / Vue / Vanilla HTML-CSS-JS / Other (let them type it) |
| 3 | Language? | Options: TypeScript / JavaScript / no preference (default to TypeScript if no preference, per best practice) |
| 4 | Exact framework version? | Always ask them to type it (e.g. "React 19.1", "Vue 3.5.13"). If they say "latest" or "don't know," resolve to the current latest stable and confirm the resolved number back to them before proceeding. |
| 5 | Exact language version? | Only if relevant (e.g. TypeScript version). Same "type it, or latest stable" handling as above. |
| 6 | Build approach? | **Only if framework is React or Vue.** Options: plain SPA via Vite, or a meta-framework for SSR (Next.js for React, Nuxt for Vue). Skip this question for Vanilla/Other. |
| 7 | Styling approach? | Options: Tailwind CSS / Plain CSS or CSS Modules / Sass |
| 8 | Project folder/path? | Ask for a path or folder name. If relative, scaffold under the current working directory; if absolute, use as given. |
| 9 | Initialize git? | Yes/No |

**Do not ask about:** package manager (always npm), linting/formatting (always set up), testing frameworks (never set up unless the user separately asks), or extra libraries like routing/state management (never pre-installed — only ever mentioned as advisory notes in step 2).

---

## Step 2: Best-practice advisory notes

After the interview, generate 1–4 short advisory notes based on the specific combination of answers. These are **informational only** — never auto-installed, never presented as a checklist to select from. Just a few sentences in the plan summary. Pull from the guidance below; don't feel bound to only these if something more specific fits the user's answers better.

**By framework + project type:**
- Vue 3 + Web app/dashboard → mention Pinia for state management once local state stops being enough, and Vue Router if the app will have multiple views.
- React + Web app/dashboard → mention TanStack Query for server-state/data-fetching, and React Router or TanStack Router if multiple views are likely. Only mention a state library (Zustand/Redux Toolkit) if the app sounds like it'll have meaningfully complex shared state — don't recommend it reflexively.
- Next.js → mention the App Router's server components model, `next/image` for images, and the `.env.local` / `NEXT_PUBLIC_` prefix convention for env vars.
- Nuxt → mention Nuxt's auto-import conventions, Pinia as the officially recommended state module, and the Nuxt Content module if the project type is Blog/CMS.
- Blog/CMS-driven, any framework → mention either MDX support or a headless CMS client depending on what they've hinted at needing.
- Vanilla → mention that Vite's vanilla template is still a fine choice for build/HMR even without a framework, and that native ES modules keep things simple for a small/marketing site.
- Other (framework not in the shortlist) → don't invent advisory notes; instead note that best-practice specifics will need to be worked out together since the stack isn't one of the common ones.

**By language:**
- TypeScript → mention enabling `strict: true` (and ideally `noUncheckedIndexedAccess`) in `tsconfig.json` from day one — much easier than retrofitting later.

**By styling choice:**
- Tailwind CSS → mention `clsx` or `tailwind-merge` for conditional class logic, and the `@tailwindcss/forms` / `@tailwindcss/typography` plugins if the project type is form-heavy or content-heavy respectively.
- Sass → mention organizing partials with a lightweight 7-1-style pattern (`abstracts/`, `base/`, `components/`, `layout/`) rather than one giant stylesheet.
- Plain CSS/CSS Modules → mention colocating `*.module.css` files next to their components (Vite supports this out of the box).

---

## Step 3: Present the plan and get confirmation

Show a clear, scannable summary — then explicitly ask "Should I go ahead?" and **wait for a clear yes** before doing anything in Step 4. Example shape:

```
Project Plan
------------
Type:        Web app/dashboard
Framework:   Vue 3.5.13
Language:    TypeScript 5.6.3
Build:       Vite (SPA)
Styling:     Tailwind CSS
Folder:      ~/projects/my-app
Git init:    Yes

Best-practice notes:
- Consider Pinia once local component state isn't enough.
- Consider Vue Router if you'll have more than one view.
- Enable `strict: true` in tsconfig.json from the start.

Commands that will run:
1. npm create vite@latest my-app -- --template vue-ts
2. cd my-app && npm install
3. npm install vue@3.5.13
4. npm install -D tailwindcss postcss autoprefixer && npx tailwindcss init -p
5. npm install -D eslint prettier eslint-config-prettier eslint-plugin-vue @typescript-eslint/parser @typescript-eslint/eslint-plugin
6. git init && git add -A && git commit -m "Initial commit"

Proceed?
```

If the user asks for changes, update the relevant answer(s) and re-show the plan before proceeding — don't just proceed on the assumption the change was approved.

---

## Step 4: Execute (only after explicit yes)

Run the commands from the confirmed plan. General patterns per choice:

**Scaffold command by framework:**
- React + Vite: `npm create vite@latest <folder> -- --template react-ts` (or `react` for JS)
- React + Next.js: `npx create-next-app@<version> <folder> --typescript --eslint --tailwind --app --src-dir --import-alias "@/*"` (adjust flags to match actual answers — e.g. drop `--tailwind` if a different styling choice was made)
- Vue + Vite: `npm create vite@latest <folder> -- --template vue-ts` (or `vue` for JS)
- Vue + Nuxt: `npx nuxi@<version> init <folder>`
- Vanilla: `npm create vite@latest <folder> -- --template vanilla-ts` (or `vanilla`)
- Other: no fixed CLI — work out scaffolding manually with the user based on what the framework actually needs

After scaffolding, pin the exact framework/language version the user asked for if the CLI didn't already install that exact version (`npm install <package>@<version>`).

**Styling setup:**
- Tailwind: `npm install -D tailwindcss postcss autoprefixer && npx tailwindcss init -p`, wire up `content` paths in `tailwind.config.js`, add the `@tailwind` directives to the main CSS file.
- Sass: `npm install -D sass`, convert the main stylesheet to `.scss`, set up the partials folders mentioned in the advisory notes.
- Plain CSS/CSS Modules: no extra install needed — just follow the `*.module.css` naming convention for component-scoped styles.

**Linting/formatting (always, every project):**
`npm install -D eslint prettier eslint-config-prettier` plus the framework-appropriate plugin (`eslint-plugin-react`, `eslint-plugin-vue`, etc.) and `@typescript-eslint/parser` + `@typescript-eslint/eslint-plugin` if TypeScript was picked. Set up a flat `eslint.config.js` and a `.prettierrc`.

**Folder structure — scale to project type:**
- Marketing/landing: keep it flat — `src/components/`, `src/assets/`, `src/styles/`.
- Web app/dashboard: `src/components/`, `src/pages/` (or `src/views/` for Vue), `src/hooks/` (React) or `src/composables/` (Vue), `src/services/` (API calls), `src/utils/`, `src/types/` (if TS), plus a `src/router/` if routing came up in advisory notes.
- Blog/CMS: `src/content/` or `src/posts/`, `src/components/`, `src/layouts/`, `src/lib/` (CMS/data client).
- General purpose: default to the Web app/dashboard structure — safer general-purpose default without being bloated for something simpler.

**Git:**
If yes, run `git init`, write a `.gitignore` appropriate to the stack (`node_modules/`, `dist/`, `.env*`, editor folders), and make an initial commit.

---

## Step 5: Wrap up

Give a short summary: what was created, where, and 1–2 concrete next steps (e.g. "run `npm run dev` to start the local server"). Don't repeat the full plan again — they already saw it in Step 3.

---

## Fixed defaults — never asked about, always applied

- Package manager: **npm**
- Linting + formatting (ESLint + Prettier): **always set up**
- Testing framework: **never set up** unless separately requested outside this skill
- Extra libraries (routing, state management, UI kits): **never pre-installed** — only ever mentioned as advisory notes
