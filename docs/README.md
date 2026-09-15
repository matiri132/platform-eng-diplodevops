# Deck — De DevOps a Platform Engineering

Presentación reveal.js de la clase, con la identidad de la diplomatura.

| | |
|---|---|
| Slides | 54 de contenido —una de reserva, oculta— más 7 separadores de bloque |
| Tema | `dist/theme/diplodevops.css` |
| Identidad | Paleta, tipografía y logos del deck institucional de la diplomatura |
| Contenido | [`../01-apunte-teorico.md`](../01-apunte-teorico.md) · las notas del orador viajan embebidas en las slides |

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
| 1 | ~~Nombre y contacto del docente~~ | ✅ Hecho: portada y filmina de cierre |
| 2 | Las capturas de la organización de demostración | Recuadros punteados `.dd-shot` de la slide 41b. El resto del bloque usa capturas de la documentación pública de Port |
| 3 | El diagrama oficial de los cinco planos | Recuadro punteado de la slide 20 |
| 4 | Nombres reales de los módulos previos | Slide 20b |
| 5 | Video de respaldo de la demostración | Slide gemela de la 45 |
| 6 | Confirmar que la identidad de 2024 sigue vigente | Todo el tema |

## Estructura del tema

Mismo vocabulario de clases que el tema Craftech, con la paleta y la tipografía de la diplomatura.

Lo que conviene saber para editar:

- `section.on-dark` en toda slide con `data-background-color` azul u oscuro. Sin eso, el texto y el pie institucional quedan ilegibles.
- `section.dense` cuando la slide tiene una tabla larga o muchas tarjetas.
- El pie institucional vive fuera de `.slides`, en `div.dd-footer`, y alterna blanco y azul por JavaScript según la clase de la slide activa.
- Los diagramas ASCII van en `<pre><code class="plaintext nohighlight">`. Sin esas clases, el resaltador de sintaxis colorea palabras sueltas en español.

## Dependencias

Poppins y Roboto Mono se cargan desde Google Fonts. Sin conexión el deck funciona, pero cae a la tipografía del sistema. Para presentar sin red, descargar las fuentes a `assets/fonts/` y reemplazar el `@import` del tema.
