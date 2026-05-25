# 🚀 Guía Git + GitHub + Netlify — para Rodolfo

Esta es **tu** guía personal, no es del público. La uso para enseñarte cómo piensa un dev senior cuando despliega un sitio. **Léela completa antes de ejecutar nada.** Después la sigues paso a paso.

---

## Parte 0 — Mental model de Git (5 min de lectura)

Antes de tocar un comando, necesitas entender qué representa cada cosa. Si lo haces sin esto, vas a copiar y pegar sin saber qué pasa cuando algo falla.

### Las 4 capas

```
1. Working directory  →  Los archivos en tu carpeta. Lo que ves en el explorador.
2. Staging area       →  La "lista de cambios que voy a empaquetar en el próximo commit".
3. Local repo (.git)  →  El historial de commits que vive en tu máquina.
4. Remote (GitHub)    →  El historial sincronizado en la nube.
```

Cada comando mueve archivos entre estas capas:

```
[Working]  --git add-->  [Staging]  --git commit-->  [Local]  --git push-->  [Remote]
```

### Conceptos críticos

**Commit.** Un snapshot del estado del repo en un momento. No es "guardar el archivo" — es decir "este conjunto de cambios es una unidad lógica". Buen commit = un cambio coherente con un mensaje que lo explica.

**Branch (rama).** Una línea de historia. La principal se llama `main`. Cuando empiezas un experimento, abres una rama nueva para no romper `main`. Al terminar, "merge" la rama de vuelta.

**Remote.** Un nombre que apunta a un repo en otra parte (típicamente GitHub). El remote por defecto se llama `origin`.

**Pull vs Push.**
- `git pull` = traer cambios del remoto a tu máquina.
- `git push` = mandar tus cambios al remoto.

### Por qué un senior piensa en commits

Un junior hace un commit de "cosas varias" cada semana. Un senior hace un commit por cambio lógico, y el mensaje del commit explica **el porqué**, no el qué.

Mal:
```
"updates"
"fix"
"more changes"
```

Bien:
```
"feat: añadir Open Graph + Twitter Cards al index"
"fix: corregir href absoluto del logo (apuntaba a ruta local)"
"refactor: mover imágenes a assets/images y limpiar paths"
"a11y: agregar prefers-reduced-motion y focus-visible"
```

**Convención que voy a usar contigo: Conventional Commits.**
- `feat:` nueva funcionalidad
- `fix:` corrección de bug
- `refactor:` cambio interno sin cambio de comportamiento
- `style:` solo CSS / formato
- `docs:` documentación
- `chore:` mantenimiento (gitignore, configs)
- `a11y:` accesibilidad
- `perf:` performance

---

## Parte 1 — Setup inicial en tu máquina (una vez por máquina, ~3 min)

### 1.1 Verificar Git instalado

Abre PowerShell (Windows) o Terminal (macOS). Escribe:

```bash
git --version
```

