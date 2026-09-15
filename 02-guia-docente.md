# Guía del docente — De DevOps a Platform Engineering

**Preparado por:** Craftech (docente invitado)
**Programa:** DiploDevops — módulo Platform Engineering
**Duración:** 90 minutos — 60 de teoría, 26 de demostración, 4 de cierre
**Audiencia:** estudiantes sin experiencia laboral previa
**Material del alumno:** [`01-apunte-teorico.md`](01-apunte-teorico.md)
**Slides:** [`03-propuesta-slides.md`](03-propuesta-slides.md)
**Fecha:** 2026-09-14
**Estado:** borrador — pendiente confirmar branding de DiploDevops y ensayo completo

---

## 1. Advertencia sobre el alcance

El arco completo —DevOps, sus límites, Platform Engineering, disciplinas, plataforma, portal, Port, estandarización, era agéntica— **no entra en 60 minutos a la profundidad con la que está escrito el apunte**. Entra a la profundidad de esta guía, que es la versión dictada.

Tres opciones, en orden de preferencia:

| Opción | Cómo queda |
|---|---|
| **Dos encuentros de 90 min** | Encuentro 1: bloques 1 a 4 más demostración del catálogo. Encuentro 2: Port, estandarización, era agéntica, demostración completa. Es la que hace justicia al material |
| **Un encuentro de 120 min** | 85 de teoría, 30 de demostración, 5 de cierre. Entra el arco completo sin apretar |
| **Un encuentro de 90 min** | Lo que describe esta guía. Se dicta el arco entero, con profundidad recortada en los bloques 3 y 5 |

Esta guía desarrolla la tercera. El apunte cubre lo que se recorta y está marcado 📖 en las secciones que se leen y no se dictan.

---

## 2. Objetivos de aprendizaje

| # | Objetivo | Se verifica con |
|---|---|---|
| O1 | Explicar qué resolvió DevOps y qué problema nuevo produjo | Pregunta de apertura del bloque 2 |
| O2 | Distinguir Internal Developer Platform de Internal Developer Portal | Pregunta directa en el bloque 4 |
| O3 | Reconocer la plataforma implícita de una organización y mapearla a los cinco planos | Ejercicio de la sección 6.2 |
| O4 | Argumentar cuándo un portal tiene sentido y cuándo conviene estandarizar primero | Pregunta de cierre |
| O5 | Explicar por qué la estandarización es prerrequisito de la automatización y de la operación con agentes | Bloque 5, la escalera de seis escalones |

Lo que la clase **no** persigue: que sepan configurar Port. Es una clase de conceptos con una herramienta como ejemplo, no un taller de producto.

---

## 3. Estructura y tiempos

| Bloque | Tema | Minutos | Acumulado | Apunte |
|---|---|---|---|---|
| B0 | Apertura | 3 | 3 | — |
| B1 | DevOps: qué resolvió | 8 | 11 | 1 |
| B2 | Por qué aparece Platform Engineering | 9 | 20 | 2 |
| B3 | Plataforma implícita | 10 | 30 | 4 |
| B4 | Portal | 11 | 41 | 5 y 9.2 |
| B5 | Estandarización | 9 | 50 | 6 |
| B6 | Port | 5 | 55 | 7 |
| B7 | Era agéntica | 5 | 60 | 8 |
| D | Demostración en vivo | 26 | 86 | — |
| C | Cierre y preguntas | 4 | 90 | — |

Las secciones 3, 4.4, 5.6, 6.4, 8.4, 9.1 y 9.3 del apunte no se dictan: están listadas como lectura en su guía de lectura. Si alguien pregunta por ellas, remitir ahí en lugar de improvisar.

**Puntos de control.** A los 20 minutos hay que estar entrando a B3. A los 41, a B5. Si se llega tarde, el recorte es en este orden: el panorama de herramientas de B4, la prueba de cuatro preguntas del cierre de B4, y el ejercicio de los cinco planos de B3. **B5 no se recorta**: es la tesis de la clase, y va antes que Port justamente para que no quede como apéndice de la herramienta.

---

## 4. Guion por bloque

### B0 · Apertura (3 min)

Presentarse, presentar a Craftech como consultora invitada, declarar el encuadre: se usa una herramienta comercial como ejemplo y no es una recomendación de compra.

Anunciar el recorrido en una frase, porque el arco es largo y conviene que sepan dónde están:

> "Vamos a ir de un problema de organización a una herramienta, en ese orden. Primero qué resolvió DevOps y qué rompió. Después por qué apareció Platform Engineering. Después una idea que a muchos clientes les cambia la conversación: que ya tienen una plataforma aunque no la llamen así. Después el portal, que es la interfaz de todo eso. Y antes de mostrarles ninguna herramienta, lo único que de verdad importa: el estándar. La herramienta viene al final, y a propósito."

