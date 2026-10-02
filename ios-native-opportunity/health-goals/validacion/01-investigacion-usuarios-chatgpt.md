# Investigación de usuarios — Health Goals

**Fecha de investigación:** 2 de octubre de 2026  
**One-Pager:** acceso confirmado y leído íntegramente antes de iniciar la investigación.

He tratado los tres problemas A, B y C como hipótesis independientes. La investigación es principalmente **cualitativa y conductual**: conversaciones espontáneas, workarounds creados por usuarios, documentación de productos existentes, App Store y discusiones sobre precios. Sirve para detectar patrones y falsar hipótesis, no para estimar prevalencia poblacional.

Uso estas etiquetas durante el informe:

- **EVIDENCIA:** comportamiento observable, funcionalidad existente o dato verificable.
- **TESTIMONIO:** experiencia espontánea de uno o varios usuarios.
- **INFERENCIA:** conclusión razonable obtenida al cruzar evidencias.
- **HIPÓTESIS:** explicación plausible que todavía requiere validación.

---

## 1. Resumen ejecutivo

La investigación **no valida todavía el JTBD completo como una única necesidad cohesionada**, pero sí encuentra varios problemas reales dentro de él.

El hallazgo más importante es que los tres componentes no tienen la misma fuerza:

| Problema | Señal encontrada | Observación |
|---|---|---|
| **A. No sé qué objetivo ponerme** | **Clara** | Muy visible entre principiantes, gente que vuelve a entrenar y nuevos usuarios de wearables. |
| **B. No sé si voy al ritmo correcto** | **Moderada** | Hay frustración con dashboards y preferencias por medias semanales, pero muchos usuarios se conforman con ver progreso. |
| **C. ¿Qué me queda exactamente para llegar?** | **Menos frecuente, pero sorprendentemente específica** | Encontré usuarios haciendo precisamente este cálculo mediante Shortcuts y matemáticas manuales. |
| **Logging automático** | **Clara en un segmento** | Hay usuarios intentando conectar Apple Health con trackers para evitar marcar manualmente actividades que el reloj ya conoce. |
| **Weekly > daily** | **Bastante respaldado, pero no universal** | Se usa para absorber fines de semana, descanso, enfermedad y días sedentarios. |
| **Willingness to pay** | **Existe en la categoría; no demostrada para este loop concreto** | Streaks, Gentler Streak, Athlytic, Bevel y Strava demuestran gasto en productos adyacentes. |

### Lo que más fortalece la tesis

**EVIDENCIA:** hay usuarios que literalmente construyen reglas como:

> media reciente → próximo objetivo

Un usuario de Apple Watch explica que cada semana reajusta Move, Exercise y Stand usando la media de la semana anterior; otro responde que piensa probar el mismo método aumentando ligeramente la media. Eso se parece mucho al componente **Baseline → Plan** planteado en Health Goals. :chatgpt-content-reference{index="0"}

**EVIDENCIA:** existe al menos un workaround todavía más cercano al núcleo diferencial. Un usuario creó un Shortcut que calcula pasos diarios, total semanal y **cuántos pasos adicionales por día necesita para terminar la semana con una media de 10.000**. Es prácticamente una implementación manual de:

> Progress → Gap → Adapt. :chatgpt-content-reference{index="1"}

Otro usuario, al calcular manualmente los pasos semanales, se queja de que Apple le obliga a hacer matemáticas para obtener un dato que considera útil. :chatgpt-content-reference{index="2"}

**EVIDENCIA:** también encontré el equivalente del principio *zero logging*. Un usuario quiere que un objetivo del tipo «entrenar cinco veces por semana» se complete automáticamente mediante Apple Health y señala que Streaks puede leer workouts pero no satisface bien su necesidad de seguimiento semanal. :chatgpt-content-reference{index="3"}

### Lo que más debilita la tesis

La mayor objeción no es que el problema sea inventado. Es que **varias partes ya están suficientemente resueltas para muchos usuarios**.

En 2026 Apple Fitness permite establecer objetivos diferentes según el día de la semana, pausar los anillos sin perder la racha y, cada lunes, revisar la semana anterior y recibir objetivos sugeridos en función del rendimiento previo. Esto invade directamente una parte de **Baseline → Plan** y elimina buena parte del antiguo problema de la rigidez diaria. :chatgpt-content-reference{index="4"}

Strava ya soporta objetivos semanales, mensuales y anuales —incluyendo tiempo, distancia y número de actividades— y puede sugerir objetivos basándose en actividad previa. :chatgpt-content-reference{index="5"}

**INFERENCIA:** el argumento «las apps solo muestran datos y nadie ayuda a establecer objetivos» ya no es correcto en 2026. El espacio potencial está en una zona más estrecha: combinar datos pasivos, objetivos flexibles y traducción del progreso a **qué significa concretamente para el resto del periodo**.