Si te devuelve un número (ej. `git version 2.44.0`), está instalado. Si dice "command not found", descarga e instala desde [git-scm.com/downloads](https://git-scm.com/downloads).

### 1.2 Configurar tu identidad

Esto NO es opcional. Cada commit lleva tu nombre y email. Si no los configuras, GitHub no te reconoce como autor.

```bash
git config --global user.name "Rodolfo Alabarca"
git config --global user.email "rodophybusiness08@gmail.com"
```

> **Nota:** este email es el mismo de tu cuenta de GitHub. Si tu GitHub usa otro email, ponlo aquí. De lo contrario, los commits no van a aparecer asociados a tu perfil.

### 1.3 (Opcional, recomendado) Configurar editor por defecto

Cuando Git te pida un mensaje de commit largo, abre un editor. Si tienes VS Code:

```bash
git config --global core.editor "code --wait"
```

### 1.4 (Recomendado) Renombrar la rama por defecto a `main`

GitHub usa `main` (no `master`). Para que tu primer commit nazca ya en `main`:

```bash
git config --global init.defaultBranch main
```

---

## Parte 2 — Preparar el folder de tu proyecto (~5 min)

### 2.1 Estructura final

Te paso lo que debe ver Git cuando arranques. Te lo doy como árbol:

```
portfolio/                       ← carpeta raíz (tu nombre, ej. portfolio-rodolfo)
├── index.html                   ← (yo te lo entregué actualizado)
├── og-image.html                ← (yo te lo entregué)
├── og-image.png                 ← (lo generas tú con DevTools, ver Acción 1 del mensaje anterior)
├── README.md                    ← (yo te lo entregué)
├── _redirects                   ← (yo te lo entregué — sin extensión)
├── robots.txt                   ← (yo te lo entregué)
├── sitemap.xml                  ← (yo te lo entregué)
├── netlify.toml                 ← (yo te lo entregué)
├── .gitignore                   ← (yo te lo entregué — empieza con punto)
├── GUIA_DEPLOY.md               ← (este archivo — opcional commitearlo)
└── assets/
    └── images/
        ├── rodolfo.png          ← (lo copias de tu folder original / index_files/)
        ├── sommelier-no.png     ← (lo copias de tu folder original / index_files/)
        └── dashboard_canapty.png ← (lo copias de tu folder original / index_files/)
```

### 2.2 Pasos concretos

**Paso A — Crear la carpeta del proyecto.** En la ubicación que prefieras (ej. `Documents/PROYECTOS PROFESIONALES/`):

```bash
mkdir portfolio-rodolfo
cd portfolio-rodolfo
```

**Paso B — Copiar los archivos que yo te entregué.** Todos los archivos están en la carpeta de outputs de esta sesión. Cópialos a `portfolio-rodolfo/`:
- `index.html`
- `og-image.html`
- `README.md`
- `_redirects`
- `robots.txt`
- `sitemap.xml`
- `netlify.toml`
- `.gitignore`
- (`GUIA_DEPLOY.md` es opcional — si lo commiteas será visible en el repo público)

**Paso C — Crear la carpeta de assets:**

```bash
mkdir -p assets/images
```

**Paso D — Mover tus PNGs originales a `assets/images/`.** Estos están en tu folder original, dentro de `index_files/`:
- `rodolfo.png`
- `sommelier-no.png`
- `dashboard_canapty.png`

Cópialos a `portfolio-rodolfo/assets/images/`.

**Paso E — Generar `og-image.png`** (si aún no lo hiciste):
1. Abre `og-image.html` en Chrome.
2. F12 → "Toggle device toolbar" → resolución 1200 × 630.
3. Menú 3 puntos de DevTools → "Capture screenshot".
4. Renombra el PNG a `og-image.png` y mételo a la raíz del folder.

**Paso F — Verificar.** Abre `index.html` en doble clic. Deberías ver:
- Tu foto cargada.
- Los previews de Sommelier y Dashboard cargados.
- Solo dos casos en Work (no "Plataforma Foodie").
- Sin badge verde "Open to Work" en el retrato.
- Ícono naranja "R" en la pestaña del navegador.

Si algo no carga, revisa los nombres de los archivos en `assets/images/` — deben ser exactamente: `rodolfo.png`, `sommelier-no.png`, `dashboard_canapty.png`. Distingue mayúsculas.

---

## Parte 3 — Inicializar Git y hacer el primer commit (~3 min)

Desde dentro de `portfolio-rodolfo/`:

```bash
# 1. Inicializa el repo. Crea la carpeta oculta .git/
git init

# 2. Mira qué archivos detecta Git como nuevos
git status
# Deberías ver tus archivos en rojo bajo "Untracked files".

# 3. Agrégalos todos al staging area
git add .

# 4. Verifica que están listos para commit
git status
# Ahora todos los archivos deben aparecer en verde bajo "Changes to be committed".

# 5. Hace el primer commit
git commit -m "feat: initial portfolio commit — production-ready static site"
```

> **Por qué el mensaje así:** "feat" indica funcionalidad nueva; el resto explica brevemente que es la versión inicial lista para producción.

---

## Parte 4 — Conectar con GitHub (~5 min)

### 4.1 Crear el repo en GitHub

1. Entra a [github.com/new](https://github.com/new).
2. **Owner:** tu usuario (`RodCode088`).
3. **Repository name:** `portfolio` (corto y limpio — *evita* nombres tipo `rodolfo-portfolio-final-v2`).
4. **Description:** `Portfolio personal — Systems Builder · Automation · AI`
5. **Public.** Sí, público. Es tu carta de presentación.
6. **NO** marques "Initialize this repository with a README". Ya tienes uno.
7. Click "Create repository".

GitHub te muestra una pantalla con instrucciones. Mira la sección **"…or push an existing repository from the command line"**. Es lo que vas a usar.

### 4.2 Conectar tu repo local con el remoto

GitHub te da algo así (con tu username):

```bash
git remote add origin https://github.com/RodCode088/portfolio.git
git branch -M main
git push -u origin main
```

**Qué hace cada uno:**

1. `git remote add origin <URL>` → registra ese GitHub URL bajo el alias `origin`. Desde ahora cuando digas `git push origin`, sabe a dónde mandar.
2. `git branch -M main` → fuerza el nombre de tu rama actual a `main` (por si Git le había puesto `master`).
3. `git push -u origin main` → manda todos tus commits al remoto. El `-u` le dice "y desde ahora, esta rama local trackea esa rama remota" (te ahorra escribir `origin main` en futuros pushes).

**Te va a pedir autenticación.** Hay dos formas:

- **Recomendada — Personal Access Token:** Settings de GitHub → Developer settings → Personal access tokens → Tokens (classic) → Generate new token. Marca `repo` scope. Cópialo. Cuando Git te pida password, pega el token (no tu password).
- **Más fácil pero más pesada:** instala GitHub CLI (`gh auth login`).

### 4.3 Verifica en GitHub

Recarga `github.com/RodCode088/portfolio`. Tienes que ver tus archivos. Si tu README se ve renderizado en la página, el primer push funcionó.

---

## Parte 5 — Deploy a Netlify (~5 min)

### 5.1 Conectar el repo

1. Entra a [app.netlify.com](https://app.netlify.com). Crea cuenta gratis si no tienes (usa "Sign up with GitHub" para evitar fricción).
2. Click **"Add new site"** → **"Import an existing project"**.
3. Selecciona **"Deploy with GitHub"** y autoriza Netlify a leer tus repos.
4. Busca y selecciona `portfolio`.
5. **Build settings — déjalos vacíos:**
   - Build command: *(vacío)*
   - Publish directory: `.` *(punto, significa "raíz del repo")*
6. Click **"Deploy site"**.

Netlify va a crear un subdominio random tipo `glittering-pixie-a1b2c3.netlify.app`. Lo cambiamos ya.

### 5.2 Cambiar el subdominio

1. En el dashboard del site, **Site configuration** → **Domain management** → **Site name** → **"Edit site name"**.
2. Cambia a `rodolfo-alabarca`.
3. Save.

Tu sitio ahora vive en: **`https://rodolfo-alabarca.netlify.app`**.

### 5.3 Verificar headers y forms

- Visita tu URL. Inspecciona (F12) → Network → recarga → click en el documento HTML → tab "Headers". Deberías ver `cache-control: public, max-age=0, must-revalidate`, `x-frame-options: DENY`, etc. Si están, `netlify.toml` se aplicó.
- Ve a **Forms** en el panel de Netlify. Tu formulario `contact` debería aparecer detectado. Manda un mensaje de prueba desde la web — debería aparecer.

### 5.4 Compartir el link y validar el OG

Hay una herramienta increíble: [opengraph.xyz](https://www.opengraph.xyz/url/). Pega tu URL. Te muestra preview exacto como aparece en LinkedIn, Twitter, WhatsApp, Slack y Facebook. Validación 100% pre-launch.

---

## Parte 6 — Workflow continuo (de aquí en adelante)

Cuando hagas cualquier cambio al portafolio:

```bash
# Trabaja en los archivos como siempre

# 1. Ver qué cambió
git status
git diff           # muestra los cambios línea por línea

# 2. Agregar al staging (selectivo si quieres)
git add archivo-modificado.html
# o todo:
git add .

# 3. Commit con mensaje descriptivo
git commit -m "feat: agregar testimonial de Nelvin al caso Sommelier"

# 4. Push
git push
```

Netlify detecta el push automáticamente y redeploya. En ~30 segundos tu cambio está vivo.

### Si rompes algo y quieres revertir

```bash
# Ver historial
git log --oneline

# Volver el working directory al commit anterior (NO destructivo)
git checkout HEAD~1 -- archivo-roto.html

# O resetear todos los cambios sin commit
git checkout .
```

### Cuando vayas a agregar features grandes (Tier 3 del roadmap)

Usa ramas. Ejemplo: cuando quieras agregar el background tecnológico:

```bash
git checkout -b feat/tech-background       # crea y entra a rama nueva
# trabajas tranquilo, haces commits ahí
git push -u origin feat/tech-background    # subes la rama
# en GitHub abres un PR (Pull Request) de feat/tech-background → main
# cuando estés feliz, mergeas vía botón de GitHub
```

Esto te da: trabajo aislado, preview deploy automático en Netlify (sí — cada rama tiene su URL de preview), y la posibilidad de descartar si no funciona.

---

## Parte 7 — Errores comunes (lee esto si algo falla)

**`fatal: not a git repository`** → estás corriendo `git` fuera de la carpeta del proyecto. `cd` a `portfolio-rodolfo/`.

**`Updates were rejected because the remote contains work that you do not have locally`** → alguien (¿GitHub auto-inicializó?) tiene commits que tú no tienes. Solución: `git pull origin main --rebase` y luego `git push`.

**`Authentication failed`** → ya no se acepta password de GitHub. Usa Personal Access Token (ver Parte 4.2).

**Netlify dice "Site deploy failed"** → entra al deploy log. 99% de veces es ruta mal escrita en `netlify.toml` o `_redirects`.

**Las imágenes no cargan en producción pero sí localmente** → diferencia entre Windows (case-insensitive) y Linux/Netlify (case-sensitive). `Rodolfo.PNG` ≠ `rodolfo.png`. Verifica nombres exactos.

**El form no recibe nada** → Netlify Forms necesita que el HTML del form esté en el primer build. Cada vez que cambies el form, hay que redeployar. Si el form todavía no aparece detectado: Site → Forms → "Verify HTML form detection" → forzar rebuild.

---

## Parte 8 — Qué viene después (Tier 3+, post-launch)

Una vez que el site esté vivo y validado, vamos por estos en orden:

1. **Analytics privacy-first** (Plausible o Umami): sin cookies, sin GDPR drama, ~5 min de setup.
2. **Background tecnológico**: efecto de profundidad con Canvas 2D.
3. **Comentarios profesionales en código**: separación CSS → archivo, sección de comentarios por bloque.
4. **CV descargable** (PDF generado desde un HTML print template — mismo enfoque que `og-image.html`).
5. **Testimoniales reales** (te paso plantilla de mensaje a Nelvin cuando lleguemos ahí).
6. **Dominio propio** cuando estés listo.

---

## Resumen TL;DR para mañana

```bash
# Una vez (configuración Git)
git config --global user.name "Rodolfo Alabarca"
git config --global user.email "rodophybusiness08@gmail.com"
git config --global init.defaultBranch main

# Setup proyecto
cd portfolio-rodolfo/
git init
git add .
git commit -m "feat: initial portfolio commit — production-ready"

# Conectar GitHub
git remote add origin https://github.com/RodCode088/portfolio.git
git branch -M main
git push -u origin main

# Conectar Netlify (UI):
# 1. app.netlify.com → Add new site → Import from GitHub → portfolio
# 2. Site name → rodolfo-alabarca
# 3. Forms → verifica que contact aparece
```

Cualquier duda, me la dices ANTES de seguir adelante. Mejor pausar 2 min que romper algo en pleno launch.
