# Walkthrough: Panel Interactivo de Preparación Física de Sofía

He desarrollado e integrado un panel de control interactivo premium en el archivo [00-dashboard_preparacion_sofia.html](file:///G:/Mi%20unidad/01%20-%20Preparacion%20Sofia/00-dashboard_preparacion_sofia.html) para la planificación física, control de peso y pasos diarios de Sofía.

---

## 📂 Archivos Creados y Ubicación

Todos los archivos han sido generados en tu Google Drive en la siguiente ruta:
📂 **`G:\Mi unidad\01 - Preparacion Sofia\`**

Y una copia de respaldo para control de versiones en el espacio de trabajo local:
📂 **`d:\Nico\ProyectosAntigravity\PreparacionFisicaSofia\`**

### Lista de Archivos:
1.  **[00-dashboard_preparacion_sofia.html](file:///G:/Mi%20unidad/01%20-%20Preparacion%20Sofia/00-dashboard_preparacion_sofia.html)**: El panel de control interactivo responsivo (HTML, CSS y JS autocontenido).
2.  **[registro_peso_semanal.csv](file:///G:/Mi%20unidad/01%20-%20Preparacion%20Sofia/registro_peso_semanal.csv)**: Archivo físico para sincronizar los pesajes semanales.
3.  **[registro_fuerza_gimnasio.csv](file:///G:/Mi%20unidad/01%20-%20Preparacion%20Sofia/registro_fuerza_gimnasio.csv)**: Archivo físico para registrar cada serie completada del gimnasio.
4.  **[registro_pasos_semanal.csv](file:///G:/Mi%20unidad/01%20-%20Preparacion%20Sofia/registro_pasos_semanal.csv)**: Archivo físico para registrar el recuento de pasos diarios.

---

## 🧭 Guía de Sincronización en Tiempo Real (PC)

Para asegurar que ningún dato se pierda y se guarden directamente en los archivos `.csv` en tu Google Drive:

1.  Abre **[00-dashboard_preparacion_sofia.html](file:///G:/Mi%20unidad/01%20-%20Preparacion%20Sofia/00-dashboard_preparacion_sofia.html)** en Google Chrome o Microsoft Edge en tu ordenador.
2.  Ve a la pestaña **🔗 Datos**.
3.  En la sección "Sincronización Local con Google Drive", haz clic en **Vincular Archivo** para cada uno de los tres archivos.
4.  Selecciona el archivo `.csv` correspondiente dentro de la carpeta `G:\Mi unidad\01 - Preparacion Sofia\`.
5.  El navegador te pedirá confirmación de permisos de escritura. Acéptala.
6.  Una vez vinculado, verás el estado en verde como **Vinculado**. Los handles de los archivos se guardarán de manera persistente en la IndexedDB de tu navegador, por lo que **no tendrás que volver a vincularlos** al recargar o abrir el panel en el futuro (solo te pedirá confirmación de acceso al iniciar la sesión).

*Nota: Si usas el dashboard en el móvil (donde no está disponible la File System Access API de Chrome/Edge), tus datos se guardarán localmente en el almacenamiento del navegador (LocalStorage). Puedes exportarlos de forma manual usando los botones de descarga en la pestaña Datos.*

---

## 🏋️ Explicación de las Pestañas del Dashboard

### 1. 📅 Calendario
*   Muestra los 7 días de la semana seleccionada, marcando claramente qué días toca ir al gimnasio (Fuerza) y cuáles son de descanso activo.
*   Muestra el total de pasos diarios de cada día directamente debajo del estado para tener una vista integrada de tu actividad (NEAT).
*   **Selector de Días de Gimnasio (Configuración):** En la parte inferior, puedes reajustar los dos días de la semana asignados a fuerza (por defecto Martes y Jueves). Al cambiarlos, el calendario de esa semana y los botones de entrenamiento de gimnasio se reprogramarán de forma instantánea.

### 2. 🏋️ Rutina Gym
Carga automáticamente la rutina que corresponde según la semana que tengas seleccionada en el navegador global superior (planificado hasta finales de septiembre, cubriendo todo el verano):
*   **Foco en Fuerza Controlada e Integridad Articular:** Diseñado específicamente para ganar fuerza de base y masa muscular útil de forma segura (evitando saltos o aceleraciones bruscas).
*   **Tempos y Paradas Isométricas [NUEVO]:** Se han reajustado los tempos de los ejercicios para eliminar cualquier inercia o impulso (explosividad):
    *   La fase concéntrica (empuje/tirón) se realiza a un tempo controlado de **2 segundos** (en lugar de subir rápido/explosivo).
    *   Se añaden **paradas de 1 segundo** en puntos clave (ej. abajo en la Sentadilla Goblet, en la contracción del Remo o en el máximo estiramiento del Peso Muerto Rumano) para ganar fuerza isométrica estática y proteger las articulaciones.
*   **Bloques de Calentamiento:** Se incorporan bloques de Movilidad (Gato-Camello o Movilidad 90/90) y de Activación (Puente de Glúteos normal o a una pierna) antes de los ejercicios principales para activar la musculatura estabilizadora de forma controlada.
*   **Mes 1 (Semanas 1 a 4):** Adaptación en máquinas (Prensa inclinada, Press de pecho, Remo sentado y Curl femoral) más plancha. Series a RIR 3.
*   **Mes 2 (Semanas 5 a 8):** Mayor intensidad a RIR 1. Remo a una mano unilateral para estabilidad.
*   **Mes 3 (Semanas 9 a 12):** Transición a peso libre con mancuernas (press inclinado, remo en banco, peso muerto rumano) y paseo de maleta. RIR 1.
*   **Mes 4 (Semanas 13 a 16):** Consolidación con Sentadilla Goblet con mancuerna y press plano con mancuernas. RIR 1.

**🎁 Pantalla de Bienvenida y Regalo Personalizado [NUEVO]:**
*   La primera vez que Sofía abra el dashboard en su navegador, aparecerá de forma automática una ventana emergente de bienvenida con una **foto personalizada** de Sofía y Nico ([foto_sofia.jpg](file:///G:/Mi%20unidad/01%20-%20Preparacion%20Sofia/foto_sofia.jpg)) y el mensaje: **"Es un regalo para ayudarte a cumplir el objetivo. 💖"**.
*   Una vez que cierre la ventana emergente, esta no volverá a mostrarse en ese navegador (se almacena la preferencia en `localStorage`).
*   Además, se mantiene visible de forma permanente el banner premium superior con gradiente animado y el mensaje: **"🎁 ¡Es un regalo para ayudarte a cumplir el objetivo! 💖"**.

**Funcionamiento del registro:**
*   Aparecen dos botones selector de día (`Día 1` y `Día 2`) sincronizados con las fechas de la semana.
*   Para cada ejercicio, se muestran 3 filas de registro de series.
*   Introduce la carga en **Carga (kg)**, las repeticiones en **Reps** (puedes ajustarlas libremente ya que el plan indica el objetivo de RIR pero no repeticiones fijas) e indica el **RIR Real** que has sentido.
*   Haz clic en el botón de verificación **✓** para clavar la serie. Verás cómo cambia a verde y se guarda/sincroniza en el acto.
*   Al clavar todas las series de la sesión, se mostrará un banner verde de **"¡Sesión Completada!"** en la cabecera del entrenamiento.

### 3. ⚖️ Peso
*   Registra tu peso corporal en kilogramos y añade notas descriptivas del día (ej. en ayunas, retención, etc.).
*   El panel dibuja dinámicamente un gráfico lineal histórico de tu evolución en un `<canvas>` nativo, con una línea verde horizontal que marca tu **Peso Objetivo** (por defecto 75.0 kg, editable en la pestaña Datos).
*   Visualiza una tabla histórica con la fecha de pesaje y la variación de peso respecto a la semana anterior (en verde si es pérdida, rojo si es ganancia).

### 4. 👟 Pasos
*   Formulario simplificado para registrar los pasos diarios de cada día de la semana seleccionada (Lunes a Domingo) con notas explicativas opcionales.
*   Gráfico de barras semanal en `<canvas>` con colores dinámicos: verde si alcanzas el objetivo diario (ej. 8,000 pasos), naranja si estás cerca (>= 70%) y rojo si te quedas por debajo.
*   Métricas clave de la semana: Pasos totales, Promedio diario, porcentaje de cumplimiento de meta y estimación de calorías activas quemadas.
*   Permite ajustar la meta diaria de pasos directamente en la pestaña (por defecto 8,000 pasos).

### 5. 🔗 Datos
*   Vincular o desvincular los tres archivos CSV locales.
*   Exportar manualmente los datos a CSV.
*   Hacer copias de seguridad de toda la base de datos local en formato de texto JSON para poder copiarla al portapapeles o restaurarla en cualquier dispositivo (ideal para sincronizar móvil y ordenador).
*   Ajustes rápidos de peso objetivo y reinicio de fábrica de la base de datos.