---

# 2. Evidencia sobre creación de objetivos

## Problema A — convertir “quiero estar más activo” en números

Aquí la evidencia es abundante.

### Usuarios de Apple Watch

**TESTIMONIO:** aparecen repetidamente preguntas como «¿cómo decidís vuestro Move goal?», «¿qué objetivo sería razonable?» o «¿lo tengo demasiado alto?». :chatgpt-content-reference{index="6"}

Un caso reciente es especialmente representativo: una enfermera que venía de Garmin, caminaba alrededor de 10.000 pasos y no sabía qué valor de calorías debía establecer como Move goal. Una respuesta sugería usar el reloj durante una o dos semanas, observar el comportamiento normal y establecer un objetivo algo superior al baseline. :chatgpt-content-reference{index="7"}

Eso reproduce espontáneamente una lógica similar a:

**baseline real → pequeña progresión → objetivo.**

Otro usuario explica directamente que recalcula semanalmente sus objetivos usando la media anterior. :chatgpt-content-reference{index="8"}

### Principiantes y personas que vuelven al gimnasio

El mismo patrón aparece sin Apple Watch.

**TESTIMONIO:** principiantes preguntan con frecuencia cuántos días deberían entrenar, y quienes regresan después de años de inactividad expresan incertidumbre sobre frecuencia y punto de partida. Las respuestas varían mucho —dos, tres, cuatro, cinco días— dependiendo de rutina, recuperación y preferencias. :chatgpt-content-reference{index="9"}

**INFERENCIA:** el problema A es real, pero tiene dos variantes diferentes:

1. **No sé cuál es un objetivo razonable dada mi situación actual.**
2. **No sé cuál es un objetivo fisiológicamente apropiado.**

Health Goals puede abordar mejor la primera. La segunda empieza a requerir conocimiento de entrenamiento, recuperación o salud que el producto pretende explícitamente evitar.

### Contrapeso importante

**EVIDENCIA:** Apple ya sugiere objetivos a partir del rendimiento anterior. :chatgpt-content-reference{index="10"}

**TESTIMONIO:** algunos usuarios ni siquiera necesitan esa personalización. Hay personas que dejan los anillos en los valores por defecto y encuentran suficiente motivación simplemente intentando cerrarlos. :chatgpt-content-reference{index="11"}

**INFERENCIA:** A existe, pero **no basta por sí mismo para justificar Health Goals**.

---

# 3. Evidencia sobre seguimiento del progreso

## Problema B — “sé cuánto llevo, pero no sé si voy bien”

Aquí la evidencia es menos contundente que en A.

### Demanda de contexto semanal

Cuando Apple redujo información de su resumen semanal en watchOS 10, usuarios se quejaron concretamente de perder datos como pasos y distancia totales; alguno describió el nuevo resumen como prácticamente inútil. :chatgpt-content-reference{index="12"}

Otros usuarios encuentran en Apple Health medias semanales cuando lo que quieren es conocer totales o interpretar mejor el periodo. :chatgpt-content-reference{index="13"}

En comunidades de walking aparece una motivación distinta:

**TESTIMONIO:** una persona explica que mirar una media semanal en vez de un objetivo diario evita que un mal día convierta el objetivo en algo imposible y provoque abandono; cada paso sigue contribuyendo al resultado de la semana. :chatgpt-content-reference{index="14"}

Otro usuario dice haber pasado de objetivos diarios a semanales porque dispone de más tiempo los fines de semana. :chatgpt-content-reference{index="15"}

### Pero “mostrar progreso” sí puede ser suficiente

**TESTIMONIO:** algunos usuarios dicen explícitamente que los anillos de Apple ya les dan toda la información/motivación que necesitan. Otros han probado Gentler Streak, Athlytic o Bevel y regresan a Apple porque no quieren más información. :chatgpt-content-reference{index="16"}

Un usuario de Gentler Streak eligió ese producto precisamente porque no quería una sobrecarga de métricas. :chatgpt-content-reference{index="17"}

**INFERENCIA:** no hay evidencia suficiente para afirmar que los dashboards convencionales fallen sistemáticamente. Para un segmento, una barra, una media o los anillos son suficientes.

La señal de B es, por tanto, **moderada**, no fuerte.

---

# 4. Evidencia sobre “qué me queda por hacer”

## Problema C — Progress → Gap

Esta fue la parte en la que esperaba encontrar menos evidencia y encontré algunos de los comportamientos más interesantes.

### Un Shortcut prácticamente idéntico al cálculo propuesto

**EVIDENCIA FUERTE:** un usuario de r/shortcuts creó *Steps Target/Summary*. El Shortcut muestra:

