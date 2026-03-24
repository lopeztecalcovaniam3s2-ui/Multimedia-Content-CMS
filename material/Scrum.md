## Scrum

Para mejorar tu comprensión y ser más precisos, hay un par de matices importantes que debemos entender respecto a Scrum.

### 1. No es una "metodología", es un "marco de trabajo" (Framework)

Una metodología suele ser prescriptiva: te da un conjunto exhaustivo y rígido de instrucciones y procesos paso a paso ("haz A, luego B, y obtendrás C").

Scrum, por el contrario, es un **marco de trabajo ligero**. Te proporciona unas reglas del juego mínimas y estructurales, pero confía en la inteligencia y autoorganización del equipo para decidir *cómo* hacer el trabajo técnico. Está diseñado para adaptarse al contexto, no para dictar cada movimiento. No te dice cómo programar, te dice cómo organizarte para descubrir la mejor forma de hacerlo.

### 2. Ya no es exclusivo del "desarrollo de software"

Aunque sus raíces y su popularidad nacieron en el desarrollo de software en los años 90, hoy en día ha evolucionado. La Guía de Scrum oficial lo define de una manera más universal:

> *Scrum es un marco de trabajo ligero que ayuda a las personas, equipos y organizaciones a generar valor a través de soluciones adaptativas para problemas complejos.*

Hoy en día, Scrum se aplica con éxito en marketing, investigación, diseño de hardware, educación, y operaciones, básicamente en cualquier entorno donde haya alta incertidumbre y el problema sea demasiado complejo para predecirlo todo desde el principio.

------

### Los Cimientos de Scrum

Scrum se basa en el **empirismo** (tomar decisiones basadas en la experiencia, en lo que se observa y no en suposiciones) y en el pensamiento *Lean* (reducir el desperdicio y enfocarse en lo esencial). Esto se sostiene sobre tres pilares:

- **Transparencia:** El trabajo y el estado real del producto deben ser visibles y comprensibles para todos (equipo y negocio). Sin transparencia, no hay confianza.
- **Inspección:** El equipo debe revisar frecuentemente lo que está construyendo y cómo lo está construyendo para detectar problemas a tiempo.
- **Adaptación:** Si en la inspección detectamos que algo no funciona o el mercado cambió, ajustamos el rumbo inmediatamente.

### La Estructura de Scrum (Las reglas del juego)

Para hacer realidad esos pilares, Scrum establece componentes muy claros y limitados:

- **3 Responsabilidades (Roles):** 
  - **Product Owner:** Define el *Qué* (maximiza el valor del producto y prioriza el trabajo).
  - **Developers:** Definen el *Cómo* (los profesionales que construyen el producto).
  - **Scrum Master:** Cuida el *Proceso* (asegura que Scrum se entienda, elimina impedimentos y ayuda al equipo a ser más efectivo).
- **5 Eventos:** El **Sprint** (el ciclo de trabajo, de 1 a 4 semanas, que contiene al resto), *Sprint Planning*, *Daily Scrum*, *Sprint Review* y *Sprint Retrospective*.
- **3 Artefactos:** *Product Backlog* (la lista de todo lo que podría necesitar el producto), *Sprint Backlog* (el plan de trabajo para el Sprint actual) y el *Incremento* (el resultado funcional y de valor que se entrega al final del Sprint).

En resumen: Scrum es un marco de trabajo iterativo e incremental que te ayuda a navegar la complejidad, entregando valor de forma continua mientras aprendes y te adaptas en el camino.

### El Product Owner

Te comparto que el Product Owner (PO) es uno de los roles más cruciales y, curiosamente, uno de los que más se malinterpretan en las organizaciones.

Para resumirlo en un solo concepto: **el Product Owner es el maximizador de valor**. Su objetivo principal no es que el equipo trabaje mucho, sino asegurar que el equipo esté construyendo lo correcto, es decir, el producto debe aportar el mayor beneficio posible al negocio y a los usuarios.

Aquí te detallo sus responsabilidades principales desde la perspectiva más pura del marco de trabajo:

#### 1. Gestión efectiva del Product Backlog

El Product Backlog es la lista viva de todo lo que se necesita para mejorar el producto. El PO es el único dueño de esta lista y es responsable de:

- **Desarrollar y comunicar explícitamente el Objetivo del Producto (Product Goal):** Esta es la meta a largo plazo que da dirección y propósito a todo el equipo.
- **Crear y comunicar claramente los elementos del Product Backlog:** Ya sea en forma de historias de usuario, casos de uso o simples descripciones, el PO debe asegurar que el equipo entienda qué se necesita.
- **Ordenar (Priorizar) los elementos:** El PO decide qué va primero. Esta priorización se basa en el valor de negocio, el riesgo, las dependencias o la retroalimentación del mercado.
- **Asegurar la transparencia:** El Product Backlog debe ser visible, transparente y comprendido por todos. Cualquiera que quiera saber en qué está trabajando el equipo a futuro, solo tiene que mirar esta lista.

*Nota: El PO puede delegar la redacción técnica de estos elementos a los Developers, pero la responsabilidad final de que estén correctos y bien ordenados sigue siendo suya.*

#### 2. Toma de decisiones y Autoridad

Para que el PO tenga éxito, toda la organización debe respetar sus decisiones.

- **Es una única persona, no un comité:** El PO puede representar los deseos de un comité o de múltiples interesados (stakeholders), pero si alguien quiere cambiar la prioridad de un elemento, debe convencer al Product Owner.
- **Es el dueño del "Qué":** Decide qué características se construyen y cuándo se lanzan al mercado.

#### 3. Colaboración y Gestión de Expectativas

El PO es el puente principal entre el negocio y el equipo de desarrollo.

