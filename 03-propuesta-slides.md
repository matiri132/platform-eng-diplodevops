# Propuesta de slides — De DevOps a Platform Engineering

**Preparado por:** Craftech (docente invitado)
**Programa:** DiploDevops — módulo Platform Engineering
**Alcance:** guion visual, slide por slide. No incluye el archivo de la presentación
**Contenido de referencia:** [`01-apunte-teorico.md`](01-apunte-teorico.md) · [`02-guia-docente.md`](02-guia-docente.md)
**Fecha:** 2026-09-14
**Estado:** borrador — bloqueado por los activos de marca de DiploDevops

---

## 1. Branding

La presentación usa la identidad de **DiploDevops**. Craftech aparece como **docente invitado**, no como marca anfitriona.

| Regla | Detalle |
|---|---|
| Plantilla | DiploDevops: colores, tipografía, retícula y pie de página del programa |
| Logo DiploDevops | Portada y pie de todas las slides |
| Logo Craftech | Dos apariciones: portada, bajo "docente invitado", y la slide de apertura de la demostración. En ninguna otra |
| Proporción | En la portada, el logo de Craftech no supera el 60% del tamaño del de DiploDevops |
| Capturas | Solo de la organización de demostración. Ninguna del portal interno productivo |
| Logos de terceros | Backstage, Port, Cortex y demás aparecen solo en la slide de panorama de herramientas, todos al mismo tamaño |

✅ **Resuelto — identidad.** La paleta, la tipografía y los logos se extrajeron de el deck institucional de la diplomatura y están documentados en [`04-diseno-diplodevops.md`](04-diseno-diplodevops.md). Los activos, en [`docs/assets/`](docs/assets/).