### B1 · DevOps (8 min)

El muro: dos áreas con incentivos opuestos, y el ciclo de despliegues infrecuentes → grandes → riesgosos → infrecuentes. Con esta audiencia conviene dibujarlo como ciclo.

Los dos hechos de 2009: Velocity en junio, DevOpsDays en octubre. Vale contar que Debois vio la charla de Flickr por streaming porque no pudo viajar, y que de esa frustración salió la conferencia que le puso nombre al movimiento. Es anecdótico y se retiene.

Qué resolvió, con evidencia: las cuatro métricas de DORA y el hallazgo de que velocidad y estabilidad no se oponen. Nombrar que detrás hay un estudio de encuesta de más de una década, no una opinión.

Si sobran dos minutos —solo si sobran—, la **tipología de Westrum** es el mejor rendimiento por segundo de todo el bloque, y aterriza la parte cultural con algo medible:

> "Westrum estudió accidentes de aviación y errores médicos, y clasificó a las organizaciones por qué hacen con una mala noticia: la ocultan, la ignoran porque no corresponde al procedimiento, o la buscan. DORA midió que la tercera entrega software más rápido. Cómo tratás al que avisa que algo está mal predice tu velocidad de entrega."

Las 24 capacidades quedan en el apunte. Mencionar que están.

Cerrar con la ley de Conway y el antipatrón del equipo DevOps:

> "Si en una empresa hay un 'equipo DevOps' al que se le pide el despliegue, el muro volvió. Cambió de lugar y de nombre."

Si hay tiempo, agregar el criterio de diagnóstico, que es lo que se van a llevar aplicable:

> "¿Cómo distinguís un equipo de plataforma de un 'equipo DevOps'? Por el modo de interacción. Si le pedís cosas y las hace, es un silo. Si publica capacidades que consumís sin pedirle nada, es plataforma. El nombre no decide nada."

**Riesgo del bloque:** irse por la historia. Ocho minutos, no doce. La historia es el encuadre, no el tema. El anexo del apunte tiene el relato completo de 2009 y el resumen de la entrevista a Vogels; si alguien pregunta por el detalle, remitir ahí en lugar de contarlo en clase.

### B2 · Por qué aparece Platform Engineering (9 min)

Empezar por lo que cambió debajo: la línea de tiempo de cloud, Docker, Kubernetes, IaC, microservicios. No explicar cada tecnología —las conocen o las verán en otros módulos—; el punto es acumulativo.

> "Cada una de estas resolvió un problema real. Sumadas produjeron uno que ninguna buscaba: la cantidad de cosas que hay que saber para poner un servicio en producción creció más rápido que la capacidad de una persona para saberlas."

Mostrar la tabla de las ocho dimensiones de decisión. **Contarla, no leerla**: nombrar tres o cuatro filas y dejar que la densidad haga el trabajo.

Carga cognitiva, con los tres tipos. Analogía para esta audiencia:

> "Rendir un final en un aula que no conocen, con una calculadora que no es la suya. La materia es la carga intrínseca. Buscar el aula y pelearse con la calculadora es la extrínseca. Pensar el problema del examen es la germane. La plataforma existe para que nadie pierda tiempo buscando el aula."

Nombrar el antipatrón de operaciones en la sombra: la tarea no desapareció, se concentró informalmente en dos o tres personas que además tienen otro trabajo.

Cerrar con la definición y con la aclaración que evita el malentendido más común:

> "Platform Engineering no reemplaza a DevOps. Es una forma de organizar el trabajo que DevOps hizo necesario."

**Riesgo del bloque:** estudiantes sin experiencia laboral no tienen el dolor que esto resuelve. Anclarlo en algo propio: un trabajo práctico grupal donde cada integrante armó su entorno a su manera y nada funcionaba igual en dos máquinas.

### B3 · Plataforma (10 min)

**Es el bloque que más cambia la cabeza de alguien que después va a trabajar con clientes.** Abrir con la afirmación, sin rodeo:

> "Si una empresa despliega software a producción, ya tiene una plataforma. La pregunta no es si la tiene. Es si es explícita o implícita."

Desarrollar la lista: tiene repositorios, tiene una forma de construir el artefacto, tiene algún mecanismo de despliegue, tiene infraestructura, tiene alguna forma de saber si funciona, tiene credenciales guardadas en algún lado, tiene reglas sobre quién toca producción.

Los cinco planos, como mapa para reconocerla. Mostrar el diagrama oficial de la arquitectura de referencia —el mismo que van a encontrar cuando busquen el tema— y recién después la capa con los temas de los módulos anteriores encima:

> "Fíjense dónde cae todo lo que vienen cursando. Git y el flujo de ramas son el plano 1: es la interfaz real de la mayoría de los cambios, mucho antes que cualquier portal. Contenedores y CI/CD, el plano 2. Kubernetes y las redes, el 3. Observabilidad, el 4. IAM y secretos, el 5. No aprendieron herramientas sueltas: vienen aprendiendo una plataforma por partes, sin que nadie se las haya presentado junta."

Esa frase es el objetivo del bloque. Un estudiante sin experiencia laboral no tiene con qué ordenar lo que cursó; el mapa se lo da.

Proponer después el ejercicio en voz alta sobre una empresa que conozcan.

Contrastar implícita frente a explícita con la tabla. La fila que más impacta con esta audiencia:

> "Qué pasa si se va una persona. En una plataforma implícita, se pierde capacidad. En una explícita, se pierde una persona."

Definiciones formales de Bottcher y CNCF, y el dato de Bottcher sobre el costo de depender de otro equipo: tareas entre 10 y 12 veces más lentas. Es el argumento económico del autoservicio.

Golden path al final del bloque, con la mención de Dune —ancla el término y dura veinte segundos— y con la propiedad que no se puede perder:

> "Es opcional. Si el camino es obligatorio, volviste a tener tickets, con mejor tipografía."

Rematar con el modelo de Netflix, que es el que hace entender por qué la opcionalidad no es blandura:

> "Netflix le dice camino pavimentado. Podés cruzar el campo por afuera, pero el asfalto es más rápido. No te obligan: se ocupan de que usarlo sea mejor que no usarlo. Y si un equipo se sale, se banca mantener lo suyo. Lo interesante es lo que eso permite medir: si muchos equipos se salen del camino, el problema no son los equipos. Es el camino. En una empresa que te obliga, esa señal no existe: todos cumplen y nadie sabe si lo que construyó sirve."

📖 Las disciplinas que engloba la práctica y la diferencia con SRE quedan en el apunte. Mencionar que están ahí.

### B4 · Portal (11 min)

La distinción **platform / portal** es el objetivo O2 y es lo que más se confunde. Detenerse y preguntar:

> "Si mañana instalan un portal en una empresa que no tiene pipelines ni infraestructura como código, ¿qué obtienen?"

Respuesta esperada: un catálogo de vínculos rotos y formularios que no hacen nada.

Las siete capacidades, alrededor de un minuto cada una. Priorizar catálogo, ingesta, autoservicio y scorecards.

De las tres restantes, la que más rinde con esta audiencia es **tableros por audiencia**, porque es la que no pueden imaginar sin haber trabajado. Entrar por la analogía antes que por la definición:

> "Piensen en el campus virtual de la facultad. Los datos son los mismos: alumnos, materias, notas. Pero la pantalla del alumno muestra sus materias, la del docente muestra el curso completo y quién está por debajo, y la de secretaría muestra tasas de aprobación por carrera. A nadie se le ocurriría darles la misma pantalla con un filtro. En una empresa pasa igual: el tablero de un equipo, el de un líder y el de seguridad responden preguntas distintas, con otro grano y otro horizonte."

De permisos, decir la tercera pregunta, que es la que se olvida: además de quién ve y quién ejecuta, **quién puede cambiar las reglas**. De automatizaciones, una sola idea: *actuar, no solo avisar* — la que crea el ticket y lo asigna vale mucho más que la que manda un mensaje.

Dos reglas que conviene decir textuales porque reaparecen en la demostración:

> "Todo dato que alguien tenga que cargar a mano queda desactualizado."

> "El formulario solo pregunta lo que la plataforma no puede averiguar."

El panorama de herramientas: Backstage, Port, Cortex, OpsLevel, y la aclaración de que Humanitec y Kratix **no son portales** sino que viven debajo. Este es el primer candidato a recortar si el reloj apremia.

Cuándo tiene sentido: las cinco señales. Y el reverso, que es lo que diferencia una clase de una presentación de producto:

> "Si cada servicio se despliega distinto, si no hay convención de nombres, si la infraestructura se crea a mano, el portal va a reflejar ese desorden con mejor diseño. Primero se estandariza un camino, después se le pone interfaz."

**Cerrar el bloque con la evidencia en contra.** Son noventa segundos y es lo que separa una clase universitaria de una charla de producto. Dar el hallazgo de DORA 2024 sin suavizarlo, y después el mecanismo:

> "El mejor estudio disponible dice que una plataforma interna mejora la productividad individual y el desempeño del equipo, y que **al mismo tiempo** puede bajar la estabilidad de los cambios y el ritmo de entrega. Suena contradictorio hasta que mirás cómo pasa: si todos los despliegues pasan por la plataforma, la plataforma se vuelve el lugar más cómodo para poner controles. Cada control agrega espera, la espera agranda el lote, y volvimos al ciclo del principio de la clase."