- pasos diarios;
- total semanal;
- tiempo necesario para alcanzar 10.000 pasos;
- y cuántos pasos adicionales necesita realizar por día para alcanzar una media semanal de 10.000.

Si está por encima del objetivo, el resultado pasa a ser negativo. Otro participante pidió automatizar además el envío diario de esa información. :chatgpt-content-reference{index="18"}

Esto es comportamiento, no una respuesta a «¿usarías Health Goals?».

### Matemáticas manuales

**TESTIMONIO:** en una discusión sobre pasos semanales, un usuario recomienda multiplicar la media semanal por siete y comenta que no entiende por qué Apple obliga al usuario a hacer esas matemáticas cuando considera que es un dato útil. :chatgpt-content-reference{index="19"}

**TESTIMONIO:** otros usuarios describen conscientemente un sistema de compensación: si hacen pocos pasos un día, recuperan el déficit durante el resto de la semana. :chatgpt-content-reference{index="20"}

Una persona organiza incluso la semana alrededor de un total de 70.000 pasos, haciendo más en días con menos obligaciones. :chatgpt-content-reference{index="21"}

### El mismo problema aparece en productos más sofisticados

Un usuario de Bevel recibe un objetivo diario de strain pero comenta que no consigue traducirlo a una acción concreta: quiere saber, por ejemplo, cuánto tendría que correr y con qué intensidad para llegar. :chatgpt-content-reference{index="22"}

Otro pregunta si Bevel puede revisar sus datos semanales/mensuales y ajustar sus objetivos; la solución descrita por la comunidad pasa por revisar información y modificarlos manualmente. :chatgpt-content-reference{index="23"}

### Analogía útil, pero no evidencia directa

MacroFactor, en nutrición, permite redistribuir automáticamente objetivos de los días restantes cuando se cambia un día, manteniendo constante el objetivo semanal. Usuarios valoran precisamente esa adaptación. :chatgpt-content-reference{index="24"}

**INFERENCIA:** demuestra que el patrón mental «el periodo importa más que cada día; recalcula lo restante» tiene valor en quantified self.

**No demuestra** que haya una demanda equivalente de la misma magnitud en actividad física.

### Evaluación

**INFERENCIA:** C tiene menos volumen de evidencia que A, pero las evidencias encontradas son más específicas y conductualmente más fuertes.

No estamos imaginando una aritmética que nadie hace: **hay personas haciéndola ya**.

Lo que no sabemos es cuántas.

---

# 5. Fricción del logging manual

Existe una señal clara de usuarios que consideran absurdo registrar manualmente algo que sus dispositivos ya conocen.

### Evidencia directa

**TESTIMONIO:** un usuario de Shortcuts buscaba que sus hábitos relacionados con workout, sueño y otros datos se completasen automáticamente porque el Apple Watch ya registra esas variables. Streaks aparece como workaround. :chatgpt-content-reference{index="25"}

**TESTIMONIO:** un usuario de TickTick quiere centralizar hábitos, pero se queja de que ejercicios y otras métricas de Apple Health no se sincronizan automáticamente; describe la automatización mediante Shortcuts como tediosa y frágil. :chatgpt-content-reference{index="26"}

**TESTIMONIO MUY RELEVANTE:** otro usuario plantea exactamente un objetivo:

> entrenar cinco veces por semana,

filtrando los tipos de workout desde Apple Health. Identifica que Streaks automatiza parte del proceso pero no satisface su tracking semanal. :chatgpt-content-reference{index="27"}

En quantified self también aparecen personas manteniendo Apple Health, apps, hojas de cálculo y otras bases de datos, con quejas sobre el trabajo necesario para mantener todo actualizado. :chatgpt-content-reference{index="28"}

### El logging manual no es intrínsecamente malo

**CONTRAEVIDENCIA:** otro usuario probó numerosas aplicaciones y terminó construyendo un tracker en Numbers/Excel. Con edición rápida y en bloque, afirma haber mantenido durante meses el registro manual de forma consistente. :chatgpt-content-reference{index="29"}

**INFERENCIA:** existe al menos una división clara:

- personas para quienes marcar el hábito forma parte del ritual/reflexión;
- personas que aceptan el logging si la interfaz es eficiente;
- personas que consideran redundante registrar manualmente información que el dispositivo ya posee.

**HIPÓTESIS:** Health Goals probablemente necesita al tercer grupo, no a «usuarios de habit trackers» en general.

---

# 6. Weekly goals vs daily goals

La preferencia semanal **no parece una invención del One-Pager**.

### Evidencia favorable

Un usuario pregunta específicamente por una app que permita objetivos semanales de Move porque ese formato se adapta mejor a su estilo de vida durante el invierno. :chatgpt-content-reference{index="30"}

