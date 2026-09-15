# Sistema de diseño DiploDevOps

**Preparado por:** Craftech
**Origen:** ingeniería inversa del deck institucional "Infraestructura en la Nube, Clase 2", 29/08/2024, 35 slides
**Uso:** reproducir la identidad de la diplomatura en materiales nuevos
**Fecha:** 2026-09-15
**Estado:** derivado de un deck de agosto de 2024 — pendiente confirmar que sigue vigente

---

## 1. Advertencia sobre la fuente

Todo lo de abajo se extrajo de un único archivo, del que el propio usuario avisó que puede no ser la versión actual. Dos consecuencias:

| Riesgo | Mitigación |
|---|---|
| La identidad pudo cambiar desde agosto de 2024 | Contrastar la portada y los colores con un deck reciente antes de dar el diseño por bueno |
| No hay manual de marca: todo es inferido de un archivo | Los valores son los que el archivo usa, no necesariamente los que la marca declara |

🟡 **Pendiente.** Confirmar con la coordinación del programa si esta es la identidad vigente y si existe un manual de marca o una plantilla oficial. **Bloquea:** dar por cerrado el diseño del deck.

Un hallazgo que cambia una decisión previa: **Craftech ya aparece en la franja institucional de todas las slides**, junto a UNC, FCEFyN y la Secretaría de Extensión. No es una marca invitada que haya que introducir con cuidado — es parte del pie estándar del programa.

---

## 2. Paleta

Colores medidos sobre el XML del archivo, con su frecuencia de uso.

| Token | Hex | Rol | Dónde aparece |
|---|---|---|---|
| Azul primario | `#4A86E6` | Marca. Fondo de portada, títulos de contenido, acentos | 109 usos; es el color dominante |
| Azul profundo | `#1D419F` | Paneles de separador de sección, texto sobre claro | Overlay del divisor |
| Panel | `#EAF5F7` | Fondo de bloques, columnas laterales, tarjetas | 21 usos |
| Blanco | `#FFFFFF` | Fondo de slides de contenido, texto sobre azul | — |
| Tinta | `#212121` | Texto de cuerpo | `accent2` del tema |
| Verde | `#188038` | Estado correcto | — |
| Rojo | `#EB5757` | Código y errores | Bloques de terminal |
| Ámbar | `#FFAB40` | Acento secundario | `accent4` del tema |
| Teal | `#0097A7` | Enlaces | `hlink` del tema |

La combinación que define la identidad es **blanco de fondo con títulos `#4A86E6`**; el azul saturado se reserva para portada y cierre, y el `#1D419F` para los separadores.

---

## 3. Tipografía

| Rol | Fuente | Evidencia |
|---|---|---|
| Títulos y cuerpo | **Poppins** | 717 usos, dominante por amplio margen |
| Secundaria | Open Sans | 56 usos |
| Código | Roboto Mono, con Courier New como caída | 20 y 8 usos |

Tamaños medidos, sobre un lienzo de 10 × 5,625 pulgadas (16:9):

| Elemento | Tamaño |
|---|---|
| Título de portada | 34 pt |
| Subtítulo de portada | 22 pt |
| Título de sección | 33-34 pt |
| Título de contenido | 25-29 pt |
| Subtítulo de bloque | 15 pt |
| Cuerpo | 9-12 pt |
| Fecha y pies | 7-12 pt |

El salto entre título y cuerpo es grande —de 26 a 10 pt—, y es parte del carácter del diseño: títulos rotundos, cuerpo pequeño y denso.

---

## 4. Arquetipos de slide

Cada uno está escrito como un prompt reutilizable: describe qué componer, sin depender de la herramienta.

### 4.1 Portada

> Lienzo 16:9 con fondo azul sólido `#4A86E6`. Título en Poppins bold blanco, 34 pt, alineado a la izquierda, en el tercio central. Subtítulo blanco 22 pt debajo. Fecha en 12 pt arriba a la izquierda. Elementos decorativos: el símbolo de infinito en trazo blanco grueso, recortado por el borde inferior izquierdo, y una mancha orgánica azul-violeta con textura de líneas entrando desde el borde superior derecho. Franja institucional blanca abajo a la derecha, de 1,4 × 0,27 pulgadas. Sin caja ni marco alrededor del texto.

### 4.2 Separador de sección

> Fotografía a sangre completa, en tono frío, ocupando toda la slide. Encima, un panel rectangular azul profundo `#1D419F` que cubre la mitad izquierda hasta media altura. Sobre el panel, el número y el título de la sección en Poppins bold blanco, 34 pt. Franja institucional blanca abajo a la derecha. Sin viñetas ni cuerpo de texto: la slide es solo el título.

### 4.3 Contenido con imagen

