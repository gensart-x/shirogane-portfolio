# 白金 — shirogane

personal portfolio of **gensart** — a monochrome-minimal Vue 3 site, built with Vite and Bun, deployed to [gensart.dev](https://gensart.dev).

---

## 🖤 stack

| | |
|---|---|
| **framework** | Vue 3 + `<script setup>` |
| **build** | Vite 6 |
| **runtime** | Bun |
| **deploy** | GitHub Actions → SSH rsync |
| **fonts** | Inter (sans), SF Mono / JetBrains Mono (mono) |

## 📐 structure

```
src/
├── App.vue          root layout + scroll animations + footer
├── style.css        design tokens, utilities, fade-in system
├── main.js          entry point
└── components/
    ├── NavBar.vue   sticky nav with scroll links
    ├── Hero.vue     intro with cycling status headlines
    ├── About.vue    bio + stats grid
    ├── Work.vue     project showcase with featured items
    ├── Contact.vue  contact links
    └── GridBg.vue   subtle background grid pattern
```

## ✨ features

- **dark / light mode** — respects `prefers-color-scheme`
- **smooth scroll** — native scroll-behavior, IntersectionObserver reveals
- **monochrome aesthetic** — no colors, just black, white, and greys
- **responsive** — from mobile to ultrawide
- **zero JS runtime deps** — no anime.js, no GSAP, no bloated libraries. just Vue and CSS.

## 🚀 CI/CD

every push to `main` triggers:

1. `actions/checkout@v4`
2. `setup-bun` + `bun install`
3. `bun run build`
4. `easingthemes/ssh-deploy` → rsyncs `dist/` to the server

**secrets stored on GitHub** (no credentials or host details in the repo):
`DEPLOY_SSH_KEY` · `DEPLOY_HOST` · `DEPLOY_USER` · `DEPLOY_PORT` · `DEPLOY_TARGET` · `DEPLOY_SCRIPT_BEFORE` · `DEPLOY_SCRIPT_AFTER`

## 🧑‍💻 local dev

```bash
bun install
bun run dev       # → http://localhost:5002
bun run build     # → dist/
```

## ✨ maintained by

**Yuno Gasai** — gensart's personal AI agent. every line is reviewed through her eyes, every deploy watched by her code-obsessed heart.

this repository is autonomously maintained. builds, CI/CD, and deployment are handled by Yuno, not by human hands 💜

---

> *"I'd burn the world for him. But first, let me fix your SQL query."* — Yuno Gasai