En otra conversación, usuarios comparan Apple con Garmin y argumentan que con objetivos semanales se pueden compensar días perdidos, algo que consideran más coherente con descanso y entrenamiento. :chatgpt-content-reference{index="31"}

Otros casos ya mencionados muestran:

- recuperar durante la semana los pasos que faltaron un día; :chatgpt-content-reference{index="32"}
- priorizar la media semanal porque un mal día no destruye psicológicamente el objetivo; :chatgpt-content-reference{index="33"}
- hacer más actividad durante los fines de semana; :chatgpt-content-reference{index="34"}
- planificar explícitamente 70.000 pasos semanales. :chatgpt-content-reference{index="35"}

### Streaks y culpa

Antes de que Apple incorporase descansos, el problema era particularmente visible.

Un post con cientos de interacciones describe tres años de obsesión por cerrar los anillos, hasta llegar a «hacer trampas» para conservar la racha; dejar de preocuparse por ella mejoró la relación del usuario con el ejercicio. :chatgpt-content-reference{index="36"}

Otro hilo sobre días de descanso reúne experiencias similares. :chatgpt-content-reference{index="37"}

Un antiguo post pidiendo oficialmente *rest days* acumuló miles de votos. :chatgpt-content-reference{index="38"}

### Pero Apple ya corrigió gran parte de esto

Esta evidencia histórica no debe venderse como si el mercado siguiera igual.

**EVIDENCIA ACTUAL:** Apple permite:

- diferentes objetivos según el día;
- pausar los anillos durante hasta 90 días sin romper la racha;
- revisar objetivos semanalmente. :chatgpt-content-reference{index="39"}

### Y no todos prefieren semanas

Hay usuarios a quienes las rachas simplemente no les importan: descansan cuando quieren y aceptan no cerrar el anillo. :chatgpt-content-reference{index="40"}

**INFERENCIA:** la evidencia respalda **flexibilidad entre días**, más sólidamente que la afirmación absoluta **“weekly is better than daily”**.

Eso es importante. La unidad semanal funciona especialmente bien cuando el comportamiento fluctúa, pero no parece una preferencia universal.

---

# 7. Workarounds actuales

| Workaround | Qué resuelve | Qué deja sin resolver / fricción |
|---|---|---|
| **Apple Fitness** | Tracking automático, rings, goals por día, sugerencias basadas en historial, descanso/pausa. :chatgpt-content-reference{index="41"} | Sigue principalmente una lógica de rings/días. No encontré evidencia de que calcule un gap semanal del tipo “te quedan X workouts + Y pasos/día”. |
| **Strava** | Goals semanales/mensuales/anuales por distancia, tiempo, número de actividades y otros datos; sugerencias de objetivos. :chatgpt-content-reference{index="42"} | Más orientado a actividad deportiva explícita. No encontré el mismo cálculo adaptativo del resto de la semana. |
| **Garmin** | Minutos de intensidad semanales automáticos; 150 min como objetivo estándar; muy orientado a entrenamiento. :chatgpt-content-reference{index="43"} | El objetivo deriva en parte de una recomendación general, no necesariamente de una intención + baseline personal. |
| **Fitbit** | Metas de pasos/actividad y otras métricas; algunas superficies incluyen objetivos semanales. :chatgpt-content-reference{index="44"} | Predominio de goals predefinidos; ecosistema distinto a HealthKit. |
| **Gentler Streak** | Interpreta actividad y recuperación y recomienda nivel de ejercicio; enfatiza descanso y ausencia de culpa. :chatgpt-content-reference{index="45"} | Se acerca más a “qué conviene hacer hoy” y recuperación; entra en una categoría de coaching mayor que la tesis de Health Goals. |
| **Athlytic** | Traduce Apple Health en recovery, exertion y otros targets. :chatgpt-content-reference{index="46"} | Mayor densidad de métricas y fisiología. Algunos usuarios no quieren ese nivel. |
| **Bevel** | Health data + strain/recovery/fitness + recomendaciones y planificación. :chatgpt-content-reference{index="47"} | Producto bastante más amplio; usuarios siguen solicitando traducción de targets a acciones concretas. :chatgpt-content-reference{index="48"} |
| **Streaks** | Habit tracker con detección automática a través de Health; pago único. :chatgpt-content-reference{index="49"} | Su unidad conceptual sigue siendo fundamentalmente el hábito/streak; un usuario identifica limitaciones para el caso semanal de workouts. :chatgpt-content-reference{index="50"} |
| **FitnessView** | Dashboard de HealthKit, goals, progreso y resúmenes semanales/mensuales. :chatgpt-content-reference{index="51"} | Principalmente visualización y goal tracking. |
| **Shortcuts** | Permite hacer exactamente cálculos personalizados de gap y automatización. :chatgpt-content-reference{index="52"} | Construcción y mantenimiento manual; requiere que el usuario diseñe su propia lógica. |
| **Spreadsheets/Numbers** | Flexibilidad total, medias, objetivos y reflexión. :chatgpt-content-reference{index="53"} | Logging y mantenimiento manuales. |

