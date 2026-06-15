# Portal Inventario DEGASA

Dashboard de inventario alimentado desde Google Sheets (vía opensheet), con tablas Tabulator
a pantalla completa, barras de magnitud de stock, semáforo de caducidad y filtros rápidos.

## Estructura

| Archivo | Responsabilidad |
|---|---|
| `index.html` | Solo el marcado (estructura de la página). |
| `styles.css` | Todo el diseño/estilos. |
| `config.js` | Parámetros de negocio (editar aquí, sin tocar la lógica). |
| `app.js` | Lógica: carga de datos, columnas, filtros, modal, persistencia, toggles. |

El orden de carga importa: `config.js` se carga **antes** que `app.js`.

## Cómo ejecutar

- **Local**: abrir `index.html` directamente en el navegador (funciona con `file://`).
- **Vercel / hosting estático**: subir los 4 archivos juntos a la raíz. No requiere build.

## Interfaz / distribución

- **Barra superior fija** con el título, las pestañas de vista (Resumen / Lote),
  los botones para mostrar/ocultar **KPIs** y **Filtros**, y recargar.
- **KPIs arriba**: se desplazan con la página; al bajar desaparecen.
- **Filtros en columna izquierda** (sticky): búsqueda, filtro rápido, constructor de
  filtros, selector de inventarios, exportación y zoom.
- **Tabla a la derecha**, sticky y a ~pantalla completa: al hacer scroll hacia abajo
  los KPIs se ocultan y la tabla queda ocupando el máximo espacio.
- Scroll **vertical y horizontal** dentro de la tabla; la primera columna queda fija.

## Configuración (`config.js`)

- `sheetId` / `tabs`: hoja y pestañas de Google Sheets.
- `lowStock`: umbral de "stock bajo" (barras y filtro rápido de stock).
- `expiry.mes1/mes3/mes6`: cortes de caducidad en días (color y filtro "por vencer").
- `refreshMs`: intervalo de autorrecarga.
- `persistUi`: recordar zoom, centros visibles y estado de Indicadores/Filtros. La vista siempre inicia en "Resumen General".

## Funciones destacadas

- Barras de magnitud proporcionales por columna en cantidades.
- Caducidad con meses + días y 5 niveles de color, con leyenda.
- Primera columna congelada, orden numérico real y fila de totales.
- Filtros rápidos: caducidad (Vencidos / Por vencer) y stock (Agotados / Bajos) con conteos.
- Persistencia de estado de UI.
