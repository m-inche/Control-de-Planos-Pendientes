# 📊 Dashboard - Control de Planos Pendientes

Un dashboard web interactivo de una sola página (SPA) diseñado para el monitoreo dinámico de aprobaciones de planos, lectura de datos desde Google Sheets o Excel, y generación de reportes ejecutivos en imágenes de alta resolución (PNG).

## 🚀 Características Principales

*   **Carga Dinámica de Datos:** Sincronización automática desde Google Sheets (formato CSV) o carga manual de archivos Excel (`.xlsx`, `.xls`).
*   **3 Vistas de Análisis (Pestañas):**
    1.  **Reporte Jerárquico:** Desglose visual por Departamento -> Supervisor, mostrando días de retraso (en rojo) y cantidad de planos afectados.
    2.  **Resumen General y Gráficos:** KPIs principales y 4 gráficos interactivos (Chart.js) de cumplimiento y montos.
    3.  **Detalle Operativo:** Tabla completa de requerimientos con columnas redimensionables y **reordenables (arrastrar y soltar)**.
*   **Filtrado Interconectado (Cascada):** Filtros dinámicos por Departamento, Contratista, Responsable y Condición de Plazo.
*   **Cálculo Automatizado:** El "Monto Total Proyectado" se calcula estrictamente sumando la columna `Monto MT` + `Monto MO`, ignorando totales precalculados en el origen.
*   **Exportación a PNG Full HD:** Botón "Resumen PNG" que genera un reporte visual en alta calidad (escala 3x), ideal para imprimir o compartir. Corrige problemas de truncamiento de texto y superposición de columnas.

## 🛠️ Tecnologías Utilizadas

*   **HTML5 / CSS3** (Estilos con [Tailwind CSS](https://tailwindcss.com/))
*   **JavaScript** (Vanilla)
*   **[Chart.js](https://www.chartjs.org/)** (Gráficos interactivos)
*   **[SheetJS (xlsx)](https://sheetjs.com/)** (Parseo de archivos Excel y CSV)
*   **[html2canvas](https://html2canvas.hertzen.com/)** (Captura del DOM a imagen PNG)
*   **[Lucide Icons](https://lucide.dev/)** (Iconografía)

## 📋 Requisitos de la Fuente de Datos

Para que el dashboard funcione correctamente, la hoja de cálculo (Google Sheets o Excel) debe cumplir con el siguiente formato:

1.  **Pestaña de Origen:** El sistema buscará explícitamente una pestaña llamada **`Fuente`** (o usará la primera pestaña por defecto si no la encuentra).
2.  **Cabeceras Requeridas (Nombres exactos o similares):**
    *   `SST` (Código del requerimiento)
    *   `Departamento`
    *   `Contratista`
    *   `Responsable Tecsur` (o Sup. Responsable)
    *   `Días pendientes Revisión 1`
    *   `Monto MT Proyectado` (o Monto MT)
    *   `Monto MO Proyectado` (o Monto MO)
    *   `CORRESPONDE PLANO` (Condición: "Dentro de plazo" / "Fuera de Plazo")

## ⚙️ Configuración (Google Sheets)

Si deseas conectar el dashboard a un Google Sheet en vivo:

1.  En tu Google Sheet, ve a **Archivo > Compartir > Publicar en la web**.
2.  Selecciona la pestaña `Fuente`, elige el formato **CSV** y haz clic en **Publicar**. Asegúrate de marcar la casilla *"Volver a publicar automáticamente cuando se realicen cambios"*.
3.  Copia el enlace generado.
4.  Abre el archivo `index.html` y busca la siguiente línea (cerca de la línea 350):
    ```javascript
    const GOOGLE_SHEET_CSV_URL = "TU_URL_AQUI?output=csv";
