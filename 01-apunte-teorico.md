# De DevOps a Platform Engineering: plataformas, portales y estandarización

**Preparado por:** Craftech (docente invitado)
**Programa:** DiploDevops — módulo Platform Engineering
**Audiencia:** estudiantes sin experiencia laboral previa en equipos de ingeniería
**Formato:** clase de 90 minutos — teoría y demostración en vivo
**Fecha:** 2026-09-14
**Estado:** borrador para revisión del coordinador del programa

---

## Guía de lectura

Extensión completa: alrededor de 70 minutos de lectura. El apunte cubre más de lo que entra en una clase de 90 minutos.

| Perfil | Ruta | Tiempo |
|---|---|---|
| Antes de la clase | Secciones 1 y 2 | 20 min |
| Después de la clase | Completo | 70 min |
| Lectura mínima | 2.4, 4.1, 5.1 y 6 | 12 min |
| Docente | Completo, más [`02-guia-docente.md`](02-guia-docente.md) | 90 min |

Las secciones 1.1 y 1.2 incluyen el detalle de las dos fuentes fundacionales —la entrevista a Werner Vogels y la charla de Flickr— con todos sus conceptos explicados. Quien ya los conozca puede saltearlos sin perder el hilo.

El símbolo 📖 marca lecturas externas complementarias: libros, papers y documentos que amplían un punto y no hacen falta para seguir el apunte.

**Hilo conductor.** El recorrido va de un problema organizacional a una herramienta, en este orden: DevOps resolvió un muro entre áreas y creó uno nuevo, de carga cognitiva → Platform Engineering responde a ese segundo problema → toda empresa de tecnología ya tiene una plataforma, aunque no la nombre → un portal la vuelve visible y usable → lo que hace que todo eso funcione no es la herramienta sino el estándar → Port es un ejemplo de herramienta que ayuda a sostener ese estándar → una empresa estandarizada es la que puede automatizar y, hoy, la que puede incorporar agentes.

**Qué se dicta y qué se lee.** La clase recorre el mismo orden, con menos profundidad. Estas secciones no se dictan y viven solo en el apunte:

| Sección | Por qué queda para lectura |
|---|---|
| 3 · Disciplinas que engloba | Es un mapa de referencia, no un argumento |
| 4.4 · Atributos de una plataforma que funciona | La lista de CNCF se consulta, no se recorre en voz alta |
| 5.6 · Modos de falla | Se entiende mejor leída que escuchada |
| 6.4 · Dónde está el límite | Matiz sobre el bloque de estandarización |
| 8.4 · Qué tiene que ser cierto | Resumen de condiciones, útil como checklist |
| 9.1 y 9.3 · Adopción y medición | Datos de contexto; en clase se dicta solo la evidencia en contra, 9.2 |

---

# 1. DevOps

## 1.1 El muro

Hasta fines de los 2000, la organización típica de software tenía dos áreas con incentivos opuestos:

| Área | Se le pedía | Se la medía por |
|---|---|---|
| Desarrollo | Entregar funcionalidad nueva | Velocidad de cambio |
| Operaciones | Sostener el sistema en producción | Estabilidad, ausencia de incidentes |

Cada cambio amenazaba el objetivo de la otra área. El resultado fue un patrón conocido: desarrollo "tiraba el software por encima del muro" y operaciones lo recibía sin haber participado de ninguna decisión que lo hiciera operable. Los despliegues se agrupaban en ventanas mensuales o trimestrales, de noche, con equipos de guardia, porque cada uno era riesgoso. Y era riesgoso porque era infrecuente, lo que lo hacía grande, lo que lo volvía riesgoso.

Amazon había roto ese ciclo internamente. En una entrevista de 2006, Werner Vogels describió la regla:

> "You build it, you run it. This brings developers into contact with the day-to-day operation of their software. It also brings them into day-to-day contact with the customer."
> — [Werner Vogels, *A Conversation with Werner Vogels*, ACM Queue, 2006](https://queue.acm.org/detail.cfm?id=1142065)
>
> *"Quien lo construye, lo opera. Esto pone a quien desarrolla en contacto con la operación diaria de su software. También lo pone en contacto diario con el cliente."*

### Detalle de la entrevista

La frase viene de [*A Conversation with Werner Vogels*](https://queue.acm.org/detail.cfm?id=1142065), publicada en ACM Queue —la revista de la Association for Computing Machinery, la sociedad científica de computación— en mayo de 2006. El entrevistador es **Jim Gray**, investigador de Microsoft y Premio Turing 1998. El entrevistado, CTO de Amazon desde 2005. El tema declarado es cómo funciona el sitio de Amazon por dentro.

**Qué cuenta, en cuatro puntos.**

1. **El cambio arquitectónico.** Amazon pasó de un monolito de dos capas a una plataforma distribuida y descentralizada, orientada a servicios. Lo hizo alrededor de 2001-2005, antes de que existiera la palabra "microservicios", y sin literatura previa: tuvieron que inventar buena parte del camino.
2. **La regla operativa.** Los equipos que construyen un servicio lo operan. De ahí la frase que quedó: *you build it, you run it*.
3. **El efecto que reporta.** Según su propio relato, dar responsabilidad operativa a quien desarrolla mejoró la calidad del servicio "tanto desde el punto de vista del cliente como de la tecnología".
4. **El circuito con el cliente.** El argumento de Vogels no es solo técnico: quien atiende la guardia escucha al cliente, y esa retroalimentación directa es la que mejora el producto.

**Conceptos que aparecen en el texto.**

| Concepto | Qué significa |
|---|---|
| Monolito de dos capas | Aplicación única sobre una base de datos única. Todo el código se despliega junto; un cambio en cualquier parte obliga a desplegar el conjunto |
| SOA (*service-oriented architecture*) | Arquitectura donde el sistema se parte en servicios que se comunican por interfaces explícitas. Cada servicio se despliega, escala y falla por separado |
| Descentralización | Ningún componente central coordina a los demás. Es lo que permite que un equipo avance sin esperar a otro |
| Responsabilidad operacional | Que el equipo que escribe el código responda también por su comportamiento en producción: guardias, incidentes, capacidad, costo |
| Guardia (*on-call*) | Rotación por la cual una persona del equipo queda disponible fuera de horario para atender incidentes de sus propios servicios |
| Circuito de retroalimentación con el cliente | Que la información sobre cómo se usa y cómo falla el producto llegue a quien lo construye, sin intermediarios que la filtren |
| *Two-pizza team* | Regla informal de Amazon: un equipo no debe ser más grande de lo que dos pizzas alcanzan a alimentar. No aparece en esta entrevista, pero pertenece al mismo cuerpo de prácticas y suele citarse junto a ella |

**Por qué importa para lo que sigue.** Es el enunciado más claro de la premisa que DevOps adoptó tres años después. Y contiene, sin decirlo, el problema que Platform Engineering vino a resolver: *you build it, you run it* funciona si el desarrollador tiene una plataforma debajo. Amazon había construido la suya. La mayoría de las empresas adoptó la frase sin construir la plataforma, y el resultado fue la carga cognitiva de la sección 2.3.

## 1.2 Dos hechos de 2009

DevOps no nace de un paper ni de un producto. Nace de dos eventos en el mismo año.

| Fecha | Hecho |
|---|---|
| Junio 2009 | John Allspaw y Paul Hammond presentan *10+ Deploys per Day: Dev and Ops Cooperation at Flickr* en la conferencia Velocity de O'Reilly |
| Octubre 2009 | Patrick Debois organiza en Gante, Bélgica, la primera **DevOpsDays**. El término "DevOps" aparece ahí |

### Junio: la charla

Allspaw venía de operaciones y Hammond de desarrollo, y esa fue la mitad del efecto: dos personas de los dos lados del muro presentando juntas. La tesis de la charla es que la cooperación entre ambas áreas no se arregla con proceso, sino con dos cosas a la vez: herramientas y cultura. La prueba es una empresa desplegando más de diez veces por día, cuando la norma de la industria era mensual o trimestral.

La charla se organiza en dos listas, y son el primer inventario de lo que años después se llamaría una plataforma.

**Herramientas.**

| Herramienta | Qué es, y por qué está en la lista |
|---|---|
| Infraestructura automatizada | Los entornos se crean por código, no a mano. Es lo que hace que desarrollo y producción se parezcan |
| Control de versiones compartido | Desarrollo y operaciones trabajan sobre el mismo repositorio. No hay una "versión de ops" separada |
| Build de un paso | Un solo comando construye el artefacto. Si construir requiere una secuencia que alguien recuerda, no es reproducible |
| Deploy de un paso | Un solo comando despliega. El riesgo de un despliegue baja cuando deja de depender de la memoria de una persona |
| Registro de despliegues | Quién desplegó, qué y cuándo. Permite correlacionar un síntoma con el cambio que lo causó, que es el 80% de un diagnóstico |
| *Feature flags* | Interruptores en el código que permiten desplegar una funcionalidad apagada y encenderla después. Separan **desplegar** de **liberar**, y por eso permiten desplegar seguido sin exponer trabajo a medio hacer. Flickr tenía cientos |
| Métricas compartidas | Los mismos gráficos para desarrollo y operaciones, con marcas de los últimos despliegues sobre la línea de tiempo |
| Bots de IRC y mensajería | Notificaciones y comandos en el canal donde el equipo ya está conversando. Es el antecedente directo del *ChatOps* |

**Cultura.** Cuatro elementos, y son la mitad de la charla, no un apéndice.

| Elemento | Qué significa |
|---|---|
| **Respeto** | *"Respect the opinions of other people and the responsibilities of other people"* — "respetar las opiniones de las otras personas y las responsabilidades de las otras personas". No asumir que la contraparte no entiende, ni que sus prioridades son caprichos |
| **Confianza mutua** | Transparencia operativa como mecanismo concreto: dar a desarrollo acceso de solo lectura a los sistemas de producción, para que vea qué está pasando en lugar de preguntar |
| **Actitud sana frente al fallo** | *"Failure will happen. Think about what to do when failure happens"* — "el fallo va a ocurrir; pensar qué hacer cuando ocurra". El fallo se asume como propiedad del sistema, y el diseño se hace en función de cómo se responde |
| **Evitar la culpa** | *"Avoiding blame, rule of no finger-pointing"* — "evitar la culpa, regla de no señalar con el dedo". Primero se arregla, después se analiza. De aquí sale la práctica del **postmortem sin culpables** |

### Octubre: la conferencia

Patrick Debois, consultor belga que venía trabajando en la frontera entre desarrollo y operaciones, no pudo viajar a Velocity y vio la charla por streaming. De esa conversación —continuada en Twitter, con aliento de otras personas de la comunidad— salió la decisión de organizar su propio encuentro. La primera **DevOpsDays** abrió sus puertas en Gante, Bélgica, el 30 de octubre de 2009. El nombre se armó con las tres primeras letras de *development*, las de *operations* y la palabra *days*.

El relato más difundido agrega un detalle sobre el nombre: la etiqueta se acortó a **#devops** para que entrara cómoda en los 140 caracteres de Twitter, y fue esa versión corta —no el nombre de la conferencia— la que quedó como nombre del movimiento ([New Relic](https://blog.newrelic.com/engineering/devops-name/)).

### Conceptos de esta historia

| Concepto | Qué significa |
|---|---|
| Postmortem sin culpables | Análisis posterior a un incidente cuyo objetivo declarado es entender el sistema, no identificar responsables. Se asume que quien actuó lo hizo razonablemente con la información que tenía |
| ChatOps | Operar los sistemas desde el canal de conversación del equipo: los comandos y sus resultados quedan a la vista de todos, y el registro de la conversación es también el registro de lo que se hizo |
| Desplegar frente a liberar | Desplegar es poner el código en producción; liberar es exponerlo a los usuarios. Los feature flags permiten separarlos |
| Simulacro de fallo (*fire drill*) | Provocar una falla a propósito, en un momento elegido, para verificar que la respuesta funciona. Antecedente de la ingeniería del caos |
| Ventana de despliegue | Franja horaria acordada para desplegar, típicamente de madrugada. Es el síntoma de que cada despliegue es riesgoso; desaparece cuando dejan de serlo |
| Streaming | Que Debois haya visto la charla en vivo por internet, en 2009, es parte de la historia: el movimiento se formó por conversación pública distribuida |

### Advertencia sobre el relato

Quince años después, IT Revolution publicó una relectura del caso Flickr señalando que la historia se simplificó en la repetición: lo que Allspaw y Hammond mostraron fue una organización que aprendía, y la industria se quedó con la lista de herramientas ([IT Revolution](https://itrevolution.com/articles/organizational-learning-and-competitiveness-a-different-view-of-the-allspawhammond-10-deploys-per-day-at-flickr-story/)). Es el mismo error que esta clase señala sobre los portales: adoptar el artefacto sin la práctica que lo hacía funcionar.

Un último detalle, que explica el fenómeno: DevOps nunca tuvo una definición canónica ni un cuerpo normativo. Nació de una charla y una conferencia, no de un comité de estándares. Eso explica su difusión rápida y también su deriva posterior.

## 1.3 Qué proponía

Cuatro ideas, en el orden en que importan:

| Idea | Contenido |
|---|---|
| Responsabilidad compartida | Quien construye participa de operar. El muro desaparece porque desaparece la entrega entre áreas |
| Automatización | Todo paso manual y repetido se automatiza: build, prueba, despliegue, aprovisionamiento |
| Lotes pequeños y frecuentes | Desplegar seguido hace cada despliegue chico, y cada despliegue chico es menos riesgoso |
| Medición y retroalimentación | El sistema se instrumenta para que el equipo vea el efecto de sus cambios |

El acrónimo divulgado es CALMS —cultura, automatización, lean, medición, compartir—. La sistematización más citada es la de Gene Kim en *The Phoenix Project* (2013) y *The DevOps Handbook* (2016), con sus "tres caminos": flujo, retroalimentación y aprendizaje continuo.

## 1.4 Qué resolvió: la evidencia

Aquí DevOps deja de ser relato. El programa **DORA** —*DevOps Research and Assessment*, iniciado en 2014 por Nicole Forsgren, Jez Humble y Gene Kim, hoy alojado en Google Cloud— es un estudio de encuesta continuo sobre decenas de miles de profesionales de tecnología, en organizaciones de todo tamaño e industria. Sus resultados se publicaron primero en el libro *Accelerate* (2018) y desde entonces en el reporte anual *State of DevOps*.

### Cuatro métricas

Miden dos dimensiones que la industria creía opuestas:

| Dimensión | Métrica | Qué mide |
|---|---|---|
| Rendimiento | Frecuencia de despliegue | Cada cuánto se libera a producción |
| Rendimiento | Lead time para cambios | Tiempo desde el commit hasta producción |
| Estabilidad | Tasa de fallas de cambios | Porcentaje de despliegues que causan degradación |
| Estabilidad | Tiempo de restauración | Cuánto tarda el servicio en recuperarse |

**El hallazgo central: velocidad y estabilidad no se oponen.** Los equipos de mejor desempeño puntúan alto en las cuatro a la vez. Eso invalidó la premisa del muro —no hay que elegir entre entregar rápido y no romper nada— y le dio a DevOps una base empírica en lugar de una opinión ([DORA](https://dora.dev/)).

### Veinticuatro capacidades

*Accelerate* no se queda en medir. Identifica 24 prácticas que predicen alto desempeño, agrupadas en cinco categorías:

| Categoría | Cuántas | Ejemplos |
|---|---|---|
| Entrega continua | 8 | Control de versiones para todo, despliegue automatizado, integración continua, pruebas automatizadas, desarrollo basado en tronco, seguridad incorporada al pipeline |
| Arquitectura | 2 | Arquitectura desacoplada; equipos con potestad de elegir sus herramientas |
| Producto y proceso | 4 | Trabajo en lotes chicos, visibilidad del flujo, experimentación del equipo, retroalimentación del cliente |
| Gestión lean y monitoreo | 5 | Límites de trabajo en curso, monitoreo proactivo, aprobación de cambios liviana, visualización del trabajo |
| Cultura | 5 | Cultura generativa, aprendizaje continuo, colaboración entre equipos, satisfacción laboral, liderazgo transformacional |

Dos observaciones que importan para esta clase. La primera: *arquitectura desacoplada* y *equipos que eligen sus herramientas* son capacidades medidas, no preferencias de gusto — y son, exactamente, lo que una plataforma mal diseñada destruye. La segunda: cinco de las veinticuatro son culturales, y no son las menos predictivas.

### Tipología de Westrum

La capacidad cultural con más peso viene de fuera del software. Ron Westrum estudió factores humanos en seguridad de sistemas —aviación, salud— y clasificó las organizaciones por **cómo circula la información** dentro de ellas:

| Tipo | Orientación | Qué hace con una mala noticia |
|---|---|---|
| Patológica | Al poder | Se oculta. El mensajero se castiga |
| Burocrática | A las reglas | Se ignora si no corresponde al procedimiento |
| Generativa | Al desempeño | Se busca. El fallo es información |

DORA encontró que la cultura generativa **predice** el desempeño de entrega y el organizacional ([Westrum, *A typology of organisational cultures*, 2004](https://qualitysafety.bmj.com/content/13/suppl_2/ii22)). Dicho de otro modo: cómo trata una organización a quien reporta un problema es un predictor medible de su velocidad de entrega.

📖 El detalle de las veinticuatro capacidades y la metodología estadística están en *Accelerate* (Forsgren, Humble y Kim, 2018), capítulos 2 a 4. Las definiciones vigentes de las métricas, en [dora.dev](https://dora.dev/).

## 1.5 Ley de Conway y taxonomía de equipos

En 1968, Melvin Conway formuló lo que hoy se cita como su ley:

> "Organizations which design systems [...] are constrained to produce designs which are copies of the communication structures of these organizations."
> — [Melvin Conway, *How Do Committees Invent?*, 1968](https://www.melconway.com/Home/Committees_Paper.html)
>
> *"Las organizaciones que diseñan sistemas están obligadas a producir diseños que son copias de las estructuras de comunicación de esas organizaciones."*

La arquitectura de un sistema termina pareciéndose al organigrama de quien lo construye. El razonamiento de Conway es simple: dos módulos que tienen que hablar entre sí requieren que dos personas hablen entre sí. Si esas dos personas están en áreas que se comunican mal, la interfaz entre los módulos va a ser mala.

De ahí sale la **maniobra Conway inversa** (*reverse Conway maneuver*): si la estructura de comunicación determina la arquitectura, entonces para obtener la arquitectura deseada hay que diseñar primero los equipos. Es la premisa de *Team Topologies* (Skelton y Pais, 2019), el libro que le dio a esta disciplina su vocabulario organizacional.

### Cuatro tipos de equipo

| Tipo | Rol | Cuántos hay |
|---|---|---|
| **Stream-aligned** | Alineado a un flujo de valor: un producto, un segmento de cliente, un dominio. Es el equipo que entrega | La mayoría. Todos los demás existen para servirlo |
| **Platform** | Provee capacidades reutilizables que los stream-aligned consumen sin coordinar | Pocos |
| **Enabling** | Ayuda a otro equipo a adquirir una capacidad que le falta, y se retira | Pocos, y temporales en cada relación |
| **Complicated-subsystem** | Se hace cargo de una parte que exige especialización profunda: un motor de cálculo, un códec, un modelo | Los mínimos indispensables |

### Tres modos de interacción

El aporte menos citado del libro y el más útil para diagnosticar: no alcanza con nombrar los equipos, hay que definir **cómo se relacionan**.

| Modo | Qué significa | Cuándo corresponde |
|---|---|---|
| **Colaboración** | Dos equipos trabajan juntos, con responsabilidad compartida y límites difusos | Descubrimiento de algo nuevo. Caro; debe ser temporal |
| **X-as-a-Service** | Un equipo consume una capacidad del otro sin coordinar nada | Estado deseado de la relación con la plataforma |
| **Facilitación** | Un equipo ayuda a otro a aprender algo, sin hacerlo por él | Temporal por definición |

La relación entre un equipo de plataforma y sus usuarios **tiene que tender a X-as-a-Service**. Si se queda en colaboración permanente, la plataforma es un cuello de botella con vocabulario nuevo.

### Antipatrón del "equipo DevOps"

De todo lo anterior se sigue una consecuencia que muchas organizaciones aprendieron por las malas: **crear un "equipo DevOps" reconstruye el muro**. Si hay un equipo al que se le piden los despliegues, volvió a existir una entrega entre áreas, con otro nombre.

Matthew Skelton catalogó los patrones y antipatrones organizacionales en [DevOps Topologies](https://web.devopstopologies.com/), anterior al libro y de consulta libre. Los antipatrones más frecuentes:

| Antipatrón | Qué ocurre |
|---|---|
| Silos Dev y Ops | La separación clásica, sin colaboración. El punto de partida |
| Silo del equipo DevOps | Un tercer equipo entre los dos: la brecha ahora tiene dos bordes en lugar de uno |
| "Dev no necesita Ops" | Desarrollo subestima la operación. Reaparece como operaciones en la sombra |
| DevOps como equipo de herramientas | Se construye tooling sin cambiar cómo se reparte la responsabilidad |
| SysAdmin renombrado | El mismo equipo con otro título en la tarjeta. Cero cambio cultural |
| SRE falso | Se adopta el nombre de SRE (*site reliability engineering*, ingeniería de confiabilidad) para perpetuar la separación de siempre |
| Silos Dev y DBA | La misma dinámica del muro, aplicada a las bases de datos |

**Criterio para distinguir un equipo de plataforma de un "equipo DevOps": el modo de interacción.** Si se le piden cosas y las hace, es un silo. Si publica capacidades que otros consumen sin pedirle nada, es plataforma. El nombre del equipo no decide nada; el modo, sí.

---

# 2. De DevOps a Platform Engineering

## 2.1 Lo que cambió debajo

DevOps se formula en 2009. La base técnica sobre la que corre cambió por completo desde entonces:

| Año aproximado | Cambio | Efecto |
|---|---|---|
| 2006 en adelante | Cloud pública | La infraestructura pasa a ser software: se pide por API (*application programming interface*, interfaz de programación) |
| 2013 | Docker | La unidad de entrega deja de ser el servidor y pasa a ser la imagen |
| 2014 en adelante | Kubernetes | El despliegue se vuelve declarativo, y también mucho más configurable |
| 2014 en adelante | Terraform e IaC (*infrastructure as code*, infraestructura como código) | La infraestructura se versiona, se revisa en pull requests y falla como código |
| 2015 en adelante | Microservicios | Un sistema pasa de ser un despliegue a ser cincuenta |
| 2020 en adelante | GitOps, service mesh, políticas como código, observabilidad distribuida | Más capas, cada una con su modelo mental |

Cada una de estas tecnologías resolvió un problema real. Sumadas, produjeron un efecto que ninguna buscaba: **la superficie de conocimiento necesaria para poner un servicio en producción creció más rápido que la capacidad de una persona para sostenerla.**

## 2.2 El costo del "shift left"

DevOps, llevado a la práctica en ese contexto, significó mover responsabilidades hacia el desarrollador: pruebas, seguridad, infraestructura, despliegue, guardias. El movimiento se llamó *shift left*, y para la comunidad de platform engineering es exactamente donde el modelo se rompió:

> "The shift left movement has forced developers to have an end-to-end understanding of a growing number of complex, often infrastructure-centric tools and workflows."
> — [Luca Galante, *What is platform engineering?*, platformengineering.org](https://platformengineering.org/blog/what-is-platform-engineering)
>
> *"El movimiento de shift left obligó a quienes desarrollan a tener una comprensión de punta a punta de una cantidad creciente de herramientas y flujos de trabajo complejos, muchas veces centrados en infraestructura."*

El mismo texto nombra el síntoma organizacional resultante, el **antipatrón de operaciones en la sombra**: en la práctica, algunos desarrolladores terminan haciendo las tareas de infraestructura de todo el equipo y ayudando a sus colegas menos experimentados. La tarea no desapareció; se volvió invisible y quedó concentrada en dos o tres personas que además tienen otro trabajo.

Concretamente, para poner un "hola mundo" en producción en una organización que adoptó todo lo de la sección 2.1 hay que decidir:

| Dimensión | Decisiones |
|---|---|
| Código | Repositorio, convención de nombres, estructura, licencia, protección de rama |
| Empaquetado | Dockerfile o build nativo, registro de imágenes, versionado, firma |
| Infraestructura | Cuenta cloud, región, red, cómputo, almacenamiento, base de datos |
| Entrega | Pipeline de CI (integración continua), pipeline de CD (entrega continua), estrategia de despliegue, rollback |
| Exposición | DNS (sistema de nombres de dominio), certificado TLS (*transport layer security*), balanceo, reglas de ingreso |
| Identidad | Roles de ejecución, permisos mínimos, gestión de secretos |
| Operación | Logs, métricas, alertas, objetivo de disponibilidad, contacto de guardia |
| Gobierno | Etiquetado de costos, retención de datos, controles de cumplimiento |

Más de treinta decisiones antes de que el código haga algo útil. Ninguna es opcional en producción, y casi ninguna es específica del producto que se está construyendo.

## 2.3 Carga cognitiva

Team Topologies toma de la psicología cognitiva una distinción que ordena el problema ([Team Topologies — Key concepts](https://teamtopologies.com/key-concepts)):

| Tipo | Qué es | Ejemplo |
|---|---|---|
| Intrínseca | Habilidad base que el trabajo requiere | Saber programar en el lenguaje del equipo |
| Extrínseca | Mecánica del entorno, ajena al problema | Recordar el nombre del bucket de estado de Terraform |
| Germane | Dominio del negocio, lo diferenciador | Entender cómo se calcula un envío en el checkout |

Todo lo que enumera la tabla de la sección anterior es carga extrínseca, y **desplaza a la germane**: la capacidad de un equipo es finita, y lo que se va en mecánica no está disponible para el problema del negocio. Un equipo que dedica tres días a armar la infraestructura de un servicio dedica tres días menos al problema por el que existe.

## 2.4 Definición

> "Platform engineering is the discipline of designing and building toolchains and workflows that enable self-service capabilities for software engineering organizations in the cloud-native era."
> — [platformengineering.org](https://platformengineering.org/blog/what-is-platform-engineering)
>
> *"Platform engineering es la disciplina de diseñar y construir cadenas de herramientas y flujos de trabajo que habilitan capacidades de autoservicio para organizaciones de ingeniería de software en la era cloud-native."*

La versión de la CNCF (*Cloud Native Computing Foundation*, la fundación que aloja Kubernetes y buena parte del ecosistema cloud-native), más amplia, incluye explícitamente lo organizacional:

> "the practice of planning and providing such computing platforms to developers and users [...] encompasses all parts of platforms and their capabilities — their people, processes, policies and technologies; as well as the desired business outcomes that drive them."
> — [CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/)
>
> *"la práctica de planificar y proveer esas plataformas de cómputo a quienes desarrollan y usan [...] abarca todas las partes de las plataformas y sus capacidades — sus personas, procesos, políticas y tecnologías; así como los resultados de negocio que las motivan."*

**Platform Engineering no reemplaza a DevOps: es una forma de organizar el trabajo que DevOps hizo necesario.** Los objetivos de DevOps —responsabilidad compartida, automatización, lotes chicos— siguen vigentes. Lo que cambia es quién construye la mecánica para que un equipo de producto pueda cumplirlos sin volverse experto en seis herramientas de infraestructura.

## 2.5 Base fundacional

Cuatro principios. Sacar cualquiera de ellos produce un fracaso conocido, documentado en la sección 5.6.

| Principio | Enunciado | Qué falla sin él |
|---|---|---|
| Autoservicio | El usuario pide y recibe la capacidad de forma autónoma y automática | Ticket ops con mejor interfaz |
| Producto, no proyecto | La plataforma tiene usuarios, no destinatarios: se releva, se mide adopción, se versiona | Se construye lo que el equipo de plataforma cree, nadie lo usa |
| Reducción de carga cognitiva | Objetivo explícito, no efecto lateral | La plataforma agrega más conceptos de los que abstrae |
| Opcionalidad | El camino soportado es conveniente, no obligatorio | Los equipos lo esquivan, y la plataforma pierde la señal de qué mejorar |

Sobre el primero, el argumento cuantitativo más citado viene de Evan Bottcher: un estudio que cita muestra que las tareas que requieren la intervención de otro equipo son **entre 10 y 12 veces más lentas** en tiempo transcurrido que el trabajo independiente ([Bottcher, *What I Talk About When I Talk About Platforms*, martinfowler.com, 2018](https://martinfowler.com/articles/talk-about-platforms.html)). Ese número es toda la justificación económica del autoservicio.

## 2.6 Mirada holística

La ley de Conway y la taxonomía de la sección 1.5 tienen una consecuencia directa en este punto: **no se puede diseñar la plataforma sin diseñar la organización que la usa.** Una plataforma es un sistema socio-técnico; el software y el equipo que lo sostiene son la misma cosa a efectos del resultado.

Lo que importa de esa taxonomía en este punto es el modo de interacción. El de un equipo de plataforma con los demás es **X-as-a-Service**: se consume sin coordinar. Si el equipo de plataforma necesita reunirse con cada equipo para cada pedido, la topología está mal —y el síntoma es una cola de tickets.

De ahí viene el principio de **Thinnest Viable Platform** (TVP, plataforma viable más delgada): la plataforma mínima que acelera de forma medible, y nada más ([Team Topologies — Platform Engineering](https://teamtopologies.com/platform-engineering)). Una plataforma que crece sin este freno termina siendo un sistema que hay que aprender además de todos los demás.

---

# 3. Disciplinas que engloba

Platform engineering no es una tecnología. Es un punto de integración entre disciplinas que ya existían.

| Disciplina | Qué aporta a la plataforma |
|---|---|
| Infraestructura como código | Reproducibilidad: la infraestructura se describe, se versiona y se recrea |
| CI/CD | El camino automatizado del commit a producción |
| Orquestación de contenedores | Un sustrato común de ejecución para cargas heterogéneas |
| Observabilidad | Los datos que hacen operable lo desplegado: logs, métricas, trazas |
| SRE | Confiabilidad como disciplina de ingeniería: SLI (indicador de nivel de servicio), SLO (objetivo de nivel de servicio), presupuesto de error |
| Seguridad y cumplimiento | Controles incorporados al camino, no auditados después |
| FinOps | El costo como propiedad visible de cada componente |
| Gestión de producto | Relevamiento, priorización, adopción, ciclo de vida |
| Diseño de experiencia | Que la interfaz sea usable por alguien que no la construyó |
| Arquitectura | Las decisiones que la plataforma vuelve difíciles de violar |

### Platform Engineering y SRE

Se confunden porque comparten herramientas y perfil de gente. La diferencia está en la pregunta que responde cada una:

| Disciplina | Pregunta |
|---|---|
| SRE | ¿El sistema en producción cumple su objetivo de confiabilidad? |
| Platform Engineering | ¿Los equipos pueden entregar sin volverse expertos en infraestructura? |

Conviven: la plataforma provee los mecanismos —SLO declarados, alertas generadas, presupuesto de error visible— que SRE define y usa. En la demostración de la clase, la regla de nivel oro "tiene alerta configurada" es exactamente esa unión: el servicio declara su objetivo en un archivo y la plataforma crea la alarma que lo hace cumplir.

📖 Para leer: [Google SRE Book](https://sre.google/books/), capítulos 3 y 4.

---

# 4. Plataforma

## 4.1 Plataforma implícita

Casi ninguna organización cree tener una plataforma, y casi todas la tienen. La diferencia entre las dos afirmaciones es de vocabulario, no de infraestructura, y es el punto que más cambia la conversación con un equipo o con un cliente.

Cuando una empresa de tecnología dice "nosotros no tenemos plataforma", casi siempre quiere decir "no tenemos un producto interno al que le pusimos un nombre". Pero si esa empresa despliega software a producción, entonces tiene:

- un lugar donde vive el código y una convención —aunque sea implícita— de cómo se organiza;
- una forma de construir el artefacto y un lugar donde guardarlo;
- un mecanismo de despliegue, aunque sean tres scripts y una persona que sabe el orden;
- infraestructura corriendo, provista de alguna manera;
- alguna forma de saber si está funcionando;
- una manera de gestionar credenciales, aunque sea mala;
- reglas sobre quién puede tocar producción.

**Eso es una plataforma.** La pregunta no es si existe, sino si es explícita o implícita.

| Dimensión | Plataforma implícita | Plataforma explícita |
|---|---|---|
| Dónde vive | En la cabeza de quienes llevan más tiempo | En código, documentación y automatización |
| Cómo se aprende | Preguntando | Leyendo y usando |
| Consistencia | Cada servicio se armó distinto | Los servicios nuevos se parecen entre sí |
| Onboarding | Semanas de acompañamiento | Días |
| Qué pasa si se va una persona | Se pierde capacidad | Se pierde una persona |
| Quién la mantiene | Nadie explícitamente | Un equipo, con presupuesto |

El trabajo de platform engineering, en la enorme mayoría de los casos, no es construir una plataforma desde cero. Es **hacer explícita, estandarizar y dar interfaz a la plataforma que la empresa ya tiene**, por accidente y sin nombre.

De ahí que, en trabajo de consultoría, esta distinción sea el argumento de entrada: a la organización no se le propone comprar algo nuevo, sino reconocer, ordenar y hacer usable lo que ya paga todos los meses.

## 4.2 Los cinco planos

Para mostrarle a alguien que ya tiene una plataforma sirve un mapa. La arquitectura de referencia más difundida la divide en cinco planos: la presentó McKinsey Digital en PlatformCon 2023, a partir de cientos de instalaciones reales, y desde entonces se volvió el vocabulario común de la disciplina ([McKinsey Digital, *Platform as code*](https://medium.com/digital-mckinsey/platform-as-code-reference-architectures-to-simplify-developer-platforms-f2fb48e0c874)). Hay implementaciones publicadas como código para [AWS](https://github.com/humanitec-architecture/reference-architecture-aws), [Azure](https://github.com/humanitec-architecture/reference-architecture-azure) y [GCP](https://github.com/humanitec-architecture/reference-architecture-gcp), y los reportes con el diagrama completo están en [platformengineering.org/reports](https://platformengineering.org/reports).

**Un plano no es una capa de despliegue: es un agrupamiento de responsabilidades.** Una misma herramienta puede aparecer en dos planos, y un plano puede resolverse con una herramienta o con siete.

```
┌──────────────────────────────────────────────────────────────────────┐
│ 1 · CONTROL DEL DESARROLLADOR                                        │
│   Por dónde se pide algo                                             │
│   Portal · repositorio Git · CLI · IDE · especificación de workload  │
└───────────────────────────────┬──────────────────────────────────────┘
                                │  una intención: "quiero un servicio"
┌───────────────────────────────▼──────────────────────────────────────┐
│ 2 · INTEGRACIÓN Y ENTREGA                                            │
│   Qué convierte esa intención en algo que corre                      │
│   CI · registro de imágenes · orquestador · CD · motor de IaC        │
└───────────────────────────────┬──────────────────────────────────────┘
                                │  recursos concretos
┌───────────────────────────────▼──────────────────────────────────────┐
│ 3 · RECURSOS                                                         │
│   Dónde corre de verdad                                              │
│   Clúster · cómputo · base de datos · almacenamiento · red · DNS     │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
        ┌───────────────────────┴───────────────────────┐
┌───────▼───────────────────────┐   ┌───────────────────▼──────────────┐
│ 4 · MONITOREO Y LOGGING       │   │ 5 · SEGURIDAD                    │
│   Cómo se sabe qué ocurre     │   │   Quién puede qué, y con qué     │
│   Métricas · logs · trazas    │   │   Secretos · identidad · políticas│
│   Alertas · tableros          │   │   Certificados · permisos        │
└───────────────────────────────┘   └──────────────────────────────────┘
       atraviesan los tres planos de arriba, no van "abajo" de ellos
```

| # | Plano | Qué contiene | Ejemplos |
|---|---|---|---|
| 1 | Control del desarrollador | El punto de interacción: por dónde una persona pide algo y en qué formato lo describe | Portal, repositorio, CLI (interfaz de línea de comandos), IDE (entorno integrado de desarrollo), especificación de workload |
| 2 | Integración y entrega | Construir el artefacto, generar la configuración, aplicar la infraestructura, desplegar | CI, registro de imágenes, CD, orquestador, motor de IaC |
| 3 | Recursos | La infraestructura real donde corre la aplicación | Clústeres, cómputo, bases de datos, almacenamiento, red, DNS |
| 4 | Monitoreo y logging | Métricas, logs y trazas de aplicaciones e infraestructura, y las alertas sobre ellos | Prometheus, Grafana, OpenTelemetry, CloudWatch, Datadog |
| 5 | Seguridad | Gestión de secretos, identidad y políticas | OpenBao, Secrets Manager, OIDC (*OpenID Connect*), IAM (gestión de identidades y accesos), Open Policy Agent (OPA) |

### Dónde encaja lo que ya viste en la diplomatura

El valor del mapa para esta altura del programa es que casi todo lo cursado hasta ahora cae en alguno de los cinco planos. Lo que cambia no es la herramienta: es dejar de verla suelta y verla como parte de un sistema con responsabilidades repartidas.

| Tema | Plano | Qué aporta al conjunto |
|---|---|---|
| Git y flujo de ramas | 1 | Es la interfaz real de la mayoría de los cambios, antes que cualquier portal |
| Contenedores e imágenes | 2 | La unidad de entrega que atraviesa todo el pipeline |
| CI/CD | 2 | El camino automatizado del commit a producción |
| Infraestructura como código | 2 y 3 | Describe el plano 3 y se ejecuta desde el plano 2 |
| Kubernetes | 3 | El sustrato de ejecución, y buena parte de la complejidad que hay que abstraer |
| Redes y DNS en la nube | 3 | Lo que hace que un servicio sea alcanzable |
| Observabilidad | 4 | Lo que convierte un sistema desplegado en un sistema operable |
| IAM, roles y secretos | 5 | Lo que decide qué puede hacer cada pieza, incluidas las automáticas |

🟡 **Pendiente — programa de la diplomatura.** Esta tabla usa temas genéricos. Con el temario real de los módulos anteriores, cada fila puede nombrar la clase concreta, que es lo que hace que el mapa se sienta propio en lugar de prestado. **Bloquea:** la versión final de esta sección y de la slide correspondiente.

### Opciones abiertas por plano

Ningún plano exige software comercial. Las opciones de código abierto, la mayoría alojadas en fundaciones neutrales —CNCF y Linux Foundation—, cubren los cinco:

| Plano | Opciones de código abierto |
|---|---|
| Control del desarrollador | Backstage (CNCF), Score (especificación abierta de workload) |
| Integración y entrega | Argo CD y Flux (CNCF, graduados), Tekton, Jenkins, Crossplane, Kratix |
| Recursos | Kubernetes, OpenTofu, Crossplane |
| Monitoreo y logging | Prometheus, Grafana, OpenTelemetry, Loki, Jaeger |
| Seguridad | Keycloak, OpenBao, cert-manager, Open Policy Agent, Kyverno |

Dos de esos nombres merecen una nota, porque explican algo sobre la dependencia de proveedores. El 10 de agosto de 2023 HashiCorp cambió la licencia de Terraform de MPL (*Mozilla Public License*) a **BUSL 1.1** (*Business Source License*), una licencia que ya no es de código abierto según la definición de la OSI (*Open Source Initiative*, la organización que mantiene la definición de referencia). La respuesta de la comunidad fue un fork: **OpenTofu**, aceptado por la Linux Foundation en septiembre de 2023 y estable desde enero de 2024 ([OpenTofu Manifesto](https://opentofu.org/manifesto/), [OpenTofu — Wikipedia](https://en.wikipedia.org/wiki/OpenTofu)). **OpenBao** es el fork equivalente de Vault.

La lección no es sobre licencias sino sobre plataformas: **una plataforma bien diseñada hace que cambiar una pieza sea un trabajo acotado.** Si sustituir la herramienta de aprovisionamiento implica reescribir todo lo que la rodea, la plataforma no era una abstracción, era una dependencia.

**Ejercicio de reconocimiento.** Tomar una empresa —la propia, la de un trabajo práctico, una conocida— y completar la tabla con sus herramientas actuales. Dos resultados posibles, ambos informativos:

- Todos los planos tienen algo: la plataforma existe, está dispersa y sin interfaz común. El trabajo es de estandarización e interfaz.
- Un plano está vacío: ahí está el agujero. Un portal encima no lo va a tapar.

Observación sobre el primer plano: el portal es **una parte** del plano de control del desarrollador, no la plataforma entera. Es un cuarto de un quinto del sistema.

## 4.3 Definiciones formales

La definición más citada, anterior al término platform engineering:

> "A digital platform is a foundation of self-service APIs, tools, services, knowledge and support which are arranged as a compelling internal product."
> — [Evan Bottcher, martinfowler.com, 2018](https://martinfowler.com/articles/talk-about-platforms.html)
>
> *"Una plataforma digital es una base de APIs, herramientas, servicios, conocimiento y soporte de autoservicio, dispuestos como un producto interno atractivo."*

La de CNCF:

> "A platform for cloud-native computing is an integrated collection of capabilities defined and presented according to the needs of the platform's users."
> — [CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/)
>
> *"Una plataforma para cómputo cloud-native es una colección integrada de capacidades, definidas y presentadas según las necesidades de quienes la usan."*

Tres palabras cargan el peso en las dos: *self-service*, *product*, *needs of the users*. Ninguna menciona una tecnología.

Una formulación más reciente, útil porque descarta explícitamente la confusión con la herramienta:

> "a platform is not a tool, a portal, or a dashboard, but the sum of paths enabled by a set of capabilities, exposed through interfaces."
> — [platformengineering.org](https://platformengineering.org/blog/what-is-platform-engineering)
>
> *"una plataforma no es una herramienta, ni un portal, ni un tablero: es la suma de los caminos que habilita un conjunto de capacidades, expuestas a través de interfaces."*

## 4.4 Atributos de una plataforma que funciona

Los siete que enumera CNCF ([fuente](https://tag-app-delivery.cncf.io/whitepapers/platforms/)):

| Atributo | Qué implica |
|---|---|
| Plataforma como producto | Se diseña según necesidades relevadas de sus usuarios |
| Experiencia de usuario | Interfaces consistentes: GUI (interfaz gráfica), API, CLI, portal |
| Documentación y onboarding | Golden paths y plantillas reutilizables |
| Autoservicio | El usuario pide y recibe la capacidad de forma autónoma y automática |
| Reducción de carga cognitiva | Objetivo esencial, no efecto lateral |
| Opcional y componible | Se pueden usar partes; se puede resolver por fuera |
| Seguro por defecto | Cumplimiento y validación incorporados |

## 4.5 Golden path

Un *golden path* es el camino soportado y documentado para hacer algo común: crear un servicio, agregar una base de datos, exponer una API. No es el único camino posible, es el que la organización mantiene.

El término lo acuñó Spotify, tomado de *Hijos de Dune* de Frank Herbert, donde nombra la única ruta que evita la catástrofe. El problema que resolvía tenía nombre propio en la empresa: *development by rumor* — la única forma de averiguar cómo hacer algo era preguntarle a alguien que quizá supiera ([Spotify Engineering, 2020](https://engineering.atspotify.com/2020/08/how-we-use-golden-paths-to-solve-fragmentation-in-our-software-ecosystem)).

La definición operativa más útil es la de Kaspar von Grünberg: un golden path es cualquier procedimiento del ciclo de vida del software que un usuario puede seguir con carga cognitiva mínima y **que impulsa estandarización** ([The New Stack](https://thenewstack.io/humanitec-the-golden-path-to-platform-engineering/)). La segunda mitad de esa frase es la sección 6 de este apunte: el camino no solo facilita la tarea, además hace que todos la resuelvan igual.

### Paved road: la versión de Netflix

Netflix llegó a la misma idea por otro camino y con otra metáfora. Un *paved road* es un camino pavimentado que cruza un terreno: **se puede ir por afuera, pero el asfalto es más rápido**. La palabra que importa es la que no está en la metáfora: *obligatorio*.

**De dónde sale.** Netflix opera con un modelo llamado **full cycle developers**: cada equipo diseña, construye, prueba, despliega y opera sus propios servicios, combinando competencias que en otras organizaciones están en tres roles separados —desarrollo, testing y confiabilidad— ([Netflix Technology Blog, *Full Cycle Developers at Netflix*, 2018](https://medium.com/netflix-techblog/full-cycle-developers-at-netflix-a08c31f83249); cobertura en [InfoQ](https://www.infoq.com/news/2018/06/netflix-full-cycle-developers/)).

> "Distributing this responsibility to each development team, rather than externalizing it, creates direct feedback loops and aligns incentives."
> — Netflix Technology Blog, 2018
>
> *"Distribuir esta responsabilidad en cada equipo de desarrollo, en lugar de externalizarla, crea circuitos de retroalimentación directos y alinea los incentivos."*

Ese modelo solo es sostenible si hay algo debajo. Lo que hay son **equipos centralizados** —plataforma cloud, confiabilidad y rendimiento, herramientas de ingeniería— que construyen y mantienen el camino pavimentado: las herramientas comunes que todos los equipos necesitan y que ninguno debería resolver por su cuenta. Es, con otro nombre, un equipo de plataforma en el sentido de la sección 1.5.

**Cómo funciona la opcionalidad.** Netflix no impone la adopción. La fomenta asegurándose de que desarrollar y operar sobre el camino pavimentado sea una experiencia mejor que hacerlo por afuera, por un margen que se nota. Un equipo puede salirse —*go off-road*— y entonces asume las consecuencias: mantiene lo suyo, opera lo suyo y no recibe el soporte central.

Eso tiene dos efectos, y el segundo es el menos obvio:

| Efecto | Qué produce |
|---|---|
| El camino gana por mérito | La adopción es voluntaria, así que es una señal honesta de si el camino sirve |
| Salirse tiene costo, no castigo | El equipo que se sale no viola una regla: paga un precio, y puede estar justificado que lo pague |

De ahí sale el criterio de éxito que conviene retener: **si muchos equipos se salen del camino, el problema es el camino.** En una organización que impone el camino, esa señal desaparece: los equipos cumplen y el equipo de plataforma se queda sin saber si lo que construyó sirve.

**Lo que Netflix reconoce que cuesta.** El propio texto enumera los límites: no todas las personas tienen las habilidades que el modelo exige —invierten mucho en formación—, no todas quieren trabajar así, y copiarlo sin adaptarlo falla.

> "Evaluate what you need and be mindful of bringing in the least complexity necessary."
> — Netflix Technology Blog, 2018
>
> *"Hay que evaluar lo que se necesita y prestar atención a incorporar la menor complejidad necesaria."*

Es la misma advertencia que Thinnest Viable Platform, formulada por una empresa que construyó una plataforma enorme.

**Golden path y paved road.** En la práctica se usan como sinónimos y no vale la pena discutirlos. Si se quiere una distinción de énfasis —y esto es lectura propia, no una definición de las fuentes—: el *golden path* de Spotify apunta al camino documentado y opinado para **una tarea** concreta, con plantillas incluidas; el *paved road* de Netflix apunta al **conjunto de herramientas soportadas** sobre el que corre todo. Uno es la ruta, el otro es el asfalto.

De todo lo anterior queda una prueba de diseño con dos resultados posibles, y los dos informan: si el camino es obligatorio, el equipo de plataforma reinventó el ticket ops con otra interfaz; si es opcional y nadie lo usa, está mal diseñado.

---

# 5. Portal

## 5.1 Platform y Portal

La sigla IDP se usa para dos cosas distintas, y la confusión es sistemática.

| Sigla | Qué es | Ejemplos |
|---|---|---|
| Internal Developer **Platform** | El conjunto de capacidades que aprovisionan y operan: pipelines, módulos de IaC, clústeres, políticas, secretos | Los cinco planos de la sección 4.2 |
| Internal Developer **Portal** | La interfaz sobre esas capacidades: catálogo, formularios de autoservicio, estándares, tableros | Backstage, Port, Cortex, OpsLevel |

El portal no aprovisiona nada por sí mismo. Dispara lo que la plataforma ya sabe hacer y muestra el resultado. La formulación de un análisis comparativo reciente es directa: *Port, Cortex y Backstage proveen la capa de interfaz pero requieren una plataforma separada debajo para ejecutar cualquier cosa* ([Encore, *Platform Engineering Tools Compared*](https://encore.dev/articles/platform-engineering-tools)).

La consecuencia práctica, y lo que conviene retener de esta sección: **un portal instalado sobre una empresa sin pipelines ni IaC produce un catálogo de vínculos rotos y formularios que no hacen nada.**

En este apunte, de aquí en adelante, **IDP significa portal**, salvo indicación explícita.

## 5.2 Qué features busca brindar un portal

Siete capacidades. Un portal serio tiene las siete; la mayoría de los proyectos que fracasan implementan solo la primera.

### Catálogo y modelo de datos

El inventario de lo que existe: servicios, repositorios, entornos, equipos, clústeres, bases de datos, incidentes, clientes. Su valor no está en la lista sino en las **relaciones**: qué equipo posee qué servicio, en qué entorno corre, sobre qué infraestructura, para qué línea de negocio.

Criterio de diseño: el modelo de datos refleja cómo la organización piensa, no cómo las herramientas exportan. **Un catálogo que solo modela lo que GitHub devuelve responde preguntas de GitHub, no preguntas de la organización** — y para las primeras ya estaba GitHub.

La diferencia se ve mejor con dos preguntas:

| Pregunta | Quién la responde |
|---|---|
| "¿Cuántos repositorios tenemos y cuál se tocó último?" | GitHub, sin catálogo de por medio |
| "¿Qué servicios de este cliente corren en producción, sin dueño asignado y sin alertas?" | Solo un catálogo cuyo modelo tenga cliente, entorno, dueño y estado |

La segunda no la responde ninguna herramienta de origen, porque *cliente*, *dueño* y *criticidad* no son conceptos de GitHub, de Kubernetes ni de la nube: son conceptos de la organización. **Si el modelo de datos no los tiene, el catálogo es un espejo de las herramientas y no un modelo de la empresa.**

### Ingesta automática

El catálogo se puebla solo o no se puebla.

| Mecanismo | Cómo funciona | Cuándo se usa |
|---|---|---|
| Integración *pull* | El portal consulta la API de la herramienta cada N minutos | Fuentes con API estable: cloud, Git, Kubernetes |
| *Webhook* / push | La herramienta notifica al portal ante un evento | Latencia baja, fuentes que emiten eventos |
| API directa | Un pipeline escribe en el portal durante su ejecución | Datos que solo existen durante el despliegue |

Regla práctica: **todo dato que alguien tenga que cargar a mano queda desactualizado.** La única excepción razonable son los datos que no existen en ningún sistema —criticidad declarada, contacto de guardia, objetivo de disponibilidad.

### Autoservicio y scaffolding

Formularios que disparan automatizaciones. El caso canónico es crear un servicio: un formulario recoge lo que la plataforma no puede deducir, y un pipeline hace el resto.

Criterio de diseño: **el formulario solo pregunta lo que la plataforma no puede averiguar.** Si un campo se puede derivar del nombre, del repositorio o de la entidad relacionada, preguntarlo es introducir una oportunidad de que dos fuentes se contradigan.

### Estándares y scorecards

Reglas evaluadas continuamente sobre las entidades del catálogo: si tiene dueño, si tiene runbook, si tiene alertas, si la rama principal está protegida.

Un scorecard convierte una política escrita en un dato consultable. El cambio de fondo es de mecanismo: se pasa de auditar una vez por trimestre a medir de forma continua, y de perseguir equipos a mostrar una brecha.

**Por qué por niveles y no por sí o no.** Un *criterio binario* es un scorecard con un solo veredicto: el servicio cumple el estándar o no lo cumple. Con veinte reglas y una sola aprobación, alcanza con incumplir una para quedar del lado de afuera. El resultado previsible es que casi todos quedan afuera, y ahí el dato deja de informar:

| Servicio | Reglas que cumple | Veredicto binario | Qué le falta de verdad |
|---|---|---|---|
| `checkout-api` | 19 de 20 | ❌ No cumple | Le falta el runbook |
| `legacy-billing` | 2 de 20 | ❌ No cumple | No tiene dueño, ni repositorio, ni alertas, y corre en producción |

Los dos aparecen igual en la lista, y no están ni cerca de la misma situación. Un líder que mira ese tablero no sabe a cuál atender primero, y el equipo de `checkout-api` aprende que esforzarse no cambia el resultado — que es la forma más rápida de que un estándar se vuelva decorativo.

**Los niveles resuelven las dos cosas a la vez:** ordenan las reglas por dificultad y dan un próximo paso concreto. El diseño que funciona agrupa por **quién puede satisfacer cada regla**:

| Nivel | Qué mide | Quién lo satisface |
|---|---|---|
| Bronce | Que la entidad esté bien descripta y tenga dueño | El camino soportado, sin esfuerzo adicional |
| Plata | Que existan las automatizaciones básicas | Los pipelines, cuando corren |
| Oro | Que el servicio sea operable por alguien que no lo escribió | Requiere artefactos reales: runbook, alertas, objetivo declarado, contacto |

Así, un servicio en bronce sabe exactamente qué le falta para llegar a plata, y la organización puede exigir bronce a todo y oro solo a lo crítico.

**Tres criterios para que una regla sirva.** Una regla vale si cumple las tres:

| Criterio | Qué significa |
|---|---|
| Medible con datos que ya están | Si evaluarla requiere que alguien complete un campo a mano, la regla mide voluntad de completar formularios |
| Accionable por el equipo dueño | Si depende de otro equipo, el scorecard genera frustración, no mejora |
| Acordada | Una regla que nadie discutió antes se lee como una imposición, y se ignora |

### Visualización

Un **tablero por audiencia** es un conjunto de vistas armado para responder las preguntas que un rol concreto se hace todas las semanas. La palabra clave es *preguntas*: no es el mismo tablero con otro filtro, porque cada rol mira datos distintos, con otro nivel de detalle y otro horizonte de tiempo.

La analogía más cercana para quien todavía no trabajó en una empresa es el campus virtual de una universidad. Los datos son los mismos —alumnos, materias, notas—, pero la pantalla del alumno muestra sus materias y sus notas, la del docente muestra el curso completo y quiénes están por debajo, y la de la secretaría académica muestra tasas de aprobación por carrera. Nadie pensaría en darle a los tres la misma pantalla con un filtro distinto.

Tres ejemplos de una organización de software:

| Audiencia | Pregunta que se hace | Qué muestra su tablero |
|---|---|---|
| **Equipo de desarrollo** | "¿Cómo están mis servicios y qué tengo que arreglar esta semana?" | Sus servicios y solo los suyos; nivel de scorecard de cada uno y qué regla le falta para subir; alertas activas; último despliegue; pull requests abiertas hace más de una semana |
| **Líder técnico o de área** | "¿Dónde está el riesgo, y qué equipo necesita ayuda?" | Distribución del scorecard por equipo; servicios críticos por debajo del estándar; servicios sin dueño asignado; qué equipos tienen más servicios de los que pueden sostener |
| **Seguridad** | "¿Qué incumple hoy, y qué tan expuesto está?" | Servicios con vulnerabilidades críticas abiertas; repositorios sin protección de rama; imágenes sin escanear; servicios expuestos a internet sin autenticación |

Dos cosas cambian entre ellos y explican por qué no es un filtro:

| Dimensión | Equipo | Líder | Seguridad |
|---|---|---|---|
| Grano | Un servicio a la vez | Un equipo a la vez | Toda la organización |
| Horizonte | Esta semana | Este trimestre | Ahora mismo |
| Qué hace con el dato | Lo arregla | Reasigna gente y prioridades | Escala o bloquea |

Un cuarto tablero aparece cuando la organización vende servicios profesionales, como es el caso de la demostración de esta clase: el de **cuentas o dirección**, que agrupa por cliente y no por tecnología —qué servicios pertenecen a cada contrato, cuáles están por debajo del estándar acordado, cuánto cuesta cada uno—. Es la vista que ninguna herramienta de ingeniería produce, porque ninguna sabe qué es un cliente.

### Permisos y gobierno

Dos preguntas distintas, que se suelen mezclar:

| Pregunta | Nombre | Ejemplo |
|---|---|---|
| ¿Quién **ve** qué? | Permisos de lectura | Un squad ve las entidades del cliente en el que trabaja, y no las de los otros |
| ¿Quién **ejecuta** qué? | Permisos de acción | Cualquiera crea un servicio en entorno de prueba; solo el líder del equipo lo hace en producción |
| ¿Quién **cambia las reglas**? | Gobierno | Quién puede crear un tipo de entidad nuevo, cambiar un scorecard o agregar una integración |

La tercera fila es la que se olvida y la que más importa a mediano plazo. Si cualquiera puede agregar propiedades y tipos, en seis meses el modelo de datos tiene tres formas de decir lo mismo y el catálogo deja de ser confiable. El gobierno incluye también el **registro de auditoría**: quién ejecutó qué acción, cuándo y con qué parámetros.

De nuevo la analogía del campus: el alumno ve su legajo, el docente ve el curso, y solo unas pocas personas pueden modificar el plan de estudios. Lo último no es un permiso más grande: es una categoría distinta de permiso.

**Por qué en una consultora esto no es configuración sino condición de existencia.** Una empresa que opera varios clientes en paralelo tiene, en un mismo catálogo, información de organizaciones que compiten entre sí. Si el equipo del cliente A puede ver la infraestructura, los contratos o los incidentes del cliente B, ese catálogo no se puede construir: el problema deja de ser de comodidad y pasa a ser contractual y legal. Los permisos son lo que hace posible que los datos convivan en un solo lugar.

Un matiz que conviene tener claro desde el principio: **ocultar no es lo mismo que impedir**. Que alguien no vea una acción en la pantalla no significa que no pueda invocarla por la API. Los permisos se aplican en el servidor o no se aplican.

### Automatizaciones

Una automatización tiene tres partes: un **disparador** —algo cambió en el catálogo—, una **condición** y una **acción**. Se diferencia de una acción de autoservicio en quién la inicia: la acción la dispara una persona que aprieta un botón; la automatización la dispara un evento, sin que nadie esté mirando.

| Disparador | Condición | Acción |
|---|---|---|
| Una entidad pasa a estado `deprecated` | Tiene infraestructura asociada | Abre un ticket de desmantelamiento y se lo asigna al equipo dueño |
| Un servicio baja de nivel en el scorecard | Es de criticidad alta | Avisa en el canal del equipo, diciendo qué regla se rompió |
| Se registra un repositorio nuevo | No tiene equipo dueño después de 48 horas | Recuerda al creador; a los siete días, escala al líder del área |
| Cambia el propietario de un servicio | Siempre | Actualiza el contacto de guardia y la lista de aprobadores |
| Un certificado vence en 30 días | El servicio está en producción | Crea el ticket de renovación antes de que alguien se acuerde |

Tres observaciones sobre el diseño, porque es fácil hacerlas mal:

| Criterio | Detalle |
|---|---|
| Actuar, no solo avisar | Una automatización que crea el ticket y lo asigna vale mucho más que una que manda un mensaje. El mensaje hay que convertirlo en trabajo a mano |
| Silenciar lo que no es accionable | Un canal que recibe cincuenta notificaciones por día se silencia en una semana, y con él se pierden las cinco que importaban |
| Escalar por tiempo, no por grito | La secuencia recordatorio → escalamiento reparte la presión. Avisar diez veces a la misma persona, no |

Y una regla que vale para todo el capítulo: la automatización se construye **después** de que el proceso está estandarizado, no antes. Es el punto de la sección 6.5.

## 5.3 Enfoques de los distintos portales

El mercado no es homogéneo: las herramientas resuelven problemas distintos y algunas ni siquiera son portales.

| Herramienta | Naturaleza | Licencia | Énfasis | Sitio |
|---|---|---|---|---|
| **Backstage** | Framework de portal (Spotify → CNCF) | Open source, Apache 2.0 | Extensibilidad. Se programa en TypeScript; hay plugin para casi todo | [backstage.io](https://backstage.io) |
| **Port** | Portal, producto SaaS | Privado | Modelo de datos definido por el usuario y tiempo a valor | [port.io](https://port.io) |
| **Cortex** | Portal, producto | Privado | Estándares de ingeniería y madurez de servicios | [cortex.io](https://www.cortex.io) |
| **OpsLevel** | Portal, producto | Privado | Propiedad de servicios, salud y compuertas de despliegue | [opslevel.com](https://www.opslevel.com) |
| **Spotify Portal** | Distribución de Backstage | Privado, sobre base open source | Backstage operado por Spotify, sin tener que construirlo | [backstage.spotify.com](https://backstage.spotify.com) |
| **Roadie** | Backstage gestionado por un tercero | Privado, sobre base open source | Lo mismo, con otro proveedor | [roadie.io](https://roadie.io) |
| **Humanitec** | **Orquestador**, no portal | Privado. La especificación Score que usa es abierta | Ejecuta el aprovisionamiento. Vive en el plano de integración y entrega | [humanitec.com](https://humanitec.com) |
| **Kratix** | **Framework de plataforma**, no portal | Open source | Provee capacidades como *promises* de Kubernetes | [kratix.io](https://www.kratix.io) |

La columna de licencia esconde una distinción que conviene leer con cuidado: **"privado sobre base open source" no es lo mismo que open source.** Spotify Portal y Roadie empaquetan y operan Backstage; el código base sigue siendo abierto, pero lo que se contrata —el alojamiento, los plugins propios, el soporte— no lo es. La ventaja es real: se obtiene Backstage sin el equipo que lo mantiene. El costo también: se vuelve a depender de un proveedor, que era justo lo que el open source evitaba.

Las dos últimas filas son la distinción de la sección 5.1 hecha producto: Humanitec y Kratix no compiten con Backstage ni con Port, se ubican debajo. Un stack completo suele combinar portal y orquestador ([Encore](https://encore.dev/articles/platform-engineering-tools)).

### Backstage y los portales comerciales

| Dimensión | Backstage | Portal comercial |
|---|---|---|
| Licencia | Open source, Apache 2.0 | Suscripción |
| Naturaleza | Framework que se programa | Producto que se configura |
| Modelo de datos | System Model fijo, extensible con código | Definido por el usuario |
| Tiempo al primer valor | Meses | Días o semanas |
| Costo real | Ingenieros dedicados a mantenerlo | Licencia, más quien lo configure |
| Techo | Alto: se puede construir cualquier cosa | El del producto |

Backstage se liberó el 16 de marzo de 2020 y se donó ese mismo año a CNCF, donde hoy es proyecto en nivel *Incubating* ([Spotify Engineering](https://engineering.atspotify.com/2020/9/cloud-native-computing-foundation-accepts-backstage-as-a-sandbox-project), [CNCF](https://www.cncf.io/announcements/2026/03/25/cncf-backstage-documentary-highlights-project-evolution-from-development-to-global-open-source-standard-for-platform-engineering/)).

La elección no es técnica sino de asignación de personas: **la licencia es gratis, el equipo que lo mantiene no.** Un portal es software productivo; alguien lo mantiene siempre. La diferencia está en si ese alguien está en la nómina propia o en la del proveedor.

## 5.4 Cuándo tiene sentido montar un portal

La pregunta correcta no es de tamaño sino de dolor. Cinco señales; con dos o tres, el portal se justifica:

| Señal | Cómo se manifiesta |
|---|---|
| **Opacidad del inventario** | No hay una respuesta confiable a "cuántos servicios tenemos y quién los opera". Dos personas dan dos números distintos, y ninguna se equivoca del todo |
| **Onboarding lento** | Una persona nueva necesita semanas y a alguien con antigüedad que le explique el camino. El costo se paga en dos personas, no en una |
| **Conocimiento tribal** | "¿A quién le pregunto por este servicio?" aparece en el chat varias veces por semana. La respuesta existe, pero vive en la memoria de alguien |
| **Auditoría manual** | Saber quién cumple una política obliga a revisar repositorios a mano. Cada auditoría cuesta lo mismo que la anterior, porque no deja nada construido |
| **Saturación de memoria** | El número de servicios supera lo que una persona puede sostener en la cabeza. A partir de ahí, nadie tiene el panorama completo y las decisiones se toman con información parcial |

Como referencia de tamaño —criterio de mercado, no medición—: un análisis comparativo de 2026 ubica el umbral de *build vs buy* alrededor de los 50 desarrolladores, y el de Backstage con equipo dedicado a partir de los 200 ([Encore](https://encore.dev/articles/platform-engineering-tools)). Galante señala un umbral más bajo y en otra unidad: pasados los 20 o 30 usuarios de plataforma, el costo de coordinación manual deja de ser manejable ([platformengineering.org](https://platformengineering.org/blog/what-is-platform-engineering)). Las dos cifras son estimaciones de la industria, no resultados de estudio.

## 5.5 Prerrequisitos, y cuándo estandarizar primero

Un portal no arregla una plataforma que no existe. Antes de montarlo conviene verificar:

| Prerrequisito | Por qué |
|---|---|
| Control de versiones universal | El catálogo se puebla del repositorio. Si hay código fuera de Git, queda fuera |
| CI automatizada | Sin pipeline no hay nada que un formulario pueda disparar |
| Infraestructura como código, aunque sea parcial | El aprovisionamiento por consola no es automatizable ni reproducible |
| Propiedad definida | Si nadie sabe qué equipo posee qué, el catálogo hereda esa ambigüedad |
| Un golden path, aunque sea uno solo | Un portal sin camino que ofrecer es un inventario |

**Cuándo estandarizar la plataforma en lugar de montar un portal.** Si cada servicio se despliega distinto, si no hay convención de nombres, si el aprovisionamiento es manual, el portal va a reflejar ese desorden con mejor tipografía. El orden correcto es: estandarizar un camino, automatizarlo, y recién entonces ponerle interfaz y catálogo.

La excepción, y es real: el catálogo tiene valor **antes** de que haya nada estandarizado, como herramienta de diagnóstico. Inventariar lo que existe y medirlo contra un estándar aspiracional muestra el tamaño del problema con datos en lugar de con opiniones. Es lo que hace la demostración de esta clase cuando exhibe cinco servicios heredados que no llegan al estándar.

## 5.6 Modos de falla

| Falla | Síntoma | Causa |
|---|---|---|
| Catálogo muerto | Nadie lo abre; los datos tienen meses | Se pobló a mano, sin ingesta automática |
| Portal sin plataforma | Formularios que abren tickets | No hay automatización detrás, solo presentación |
| Golden path obligatorio | Los equipos lo evitan o lo esquivan | Se volvió un control, dejó de ser una conveniencia |
| Plataforma como cuello de botella | La cola de pedidos crece | Se reimplementó ticket ops con mejor interfaz |
| Scorecard ignorado | Todos en bronce durante meses | Se mide lo que nadie acordó, o no hay camino para subir |
| Plataforma sin producto | Se construyó lo que el equipo de plataforma creía | No hubo relevamiento ni medición de adopción |

📖 Para leer: el [CNCF Platform Engineering Maturity Model](https://tag-app-delivery.cncf.io/whitepapers/platform-eng-maturity-model/) ordena estos problemas en niveles de madurez sobre cinco aspectos: inversión, adopción, interfaces, operaciones y medición.

---

# 6. Estandarización

Un portal, un orquestador y un pipeline son reemplazables. Lo que una organización acuerda —cómo se nombran las cosas, qué significa cada concepto, dónde termina un proceso— sobrevive a los tres, y condiciona todo lo que se pueda automatizar después.

## 6.1 Qué significa estandarizar

No significa que todos los equipos usen el mismo lenguaje ni la misma base de datos. Significa que **las decisiones que no diferencian al producto se toman una vez y se reutilizan**.

| Nivel | Qué se estandariza | Ejemplo |
|---|---|---|
| Nomenclatura | Cómo se nombran las cosas | Un servicio se llama igual en el repositorio, en el registro de imágenes, en el clúster y en la ruta de la API |
| Modelo de datos | Qué conceptos existen y cómo se relacionan | "Servicio", "proyecto", "cliente" significan lo mismo para todos |
| Procesos | Qué pasos tiene una operación común y cuándo termina | Crear un servicio, dar de baja un servicio, rotar un secreto |
| Estructura | Qué contiene un componente válido | Todo repositorio tiene README, runbook y declaración de SLO |
| Propiedad | Quién responde por cada cosa | Cada servicio tiene un equipo dueño y un contacto de guardia |
| Niveles | Qué significa "listo para producción" | Los criterios de un scorecard |

## 6.2 Nomenclatura

Parece el nivel más trivial y es el que habilita todo lo demás. En la demostración de esta clase, el nombre del servicio deriva: el repositorio, el registro de imágenes, el servicio de ECS (el orquestador de contenedores de AWS), la entrada de descubrimiento y la ruta de la API.

La consecuencia es fuerte: **si todo se deriva de un nombre, nada puede desincronizarse.** No hay un lugar donde alguien escriba el nombre por segunda vez y se equivoque. Y en sentido inverso: dado un recurso cualquiera en la nube, se puede reconstruir a qué servicio pertenece sin preguntarle a nadie.

Sin esa disciplina, la relación entre un recurso de infraestructura y el servicio que lo usa vive en la memoria de alguien. Esa es, exactamente, la información que un catálogo necesita y que un agente de IA no puede inferir.

## 6.3 Proceso cerrado

Un proceso está cerrado cuando tiene tres cosas: **un inicio definido, un final definido, y un estado observable en el medio**. La mayoría de los procesos de una empresa de tecnología fallan en el tercero.

| Proceso abierto | Proceso cerrado |
|---|---|
| "Se pidió el alta hace unos días" | La entidad está en estado `provisioning` desde hace 4 minutos |
| "Creo que ya lo dieron de baja" | La acción de baja destruyó la infraestructura, borró el repositorio y eliminó la entidad |
| "Hay que preguntarle a alguien si terminó" | El pipeline reportó cada paso contra la ejecución |

Detalle de diseño de la demostración que ilustra el punto: **la entidad del catálogo se crea antes que la infraestructura**, y progresa por estados hasta `ready`. El catálogo es registro de intención, no solo de resultado. Un fallo a mitad de camino deja la entidad marcada `failed` en lugar de aparentar que sigue construyendo.

## 6.4 Dónde está el límite

La estandarización tiene un punto de rendimiento decreciente y hay que saber verlo.

| Se estandariza | No se estandariza |
|---|---|
| Lo que no diferencia al producto | Las decisiones de dominio |
| Lo que se repite | Lo que ocurre una vez |
| Lo que cuesta caro equivocar | Lo que es barato revertir |
| La forma de pedir una capacidad | Qué se construye con ella |

El criterio de Team Topologies es el freno: Thinnest Viable Platform. Una plataforma que estandariza más de lo necesario deja de acelerar y empieza a estorbar, y el síntoma es que los equipos la esquivan. El estándar que nadie sigue no es un estándar, es un documento.

## 6.5 Escalera: de estandarizar a automatizar

Ninguna organización salta del primer escalón al último. Y ninguna puede saltarse uno.

| # | Escalón | Qué existe |
|---|---|---|
| 1 | Manual y tribal | Alguien sabe hacerlo. No está escrito |
| 2 | Documentado | Hay un instructivo. Cada quien lo ejecuta a mano |
| 3 | Automatizado | Hay un script o un pipeline. Lo corre quien tiene acceso |
| 4 | Autoservicio | Cualquiera con permiso lo dispara desde una interfaz, sin pedir nada |
| 5 | Automático | Se dispara solo ante un evento, sin persona |
| 6 | Agéntico | Un agente decide que hay que hacerlo, lo hace dentro de límites y queda auditado |

**Cada escalón requiere que el anterior esté estandarizado.** No se puede automatizar un proceso cuyos pasos cambian según quién lo ejecute; no se puede dar en autoservicio algo que no está automatizado; y no se le puede delegar a un agente una decisión sobre un sistema cuyo estado nadie puede consultar de forma estructurada.

La conclusión que sostiene el resto del apunte: **la estandarización no es prolijidad, es el prerrequisito de la automatización, y la automatización es el prerrequisito de todo lo demás** — del autoservicio, de la medición y, desde hace poco, de poder delegarle trabajo a un agente.

Las dos secciones que siguen son esa escalera en concreto. **Port** (sección 7) es un ejemplo de herramienta que ayuda a subir del escalón 3 al 5: permite declarar el estándar, medirlo y exponerlo como autoservicio. La **era agéntica** (sección 8) es el escalón 6, y depende de que los anteriores existan. Ninguna de las dos reemplaza a esta sección: una empresa sin estándar que compra un portal tiene un estándar ausente con mejor interfaz.

---

# 7. Port

Con el estándar planteado, una herramienta se evalúa por una sola pregunta: **qué problema de estandarización resuelve**, no cuántas funcionalidades tiene. Port se presenta en ese orden porque es el producto sobre el que corre la demostración de la clase, y porque su modelo de datos hace visibles varios de los conceptos de la sección anterior.

## 7.1 Qué es

[Port](https://port.io) es un portal comercial en modalidad SaaS (*software as a service*: se paga por uso y lo opera el proveedor). Su documentación actual se presenta como *agentic engineering platform*, organizada en pilares: Context Lake, Workflows, Port AI, Agent Management, Interface Builder y Governance ([docs.port.io](https://docs.port.io/getting-started/overview)).

| Pilar | Qué cubre | Doc |
|---|---|---|
| Context Lake | El catálogo: modelo de datos, ingesta, consulta | [/context-lake](https://docs.port.io/context-lake/overview/) |
| Workflows | Acciones de autoservicio y automatizaciones | [/workflows](https://docs.port.io/workflows/overview/) |
| Governance | Scorecards, estándares y cumplimiento | [/governance](https://docs.port.io/governance/overview/) |
| Interface Builder | Tableros y páginas de catálogo | [/interface-builder](https://docs.port.io/interface-builder/overview/) |
| Port AI | Consultas y asistencia sobre el catálogo | [/port-ai](https://docs.port.io/port-ai/overview/) |
| Agent Management | Registro y gobierno de agentes | [/agent-management](https://docs.port.io/agent-management/overview/) |

> Nota de método: la nomenclatura de Port cambió de forma significativa durante 2026 —el catálogo pasó a llamarse Context Lake—. Cualquier afirmación sobre features, límites o precios debe verificarse contra [docs.port.io](https://docs.port.io) antes de repetirse, y **los enlaces de esta sección conviene revisarlos antes de cada dictado**: una reorganización de la documentación los rompe sin aviso.

## 7.2 Features, leídas como problemas

La forma útil de leer un producto no es por su lista de funcionalidades sino por el problema de industria que cada una ataca.

| Problema | Feature | Cómo lo resuelve | Doc |
|---|---|---|---|
| El catálogo modela lo que las herramientas exportan, no lo que la empresa piensa | **Blueprints definidos por el usuario** | El modelo de datos se declara: qué tipos existen, qué propiedades y qué relaciones | [blueprints](https://docs.port.io/context-lake/data-model/setup-blueprint/overview/) |
| El mismo dato se carga en varios lugares y se contradice | **Mirror properties** | El valor se lee de la entidad relacionada siguiendo la relación. Se escribe una vez | [mirror](https://docs.port.io/context-lake/data-model/setup-blueprint/properties/mirror-property/) |
| Los datos del catálogo envejecen | **Integraciones Ocean, webhooks y API** | El catálogo se puebla solo desde la herramienta de origen | [ingesta](https://docs.port.io/context-lake/ingestion/overview/) |
| Crear un servicio requiere un ticket y tres días | **Self-service actions** | Un formulario dispara el pipeline que ya existe | [acciones](https://docs.port.io/workflows/actions-and-automations/overview/) |
| El formulario ofrece opciones que el pipeline no soporta | **Inputs de tipo entidad** | Las listas desplegables salen del catálogo, no de constantes del pipeline | [inputs](https://docs.port.io/workflows/build-workflows/self-service-trigger/user-inputs/structure-and-fields/) |
| Las políticas están escritas y nadie sabe quién las cumple | **Scorecards por niveles** | Cada regla se evalúa de forma continua y el nivel es un dato filtrable | [scorecards](https://docs.port.io/governance/standards-and-compliance/overview/) |
| Cada área necesita una vista distinta de lo mismo | **Dashboards y catalog pages** | Vistas por audiencia sobre el mismo grafo | [interfaz](https://docs.port.io/interface-builder/overview/) |
| Un cambio en el catálogo requiere que alguien lo note | **Automations** | Disparadores sobre cambios de entidad | [automations](https://docs.port.io/workflows/actions-and-automations/overview/) |
| En una consultora, un cliente no puede ver a otro | **RBAC por equipo y por blueprint** (*role-based access control*, control de acceso basado en roles) | Permisos sobre el modelo de datos | [permisos](https://docs.port.io/api-reference/update-a-blueprints-permissions/) |
| Un agente de IA (inteligencia artificial) sin contexto es peligroso | **Context Lake, MCP, guardrails** | Ver la sección 8 | [Port AI](https://docs.port.io/port-ai/overview/) |

> 📸 **Figura 7.1 — Vista general del portal.** Captura de la pantalla de inicio de la organización de demostración, con el menú lateral visible: catálogo, autoservicio, scorecards, tableros. Sirve para que el resto de la sección tenga dónde ubicarse.

## 7.3 Modelo de datos

Tres primitivas, y todo lo demás se construye encima.

| Primitiva | Qué es | Analogía | Doc |
|---|---|---|---|
| **Blueprint** | Definición de un tipo: propiedades y relaciones | Clase, o tabla | [blueprints](https://docs.port.io/context-lake/data-model/setup-blueprint/overview/) |
| **Entidad** | Instancia concreta de un blueprint | Objeto, o fila | [modelo de datos](https://docs.port.io/context-lake/data-model/configure-data-model/) |
| **Relación** | Vínculo tipado entre dos blueprints | Clave foránea | [relaciones](https://docs.port.io/context-lake/data-model/setup-blueprint/relate-blueprints/) |

> 📸 **Figura 7.2 — El grafo del modelo de datos.** Captura de la vista de modelo de datos de la organización de demostración, con los blueprints y las flechas de relación entre ellos. Es la imagen que hace concreto todo lo anterior: se ve que cliente, proyecto, servicio y squad son tipos declarados, no tablas de una herramienta.

Los tipos de propiedad son la parte que decide qué se carga a mano y qué no:

| Tipo | Origen del valor | Ejemplo | Doc |
|---|---|---|---|
| Normal | Ingesta o formulario | `tier: tier-2` | [propiedades](https://docs.port.io/context-lake/data-model/setup-blueprint/properties/overview/) |
| **Mirror** | Se lee de una entidad relacionada, siguiendo la relación | El nombre del cliente sale de `proyecto.cliente` | [mirror](https://docs.port.io/context-lake/data-model/setup-blueprint/properties/mirror-property/) |
| **Calculated** | Se computa con una expresión sobre otras propiedades | Título legible derivado del nombre técnico | [calculation](https://docs.port.io/context-lake/data-model/setup-blueprint/properties/calculation-property/) |
| Aggregation | Agrega sobre entidades relacionadas | Cantidad de PRs abiertas de un repositorio | [aggregation](https://docs.port.io/context-lake/data-model/setup-blueprint/properties/aggregation-property/) |

> 📸 **Figura 7.3 — Una entidad y sus propiedades.** Captura de la página de un servicio concreto, con las propiedades normales y las mirror señaladas por separado. La mirror conviene marcarla con una flecha hacia la entidad de la que se lee: es lo que hace entender que ese dato no se cargó ahí.

## 7.4 Acciones de autoservicio

Dos mitades: un **formulario** —esquema JSON con validaciones, valores por defecto y campos de tipo entidad ([user inputs](https://docs.port.io/workflows/build-workflows/self-service-trigger/user-inputs/structure-and-fields/))— y un **backend** que lo ejecuta ([action nodes](https://docs.port.io/workflows/build-workflows/action-nodes/configuration-and-outputs/)).

| Backend | Qué hace | Doc |
|---|---|---|
| Integración con GitHub | Dispara un workflow de GitHub Actions | [github](https://docs.port.io/workflows/build-workflows/action-nodes/integration-actions/github/) |
| Integración con GitLab | Dispara un pipeline de GitLab | [gitlab](https://docs.port.io/workflows/build-workflows/action-nodes/integration-actions/gitlab/) |
| Webhook | Llama a un endpoint propio, por ejemplo un flujo de n8n | [webhook](https://docs.port.io/workflows/build-workflows/action-nodes/webhook/) |
| Kafka | Publica el pedido en un tópico que alguien consume | [kafka](https://docs.port.io/workflows/build-workflows/action-nodes/kafka/) |
| Agentes gestionados | Delega el trabajo a un agente de IA con límites declarados | [claude managed agents](https://docs.port.io/workflows/build-workflows/action-nodes/integration-actions/claude-managed-agents/) |

Referencia general de acciones y automatizaciones: [actions and automations](https://docs.port.io/workflows/actions-and-automations/overview/).

> 📸 **Figura 7.4 — El formulario, y su ejecución.** Dos capturas en una: a la izquierda, el formulario de creación de servicio con sus ocho campos y una lista desplegable abierta mostrando que las opciones salen del catálogo; a la derecha, la página de ejecución con los pasos reportados por el pipeline. Es el par de imágenes que resume toda la clase.

## 7.5 Scorecards

Reglas agrupadas en niveles sobre un blueprint. Cada regla es una condición sobre propiedades o relaciones. El nivel se calcula de forma continua y se expone como una propiedad más: filtrable, graficable y utilizable como condición de otra automatización.

| Tema | Doc |
|---|---|
| Qué son y para qué sirven | [overview](https://docs.port.io/governance/standards-and-compliance/overview/) |
| Anatomía: reglas, niveles, condiciones | [concepts and structure](https://docs.port.io/governance/standards-and-compliance/concepts-and-structure/) |
| Crearlos y editarlos | [manage scorecards](https://docs.port.io/governance/standards-and-compliance/manage-scorecards/) |
| Ejemplos de uso | [scorecard use cases](https://docs.port.io/governance/standards-and-compliance/examples/scorecard-use-cases/) |

> 📸 **Figura 7.5 — El scorecard, desde los dos lados.** Arriba, el gráfico de torta del tablero con la distribución por nivel; abajo, la pestaña de scorecard de un servicio concreto con las doce reglas y las que no cumple marcadas. La primera es la vista de quien decide, la segunda la de quien tiene que arreglarlo.

## 7.6 Integraciones

El framework de integraciones se llama **Ocean**. Cada integración declara un *mapping*: qué recurso de la herramienta origen se convierte en qué entidad de qué blueprint, con expresiones `jq` para transformar campos. El mapping es el artefacto que conviene versionar en Git: ahí vive la decisión de qué entra al catálogo y con qué forma.

| Tema | Doc |
|---|---|
| Panorama de métodos de ingesta | [ingestion overview](https://docs.port.io/context-lake/ingestion/overview/) |
| Integraciones nativas (Ocean) | [native integrations](https://docs.port.io/context-lake/ingestion/ingest-data-into-port/native-integrations/overview/) |
| Configurar el mapping | [configure mapping](https://docs.port.io/context-lake/ingestion/configure-mapping/overview/) |
| Ingesta por webhook | [webhooks](https://docs.port.io/context-lake/ingestion/ingest-data-into-port/webhook/ingest-via-webhooks-overview/) |
| Ingesta por API | [API](https://docs.port.io/context-lake/ingestion/ingest-data-into-port/api/ingest-via-api-overview/) |
| Integraciones propias | [custom integration](https://docs.port.io/context-lake/ingestion/ingest-data-into-port/custom-integration/overview/) |

> 📸 **Figura 7.6 — El mapping, en YAML.** Captura del editor de mapping de la integración de GitHub, con un bloque `jq` visible. Es la imagen que muestra que el catálogo no se llena a mano: hay una regla declarada que dice qué entra y con qué forma.

## 7.7 Capturas: qué hace falta

🟡 **Pendiente — las seis figuras.** Ninguna se puede tomar antes del ensayo, porque tienen que salir de la organización de demostración con datos cargados. Se toman todas en la misma sesión, después del ensayo completo.

| Figura | Pantalla | Qué tiene que verse |
|---|---|---|
| 6.1 | Inicio del portal | El menú lateral completo, para ubicar lo demás |
| 6.2 | Modelo de datos | El grafo de blueprints con sus relaciones |
| 6.3 | Página de un servicio | Propiedades normales y mirror, diferenciadas |
| 6.4 | Formulario y ejecución | Una lista desplegable abierta; los pasos reportados |
| 6.5 | Tablero y scorecard | La torta por nivel; las reglas incumplidas de un servicio |
| 6.6 | Editor de mapping | Un bloque `jq` legible |

Reglas para las capturas: solo de la organización de demostración, recortadas al área relevante, y sin barra de navegador ni pestañas abiertas que muestren otra cosa. **Bloquea:** la versión final del apunte y las slides 38 a 41b.

---

# 8. Era agéntica

El escalón 6 de la escalera de la sección 6.5. Se trata aparte porque es el único que todavía no tiene la evidencia que tienen los otros cinco, y porque es donde más se confunde una capacidad con una promesa.

## 8.1 Por qué un agente necesita contexto estructurado

Un modelo de lenguaje grande (LLM, *large language model*) puede escribir código. Lo que no puede es saber, por sí solo, qué servicios existen en una empresa, quién los opera, de cuál depende cuál, cuál es crítico, cuál está deprecado y cuál tiene tráfico de producción a esta hora. Esa información no está en el modelo: está en los sistemas de la organización, o en la cabeza de la gente.

La formulación de Port es directa:

> "when AI is introduced to your engineering environments without context, such as knowledge about your application architecture, dependencies, or ownership teams, it can't act safely."
> — [Zohar Einy, *Agentic Engineering: Evolution of Developer Portals*, port.io, 2025](https://www.port.io/blog/port-agentic-engineering-platform)
>
> *"cuando se introduce IA en los entornos de ingeniería sin contexto —sin conocimiento de la arquitectura de la aplicación, sus dependencias o los equipos que la poseen— no puede actuar de forma segura."*

Es la misma afirmación que la sección 4.1, llevada a su conclusión. Una empresa cuya plataforma es implícita —donde la relación entre un recurso y su dueño vive en la memoria de tres personas— **no tiene nada que darle a un agente**. Un catálogo estandarizado y poblado automáticamente sí lo tiene.

## 8.2 De catálogo a fuente de contexto

El mismo grafo que sirve para que una persona encuentre un servicio sirve para darle contexto a un agente que actúa sobre él. Eso es lo que Port llama **Context Lake** ([docs.port.io](https://docs.port.io/context-lake/overview/)), y la tesis detrás del renombre.

El protocolo que estandarizó cómo un agente consume ese contexto es **MCP** (*Model Context Protocol*, protocolo de contexto para modelos). Un portal que lo expone le da al agente una forma tipada de preguntar "qué servicios dependen de esta base de datos" en lugar de adivinar.

**Por qué importa que sea un estándar abierto.** MCP lo publicó Anthropic en noviembre de 2024 y en diciembre de 2025 lo donó a la **Agentic AI Foundation (AAIF)**, una entidad bajo la Linux Foundation cofundada por Anthropic, Block y OpenAI, con apoyo de Google, Microsoft, AWS, Cloudflare y Bloomberg. Sus otros dos proyectos fundadores son *goose* (Block) y *AGENTS.md* (OpenAI) ([Linux Foundation, comunicado](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation); [blog de MCP](https://blog.modelcontextprotocol.io/posts/2025-12-09-mcp-joins-agentic-ai-foundation/)).

Es el mismo patrón que la sección 4.2: **una capacidad que depende de un proveedor es una dependencia; una que depende de un estándar gobernado por una fundación neutral es una abstracción.** Que competidores directos cofunden la misma fundación es la señal de que el protocolo va a sobrevivir a cualquiera de ellos.

| Recurso | Qué es |
|---|---|
| [modelcontextprotocol.io](https://modelcontextprotocol.io/) | Sitio y documentación oficiales del protocolo |
| [Especificación](https://modelcontextprotocol.io/specification/) | El estándar en sí: transporte, primitivas, autorización |
| [Agentic AI Foundation](https://agenticaifoundation.org/) | La fundación que lo aloja, con sus proyectos y su gobernanza |
| [Linux Foundation — comunicado de formación](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation) | Quiénes la fundan y con qué alcance |
| [GitHub Blog — qué significa para quien desarrolla](https://github.blog/open-source/maintainers/mcp-joins-the-linux-foundation-what-this-means-for-developers-building-the-next-era-of-ai-tools-and-agents/) | Lectura de la donación desde fuera de Anthropic |

## 8.3 Guardrails

El contexto sin límites es la mitad peligrosa. Port plantea tres pilares —Context Lake, guardrails e interfaz de colaboración humano-agente— y el argumento para el segundo es de riesgo: un agente con acceso y sin restricciones puede destruir producción.

Reaparece aquí algo de la sección 5.2: **las acciones de autoservicio son la superficie segura**. Una acción tiene un esquema de entrada validado, permisos, un backend fijo y una traza de ejecución. Darle a un agente una acción de autoservicio es cualitativamente distinto de darle una credencial de administrador: la acción define qué puede hacer, con qué parámetros y qué queda registrado.

El mismo mecanismo que se construyó para que una persona no tuviera que abrir un ticket resulta ser el mecanismo para que un agente no pueda hacer cualquier cosa.

**Qué dice la literatura de seguridad.** Este no es territorio de opinión de proveedores: hay cuerpos normativos y comunitarios que ya catalogaron los riesgos.

| Fuente | Qué aporta |
|---|---|
| [OWASP — Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) | Las diez categorías de riesgo de sistemas que planifican, recuerdan, llaman herramientas y actúan con autoridad delegada |
| [OWASP — Top 10 for LLM Applications](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/) | El riesgo **Excessive Agency** es exactamente el de esta sección: darle a un modelo más capacidad de acción de la que su tarea requiere |
| [NIST — AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) | Marco voluntario del organismo de estándares estadounidense, con cuatro funciones: gobernar, mapear, medir y gestionar |
| [MCP — Security best practices](https://modelcontextprotocol.io/docs/2026-07-28/tutorials/security/security_best_practices) | Las prácticas al nivel del protocolo: autorización, validación de tokens, prohibición de reenviarlos |
| [Cloud Security Alliance — Agentic MCP security](https://labs.cloudsecurityalliance.org/agentic/agentic-mcp-security-best-practices-v1/) | Guía de despliegue: aislamiento, identidad por solicitud, registros curados, auditoría |
| [Red Hat — riesgos y controles de MCP](https://www.redhat.com/en/blog/model-context-protocol-mcp-understanding-security-risks-and-controls) | Lectura práctica de los mismos controles, con ejemplos |

El punto que estas fuentes comparten y que conviene retener: **el control no va en el modelo, va en la superficie de acción.** Un agente se acota decidiendo qué herramientas ve, con qué identidad las llama, qué política se evalúa antes de ejecutar y qué evidencia queda después. Es lo mismo que una acción de autoservicio bien definida, y por eso una organización que ya tiene sus acciones modeladas tiene la mitad del trabajo hecho.

⚠️ Una precaución sobre los enlaces de esta tabla: los documentos de OWASP y la especificación de MCP se versionan y sus URLs cambian entre revisiones. Conviene entrar por las portadas —[genai.owasp.org](https://genai.owasp.org/) y [modelcontextprotocol.io](https://modelcontextprotocol.io/)— si un enlace directo deja de responder.

## 8.4 Qué tiene que ser cierto

| Condición | Por qué |
|---|---|
| El catálogo se puebla solo | Un agente actuando sobre datos de hace tres meses es peor que ningún agente |
| El modelo de datos es explícito | Sin tipos y relaciones, el agente recibe texto y adivina |
| Las acciones tienen esquema y permisos | Es lo que convierte una capacidad en una superficie acotada |
| Todo queda auditado | Sin traza no hay forma de revisar una decisión automática |
| Hay una persona en el circuito donde importa | Los límites se definen antes, no después del incidente |

Las cinco son, palabra por palabra, las condiciones de una plataforma bien estandarizada. Ninguna es específica de la IA.

## 8.5 Nota del docente: cómo leer esta sección

Esta es la parte del apunte que menos evidencia independiente tiene, y la que más rápido va a envejecer. Se las dejo con una advertencia sobre cómo mirar las fuentes, porque es una habilidad que les va a servir mucho más allá de este tema.

**Cuando un proveedor publica el problema y la solución, lean la fuente original.** El texto de Port que citamos más arriba —[*Agentic Engineering: Evolution of Developer Portals*](https://www.port.io/blog/port-agentic-engineering-platform)— es un buen artículo y su argumento central me parece correcto. También es el blog de una empresa que vende exactamente lo que ese argumento vuelve necesario. Las dos cosas son ciertas a la vez, y ninguna invalida a la otra: lo que cambia es el nivel de verificación que les debo pedir.

**El caso concreto: el dato del 95%.** Ese artículo cita un reporte del MIT según el cual el 95% de los pilotos de IA en empresas no dio retorno durante 2025. La cifra circuló por todos lados. Cuando uno va a buscarla, encuentra esto:

| Qué se dice | Qué hay detrás |
|---|---|
| "Un estudio del MIT" | Un reporte de industria del *Project NANDA*, del MIT Media Lab. No es investigación académica revisada por pares |
| "95% de los pilotos fracasan" | Basado en 52 entrevistas, 153 encuestas y 300 despliegues públicos analizados |
| Se cita como dato duro | El conjunto de datos completo no se publicó, y la metodología recibió críticas |

Referencias para que lo vean ustedes mismos: la [cobertura de Forbes](https://www.forbes.com/sites/jasonsnyder/2025/08/26/mit-finds-95-of-genai-pilots-fail-because-companies-avoid-friction/) y una [copia del reporte en PDF](https://cloudelligent.com/wp-content/uploads/2026/02/v0.1_State_of_AI_in_Business_2025_Report.pdf) —alojada por un tercero, que ya es parte del problema: un dato repetido miles de veces cuya fuente primaria no tiene una URL estable—.

Mi posición: **no uso ese número.** No porque lo crea falso, sino porque no lo puedo verificar, y un dato que no puedo defender si alguien me lo discute no me sirve para sostener un argumento.

**Lo que sí sostengo.** Que un catálogo sea condición necesaria para operar agentes con seguridad no lo vuelve condición suficiente, ni prueba que operar agentes sea buena idea en un caso dado. El argumento defendible es más modesto y más sólido:

> *La estandarización que hace falta para automatizar es la misma que hace falta para incorporar agentes. Una organización que la tiene está en mejor posición, haga o no haga IA.*

Esa frase no necesita ninguna cifra para sostenerse, y es la que les pido que se lleven. Si dentro de dos años la ola agéntica resultó menos de lo prometido, la sección 6 de este apunte sigue siendo verdadera; si resultó más, también.

**Una última cosa, sobre esta clase.** Yo trabajo en una consultora que implementa estas plataformas, y la demostración que van a ver la construimos nosotros sobre un producto comercial. Eso me da ejemplos reales que de otro modo no tendrían, y también un sesgo. Contrasten lo que digo con las fuentes neutrales que están en la sección 11 —CNCF, DORA, OWASP, NIST, Linux Foundation— y, sobre todo, con lo que vean cuando les toque trabajar.

---

# 9. Límites y crítica

Platform Engineering tiene adopción proyectada masiva y evidencia mixta. Las dos cosas a la vez.

## 9.1 Adopción

| Dato | Fuente |
|---|---|
| Para 2026, el 80% de las grandes organizaciones de ingeniería tendrán equipos de platform engineering, contra 45% en 2022 | [Gartner](https://www.gartner.com/en/infrastructure-and-it-operations-leaders/topics/platform-engineering) |
| 70% de los encuestados reporta plataformas de al menos 3 años; automatización, productividad y procesos estandarizados son los tres casos de uso principales | [Puppet, State of DevOps Report 2024](https://www.puppet.com/blog/state-devops-report-2024) |
| 52% dice que un rol de gestión de producto es crucial para el éxito del equipo de plataforma | [Puppet, 2024](https://www.puppet.com/blog/state-devops-report-2024) |

### Qué dice el segundo dato

Vale desarmarlo, porque es el único lugar del apunte donde la tesis central aparece medida en lugar de argumentada.

Puppet encuestó a organizaciones que ya tienen equipos de plataforma —el 70% con plataformas de al menos tres años— y les preguntó **qué problemas les resuelve la plataforma**. No qué esperaban de ella ni qué les gustaría: qué resuelve, con la plataforma ya funcionando. Las tres respuestas más frecuentes fueron:

| # | Respuesta | Qué significa |
|---|---|---|
| 1 | Automatización | Tareas que antes se hacían a mano ahora no se hacen |
| 2 | Productividad | Los equipos entregan más, o entregan lo mismo con menos fricción |
| 3 | **Procesos estandarizados** | Las operaciones comunes se hacen de una sola forma en toda la organización |

El tercero es el que importa para este apunte, por dos motivos.

**Primero, porque contradice la intuición.** Quien se acerca a esta disciplina desde afuera supone que una plataforma sirve para desplegar más rápido: una ganancia de velocidad. Que "procesos estandarizados" aparezca al nivel de la automatización y la productividad dice otra cosa — que buena parte del valor percibido no está en hacer lo mismo más rápido, sino en **que deje de hacerse de cinco formas distintas**.

**Segundo, porque es la sección 6 medida por terceros.** Ahí el argumento va de la estandarización a la automatización: no se puede automatizar un proceso cuyos pasos cambian según quién lo ejecute. Este dato muestra el mismo par, pero visto desde el otro extremo: las organizaciones que ya recorrieron el camino reportan las dos cosas juntas, la automatización y el estándar, como si fueran una sola. Es coherente con el argumento, aunque no lo demuestra: una encuesta de percepción registra lo que la gente cree que le pasó, no una relación causal.

Y una advertencia sobre la fuente, que vale para todo este apunte: el reporte lo publica Puppet, un proveedor del rubro. El dato es plausible y es consistente con el resto, pero no tiene el peso de un estudio con metodología publicada como los de DORA.

## 9.2 Evidencia en contra

El reporte DORA 2024 encontró un resultado incómodo para la narrativa de la industria:

> "Utilizing an internal developer platform improves individual productivity, team performance, and overall organizational performance. However, it can also lead to decreased change stability and throughput, requiring careful implementation focused on developer independence."
> — [DORA, Accelerate State of DevOps Report 2024](https://dora.dev/research/2024/dora-report/)
>
> *"Usar una plataforma interna de desarrollo mejora la productividad individual, el desempeño del equipo y el desempeño organizacional general. Sin embargo, también puede llevar a una menor estabilidad de los cambios y a un menor rendimiento de entrega, por lo que exige una implementación cuidadosa, centrada en la independencia de quien desarrolla."*

Cobertura secundaria cita caídas del orden del 8% en throughput —el rendimiento de entrega: cuánto llega a producción y cada cuánto— y 14% en estabilidad de cambios. Esas cifras no se pudieron verificar en la página pública de DORA y se citan como reportadas, no como medidas.

### Cómo una plataforma frena lo que venía a acelerar

El resultado suena contradictorio hasta que se mira el mecanismo. Tres formas concretas, y las tres se introducen con buenas intenciones:

| Mecanismo | Cómo se instala | Qué produce |
|---|---|---|
| Capas de aprobación | "Ya que todos los despliegues pasan por la plataforma, aprovechemos para revisarlos" | La plataforma se vuelve el lugar natural para poner controles. Cada control agrega espera, y la espera agranda el lote |
| Entregas por lotes | La plataforma publica versiones y los equipos esperan la próxima para obtener lo que necesitan | Se vuelve a desplegar de a mucho y cada tanto, que es el ciclo de la sección 1.1 |
| Estructuras rígidas | El camino soportado cubre el caso común y nada más | Todo caso que no encaja se negocia con el equipo de plataforma. La cola vuelve |

Los tres tienen la misma raíz: **un punto único por el que pasa todo es, por construcción, un lugar cómodo donde poner controles.** La plataforma no frena porque sea mala; frena porque es el cuello por el que ahora pasa la organización entera, y cada cosa que se le cuelga encima la angosta.

### Qué es autoservicio real

*Developer independence* es lo que DORA señala como condición, y se traduce en algo verificable: que quien pide una capacidad la obtenga **sin depender de la decisión ni del calendario de otra persona**. Cuatro preguntas alcanzan para distinguirlo de un formulario que abre un ticket:

| Pregunta | Autoservicio real | Ticket con otra cara |
|---|---|---|
| ¿Qué pasa cuando aprieto el botón? | La capacidad se aprovisiona | Alguien recibe una notificación |
| ¿Cuánto tardo en saber el resultado? | Minutos, y el estado es visible mientras tanto | Depende de cuándo lo miren |
| ¿Necesito saber a quién le llega? | No. No le llega a nadie | Sí, y conviene conocerlo |
| Si sale mal, ¿lo puedo reintentar o deshacer? | Sí, con la misma interfaz | Hay que pedir otra cosa |

La aprobación humana no está prohibida, y en operaciones de alto impacto corresponde. Lo que la evidencia castiga es la **aprobación por defecto**: exigirla para todo, incluido lo reversible y lo de bajo impacto. El criterio práctico es poner la aprobación donde el blast radius —cuánto se rompe si sale mal— la justifica, y en ningún otro lado.

### Qué es el principio de opcionalidad

Es el cuarto principio de la sección 2.5: **el camino soportado es conveniente, no obligatorio**. Un equipo puede resolver por fuera de la plataforma, y si lo hace, asume el costo de mantener lo suyo — es el *off-road* de Netflix de la sección 4.5.

Se suele leer como una concesión blanda, y es lo contrario: es un mecanismo de control de calidad sobre la plataforma misma.

| Con opcionalidad | Sin opcionalidad |
|---|---|
| La adopción es voluntaria, así que mide si el camino sirve | Todos cumplen, y la adopción no mide nada |
| Un caso que no encaja se resuelve por afuera, sin frenar a nadie | Un caso que no encaja se convierte en un pedido al equipo de plataforma |
| El equipo de plataforma ve dónde pierde y corrige | El equipo de plataforma se entera tarde, o nunca |

**El hallazgo de DORA es ese principio medido en producción.** Las organizaciones que impusieron la plataforma como paso obligatorio obtuvieron lo que el principio predice: los equipos dejaron de poder avanzar solos, la cola se trasladó del área de operaciones al equipo de plataforma, y el rendimiento de entrega bajó. Lo que empeoró no fue tener una plataforma: fue volverla obligatoria sin haberla hecho, antes, mejor que la alternativa.

## 9.3 Cómo se mide que funciona

| Señal | Qué indica |
|---|---|
| Tiempo desde la idea hasta el primer despliegue | La medida más directa del golden path |
| Porcentaje de servicios nuevos creados por el portal | Adopción voluntaria |
| Distribución del scorecard en el tiempo | Si el estándar sube o solo se mide |
| Métricas DORA por equipo | Si la plataforma acelera o frena |
| Encuesta de experiencia de desarrollo | Lo que ninguna métrica automática captura |

---

# 10. Glosario

Siglas y términos, en orden alfabético.

| Término | Definición |
|---|---|
| AAIF | *Agentic AI Foundation*: entidad de la Linux Foundation que aloja MCP, goose y AGENTS.md |
| API | *Application programming interface*: interfaz por la que un sistema le pide algo a otro |
| Blueprint | Definición de un tipo de entidad: sus propiedades y relaciones |
| BUSL | *Business Source License*: licencia de fuente disponible; no califica como código abierto |
| CALMS | Cultura, automatización, lean, medición, compartir. Acrónimo divulgado de DevOps |
| Carga cognitiva | Cantidad de información que un equipo debe sostener para trabajar |
| Catálogo de software | Inventario relacionado de lo que la organización opera |
| CI / CD | Integración continua y entrega continua |
| CNCF | *Cloud Native Computing Foundation*: fundación que aloja Kubernetes y el ecosistema cloud-native |
| Context Lake | Nombre de Port para su catálogo, en clave de contexto para agentes |
| Criterio binario | Scorecard con un único veredicto de cumple o no cumple. Con muchas reglas, deja de informar |
| DORA | *DevOps Research and Assessment*: programa de investigación sobre desempeño de entrega de software |
| Entidad | Instancia concreta de un blueprint |
| Full cycle developer | Modelo de Netflix: el mismo equipo diseña, construye, prueba, despliega y opera sus servicios |
| Golden path | Camino soportado y documentado para una tarea común |
| IaC | *Infrastructure as code*: infraestructura descripta en archivos versionados |
| IAM | *Identity and Access Management*: gestión de identidades y accesos |
| IDP (platform) | *Internal Developer Platform*: las capacidades que aprovisionan y operan |
| IDP (portal) | *Internal Developer Portal*: la interfaz sobre esas capacidades |
| Ley de Conway | La arquitectura de un sistema copia la estructura de comunicación de quien lo construye |
| LLM | *Large language model*: modelo de lenguaje grande |
| MCP | *Model Context Protocol*: estándar para que un agente consuma contexto y herramientas |
| Mirror property | Propiedad cuyo valor se lee de una entidad relacionada |
| Ocean | Framework de integraciones de Port |
| Off-road | Salirse del camino soportado. En el modelo de Netflix es legítimo, y tiene costo |
| OIDC | *OpenID Connect*: protocolo de identidad federada; permite autenticar pipelines sin credenciales fijas |
| OPA | *Open Policy Agent*: motor de políticas como código |
| Orquestador de plataforma | Componente que ejecuta el aprovisionamiento; vive debajo del portal |
| OSI | *Open Source Initiative*: mantiene la definición de referencia de código abierto |
| Paved road | Camino pavimentado: el conjunto de herramientas soportadas, en terminología de Netflix |
| Proceso cerrado | Proceso con inicio, final y estado observable |
| RBAC | *Role-based access control*: control de acceso basado en roles |
| SaaS | *Software as a service*: el proveedor opera el software y se paga por uso |
| Scaffolding | Generación automática de un proyecto desde una plantilla |
| Scorecard | Conjunto de reglas evaluadas de forma continua sobre entidades |
| Shadow ops | Antipatrón: la tarea de infraestructura no desaparece, se concentra informalmente |
| Shift left | Mover responsabilidades hacia etapas tempranas y hacia quien desarrolla |
| SLI | *Service level indicator*: la métrica que se mide |
| SLO | *Service level objective*: el objetivo declarado sobre esa métrica |
| SRE | *Site reliability engineering*: ingeniería de confiabilidad |
| Stream-aligned team | Equipo alineado a un flujo de valor |
| TLS | *Transport layer security*: cifrado del tráfico en tránsito |
| TVP | *Thinnest viable platform*: la plataforma mínima que acelera de forma medible |
| X-as-a-Service | Modo de interacción donde una capacidad se consume sin coordinar |

---

# 11. Fuentes

## Primarias

| Fuente | Tipo | Uso |
|---|---|---|
| [Conway, *How Do Committees Invent?* (1968)](https://www.melconway.com/Home/Committees_Paper.html) | Artículo | Ley de Conway |
| [*A Conversation with Werner Vogels*, ACM Queue (2006)](https://queue.acm.org/detail.cfm?id=1142065) | Entrevista | Origen de "you build it, you run it" |
| [Bottcher, *What I Talk About When I Talk About Platforms* (2018)](https://martinfowler.com/articles/talk-about-platforms.html) | Ensayo | Definición de plataforma digital; costo de la dependencia entre equipos |
| [CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/) | White paper | Definiciones, siete atributos, trece dominios |
| [CNCF Platform Engineering Maturity Model](https://tag-app-delivery.cncf.io/whitepapers/platform-eng-maturity-model/) | White paper | Niveles de madurez |
| [DORA, State of DevOps 2024](https://dora.dev/research/2024/dora-report/) | Reporte | Evidencia sobre efectos de plataformas internas |
| ⚠️ [Puppet, State of DevOps Report 2024](https://www.puppet.com/blog/state-devops-report-2024) | Reporte | Madurez y casos de uso de equipos de plataforma. Publicado por un proveedor |
| [Westrum, *A typology of organisational cultures* (2004)](https://qualitysafety.bmj.com/content/13/suppl_2/ii22) | Paper revisado por pares | Tipología cultural que DORA adoptó |
| [Spotify Engineering, *Golden Paths* (2020)](https://engineering.atspotify.com/2020/08/how-we-use-golden-paths-to-solve-fragmentation-in-our-software-ecosystem) | Blog de ingeniería | Origen del término; *development by rumor* |
| [Team Topologies — Key concepts](https://teamtopologies.com/key-concepts) | Sitio del libro | Carga cognitiva, tipos de equipo |
| [Team Topologies — Platform Engineering](https://teamtopologies.com/platform-engineering) | Sitio del libro | Thinnest Viable Platform |

## Libros

| Título | Autores | Relevancia |
|---|---|---|
| *Team Topologies* (2019) | Skelton, Pais | Base organizacional de toda la disciplina |
| *Accelerate* (2018) | Forsgren, Humble, Kim | Evidencia empírica de las prácticas de DevOps |
| *The DevOps Handbook* (2016) | Kim, Humble, Debois, Willis | Sistematización de las prácticas |
| *The Phoenix Project* (2013) | Kim, Behr, Spafford | Novela; el problema organizacional contado como relato |
| *Site Reliability Engineering* (2016) | Beyer y otros — [texto completo libre](https://sre.google/books/) | Confiabilidad como disciplina |

> **Criterio de lectura.** Buena parte de la divulgación sobre esta disciplina la publican proveedores que venden la solución que describen. No la vuelve falsa, pero cambia cómo se lee: un dato de un proveedor se verifica antes de repetirse, y una definición suya se contrasta con la de una fuente neutral. Las filas marcadas ⚠️ son de origen comercial.

## Divulgación y comunidad

| Recurso | Tipo |
|---|---|
| [Netflix Technology Blog — *Full Cycle Developers at Netflix* (2018)](https://medium.com/netflix-techblog/full-cycle-developers-at-netflix-a08c31f83249) | El paved road contado por quien lo opera |
| [InfoQ — cobertura del modelo de Netflix](https://www.infoq.com/news/2018/06/netflix-full-cycle-developers/) | Lectura editorial del mismo texto |
| [McKinsey Digital — *Platform as code*](https://medium.com/digital-mckinsey/platform-as-code-reference-architectures-to-simplify-developer-platforms-f2fb48e0c874) | Origen de la arquitectura de referencia de cinco planos |
| [platformengineering.org/reports](https://platformengineering.org/reports) | Los diagramas completos por nube. Requiere registro |
| [DevOps Topologies](https://web.devopstopologies.com/) | Catálogo abierto de patrones y antipatrones organizacionales |
| [Model Context Protocol](https://modelcontextprotocol.io/) · [especificación](https://modelcontextprotocol.io/specification/) | El estándar por el que un agente consume contexto y herramientas |
| [Agentic AI Foundation](https://agenticaifoundation.org/) · [comunicado de la Linux Foundation](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation) | La fundación neutral que aloja MCP, goose y AGENTS.md |
| [GitHub Blog — MCP se une a la Linux Foundation](https://github.blog/open-source/maintainers/mcp-joins-the-linux-foundation-what-this-means-for-developers-building-the-next-era-of-ai-tools-and-agents/) | Lectura de la donación desde fuera de quien la hizo |
| [OWASP — Top 10 for Agentic Applications 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) | Riesgos de sistemas que actúan con autoridad delegada |
| [OWASP — Top 10 for LLM Applications](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/) | Incluye *Excessive Agency*, el riesgo central de la sección 8 |
| [NIST — AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) | Marco del organismo de estándares: gobernar, mapear, medir, gestionar |
| [Cloud Security Alliance — Agentic MCP security](https://labs.cloudsecurityalliance.org/agentic/agentic-mcp-security-best-practices-v1/) | Prácticas de despliegue para agentes sobre MCP |
| [Red Hat — riesgos y controles de MCP](https://www.redhat.com/en/blog/model-context-protocol-mcp-understanding-security-risks-and-controls) | Los mismos controles, con ejemplos |
| [Backstage — documentación](https://backstage.io/docs/overview/what-is-backstage) | Modelo de catálogo y plantillas, desde el proyecto mismo |
| [OpenTofu Manifesto](https://opentofu.org/manifesto/) | El fork abierto de Terraform y sus motivos |
| [IT Revolution — revisión de la historia de Flickr](https://itrevolution.com/articles/organizational-learning-and-competitiveness-a-different-view-of-the-allspawhammond-10-deploys-per-day-at-flickr-story/) | Relectura crítica del relato fundacional, quince años después |
| [InfoQ — cobertura de platform engineering](https://www.infoq.com/devops/) | Medio editorial, no de proveedor |
| [USENIX — SREcon, actas y videos](https://www.usenix.org/conferences/byname/925) | Conferencia académico-profesional, archivo abierto |
| [Notas de la charla de 2009](https://tech-talks.code-maven.com/ten-plus-deploys-per-day.html) | Transcripción de las listas de herramientas y cultura |
| [New Relic — *How DevOps Got Its Name*](https://blog.newrelic.com/engineering/devops-name/) | Relato de 2009 |
| ⚠️ [platformengineering.org — *What is platform engineering*](https://platformengineering.org/blog/what-is-platform-engineering) | Artículo de referencia de la comunidad. Sostenido por Humanitec |
| ⚠️ [internaldeveloperplatform.org](https://internaldeveloperplatform.org) | Referencia sobre componentes de IDP. Sostenido por Humanitec |
| ⚠️ [Humanitec — *How to build an IDP*](https://humanitec.com/blog/how-to-build-an-internal-developer-platform) | Arquitectura de referencia de cinco planos |
| [Arquitecturas de referencia, en código abierto: AWS](https://github.com/humanitec-architecture/reference-architecture-aws) · [Azure](https://github.com/humanitec-architecture/reference-architecture-azure) · [GCP](https://github.com/humanitec-architecture/reference-architecture-gcp) | Implementaciones publicadas bajo licencia abierta |
| ⚠️ [The New Stack — *Humanitec: The Golden Path to Platform Engineering*](https://thenewstack.io/humanitec-the-golden-path-to-platform-engineering/) | Definición operativa de golden path. Entrevista a un proveedor |
| ⚠️ [Encore — *Platform Engineering Tools Compared*](https://encore.dev/articles/platform-engineering-tools) | Comparativa de portales y orquestadores. Encore es proveedor del rubro |

## Video

| Recurso | Duración aproximada |
|---|---|
| [Allspaw y Hammond, *10+ Deploys per Day* (Velocity 2009)](https://www.youtube.com/watch?v=LdOe18KhtT4) | 46 min — la charla fundacional |
| [Kelsey Hightower y Kaspar von Grünberg, *Real talk: platform engineering* (PlatformCon 2024)](https://www.youtube.com/watch?v=puxNUkbrCVk) | ~40 min — conversación crítica sobre el estado de la disciplina |
| [PlatformCon — archivo de charlas](https://platformcon.com) | Conferencia anual, con archivo abierto |

## Producto

| Recurso | Uso |
|---|---|
| [docs.port.io](https://docs.port.io) | Conceptos y features de Port |
| ⚠️ [Port — *Agentic Engineering: Evolution of Developer Portals*](https://www.port.io/blog/port-agentic-engineering-platform) | Argumento de portales agénticos, en el blog del proveedor |
| [demo.backstage.io](https://demo.backstage.io) | Backstage navegable, sin registro |