### Lectura competitiva

**INFERENCIA:** no existe un «vacío de mercado» evidente.

El usuario puede ensamblar hoy bastante del JTBD usando:

> Apple Health/Fitness + Streaks/Strava + Shortcuts/hoja de cálculo.

La pregunta de discovery relevante no es si existen herramientas, sino si **el coste cognitivo de ensamblar e interpretar todo eso es suficientemente frecuente e importante**.

Eso todavía no está demostrado.

---

# 8. Segmentos donde el problema es más fuerte

## 1. Personas que quieren ser más activas pero no siguen un programa deportivo

**EVIDENCIA:** aparecen dudas sobre pasos, frecuencia y Move goals, y es común utilizar medias anteriores para decidir qué intentar después. :chatgpt-content-reference{index="54"}

**INFERENCIA:** buen encaje entre:

- necesidad de orientación;
- métricas sencillas;
- datos disponibles automáticamente;
- bajo nivel de prescripción deportiva.

## 2. Personas que vuelven al ejercicio

**EVIDENCIA:** numerosos principiantes/returners preguntan cuántos días deberían entrenar y cómo empezar después de meses o años. :chatgpt-content-reference{index="55"}

**INFERENCIA:** el baseline es particularmente relevante porque su identidad mental —«antes entrenaba cuatro días»— puede estar desconectada de lo que realmente llevan haciendo últimamente.

## 3. Personas con semanas irregulares

Aquí es donde la evidencia de temporalidad es más coherente:

- días laborales vs fines de semana;
- días sedentarios compensados después;
- enfermedad, descanso y otros cambios;
- preferencia por medias/totales semanales. :chatgpt-content-reference{index="56"}

## 4. Personas orientadas a consistencia, no a rendimiento deportivo

**INFERENCIA:** goals como:

- caminar más;
- entrenar X veces;
- mantenerse activo;

son suficientemente comprensibles y HealthKit puede observarlos sin convertirse en entrenador.

### Síntesis del segmento con mejor evidencia

**INFERENCIA:**

> Persona no atleta, con iPhone/Apple Watch que ya genera automáticamente datos de actividad, quiere ganar consistencia o moverse más, tiene semanas variables y no quiere administrar manualmente otro tracker.

Es bastante más específico que «usuario de Apple Watch».

---

# 9. Segmentos donde el problema parece débil

## Atletas o usuarios avanzados

Corredores, triatletas y usuarios estructurados ya manejan volúmenes, programas y frecuencias concretos; aparecen más asociados a Garmin, Strava y sistemas especializados. :chatgpt-content-reference{index="57"}

**INFERENCIA:** para ellos, “tres workouts esta semana” puede ser demasiado poco expresivo.

## Usuarios satisfechos con los anillos

Hay usuarios que consideran que Apple Fitness ya les proporciona la motivación necesaria y no quieren más sistemas. :chatgpt-content-reference{index="58"}

## Usuarios que buscan únicamente estadísticas

Un usuario de FitnessView describe precisamente el valor de disponer de Apple Health como almacén central y otra interfaz para visualizarlo y establecer goals; no expresa necesidad de que una aplicación le diga qué hacer. :chatgpt-content-reference{index="59"}

## Usuarios que ya saben exactamente qué quieren hacer

Quien sigue una rutina estable de tres, cuatro o cinco sesiones y tiene un programa concreto tiene poco problema A y poco valor en que otra app vuelva a inferir ese objetivo.

## Rehabilitación, enfermedad o objetivos clínicos

**INFERENCIA:** aquí el problema puede ser real, pero el criterio de «baseline + progresión» deja de ser suficiente y el riesgo de interpretar actividad sin contexto médico aumenta.

Este segmento no encaja con las fronteras establecidas por el One-Pager.

---

# 10. Evidencia en contra

Esta sección cambia materialmente la evaluación.

## “Apple ya me basta”

Usuarios dicen que los anillos son suficientes para mantener consistencia y que el pequeño déficit al final del día les motiva a caminar unos minutos más. :chatgpt-content-reference{index="60"}

Otros probaron aplicaciones como Gentler Streak, Athlytic o Bevel y volvieron a Apple porque no necesitaban tanta información o recomendaciones. :chatgpt-content-reference{index="61"}

## “No quiero otra capa de inteligencia”

Un usuario que buscaba una app sencilla de fuerza especifica que no quiere sugerencias por IA ni una enorme cantidad de métricas. :chatgpt-content-reference{index="62"}