Y la condición que DORA subraya, con la prueba de cuatro preguntas si hay tiempo —qué pasa cuando aprieto el botón, cuánto tardo en saber el resultado, necesito saber a quién le llega, puedo reintentar solo—:

> "La condición es lo que DORA llama independencia de quien desarrolla. Autoservicio de verdad, no un formulario que abre un ticket. Y va con lo que vimos de Netflix: lo que empeoró en esas organizaciones no fue tener plataforma, fue volverla obligatoria antes de hacerla mejor que la alternativa."

Si el reloj apremia, esto se recorta a la cita de DORA sola. No se elimina.

### B5 · Estandarización (9 min)

Es la tesis. No se recorta y no se apura.

Qué significa estandarizar: no que todos usen el mismo lenguaje, sino que **las decisiones que no diferencian al producto se toman una vez**. Los seis niveles, nombrados rápido.

Detenerse en la nomenclatura, porque es el ejemplo concreto que la demostración va a mostrar:

> "Si el nombre del servicio deriva el repositorio, el registro de imágenes, el servicio del clúster y la ruta de la API, entonces nada puede desincronizarse. No hay un segundo lugar donde alguien lo escriba mal. Y al revés: agarrás cualquier recurso en la nube y sabés a qué servicio pertenece sin preguntarle a nadie."

Proceso cerrado: inicio, final y **estado observable**. El tercero es el que falta casi siempre.

La escalera de seis escalones, en pantalla, con la regla:

> "Cada escalón necesita que el anterior esté estandarizado. No se puede automatizar un proceso cuyos pasos cambian según quién lo ejecute. Y no se le puede delegar a un agente una decisión sobre un sistema cuyo estado nadie puede consultar de forma estructurada."

Cerrar el bloque anunciando los dos que siguen:

> "Esto es lo que hay que lograr. Ahora vemos una herramienta que ayuda a lograrlo, y después el escalón que viene después de automatizar."

### B6 · Port (5 min)

Ahora que el estándar está planteado, Port se lee como una herramienta para sostenerlo, no como un catálogo de funcionalidades. **No recorrer la lista de features.** Mostrar la tabla de problema → feature y desarrollar cuatro filas: blueprints definidos por el usuario, mirror properties, inputs de tipo entidad, scorecards por niveles.

Las tres primitivas —blueprint, entidad, relación— con la analogía de clase, objeto y clave foránea. Si el grupo cursó bases de datos, cierra sola.

Las mirror properties merecen dos minutos porque son el mecanismo detrás de lo que la demostración va a mostrar.

Todas las slides de este bloque llevan captura real de la organización de demostración. Mostrar el producto quieto antes de mostrarlo en movimiento baja el riesgo de la demo: si algo falla en vivo, el grupo ya vio de qué se está hablando.

**Precaución factual:** la nomenclatura de Port cambió durante 2026 —el catálogo hoy se llama Context Lake—. No afirmar features, límites ni precios de memoria; verificar contra docs.port.io antes de la clase. Los enlaces a la documentación que lleva el apunte conviene revisarlos antes de cada dictado: una reorganización de la doc los rompe sin aviso.

### B7 · Era agéntica (5 min)

Es el escalón 6 de la escalera de B5, ahora del otro lado de Port. Retomarla en pantalla antes de empezar, para que no se lea como un tema nuevo. El argumento es el mismo, un escalón más arriba:

> "Un modelo puede escribir código. Lo que no puede es saber qué servicios existen en la empresa, quién los opera, cuál depende de cuál y cuál está en producción ahora. Eso no está en el modelo: está en los sistemas de la organización, o en la cabeza de la gente. Una empresa con la plataforma implícita no tiene nada que darle a un agente."

Los guardrails, con la observación que cierra el círculo de la clase:

> "Una acción de autoservicio tiene un esquema validado, permisos, un backend fijo y una traza. Darle eso a un agente no es lo mismo que darle una credencial de administrador. El mecanismo que se construyó para que una persona no tuviera que abrir un ticket resulta ser el mecanismo para que un agente no pueda hacer cualquier cosa."

**Cerrar con escepticismo, no con entusiasmo.** Esto es lo que separa una clase universitaria de una charla de producto:

> "El dato del 95% de pilotos de IA fracasados circula mucho y lo cita el blog de un proveedor que vende la solución al problema que describe. Antes de repetirlo, lean el reporte. El argumento sólido es más modesto: la estandarización que hace falta para automatizar es la misma que hace falta para incorporar agentes. Una organización que la tiene está mejor parada, haga o no haga IA."

### D · Demostración (26 min)

Ver la sección 5.

### C · Cierre (4 min)

Volver a los objetivos. Dejar una pregunta abierta:

> "Si mañana entran a una empresa que no tiene nada de esto, ¿por dónde empiezan: por el catálogo o por el golden path?"

No hay respuesta única, y decirlo es parte de la respuesta. El argumento por el catálogo es que sin inventario no se sabe qué automatizar; el argumento por el golden path es que un catálogo sin automatización no cambia el comportamiento de nadie. En la práctica se hacen en paralelo, con un catálogo mínimo y un solo camino.

---

## 5. La demostración

### 5.1 Qué se muestra

La organización **Craftech-Demo**: una organización de Port aislada, con datos ficticios, que despliega infraestructura real en una cuenta AWS de laboratorio.

**No se muestra el portal interno productivo de Craftech.** Contiene datos de clientes reales —contratos, proyectos, personas—. Fuera de alcance para esta clase.

Los cuatro conceptos que la demostración tiene que dejar, en este orden: **modelo de datos, catálogo, acciones de autoservicio, scorecards.**

### 5.2 Los cuatro conceptos que la demostración tiene que dejar

Antes de abrir el navegador, decir en voz alta qué hay que mirar. Sin eso, el grupo mira la pantalla y no el argumento.

| # | Qué mirar | Concepto que ilustra |
|---|---|---|
| 1 | **Modelo de datos** — cliente, proyecto, servicio, squad, entorno, cuenta, repositorio, recursos | Sección 7.3 del apunte. El catálogo modela el negocio, no solo la infraestructura |
| 2 | **Catálogo y trazabilidad** — subir de un servicio hasta el cliente siguiendo relaciones | Sección 7.3, mirror properties. El dato se escribe una vez |
| 3 | **Acción de autoservicio** — un formulario de ocho campos, seis minutos, un servicio respondiendo | Secciones 5.2 y 6.3. Proceso cerrado con estado observable |
| 4 | **Scorecard** — doce reglas en tres niveles sobre siete servicios | Secciones 5.2 y 6.1. El estándar como dato, no como documento |

El argumento está en la correlación: **los servicios creados desde el portal llegan al nivel más alto; los heredados no.** No porque el portal sea mágico, sino porque el camino que los creó tenía el estándar incorporado.

El nivel oro merece atención especial: sus cuatro reglas no son casillas que un pipeline marcó. Detrás de cada una hay un artefacto que se puede abrir —un `RUNBOOK.md`, una alarma real en la nube, un `slo.yaml` cuyo número esa alarma hace cumplir, un contacto heredado del equipo dueño—. Si alguien pide verlo, abrirlo: es el servicio que sobrevive a la inspección.

### 5.3 Secuencia

| # | Momento | Min | Concepto que ancla |
|---|---|---|---|
| 1 | Tablero y scorecard | 4 | El estándar como dato |
| 2 | Modelo de datos y trazabilidad | 5 | Blueprints, relaciones, mirror properties |
| 3 | Creación en vivo | 11 | Acción de autoservicio, proceso cerrado |
| 4 | Vuelta al scorecard | 3 | Estandarización: por qué el nuevo llega a oro |
| 5 | Preguntas | 3 | — |

### 5.4 Guion, momento por momento

**Momento 1 — Tablero.** Abrir el tablero Golden Path. Señalar la distribución del scorecard antes de explicar nada.

> "Siete servicios, todos medidos contra el mismo estándar. Dos llegan a oro. La división no es casual: los dos de oro nacieron del portal, los cinco importados se quedan cortos."

Abrir el peor puntuado: sin descripción, sin repositorio vinculado, marcado obsoleto, corriendo en producción.

> "Nadie ocultó esto. El catálogo lo muestra. Esa es la primera mitad del valor de un catálogo: hace visible lo que antes solo sabía quien estaba hace años en la empresa."

**Momento 2 — Modelo de datos.** Mostrar el grafo: cliente, proyecto, servicio, squad, entorno, cuenta, repositorio, recursos. Después abrir un servicio y subir por las relaciones hasta el cliente.

> "Ninguno de estos datos se cargó a mano acá. El nombre del cliente vive en la entidad cliente y se lee desde el servicio siguiendo dos relaciones. Eso es una mirror property, y por eso no pueden discrepar."

Señalar lo que un catálogo puramente técnico no responde: a qué cliente pertenece este servicio. Conecta con B5 de forma directa.

**Momento 3 — Creación en vivo.** Self-Service → Create Service. Llenar el formulario con el grupo mirando.

Valores sugeridos: nombre `payments-api` —o uno distinto si ya se usó en un ensayo—, tipo `docker-backend`, criticidad `tier-2`, y las entidades de proyecto, squad, entorno y cuenta de las listas desplegables.

Al llegar a la cuenta cloud:

