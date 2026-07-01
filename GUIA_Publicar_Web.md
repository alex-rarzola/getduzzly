# Publicar la landing de Duzzly en GitHub Pages + dominio (Cloudflare)

## Parte A — Subir el sitio a GitHub Pages

1. **Crea una cuenta** en [github.com](https://github.com) (si no tienes) e inicia sesión.
2. **Crea un repositorio nuevo:** botón **+** (arriba a la derecha) → **New repository**.
   - Name: `duzzly-landing` (o el que quieras)
   - Visibility: **Public**
   - No marques "Add README". Clic en **Create repository**.
3. **Sube los archivos:** en la página del repo → **Add file ▸ Upload files**.
   - Arrastra: `index.html`, `privacy.html`, `terms.html` (y tus capturas: `home.png`, `analytics.png`, `scan.png`, y `icon.png` si quieres).
   - Abajo, clic en **Commit changes**.
4. **Activa GitHub Pages:** en el repo → **Settings** (pestaña superior) → menú lateral **Pages**.
   - En **Source** elige **Deploy from a branch**.
   - En **Branch** elige **main** y carpeta **/(root)** → **Save**.
5. Espera ~1 minuto. Arriba aparecerá la URL: `https://TU-USUARIO.github.io/duzzly-landing/`.
   Ábrela para confirmar que se ve bien. ✅

> Los enlaces del sitio son relativos (`privacy.html`, `terms.html`), así que funcionan aunque esté en subcarpeta.

## Parte B — Conectar tu dominio de Cloudflare (ej. getduzzly.com)

Una vez que tengas el dominio en Cloudflare:

1. **En GitHub** → repo → **Settings ▸ Pages ▸ Custom domain**: escribe `getduzzly.com` → **Save**.
   (Esto crea un archivo `CNAME` en tu repo automáticamente.)
2. **En Cloudflare** → tu dominio → **DNS ▸ Records ▸ Add record**. Agrega:

   **Para el dominio raíz (getduzzly.com) — 4 registros A:**
   | Type | Name | Content |
   |------|------|---------|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |

   **Para www:**
   | Type | Name | Content |
   |------|------|---------|
   | CNAME | www | TU-USUARIO.github.io |

3. **Importante:** en cada registro pon la **nube en GRIS ("DNS only")**, no naranja, al inicio. Así GitHub puede emitir su certificado HTTPS.
4. Vuelve a **GitHub ▸ Settings ▸ Pages**, espera a que valide el dominio (unos minutos) y marca **✅ Enforce HTTPS**.
5. Prueba `https://getduzzly.com` y `https://www.getduzzly.com`. 🎉

> Cuando ya funcione con HTTPS, si quieres el proxy/CDN de Cloudflare puedes poner la nube naranja y en **SSL/TLS** elegir modo **Full**. Pero para empezar, "DNS only" es lo más simple y estable.

## Recordatorios

- La **URL de privacidad** para App Store Connect será: `https://getduzzly.com/privacy.html`
- Para actualizar el sitio en el futuro: sube los archivos nuevos al repo (Add file ▸ Upload) y se publica solo.
- Agrega tus capturas reales (`home.png`, `analytics.png`, `scan.png`) para que la galería se vea con imágenes.
