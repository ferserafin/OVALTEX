# Control de Órdenes · Ovaltex (Netlify)

Aplicación web con formulario, base de datos, dashboard con semáforo y exportación a CSV.

## Estructura
- `public/index.html` → toda la aplicación (formulario, dashboard, tabla, CSV)
- `netlify/functions/api.mjs` → API que guarda los datos en la base de Netlify (Netlify Blobs)
- `netlify/functions/seed.mjs` → datos iniciales tomados de CONTROL_DE_ORDENES.xlsx (96 líneas)
- `netlify/functions/productos.mjs` → catálogo de claves/productos (hoja PRODUCTOS) para autocompletar
- `netlify.toml`, `package.json` → configuración

## IMPORTANTE: no uses "arrastrar y soltar"
Netlify Drop (arrastrar carpeta) NO ejecuta funciones, así que no habría base de datos.
Usa una de estas dos opciones:

### Opción A · GitHub (sin terminal)
1. Crea un repositorio en GitHub y sube TODO el contenido de esta carpeta.
2. En Netlify: Add new project → Import an existing project → elige el repositorio.
   (Netlify toma la configuración de netlify.toml; no cambies nada.)
3. Antes o justo después del primer deploy: Project configuration → Environment variables →
   agrega `APP_PASSWORD` con la contraseña que quieras.
4. Vuelve a desplegar (Deploys → Trigger deploy) para que tome la variable.

### Opción B · Netlify CLI
```
npm install
npm install -g netlify-cli
netlify login
netlify init            # o: netlify link
netlify env:set APP_PASSWORD "tu-contraseña"
netlify deploy --prod
```

## Primer uso
1. Abre el sitio, escribe la contraseña.
2. Si la base está vacía aparece un aviso: pulsa "Cargar datos de CONTROL_DE_ORDENES.xlsx".
3. Listo: captura en la pestaña Captura, consulta el semáforo en Dashboard, exporta en Exportar / Datos.

## Notas
- Si no existe `APP_PASSWORD`, la API se niega a responder (para no dejar tus datos públicos).
- Los datos viven en Netlify Blobs: persisten entre despliegues.
- El criterio del semáforo (fecha de referencia y días de aviso) se ajusta al final del Dashboard.

## Importar desde Excel (nuevo)
En la pestaña "Exportar / Importar" sube tu Excel o CSV. Modos: solo agregar nuevas, agregar y actualizar existentes, o reemplazar todo.
Para actualizar la app ya desplegada reemplaza en GitHub estos dos archivos (Netlify redespliega solo):
`public/index.html` y `netlify/functions/api.mjs`.