> "Esta lista sale del catálogo, no está escrita en el pipeline. Si mañana se agrega una cuenta al catálogo, aparece acá sin que nadie toque un workflow. Eso es lo que decía antes: el formulario solo pregunta lo que la plataforma no puede averiguar."

Presionar. Quedarse en la página de ejecución de Port, que reporta los pasos. Cuando informe el repositorio, cambiar a GitHub Actions y mostrar las etapas avanzando por nombre.

**Los dos minutos y medio de Terraform son el mejor momento de la clase.** Ahí va el argumento de B6, con la pantalla mostrando el pipeline:

> "Nadie abrió un ticket. Nadie eligió una convención de nombres. El repositorio, el registro de imágenes, el servicio del clúster y la ruta de la API toman su nombre del servicio, así que ninguno puede desincronizarse de los otros. Y fíjense en la entidad del catálogo: existe desde antes que la infraestructura, y va cambiando de estado. Si esto fallara ahora, quedaría marcada como fallida, no como si siguiera construyendo. Eso es un proceso cerrado."

Cuando el pipeline verifique que el servicio responde, abrir la URL.

**Momento 4 — Scorecard.** Volver al tablero. El servicio nuevo aparece en oro.

> "Doce de doce, y no porque un pipeline haya marcado casillas. Hay un runbook en el repositorio, una alarma que hace cumplir el objetivo de disponibilidad que el propio servicio declara en su archivo de SLO, y un contacto de guardia heredado del equipo dueño. Comparen con los cinco de abajo, que alguien construyó antes de que nada de esto existiera. La diferencia no es el portal: es que el camino que creó a este tenía el estándar adentro."

Ese contraste —importado contra creado acá— es la tesis. No recortarlo para ganar un minuto.

---

## 6. Preparación

### 6.1 Checklist previo

| Cuándo | Tarea |
|---|---|
| La noche anterior | Verificar que la infraestructura de laboratorio esté levantada. Una limpieza automática vacía la cuenta cada madrugada; si la clase es después de medianoche hay que reconstruirla |
| 24 h antes | Ensayo completo de la demostración, de punta a punta |
| 24 h antes | Grabar el video de respaldo, con la creación completa |
| 24 h antes | Verificar contra docs.port.io que la nomenclatura usada en las slides sigue vigente |
| 15 min antes | Desplegar la configuración de Port y abrir el tablero. Confirmar que el catálogo tiene solo las entidades de demostración |
| 15 min antes | Abrir las tres pestañas: tablero de Port, GitHub Actions del repositorio de infraestructura, terminal |
| 15 min antes | Compartir pantalla de prueba y verificar ancho de banda de la sede |

El runbook operativo completo —comandos de reconstrucción, verificación y limpieza— vive en el repositorio interno de la demostración, en Craftech. Esta guía no lo duplica.

### 6.2 Ejercicio para los alumnos

Cubre O3 y O4, y sirve tanto como consigna entre clases como trabajo en el aula si el formato lo permite.

> Elegir una organización —la propia, la de un trabajo práctico, una empresa conocida— y completar la tabla de los cinco planos con sus herramientas actuales. Después responder dos preguntas: qué plano está vacío, y si esa organización necesita un portal o necesita estandarizar un camino primero. Una carilla.

Criterio de corrección: no se evalúa la cantidad de herramientas nombradas, sino si la conclusión se sostiene sobre lo que la tabla muestra.

---

## 7. Riesgos

| Riesgo | Probabilidad | Mitigación |
|---|---|---|
| El bloque teórico se estira y come la demostración | **Alta** | Puntos de control a los 21 y 43 minutos. Recortar en el orden indicado. Nunca B6 |
| Falla la demostración en vivo: red, incidente de GitHub Actions, error de Terraform | Media | Video de respaldo grabado. No depurar en vivo: pasar al servicio ya creado por esta misma vía y recorrer su infraestructura |
| La cuenta de laboratorio amaneció vacía por la limpieza automática | Media | Reconstrucción la noche anterior, verificada |
| El nombre del servicio ya existe de un ensayo | Alta | Tener dos o tres nombres alternativos decididos de antemano |
| Preguntas de precios de Port | Alta | No responder de memoria. Remitir a la página de precios y ofrecer seguimiento |
| La clase se lee como venta de Craftech o de Port | Media | El panorama de herramientas y la evidencia de DORA en B4, y la nota personal del cierre de B7, son el contrapeso. Ninguno de los tres se elimina |
| La sección de IA suena a entusiasmo de proveedor | Media | Dictar B6 en el orden escrito: primero la escalera, después los agentes, y cerrar con la advertencia sobre el dato del 95% |

---

## 8. Preguntas frecuentes previstas