- **Con los Stakeholders (Interesados):** Entiende el mercado, los clientes y las necesidades del negocio para traducirlas en requerimientos valiosos. Gestiona sus expectativas durante la *Sprint Review*.
- **Con los Developers:** Está disponible diariamente para resolver dudas de negocio, aclarar los criterios de aceptación y colaborar sin interrumpir el flujo técnico de trabajo.

------

#### Lo que un Product Owner NO es (Antipatrones comunes)

Desde la trinchera del Scrum Master, siempre busco proteger al equipo de estos escenarios:

- **No es un Jefe de Proyecto tradicional:** No asigna tareas a las personas ni controla sus horarios.
- **No dicta el "Cómo":** El PO dice *qué* problema resolver, pero confía ciegamente en los Developers para decidir *cómo* construir técnicamente la solución.
- **No es un simple "tomador de pedidos":** No se limita a anotar lo que piden los clientes; debe tener el criterio, el conocimiento y la autoridad para decir "No" a peticiones que no alineen con el Objetivo del Producto.

---

### El Scrum Master

Si el Product Owner es el encargado de responder al **"Qué"** (el valor) y los Developers responden al **"Cómo"** (la construcción técnica), el Scrum Master es el guardián del **"Proceso"** y la efectividad del equipo.

Para entenderlo fácilmente, imagina este rol como el de un docente o un facilitador experto: no realiza el trabajo técnico ni toma las decisiones de negocio, pero crea el entorno perfecto, proporciona las herramientas, elimina los obstáculos y guía a las personas para que alcancen su máximo potencial y aprendan a autogestionarse. Es lo que en agilidad llamamos un **Líder Servicial** (*Servant Leader*).

Sus responsabilidades se dividen en tres grandes frentes de servicio:

#### 1. Servicio a los Developers (El Equipo de Desarrollo)

El Scrum Master trabaja mano a mano con quienes construyen el producto para que puedan fluir sin interrupciones.

- **Coach de autogestión:** Ayuda al equipo a organizarse por sí mismos y a ser multifuncionales. No les dice quién debe hacer qué tarea, sino que les enseña a tomar esas decisiones juntos.
- **Eliminador de impedimentos:** Esta es vital. Si a un programador le falta un acceso a una base de datos, si una herramienta se cae, o si hay burocracia frenando el avance, el Scrum Master interviene para remover ese bloqueo inmediatamente para que el equipo no pierda el ritmo.
- **Facilitador de eventos:** Se asegura de que todas las reuniones de Scrum (la *Daily*, la *Retrospective*, etc.) ocurran, sean positivas, productivas y, muy importante, que se mantengan dentro de su límite de tiempo (*timebox*).

#### 2. Servicio al Product Owner (PO)

A veces el PO es un experto en el negocio, pero no domina Scrum. El Scrum Master es su asesor principal.

- **Técnicas de gestión:** Ayuda al PO a encontrar las mejores técnicas para definir el Objetivo del Producto y organizar el *Product Backlog* de forma efectiva.
- **Claridad:** Entrena al equipo completo para que entiendan la importancia de tener historias de usuario o elementos del Backlog claros, concisos y valiosos.
- **Colaboración empírica:** Facilita la colaboración entre el PO y los interesados (stakeholders), asegurando que se tomen decisiones basadas en datos reales y no en suposiciones.

#### 3. Servicio a la Organización

El Scrum Master no solo trabaja con su equipo, también es un agente de cambio organizacional.

- **Liderar la adopción de Scrum:** Capacita y guía a la empresa entera para que entiendan qué es Scrum y cómo funciona el enfoque empírico en problemas complejos.
- **Romper silos:** Ayuda a eliminar las barreras de comunicación que suelen existir entre los equipos de desarrollo y el resto de los departamentos.

------

#### Lo que un Scrum Master NO es (Antipatrones comunes)

Así como protegemos al PO de malas prácticas, también debemos desmitificar al Scrum Master:

- **No es el jefe del equipo:** No contrata, no despide, ni evalúa el desempeño individual. Si actúa como un jefe tradicional que da órdenes, destruye la autoorganización.
- **No es el "secretario" del equipo:** No está ahí solo para agendar reuniones en Zoom, actualizar los tickets en Jira o traer el café. Su rol es estratégico y de coaching.
- **No es la "Policía de Scrum":** Un buen Scrum Master no impone las reglas del marco de trabajo a la fuerza y sin contexto ("¡tienes que estar de pie en la Daily!"). En su lugar, explica el *porqué* detrás de la regla para que el equipo vea el valor de adoptarla.

---

### Los Developers

Hablemos de los verdaderos motores que hacen realidad el producto.

Me gustaría empezar con una pequeña pero muy importante aclaración técnica: en la actualización más reciente de la Guía de Scrum (2020), se eliminó formalmente el término "Development Team" (Equipo de Desarrollo) y ahora se les llama simplemente **Developers** (Desarrolladores).

¿Por qué se hizo este cambio? Para destruir el antipatrón de tener "un equipo dentro de otro equipo". En Scrum solo hay un equipo cohesionado: el **Scrum Team**, compuesto por el Product Owner, el Scrum Master y los Developers. Todos comparten el mismo objetivo.

Aquí te detallo quiénes son y cuáles son sus responsabilidades exactas dentro del marco de trabajo:

#### 1. ¿Quiénes son los Developers?

La palabra "Developer" en Scrum es un término paraguas. **No significa exclusivamente "programador de software".** Un Developer es cualquier profesional que esté trabajando activamente en la creación del incremento del producto durante el Sprint. Dependiendo de tu industria, los Developers pueden ser ingenieros de software, diseñadores UX/UI, analistas de datos, redactores, investigadores, arquitectos o especialistas en marketing. La regla de oro es: **son multifuncionales**. Como grupo, deben tener *todas* las habilidades necesarias para transformar los elementos del Product Backlog en un producto terminado y funcional.

