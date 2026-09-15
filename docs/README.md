# Deck — De DevOps a Platform Engineering

Presentación reveal.js de la clase, con la identidad de la diplomatura.

| | |
|---|---|
| Slides | 55 de contenido, más 7 separadores de bloque y 1 de reserva oculta |
| Tema | `dist/theme/diplodevops.css` |
| Identidad | Derivada del deck institucional de la diplomatura — ver [`../04-diseno-diplodevops.md`](../04-diseno-diplodevops.md) |
| Contenido | [`../03-propuesta-slides.md`](../03-propuesta-slides.md) · notas del orador desde [`../02-guia-docente.md`](../02-guia-docente.md) |

## Ver y presentar

```bash
python3 -m http.server 8000     # desde este directorio
```

| Tecla | Qué hace |
|---|---|
| `S` | Vista del orador, con las notas y el reloj |
| `Esc` | Vista general de todas las slides |
| `F` | Pantalla completa |
| `Ctrl` + clic | Acercar una zona |

Para exportar a PDF, abrir `http://localhost:8000/?print-pdf` y usar la impresión del navegador.

## Qué falta antes de dictar

| # | Pendiente | Dónde |
|---|---|---|
| 1 | Nombre y contacto del docente | Slides 1 y 47 — buscar `[nombre]` y `[contacto]` |
| 2 | Las seis capturas de Port | Recuadros punteados `.dd-shot`, slides 38 a 41b |
| 3 | El diagrama oficial de los cinco planos | Recuadro punteado de la slide 20 |
| 4 | Nombres reales de los módulos previos | Slide 20b |
| 5 | Video de respaldo de la demostración | Slide gemela de la 45 |
| 6 | Confirmar que la identidad de 2024 sigue vigente | Todo el tema |

## Estructura del tema

Mismo vocabulario de clases que el tema Craftech, con la paleta y la tipografía de la diplomatura. Las clases están documentadas en [`../04-diseno-diplodevops.md`](../04-diseno-diplodevops.md), sección 6.

Lo que conviene saber para editar:

- `section.on-dark` en toda slide con `data-background-color` azul u oscuro. Sin eso, el texto y el pie institucional quedan ilegibles.
- `section.dense` cuando la slide tiene una tabla larga o muchas tarjetas.
- El pie institucional vive fuera de `.slides`, en `div.dd-footer`, y alterna blanco y azul por JavaScript según la clase de la slide activa.
- Los diagramas ASCII van en `<pre><code class="plaintext nohighlight">`. Sin esas clases, el resaltador de sintaxis colorea palabras sueltas en español.

## Dependencias

Poppins y Roboto Mono se cargan desde Google Fonts. Sin conexión el deck funciona, pero cae a la tipografía del sistema. Para presentar sin red, descargar las fuentes a `assets/fonts/` y reemplazar el `@import` del tema.
