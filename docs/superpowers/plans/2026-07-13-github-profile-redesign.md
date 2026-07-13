# GitHub Profile Redesign ("JaviWarrior Dark Premium") Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Reescribir el README de perfil y el `header.svg` de `Javiko0420/Javiko0420` con la estética Dark Premium aprobada en `docs/superpowers/specs/2026-07-13-github-profile-redesign-design.md`.

**Architecture:** Dos assets independientes — un `header.svg` self-contained (SVG nativo con animación CSS embebida, sin recursos externos) y un `README.md` con estructura identity-first (About → Stack → Featured → Analytics → Connect → Snake). La verificación final se hace sobre el perfil renderizado en GitHub en modo dark y light.

**Tech Stack:** GitHub-flavored Markdown, SVG nativo + CSS embebido, shields.io (flat-square), github-readme-stats (instancia oficial), workflow snake existente (sin cambios).

## Global Constraints

- Paleta exacta del spec: fondos `#090D13`/`#0A0F14`, superficie `#161B22`, bordes `#21262D`/`#30363D`, texto `#F0F6FC`/`#8B949E`, acento único `#00BFFF`.
- **Prohibido** en SVGs: `@import`, fuentes externas (fonts.googleapis.com), `foreignObject` para texto. Solo font stacks del sistema.
- Badges shields.io **solo** `style=flat-square` con fondo `161B22`. Nunca `for-the-badge`.
- Todo el contenido del README en **inglés**.
- **Prohibido** el atributo `height` fijo en los `<img>` de Analytics.
- Instancia oficial `github-readme-stats.vercel.app` (no la third-party `eight-theta`).
- `.github/workflows/snake.yml` no se toca.
- Mensajes de commit en inglés, concisos, enfocados en el "why".
- El badge de LinkedIn va **sin logo** (`simple-icons` eliminó el ícono de LinkedIn por restricciones de marca; shields.io lo ignoraría en silencio y quedaría inconsistente).

---

### Task 1: Nuevo `header.svg` (Dark Premium, self-contained)

**Files:**
- Modify: `header.svg` (reemplazo completo del contenido)

**Interfaces:**
- Consumes: nada (asset raíz).
- Produces: `./header.svg` — imagen de 800×190 referenciada por `README.md` en Task 2 como `<img src="./header.svg" ...>`.

- [ ] **Step 1: Reemplazar el contenido completo de `header.svg`**

Sobrescribir el archivo con exactamente este contenido:

```xml
<svg viewBox="0 0 800 190" width="800" height="190" fill="none" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Javier Guerrero — JaviWarrior — Full Stack Developer, security-first mindset">
  <defs>
    <radialGradient id="glow" cx="50%" cy="50%" r="50%">
      <stop offset="0%" stop-color="#00BFFF" stop-opacity="0.18"/>
      <stop offset="100%" stop-color="#00BFFF" stop-opacity="0"/>
    </radialGradient>
    <linearGradient id="accent" x1="0" y1="0" x2="1" y2="0">
      <stop offset="0%" stop-color="#00BFFF"/>
      <stop offset="70%" stop-color="#00BFFF" stop-opacity="0.05"/>
      <stop offset="100%" stop-color="#00BFFF" stop-opacity="0"/>
    </linearGradient>
    <clipPath id="card">
      <rect x="1" y="1" width="798" height="188" rx="8"/>
    </clipPath>
  </defs>

  <style>
    .mono { font-family: ui-monospace, 'SF Mono', Menlo, Consolas, monospace; }
    .sans { font-family: -apple-system, 'Segoe UI', system-ui, sans-serif; }
    .glow-circle { animation: breathe 6s ease-in-out infinite; }
    .accent-line {
      transform-box: fill-box;
      transform-origin: left center;
      transform: scaleX(0);
      animation: draw 1.2s ease-out 0.3s forwards;
    }
    .fade { opacity: 0; animation: fadeUp 0.8s ease-out forwards; }
    .d1 { animation-delay: 0.10s; }
    .d2 { animation-delay: 0.25s; }
    .d3 { animation-delay: 0.40s; }
    .d4 { animation-delay: 0.55s; }
    @keyframes breathe { 0%, 100% { opacity: 0.55; } 50% { opacity: 1; } }
    @keyframes draw { to { transform: scaleX(1); } }
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(8px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @media (prefers-reduced-motion: reduce) {
      .glow-circle, .accent-line, .fade { animation: none; }
      .accent-line { transform: scaleX(1); }
      .fade { opacity: 1; }
    }
  </style>

  <!-- Card base -->
  <rect x="1" y="1" width="798" height="188" rx="8" fill="#090D13" stroke="#1C2530" stroke-width="1.5"/>

  <g clip-path="url(#card)">
    <!-- Radial glow, top-right -->
    <circle class="glow-circle" cx="760" cy="10" r="150" fill="url(#glow)"/>
    <!-- Accent line, bottom -->
    <rect class="accent-line" x="1" y="186.5" width="798" height="2.5" fill="url(#accent)"/>
  </g>

  <!-- Label -->
  <text class="mono fade d1" x="34" y="52" font-size="12" letter-spacing="3" fill="#00BFFF">/// JAVIWARRIOR</text>

  <!-- Name -->
  <text class="sans fade d2" x="34" y="94" font-size="36" font-weight="700" letter-spacing="0.3" fill="#F0F6FC">Javier Guerrero</text>

  <!-- Tagline -->
  <text class="sans fade d3" x="34" y="121" font-size="15" fill="#8B949E">Full Stack Developer — security-first mindset</text>

  <!-- Chips -->
  <g class="fade d4">
    <rect x="34" y="138" width="72" height="24" rx="12" fill="none" stroke="#00BFFF" stroke-opacity="0.35"/>
    <text class="mono" x="70" y="154" font-size="10" letter-spacing="1" fill="#00BFFF" text-anchor="middle">NEXT.JS</text>

    <rect x="114" y="138" width="92" height="24" rx="12" fill="none" stroke="#00BFFF" stroke-opacity="0.35"/>
    <text class="mono" x="160" y="154" font-size="10" letter-spacing="1" fill="#00BFFF" text-anchor="middle">TYPESCRIPT</text>

    <rect x="214" y="138" width="72" height="24" rx="12" fill="none" stroke="#00BFFF" stroke-opacity="0.35"/>
    <text class="mono" x="250" y="154" font-size="10" letter-spacing="1" fill="#00BFFF" text-anchor="middle">FLUTTER</text>

    <rect x="294" y="138" width="80" height="24" rx="12" fill="none" stroke="#00BFFF" stroke-opacity="0.35"/>
    <text class="mono" x="334" y="154" font-size="10" letter-spacing="1" fill="#00BFFF" text-anchor="middle">SUPABASE</text>

    <rect x="382" y="138" width="104" height="24" rx="12" fill="none" stroke="#30363D"/>
    <text class="mono" x="434" y="154" font-size="10" letter-spacing="1" fill="#8B949E" text-anchor="middle">BRISBANE, AU</text>
  </g>
</svg>
```

- [ ] **Step 2: Validar XML bien formado**

Run: `xmllint --noout header.svg && echo "XML OK"`
Expected: `XML OK` (sin errores de parseo)

- [ ] **Step 3: Verificar que es self-contained (constraint del spec)**

Run: `grep -nE "foreignObject|@import|googleapis" header.svg || echo "OK: self-contained"`
Expected: `OK: self-contained` (cero coincidencias)

- [ ] **Step 4: Verificación visual en navegador**

Run: `open -a "Google Chrome" "$(pwd)/header.svg"`
Expected (revisar a ojo): fondo oscuro con borde sutil, `/// JAVIWARRIOR` en azul mono, nombre en sans-serif del sistema (NO serif tipo Times — si sale serif, el font stack está mal), tagline gris, 5 chips (4 azules + 1 gris), la línea azul inferior se dibuja al cargar, el glow superior derecho pulsa lentamente.

