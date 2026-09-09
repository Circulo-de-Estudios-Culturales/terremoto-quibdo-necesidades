# Bitácora de avances — Terremoto Quibdó

Registro de qué se ha hecho en este proyecto, en orden cronológico (lo más reciente arriba). Cada vez que hagas un cambio importante, agrega una entrada nueva aquí — así queda memoria de las decisiones, sin depender de recordar por qué se hizo algo.

**Cómo agregar una entrada:** abre este archivo en GitHub, ícono de lápiz (editar), escribe tu entrada nueva justo debajo de este párrafo, y confirma el cambio ("Commit changes"). No hace falta ningún otro paso.

---

### 2026-09-08 — Corrección de barrios duplicados
Se identificó que algunas respuestas del formulario nombran el mismo barrio de formas distintas ("El reposo número 2" / "Reposo 2", "Caraño" / "Caraño Piñal"). Se agregó al script (`Mapa_Necesidades_AppsScript.gs`) una tabla `ALIASES_BARRIO` que une esas variantes antes de sumar los hogares, para que no aparezcan como barrios separados en el Mapa de Necesidades.

### 2026-09-04 — Página pública conectada al Google Sheet
Se construyó `index.html`: una página independiente (sin dependencias externas) que lee en vivo el CSV publicado de la pestaña "Mapa de Necesidades" y colorea el mapa de barrios según cantidad de hogares registrados. Se ajustó el estilo a Courier New y a los colores de la Fundación (naranja `#C55A11`).

Para conectar un nuevo enlace de CSV: Google Sheet → Archivo → Compartir → Publicar en la web → elegir la pestaña "Mapa de Necesidades" → formato CSV → Publicar → copiar el enlace → pegarlo en la línea `SHEET_CSV_URL` al inicio de `index.html`.

### 2026-09-04 — Script de Apps Script instalado y corregido
Se instaló `Mapa_Necesidades_AppsScript.gs` en el Google Sheet de respuestas del formulario. Se corrigieron dos problemas: el nombre real de la pestaña de respuestas ("Respuestas de formulario 1", no el nombre del archivo), y espacios invisibles al final de algunas preguntas del formulario que impedían encontrar las columnas de barrio y necesidades. El script excluye por completo las columnas de texto libre (donde queda información identificable) y solo agrega por barrio.

### Pendiente
- Registro de ayudas entregadas (qué se entregó, dónde, cuándo) — todavía no existe como parte de este sistema. Ver propuesta en la conversación con Claude del 2026-09-08.
- Resolver los hogares que caen en "Sin barrio registrado" u "OTRO" — su barrio real solo quedó escrito en una columna de comentarios que no se puede usar de forma segura.
- Decidir si se agregan más equivalencias de barrios a `ALIASES_BARRIO` (hay varias posibles en la lista de opciones del formulario que aún no se han confirmado).