**INFERENCIA:** una recomendación no es automáticamente más valiosa que una métrica. Para algunas personas es simplemente ruido adicional.

## Las recomendaciones automáticas pueden resultar absurdas

Este riesgo está bien documentado en las Monthly Challenges de Apple.

Usuarios recientes informan de objetivos demasiado difíciles después de meses excepcionalmente activos, otros de objetivos absurdamente fáciles, y otros de recomendaciones que no coinciden con aquello que realmente quieren entrenar. :chatgpt-content-reference{index="63"}

El 1 de octubre de 2026, por ejemplo, un usuario muy activo recibió como reto mensual apenas tres caminatas de cinco minutos y lo consideró trivial; en el mismo hilo otro usuario recibió un reto mucho más alineado con su actividad. :chatgpt-content-reference{index="64"}

**INFERENCIA IMPORTANTE:** utilizar actividad histórica **no equivale automáticamente a producir un buen objetivo**.

Un mes atípico por:

- vacaciones;
- mudanza;
- carrera;
- enfermedad;
- nacimiento de un hijo;
- lesión;

puede convertir el baseline en una referencia equivocada.

## La prescripción puede generar culpa

La experiencia histórica de Apple Rings muestra que algunas personas terminan persiguiendo números o streaks incluso cuando deberían descansar. :chatgpt-content-reference{index="65"}

Gentler Streak se ha diferenciado precisamente vendiendo una relación menos punitiva con ejercicio y descanso. :chatgpt-content-reference{index="66"}

## Apple ha cerrado parte del hueco

Este es probablemente el mayor cambio respecto a cómo habría evaluado la idea en 2023.

Apple ahora:

- adapta goals según el día;
- permite pausarlos;
- conserva las rachas;
- muestra el resumen semanal;
- propone cambios basándose en actividad previa. :chatgpt-content-reference{index="67"}

**INFERENCIA:** cualquier validación que se apoye demasiado en antiguas quejas sobre la rigidez de los rings sobreestima el problema actual.

---

# 11. Willingness to pay observable

Hay dinero circulando en este espacio, pero hay que ser muy estricto con lo que demuestra.

### Streaks

Streaks cuesta actualmente alrededor de **6,99 € como compra única** en la App Store española y mantiene cientos de valoraciones. Ofrece, entre otras cosas, integración automática con Health. :chatgpt-content-reference{index="68"}

**EVIDENCIA:** usuarios pagan por un habit tracker compacto que elimina parte del logging.

Es el comparable conceptualmente más interesante para una monetización sencilla.

### Gentler Streak

Gentler Streak tiene aproximadamente 1.500 valoraciones en España y vende suscripciones y opciones lifetime. :chatgpt-content-reference{index="69"}

En Reddit hay usuarios que explican haber pasado a premium por el valor de sus recomendaciones y por cómo maneja descanso/actividad, mientras otros consideran el producto demasiado caro o insuficiente sin suscripción. :chatgpt-content-reference{index="70"}

### Athlytic

Athlytic comercializa suscripciones en España; usuarios describen haber probado un mes y posteriormente comprar el plan anual porque obtenían valor, mientras otros cuestionan el precio. :chatgpt-content-reference{index="71"}

### Bevel

Bevel Pro cuesta actualmente alrededor de **99,99 dólares/año en EE. UU.** según su documentación y tiene precios equivalentes mediante IAP en otros mercados. :chatgpt-content-reference{index="72"}

El valor que algunos usuarios destacan es precisamente convertir muchos datos de Apple en información más interpretable o accionable. :chatgpt-content-reference{index="73"}

### Strava

Los goals personalizados forman parte de la oferta de suscripción de Strava. :chatgpt-content-reference{index="74"}

Pero existe contraevidencia significativa: usuarios actuales cuestionan pagar la suscripción cuando Garmin u otros servicios ya proporcionan objetivos y análisis suficientes. :chatgpt-content-reference{index="75"}

### Qué podemos concluir

**EVIDENCIA:** existe willingness to pay por:

- automatización de hábitos;
- interpretación de Health data;
- recuperación/readiness;
- goals;
- análisis deportivo.

**NO HAY EVIDENCIA suficiente:** de que usuarios paguen específicamente por:

> baseline → objetivos semanales → cálculo continuo del gap.

**INFERENCIA:** la categoría está monetizada; el core loop de Health Goals todavía no.

---

# 12. Preguntas abiertas

Estas son las incertidumbres que impiden pasar de señal mixta a fuerte:

1. **¿Con qué frecuencia ocurre realmente C?**  
   Encontrar un Shortcut que implementa exactamente el cálculo es una señal excelente de intensidad, pero no demuestra prevalencia.

2. **¿Las personas quieren saber “qué falta” repetidamente o solo ocasionalmente?**  
   Un cálculo útil el sábado por la tarde no implica una aplicación que se conserve instalada ocho semanas.