> Fondo blanco. Columna izquierda de texto ocupando poco más de la mitad del ancho; columna derecha con una captura o diagrama que llega hasta el borde. Detrás de la columna de texto, un rectángulo `#EAF5F7` a sangre por el borde izquierdo. Título en Poppins bold `#4A86E6`, 26-29 pt, alineado arriba a la izquierda, con el resto del contenido comenzando a un tercio de la altura. Cuerpo en Poppins regular `#212121`, 11 pt. Wordmark "#DiploDevOps" en azul profundo abajo a la izquierda y franja institucional abajo a la derecha.

### 4.4 Índice o agenda

> Fondo blanco. Título "Agenda" en `#4A86E6`, 33 pt, arriba a la izquierda. Debajo, una columna de numeración —01, 02, 03, 04— en Poppins bold negro 30 pt, alineada a la izquierda, y a su derecha una columna con el nombre de cada punto en 15 pt y una bajada explicativa en 9 pt gris. Interlineado generoso: cada entrada ocupa aproximadamente un cuarto de la altura útil.

### 4.5 Bloque de código o terminal

> Fondo blanco. Título en `#4A86E6`. El bloque de comandos sobre un rectángulo azul muy oscuro, casi negro, esquinas apenas redondeadas, con el texto en Roboto Mono blanco y el prompt `$` en un tono más apagado. Los comentarios o resaltados dentro del bloque, en rojo `#EB5757`.

### 4.6 Pie institucional

> En todas las slides salvo la portada: el wordmark **#DiploDevOps** abajo a la izquierda, y la franja de logos institucionales abajo a la derecha, con este orden y separados por barras verticales finas — CRAFTECH · unc · FCEFyN · SECRETARÍA DE EXTENSIÓN · PROGRAMA DE CAPACITACIÓN Y FORMACIÓN CONTINUA. Altura de la franja, 0,27 pulgadas; nunca se reescala desproporcionadamente ni se reordena. Sobre fondos claros, ambos en azul profundo; sobre fondos azules u oscuros, ambos en blanco.

---

## 5. Activos extraídos

Están en `docs/assets/`, sacados del PPTX y preparados para web.

| Archivo | Qué es | Origen |
|---|---|---|
| `diplodevops-wordmark-white.png` | Wordmark #DiploDevOps, blanco, recortado | `image6.png`, en las 35 slides |
| `diplodevops-wordmark-navy.png` | El mismo, recoloreado a `#1D419F` para fondos claros | derivado |
| `institucional-white.png` | Franja CRAFTECH · UNC · FCEFyN · Secretaría, blanca | `image8.png`, en 34 slides |
| `institucional-navy.png` | La misma, recoloreada para fondos claros | derivado |
| `infinito-white.png` · `infinito-navy.png` | Símbolo de infinito, para decoración a sangre | `image10.png` |
| `infinito-azul.png` | Infinito blanco sobre cuadrado azul, 512 × 512 | `image1.png`, sirve de favicon |
| `blob-1.png` · `blob-2.png` | Manchas decorativas con textura de líneas | `image2.png`, `image3.png`, portada |

Los originales son PNG blancos con transparencia, pensados para fondo oscuro. Las variantes en azul profundo se generaron recoloreando el canal de color y conservando el alfa: es el mismo trazo, no un redibujo.

---

## 6. Traducción a reveal.js

El tema `docs/dist/theme/diplodevops.css` reimplementa esta identidad conservando **el mismo vocabulario de clases del tema Craftech**, para que quien conozca uno pueda editar el otro.

| Clase | Qué hace en este tema |
|---|---|
| `.title-slide` | Portada: texto blanco sobre azul |
| `section.divider` | Separador de sección: título blanco con regla, sobre azul profundo |
| `section.statement` | Una sola frase centrada verticalmente, para los golpes de efecto |
| `section.on-dark` | Invierte texto, reglas, viñetas, tablas y tarjetas para fondo azul u oscuro |
| `section.dense` | Reduce cuerpo y tablas cuando la slide tiene mucho contenido |
| `.ct-cards` / `.ct-card` | Tarjetas sobre `#EAF5F7`; `.num`, `.ct-title`, `.status`, `.tentative` |
| `.ct-objective` | Callout con barra azul a la izquierda, para la conclusión de una slide |
| `.dd-quote` | Cita en inglés con su traducción y la fuente al pie |
| `.dd-two` | Dos columnas; `.wide-left` para 60/40 |
| `.dd-panel` | Bloque sobre fondo `#EAF5F7` |
| `.dd-source` | Fuente en tipografía chica, anclada al pie de la slide |
| `.dd-shot` | Marco punteado que reserva el lugar de una captura pendiente |
| `.dd-footer` | Pie institucional; alterna blanco y azul según la slide |

Diferencias deliberadas respecto del tema Craftech: fondo claro en lugar de oscuro, Poppins en lugar de Inter, y la regla de acento en degradado azul en lugar de cian a coral.

**Dependencia externa:** Poppins y Roboto Mono se cargan desde Google Fonts. Sin conexión, el deck cae a la pila de sistema y pierde el carácter tipográfico. Para uso offline hay que descargar las fuentes a `assets/fonts/` y reemplazar el `@import`.
