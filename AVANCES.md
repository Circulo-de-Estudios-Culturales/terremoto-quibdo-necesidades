# Bitácora de avances — Terremoto Quibdó

Registro de qué se ha hecho en este proyecto, en orden cronológico (lo más reciente arriba). Cada vez que hagas un cambio importante, agrega una entrada nueva aquí — así queda memoria de las decisiones, sin depender de recordar por qué se hizo algo.

**Cómo agregar una entrada:** abre este archivo en GitHub, ícono de lápiz (editar), escribe tu entrada nueva justo debajo de este párrafo, y confirma el cambio ("Commit changes"). No hace falta ningún otro paso.

---

### 2026-09-09 (noche) — Corrección importante en el conteo de necesidades
**Error encontrado y corregido:** el script separaba las respuestas de selección múltiple partiendo el texto por comas, pero varias opciones del formulario tienen comas adentro del paréntesis. La opción "apoyo psicosocial (es decir, en la salud mental y emocional suya y/o de su familia)" quedaba cortada en dos y se contaba como dos necesidades distintas ("apoyo psicosocial (es decir" y "en la salud mental y emocional suya y/o de su familia)"). Ahora solo corta en las comas que están fuera de paréntesis, así que el apoyo psicosocial —que es una pregunta explícita del formulario— se cuenta correcto. Además las etiquetas largas se acortan al mostrarlas ("apoyo psicosocial" en vez de la explicación completa).

**Diseño:** barra superior con el logo pequeño y el enlace a Recursos; las cifras pasaron a tres bloques propios; el panel del barrio ahora es fijo y sigue al bajar por el mapa; la nota larga salió de la leyenda; y la lista de barrios dejó de ser 45 tarjetas y ahora es una tabla compacta ordenada por hogares, con "OTRO" y "Sin barrio registrado" al final marcados como sin clasificar.

### 2026-09-09 (tarde) — Comunas, lista plegable y página de recursos
- **Comunas en el mapa.** Se agruparon los barrios por comuna usando la asignación que ya traía la cartografía social del equipo (37 de los 39 barrios ubicados). Cada comuna es un área punteada clickeable: al hacer clic muestra el agregado de esa comuna — hogares, desglose de daño, % de daño grave, necesidad más reportada y el detalle barrio por barrio. Son agrupaciones de trabajo, no límites oficiales de comuna. *Pendiente: El Jardín y Jardín no aparecen en la cartografía social, falta decidir a qué comuna pertenecen.*
- **La lista de tarjetas quedó oculta por defecto.** Ahora la información se ve al hacer clic en el mapa. La lista completa se abre con un botón, y aparece sola cuando se escribe algo en el buscador.
- **Cabí salió del mapa.** Su punto de referencia (una escuela) queda al sur, fuera del área mapeada. Pasó a la lista de barrios sin ubicación, que es lo honesto. *Pendiente: ubicarlo.*
- **Nueva página `recursos.html`**, armada con el Directorio de Servicios Institucionales y la Ruta de Acompañamiento Psicosocial: líneas 106/155/141/192, el paso del RUD, vivienda, alimentación, salud, salud mental, VBG, protección de NNA, servicios básicos, educación y orientación jurídica; más una sección para voluntarios/as con el alcance del acompañamiento y los criterios de derivación clínica. Enlazada desde el tablero.

### 2026-09-09 — Mapa geográfico real y desglose de daño en vivienda
Dos cambios grandes:

**1. Desglose de daño.** El script ahora cuenta por separado, por barrio, las viviendas colapsadas, con daño severo, con daño leve y sin daño visible, y calcula el "% de daño grave" (colapsadas + severo). Son 5 columnas nuevas al final de la pestaña "Mapa de Necesidades". El mapa usa ese porcentaje para colorear: el color ya no significa "cuántos hogares" sino "qué tan grave es el daño".

**2. Mapa real.** Se reemplazó el mapa esquemático de la cartografía social por un mapa geográfico verdadero:
- Calles del centro de Quibdó: Copernicus EMS, activación EMSR916, producto AOI 04 Quibdo Centre (616 tramos).
- Calles del norte y río Atrato: OpenStreetMap (384 tramos).
- Ubicación de los barrios: OpenStreetMap, place=neighbourhood/suburb. 34 de los 44 barrios de la hoja quedaron con coordenada exacta.
- 6 barrios quedaron con ubicación aproximada, tomada de una referencia con el mismo nombre (escuela, aeropuerto): Cabí, Caraño, Caraño Piñal, La Esmeralda, Obrero, Parque la Gloria. Se marcan con borde punteado. **Pendiente: confirmar dónde quedan realmente.**
- 4 barrios siguen sin ubicación y solo aparecen en la lista: La Cascorba, La Paloma, Las Palmas de Medrada, Obapo. **Pendiente: ubicarlos.**
- Capa opcional: las 74 viviendas evaluadas por satélite por Copernicus (18 destruidas, 8 dañadas, 48 posiblemente dañadas). Es evaluación oficial, independiente del trabajo de campo.

Nota sobre las fuentes descartadas: el DANE bloquea la descarga directa y su Marco Geoestadístico identifica las zonas urbanas por código, no por nombre de barrio, así que no sirve para cruzar con la hoja. El paquete de Copernicus no trae ningún nombre de barrio (el campo `name` dice "Unknown" en las 74 edificaciones).

Se agregó también un buscador de barrios sobre la lista.

### 2026-09-09 — ⚠️ Hallazgo urgente: brecha de información en el reporte oficial de daños
La Alcaldía de Quibdó tiene una página oficial (reportaquibdo.com) para que las familias reporten el daño de su vivienda, con un plazo que cierra en los próximos dos días. Según una presidenta de JAC consultada, en la práctica los reportes de su sector solo se están canalizando a través de las Juntas de Acción Comunal, no directamente por la página oficial — es decir, hay riesgo real de que familias afectadas queden por fuera del censo oficial (y de la ayuda institucional asociada) si su JAC no alcanza a trasladar el reporte a tiempo. Pendiente de verificar qué tan generalizado es este patrón en otras JAC/barrios.

**Acción tomada:** se redactó un mensaje corto para difundir a través de las JAC urgiendo el registro directo antes del cierre (ver más abajo / solicitar a Silvia).

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