✅ **Resuelto — formato.** El deck está construido en reveal.js: [`docs/`](docs/) y publicado en [GitHub Pages](https://matiri132.github.io/platform-eng-diplodevops/). Exporta a PDF con `?print-pdf`. Si el programa exige Google Slides o PowerPoint, este documento sigue sirviendo como guion.

🟡 **Pendiente — vigencia de la identidad.** El PPTX de origen es de agosto de 2024. **Bloquea:** dar el diseño por cerrado.

> **Corrección sobre el branding.** Craftech **ya está en la franja institucional** de todas las slides del programa, junto a UNC, FCEFyN y la Secretaría de Extensión. No es una marca invitada que haya que introducir con cuidado: es parte del pie estándar. La regla de las dos apariciones del logo queda sin efecto — se usa la franja institucional tal como viene.

---

## 2. Estructura

55 slides, una de ellas de reserva, para 90 minutos. Densidad objetivo: una idea por slide, máximo cinco líneas de texto.

La numeración con letra —20b, 24b, 31b— marca las slides agregadas sobre la estructura original: van pegadas a la que las precede y desarrollan el mismo punto. Se numeran así para que el recorte sea evidente, no por capricho.

| Slides | Bloque | Cuántas | Minutos | Apunte |
|---|---|---|---|---|
| 1–3 | Apertura | 3 | 3 | — |
| 4–10 | DevOps | 8, una de reserva | 8 | 1 |
| 11–16 | Por qué aparece Platform Engineering | 6 | 9 | 2 |
| 17–24b | Plataforma | 10 | 10 | 4 |
| 25–33c | Portal | 13 | 11 | 5 y 9.2 |
| 34–37 | Estandarización | 4 | 9 | 6 |
| 38–41b | Port | 5 | 5 | 7 |
| 42–44 | Era agéntica | 3 | 5 | 8 |
| 45 | Apertura de demostración | 1 | — | — |
| 46–47 | Cierre | 2 | 4 | — |

Los bloques y los minutos coinciden con la tabla de la sección 3 de [`02-guia-docente.md`](02-guia-docente.md). Si se cambia uno, se cambia el otro.

Las slides marcadas **★** son las que no se recortan bajo ninguna circunstancia. La 9b es de reserva: va oculta y se muestra solo si el bloque va adelantado.

---

## 3. Slides

### Apertura

**1 · Portada**
Título: *De DevOps a Platform Engineering: plataformas, portales y estandarización*. Subtítulo: módulo y fecha. Logo DiploDevops arriba. Al pie: "Docente invitado: [nombre] — Craftech" con el logo de Craftech.

**2 · El recorrido**
Siete pasos en una línea de tiempo horizontal: DevOps → su límite → la plataforma que ya existe → el portal → el estándar → Port → los agentes.
Se muestra también como slide de transición entre bloques, con el paso actual resaltado.

**3 · Encuadre**
Tres líneas: se usa una herramienta comercial como ejemplo; no es una recomendación de compra; la demostración corre sobre datos ficticios.

### DevOps

**4 · El muro**
Dos columnas enfrentadas: Desarrollo y Operaciones, con qué se le pedía y cómo se lo medía a cada una. Un muro vertical en el medio.

**5 · El ciclo**
Diagrama circular de cuatro nodos: despliegues infrecuentes → grandes → riesgosos → se hacen menos seguido.

**6 · You build it, you run it**
Cita de Vogels, verbatim, con la fuente al pie (ACM Queue, 2006).

**7 · 2009**
Dos hitos sobre una línea de tiempo: junio, Velocity —Allspaw y Hammond—; octubre, DevOpsDays Gante —Debois—.
Al pie, el enlace a la charla de 2009.

**8 · Qué proponía**
Cuatro ítems: responsabilidad compartida, automatización, lotes chicos, medición.

**9 · ★ Qué resolvió**
Las cuatro métricas DORA en una tabla, agrupadas en sus dos dimensiones —rendimiento y estabilidad—, y debajo una línea: *velocidad y estabilidad no se oponen*.

**9b · Westrum (slide de reserva)**
Tres filas: patológica, burocrática, generativa, con qué hace cada una con una mala noticia.
Se muestra solo si el bloque va adelantado. Va oculta en la presentación, no eliminada.

**10 · ★ Ley de Conway y el antipatrón**
Cita verbatim de Conway (1968), con la fuente.
Debajo, los antipatrones de DevOps Topologies en una lista corta, y el criterio: *si le piden cosas y las hace, es un silo; si publica capacidades que otros consumen sin pedirle nada, es plataforma*.

### Por qué aparece Platform Engineering

**11 · Lo que cambió debajo**
Línea de tiempo: cloud, Docker, Kubernetes, Terraform, microservicios, GitOps.
Línea de cierre: *cada una resolvió un problema real; sumadas crearon uno que ninguna buscaba*.

**12 · Pregunta**
Una sola línea grande: *¿Cuántas decisiones hay que tomar para poner un "hola mundo" en producción?*
Queda en pantalla mientras se recogen respuestas.

**13 · ★ La respuesta**
Tabla de ocho filas: código, empaquetado, infraestructura, entrega, exposición, identidad, operación, gobierno. Revelado progresivo o completa; el efecto buscado es la densidad.

**14 · Shift left**
Cita de platformengineering.org sobre la carga que el shift left puso en el desarrollador. Debajo, el antipatrón de operaciones en la sombra, en una línea.

**15 · ★ Carga cognitiva**
Tres columnas: intrínseca, extrínseca, germane, con un ejemplo cada una.
Visual: tres bloques apilados donde el extrínseco se expande y comprime al germane.

**16 · Definición**
Cita de la definición de platform engineering, con la fuente.
Debajo, en negrita: *no reemplaza a DevOps; organiza el trabajo que DevOps hizo necesario*.

### Plataforma

**17 · ★ La plataforma que ya existe**
Una sola línea en pantalla completa: *Si una empresa despliega software a producción, ya tiene una plataforma.*
Se queda unos segundos antes de avanzar.

**18 · Qué incluye**
Los siete elementos que toda empresa que despliega ya tiene: repositorios, build, despliegue, infraestructura, monitoreo, secretos, reglas de acceso.

**19 · ★ Implícita o explícita**
Tabla comparativa de seis filas. Resaltar la fila "qué pasa si se va una persona".

**20 · ★ Los cinco planos**
**El diagrama oficial de la arquitectura de referencia**, con los servicios de cada plano. Se toma de [platformengineering.org/reports](https://platformengineering.org/reports) —AWS, Azure o GCP, el que corresponda a lo que el grupo cursó— y se muestra a pantalla completa, con atribución visible al pie.
Es la única slide de la clase donde un diagrama ajeno vale más que uno propio: los estudiantes van a encontrar ese mismo gráfico cuando busquen el tema.
Si por licencia o calidad de imagen no puede usarse, el apunte tiene una versión propia equivalente en la sección 4.2.

**20b · ★ Dónde encaja lo que ya viste**
La misma figura de los cinco planos, ahora con los temas de los módulos anteriores de la diplomatura ubicados sobre cada plano: Git, contenedores, CI/CD, IaC, Kubernetes, redes, observabilidad, IAM y secretos.
Es la slide que convierte el mapa en algo propio del grupo. Va inmediatamente después de la 20, sobre la misma figura, para que se lea como una capa encima y no como otro diagrama.

**21 · Ejercicio**
La misma tabla de cinco planos, vacía, con la consigna: completarla con las herramientas de una empresa conocida.

**22 · Definiciones**
Las dos citas —Bottcher 2018 y CNCF— una sobre otra, con las tres palabras resaltadas: *self-service*, *product*, *needs of the users*.

**23 · El costo de depender**
El dato de Bottcher: entre 10 y 12 veces más lento cuando una tarea requiere a otro equipo. Número grande, fuente al pie.

**24 · Golden path**
Definición en una línea. Mención de Dune.
Debajo, en negrita: *es opcional; si es obligatorio, volviste a tener tickets*.
Visual: un camino pavimentado con senderos alternativos que siguen existiendo.

**24b · ★ Paved road**
La misma ilustración de la 24, ahora con un equipo saliéndose del camino.
Tres líneas: Netflix no obliga; salirse tiene costo, no castigo; **si muchos equipos se salen, el problema es el camino**.
Al pie, la fuente del blog de ingeniería de Netflix.

### Portal

**25 · ★ Platform ≠ Portal**
La slide más importante del bloque. Dos columnas con ejemplos concretos de cada lado y, en el medio, una flecha: el portal dispara, la plataforma ejecuta.

**26 · Portal sin plataforma**
Una línea sobre fondo contrastante: *un catálogo de vínculos rotos y formularios que no hacen nada*. Se usa para la pregunta al grupo.

**27 · Siete capacidades**
Diagrama: el catálogo en el centro, las otras seis alrededor. Se repite como mapa al pasar a Port.

**28 · Catálogo**
Grafo pequeño de ejemplo: servicio, equipo, entorno, repositorio, cliente.
Línea de cierre: *el valor está en las relaciones, no en la lista*.

**29 · Ingesta**
Tabla de tres filas: pull, webhook, API directa.
Debajo, en negrita: *todo dato que alguien tenga que cargar a mano queda desactualizado*.

**30 · Autoservicio**
Maqueta de un formulario de ocho campos y, al lado, la lista de lo que el pipeline hace con ellos.
Línea de cierre: *el formulario solo pregunta lo que la plataforma no puede averiguar*.

**31 · Scorecards**
Tres niveles apilados —bronce, plata, oro— con dos reglas de ejemplo en cada uno.

**31b · ★ Por qué no sí o no**
Dos servicios enfrentados, ambos con el mismo veredicto binario ❌: uno cumple 19 de 20 reglas, el otro 2 de 20.
Línea de cierre: *con un solo veredicto, los dos se ven igual — y no están ni cerca de la misma situación*.
Es la slide que explica qué significa "criterio binario", que de otro modo queda como una palabra suelta.

**31c · Tableros, permisos y automatizaciones**
Tres bloques en una slide. Tableros: tres columnas —equipo, líder, seguridad— con la pregunta de cada uno. Permisos: quién ve, quién ejecuta, quién cambia las reglas. Automatizaciones: disparador → condición → acción, con un ejemplo.
Con estudiantes sin experiencia laboral, abrir por la analogía del campus virtual antes de mostrar los tableros.
Línea de cierre de la parte de automatizaciones: *actuar, no solo avisar*.

**32 · Panorama de herramientas**
Tabla de ocho filas: Backstage, Port, Cortex, OpsLevel, Spotify Portal, Roadie, Humanitec, Kratix, con naturaleza, licencia y énfasis. Las dos últimas destacadas como *no son portales, van debajo*.
La columna de licencia con un color para open source y otro para privado, para que la proporción se lea de un vistazo. Los logos, todos al mismo tamaño.
Primera candidata a recortar si el reloj apremia.

**33 · ★ Cuándo tiene sentido**
Dos mitades. Arriba, las cinco señales que justifican un portal. Abajo, en negrita: *si cada servicio se despliega distinto, primero se estandariza un camino*.

**33b · ★ La evidencia en contra**
La cita de DORA 2024 arriba, verbatim y con su traducción.
Abajo, los tres mecanismos por los que una plataforma frena —capas de aprobación, entregas por lotes, estructuras rígidas— y una línea: *un punto único por el que pasa todo es el lugar más cómodo para poner controles*.

**33c · Autoservicio real o ticket con otra cara**
La prueba de cuatro preguntas, en dos columnas.
Línea de cierre: *lo que la evidencia castiga no es la aprobación, es la aprobación por defecto*.
Primera del par a recortar si el reloj apremia; la 33b no se recorta.

### Estandarización

> **Este bloque va antes que Port, y el orden es deliberado.** Primero se establece qué hay que lograr; recién después se muestra una herramienta que ayuda a lograrlo. Invertirlo convierte la clase en una demostración de producto.

**34 · ★ Qué significa estandarizar**
Una línea: *las decisiones que no diferencian al producto se toman una vez*.
Debajo, los seis niveles en una columna: nomenclatura, modelo de datos, procesos, estructura, propiedad, niveles.

**35 · ★ La nomenclatura**
Diagrama: un nombre en el centro, del que salen flechas al repositorio, al registro de imágenes, al servicio del clúster y a la ruta de la API.
Línea de cierre: *si todo deriva de un nombre, nada puede desincronizarse*.

**36 · Proceso cerrado**
Tabla de dos columnas: proceso abierto frente a proceso cerrado, con tres pares de ejemplos.
Debajo: *inicio, final y estado observable — el tercero es el que falta casi siempre*.

**37 · ★ La escalera**
Seis escalones dibujados: manual, documentado, automatizado, autoservicio, automático, agéntico.
Línea de cierre: *cada escalón necesita que el anterior esté estandarizado*.
Se vuelve a mostrar en la slide 42, con el último escalón resaltado.

### Port

> **Todas las slides de este bloque llevan captura real**, no maqueta. Las seis figuras están especificadas en la sección 7.7 del apunte y se toman en una sola sesión después del ensayo. Cada slide lleva al pie el enlace a la documentación oficial correspondiente, en tipografía chica.

**38 · Port**
Qué es, en dos líneas. Mención de que en 2026 se reposicionó alrededor del catálogo como contexto para agentes.
**Figura 7.1**: captura de la pantalla de inicio con el menú lateral visible.
Al pie: docs.port.io

**39 · ★ Features leídas como problemas**
La tabla problema → feature, con cinco filas visibles. No se leen todas: se desarrollan cuatro.
Sin captura: esta slide es conceptual y la imagen competiría con el texto.

**40 · Tres primitivas**
Blueprint, entidad, relación, con la analogía de clase, objeto y clave foránea.
**Figura 7.2**: el grafo del modelo de datos de la organización de demostración, al lado de la tabla.
Al pie: docs.port.io/context-lake/data-model

**41 · Mirror property**
Diagrama propio: servicio → proyecto → cliente, con la flecha del valor viajando en sentido inverso.
**Figura 7.3**: la página de un servicio con las propiedades mirror señaladas, debajo del diagrama.
Al pie: docs.port.io — mirror-property

**41b · Acción y scorecard, en el producto**
**Figura 7.4** arriba —formulario con una lista desplegable abierta, y la página de ejecución— y **Figura 7.5** abajo —la torta por nivel y las reglas incumplidas de un servicio—.
Es la antesala visual de la demostración: lo que van a ver en vivo, primero quieto.

### Era agéntica

**42 · La escalera, otra vez**
La misma figura de la slide 37, con el escalón 6 resaltado.
Línea: *acá estamos ahora, y este escalón necesita los cinco anteriores*.

**43 · Por qué un agente necesita contexto**
Cita de Port sobre agentes sin contexto, verbatim, con su traducción.
Debajo: *una empresa con la plataforma implícita no tiene nada que darle a un agente*.
Al pie, mención de que MCP está en la Agentic AI Foundation de la Linux Foundation, con el enlace.

**44 · ★ Guardrails, y una nota personal**
Arriba: una acción de autoservicio tiene esquema, permisos, backend fijo y traza — el mismo mecanismo que evita el ticket es el que acota al agente. Los logos de OWASP y NIST al pie, como señal de que hay cuerpos normativos y no solo blogs de proveedores.
Abajo, en un bloque visualmente separado y en primera persona: *no uso el dato del 95% porque no lo puedo verificar; lo que sostengo es que la estandarización que hace falta para automatizar es la misma que hace falta para los agentes*.

### Demostración

**45 · Apertura de demostración**
Título: *Un golden path funcionando*. Segunda y última aparición del logo de Craftech.
Cuatro ítems de lo que hay que mirar: modelo de datos, catálogo, acción de autoservicio, scorecard.
Advertencia para quien maqueta: después de esta slide se pasa al navegador. Prever una slide gemela de respaldo con el video incrustado.

### Cierre

**46 · Qué queda**
Los cinco objetivos de aprendizaje, reformulados como afirmaciones en primera persona.

**47 · Para seguir**
Cuatro recursos con códigos QR: el apunte, el white paper de CNCF, la demo pública de Backstage, la charla de 2009 de Allspaw y Hammond.
Al pie, el contacto del docente.

---

## 4. Criterios de maquetado

| Criterio | Regla |
|---|---|
| Texto | Máximo cinco líneas por slide. Ningún párrafo |
| Tipografía | Mínimo 24 pt para cuerpo. Las capturas se recortan antes que reducirse |
| Citas | Verbatim, en el idioma original, con fuente al pie. No se traducen en la slide |
| Capturas | Solo de la organización de demostración, recortadas al área relevante, sin barra de navegador ni pestañas visibles |
| Diagramas | Construidos, no capturados de otras presentaciones |
| Animación | Solo revelado progresivo en las slides 13, 15, 22 y 37. Ninguna transición entre slides |
| Transición de bloque | Reaparece la slide 2 con el paso actual resaltado |
| Numeración | Visible en todas menos la portada |

---

## 5. Pendientes

| # | Falta | Bloquea |
|---|---|---|
| 1 | Plantilla, paleta, tipografía y logo vectorial de DiploDevops | La construcción del archivo final |
| 2 | Formato de entrega esperado por el programa | La elección de herramienta |
| 3 | Nombre del docente para portada y cierre | Slides 1 y 47 |
| 7 | Temario de los módulos anteriores de la diplomatura | La slide 20b: sin él, los temas quedan genéricos en lugar de nombrar las clases que el grupo cursó |
| 8 | Confirmación de qué nube se usó en los módulos previos | Qué variante del diagrama oficial mostrar en la slide 20 |
| 4 | Las seis capturas de la organización de demostración, tomadas tras el ensayo (especificadas en la sección 7.7 del apunte) | Slides 38, 40, 41 y 41b |
| 5 | Video de respaldo de la demostración, grabado | Slide gemela de la 45 |
| 6 | Confirmación de si la clase es de 90 o 120 minutos | El recorte de los bloques 3 y 5 |