#### 2. Responsabilidades Principales (El "Cómo")

Los Developers son los dueños absolutos de la ejecución técnica. Sus responsabilidades innegociables son:

- **Crear el plan para el Sprint (El Sprint Backlog):** Durante la planificación, ellos (y solo ellos) deciden *cuánto* trabajo pueden asumir para el Sprint y *cómo* van a transformarlo en un incremento funcional.
- **Inculcar la calidad (Definition of Done):** Son responsables de asegurar que cada elemento que construyen cumpla con un estándar de calidad acordado, conocido como la Definición de Terminado (*Definition of Done*). Si no cumple este estándar, no se entrega.
- **Adaptar su plan diariamente:** A través del evento llamado *Daily Scrum*, los Developers inspeccionan su progreso hacia la meta del Sprint (Sprint Goal) y ajustan su plan de trabajo para las siguientes 24 horas.
- **Responsabilidad mutua (Accountability):** Se hacen responsables mutuamente como profesionales. El éxito o el fracaso no recae en un solo individuo, sino en los Developers como unidad.

------

#### Lo que los Developers NO son (Antipatrones comunes)

Para que el equipo alcance un alto rendimiento, debemos evitar estas trampas comunes:

- **No hay jerarquías ni subtítulos:** Dentro de los Developers no hay "Jefes de Desarrollo", "Tech Leads" o "Testers" a los ojos de Scrum. Todos comparten el mismo título de Developer para fomentar la responsabilidad compartida y evitar que alguien diga "ese no es mi trabajo".
- **No son "tomadores de pedidos" pasivos:** No se sientan a esperar que el Product Owner les dicte cada detalle. Deben cuestionar, proponer soluciones técnicas y negociar el alcance si descubren que algo es más complejo de lo estimado.
- **No trabajan en silos:** Aunque cada uno tenga su especialidad, el objetivo es terminar los elementos juntos. Si un desarrollador termina su parte de código, no empieza una tarea nueva si su compañero necesita ayuda para terminar las pruebas de la tarea actual.

Ahora que hemos cubierto a los tres pilares del Scrum Team (Product Owner, Scrum Master y Developers), ¿te gustaría que veamos cómo interactúan en la práctica durante el evento donde arranca todo, el **Sprint Planning**, o hay algún otro concepto que quieras aclarar primero?

---

### El Sprint Planning

El **Sprint Planning** (Planificación del Sprint) es, sin duda, uno de los eventos más críticos. Es aquí donde la estrategia del negocio aterriza en la realidad operativa; es el momento en el que el equipo se alinea y decide a qué se va a comprometer.

Este evento marca el inicio formal del Sprint. Tiene un límite de tiempo (*timebox*) de máximo 8 horas para un Sprint de un mes (suele ser más corto para Sprints de 1 o 2 semanas).

Para que la planificación sea un éxito, la Guía de Scrum (en su actualización más reciente) establece que el equipo debe responder a **tres preguntas clave**. Así es como interactúan los roles en cada una de ellas:

------

#### 1. ¿Por qué es valioso este Sprint? (El Objetivo)

Aquí definimos el propósito. No se trata solo de "sacar tareas", sino de entender qué impacto queremos lograr.

- **El Product Owner (PO):** Toma la iniciativa. Llega a la reunión con el *Product Backlog* priorizado y propone cómo el producto podría incrementar su valor en este Sprint.
- **Los Developers y el PO:** Dialogan, negocian y refinan esa propuesta hasta acordar juntos el **Sprint Goal** (Objetivo del Sprint). Esta es una meta clara y concisa que explica por qué el trabajo de estas semanas vale la pena.
- **El Scrum Master (SM):** Asegura que el equipo no se salte este paso. Facilita la conversación para que el objetivo sea realista, claro y no una simple "lista del supermercado" sin conexión.

#### 2. ¿Qué se puede terminar en este Sprint? (La Selección)

Una vez que sabemos *por qué* trabajamos, decidimos *qué* vamos a construir para lograr ese objetivo.

- **Los Developers:** Evalúan su capacidad real (considerando vacaciones, días festivos o su desempeño histórico) y **son los únicos que deciden** cuántos elementos del *Product Backlog* pueden comprometerse a terminar. Seleccionan las historias o requerimientos de la parte superior de la lista.
- **El Product Owner:** Está ahí para resolver dudas en tiempo real. Si los Developers no entienden un requerimiento o descubren que es demasiado grande, el PO aclara los detalles, ajusta los criterios de aceptación o divide el elemento en partes más pequeñas.
- **El Scrum Master:** Protege a los Developers. Se asegura de que el PO no los presione para aceptar más trabajo del que realmente pueden manejar, fomentando un ritmo sostenible.

#### 3. ¿Cómo se realizará el trabajo elegido? (El Plan)

Ya tenemos el objetivo y los requerimientos. Ahora toca hablar de tecnología y ejecución.

- **Los Developers:** Toman el control absoluto. Descomponen los requerimientos seleccionados en tareas técnicas manejables (generalmente trabajo de un día o menos). Diseñan la arquitectura, deciden cómo van a probar el código y arman su plan de ataque.
- **El Product Owner:** En esta fase, el PO da un paso atrás. Observa y está disponible solo por si los Developers encuentran dependencias o dudas de negocio al desglosar el trabajo. **No dicta cómo deben hacer el trabajo.**
- **El Scrum Master:** Observa la dinámica. Si nota que los Developers están atascados en un debate técnico infinito (parálisis por análisis), interviene para destrabar la conversación y mantener el evento dentro del tiempo establecido.

------

#### El Resultado: El Sprint Backlog

Al terminar la reunión, la suma del **Objetivo del Sprint** + **Los elementos seleccionados** + **El plan de acción técnico** da como resultado el **Sprint Backlog**. A partir de este momento, el equipo tiene foco total.