| Pregunta | Respuesta breve |
|---|---|
| ¿Platform Engineering reemplaza a DevOps? | No. Es una forma de organizar el trabajo que DevOps hizo necesario. Los objetivos de DevOps siguen vigentes |
| ¿Entonces "equipo DevOps" está mal? | Si es un equipo al que se le piden despliegues, sí: es el muro otra vez. Si construye capacidades que otros consumen sin coordinar, es un equipo de plataforma |
| ¿Hace falta ser una empresa grande? | El portal se justifica cuando hay más servicios de los que una persona puede recordar. Debajo de eso, el costo supera al beneficio |
| ¿Por qué no Backstage, que es gratis? | La licencia es gratis, el equipo que lo mantiene no. Es una decisión de asignación de personas |
| ¿Quién carga los datos del catálogo? | Casi nadie. Se pueblan por integración. A mano solo lo que no existe en ningún sistema: criticidad, contacto de guardia, objetivo de disponibilidad |
| ¿Qué pasa si el portal se cae? | Nada se detiene: la plataforma sigue funcionando. Se pierde la interfaz y la visibilidad, no la capacidad de desplegar |
| ¿La IA no va a reemplazar todo esto? | Al revés: un agente necesita exactamente el contexto estructurado que esto produce. Sin catálogo y sin acciones acotadas, un agente es más riesgo que ayuda |
| ¿Esto sirve en una empresa de 10 personas? | La estandarización sí, desde el primer día y sin herramienta. El portal no |

---

## 9. Libros, reportes y prácticas nombradas en clase

Se nombran en voz alta. Nombrar algo sin explicarlo, frente a estudiantes sin experiencia laboral, es dejar una etiqueta vacía. Cada ítem necesita una línea al pasar, no un paréntesis de dos minutos.

### Libros y reportes

| Obra | Qué es | Cómo presentarlo en clase |
|---|---|---|
| ***Accelerate*** (Forsgren, Humble y Kim, 2018) | El libro que publica los resultados del programa DORA: cuatro métricas de entrega, 24 capacidades que predicen desempeño, y la metodología estadística detrás | "Es el libro donde DevOps deja de ser opinión. Cuatro años de encuestas y análisis estadístico para responder qué prácticas se correlacionan con entregar mejor" |
| ***The Phoenix Project*** (Kim, Behr y Spafford, 2013) | Novela de negocios: una empresa al borde del desastre reorganiza su área de tecnología. Divulgó las ideas de DevOps antes que cualquier manual | "Es una novela. Se lee en un fin de semana y es la forma más rápida de entender el problema organizacional, porque lo cuenta como historia en lugar de como método" |
| ***The DevOps Handbook*** (Kim, Humble, Debois y Willis, 2016) | La sistematización práctica: los "tres caminos" —flujo, retroalimentación, aprendizaje continuo— y las prácticas concretas de cada uno | "Es el manual de lo que la novela cuenta como relato" |
| ***Team Topologies*** (Skelton y Pais, 2019) | El vocabulario organizacional de la disciplina: cuatro tipos de equipo, tres modos de interacción, carga cognitiva, Thinnest Viable Platform | "Es el libro que explica por qué un equipo de plataforma es distinto de un equipo DevOps, y da el vocabulario para discutirlo" |
| ***Site Reliability Engineering*** (Google, 2016) | Cómo Google opera sus sistemas: SLI, SLO, presupuesto de error, guardias, postmortems sin culpables. **Texto completo gratuito** en sre.google/books | "Está entero y gratis en internet. Si les interesa confiabilidad, es la referencia" |
| **CNCF Platforms White Paper** (2023) | Documento de la Cloud Native Computing Foundation: define plataforma, enumera siete atributos y trece dominios de capacidades | "Es la definición neutral, de una fundación y no de un proveedor. Cuando alguien les venda una plataforma, contrástenla con esto" |
| **State of DevOps Report** | Reporte anual. El de DORA/Google es el de referencia; el de Puppet lo publica un proveedor | "Salen todos los años. Conviene mirar quién lo publica antes de citar un número" |

### Prácticas nombradas

