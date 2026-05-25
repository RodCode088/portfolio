# 🔀 Guía rápida — Combinar archivos nuevos con tu carpeta original

> **Lee esto antes de seguir con la guía de Git/Deploy.** Te dice exactamente qué archivos copiar y dónde, para que tu portafolio funcione localmente con todos los cambios.

---

## Paso 1 — Identifica tu carpeta original

Tu carpeta original es esta (la que mencionaste):

```
C:\Users\Usuario1\Documents\PROYECTOS PROFESIONALES\portfolio\
```

Y debe verse así POR DENTRO:

```
portfolio\
├── index.html              ← TU versión vieja (la vamos a reemplazar)
└── index_files\            ← Carpeta auto-generada por Chrome con tus assets
    ├── rodolfo.png
    ├── sommelier-no.png
    ├── dashboard_canapty.png
    └── css2                ← (archivo de fuentes en caché — no lo toques)
```

> ✅ **Importante:** la carpeta `index_files\` y todo su contenido se QUEDA tal cual. El nuevo `index.html` la sigue usando para cargar tus imágenes localmente.

---

## Paso 2 — Copia los archivos nuevos que te entregué

Desde la carpeta de outputs de esta sesión, copia **todos estos archivos** a tu carpeta `portfolio\`:

| Archivo | Qué es |
|---|---|
| `index.html` | El portafolio refactorizado completo (sobreescribe el viejo) |
| `og-image.html` | Plantilla para generar la imagen de Open Graph |
| `README.md` | Para GitHub |
| `.gitignore` | Reglas profesionales de Git (empieza con punto — ¡no lo pierdas!) |
| `_redirects` | Para Netlify SPA (sin extensión) |
| `robots.txt` | SEO para crawlers |
| `sitemap.xml` | Mapa de URLs |
| `netlify.toml` | Cache + security headers |
| `GUIA_DEPLOY.md` | Tu guía paso a paso para Git/Netlify (no es pública, opcional) |
| `MERGE_GUIDE.md` | Este archivo (opcional) |

> ⚠️ **`.gitignore` no se ve en Windows Explorer por defecto** (los archivos que empiezan con punto). En el Explorador: pestaña **Vista** → marca **Elementos ocultos**. Luego sí lo ves para copiar/pegar.

---

## Paso 3 — Resultado: tu carpeta debe verse así

```
portfolio\
├── index.html                  ← NUEVO (reemplazado)
├── og-image.html               ← NUEVO
├── README.md                   ← NUEVO
├── .gitignore                  ← NUEVO
├── _redirects                  ← NUEVO
├── robots.txt                  ← NUEVO
├── sitemap.xml                 ← NUEVO
├── netlify.toml                ← NUEVO
├── GUIA_DEPLOY.md              ← NUEVO (opcional)
├── MERGE_GUIDE.md              ← NUEVO (opcional)
└── index_files\                ← SE QUEDA tal cual
    ├── rodolfo.png
    ├── sommelier-no.png
    ├── dashboard_canapty.png
    └── css2
```

---

## Paso 4 — Probar localmente

Doble click en `index.html`. **Lista de verificación:**

- [ ] Tu foto aparece en el hero.
- [ ] El tab del navegador muestra una "R" naranja (favicon).
- [ ] Detrás de todo, partículas sutiles que emergen del centro.
- [ ] Sección de Stack debajo del hero con 4 categorías.
- [ ] En Work → Sommelier preview carga + Dashboard screenshot carga.
- [ ] NO se ve "Plataforma Foodie".
- [ ] Click en logo: hace scroll-to-top en la home (ya no es link roto).

Si todo eso funciona: ✅ merge completo.

Si algo no carga: el problema casi siempre es nombres de archivo (mayúsculas/extensión). Verifica que dentro de `index_files\` los archivos se llamen EXACTAMENTE:
- `rodolfo.png` (no `Rodolfo.png` ni `rodolfo.PNG`)
- `sommelier-no.png`
- `dashboard_canapty.png`

---

## Paso 5 — Activar el formulario de contacto (CRÍTICO, 60 segundos)

El formulario está configurado para usar **Web3Forms** — un servicio gratuito que envía los mensajes directos a tu email sin necesidad de backend. Para activarlo:

### 5.1 Obtener tu access key

1. Abre **[https://web3forms.com](https://web3forms.com)** en tu navegador.
2. En el campo "Email" pones: `rodophybusiness08@gmail.com`
3. Click **"Create Access Key"** (o similar — botón principal en la home).
4. Recibirás un email con tu **Access Key** (un código alfanumérico tipo `1a2b3c4d-5e6f-7g8h-9i0j-klmnopqrstuv`).

### 5.2 Pegar la access key en el index.html

1. Abre `index.html` con un editor (Notepad, VS Code, lo que tengas — **NO Word**).
2. Buscar (Ctrl+F): `YOUR_ACCESS_KEY_HERE`
3. **Reemplaza** ese texto por tu access key real. Queda así:

   **Antes:**
   ```html
   <input type="hidden" name="access_key" value="YOUR_ACCESS_KEY_HERE">
   ```

   **Después:**
   ```html
   <input type="hidden" name="access_key" value="1a2b3c4d-5e6f-7g8h-9i0j-klmnopqrstuv">
   ```

4. Guarda el archivo.

### 5.3 Probar el formulario

1. Abre `index.html` en el navegador.
2. Ve a Contact.
3. Llena el formulario con datos de prueba y envíalo.
4. Revisa tu inbox `rodophybusiness08@gmail.com` — debería llegar el mensaje en menos de 1 minuto.

> **Nota:** la primera vez puede llegar a la carpeta de Spam/Promociones. Marca como "No es spam" y los próximos llegarán bien al inbox.

> **Si NO has puesto tu access key:** el formulario detecta el placeholder y abre tu cliente de email con el mensaje prerellenado (fallback `mailto`). Funcional pero menos elegante. Por eso vale la pena los 60 segundos del setup.

---

## Paso 6 — ¿Y ahora qué?

Tienes dos caminos según tu prisa:

### Camino A — Lanzar HOY (recomendado)

Sigue la guía `GUIA_DEPLOY.md` que te entregué:

1. Setup de Git.
2. Crear repo en GitHub.
3. Conectar Netlify.
4. Sale online.

### Camino B — Probar más antes de lanzar

Si quieres seguir iterando localmente:

1. Verifica que el form funcione (Paso 5 de arriba).
2. Genera la `og-image.png` (instrucciones en el archivo `og-image.html`).
3. Cuando estés satisfecho, vamos al deploy.

---

## ❓ Errores comunes en el merge

**"Mi foto sigue sin cargar después del merge"**
→ La imagen no está donde el HTML la busca. Verifica que `index_files\rodolfo.png` exista. Distingue mayúsculas.

**"Veo el HTML pero sin estilos"**
→ Probablemente abriste el archivo desde un email/zip raro. Asegúrate de que el HTML está dentro de tu carpeta `portfolio\` junto a `index_files\`.

**"El formulario se queda cargando para siempre"**
→ Tu access key no es correcta, o falta replacement de `YOUR_ACCESS_KEY_HERE`. Verifica copia exacta sin espacios extras.

**"El email no llega"**
→ Revisa Spam/Promociones. Si después de 5 min no llega, verifica que el email de registro en web3forms.com sea el mismo donde quieres recibir los mensajes.

---

Cualquier pregunta, vuelvo aquí y la respondo. **No hagas Paso 6 (deploy) hasta que el Paso 4 y 5 pasen localmente.**
