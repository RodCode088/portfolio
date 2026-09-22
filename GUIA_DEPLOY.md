# 🚀 Guía Git + GitHub + Cloudflare Pages

Esta es la guía de publicación del portafolio. El sitio es estático: no necesita instalar dependencias ni ejecutar un build.

## Flujo de trabajo

Git mueve los cambios por estas etapas:

```text
Archivos → git add → staging → git commit → historial local → git push → GitHub
```

Cloudflare Pages está conectado a GitHub. Cada push a `main` crea automáticamente un nuevo despliegue de producción.

## Publicar cambios

Desde la raíz del proyecto:

```bash
git status
git add .
git commit -m "feat: describir el cambio"
git push origin main
```

Después del push, revisa el despliegue en Cloudflare Dashboard → Workers & Pages → tu proyecto → Deployments.

## Configuración inicial de Cloudflare Pages

Esto solo se hace una vez:

1. En Cloudflare Dashboard, abre **Workers & Pages** y crea un proyecto de Pages conectado a Git.
2. Autoriza GitHub y selecciona el repositorio `RodCode088/portfolio`.
3. Usa `main` como rama de producción.
4. Selecciona un proyecto sin framework.
5. Deja el comando de build vacío.
6. Usa `.` como directorio de salida.
7. Guarda y ejecuta el primer despliegue.

Configuración esperada:

| Campo | Valor |
|---|---|
| Repositorio | `RodCode088/portfolio` |
| Rama de producción | `main` |
| Framework preset | None |
| Build command | Vacío |
| Build output directory | `.` |

## Dominio

El dominio canónico del portafolio es [rodolfoalabarca.dev](https://rodolfoalabarca.dev/).

Para conectarlo o revisarlo: proyecto de Pages → Custom domains. Cloudflare configura el certificado HTTPS y muestra el estado del dominio desde esa sección.

## Archivos de infraestructura

- `_redirects`: entrega `index.html` como fallback para rutas del sitio.
- `_headers`: define caché y cabeceras de seguridad para los recursos estáticos.
- `robots.txt` y `sitemap.xml`: configuración de rastreo e indexación.

Estos archivos deben permanecer en la raíz porque esa misma carpeta es el directorio publicado.

## Formulario de contacto

El formulario usa Web3Forms, no el proveedor de hosting. Su `access_key` está configurada en `index.html`; cambiar de plataforma de despliegue no altera el envío del formulario.

## Reintentar un despliegue

Si un despliegue falla:

1. Abre Cloudflare Dashboard → Workers & Pages → proyecto → Deployments.
2. Abre el despliegue fallido y revisa el log.
3. Corrige el problema y vuelve a hacer push, o usa **Retry deployment** si fue un fallo temporal.

## Verificaciones rápidas

Antes de publicar:

```bash
git status
python3 -m http.server 8000
```

Abre `http://localhost:8000` y comprueba navegación, imágenes, videos, enlaces y formulario. Detén el servidor con `Ctrl+C`.

Después del deploy, confirma:

- que `https://rodolfoalabarca.dev/` carga correctamente;
- que las secciones y rutas funcionan;
- que el formulario envía;
- que las imágenes y videos no devuelven 404.
