# Lumobral One Suite (PWA)

App de gestión (cotizaciones, pedidos, órdenes de compra, empresas y proveedores)
lista para instalarse como PWA en cualquier celular, tablet o computador.

Todos los datos se guardan en el `localStorage` del navegador del dispositivo:
no hay servidor ni base de datos. Cada dispositivo/navegador tiene su propia copia.

## Archivos del repositorio

```
index.html        → la app completa (HTML + CSS + JS en un solo archivo)
manifest.json      → metadatos de la PWA (nombre, ícono, colores)
sw.js              → service worker (cachea la app para que abra sin internet)
icons/
  icon-192.png
  icon-512.png
  icon-maskable-512.png
  apple-touch-icon.png
README.md          → esta guía
```

---

## Paso 1 — Crear el repositorio en GitHub

1. Entra a [github.com](https://github.com) e inicia sesión (o crea una cuenta).
2. Arriba a la derecha, click en **+** → **New repository**.
3. Nómbralo, por ejemplo `lumobral-suite`.
4. Déjalo en **Public** (necesario para el hosting gratuito de GitHub Pages).
5. No marques "Add a README" (ya tienes uno). Click en **Create repository**.

## Paso 2 — Subir los archivos

**Opción fácil (sin usar terminal):**

1. En la página del repo recién creado, click en **uploading an existing file**.
2. Arrastra estos archivos y carpetas: `index.html`, `manifest.json`, `sw.js`, y la carpeta `icons/` completa (con sus 4 imágenes adentro).
3. Abajo, escribe un mensaje como "Primera versión" y click en **Commit changes**.

**Opción con Git (si ya lo usas):**

```bash
git clone https://github.com/TU-USUARIO/lumobral-suite.git
cd lumobral-suite
# copia aquí adentro: index.html, manifest.json, sw.js, icons/
git add .
git commit -m "Primera versión"
git push
```

## Paso 3 — Activar GitHub Pages (hosting gratuito)

1. En el repositorio, ve a **Settings** (pestaña arriba).
2. En el menú lateral izquierdo, click en **Pages**.
3. En **Source**, selecciona la rama `main` y la carpeta `/ (root)`.
4. Click en **Save**.
5. Espera 1–2 minutos. GitHub te mostrará la URL pública, algo como:
   `https://TU-USUARIO.github.io/lumobral-suite/`

Importante: la PWA solo funciona (instalación + modo offline) si se sirve por
**HTTPS**, que es justo lo que entrega GitHub Pages automáticamente. Abrir el
`index.html` directamente desde el explorador de archivos del computador
("archivo:///...") no permite instalar la app ni activar el service worker.

## Paso 4 — Instalar la app en cada dispositivo

### Android (Chrome / Brave / Edge)
1. Abre la URL de GitHub Pages en el navegador.
2. Aparecerá un banner "Agregar a pantalla de inicio" o toca el menú `⋮` →
   **Instalar app** / **Agregar a pantalla de inicio**.
3. Confirma. Queda un ícono como cualquier app nativa.

### iPhone / iPad (Safari — obligatorio, no funciona desde Chrome en iOS)
1. Abre la URL en **Safari**.
2. Toca el botón compartir (el cuadrado con la flecha hacia arriba).
3. Baja y toca **Agregar a pantalla de inicio**.
4. Confirma el nombre y toca **Agregar**.

### Windows / Mac / Linux (Chrome, Edge, Brave)
1. Abre la URL.
2. En la barra de direcciones aparece un ícono de instalar (⊕ o pantalla con flecha).
3. Click ahí → **Instalar**. Queda como app de escritorio independiente.

Una vez instalada en cualquier plataforma, la app abre en pantalla completa
(sin barra del navegador) y sigue funcionando sin conexión gracias al `sw.js`
(usa la última versión que se cargó con internet).

## Paso 5 — Publicar actualizaciones futuras

1. Edita `index.html` (o los otros archivos) y vuelve a subirlos al repositorio
   (mismo botón "Upload files", o `git push` si usas terminal).
2. **Importante:** abre `sw.js` y sube en 1 el número de versión de esta línea:
   ```js
   const CACHE_NAME = "lumobral-one-suite-v1"; // cambia a v2, v3, etc.
   ```
   Esto obliga a los dispositivos a descargar la nueva versión en vez de
   seguir usando la copia guardada en caché.
3. GitHub Pages actualiza la URL automáticamente en 1–2 minutos.
4. Los usuarios verán la actualización la próxima vez que abran la app con
   internet (puede requerir cerrar y volver a abrir la app una vez).

## Notas sobre los datos

- Cada instalación (cada combinación de navegador + dispositivo) tiene su
  propio `localStorage`; los datos **no se sincronizan** entre dispositivos.
- Si el usuario borra los datos de navegación/caché del navegador, o
  desinstala la app, se pierde la información guardada. Conviene usar el
  botón de exportar/respaldo de la app periódicamente (si el módulo lo tiene)
  o hacer capturas de los reportes importantes.
- Si en el futuro quieres que los datos se compartan entre dispositivos,
  se necesitaría agregar un backend (base de datos en la nube) — este
  paquete actual es 100% local, sin servidor.
