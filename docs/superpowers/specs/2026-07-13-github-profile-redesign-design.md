# Rediseño del perfil de GitHub — "JaviWarrior Dark Premium"

**Fecha:** 2026-07-13
**Repo:** `Javiko0420/Javiko0420` (README de perfil)
**Estado:** Aprobado por Javier (mockups validados en visual companion)

## Objetivo

Rediseño completo del README de perfil. Audiencia principal: comunidad dev / marca
personal "JaviWarrior". Identidad técnica a proyectar: **Full Stack moderno
(Next.js, TypeScript, Flutter, Supabase) con seguridad como ángulo diferenciador**.
Idioma del README: **inglés**.

Reemplaza el tema actual "Stark HUD / terminal futurista" por una estética
**Dark Premium**: fondo GitHub dark, tipografía limpia, un solo acento azul
eléctrico, chips minimalistas. Personalidad sin ruido.

## Sistema visual

| Token | Valor | Uso |
|---|---|---|
| Fondo header/cards | `#090D13` / `#0A0F14` | superficies propias en SVG e imágenes |
| Superficie | `#161B22` | fondo de badges |
| Bordes | `#21262D` / `#30363D` | contornos sutiles |
| Texto principal | `#F0F6FC` | títulos |
| Texto secundario | `#8B949E` | descripciones, labels |
| Acento | `#00BFFF` | único color de marca (continuidad con javiwarrior.com) |

- Tipografía: font stack del sistema (`-apple-system, 'Segoe UI', system-ui, sans-serif`
  + `monospace` para labels técnicos). **Prohibido `@import` de fuentes externas**:
  GitHub las bloquea vía camo/CSP (causa raíz del header roto actual).
- Labels técnicos en monospace con letter-spacing (ej. `/// JAVIWARRIOR`, `FRONTEND`).
- Badges shields.io estilo `flat-square` (nunca `for-the-badge`).

## Estructura (identity-first)

1. **Header** — `header.svg` reescrito
2. **About** — párrafo + code block TypeScript
3. **Stack** — tabla de 4 categorías con badges
4. **Featured** — Latin Territory (insignia) + javiwarrior.com
5. **Analytics** — GitHub Stats + Top Languages
6. **Connect** — 3 badges de contacto
7. **Cierre** — snake animation discreta

## Secciones en detalle

### 1. Header (`header.svg`)

Card oscura self-contained, ancho completo, ~190 px de alto:

- Etiqueta mono `/// JAVIWARRIOR` en `#00BFFF`, letter-spacing amplio
- Nombre "Javier Guerrero" grande (`#F0F6FC`, bold)
- Tagline: "Full Stack Developer — security-first mindset"
- Chips: `NEXT.JS · TYPESCRIPT · FLUTTER · SUPABASE` (azul) + `BRISBANE, AU` (gris)
- Glow radial azul en esquina superior derecha
- Línea de acento inferior con gradiente azul→transparente

**Técnica:** SVG nativo (`<text>`, `<rect>`, `<circle>` — sin `foreignObject` para
el texto). Animación CSS embebida en `<style>` dentro del SVG: la línea de acento
se dibuja al cargar (scaleX/stroke-dashoffset) y el glow "respira" (opacity loop
lento). Fondo propio oscuro → se ve correcto en GitHub dark y light sin necesitar
`<picture>` + `prefers-color-scheme`.

### 2. About

Párrafo corto en inglés con personalidad: Javier / JaviWarrior, Software Analysis
& Development Technologist, security-first, founder de Latin Territory (link).

Code block TypeScript (reemplaza al de Python):

```ts
const javiWarrior = {
  location: "Brisbane, Australia",
  stack: ["Next.js", "TypeScript", "Flutter", "Supabase"],
  focus: ["Cybersecurity", "AI", "Clean Architecture"],
  currently: "Building Latin Territory 🌏",
  motto: "The best way to predict the future is to create it",
} as const;
```

### 3. Stack

Tabla HTML de 4 filas — label mono gris a la izquierda, badges a la derecha:

| Categoría | Tecnologías |
|---|---|
| FRONTEND | Next.js, React, TypeScript, Tailwind CSS |
| MOBILE | Flutter, Dart |
| BACKEND & DATA | Supabase, PostgreSQL, Python |
| SECURITY & OPS | OWASP, Vercel, Cloudflare, GitHub Actions, Linux |

Badges: shields.io `flat-square`, `labelColor`/color de fondo uniforme `#161B22`,
logos oficiales a color. Salen del README: Django, Postman, VS Code, badge de Git/GitHub.

### 4. Featured

- **Latin Territory** (card insignia): título + chip `WEB + MOBILE`, descripción
  (directorio para la comunidad latina en Australia), chips de stack, y 3 links:
  `latinterritory.com` · repo web (`plataforma-colombiana`) · repo mobile
  (`latinterritory-mobile`).
- **javiwarrior.com** (card secundaria): una línea de descripción + link.

**Técnica:** GitHub no permite CSS en markdown. Primera aproximación con los
recursos nativos que GitHub renderiza (tabla HTML / blockquote estructurado).
Si el resultado no alcanza el look del mockup aprobado, la card insignia se
construye como SVG custom en `assets/` (mismo método que el header) con los
links en markdown debajo (un SVG-imagen solo admite un link).

### 5. Analytics

Exactamente 2 cards alineadas:

- `github-readme-stats` API card: `bg_color=0A0F14` (o `transparent`),
  `title_color=00BFFF`, `text_color=8B949E`, `icon_color=00BFFF`, `hide_border=true`,
  `show_icons=true`, `include_all_commits=true`, `count_private=true`
- Top Languages con `layout=compact` (NO donut) y misma paleta — el layout
  compact iguala alturas de forma natural; se prohíben los `height` fijos en `<img>`
  que causaron los 5 commits de ajuste de píxeles.

Instancia: la oficial `github-readme-stats.vercel.app`. La instancia third-party
actual (`github-readme-stats-eight-theta.vercel.app`) se abandona. Opcional a
futuro: self-host en la cuenta Vercel de Javier para evitar rate-limits.

**Se elimina** la streak card (`streak-stats.demolab.com`): servicio inestable.

### 6. Connect

3 badges `flat-square` con la paleta del sistema: Website (javiwarrior.com),
LinkedIn, Email. Sin contador de visitas.

### 7. Cierre

Línea divisoria fina (`#161B22`) + snake animation en versión dark, discreta.
Reutiliza el workflow existente `.github/workflows/snake.yml` y el branch
`output` tal cual — sin cambios de CI.

## Elementos eliminados

- GIF `assets/javiwarriorhud.gif` (y su sección)
- Contador de visitas (komarev)
- Streak card (demolab)
- Footer wave (capsule-render)
- Headers temáticos `< WORKSPACE_MODULE >`, `< DATA_STREAM >`, etc.
- Badges `for-the-badge`
- Code block Python
- Header SVG actual (foreignObject + Google Fonts rotas)

## Archivos afectados

| Archivo | Acción |
|---|---|
| `header.svg` | Reescribir completo (SVG nativo, sin foreignObject/fonts externas) |
| `README.md` | Reescribir completo con la nueva estructura |
| `assets/javiwarriorhud.gif` | Eliminar |
| `assets/` (posible) | Nuevo SVG de card Featured si markdown nativo no alcanza |
| `.github/workflows/snake.yml` | Sin cambios |

## Verificación

1. Renderizar README en GitHub (push a `main`) y revisar en **modo dark y light**.
2. Confirmar que `header.svg` muestra tipografía correcta (sin fuente fallback rota)
   y que las animaciones CSS corren en el README renderizado.
3. Confirmar que las 2 cards de Analytics quedan alineadas sin `height` manual.
4. Revisar en viewport móvil (GitHub responsive) que tablas HTML no desborden.
5. Verificar los 3 links de Featured (sitio, repo web, repo mobile) y los de Connect.

## Fuera de alcance

- Cambios en javiwarrior.com o en los repos de Latin Territory
- Self-hosting de github-readme-stats (solo se documenta como opción)
- Pinned repos del perfil (se gestionan en la UI de GitHub, no en el README) —
  recomendación manual: pinear `plataforma-colombiana` y `latinterritory-mobile`