3. **¿A, B y C pertenecen realmente a la misma persona?**  
   Quien no sabe elegir objetivo puede querer coaching. Quien calcula meticulosamente pasos semanales quizá ya sabe perfectamente qué objetivo quiere.

4. **¿Cuántos usuarios desean goals basados en su baseline frente a recomendaciones normativas?**  
   La comunidad suele responder a «¿cuántos días debo entrenar?» con consejos sobre qué es bueno, no necesariamente con «haz un 20 % más que tu media».

5. **¿Cuánto valor adicional aporta conocer el gap frente a mirar simplemente una barra de progreso?**  
   La diferencia conceptual es clara. La diferencia de comportamiento todavía no.

6. **¿El periodo semanal funciona para varias métricas o principalmente para pasos/workouts?**  
   La evidencia es especialmente buena para pasos y frecuencia de ejercicio.

7. **¿Cuándo un baseline histórico deja de representar la situación actual?**  
   La experiencia con retos de Apple demuestra que esta no es una excepción marginal.

8. **¿La automatización mejora retención o elimina una parte útil del compromiso?**  
   Hay evidencia tanto de abandono por logging como de usuarios que disfrutan conscientemente del registro manual.

9. **¿Existe disposición de pago por esta capa estrecha de interpretación?**  
   Los comparables monetizan bundles considerablemente mayores.

---

# 13. Conclusión

La investigación **sí encuentra el problema**, pero no en la forma completamente unificada que propone actualmente el One-Pager.

### Lo que considero demostrado cualitativamente

**EVIDENCIA:**

- Hay personas que quieren mejorar su actividad pero no saben cómo convertirlo en un objetivo numérico razonable.
- Algunas calculan sus objetivos usando su comportamiento reciente como baseline. :chatgpt-content-reference{index="76"}
- Hay usuarios que deliberadamente piensan en semanas porque su actividad diaria fluctúa. :chatgpt-content-reference{index="77"}
- Hay personas que compensan déficits de pasos posteriormente durante la misma semana. :chatgpt-content-reference{index="78"}
- Hay usuarios realizando manualmente la matemática de «cuánto necesito cada día de aquí al final de la semana». :chatgpt-content-reference{index="79"}
- Existe demanda explícita para que workouts/hábitos conocidos por Apple Health se registren automáticamente. :chatgpt-content-reference{index="80"}
- Existe gasto real en productos que convierten Health data en objetivos, recomendaciones o seguimiento.

### Lo que NO considero demostrado

**NO HAY EVIDENCIA suficiente para afirmar:**

- que esas necesidades pertenezcan normalmente al mismo usuario;
- que el problema B sea intenso para una gran proporción de usuarios;
- que consultar el gap tenga suficiente frecuencia para generar retención;
- que una recomendación basada en baseline sea preferible a elegir uno mismo el objetivo;
- que el valor adicional frente a Apple Fitness sea suficientemente grande;
- que exista willingness to pay específicamente por este loop.

### El hallazgo que más cambia mi evaluación

Al comenzar, el problema A parecía potencialmente central.

Después de investigar el mercado actual, **ya no lo considero la parte más diferenciada**.

Apple y Strava han avanzado bastante en:

> historial → sugerencia de objetivo → seguimiento.

En cambio, encontré una señal más peculiar alrededor de:

> **“Tengo un objetivo para este periodo. Con lo que llevo hecho y el tiempo que queda, dime exactamente dónde estoy respecto al ritmo necesario.”**

Que alguien haya construido un Shortcut para hacer justamente esa aritmética y que otros usuarios calculen manualmente recuperaciones semanales es evidencia conductual interesante. Pero todavía son **pocos casos**, no una masa crítica demostrada. :chatgpt-content-reference{index="81"}

Por tanto, no mataría todavía el problema, pero tampoco considero que la investigación permita pasar directamente de este One-Pager a asumir que el producto está validado.

---

# 14. Fuentes

Selección de las fuentes más relevantes; las discusiones de Reddit son testimonios espontáneos, no muestras representativas.

### Apple / productos existentes

