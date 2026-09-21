# Contraste de las cinco investigaciones y clasificación final

> Análisis cruzado de `ios-native-opportunity/`: `research-chatGPT.md`, `research-claude.md`, `research-claude-advanced.md`, `research-deepseek.md`, `research-gemini.md`.
> Fecha: 21 de septiembre de 2026. Afirmaciones técnicas decisivas re-verificadas contra `developer.apple.com`, WWDC y Apple Developer Forums.

---

## 0. Cómo he ponderado cada informe

No todos valen lo mismo, y eso cambia el ranking. Antes de comparar ideas hay que comparar el trabajo.

| Informe | Evidencia de usuario | Evidencia de mercado | Capa técnica | Criba real | Peso que le doy |
|---|---|---|---|---|---|
| **chatGPT** | **La mejor de las cinco.** Tuvo acceso a Reddit (yo no). Hilos con fecha, votos y comportamiento concreto | **Nula como fuente**: ni una URL de App Store. Todos sus precios y valoraciones son inverificables desde el documento | Mixta: buenas negativas de plataforma; toda la capa de iOS 27 cuelga de marcadores `content-reference` opacos | **Real.** Mata 10 de 15 y trata la contra-evidencia como dato | **Alto** para señal de problema, bajo para cifras |
| **claude** (estándar) | Media | **La mejor de las cinco.** ≈90 URLs con deep links a fichas con app ID, reviews citadas literalmente, precios con fuente | Sólida en frameworks estables; admite explícitamente no haber descargado la doc de iOS 27 | **Real y a veces contra sí mismo** (degrada su idea de mejor founder-fit por falta de WTP) | **Alto** |
| **claude-advanced** (mío) | Media-baja: **Reddit bloqueado**, que es el agujero grande | Alta: fichas de App Store consultadas, economía real (RevenueCat) | La más verificada; ~40 fetches a documentación primaria | Real | **Alto**, con el agujero de Reddit reconocido |
| **deepseek** | Baja: 9 de 15 candidatos solo con "Inferencia" | Cifras muy precisas ("5.638 reviews, 4.1") **sin una sola URL profunda** que las respalde | Buen mapa de capacidades; **dos wildcards construidos sobre capacidades falsas** | **Decorativa.** Los finalistas son los primeros generados; la tabla comparativa solo evalúa 8 de 15 | **Bajo** |
| **gemini** | **Cero URLs en todo el documento.** Admite que sus sesiones de WWDC son *"simuladas"* | Un único precio de competencia en todo el informe | Ancla en "iOS 18-20", rango inventado. **Sus finalistas #1 y #5 son técnicamente imposibles** | **Inexistente.** Los 5 finalistas son los 5 primeros candidatos en su orden original; 7 de 15 fichas quedaron sin rellenar | **Descartable** como investigación; útil solo como generador de hipótesis |

Dos correcciones que me hago a mí mismo, porque el cruce las saca:

1. **Me perdí AlarmKit por completo.** Es un framework real de iOS 26 que permite a terceros, por primera vez, disparar una alarma de sistema que **rompe el modo Silencio y los Focus sin el entitlement de Critical Alerts**, y que suena **con la app muerta** (la mantiene un daemon del sistema). Es la palanca más infravalorada del ecosistema y dos informes la encontraron antes que yo. Verificado: [AlarmKit](https://developer.apple.com/documentation/AlarmKit), [WWDC25 sesión 230](https://developer.apple.com/videos/play/wwdc2025/230/), y la frase literal *"It overrides both a device's focus and silent mode, if necessary"* en [Scheduling an alarm with AlarmKit](https://developer.apple.com/documentation/AlarmKit/scheduling-an-alarm-with-alarmkit).
2. **El bloqueo de Reddit me costó la categoría de señal más fuerte que tú mismo pediste** ("si mucha gente construye un Shortcut para la misma fricción, investígalo"). ChatGPT sí la encontró, y por eso su finalista #2 sube en este ranking por encima de tres de los míos.

---

## 1. Mapa de convergencia

Cuántos informes independientes llegaron a la misma idea. La convergencia no es prueba de nada por sí sola, pero la convergencia **entre los informes que sí investigaron** sí lo es.

| Idea | advanced | claude | chatGPT | deepseek | gemini | Lectura |
|---|---|---|---|---|---|---|
| **Conteo de días por jurisdicción** | **#1** | **#2** | — | — | — | Solo 2, pero son los 2 con mejor evidencia de mercado. Y el segundo aporta un disparador externo que el primero no tenía |
| **Práctica musical con Music Understanding** | **#2** | **#5** | **#5** | — | (C4, débil) | 3 informes, pero **ninguno con evidencia de demanda**: los tres llegaron por la API, no por el problema. Ver §4 |
| **Cuadrante/horario → Calendario** | — | mata (C11) | **#2** | — | — | Mejor evidencia de usuario de los cinco informes, pero un informe lo mata |
| **Alarma calculada desde el calendario** | — | **#1** | mata (C4/C5) | — | — | Apoyado en AlarmKit, que es real. Disputado |
| **Transcripción larga on-device** | **#3** | mata (C12) | mata (C12) | **#5** | — | **Empate 2-2, y los dos que la matan lo argumentan mejor** |
| **Kilometraje para autónomos** | mata | **#3** | — | — | (C12, sin evidencia) | Yo lo descarté mal; el argumento europeo de claude es mejor que el mío |
| **Registro de nicho tipo acuario** | **#4** | — | — | — | — | Único. Mejor cita individual de todos los informes |
| **Tarjeta → pase de Wallet** | — | **#4** | — | — | — | Único. **Y muere en verificación** (ver §3) |
| **Capturas / organizador de fotos** | mata | mata | mata (C3) | **#4** | **#1** | 3 lo matan, 2 lo proponen. Los 3 que lo matan miraron la App Store |
| **Automatizaciones NFC** | (wildcard) | mata (C9) | mata (C15) | **#3** | — | **Muere en verificación** (ver §3) |
| **Productos HealthKit** (sueño, migraña, marcha) | 2 candidatos | excluido a priori | — | **#1 y #2** | **#2** | Apple reescribió Salud este mes. Ver la nota de §4 |

---

## 2. Lo que la verificación técnica confirma (y por qué importa)

| Afirmación | Quién la hacía | Veredicto |
|---|---|---|
| AlarmKit rompe Silencio y Focus sin Critical Alerts, y dispara con la app muerta | claude, chatGPT | **CIERTO** |
| El botón de parar la alarma lo pone **siempre el sistema** → el patrón "misión para apagarla" tipo Alarmy **no es reproducible** | claude lo advertía | **CIERTO.** El init con `stopButton` propio está deprecado precisamente por eso |
| Music Understanding (iOS 27) da beats, tonalidad, estructura y actividad instrumental on-device | advanced, claude, chatGPT | **CIERTO** |
| El catálogo de Apple Music tiene DRM: **no hay acceso a PCM**, y el FAQ dice que "no hay soporte para apps de estilo DJ" | advanced, claude | **CIERTO.** Techo estructural del candidato musical |
| `predicateForEvents` de EventKit está limitado a **4 años** | claude | **CIERTO**, literal en la doc |
| Existe un protocolo público de proveedores de modelo en Foundation Models (iOS 27) | claude, deepseek | **CIERTO** ([WWDC26 339](https://developer.apple.com/videos/play/wwdc2026/339/)) — pero el executor vive **dentro de tu app**, no es un cambio de modelo a nivel de sistema |
| iOS 27 permite crear Atajos describiéndolos en lenguaje natural | deepseek | **CIERTO** |

---

## 3. Lo que la verificación técnica **mata** — cuatro finalistas ajenos caen aquí

Esto es lo más valioso del cruce: cuatro ideas que otro modelo puso en su top 5 no son construibles tal como están descritas.

**ProofPic (gemini #1) — imposible.** Todo el producto es "las fotos se borran solas a las 24 h sin abrir la app". **PhotoKit no permite borrar fotos en silencio**: el sistema interpone siempre una hoja de confirmación ("¿Permitir que X borre la foto?"), no hay API para suprimirla, y `BGTaskScheduler` tampoco garantiza la ventana de 24 h. El informe tiene una sección entera dedicada a "restricciones de plataforma descubiertas" y no menciona ninguna de las dos.

**TaperKit (gemini #5) — imposible.** Depende de escribir pautas en `HKMedicationSchedule`. **Ese símbolo no existe.** Y un ingeniero de DTS de Apple lo confirma en los foros: *"la API de medicación es de solo lectura, así que no puedes escribir un evento de dosis en el almacén de HealthKit"*. Los tipos reales (`HKMedicationDoseEvent`) tienen inicializador inaccesible.

**Gestor de automatizaciones NFC (deepseek #3) — la premisa es falsa.** La lectura NFC en background **no registra nada en silencio**: muestra una notificación del sistema que el usuario debe tocar, y si el teléfono está bloqueado debe desbloquearlo primero. Además: solo iPhone XS+, solo universal links (nada de esquemas propios), requiere Associated Domains, y se desactiva mientras Wallet o la cámara estén en uso. Dos toques mínimo. A eso hay que sumar la fiabilidad física real (2-3 intentos por lectura, documentado por usuarios).

**Tarjeta → pase de Wallet (claude #4) — riesgo regulatorio que cancela el negocio.** Es la idea mejor argumentada de las que caen, y por eso duele. Técnicamente funciona y Pass2U demuestra que hay dinero (2,8 K valoraciones, 4,3★, #60 en top-grossing de Compras en EE. UU.). Pero la **guía 1.5 de App Review** exige que los pases estén *"firmados con un certificado dedicado asignado al propietario de la marca o marca registrada del pase"*, y la **3.2.1(iv)** advierte de que otros usos *"pueden resultar en el rechazo de la app y **la revocación de las credenciales de Wallet**"*. Firmar el carnet del gimnasio de otro con tu certificado es exactamente el caso prohibido. Que Pass2U lleve años haciéndolo prueba que la aplicación de la norma es laxa, no que la norma no exista: es un negocio entero colgando de un certificado que Apple puede revocar de un día para otro, sin aviso y sin apelación. Para un desarrollador solo, es la peor forma posible de riesgo.

Y dos premisas menores que también caen: **generar y distribuir App Intents dinámicamente** (deepseek, wildcard 1) es imposible — los App Intents se compilan en el binario; y **`CMHeadphoneMotionManager` en segundo plano** (gemini C7) no tiene mecanismo soportado, porque iOS no tiene un background mode de movimiento.

> Nota de método que vale la pena conservar: hay un hilo en los foros de Apple donde un desarrollador no conseguía compilar por un entitlement `com.apple.developer.alarmkit` **que no existe**, y el hilo termina con él confirmando que *"un LLM había generado el entitlement falso"*. Es exactamente el modo de fallo que aparece en tres de estos cinco informes.

---

## 4. Por qué el candidato musical sale del top 5

Esta sección sustituye a una versión anterior en la que la práctica instrumental con Music Understanding aparecía en segundo lugar. La revisión no se debe a que el fundador no toque un instrumento: eso era el menor de sus problemas. Se debe a que, al quitar el founder fit de la ecuación y mirar solo la monetización, quedan al descubierto tres problemas estructurales y un sesgo metodológico.

### 4.1 El sesgo: la convergencia entre modelos no es convergencia entre usuarios

Tres informes independientes propusieron esta idea, y eso pesó mucho en la primera clasificación. Revisando la evidencia que aporta cada uno, la convergencia se explica de otra manera:

| Informe | Evidencia de demanda que aporta |
|---|---|
| chatGPT | **Ninguna de usuario.** Su propia ficha lo admite: sobrevive *"no porque la competencia sea baja —no lo es— sino porque la plataforma acaba de cambiar"* |
| claude | Evidencia de **precios de competidores**, no de dolor de usuario |
| claude-advanced | Dos hilos de foro de recomendación de apps, de 2016 y sin volumen |

Los tres encontraron primero el framework y después el problema. Eso es exactamente el modo de fallo que el prompt original advertía en su principio nº 1: *"NO propongas algo simplemente porque existe una API interesante"*. Tres modelos entusiasmados con el mismo juguete nuevo no son tres señales independientes de mercado; son una sola señal, y es sobre la API.

### 4.2 Los tres problemas estructurales

**Adopción.** Music Understanding es exclusivo de iOS 27, publicado hace una semana. Un producto que lo exija no tiene base instalada hasta bien entrado 2027. No es un matiz de calendario: es que el momento de cobrar llega dieciocho meses después del momento de construir.

**El titular recibe el mismo regalo.** Anytune tiene 4,9 estrellas, 8.300 valoraciones, un equipo activo y exactamente el usuario objetivo. Music Understanding es gratis **también para ellos**, y para Capo, y para Moises. La ventaja que estarías explotando no es una ventaja tuya: es una capacidad de plataforma que tu competidor mejor posicionado puede adoptar en semanas, con su marca y su base instalada ya hechas. Competir contra un incumbente que recibe tu misma arma y llega antes al mismo usuario es una mala posición estructural, toque el fundador el piano o no.

**El techo del DRM se estrecha con el tiempo.** El producto solo puede analizar ficheros que el usuario posee. En 2026 la mayoría de la gente no tiene música en ficheros locales, y la tendencia va en la dirección contraria. Moises resuelve esto porque procesa en servidor lo que el usuario sube; tú no puedes tocar el catálogo de Apple Music ni el de Spotify. El mercado direccionable no solo es pequeño: **encoge cada año**.

### 4.3 Qué haría falta para que volviera

Si la respuesta a las tres objeciones apareciera, la idea vuelve. En concreto: que en seis meses Anytune y Capo **no** hayan adoptado el framework (comprobable mirando sus changelogs), y que un sondeo en comunidades de guitarra y bajo muestre que la gente sigue trabajando sobre ficheros propios. Es barato de vigilar y no cuesta nada dejarlo en observación. Pero no es donde empezar.

**Una nota sobre el founder fit, ya que se ha relajado el criterio.** Tener razón sin ser usuario es posible, pero se paga: hay que reclutar cinco o seis músicos reales y validar con ellos cada decisión de producto durante meses. Es un coste asumible. Simplemente no compensa pagarlo por un producto que además llega tarde, compite contra quien recibe la misma capacidad y apunta a un mercado que se encoge.

---

## 5. Los 5 mejores, ordenados por monetización

Criterio: **dinero demostrado × probabilidad real de que un desarrollador solo lo capture × que sobreviva a la verificación técnica.** El founder fit deja de ser criterio de exclusión y pasa a ser un coste a pagar, señalado en cada ficha.

---

### 1.º — Contador automático de días por jurisdicción (Schengen 90/180 + residencia fiscal)

Se mantiene primero, y al relajar el founder fit se refuerza: es el candidato donde menos importa quién seas, porque el producto es un motor de reglas auditable con tests.

**Dinero demostrado, por dos vías independientes.** Schengen Simple: 2.500 valoraciones, 4,8★, **pago único de 7,99-14,99 £**, equipo diminuto. TrackingDays: **3,99 $/mes, activa desde 2013**, apuntando a *"snowbirds and overseas homeowners"*. Nomad Tracker ya prueba **129,99 £ vitalicio**. Que un producto sostenga a la vez pago único barato y suscripción mensual durante trece años significa que el gasto está normalizado en el segmento.

**El disparador externo.** El Entry/Exit System europeo está operativo en todas las fronteras Schengen desde el **9-10 de abril de 2026**. Hasta ahora el conteo dependía de sellos y de la memoria del viajero; ahora lo lleva la frontera y el error se detecta solo. Prensa local citando el caso: *"very nasty trap for British second home owners"*.

**Dónde está el dinero que nadie ha cogido.** Schengen puro está resuelto. La capa de al lado —**residencia fiscal multi-jurisdicción con evidencia auditable en PDF**— tiene mayor consecuencia económica, no tiene marca dominante y soporta precio 5-10× superior.

**Coste de no ser el usuario:** bajo. Las reglas están escritas y son públicas; se verifican con tests de casos límite, no con intuición.

**El spike que decide:** `CLMonitor` + visitas durante un cruce real o simulado. Si la atribución automática de país no es fiable, el producto pierde su única ventaja sobre una calculadora web.

---

### 2.º — Cuadrante de turnos → Calendario, con alarma (AlarmKit)

Sube al segundo puesto porque tiene **la mejor evidencia de usuario de los cinco informes** y porque la relajación del founder fit no le afecta: cualquiera entiende un cuadrante de turnos.

**La señal.** Tres artefactos distintos, con URL y fecha: un usuario de Amazon Flex que dedicó **tres horas** a automatizarlo; una petición de **agosto de 2026** con PDF tabular; y un Shortcut para baristas de Starbucks calificado *"life changing"* **cuyo autor lo siguió corrigiendo en 2026**. Gente construyendo y **manteniendo** software casero durante meses para la misma fricción. Es literalmente el patrón que el prompt original definía como la señal más valiosa.

**Lo que lo convierte en producto: AlarmKit.** El trabajo no acaba cuando el turno entra en el calendario; acaba cuando **suena la alarma correcta el martes a las 5:40 porque el turno cambió el domingo**. AlarmKit (iOS 26, verificado) permite por primera vez a un tercero disparar una alarma de sistema que atraviesa Silencio y Focus sin entitlement especial, sostenida por un daemon aunque la app esté cerrada. La cadena completa —foto o PDF → Vision + Foundation Models → EventKit → AlarmKit— no era construible hace quince meses.

**Dinero: la parte más floja de esta ficha, y hay que decirlo.** ShiftInbox opera en gratis + desbloqueo vitalicio; Supershift vende suscripción. Ninguno de los informes consiguió un precio ni un número de valoraciones verificable. **La evidencia de demanda es la mejor del conjunto; la de disposición a pagar es la peor de los cinco finalistas.** Esa asimetría es el riesgo real.

**Coste de no ser el usuario:** bajo, pero hay que conseguir veinte cuadrantes reales de gente real antes de escribir código.

**El spike que decide:** esos veinte cuadrantes por Vision + Foundation Models. Si ShiftInbox ya resuelve bien el 80 % del corpus, llegas tarde.

---

### 3.º — Registro de kilómetros para autónomos europeos

Sube al podio precisamente porque el criterio ahora es monetización: **es el único del top 5 con ingreso recurrente demostrado a escala real**.

**Dinero.** MileIQ subió de 5,99 $ a **8,99 $/mes en 2026, un +50 %**, con 80.000 reseñas de cinco estrellas de por medio: eso genera una masa localizable de gente descontenta buscando alternativa. El rango de la categoría va de **15 a 108 $/año**. Magica cobra 14,99 $/año y su argumento comercial es literalmente *"sin servidores"*, que es tu ventaja estructural regalada.

**El hueco.** El mercado europeo está mal servido por apps pequeñas con localización desigual: 0,26 €/km en España, GoBD en Alemania, barème en Francia. Los líderes son estadounidenses y la fiscalidad no se traduce.

**El riesgo, que es el mayor de los cinco.** Competidores financiados, y **la fiabilidad de detección de inicio y fin de trayecto se juzga en las reseñas de una estrella**. Si fallas ahí, ninguna localización fiscal te salva. Y el diferencial puede degenerar en precio, que es la peor forma de competir.

**Coste de no ser el usuario:** medio-alto. Si no conduces por trabajo, no vas a notar cuándo la detección falla ni por qué. Mitigable pagando a tres o cuatro autónomos para que lo usen durante un mes.

---

### 4.º — Registro de nicho con captura por cámara (arquetipo: parámetros de acuario)

Baja un puesto por techo, no por calidad. Sigue en el top 5 porque **es el que con más probabilidad terminas y publicas**, y eso tiene valor propio: enseña el ciclo completo de publicar, cobrar y dar soporte con riesgo casi nulo.

**El hueco mejor documentado del conjunto.** Hilo de Reef2Reef titulado literalmente *"me sorprende lo malas que son las opciones"*, cuatro páginas, con el autor desmontando las tres apps del mercado: *"Aquarimate: pagué 10 $, la interfaz parecía diseñada en 2012, no conseguí borrar una entrada errónea"*; *"AquaticLog: ¿el plan pro de 25 $/año solo para recordatorios? ¿Para recordatorios?"*. Titular con quince meses sin actualizar, peaje de tres capas que sus usuarios llaman deshonesto, soporte muerto. Los entrantes de 2025-26 tienen 1 y 3 valoraciones.

**El ángulo iOS:** `DataScannerViewController` leyendo el display digital del comprobador con la cámara. No es otro formulario; es el que elimina teclear con las manos mojadas.

**El límite, sin adornos.** 625 + 401 valoraciones es todo el mercado visible. Ganarlo entero son **1.000-3.000 €/mes**. Con la monetización como objetivo declarado, eso lo sitúa cuarto y no primero.

**Coste de no ser el usuario:** bajo. El dominio se aprende en una tarde y la comunidad es extremadamente conversadora.

---

### 5.º — Informe fotográfico de visita técnica generado en el dispositivo

**Entra al top 5 precisamente porque se ha relajado el founder fit.** Lo había descartado en mi informe original por eso; con la monetización como criterio dominante, merece el puesto.

**Es el ingreso por cliente más alto de todo el conjunto, por un orden de magnitud.** CompanyCam cobra **63-79 $/mes para 1-2 usuarios y 199-249 $/mes en su nivel Scale**, y en 2026 eliminó el mínimo de tres usuarios, abriendo un camino real de licencia individual. Sus quejas documentadas —*"casos sin resolver durante más de dos meses"*, ausencia de facturación y planificación— son la especificación de lo que falta. Y Spectacular demuestra una cuña de bajo compromiso muy interesante: **gratis con informe a 14,99 $**, es decir, pago por entregable.

**La palanca iOS:** PhotoKit + Vision para anotar, **Foundation Models on-device para redactar el borrador del informe** (la parte que hasta 2025 exigía una API de IA de pago), `SpeechTranscriber` para dictar la nota de cada foto, PDFKit para el entregable. Sin backend, sin coste por token.

**El trade que hay que aceptar conscientemente.** Spectacular tiene **60 valoraciones** tras años. Esto **no se vende por descubrimiento en la App Store**: se vende por asociaciones gremiales, boca a boca en obra y llamadas de onboarding. El dato duro de RevenueCat lo confirma: Business es la categoría más lenta en alcanzar 1.000 $/mes, 113 días de mediana. Es un negocio con ventas y soporte, no una app indie clásica — y eso choca de frente con trabajar a tiempo completo y con responsabilidades familiares.

**Coste de no ser el usuario:** alto en discernimiento, bajo en aprendizaje. No necesitas saber instalar una caldera; necesitas que tres instaladores te digan si el PDF les sirve para cobrar. Pero tienes que salir a buscarlos.

---

## 6. Qué haría con esto

El orden del ranking no es el orden de ejecución.

**Primero, tres spikes de dos días.** Cada uno puede matar un candidato antes de escribir producto:

1. `CLMonitor` + visitas en un cruce real o simulado → decide el #1.
2. Veinte cuadrantes reales por Vision + Foundation Models → decide el #2.
3. `DataScannerViewController` sobre el display de un comprobador digital → decide el #4.

**Después, la decisión de fondo, que ya no es técnica sino de forma de vida:** el #3 y el #5 tienen el dinero, y los dos exigen algo que el #1, el #2 y el #4 no exigen — el #3 competir de frente con empresas financiadas en una métrica (fiabilidad de detección) que se juzga públicamente en reseñas de una estrella, y el #5 vender por teléfono. Si estás dispuesto a eso, el orden es 3 → 1 → 5. Si no, el orden es **1 → 2 → 4**, y el techo realista del conjunto es de unos pocos miles de euros al mes, que es exactamente el objetivo que te habías marcado.

**Y el modelo de monetización, sea cual sea el elegido: el de forScore.** Pago por adelantado de 24,99 $, más una capa Pro anual genuinamente opcional a 14,99 $, más un pase de 30 días a 2,99 $ para quien lo necesita una semana concreta. 43.000 valoraciones y 4,8 estrellas lo avalan, y encaja con el dato duro de RevenueCat: los muros de pago duros convierten al **10,7 %** a día 35 frente al **2,1 %** del freemium, con 8× los ingresos por instalación a día 60.
