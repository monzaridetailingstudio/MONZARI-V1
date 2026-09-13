# Monzari Detail

Web responsive para Monzari Detail Studio: catálogo, solicitud de turnos, Monzari Club y panel privado de administración. Está preparada para publicarse como web y convertirse en APK con Capacitor.

## Probar localmente

No requiere instalación de dependencias. Desde la raíz del proyecto ejecutá:

```bash
python3 -m http.server 8080
```

Abrí [http://localhost:8080](http://localhost:8080). No abras `index.html` directamente: el servidor permite registrar el modo instalable de la web.

### Credenciales demo

| Acceso | Email | Contraseña |
| --- | --- | --- |
| Administración oculta | `admin@monzari.com` | `monzari` |
| Monzari Club | `cliente@monzari.com` | `monzari` |

El acceso de administración está en el texto `© 2025 MONZARI` del pie de página. Las reservas y clientes creados durante la demo se guardan en el `localStorage` del navegador; para borrar datos de prueba, eliminá los datos del sitio desde las herramientas del navegador.

## Activar funcionalidad real (producción)

La interfaz está lista, pero para una operación real se deben sustituir las funciones de `localStorage` en `app.js` por un backend seguro. Recomendación: **Supabase**.

1. Creá un proyecto en Supabase y tablas `reservas`, `clientes` y `documentos`.
2. Configurá [Supabase Auth](https://supabase.com/docs/guides/auth) con Google y email/contraseña. Nunca guardes contraseñas en el navegador como hace la demo.
3. Guardá los PDFs en Supabase Storage, con reglas para que cada cliente vea únicamente sus propios documentos.
4. Reemplazá `reservations()`, `saveReservations()`, `customers()` y `saveCustomers()` de `app.js` por consultas al SDK de Supabase. Protegé el panel admin usando roles o una tabla de usuarios autorizados.
5. Publicá los archivos en Vercel, Netlify o cualquier hosting HTTPS. Cambiá el enlace de Instagram y las imágenes por los activos oficiales.

## Crear APK Android

Capacitor empaqueta esta misma web como una app nativa, conservando web y APK en un único proyecto.

```bash
npm create @capacitor/app@latest
# Elegí un nombre y package id, por ejemplo com.monzari.detail
cd <carpeta-creada>
npm install @capacitor/android
npx cap add android
```

Después, copiá `index.html`, `styles.css`, `app.js`, `manifest.webmanifest` y `sw.js` a la carpeta web (`www`) creada por Capacitor; configurá `webDir: 'www'` en `capacitor.config.ts`; luego ejecutá:

```bash
npx cap sync android
npx cap open android
```

Android Studio abrirá el proyecto: seleccioná **Build > Generate Signed Bundle / APK > APK** para generar el archivo instalable. Antes de publicar, conectá el backend de producción, cambiá las credenciales demo y agregá iconos/splash oficiales de Monzari.
