# Gestor de Incidencias SKY · Calidad Directo

Herramienta web para gestionar las evaluaciones con estrellas de los pasajeros de SKY que se descargan de Llegando: importar la descarga diaria, clasificar incidencias, notificar a las áreas, registrar planes de acción y estados, generar el reporte al cliente, exportar al formato de la BD de Incidencias de Calidad y ver el dashboard de reincidencias.

Los datos se guardan en **Firebase (Firestore)**, así que todas las personas autorizadas ven y gestionan la misma información, día a día. Para entrar se usa una cuenta de Google que esté en la lista autorizada.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La herramienta completa |
| `firebase-config.js` | Conexión con tu proyecto Firebase (se completa una sola vez) |
| `firestore.rules` | Lista de correos con acceso a los datos |

## Puesta en marcha (una sola vez)

1. **Crear el proyecto Firebase**: entra a <https://console.firebase.google.com>, *Agregar proyecto* (por ejemplo `incidencias-sky`). Google Analytics no es necesario.
2. **Base de datos**: menú *Firestore Database* → *Crear base de datos* → modo producción → ubicación `southamerica-east1` (São Paulo) o la que prefieras.
3. **Reglas de acceso**: en Firestore → pestaña *Reglas*, pega el contenido de `firestore.rules`, reemplaza los correos de ejemplo por los de las personas que gestionan (por ejemplo Melisa y Jorge) y pulsa *Publicar*.
4. **Inicio de sesión**: menú *Authentication* → *Comenzar* → *Método de acceso* → habilita **Google**. En *Configuración → Dominios autorizados* agrega el dominio de GitHub Pages (por ejemplo `directo-central.github.io`).
5. **Conectar la página**: *Configuración del proyecto* (engranaje) → *Tus apps* → icono web `</>` → registra la app → copia el bloque `firebaseConfig` y pega sus valores en `firebase-config.js`.
6. **Publicar en GitHub Pages**: sube los tres archivos al repositorio → *Settings → Pages* → *Deploy from a branch* → rama `main`, carpeta `/ (root)`. En uno o dos minutos queda en `https://<cuenta>.github.io/<repositorio>/`.

## Pasar los datos que ya están en el gestor de Claude

1. En el gestor de Claude: pestaña **Configuración → Exportar respaldo (JSON)**.
2. En la página de GitHub (ya con sesión iniciada): **Configuración → Restaurar respaldo** y elige ese archivo.

Se cargan las evaluaciones, la gestión de cada caso (planes, estados, fechas), la flota y la configuración de áreas y correos.

## Uso diario

1. **Importar descarga**: sube el archivo `Tabla_feedback_OMW` de Llegando. Las evaluaciones repetidas se ignoran.
2. **Importar flota**: cuando tengas un Reporte de Conductores nuevo.
3. Gestiona en **Casos**, envía en **Correos**, arma el **Reporte cliente**, descarga la **BBDD** y revisa el **Dashboard**.

## Diferencias con la versión de Claude

- El botón **"Generar 'Caso' con IA"** no aparece: el resumen del caso se escribe a mano en el formulario.
- Agregar o quitar personas se hace en las reglas de Firestore (paso 3).

## Seguridad

La página es pública, pero los datos no: sin una cuenta autorizada solo se ve la pantalla de ingreso. Los datos contienen DNI de pasajeros; mantén la lista de correos solo con quienes gestionan las incidencias. Si haces el repositorio privado, GitHub Pages necesita un plan pago de GitHub; con repositorio público el código es visible pero los datos siguen protegidos por Firebase.