| Práctica | Explicación de una línea |
|---|---|
| **CALMS** | Acrónimo divulgado de DevOps: cultura, automatización, lean, medición, compartir. Es un recordatorio, no un método |
| **Los tres caminos** | Flujo de izquierda a derecha, retroalimentación de derecha a izquierda, y aprendizaje continuo sobre ambos |
| **You build it, you run it** | Quien construye un servicio responde por él en producción, guardias incluidas |
| **Two-pizza team** | Regla informal de Amazon: un equipo no debe superar lo que dos pizzas alimentan. Unas seis a diez personas |
| **Feature flag** | Interruptor en el código que permite desplegar algo apagado y encenderlo después. Separa desplegar de liberar |
| **Postmortem sin culpables** | Análisis de un incidente orientado a entender el sistema, no a encontrar responsables |
| **ChatOps** | Operar desde el canal de conversación del equipo, de modo que el registro de la charla sea también el de lo que se hizo |
| **Trunk-based development** | Todos integran a una rama principal con frecuencia alta, en lugar de sostener ramas largas |
| **IaC** | La infraestructura se describe en archivos versionados y se aplica por herramienta, no por consola |
| **GitOps** | El estado deseado del sistema vive en Git, y un agente reconcilia la realidad contra ese estado |
| **Maniobra Conway inversa** | Diseñar los equipos para obtener la arquitectura deseada, porque la estructura de comunicación la determina igual |
| **X-as-a-Service** | Modo de relación donde un equipo consume la capacidad de otro sin coordinar nada |
| **Shift left** | Mover responsabilidades hacia etapas tempranas: pruebas, seguridad, infraestructura, hacia el desarrollador |
| **Scaffolding** | Generar un proyecto nuevo desde una plantilla, con su estructura y su pipeline ya armados |
| **SLI / SLO / presupuesto de error** | Qué se mide, qué objetivo se declara, y cuánto incumplimiento se acepta antes de frenar los cambios |
| **Blast radius** | Cuánto se rompe si una operación sale mal. Criterio para decidir qué se automatiza y con qué permisos |

### Tecnologías de código abierto nombradas

Conviene nombrarlas cuando aparezca cada plano, para que no quede la impresión de que esto requiere software comercial.

| Plano | Qué nombrar |
|---|---|
| Control del desarrollador | Backstage, Score |
| Integración y entrega | Argo CD, Flux, Tekton, Crossplane, Kratix |
| Recursos | Kubernetes, OpenTofu |
| Monitoreo | Prometheus, Grafana, OpenTelemetry |
| Seguridad | Keycloak, OpenBao, Open Policy Agent |

El caso OpenTofu merece treinta segundos porque enseña algo que no es sobre licencias:

> "Terraform dejó de ser software libre en 2023 y la comunidad hizo un fork, OpenTofu, que hoy está en la Linux Foundation. Lo que importa para nosotros no es la licencia: es que en una plataforma bien diseñada cambiar una pieza es un trabajo acotado. Si cambiar la herramienta de aprovisionamiento implica reescribir todo lo que la rodea, eso no era una abstracción, era una dependencia."

---

## 10. Pronunciación

Nombres que aparecen en la clase y no se pronuncian según las reglas del español. Las aproximaciones están escritas con ortografía española y la sílaba tónica en mayúsculas; son aproximaciones, no transcripción fonética. **Esta tabla vive solo acá**: el apunte del alumno no la lleva.

| Nombre | Origen | Aproximación | Nota |
|---|---|---|---|
| Patrick **Debois** | Francés (es belga flamenco) | *pa-TRIK de-BUÁ* | El apellido es de origen francés: la *s* final no suena |
| **Gent** / Gante | Neerlandés | *JENT* | La *g* neerlandesa es gutural, como la *j* española. En español la ciudad es Gante |
| Werner **Vogels** | Neerlandés | *VÉR-ner FÓ-jels* | En neerlandés la *v* suena como *f* y la *g* es gutural |
| Kaspar von **Grünberg** | Alemán | *KÁS-par fon GRÜN-berk* | La *ü* alemana no existe en español: labios de *u*, lengua de *i* |
| **Jez** Humble | Inglés | *YEZ HÁM-bol* | Diminutivo de Jeremy |
| Nicole **Forsgren** | Inglés, apellido sueco | *FÓRS-gren* | — |
| Ron **Westrum** | Inglés | *UÉS-trum* | — |
| Evan **Bottcher** | Inglés, apellido alemán | *BÓT-cher* | — |
| Manuel **Pais** | Portugués | *ma-nu-ÉL PA-ish* | La *s* final portuguesa suena *sh* |
| Matthew **Skelton** | Inglés | *SKÉL-ton* | — |
| **Kubernetes** | Griego | *ku-ber-NÉ-tes* | Del griego κυβερνήτης, "timonel". En inglés se dice *ku-ber-NÉ-tis* |
| **Backstage** | Inglés | *BÁK-steich* | — |
| Zohar **Einy** | Hebreo | *zo-HAR ÉI-ni* | — |
| **Ocean** | Inglés | *Ó-shan* | Nombre del framework de integraciones de Port |

Los siete que más se dicen en voz alta: Debois, Gent, Vogels, von Grünberg, Jez Humble, Pais y Kubernetes.

Si no se está seguro de una pronunciación frente al grupo, decir el nombre y aclarar la duda vale más que inventarla. Lo que no sirve es evitar el nombre: los van a encontrar escritos cuando busquen.
