# Terremoto Quibdó — Necesidades por barrio

Repositorio público de la Fundación Círculo de Estudios Culturales y Políticos con información **exclusivamente relacionada con el terremoto de Quibdó (agosto de 2026)**. No contiene, ni contendrá, datos sobre otros temas de la Fundación (por ejemplo, casos de homicidios NNAJ) ni ningún dato identificable de personas — solo conteos y porcentajes agregados por barrio.

## Qué hay aquí

| Archivo | Qué es |
|---|---|
| `index.html` | El tablero público. Se publica solo con GitHub Pages — es la página que la gente ve. |
| `AVANCES.md` | Bitácora: qué se ha hecho, cuándo y quién lo hizo. |
| `README.md` | Este archivo. |

## Cómo funciona el sistema completo

Esto no vive solo en GitHub — es una cadena de tres partes que se alimentan solas:

1. **Formulario de campo (Google Forms)** — los voluntarios registran hogares afectados.
2. **Google Sheet + Apps Script** — cada respuesta nueva dispara el script `Mapa_Necesidades_AppsScript.gs`, que agrega los datos por barrio (nunca por hogar individual) y los escribe en la pestaña "Mapa de Necesidades" de la hoja.
3. **Esta página (`index.html`)** — publicada en GitHub Pages, lee en vivo el CSV publicado de esa pestaña cada vez que alguien la abre. No hay que resubir nada a GitHub cuando llega información nueva: se actualiza sola.

```
Formulario → Google Sheet → Apps Script (agrega por barrio) → Sheet publicada como CSV → index.html (GitHub Pages)
```

## Enlace del tablero en vivo

`https://TU-USUARIO.github.io/terremoto-quibdo-necesidades/`
*(actualiza esta línea con tu URL real una vez actives GitHub Pages)*

## Cómo actualizar el enlace del CSV

Si el enlace publicado del Google Sheet cambia (por ejemplo, si recreas la hoja), edita la línea `SHEET_CSV_URL` cerca del inicio de `index.html` — instrucciones detalladas en `AVANCES.md`, entrada del 4 de septiembre de 2026.

## Próximo paso pendiente

Registro de ayudas entregadas (qué se entregó, en qué barrio, cuándo) — todavía no está integrado a este sistema. Ver `AVANCES.md` para el estado actual.
