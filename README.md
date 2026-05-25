# rodolfo-alabarca · portfolio

> **Systems Builder — Automation · Data · AI Workflows.**
> Construyo sistemas de automatización, dashboards y agentes de IA con foco en utilidad real para operaciones de negocio. Python · Power BI · SQL.

[![Live](https://img.shields.io/badge/status-live-d97706?style=flat-square)](https://rodolfo-alabarca.netlify.app)
[![Stack](https://img.shields.io/badge/stack-HTML%20·%20CSS%20·%20JS-0a0a0a?style=flat-square)]()
[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)

---

## 🌐 Sitio

**Producción:** [rodolfo-alabarca.netlify.app](https://rodolfo-alabarca.netlify.app)

## ⚙️ Stack

| Capa | Tecnología |
|---|---|
| Markup | HTML5 semántico |
| Estilos | CSS3 con custom properties (sistema de tokens) |
| Comportamiento | JavaScript vanilla (sin framework) |
| Tipografía | Inter · JetBrains Mono (Google Fonts) |
| Formulario | Netlify Forms + fallback a `mailto:` |
| Hosting | Netlify · build sin step (static deploy) |

**Decisión de arquitectura:** zero-build. El portafolio es estático y rápido; no necesita React, Vite, ni npm install. La regla "lo que no agrega valor, no se incluye" aplica también al stack.

---

## 📂 Estructura

```
.
├── index.html              # SPA con view-routing por hash
├── og-image.html           # Plantilla para generar la imagen social (1200×630)
├── og-image.png            # Imagen social generada (Open Graph / Twitter)
├── _redirects              # Netlify: SPA fallback a index.html
├── robots.txt              # Permisos para crawlers
├── sitemap.xml             # Map de URLs públicas
├── netlify.toml            # Cache + security headers
├── assets/
│   └── images/
│       ├── rodolfo.png
│       ├── sommelier-no.png
│       └── dashboard_canapty.png
├── .gitignore
└── README.md
```

---

## 🚀 Local

No hay build step. Para verlo en tu máquina:

```bash
# Opción A — abrir directo
open index.html        # macOS
start index.html       # Windows

# Opción B — servidor local (recomendado: paths absolutos funcionan)
python3 -m http.server 8000
# luego: http://localhost:8000
```

Sirve también con `npx serve` o cualquier server estático.

---

## 🌍 Deploy

Conectado a Netlify desde `main`. Cada push despliega automáticamente:

1. Push a `main` → Netlify detecta cambio.
2. Sin build command, sin publish directory custom → Netlify sirve el repo entero.
3. `_redirects` maneja rutas de SPA (`/work`, `/contact`, etc.).
4. `netlify.toml` aplica cache headers (HTML no-cache, assets long-cache).

**Para redeploy manual:** [app.netlify.com](https://app.netlify.com) → Site → "Trigger deploy" → "Clear cache and deploy site".

---

## 🎨 Decisiones de diseño

- **Paleta:** dark `#0a0a0a` + accent naranja `#d97706`. Aire SaaS / dev-tools sin ser cliché.
- **Tipografía:** Inter (sans humanista) + JetBrains Mono (etiquetas técnicas). Pairing usado por Linear, Vercel, Resend.
- **Bilingüe:** spans `.es` / `.en` toggle por `data-lang` + persistencia en `localStorage`. Sin libs.
- **Routing:** hash-based SPA con `popstate` y `pushState`. Compatible con compartir URLs directas (`#contact`).
- **A11y baseline:** `aria-label`, `prefers-reduced-motion`, `focus-visible`.

---

## 📬 Contacto

- **Email:** [rodophybusiness08@gmail.com](mailto:rodophybusiness08@gmail.com)
- **LinkedIn:** [rodolfo-alabarca](https://www.linkedin.com/in/rodolfo-alabarca-16b187239/)
- **GitHub:** [@RodCode088](https://github.com/RodCode088)

---

## 📄 Licencia

El código de este portafolio es MIT. **El contenido y la identidad visual (copy, imágenes, branding) no.** No reutilizar marca personal.

---

<sub>Built with code and coffee · Panamá · 2026</sub>
