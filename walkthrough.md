# Walkthrough: Dashboard de Preparación Física de Sofía (Fase 2)

He actualizado el panel de control interactivo unificado para la preparación física de Sofía ([00-dashboard_preparacion_sofia.html](file:///d:/Nico/ProyectosAntigravity/PreparacionFisicaSofia/00-dashboard_preparacion_sofia.html)). En esta versión v2.0.0, el dashboard incorpora toda la arquitectura de seguridad, cifrado en la nube y configuración dinámica basada en el proyecto de Nico (Goalkeeper), pero manteniendo la planificación física intacta de Sofía.

---

## 🔒 Nuevas Características de Seguridad y Privacidad

### 1. Pantalla de Bloqueo y Configuración Inicial
- **Primera Visita**: El panel se inicia en una pantalla de bloqueo completa que detiene la carga del dashboard y solicita al usuario configurar su perfil y contraseña de acceso:
  - **Datos del Perfil**: Nombre de la atleta (ej. Sofía), Edad, Altura, Peso Inicial (se registra como el primer pesaje base en el historial) y Peso Objetivo (Meta).
  - **Contraseña**: Se establece una contraseña de acceso (mínimo 4 caracteres).
- **Accesos Posteriores**: Solicita la contraseña para desbloquear el panel. Permite marcar la opción "Recordarme en este dispositivo" para guardar la clave temporalmente (mediante `localStorage` / `sessionStorage`) y agilizar el acceso diario.

### 2. Cifrado Simétrico en la Nube (AES-GCM)
- Los datos de peso, marcas y pasos ya no se suben en texto claro a GitHub.
- Antes de realizar cualquier push a la nube, los datos se convierten en JSON y se cifran utilizando el algoritmo simétrico **AES-GCM de 256 bits** provisto de forma nativa por el navegador a través de la API `crypto.subtle`.
- La contraseña de acceso creada en el primer ingreso actúa como la clave de cifrado y descifrado.
- En GitHub, la base de datos se guarda en el archivo `goalkeeper_phys_prep_db.json` con formato cifrado seguro (propiedades `encrypted: true`, `iv` y `data` codificados en Base64). Nadie que acceda al repositorio en GitHub podrá leer las marcas, notas o peso de Sofía.

### 3. Sincronización en la Nube (GitHub Sync)
- **Sanitización de Tokens**: El token de GitHub (PAT) introducido se limpia automáticamente de caracteres invisibles para evitar errores silenciosos de autenticación.
- **Fusión Segura de Datos (Merge)**: Se implementó un algoritmo de fusión automática que mezcla cronológicamente los históricos de pesajes, pasos diarios y logs de fuerza locales y remotos para evitar la pérdida de datos al cambiar entre ordenador y móvil.
- **Auto-Resolución de Conflictos (409)**: En caso de que se realicen registros en varios dispositivos simultáneamente y ocurra un conflicto de Git (código 409), el panel descarga automáticamente el estado de la nube, realiza la fusión segura de arrays localmente y empuja el commit resuelto de manera transparente.

---

## 🚀 Despliegue en GitHub Pages

El código ya se encuentra inicializado en un repositorio Git local en su carpeta y se ha subido con éxito a la rama `main` de su cuenta de GitHub en:
🔗 **[nicomrtnz97/PreparacionSofia](https://github.com/nicomrtnz97/PreparacionSofia)**

### Pasos para Activar la Web en tu Móvil u Ordenador (GitHub Pages):
Para disponer de la aplicación online en cualquier navegador a través de una URL de confianza:
1. Entra a tu cuenta en GitHub e ingresa al repositorio **PreparacionSofia**.
2. Ve a la pestaña **Settings** (Configuración) en la barra superior del repositorio.
3. En el menú lateral izquierdo, haz clic en **Pages** (Páginas).
4. En la sección **Build and deployment**:
   - En **Source**, selecciona **Deploy from a branch** (Desplegar desde una rama).
   - En **Branch**, selecciona la rama **main** y en la carpeta elige el directorio raíz **`/ (root)`**.
   - Haz clic en **Save** (Guardar).
5. Espera 1 minuto. GitHub construirá la web y te mostrará la URL pública de la aplicación arriba en esa misma página (ej. `https://nicomrtnz97.github.io/PreparacionSofia/00-dashboard_preparacion_sofia.html`).
6. **¡Listo!** Puedes entrar desde tu iPhone, Android u ordenador a esa URL, ingresar tu contraseña para descifrar la base de datos y tener tus datos sincronizados en tiempo real.

---

## 🧭 Guía de Sincronización de Archivos Locales en PC (Drive)

El panel mantiene la sincronización de archivos CSV físicos en Google Drive si se abre de forma local en ordenador:
1. Abre la web.
2. Ve a la pestaña **Datos** en el menú de navegación.
3. Haz clic en **Vincular Archivo** para vincular `registro_peso_semanal.csv`, `registro_fuerza_gimnasio.csv` y `registro_pasos_semanal.csv` de la carpeta `G:\Mi unidad\01 - Preparacion Sofia\`.
4. Concede permisos de escritura cuando el navegador lo solicite.
