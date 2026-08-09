# Lumo360 (PWA)

App de gestión de Lumobral — cotizaciones, pedidos, órdenes de compra,
empresas y proveedores — lista para instalarse como PWA en cualquier
celular, tablet o computador.

Todos los datos se guardan en el dispositivo (IndexedDB, con respaldo en
`localStorage`), y opcionalmente se pueden sincronizar entre dispositivos
conectando un espacio de trabajo en la nube desde Configuración.

## Archivos del repositorio

Todos los archivos van sueltos en la raíz del repo (sin subcarpetas):

```
index.html              → la app completa (HTML + CSS + JS en un solo archivo)
manifest.json           → metadatos de la PWA (nombre, ícono, colores)
sw.js                   → service worker (cachea la app para que abra sin internet)
icon-192.png
icon-512.png
icon-maskable-512.png
apple-touch-icon.png
README.md               → esta guía
```

---

## Paso 1 — Crear el repositorio en GitHub

1. Entra a [github.com](https://github.com) e inicia sesión (o crea una cuenta).
2. Arriba a la derecha, click en **+** → **New repository**.
3. Nómbralo, por ejemplo `LumOne`.
4. Déjalo en **Public** (necesario para el hosting gratuito de GitHub Pages).
5. No marques "Add a README" (ya tienes uno). Click en **Create repository**.

## Paso 2 — Subir los archivos

En la página del repo, click en **uploading an existing file** y arrastra
los 7 archivos (`index.html`, `manifest.json`, `sw.js` y los 4 `.png`) —
todos juntos, sueltos en la raíz, no dentro de una carpeta.
Escribe un mensaje de commit y click en **Commit changes**.

## Paso 3 — Activar GitHub Pages (hosting gratuito)

1. En el repositorio, ve a **Settings** → **Pages**.
2. En **Source**, selecciona la rama `main` y la carpeta `/ (root)`. Guarda.
3. Espera 1–2 minutos. La URL pública queda como:
   `https://TU-USUARIO.github.io/TU-REPO/`

La PWA solo funciona (instalación + modo offline) servida por **HTTPS**,
que es justo lo que entrega GitHub Pages automáticamente.

## Paso 4 — Instalar la app en cada dispositivo

### Android (Chrome)
Abre la URL en Chrome → menú `⋮` → **Instalar app**.
*(Opera y Firefox de escritorio no soportan instalar PWAs — en celular,
Opera Android sí funciona igual que Chrome.)*

### iPhone / iPad (Safari — obligatorio, no funciona desde Chrome en iOS)
Abre la URL en Safari → botón compartir → **Agregar a pantalla de inicio**.

### Windows / Mac / Linux (Chrome, Edge o Brave — no Opera ni Firefox)
Abre la URL → ícono de instalar en la barra de direcciones (⊕) → **Instalar**.

Una vez instalada, la app abre en pantalla completa y sigue funcionando
sin conexión gracias al `sw.js` (usa la última versión cargada con internet).

## Paso 5 — Publicar actualizaciones futuras

1. Sube los archivos modificados (mismo botón "Upload files").
2. **Importante:** abre `sw.js` y sube en 1 el número de versión de esta línea:
   ```js
   const CACHE_NAME = "lumobral-one-suite-v8"; // sube el número en cada publicación
   ```
   Esto obliga a los dispositivos a descargar la nueva versión en vez de
   seguir usando la copia guardada en caché.
3. En Android, si cambiaste el ícono o el nombre de la app, puede no
   alcanzar con solo actualizar los archivos: **desinstala la app del
   celular, limpia caché de Chrome (Configuración → Privacidad → Borrar
   datos de navegación → Imágenes y archivos en caché), y vuelve a
   instalarla**. Android empaqueta la PWA como WebAPK y a veces no refresca
   el ícono/nombre solo.

## Notas sobre los datos

- Si usas sincronización en la nube (Configuración), los datos se
  comparten entre dispositivos conectados al mismo espacio de trabajo;
  si no la activas, cada instalación guarda su copia local únicamente.
- Usa el botón de exportar/respaldo de la app periódicamente para no
  depender solo de la caché del navegador.