#### Antipatrones comunes en el Sprint Planning (Lo que evitamos)

Desde las trincheras, te comparto lo que un buen Scrum Master debe corregir inmediatamente en este evento:

- **El PO "empuja" el trabajo:** El PO no le asigna tareas a los Developers ("Tú haces esto, tú haces lo otro"). Los Developers "jalan" el trabajo de la lista basándose en su capacidad.
- **Llegar sin preparación:** Si el *Product Backlog* es un desastre y el PO no lo ordenó antes de la reunión, el Sprint Planning se convierte en una pesadilla de 8 horas tratando de entender qué hacer.
- **Olvidar el Sprint Goal:** Terminar la reunión solo con una lista de 40 tareas aisladas, sin un propósito claro que las una.

---

### Daily Scrum

La **Daily Scrum** (o Scrum Diario) es el latido del corazón del equipo. Como Scrum Master, te confieso que este es el evento que más rápido revela la madurez de un equipo y, al mismo tiempo, el que más se contamina de malas prácticas (como convertirlo en una junta de reporte de estado).

El propósito real de la Daily Scrum es simple pero poderoso: **inspeccionar el progreso hacia el Objetivo del Sprint (Sprint Goal) y adaptar el plan de trabajo (Sprint Backlog) para las siguientes 24 horas.** Tiene una regla de oro inquebrantable: un límite de tiempo (*timebox*) de **máximo 15 minutos**, sin importar el tamaño del equipo.

Así es como interactúan los roles en la práctica real:

#### 1. Los Developers (Los Protagonistas Absolutos)

Este evento es **por y para los Developers**. Ellos son los dueños de la reunión.

- **Autoorganización:** Ellos deciden la estructura y las técnicas de la reunión, siempre y cuando se enfoquen en el progreso hacia el Objetivo del Sprint y produzcan un plan viable para el siguiente día.
- **Sincronización:** Comparten qué descubrieron ayer, qué planean atacar hoy y cómo van a colaborar. ("*Ayer terminé la API, hoy iba a empezar el frontend, pero veo que Juan está atascado con la base de datos, así que hoy me sumaré a ayudarle para cerrar esa historia*").
- **Identificación de bloqueos:** Si algo les impide avanzar (un servidor caído, falta de accesos, dudas técnicas graves), lo levantan aquí para que se resuelva lo antes posible.

#### 2. El Scrum Master (El Coach y Facilitador)

Contrario a la creencia popular, el Scrum Master **no dirige esta reunión**.

- **Enseña, no microgestiona:** Su responsabilidad es enseñar a los Developers a mantener la reunión dentro de los 15 minutos y asegurar que el evento ocurra todos los días.
- **Toma nota de los impedimentos:** Si los Developers mencionan bloqueos organizacionales o externos que no pueden resolver por sí mismos, el Scrum Master se los lleva de tarea para resolverlos fuera de la reunión.
- **Protege el espacio:** Si personas externas al equipo intentan interrumpir o convertir la Daily en una reunión de reporte, el Scrum Master interviene para proteger el enfoque de los Developers.

#### 3. El Product Owner (El Observador Opcional)

La regla aquí suele sorprender a muchos: **el Product Owner no tiene que asistir a la Daily Scrum**, a menos que también esté ejecutando tareas técnicas del Sprint Backlog (es decir, actuando también como Developer).

- **Si asiste:** Debe hacerlo como oyente silencioso. No es el momento para pedir nuevas funcionalidades, cambiar prioridades o pedir explicaciones de por qué alguien va lento.
- **Después de la Daily (El "Meet After"):** Es muy común que, al terminar los 15 minutos oficiales, los Developers le pidan al PO que se quede unos minutos más para aclarar una regla de negocio rápida o un criterio de aceptación sobre la tarea del día.

------

#### Lo que la Daily Scrum NO es (Antipatrones comunes)

Estas son las "luces rojas" que se busca apagar inmediatamente:

- **No es un reporte de estado para el jefe:** Los Developers no le rinden cuentas al Scrum Master ni al PO. Se rinden cuentas *entre ellos mismos*. Si todos miran al Scrum Master mientras hablan, la Daily está rota.
- **No es una reunión para resolver problemas (Troubleshooting):** Si surge un debate técnico profundo sobre cómo arreglar un bug de 45 minutos, el Scrum Master (o cualquier Developer) debe pedir que se "estacione" el tema para discutirlo terminando la Daily, solo con las personas involucradas.
- **No es un cuestionario robótico:** Durante mucho tiempo se popularizaron "las 3 preguntas" (¿Qué hice ayer? ¿Qué haré hoy? ¿Qué me bloquea?). Aunque son útiles para equipos novatos, a menudo hacen que la gente pierda de vista el Objetivo del Sprint para solo justificar en qué invirtieron sus 8 horas de trabajo.

---

### Sprint Review

Se puede decir que la **Sprint Review** (Revisión del Sprint) es el evento donde la magia del empirismo (transparencia, inspección y adaptación) cobra vida frente a los ojos del negocio.

Es muy común que los equipos confundan este evento con una simple "demostración" o presentación unidireccional (el famoso *demo*). Pero en la práctica real, la Sprint Review es **una sesión de trabajo colaborativa** entre el equipo Scrum y las personas interesadas (stakeholders). Su objetivo es inspeccionar el resultado del Sprint (el Incremento) y determinar juntos qué es lo más valioso que podemos hacer a continuación.

Tiene un límite de tiempo (*timebox*) de máximo 4 horas para un Sprint de un mes, y suele ser más corta para Sprints de menor duración.

Así es como interactúan los roles y los invitados durante esta sesión:

#### 1. El Product Owner (El Anfitrión y Estratega)