- [ ] **Step 5: Commit**

```bash
git add header.svg
git commit -m "feat: rebuild header as self-contained native SVG

Replaces foreignObject + Google Fonts (blocked by GitHub's camo CSP,
which broke typography) with native SVG text using system font stacks
and embedded CSS animations."
```

---

### Task 2: Reescribir `README.md` y eliminar assets obsoletos

**Files:**
- Modify: `README.md` (reemplazo completo del contenido)
- Delete: `assets/javiwarriorhud.gif`

**Interfaces:**
- Consumes: `./header.svg` de Task 1 (referenciado en la primera línea del README).
- Produces: `README.md` final que Task 3 publica y verifica. URLs externas usadas: shields.io, github-readme-stats.vercel.app, raw.githubusercontent.com (snake `output` branch).

- [ ] **Step 1: Reemplazar el contenido completo de `README.md`**

Sobrescribir el archivo con exactamente este contenido:

````markdown
<div align="center">
  <a href="https://javiwarrior.com">
    <img src="./header.svg" alt="Javier Guerrero — JaviWarrior · Full Stack Developer, security-first mindset" width="100%" />
  </a>
</div>

## About

Hi, I'm **Javier** — also known as **JaviWarrior**. I'm a Software Analysis & Development Technologist building web and mobile products with a security-first mindset. Founder of [Latin Territory](https://latinterritory.com), a platform connecting the Latin community across Australia.

```ts
const javiWarrior = {
  location: "Brisbane, Australia",
  stack: ["Next.js", "TypeScript", "Flutter", "Supabase"],
  focus: ["Cybersecurity", "AI", "Clean Architecture"],
  currently: "Building Latin Territory 🌏",
  motto: "The best way to predict the future is to create it",
} as const;
```

## Stack

<table>
  <tr>
    <td><code>FRONTEND</code></td>
    <td>
      <img src="https://img.shields.io/badge/Next.js-161B22?style=flat-square&logo=nextdotjs&logoColor=white" alt="Next.js" />
      <img src="https://img.shields.io/badge/React-161B22?style=flat-square&logo=react&logoColor=61DAFB" alt="React" />
      <img src="https://img.shields.io/badge/TypeScript-161B22?style=flat-square&logo=typescript&logoColor=3178C6" alt="TypeScript" />
      <img src="https://img.shields.io/badge/Tailwind_CSS-161B22?style=flat-square&logo=tailwindcss&logoColor=06B6D4" alt="Tailwind CSS" />
    </td>
  </tr>
  <tr>
    <td><code>MOBILE</code></td>
    <td>
      <img src="https://img.shields.io/badge/Flutter-161B22?style=flat-square&logo=flutter&logoColor=54C5F8" alt="Flutter" />
      <img src="https://img.shields.io/badge/Dart-161B22?style=flat-square&logo=dart&logoColor=29B6F6" alt="Dart" />
    </td>
  </tr>
  <tr>
    <td><code>BACKEND&nbsp;&amp;&nbsp;DATA</code></td>
    <td>
      <img src="https://img.shields.io/badge/Supabase-161B22?style=flat-square&logo=supabase&logoColor=3FCF8E" alt="Supabase" />
      <img src="https://img.shields.io/badge/PostgreSQL-161B22?style=flat-square&logo=postgresql&logoColor=4169E1" alt="PostgreSQL" />
      <img src="https://img.shields.io/badge/Python-161B22?style=flat-square&logo=python&logoColor=3776AB" alt="Python" />
    </td>
  </tr>
  <tr>
    <td><code>SECURITY&nbsp;&amp;&nbsp;OPS</code></td>
    <td>
      <img src="https://img.shields.io/badge/OWASP-161B22?style=flat-square&logo=owasp&logoColor=white" alt="OWASP" />
      <img src="https://img.shields.io/badge/Vercel-161B22?style=flat-square&logo=vercel&logoColor=white" alt="Vercel" />
      <img src="https://img.shields.io/badge/Cloudflare-161B22?style=flat-square&logo=cloudflare&logoColor=F38020" alt="Cloudflare" />
      <img src="https://img.shields.io/badge/GitHub_Actions-161B22?style=flat-square&logo=githubactions&logoColor=2088FF" alt="GitHub Actions" />
      <img src="https://img.shields.io/badge/Linux-161B22?style=flat-square&logo=linux&logoColor=FCC624" alt="Linux" />
    </td>
  </tr>
</table>

## Featured

<table width="100%">
  <tr>
    <td>
      <h3>🌏 Latin Territory <sup><code>WEB + MOBILE</code></sup></h3>
      <p>Directory platform connecting Latin businesses, services and community across Australia — web app in Next.js/TypeScript, mobile app in Flutter, backed by Supabase.</p>
      <p><code>NEXT.JS</code> <code>TYPESCRIPT</code> <code>FLUTTER</code> <code>SUPABASE</code></p>
      <p>
        <a href="https://latinterritory.com">🔗 latinterritory.com</a> ·
        <a href="https://github.com/Javiko0420/plataforma-colombiana">📂 Web repo</a> ·
        <a href="https://github.com/Javiko0420/latinterritory-mobile">📱 Mobile repo</a>
      </p>
    </td>
  </tr>
</table>

<table width="100%">
  <tr>
    <td>⚔️ <a href="https://javiwarrior.com"><b>javiwarrior.com</b></a> — Personal site &amp; portfolio: projects, experiments and how to reach me.</td>
  </tr>
</table>

## Analytics

<div align="center">
  <a href="https://github.com/Javiko0420">
    <img src="https://github-readme-stats.vercel.app/api?username=Javiko0420&show_icons=true&hide_border=true&bg_color=0A0F14&title_color=00BFFF&text_color=8B949E&icon_color=00BFFF&include_all_commits=true&count_private=true" alt="Javier's GitHub stats" />
    <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Javiko0420&layout=compact&hide_border=true&bg_color=0A0F14&title_color=00BFFF&text_color=8B949E&langs_count=6" alt="Top languages" />
  </a>
</div>

## Connect

<p>
  <a href="https://javiwarrior.com"><img src="https://img.shields.io/badge/javiwarrior.com-161B22?style=flat-square&logo=googlechrome&logoColor=00BFFF" alt="Website" /></a>
  <a href="https://www.linkedin.com/in/javier-felipe-guerrero-zambrano-8951282b/"><img src="https://img.shields.io/badge/LinkedIn-161B22?style=flat-square" alt="LinkedIn" /></a>
  <a href="mailto:javiguerreroz86@gmail.com"><img src="https://img.shields.io/badge/Email-161B22?style=flat-square&logo=gmail&logoColor=EA4335" alt="Email" /></a>
</p>

---

<div align="center">
  <img src="https://raw.githubusercontent.com/Javiko0420/Javiko0420/output/github-contribution-grid-snake-dark.svg" alt="Contribution snake" />
</div>
````

- [ ] **Step 2: Verificar que los endpoints de Analytics responden 200**

Run:
```bash
curl -s -o /dev/null -w "stats: %{http_code}\n" "https://github-readme-stats.vercel.app/api?username=Javiko0420&show_icons=true&hide_border=true&bg_color=0A0F14&title_color=00BFFF&text_color=8B949E&icon_color=00BFFF&include_all_commits=true&count_private=true"
curl -s -o /dev/null -w "langs: %{http_code}\n" "https://github-readme-stats.vercel.app/api/top-langs/?username=Javiko0420&layout=compact&hide_border=true&bg_color=0A0F14&title_color=00BFFF&text_color=8B949E&langs_count=6"
curl -s -o /dev/null -w "snake: %{http_code}\n" "https://raw.githubusercontent.com/Javiko0420/Javiko0420/output/github-contribution-grid-snake-dark.svg"
```
Expected: `stats: 200`, `langs: 200`, `snake: 200`. (Si stats/langs devuelven 429, la instancia oficial está rate-limited: reintentar en unos minutos antes de asumir error.)

- [ ] **Step 3: Verificar que no quedan elementos legacy ni heights fijos**

Run:
```bash
grep -nE "komarev|demolab|capsule-render|javiwarriorhud|for-the-badge|eight-theta" README.md || echo "OK: legacy removed"
grep -nE '<img[^>]*height=' README.md || echo "OK: no fixed heights"
```
Expected: `OK: legacy removed` y `OK: no fixed heights` (cero coincidencias en ambos).

- [ ] **Step 4: Eliminar el GIF obsoleto**

Run: `git rm assets/javiwarriorhud.gif`
Expected: `rm 'assets/javiwarriorhud.gif'`

- [ ] **Step 5: Commit**

```bash
git add README.md
git commit -m "feat: redesign profile README with Dark Premium theme

Identity-first structure (About > Stack > Featured > Analytics >
Connect). Aligns shown stack with actual work (Next.js/TS/Flutter/
Supabase + security), features Latin Territory as flagship project,
and drops visitor counter, streak card, HUD gif and footer wave.
Compact top-langs layout removes the need for manual height tuning."
```

---

### Task 3: Publicar y verificar el render real en GitHub

**Files:**
- Ninguno (push + verificación del perfil renderizado).

**Interfaces:**
- Consumes: commits de Task 1 y Task 2 en `main`.
- Produces: perfil publicado y verificado; lista de desviaciones si las hay.

- [ ] **Step 1: Push a main**

Run: `git push origin main`
Expected: push exitoso a `main` (sin rechazo).

- [ ] **Step 2: Verificar el perfil renderizado en modo dark**

Abrir `https://github.com/Javiko0420` (sesión con tema dark). Checklist:
- Header: tipografía sans del sistema (no serif), animación de línea y glow corriendo, 5 chips legibles.
- About: code block TypeScript con syntax highlighting.
- Stack: 4 filas, badges flat-square con fondo uniforme oscuro y logos a color.
- Featured: 2 cards-tabla; los bordes de tabla de GitHub se ven como contorno de card.
- Analytics: 2 cards lado a lado, sin recortes ni saltos de altura raros.
- Snake: renderiza al pie tras el divisor.

- [ ] **Step 3: Verificar en modo light**

Abrir `https://github.com/Javiko0420` en ventana de incógnito (GitHub sin sesión usa tema light). Checklist: header y cards de Analytics se ven como "cards oscuras" intencionales sobre fondo claro (self-contained), texto de tablas legible, ningún elemento con texto invisible.

- [ ] **Step 4: Verificar viewport móvil**

Con el perfil abierto, activar el modo responsive del navegador (Cmd+Opt+I → toggle device toolbar, ancho 390px). Checklist: las tablas de Stack y Featured no desbordan horizontalmente, las 2 cards de Analytics se apilan verticalmente sin recortes, el header escala a ancho completo sin distorsión.

- [ ] **Step 5: Verificar los links**

Clic (o `curl -s -o /dev/null -w "%{http_code}\n" <url>`) en:
- `https://latinterritory.com` → 200/redirección válida
- `https://github.com/Javiko0420/plataforma-colombiana` → 200
- `https://github.com/Javiko0420/latinterritory-mobile` → 200
- `https://javiwarrior.com` → 200
- Badge LinkedIn → perfil correcto; badge Email → abre `mailto:javiguerreroz86@gmail.com`

- [ ] **Step 6: Checkpoint de diseño (Featured card)**

Comparar la card de Latin Territory renderizada contra el mockup aprobado. Si la versión en markdown nativo no alcanza el look (decisión documentada en el spec), anotar y proponer como follow-up el SVG custom en `assets/` — **no** improvisarlo dentro de esta ejecución.

- [ ] **Step 7: Recordatorio manual (fuera del repo)**

Sugerir a Javier pinear `plataforma-colombiana` y `latinterritory-mobile` desde la UI del perfil (Customize your pins). No es automatizable desde este repo.
