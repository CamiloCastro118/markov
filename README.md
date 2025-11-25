## Markov Credit Risk — 

Aplicacion web ligera para modelar riesgo crediticio usando cadenas de Markov discretas. Permite introducir una matriz de transicion anual, seleccionar un estado inicial y calcular la distribucion de estados y la probabilidad de default en un horizonte temporal.

Contenido del repositorio
- `index.html` — interfaz, logica y visualizaciones (no requiere build; usa CDNs).
- `README.md` — este archivo con instrucciones y explicacion.

Resumen de funcionalidades
- Editar la matriz de transicion (filas = estados, columnas = probabilidades de ir a cada estado en 1 ano).
- Seleccionar estado inicial y horizonte (anos).
- Mostrar tabla ano a ano y graficos (linea y doughnut) con porcentajes.
- Resumen visual con probabilidad de default y una interpretacion sencilla (Bajo / Moderado / Alto).
- Control `Umbral alerta (%)` para marcar advertencias cuando la probabilidad supera el umbral.
- Selector de `Paleta` para elegir colores de visualizacion.
- Exportar resultados a CSV y descargar un informe en PDF (incluye tabla y graficos). Puedes anadir texto de firma para el PDF.

Explicacion simple del modelo
- Estados: por defecto la app usa `AAA, AA, A, BBB, BB, B, D` (D = default).
- Matriz de transicion P: cada fila i contiene las probabilidades de pasar desde el estado i a cada estado en 1 ano. Cada fila debe sumar aproximadamente 1.0.
- Si v0 es el vector one-hot del estado inicial, la distribucion tras t anos es v0 * P^t.
- La probabilidad de default al horizonte t es el componente correspondiente al estado `D` en v0 * P^t.

Formato y ejemplo de matriz
- Cada fila separada por salto de linea; columnas separadas por comas. Ejemplo (7 estados):

```
0.90,0.07,0.02,0.00,0.00,0.00,0.01
0.03,0.88,0.07,0.01,0.00,0.00,0.01
0.01,0.06,0.85,0.06,0.01,0.00,0.01
0.00,0.02,0.07,0.78,0.10,0.02,0.01
0.00,0.00,0.02,0.08,0.75,0.12,0.03
0.00,0.00,0.00,0.04,0.12,0.70,0.14
0.00,0.00,0.00,0.00,0.00,0.00,1.00
```

Pasos basicos para usar la app (rapido)
1. Abrir `index.html` en un navegador (doble clic) o servir la carpeta localmente:


2. Pegar o editar la matriz en el area de texto.
3. Elegir el `Estado inicial` (por ejemplo `A`) y el `Horizonte (anos)` (por ejemplo `3`).
4. Opcional: ajustar `Umbral alerta (%)` y la `Paleta` de colores.
5. Pulsar `Calcular probabilidades`.
6. Revisar la `Tabla de probabilidades por ano` y los graficos.
7. Exportar: usa `Exportar CSV` para descargar la tabla o `Descargar PDF` para generar un informe (puedes anadir texto de firma antes de generar el PDF).

Interpretacion de resultados (facil)
- La `Tabla por ano` muestra la probabilidad de estar en cada estado en cada ano del horizonte.
- El `Resumen` muestra la probabilidad de default al final del horizonte y la clasifica: `Bajo` (<1%), `Moderado` (1–5%), `Alto` (>5%).
- Ejemplo: si la probabilidad de default en 3 anos aparece como `4.00%`, significa que, bajo las transiciones definidas, 4 de cada 100 clientes en ese estado inicial terminarian en default en 3 anos segun el modelo.

Exportar CSV
- `Exportar CSV` descarga un archivo con columnas: `Ano,AAA,AA,A,BBB,BB,B,D` y valores en porcentaje.

Generar PDF
- `Descargar PDF` crea un informe A4 que incluye encabezado, parametros usados, tabla con `autoTable`, capturas de los graficos (si el navegador permite capturarlas) y una interpretacion breve.


Problemas comunes y soluciones
- Las filas de la matriz NO suman 1: la app muestra un error. Corrige la fila para que la suma sea 1.00 (o muy cercana).
- Imposible capturar graficos en el PDF: algunos navegadores bloquean la conversión a imagen por politicas de CORS si recursos externos estan involucrados. Solucion: usa recursos locales o abre la pagina desde un servidor local.
- (Nota) La opcion de incluir un logo en el PDF fue removida; solo se admite texto de firma en la version actual.

Detalles tecnicos
- Librerias usadas via CDN: `Chart.js`, `jsPDF` y `jsPDF-AutoTable`.
- La logica de la multiplicacion y elevacion de matrices esta implementada en `index.html` en JavaScript; `potenciaMatriz` usa exponenciacion rapida para eficiencia.



---
Autor Camilo Castro:  Este codigo es desarrollado  para una prueba educativa y como ejercicios para integrar la cadena de markov en ejemplo practicos en la vida cotidiana.