En este evento, el PO toma la batuta principal hacia el exterior del equipo.

- **Convoca y contextualiza:** Invita a los stakeholders clave (clientes, directores, usuarios finales). Inicia la reunión explicando claramente qué elementos del Product Backlog se lograron terminar (están "Done") y cuáles no se lograron.
- **Proyecta el futuro:** Habla sobre el estado actual del *Product Backlog*. Basado en el progreso del equipo, comparte proyecciones sobre posibles fechas de entrega o hitos futuros.
- **Captura el valor:** Escucha activamente el feedback de los stakeholders al ver el producto funcionando y utiliza esa información para actualizar, agregar o re-priorizar elementos en el Product Backlog.

#### 2. Los Developers (Los Expertos Técnicos)

Ellos son los que construyeron el producto y lo muestran con orgullo, pero también con total honestidad.

- **Comparten la realidad del Sprint:** Explican qué salió bien, qué problemas técnicos o de negocio enfrentaron y cómo lograron resolverlos. Esta honestidad construye mucha confianza con los stakeholders.
- **Demuestran el trabajo terminado:** Muestran el producto funcionando de verdad (nada de simulaciones en PowerPoint). Responden a las preguntas técnicas o funcionales que tengan los asistentes sobre el Incremento.
- **Colaboran en el siguiente paso:** Participan en la discusión sobre qué construir a continuación, aportando su visión sobre qué es técnicamente viable o si han descubierto nuevas herramientas o limitaciones que el negocio deba conocer.

#### 3. El Scrum Master (El Facilitador del Entorno)

Su rol aquí es asegurar que la reunión sea productiva y segura para todos.

- **Alinea las expectativas:** Se asegura de que todos los asistentes entiendan que esto no es una "evaluación de desempeño" ni una reunión para regañar al equipo por lo que no se terminó, sino un espacio para aprender y adaptar.
- **Protege el tiempo y el enfoque:** Si la conversación se desvía hacia detalles técnicos demasiado profundos o discusiones que no aportan a la revisión del producto, interviene sutilmente para reenfocar al grupo y mantenerlos dentro del *timebox*.
- **Fomenta la colaboración:** Anima a los stakeholders a que prueben el producto, hagan preguntas y den feedback real, evitando que la sesión se convierta en un monólogo de los Developers.

------

#### Lo que la Sprint Review NO es (Antipatrones comunes)

Para que este evento realmente genere valor, se evita caer en estas trampas:

- **No es una puerta de aprobación:** El trabajo terminado ya debe cumplir con la "Definición de Terminado" (*Definition of Done*) antes de llegar aquí. El PO no usa esta reunión para "aceptar" o "rechazar" el trabajo de los Developers; eso debió revisarse durante el Sprint.
- **No se muestra trabajo a medias:** Solo se demuestra software o entregables que están 100% terminados y listos para usarse. Mostrar cosas "casi listas" destruye la transparencia.
- **No es una presentación estática:** Si el equipo solo habla y los stakeholders solo asienten con la cabeza y se van, la reunión fracasó. Debe haber debate, preguntas y cambios tangibles en el Product Backlog como resultado.

Al terminar la Sprint Review, ya se sabe qué rumbo tomará el producto. Pero antes de empezar el siguiente ciclo, el equipo necesita mirarse al espejo para mejorar *cómo* trabaja.

---

### Sprint Retrospective

Si la *Sprint Review* sirve para inspeccionar y adaptar el **producto**, la *Sprint Retrospective* (Retrospectiva) sirve para inspeccionar y adaptar al **equipo y sus procesos**. Es el espacio dedicado exclusivamente a la mejora continua.

Este evento cierra formalmente el Sprint. Tiene un límite de tiempo (*timebox*) de máximo 3 horas para un Sprint de un mes (usualmente toma de 1 a 1.5 horas para Sprints más cortos).

A diferencia de la *Review*, aquí **no hay invitados externos ni stakeholders**. Es un espacio seguro y privado solo para el **Scrum Team**. Así es como interactúan en la práctica:

#### 1. El Scrum Master (El Guardián de la Seguridad Psicológica)

En la Retrospectiva, el rol de Scrum Master brilla en su faceta de facilitador y coach.

- **Crea un entorno seguro:** Se asegura de que la reunión sea un espacio de confianza donde todos puedan hablar con honestidad sin miedo a represalias. Fomenta la mentalidad de que, independientemente de lo que hayan descubierto, todos hicieron el mejor trabajo posible con la información y recursos que tenían.
- **Diseña la dinámica:** Para evitar que la reunión sea aburrida o repetitiva, prepara técnicas de facilitación (dinámicas visuales, lluvia de ideas anónimas, etc.) para ayudar al equipo a analizar qué salió bien, qué salió mal y qué procesos, herramientas o interacciones humanas causaron fricción.
- **Participa como un par:** El también es miembro del equipo, así que aporta sus propias observaciones sobre cómo está funcionando el marco de trabajo y cómo se están comunicando.

#### 2. Los Developers (Los Dueños de la Ejecución)

Ellos son los que están en las trincheras del día a día, por lo que su voz técnica y operativa es vital.

- **Evalúan la ingeniería y las herramientas:** Discuten si los entornos de prueba fallaron, si la calidad del código disminuyó, si hay deuda técnica acumulada o si la Definición de Terminado (*Definition of Done*) necesita hacerse más estricta.
- **Analizan la colaboración:** Reflexionan sobre cómo trabajaron juntos. ¿Se ayudaron mutuamente? ¿Hubo cuellos de botella porque una sola persona sabía hacer algo?
- **Proponen soluciones:** No solo levantan quejas; son proactivos proponiendo experimentos o nuevas formas de trabajar para el siguiente Sprint.

#### 3. El Product Owner (El Miembro del Equipo, no el Jefe)