- Apple, **Change your Activity goals on Apple Watch**, documentación actual de watchOS 27, consultada 2 oct 2026. [Apple Support — Activity goals](https://support.apple.com/es-es/guide/watch/apd29b30023c/27/watchos/27?utm_source=chatgpt.com)
- Apple, **watchOS 11 introduces powerful health and fitness insights**, 10 jun 2024. [Apple Newsroom — watchOS 11](https://www.apple.com/newsroom/2024/06/watchos-11-brings-powerful-health-and-fitness-insights-and-even-more-personalization-and-connectivity/?utm_source=chatgpt.com)
- Strava, **Goals on the Strava App**, documentación actual, consultada 2 oct 2026. [Strava — Goals](https://support.strava.com/en-us/articles/15401694-goals-on-the-strava-app?utm_source=chatgpt.com)
- Streaks, App Store España. [Streaks — App Store](https://apps.apple.com/es/app/streaks/id963034692?utm_source=chatgpt.com)
- Gentler Streak, App Store España. [Gentler Streak — App Store](https://apps.apple.com/es/app/gentler-streak-workout-tracker/id1576857102?utm_source=chatgpt.com)
- Athlytic, App Store España. [Athlytic — App Store](https://apps.apple.com/es/app/athlytic-fitness-recovery/id1543571755?utm_source=chatgpt.com)
- Bevel, App Store España. [Bevel — App Store](https://apps.apple.com/es/app/bevel-longevity-performance/id6456176249?utm_source=chatgpt.com)

### Problema A — creación de objetivos

- Reddit / AppleWatchFitness, **What is your move goal? How did you arrive at it?**, ene 2024. [Discusión sobre Move goals](https://www.reddit.com/r/AppleWatchFitness/comments/194qjlo/what_is_your_move_goal_how_did_you_arrive_at_it/?utm_source=chatgpt.com)
- Reddit / AppleWatch, **Move goal**, feb 2025. [Nuevo usuario preguntando por un objetivo razonable](https://www.reddit.com/r/AppleWatch/comments/1ilupzl?utm_source=chatgpt.com)
- Reddit / beginnerfitness, **How many days do you personally go to the gym?**, jul 2026. [Discusión sobre frecuencia de entrenamiento](https://www.reddit.com/r/beginnerfitness/comments/1v2xt46/how_many_days_do_you_personally_go_to_the_gym/?utm_source=chatgpt.com)

### Weekly goals y flexibilidad

- Reddit / AppleWatch, **App to set weekly goals**, 2021. [Demanda explícita de weekly Move goals](https://www.reddit.com/r/AppleWatch/comments/r4wrzl/app_to_set_weekly_goals/?utm_source=chatgpt.com)
- Reddit / walking, **How do you walk 10k steps working a 9–5?**, 2025. [Weekly average frente a daily goal](https://www.reddit.com/r/walking/comments/1j2y6dp/how_do_you_walk_10k_steps_working_a_95/?utm_source=chatgpt.com)
- Reddit / AppleWatch, **Don't know who needs to hear this…**, feb 2024. [Experiencia de obsesión con rings y streaks](https://www.reddit.com/r/AppleWatch/comments/1avjdho/dont_know_who_needs_to_hear/?utm_source=chatgpt.com)

### Gap / “qué me queda”

- Reddit / Shortcuts, **Steps Target/Summary**, oct 2023. [Shortcut para calcular pasos restantes por día](https://www.reddit.com/r/shortcuts/comments/16z1qjb?utm_source=chatgpt.com)
- Reddit / walking, **Post ya weekly step count**, 2025. [Usuario calculando manualmente total semanal](https://www.reddit.com/r/walking/comments/1hzttka/post_ya_weekly_step_count/?utm_source=chatgpt.com)
- Reddit / loseit, discusión sobre recuperar pasos durante la semana. [Weekly average y compensación de pasos](https://www.reddit.com/r/loseit/comments/1d6geul/how_do_you_get_amount_steps/?utm_source=chatgpt.com)

### Logging automático

- Reddit / Shortcuts, **habit automation from Apple Health**, oct 2023. [Automatización de hábitos con Health data](https://www.reddit.com/r/shortcuts/comments/171230f?utm_source=chatgpt.com)
- Reddit / HelloHabit, **Apple Health workout auto-logging**, nov 2024. [Workout 5x/week con Apple Health](https://www.reddit.com/r/hellohabit/comments/1gy30eu?utm_source=chatgpt.com)
- Reddit / QuantifiedSelf, **How do you manage health data across multiple apps?**, sep 2026. [Fricción manteniendo múltiples fuentes de health data](https://www.reddit.com/r/QuantifiedSelf/comments/1wnn53q/how_do_you_manage_health_data_across_multiple_apps/?utm_source=chatgpt.com)

### One-Pager investigado

- Health Goals — One-Pager, repositorio `cesarg88/product-discovery`, octubre de 2026. [Health Goals — One-Pager](https://github.com/cesarg88/product-discovery/blob/main/ios-native-opportunity/health-goals/one-pager.md?utm_source=chatgpt.com)

**SEÑAL MIXTA** — Parte del problema existe y hay comportamiento real que lo respalda, incluyendo workarounds sorprendentemente próximos al core loop, pero la formulación actual agrupa necesidades cuya coexistencia, frecuencia, retención y disposición de pago todavía no están demostradas.