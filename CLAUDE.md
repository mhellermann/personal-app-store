# Personal App Store — Project Instructions

This repository is Michael Hellermann's personal app launcher, deployed as a Progressive Web App at:

**Live URL:** https://mhellermann.github.io/personal-app-store/

The launcher is added to the iPhone home screen and acts as a hub for individually-built, custom PWAs hosted in the same repo under `apps/`.

---

## Repo Structure

- `index.html` — the launcher itself. A single self-contained HTML file. Tiles are defined in the `APPS` array near the top of the `<script>` section.
- `apps/` — directory containing individual app files. Each app is a single self-contained HTML file with all CSS/JS inline. Each app is referenced by a tile in the launcher.
- `CLAUDE.md` — this file.

---

## When asked to "build a new app" or "add an app"

Execute all four steps. Do not stop after step 1 or 2.

### Step 1 — Generate the app

Generate a single self-contained HTML file. Constraints:

- Single file. All CSS and JavaScript inline. No build step.
- External dependencies are limited to Google Fonts via `<link>` from `fonts.googleapis.com`. No npm packages, no frameworks, no CDN libraries unless explicitly requested.
- Must be a valid PWA: include `<meta name="viewport">`, `theme-color`, `apple-mobile-web-app-capable="yes"`, `apple-mobile-web-app-status-bar-style="black-translucent"`, and an inline-SVG `apple-touch-icon`.
- Use `localStorage` for persistence. Never assume a backend is available.
- Mobile-first. Assume primary use on iPhone in fullscreen PWA mode. Respect `env(safe-area-inset-*)` for notch/home indicator padding.
- Must respect `prefers-reduced-motion`.

### Step 2 — Save the file

Save to `apps/<kebab-case-name>.html`. Create the `apps/` folder if it does not exist.

### Step 3 — Update `index.html`

Find the `APPS` array near the top of the `<script>` section in `index.html`. Add a new entry **before** any commented-out examples, following the existing pattern exactly:

```javascript
{
  name: "Display Name",       // 1-3 words, title case
  desc: "Short subtitle",     // 2-5 words, sentence case, no period
  url: "https://mhellermann.github.io/personal-app-store/apps/<kebab-case-name>.html",
  monogram: "X",              // single uppercase letter, usually the first letter of name
  category: "Category",       // e.g. Health, Trading, Creative, Reflection
  gradient: "linear-gradient(135deg, #aaa 0%, #bbb 60%, #ccc 100%)"
}
```

Each tile must have a visually distinct gradient — do not duplicate existing ones. Use a three-stop linear gradient at 135° going from a near-black tone, through a mid-tone, to a brighter accent. Pick colors that fit the app's subject (e.g. greens for fitness, blues for finance, warm browns for creative, cool purples for reflection).

### Step 4 — Commit and push

From the repo root:

```
git add .
git commit -m "add <app-name>"
git push
```

Use cached credentials — no auth prompt should appear. After the push, GitHub Pages rebuilds in ~30 seconds. Confirm to the user that the push succeeded and the new tile will be live shortly.

---

## When asked to edit or modify an existing app

1. Read the existing file in `apps/<name>.html` first to understand its current structure.
2. Make the requested changes, preserving the PWA structure and the project aesthetic.
3. If the app's name or description changes, also update the corresponding entry in `index.html`'s `APPS` array.
4. Commit with `git commit -m "update <name>: <what changed>"` and push.

---

## When asked to remove an app

1. Delete the file from `apps/`.
2. Edit `index.html` to remove the corresponding entry from the `APPS` array.
3. Commit with `git commit -m "remove <name>"` and push.

---

## Aesthetic Conventions

The launcher uses a deliberate dark-editorial aesthetic. New apps should harmonize with it unless the user explicitly requests a different look.

**Color palette:**
- Background: `#0a0a0c` (near-black, slightly cool)
- Elevated surfaces: `#131316`
- Primary text ("paper"): `#f5f1e8` (warm off-white)
- Secondary text: `#b8b2a4`
- Faint text / borders: `#6b665b` and `#1f1f23`
- Accent: `#d4a574` (warm bronze)

**Typography:**
- Display / headings: `Fraunces` (variable serif). Italic is encouraged for emphasis.
- Body / UI: `Geist` (modern grotesque).
- Load via Google Fonts: `https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,400;0,9..144,600;1,9..144,300;1,9..144,400&family=Geist:wght@300;400;500;600&display=swap`

**Visual texture:**
- Subtle SVG noise overlay for paper-like grain (see `index.html` for the exact pattern). Optional but encouraged.
- Animations: gentle fade-rise on entry, staggered, with `cubic-bezier(0.2, 0.8, 0.2, 1)` easing. Always wrap in `@media (prefers-reduced-motion: reduce)` guard.

**Tone:**
- Restrained, considered, editorial. Think Braun / Dieter Rams, not iOS consumer-app cheerful.
- Avoid emoji as primary UI elements. Use typographic monograms or simple SVG icons instead.
- Avoid generic AI-stack defaults: no Inter, no purple gradients on white, no rounded-everything Material aesthetic.

---

## Local Path

The repo is cloned locally at `C:\Users\mhell\personal-app-store\` on the trading PC.
Always `cd` to that path before running git commands.

---

## Defaults

- Use Sonnet for app generation unless the user requests Opus.
- Always show the user a one-line summary of what was built and confirm the push succeeded before ending the session.
- If a generation produces an obviously broken app (syntax error, missing closing tag, etc.), fix it before committing rather than asking the user.