Un error gravísimo es pensar que el PO no debe asistir a la Retrospectiva o que asiste para regañar al equipo por no entregar a tiempo. El PO entra aquí como un miembro igualitario del Scrum Team.

- **Retroalimentación bidireccional:** El PO comparte cómo sintió el flujo de valor y la calidad de las entregas. A su vez, escucha el feedback de los Developers (por ejemplo: *"Las historias de usuario de este Sprint estaban muy ambiguas y perdimos tiempo tratando de descifrarlas"*).
- **Ajusta su propia forma de trabajar:** Basado en la conversación, el PO se compromete a mejorar cómo refina el *Product Backlog*, cómo comunica el Objetivo del Producto o su disponibilidad para resolver dudas en el día a día.

------

#### El Resultado: Mejoras Accionables

La Retrospectiva no es solo para desahogarse. El equipo debe salir de aquí con **al menos una mejora accionable e impactante** que implementarán inmediatamente en el próximo Sprint. Incluso, es una excelente práctica agregar esta tarea de mejora directamente al siguiente *Sprint Backlog* para asegurar que no se olvide.

#### Lo que la Sprint Retrospective NO es (Antipatrones comunes)

Para mantener la salud del equipo, siempre se evita caer en esto:

- **No es un juego de culpas (Blame Game):** No se trata de buscar quién tiró el servidor o quién programó mal una función. Se trata de buscar por qué *el proceso* permitió que ese error llegara a producción y cómo lo evitamos a futuro.
- **No es un muro de los lamentos:** Si el equipo se queja durante una hora pero nadie propone una solución o un experimento para mejorar, la retrospectiva fue una pérdida de tiempo.
- **No se cancela "porque hay mucho trabajo":** Cuando un equipo dice "estamos muy atrasados, cancelemos la retro para seguir programando", es exactamente el momento en el que *más* necesitan la retrospectiva para entender por qué están atrasados.

---

### Product Backlog

Entrar al terreno de los Artefactos es fundamental porque representan el trabajo o el valor en Scrum. Están diseñados para maximizar la transparencia; si no podemos ver claramente los artefactos, nuestras decisiones se basarán en suposiciones, no en hechos.

En la versión actual de la Guía de Scrum, cada uno de los 3 artefactos tiene un **"compromiso"** asociado. Este compromiso sirve para aportar contexto, enfoque y medir el progreso.

Empecemos con el panorama general y la fuente de todo el trabajo: **El Product Backlog** (La Pila del Producto).

------

#### ¿Qué es el Product Backlog?

Imagina el Product Backlog no como un documento estático de requerimientos técnicos, sino como un **organismo vivo**. Es una lista emergente y ordenada de todo lo que se sabe que es necesario para mejorar el producto. Es la **única fuente de trabajo** que asume el Scrum Team. Si algo no está en el Product Backlog, simplemente no existe para el equipo.

**Su Compromiso: El Objetivo del Producto (Product Goal)**

El compromiso asociado a este artefacto es el Objetivo del Producto. Es el estado futuro del producto que sirve como meta a largo plazo para el equipo. El Product Backlog define *qué* haremos para alcanzar ese objetivo.

Así es como interactúan los roles en el día a día para mantener este artefacto sano y valioso:

#### 1. El Product Owner (El Dueño y Curador)

El PO es el responsable absoluto de este artefacto. En la práctica:

- **Ordena por valor:** No organiza la lista por "fases del proyecto", sino por prioridad de negocio, riesgo o dependencias. Lo más importante y urgente siempre debe estar hasta arriba.
- **Mantiene el enfoque:** Se asegura de que cada elemento (ya sea una nueva funcionalidad, una corrección de un error o una mejora técnica) aporte directamente al Objetivo del Producto.
- **Transparencia total:** Se asegura de que el Product Backlog sea visible y comprendido por todos los interesados y por el equipo.

#### 2. Los Developers (Los Analistas y Estimadores)

Aunque el PO es el dueño, no trabaja en el vacío. Los Developers son vitales para darle forma a la lista a través de una actividad continua llamada **Refinamiento** (*Refinement*).

- **Aportan la viabilidad técnica:** Le dicen al PO si lo que está pidiendo en la parte superior de la lista es técnicamente posible, si es demasiado grande o si falta información.
- **Son los únicos que estiman:** El PO dice qué valor tiene un elemento, pero **solo los Developers deciden qué tan complejo es o cuánto esfuerzo requiere**. El PO jamás le dicta al equipo cuánto tiempo debe tomarles algo.
- **Descomponen el trabajo:** Ayudan al PO a dividir elementos gigantescos (Epics) en piezas más pequeñas y manejables (Historias de Usuario o tareas funcionales) que puedan completarse en un solo Sprint.

#### 3. El Scrum Master (El Asesor de Transparencia)

Su trabajo aquí no es escribir requerimientos, sino asegurar la salud del ecosistema.

- **Coach de gestión:** Enseña al PO técnicas para ordenar la lista de manera empírica (por ejemplo, usando técnicas como *User Story Mapping* o *MoSCoW*).
- **Facilitador de entendimiento:** Observa si hay una brecha de comunicación. Si los Developers constantemente dicen "no entiendo qué quiere el PO", interviene para que mejoren la forma en que redactan o discuten los elementos.
- **Protector del Refinamiento:** Se asegura de que el equipo dedique tiempo durante el Sprint actual para revisar y limpiar los requerimientos de los Sprints *futuros*, evitando que lleguen a la siguiente Planificación a ciegas.

------

#### Lo que el Product Backlog NO es (Antipatrones comunes)

El Scrum Master, debe estar alerta a estos focos rojos:

- **No es una carta a Santa Claus interminable:** Si el Backlog tiene 500 elementos que nadie ha revisado en dos años, es un cementerio de ideas, no una herramienta ágil. Hay que tener el valor de borrar lo que no aporta al objetivo.
- **Múltiples Backlogs para un producto:** A veces se ve un Backlog para los diseñadores, otro para los programadores front-end y otro para back-end. Esto es un error. **Un producto = Un solo Product Backlog**.
- **El PO lo escribe a puerta cerrada:** Si el PO redacta todo solo en su oficina y simplemente se lo entrega a los Developers el día de la Planificación, se pierde la colaboración y el entendimiento compartido.

Ahora que entendemos cómo se gestiona "el gran plan a futuro", pasemos al segundo artefacto, el **Sprint Backlog**, que es el plan táctico a corto plazo.

---

### Sprint Backlog

Pasemos de la estrategia a la trinchera. Si el Product Backlog es el mapa completo del tesoro, el **Sprint Backlog** es la mochila con las herramientas exactas y la ruta específica que el equipo usará durante los próximos días para dar el siguiente paso.

Te comparto que este es el artefacto más dinámico y táctico de Scrum. Es un plan en tiempo real creado *por* y *para* los Developers.

**Su Compromiso: El Objetivo del Sprint (Sprint Goal)**

El Sprint Backlog no es solo una lista de tareas aisladas; todo lo que contiene debe apuntar a cumplir el **Objetivo del Sprint**. Este objetivo es la estrella polar que mantiene al equipo enfocado, incluso si el plan técnico tiene que cambiar a mitad de camino.

Para que este artefacto sea transparente y útil, está compuesto por tres partes:

1. El Objetivo del Sprint (el *Por qué*).
2. Los elementos del Product Backlog seleccionados (el *Qué*).
3. El plan de acción técnico para entregarlos (el *Cómo*).

Así interactúan los roles con este plan táctico en el día a día:

#### 1. Los Developers (Los Dueños Absolutos)

En Scrum, **nadie más que los Developers puede modificar el Sprint Backlog durante el Sprint**. Ellos son los únicos responsables de este artefacto.

- **Trazan el plan técnico:** Ellos toman el requerimiento de negocio y lo desglosan. Por ejemplo, si el Objetivo del Sprint es habilitar el registro de usuarios para una aplicación web educativa, los Developers trazan la arquitectura: deciden cómo estructurar la base de datos (definiendo entidades limpias como `STUDENT` en mayúsculas, asignando su llave primaria simplemente como `id`), cómo conectar la API y se aseguran de que el código fuente y su documentación técnica se redacten profesionalmente en inglés. Todo ese "cómo" vive en el Sprint Backlog.
- **Lo actualizan diariamente:** A medida que avanzan (o encuentran problemas), actualizan este plan. Si descubren que una tarea técnica toma más tiempo del pensado, agregan nuevas tareas o ajustan el enfoque durante la *Daily Scrum*.
- **Colaboración, no asignación:** No se reparten todas las tareas el día uno para trabajar en silos. En su lugar, toman el trabajo de forma colaborativa conforme van terminando, asegurando que el diseño, la programación y las pruebas fluyan como un solo equipo.

#### 2. El Product Owner (El Consultor de Negocio)

Una vez que el Sprint comienza, el PO suelta el control del plan táctico, pero se mantiene cerca para dar contexto.

- **Negocia, no impone:** Si el PO se da cuenta de que el mercado cambió repentinamente, no puede ir al Sprint Backlog y meter nuevas tareas a la fuerza. Debe acercarse a los Developers y preguntar si es posible ajustar el plan sin poner en riesgo el Objetivo del Sprint.
- **Aclara el valor:** Si los Developers están diseñando la lógica técnica y se topan con un caso de uso ambiguo, el PO interviene para aclarar cómo debería comportarse el sistema desde la perspectiva del usuario.
- **Flexibilidad en el alcance:** Si los Developers descubren que el trabajo es mucho más complejo de lo estimado y no podrán terminar todo, se sientan con el PO para renegociar qué elementos del Sprint Backlog pueden retirarse para al menos lograr cumplir el Objetivo del Sprint.

#### 3. El Scrum Master (El Protector del Foco)

Su labor con el Sprint Backlog es protegerlo de la contaminación externa y asegurar que fluya.

- **Escudo contra interrupciones:** Si un directivo de otro departamento llega a pedir "un favorcito rápido" e intenta meterlo en el Sprint Backlog, el interviene. Ayuda a canalizar esa petición hacia el Product Owner para que lo evalúe para el *futuro* Product Backlog, protegiendo la concentración actual del equipo.
- **Fomenta la visibilidad:** Se asegura de que el Sprint Backlog no esté escondido en la computadora de un solo programador. Ya sea en un tablero físico con post-its o en una herramienta digital, impulsa al equipo a que lo mantengan actualizado para que la transparencia sea real.
- **Detecta cuellos de botella:** Al observar el flujo de las tareas en el tablero, puede identificar si el equipo se está estancando en la fase de pruebas o si hay dependencias no resueltas, y les ofrece su ayuda para destrabar el proceso.

------

#### Lo que el Sprint Backlog NO es (Antipatrones comunes)

Desde la experiencia, estos son los errores más comunes que rompen la agilidad de este artefacto:

- **No es inamovible (No es un contrato rígido):** Un error grave es pensar que, si una tarea está en el Sprint Backlog, se tiene que hacer exactamente como se pensó el primer día. Scrum abraza el empirismo; si descubrimos una mejor forma técnica de hacer las cosas al tercer día, cambiamos el plan táctico sin pedirle permiso a la gerencia.
- **No es un reporte de horas para Recursos Humanos:** El Sprint Backlog mide el progreso hacia una meta de valor, no sirve para vigilar si un Developer trabajó 8 horas exactas en su teclado.
- **El PO no asigna el trabajo:** Si el PO o un "Jefe de Proyecto" entra al tablero a asignar tickets con nombres específicos a cada Developer, se destruye la autoorganización y la responsabilidad compartida.

