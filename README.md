# 📦 Navegador de Rutas — App Reparto Amazon

Web app de un solo archivo (`index.html`, sin frameworks ni build) que lee el Excel diario de rutas de Amazon, deja elegir tu ruta y **ordena las paradas correctamente (1, 2, 3…)** para entregarlas en secuencia.

## Por qué existe

El `.xls` diario trae cada ruta en una hoja distinta, y dentro de cada hoja las paradas vienen **desordenadas** (stop 1, 28, 64, 38…). Esta app las reordena y te guía parada por parada desde el móvil.

## Cómo se usa

1. Abre la app en el móvil.
2. **Sube** el archivo `.xls` del día (arrastrando o tocando).
3. **Elige tu ruta** (ej. `C1`, `C2`…).
4. **Navega** parada por parada: ve la dirección, el Tracking ID, el horario y las notas; abre Google Maps; marca **✓ Entregado** y avanza solo.
5. Usa **Lista ☰** para ver todas las paradas y saltar a cualquiera.

## Formato del `.xls`

- Excel legacy `.xls` (también soporta `.xlsx`). Se lee con **SheetJS** por CDN.
- Una hoja por ruta: `sequencedRoute_XB_C1`, `..._C2`, …
- En cada hoja: fila 0 = metadatos (ignorada), fila 1 = nombres de columna (ignorada), fila 2+ = datos.
- Columnas por índice: `0` Stop · `1` Tracking ID · `3` Arrival · `4` Time Window · `5` Dirección · `6` Código postal · `8` Notas · `9` Lat · `10` Lng · `13` Zona.
- Se descartan filas con stop no numérico o ≤ 0; las paradas se ordenan ascendentemente; la ventana horaria se muestra sin segundos.

## Detalles técnicos

- **Vanilla JS**, sin React/Babel/build (carga rápida en móvil).
- Única dependencia: `xlsx.full.min.js` (SheetJS) por CDN.
- Estado en memoria (sin `localStorage`): el progreso se reinicia al recargar.
- Textos del Excel escapados para evitar romper el render.

## Despliegue

Sitio estático: basta `index.html` en la raíz, sin configuración de build. Desplegado en Vercel.