Ya tenemos el mapa a largo plazo y la mochila para el viaje a corto plazo. Todo este esfuerzo culmina en el resultado tangible de nuestro trabajo.

Cerremos este recorrido explorando el tercer y último artefacto: **El Incremento** (y su vital relación con la Definición de Terminado).

---

### Increment

¡Llegamos a la pieza final del rompecabezas! Como Scrum Master, te aseguro que todo el esfuerzo de planificación, sincronización y colaboración del que hemos hablado culmina en este preciso artefacto. Sin el **Incremento**, Scrum es solo un montón de reuniones bien intencionadas.

El Incremento es el resultado tangible, el valor real entregado. Es un paso concreto hacia el Objetivo del Producto (*Product Goal*).

**Su Compromiso: La Definición de Terminado (Definition of Done - DoD)**

Aquí está la clave de todo: **un Incremento nace en el momento exacto en que un elemento del Product Backlog cumple con la Definición de Terminado**.

La DoD no es un capricho; es una lista de verificación clara y transparente (por ejemplo: código revisado, pruebas automatizadas pasadas, documentación actualizada, cero errores críticos) que garantiza que el trabajo tiene la calidad necesaria para ser utilizado por el cliente final sin romper el sistema.

Así es como interactúan los tres roles para construir y proteger este artefacto en la práctica:

### 1. Los Developers (Los Creadores y Guardianes de la Calidad)

Ellos son los artesanos del Incremento y los principales responsables de que cumpla con la calidad exigida.

- **Construyen con calidad:** Durante el Sprint, transforman las ideas en software o productos funcionales. Su brújula técnica es la Definición de Terminado; si una tarea técnica no cumple con todos los puntos de la DoD, simplemente no pueden decir que está terminada.
- **Transparencia absoluta:** Son honestos sobre el estado del producto. Si no lograron terminar una funcionalidad con la calidad requerida antes de la *Sprint Review*, no la ocultan ni la entregan "a medias". Ese trabajo incompleto regresa al Product Backlog.
- **Evolucionan la DoD:** A medida que el equipo madura, los Developers proponen hacer la Definición de Terminado más estricta o completa (por ejemplo, agregando pruebas de seguridad más robustas) para aumentar la calidad del Incremento.

### 2. El Product Owner (El Estratega del Lanzamiento)

El PO utiliza el Incremento como su herramienta principal para medir el éxito y recopilar retroalimentación real del mercado.

- **Inspecciona, pero no es el "Tester":** El PO colabora durante el Sprint para asegurar que el Incremento cumple con las reglas de negocio, pero no espera hasta el último día para ser un "cuello de botella" de control de calidad. Confía en la DoD de los Developers.
- **Decide cuándo liberar (Release):** Un Incremento *siempre* debe estar en condiciones de ser entregado a los usuarios (releasable). Sin embargo, es el PO quien decide la estrategia comercial de *cuándo* apretar el botón para lanzarlo al mercado, dependiendo de qué sea lo más valioso para el negocio.
- **Valida el valor empíricamente:** Al tener un Incremento funcional, el PO ya no tiene que adivinar si una idea es buena. Puede mostrársela a los stakeholders (en la *Sprint Review*) o a usuarios reales para tomar decisiones basadas en datos concretos.

### 3. El Scrum Master (El Coach de la Calidad y el Proceso)

Mi labor respecto al Incremento es proteger la integridad del marco de trabajo y asegurar que no nos engañemos a nosotros mismos.

- **Protege la Definición de Terminado:** Si noto que el equipo, por presión de tiempo, quiere entregar algo saltándose las pruebas o la documentación, intervengo. Les recuerdo que es preferible entregar menos cosas bien hechas (que cumplan la DoD), que muchas cosas que generen "deuda técnica" y fallen en el futuro.
- **Facilita la creación de la DoD:** Si el equipo es nuevo y no tiene una Definición de Terminado clara, guío una sesión para que la construyan juntos y se aseguren de que el PO, los Developers y la organización estén alineados sobre lo que significa la palabra "Terminado".
- **Fomenta la entrega continua:** Ayudo a identificar impedimentos técnicos (como falta de automatización) que evitan que el equipo pueda generar Incrementos de forma frecuente y fluida.

------

### Lo que el Incremento NO es (Antipatrones comunes)

Desde la trinchera, estas son las peores prácticas que destruyen el valor de este artefacto:

- **El mito del "99% Terminado":** En Scrum, algo está 100% Terminado o no lo está. No existe el "ya casi está, solo falta probarlo". Si falta probarlo, no es un Incremento, no se muestra en la Review y no aporta valor aún.
- **Entregar maquetas o prototipos estáticos:** Un Incremento no es un diseño en Figma o un diagrama arquitectónico (a menos que el producto en sí sea un documento de diseño). Debe ser un componente del producto final que funcione y sume a lo que ya se construyó en Sprints anteriores.
- **Deuda técnica oculta:** Entregar un Incremento rápido pero con código espagueti o mal estructurado, engañando al PO haciéndole creer que todo está bien cuando internamente el producto está a punto de colapsar.

Con esto, hemos cubierto los pilares fundamentales, los roles, los eventos y los artefactos que conforman Scrum. Es un marco de trabajo elegante en su simplicidad, pero difícil de dominar, ¡por eso el aprendizaje empírico es vital!

Para continuar aplicando esto a la realidad, ¿te gustaría que exploremos cómo redactar buenas **Historias de Usuario** para alimentar el *Product Backlog*, o preferirías que revisemos cómo se maneja la **estimación ágil** (como el Planning Poker) en la práctica?
