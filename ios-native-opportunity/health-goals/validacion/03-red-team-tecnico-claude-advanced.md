# Technical & Product Red Team — Health Goals

**Fecha:** 2 de octubre de 2026
**Plataforma de referencia:** iOS 27 / watchOS 27 (publicados el 14 de septiembre de 2026), con soporte a iOS 26
**Método:** cada afirmación técnica se ha contrastado contra documentación de Apple Developer, sesiones WWDC, respuestas de ingenieros de Apple/DTS en los Developer Forums, App Review Guidelines (versión del 8 de junio de 2026), el Program License Agreement y Apple Support. Lo que no se pudo verificar en fuente primaria está marcado como **[NO VERIFICADO]** y recopilado en la sección 15.

---

## 1. Resumen ejecutivo

**Veredicto: SÓLIDO CON RESTRICCIONES.** No existe ningún impedimento técnico, de plataforma o de seguridad que destruya la tesis. HealthKit permite el flujo completo (intención → baseline → objetivos → progreso → gap) sobre pasos, distancia y workouts, y de forma parcial sobre minutos de ejercicio. Pero el producto solo es viable si acepta explícitamente estos límites:

1. **El baseline de 8 semanas no está garantizado en iOS 27.** El nuevo prompt de autorización ofrece al usuario "Past 30 Days and Future Data" o "All Recorded Data and Future Data". Si elige 30 días, el baseline se reduce a ~4 semanas sin que podamos impedirlo. Es detectable (`getEarliestAuthorizedSampleDate`), pero el motor de objetivos debe funcionar con 4 semanas.
2. **Minutos de ejercicio y energía activa dependen del Apple Watch.** Sin Watch, HealthKit solo produce pasos y distancia de forma pasiva. Los minutos de ejercicio solo llegan vía workouts guardados. El producto para usuarios sin Watch se reduce a pasos + distancia + workouts de terceros.
3. **La app no puede saber si el usuario denegó la lectura.** Un HealthKit "casi vacío" y un permiso denegado son indistinguibles por diseño. El onboarding necesita una rama de "no veo datos" que no acuse al usuario.
4. **Nada se actualiza con el iPhone bloqueado.** Confirmado por ingenieros de Apple: HealthKit está cifrado con el dispositivo bloqueado y la app no se despierta hasta el primer desbloqueo. Background delivery es "best effort" con tope horario para pasos. Suficiente para un loop semanal; incompatible con cualquier promesa de tiempo real.
5. **Los workouts no se deduplican solos.** Las statistics queries deduplican pasos y distancia igual que la app Salud (confirmado por Apple), pero los workouts de Strava + Watch aparecen duplicados y debemos resolverlos nosotros. Es el mayor riesgo de confianza del usuario.
6. **Ningún objetivo vive en Apple.** No existe API para escribir objetivos de anillos ni objetivos semanales. Los objetivos viven solo en nuestra app, y en local: el PLA prohíbe usar iCloud/CloudKit para información de salud identificable, y un objetivo de peso lo es.
7. **Publicidad: permitida sin targeting, pero desaconsejada.** La documentación de HealthKit dice textualmente que se pueden servir anuncios en una app con HealthKit siempre que no se usen datos de HealthKit para servirlos. Con las condiciones de 2.5.18 y ATT, el riesgo de revisión es real. El One-Pager ya propone pago único; mantenerlo.
8. **Apple no entrega hoy este loop, pero se acerca.** El rediseño de Salud anunciado el 9 de septiembre de 2026 (pestaña Insights, recomendaciones "For You", Longevity, Health Age) es cualitativo, no fija objetivos numéricos semanales. Es una señal concreta, no teórica. Ventana estimada de diferenciación: 12-18 meses.
9. **Foundation Models no es necesario para el MVP.** Cinco intents soportados se resuelven con chips de UI. FM queda como mejora opcional con fallback obligatorio (solo iPhone 15 Pro o posterior, Apple Intelligence activado).
10. **Peso: tratar solo como tendencia, nunca como objetivo numérico.** "Perder 15 kg" se debe traducir a objetivos de actividad y mostrar la tendencia de peso. Un objetivo de kilos activa 1.4.1 de App Review, el RD 1907/1996 en España y el Acceptable Use de Foundation Models en dominios médicos.

---

## 2. Matriz de datos HealthKit

| Dato | Identificador | Tipo | Quién lo produce de forma nativa | Histórico | Query recomendada | Background | Limitaciones verificadas |
|---|---|---|---|---|---|---|---|
| Pasos | `stepCount` | Acumulativo | iPhone y Apple Watch ("The system automatically records samples on iPhone and Apple Watch") | Sin límite documentado en iPhone; Watch conserva ~1 semana (DTS) | `HKStatisticsCollectionQuery` + `.cumulativeSum` | Sí, tope horario explícito en iOS | Muestras pueden estar "condensed/coalesced"; usar statistics queries, no `HKSampleQuery` |
| Distancia | `distanceWalkingRunning` | Acumulativo | iPhone y Apple Watch | Igual que pasos | Igual que pasos | Sí; tope horario [NO VERIFICADO para este tipo, plausible] | Igual que pasos |
| Energía activa | `activeEnergyBurned` | Acumulativo | Docs: solo Apple Watch. Un Frameworks Engineer afirma que iPhone sin Watch la estima desde iOS 16 | Igual | Igual | Sí; tope [NO VERIFICADO] | La doc no se compromete con iPhone; tratar como "Watch o terceros" |
| Minutos de ejercicio | `appleExerciseTime` | Acumulativo | **Solo Apple Watch** de forma pasiva. Los `HKWorkout` guardados también suman al anillo | Igual | `HKActivitySummaryQuery` si queremos coincidir con Fitness; statistics si queremos semana propia | Sí; tope [NO VERIFICADO] | Sin Watch no existe salvo por workouts. Un usuario iPhone-only no tiene baseline de minutos |
| Workouts | `HKWorkout` (`workoutActivityType`, `duration`, `statistics(for:)`, `workoutActivities`) | Objeto, no cuantitativo | Watch (app Entreno), apps de terceros | Sin límite documentado | `HKSampleQuery` + `predicateForWorkouts` o `HKAnchoredObjectQuery` | Sí (observer sobre `workoutType()`) | **No se deduplican**. `totalEnergyBurned` deprecado en iOS 18, `totalDistance` deprecado en 27.2. `statistics(for:)` puede ser nil si el workout no se creó con `HKWorkoutBuilder` (WWDC22) |
| Tiempo de pie / movimiento | `appleStandTime`, `appleMoveTime` | Acumulativo | Watch | Igual | Statistics | Sí | Fuera del alcance v1 |
| Peso | `bodyMass` | Discreto | Nadie de forma nativa; básculas vía app companion o entrada manual | Sin límite | `HKStatisticsCollectionQuery` + `.discreteAverage` / `mostRecent` | Sí | Escaso, irregular, a menudo con `HKMetadataKeyWasUserEntered` |

**Permisos:** cada tipo tiene permiso de lectura y de escritura por separado. Requiere `NSHealthShareUsageDescription` (la app crashea sin ella), entitlement `com.apple.developer.healthkit` y, para background, `com.apple.developer.healthkit.background-delivery` (sin él, `enableBackgroundDelivery` falla con `errorAuthorizationDenied`).

**Disponibilidad de plataforma:** iOS, watchOS, visionOS e iPadOS 17+ (compilando contra SDK 17+). En Mac/Catalyst `isHealthDataAvailable()` devuelve false. Activar HealthKit añade `healthkit` a `UIRequiredDeviceCapabilities`; hay que quitarlo si queremos distribuir en iPad sin HealthKit.

---

## 3. Baseline histórico

**¿Podemos ofrecer valor inmediatamente tras el onboarding?** Sí para pasos, distancia y workouts. Condicionado para minutos de ejercicio. Con dos matices que cambian el diseño:

### 3.1 Autorización limitada en iOS 27 (hallazgo crítico)

Documentación oficial ("Authorizing access to health data"): "After people review data type access, a second screen prompts them to choose how much historical data to grant your app, either a recent limited window or their full history." Un hilo del foro (agosto 2026, sin respuesta de Apple) describe las dos opciones: "Past 30 Days and Future Data" y "All Recorded Data and Future Data", con el botón Allow desactivado hasta elegir.

Consecuencias verificadas:

- "Limited authorization is the only authorization state your app can positively identify." Se detecta con `getEarliestAuthorizedSampleDate(for:)` (iOS 27+), que devuelve la fecha más antigua legible por tipo.
- Apple indica: "Adjust your app's workflow to work with less data."
- El límite se evalúa contra el `endDate` de la muestra.
- No hay callback cuando el usuario cambia el permiso, ni API pública para llevarle a los ajustes de privacidad de Salud (foro, no Apple).

**Impacto:** el One-Pager promete "analiza ocho semanas". En iOS 27 eso es una aspiración. El motor de objetivos debe producir una propuesta razonable con 4 semanas y explicar la diferencia ("Con 30 días de historial la propuesta es menos precisa. Puedes ampliar el acceso en Salud").

### 3.2 Eficiencia de las queries

- `HKStatisticsCollectionQuery` con `intervalComponents = 1 día` y `anchorDate` a inicio de día, enumerando con `enumerateStatistics(from:to:)`. Apple lo documenta exactamente para ventanas de 3 meses. Intervalos sin datos devuelven cantidad nil (no cero): hay que distinguir "sin datos" de "0 pasos".
- Advertencia de Apple: "Statistical calculations can take a considerable amount of time, especially if there are a large number of samples involved." Ejecutar fuera del hilo principal y cachear resultados diarios.
- Workouts: `HKStatisticsCollectionQuery` no admite workouts ("you must perform the appropriate query and process the data yourself"). Hay que listar los `HKWorkout` del período y contarlos por semana en la app.
- Medias, medianas y distribución por día de la semana son cálculo nuestro sobre los agregados diarios. Trivial.

### 3.3 Casos problemáticos

| Caso | Qué ocurre realmente | Mitigación |
|---|---|---|
| Usuario sin Apple Watch | Pasos y distancia completos. Energía activa estimada (no garantizada por docs). Minutos de ejercicio solo si usa apps que guardan workouts. `HKActivitySummary` existe pero solo con anillo Move | Detectar presencia de Watch vía `HKSourceQuery`/`HKDevice`. Ofrecer solo métricas con baseline real. No proponer minutos si no hay Watch |
| HealthKit casi vacío | Indistinguible de permiso denegado: "your app doesn't know whether someone granted or denied permission to read data" | Rama de onboarding "no veo datos de X" con instrucciones de Ajustes. No acusar al usuario. Permitir baseline manual mínimo como fallback explícito |
| Datos duplicados (iPhone + Watch) | Resuelto por statistics queries para cantidades (ver sección 4) | Nunca sumar `HKSampleQuery` a mano |
| Múltiples fuentes de workouts | No hay deduplicación | Heurística propia (sección 4) |
| Datos importados (migraciones de Fitbit, Garmin, etc.) | Aparecen como fuente distinta; a menudo con `HKMetadataKeyWasUserEntered` o sin `HKDevice` | Excluir o ponderar por fuente en el baseline; mostrar fuentes al usuario |
| Cambio de dispositivo | Sincronización iCloud cifrada extremo a extremo; histórico se restaura. Watch nuevo no recupera su semana local, pero el iPhone conserva todo | Calcular siempre en iPhone, nunca en watchOS |
| Datos muy antiguos | HealthKit condensa muestras de workouts de hace "al menos unos meses" en series | Usar statistics queries, que lo manejan de forma transparente |

---

## 4. Calidad y consistencia de los datos

**¿Podemos calcular progreso de forma suficientemente fiable como para que el usuario confíe?** Sí para pasos y distancia, con la condición de usar exactamente las mismas queries que la app Salud. Con riesgo moderado para workouts. Con incertidumbre documental para días que cruzan husos horarios.

### 4.1 Deduplicación de cantidades: resuelta por Apple

- Doc `HKStatistics`: "By default, these queries automatically merge the data from all of your data sources before performing the calculations."
- Frameworks Engineer (hilo 710937): "If you query for data using HKStatisticsCollectionQuery, HealthKit will do the appropriate merging for you: this is what Health is doing when you're looking at data in that app. If you're simply using HKSampleQuery... it is unlikely that you will be able to match HealthKit's merge algorithm correctly."
- DTS (hilo 759709): el resultado de `HKStatisticsQuery` "should be the same as the one shown in system-provided Health.app".
- WWDC20: la statistics query ignora los pasos duplicados del iPhone cuando llevas el Watch y suma los del iPhone cuando lo olvidas en casa.

El algoritmo no está documentado y la prioridad de fuentes que el usuario ordena en Salud no es legible por API [NO VERIFICADO que exista API; ningún hilo tiene respuesta de Apple]. No importa mientras usemos statistics queries sin `separateBySource`.

### 4.2 Workouts: deduplicación nuestra

No existe mecanismo de Apple. `HKMetadataKeySyncIdentifier` solo deduplica escrituras de la misma app. Escenario típico: el usuario corre con Strava en el Watch; Strava escribe el workout y la app Entreno también. Resultado: 2 workouts, 1 entrenamiento. Heurística necesaria: agrupar workouts cuyo intervalo se solape más de un umbral (p. ej. 50% de duración) y mismo tipo o tipo compatible; quedarse con uno; mostrar al usuario "hemos unido 2 registros" para que pueda corregir. Es trabajo de producto, no de plataforma, y es donde se pierde o gana la confianza.

Además, `HKWorkout.statistics(for:)` solo se calcula automáticamente para workouts creados con `HKWorkoutBuilder`/`HKLiveWorkoutBuilder` (WWDC22). Para workouts legacy de terceros hay que consultar las muestras asociadas con `predicateForObjects(from: workout)`. Para el MVP basta con contar workouts y usar `duration`, que siempre existe.

### 4.3 Muestras manuales y borradas

- Manuales: `HKMetadataKeyWasUserEntered` es una convención que fija quien escribe; la app Salud la pone en entradas manuales. Mostrar en el detalle y permitir excluirlas del progreso.
- Borradas: `HKAnchoredObjectQuery` devuelve `HKDeletedObject`. Advertencia de Apple: "Deleted objects are temporary... To guarantee that you receive notifications for all deleted objects, create an HKObserverQuery and register it for background delivery." Si guardamos snapshots semanales, hay que recalcular desde HealthKit, no acumular deltas.

### 4.4 Retrasos de sincronización

DTS (hilo 774953): "The HealthKit store synchronization between an iPhone and its paired Apple Watch is not real-time, and there is no API that can speed up the pace. Some actions, like bringing a HealthKit-enabled app to the foreground, can trigger a synchronization, but that is completely up to the system." Un informe de desarrollador habla de ~10 minutos para pasos [NO VERIFICADO como dato de Apple].

Consecuencia: "llevas 28.500 pasos" puede subir retroactivamente. El copy debe mostrar la hora del dato ("actualizado a las 17:40") y el widget debe marcar datos obsoletos. Nunca mostrar "0" cuando la query falla.

### 4.5 Husos horarios y días

- Las muestras se almacenan con fechas absolutas. `HKMetadataKeyTimeZone` es opcional y, según informes sin respuesta de Apple, suele ser nil en muestras del sistema [NO VERIFICADO].
- Solo `HKActivitySummary` tiene días "como los percibe el usuario": "This day may be longer or shorter than 24 hours (for example, if the user traveled across time zones)."
- Cómo la app Salud agrupa pasos por día durante un viaje: **no documentado**. Cómo se comporta `anchorDate` con DST o cambio de zona: **no documentado**.

Decisión de producto recomendada: objetivos **semanales**, no diarios (coincide con el principio "Weekly over daily" del One-Pager). La semana absorbe el error de borde de un día en viaje. El cálculo "pasos/día que te faltan" se recalcula cada vez y se presenta como aproximado ("~6.850").

---

## 5. Objetivos y APIs Apple

| Dato | Leer | Escribir | Dónde vive |
|---|---|---|---|
| Progreso diario Move/Exercise/Stand (`HKActivitySummary`) | Sí | No | Apple |
| Objetivos diarios Move/Exercise/Stand (`activeEnergyBurnedGoal`, `exerciseTimeGoal`, `standHoursGoal`) | Sí | **No**: "changes made to the object's properties have no affect on the values in the HealthKit store... you can't save HKActivitySummary objects to the store" | Apple, solo lectura |
| `isPaused` (anillos pausados, iOS 18) | Sí | No | Apple |
| Objetivos semanales (workouts/semana, pasos/semana, minutos/semana) | **No existe el concepto** | **No existe** | **Solo nuestra app** |
| Training Load, Vitals, Readiness, Workout Buddy | No hay API | No | Apple, cerrado |
| Planes de Fitness / Fitness+ Custom Plans | No | No | Apple, cerrado |
| `workoutEffortScore` / `estimatedWorkoutEffortScore` (iOS 18) | Sí | Sí | Páginas de doc vacías |
| WorkoutKit (`CustomWorkout`, `WorkoutPlan`, `WorkoutScheduler`) | Propios | Propios | Programa entrenamientos individuales en la app Entreno del Watch. `WorkoutGoal` es por sesión, no semanal. Sin cambios en iOS 26/27 |
| Zonas de FC y potencia (`HKWorkoutZone`, iOS 27) | Sí | Configuración propia | Irrelevante para v1 |

**Conclusión:** los objetivos deben vivir íntegramente en la app. Podemos leer los objetivos de anillos del usuario como señal de baseline (si tiene Move goal de 500 kcal y lo cierra 5 días de 7, es información útil), pero no escribirlos ni sincronizarlos.

**Almacenamiento:** App Review 5.1.3(ii) prohíbe "store personal health information in iCloud" y el PLA 3.3.3(D) prohíbe usar "iCloud, the iCloud Storage APIs, CloudKit APIs" para "sensitive, individually-identifiable health information". Ninguno define el término. Un objetivo de 49.000 pasos derivado del historial es zona gris; un objetivo de peso es claramente información de salud. **Recomendación:** objetivos y snapshots en local (SwiftData/archivo en App Group); sin CloudKit en v1. Perder los objetivos al cambiar de iPhone es un coste aceptable frente al riesgo de rechazo.

---

## 6. Background y actualización

| Escenario | Clasificación | Justificación verificada |
|---|---|---|
| Progreso actualizado con la app en primer plano | **Garantizado** | Dispositivo desbloqueado por definición; `statisticsUpdateHandler` funciona |
| Progreso actualizado en background en ~1 hora | **Best effort** | `enableBackgroundDelivery`: "on iOS, stepCount samples have an hourly maximum frequency". Requiere Background App Refresh activado, entitlement, llamar al completion handler (tras 3 fallos HealthKit deja de despertar la app) y registrar observers en `didFinishLaunchingWithOptions` |
| Widget actualizado en ~1 hora tras datos nuevos | **Best effort** | La app, al despertar, escribe snapshot y llama `reloadTimelines`. Eso **sí** consume el presupuesto de WidgetKit (40-70 recargas/día para widgets muy vistos; sin exención para recargas desde background). El widget puede además consultar HealthKit directamente en `getTimeline` si el dispositivo está desbloqueado |
| Widget en tiempo real | **Imposible** | Entradas de timeline ≥ ~5 min, recargas coalescidas, tope horario de HealthKit. Solo `Text(date, style:)` es "vivo" |
| Actualización con el dispositivo bloqueado (noche) | **Imposible** | Frameworks Engineer (hilo 694223): "if you are using background delivery, your app will not be launched for new data until the device unlocks and the Health database is available." Doc: "the device encrypts the HealthKit store when the user locks the device." Error `errorDatabaseInaccessible` |
| `BGAppRefreshTask` como refuerzo | **Best effort** | ~30 s, "the system doesn't guarantee launching the task at the specified date". `BGProcessingTask` corre con el dispositivo idle (= bloqueado = HealthKit ilegible). `BGContinuedProcessingTask` (iOS 26) es solo para tareas iniciadas por el usuario |
| Live Activity para estado semanal | **Imposible** | Máximo 8 h activa, 12 h en pantalla de bloqueo |
| App Intents "¿Cómo voy esta semana?" | **Viable** | App Shortcuts con frases; intent en proceso de la app lee HealthKit con normalidad; en extensión aplica la regla de widgets. Snippets interactivos en iOS 26 |

**Extensiones y HealthKit (Frameworks Engineer, hilo 653814):** "Widgets can get access to health data if the host app has permission... However, it doesn't have the ability to request authorization." Llamar `requestAuthorization` desde una extensión devuelve el error 111. Usar `getRequestStatusForAuthorization` y pedir permiso solo en la app.

**¿Podemos mantener progreso y widget suficientemente actualizados sin prometer tiempo real?** Sí. Un loop semanal tolera una latencia de 1-2 horas. Lo que no tolera es mentir: el widget debe mostrar "datos de las 17:40" y nunca inventar un cero.

---

## 7. Goal recommendation engine

### 7.1 Dónde termina el producto y dónde empieza la medicina

| Zona | Ejemplo | Clasificación | Base |
|---|---|---|---|
| Objetivos de actividad derivados del propio historial | "Hiciste ~2 entrenamientos/semana; te proponemos 3" | **Producto / general wellness** | FDA General Wellness (6 ene 2026): "Claims to promote physical fitness, such as to help log, track, or trend exercise activity... improve physical fitness" son wellness. Ejemplo 2 de la guía describe casi exactamente esta app. MDCG 2019-11: sin "medical purpose" no es software médico |
| Objetivo de "peso saludable" o "ayudar con metas de pérdida de peso" sin referencia a enfermedad | "Mantener una tendencia de peso saludable" | **General wellness en EE. UU.**, pero **publicidad regulada en España** | FDA Category 1 incluye "assist with weight loss goals". RD 1907/1996 art. 4.2 prohíbe publicidad "que sugieran propiedades específicas adelgazantes o contra la obesidad" |
| Objetivo numérico de kilos | "Perderás 15 kg en 20 semanas" | **Fuera del producto** | Promesa de resultado no validable (App Review 1.4.1: "if the level of accuracy or methodology cannot be validated, we will reject your app"); RD 1907/1996; dominio médico en el Acceptable Use de Foundation Models |
| Referencia a enfermedad | "Reduce tu riesgo de diabetes", "trata la obesidad" | **Dispositivo médico / rechazo** | FDA: "A claim that a product will treat or diagnose obesity" cruza la línea. MDR: intended medical purpose |
| Prescripción de ejercicio | "Haz 3 series de sentadillas a 70% 1RM" | **Fuera del alcance declarado** | El One-Pager excluye "training plan application". WorkoutKit no es necesario |

### 7.2 Riesgo de seguridad en la progresión

El ejemplo del brief propone +67% en workouts (1,8 → 3), +50% en minutos (80 → 120) y +19% en pasos (5.900 → 7.000/día). No he encontrado una fuente de Apple sobre progresión segura, y no cito guías deportivas sin verificarlas [NO VERIFICADO]. Como red team señalo que App Review 1.4.5 prohíbe "urge customers to participate in activities (like bets, challenges, etc.)... in a way that risks physical harm". Reglas de producto recomendadas, a validar con asesoría:

- Tope de incremento por ciclo (p. ej. ≤ 20% sobre baseline por métrica y ≤ 1 workout/semana adicional).
- Nunca proponer objetivos a usuarios con baseline cero en esa métrica sin que fijen ellos el punto de partida.
- Primera semana siempre "mantener baseline", no "superar".
- Reducir objetivos automáticamente si dos semanas seguidas quedan por debajo del 50%.

### 7.3 Wording, disclaimers y App Review

- 1.4.1: "Apps should remind users to check with a doctor in addition to using the app and before making medical decisions." Apple aplica a su propio Watch: "Before starting or modifying any exercise program using Apple Watch, consult your physician." Apple no pone disclaimer junto a la sugerencia de objetivos, sino uno global. Replicar: un aviso en onboarding, en Ajustes y en la ficha de App Store.
- 5.1.1(ii): "Paid functionality must not be dependent on or require a user to grant access to this data." No condicionar el premium a conceder HealthKit; el premium desbloquea funciones, no el acceso a datos.
- 5.1.1(ix): apps en "healthcare" deben publicarse desde entidad legal, no desarrollador individual. Somos fitness, no healthcare, pero es prudente publicar como empresa.
- Vocabulario a evitar en toda la app y marketing: perder peso, adelgazar, quemar grasa, obesidad, déficit, tratar, prevenir, riesgo cardiovascular, médico, clínico, prescripción.
- Vocabulario seguro: moverte más, entrenar con regularidad, mantener tu ritmo, tendencia, progreso, lo que te falta esta semana.

### 7.4 Intent "Quiero perder 15 kg"

Respuesta de producto recomendada: aceptar la intención, no el número. "Te ayudaremos a moverte más y entrenar con regularidad. Mostraremos la tendencia de tu peso si la registras en Salud, pero no fijamos objetivos de kilos." Esto mantiene el One-Pager ("excluye prescripciones dietéticas, déficit calórico o promesas de pérdida de grasa") y evita las tres zonas de riesgo.

---

## 8. Foundation Models

**¿Es realmente necesario?** No para el MVP. El One-Pager define cinco intenciones soportadas. Cinco chips o una lista cubren el 100% del alcance con cero riesgo. Un campo libre con FM añade:

| Aspecto | Verificado |
|---|---|
| Structured generation | `@Generable` y `@Guide`, "constrained sampling prevents the model from producing malformed output". Un enum `@Generable` como clasificador es la recomendación explícita de Apple para salidas seguras |
| Disponibilidad | `SystemLanguageModel.default.availability`: `.deviceNotEligible`, `.appleIntelligenceNotEnabled`, `.modelNotReady`. Si no está disponible "it isn't even downloaded" |
| Dispositivos | iPhone 15 Pro/Pro Max y todos los iPhone 16, 17 y 18 (support.apple.com/121115, actualizado 14 sep 2026). Excluye iPhone 15 base y anteriores, y dispositivos comprados en China continental |
| Idiomas | Español soportado. Requiere idioma de dispositivo y de Siri coincidentes |
| Contexto | 4.096 tokens en iOS 26.0-26.3; 8.192 en iOS 27. Leer `contextSize` en runtime |
| Modelo | ~3B parámetros (iOS 26): "not designed for world knowledge or advanced reasoning". Modelo nuevo en iOS 27 "rebuilt from the ground up" |
| Rate limits | Solo en background: "This error will only happen if your app is running in the background" |
| Guardrails | `guardrailViolation` y `refusal`. Apple reconoce falsos positivos ("We're actively working to improve the guardrails and reduce false positives"), influidos por locale. No hay informes específicos de fitness/peso [NO VERIFICADO en ambos sentidos] |
| Acceptable Use | Prohíbe outputs "inaccurate or dangerous... in high-risk domains, including in employment, medical, legal, or finance" y "dependency or spiraling user interactions detrimental to a user's mental health" |

**Recomendación:** v1 con chips + campo libre opcional que mapea por reglas (keywords) a los cinco intents. Si en v2 se añade FM, solo como clasificador a un enum cerrado (los cinco intents + `unknown`), con fallback a chips cuando `availability != .available` o ante cualquier error, y nunca para generar los números del objetivo. Esto coincide con el principio del One-Pager: "important numerical decisions should derive from explicit logic".

---

## 9. Widgets y surfaces

Arquitectura verificada:

1. La app (foreground u despertada por background delivery) calcula el snapshot semanal: objetivos, progreso, gap, "pasos/día restantes", timestamp del dato.
2. Lo persiste en el App Group (archivo o UserDefaults compartidos). Sin CloudKit.
3. Llama a `WidgetCenter.shared.reloadTimelines(ofKind:)`.
4. El widget, en `getTimeline`, intenta leer HealthKit directamente (funciona si la app tiene permiso y el dispositivo está desbloqueado); si falla, renderiza el snapshot marcado como "actualizado a las HH:MM".
5. Nunca llama a `requestAuthorization` desde el widget (error 111).

| Verificación | Resultado |
|---|---|
| HealthKit desde la extensión | Sí, con permiso del host y dispositivo desbloqueado |
| Cadencia | 40-70 recargas/día para widgets frecuentes, ~15-60 min; coalescidas; reducidas en páginas poco visitadas |
| Stale data | Inevitable por la noche y con el iPhone bloqueado. Mostrar timestamp |
| Privacidad / redacción | Widget de pantalla de bloqueo: usar `privacySensitive()` para ocultar cifras con el dispositivo bloqueado. Botones inactivos en dispositivo bloqueado |
| Interacción | Botón `AppIntent` "Actualizar" garantiza recarga sin consumir presupuesto, solo desbloqueado |
| Publicidad en widget | Prohibida por 2.5.18 ("should not be included in extensions... widgets") |
| Apple Watch | Complicaciones WidgetKit; el Watch en la muñeca está desbloqueado, pero solo conserva ~1 semana de datos. Fuera de v1, como dice el One-Pager |

Un widget con dos estados ("ON TRACK" / "2 entrenamientos + 12.400 pasos restantes") es técnicamente sencillo. Lo difícil es que el número sea creíble: con latencia de una hora y el gap de un día entero, mostrar "12.400 pasos" a las 23:00 cuando el usuario ya ha hecho 3.000 más es el fallo que destruye confianza. Preferir rangos y timestamp.

---

## 10. Apple encroachment

### Señales concretas (con fecha y fuente primaria)

| Fecha | Qué | Solapa con el loop | Clasificación |
|---|---|---|---|
| Desde watchOS 1; watchOS 11 (jun 2024) | Anillos con objetivos diarios; "Your Apple Watch suggests goals based on your previous performance"; resumen semanal cada lunes con ajuste de objetivos; objetivos por día de semana; pausar anillos | **Parcial.** Es baseline → objetivo → ajuste semanal, pero diario, en kcal/min/horas, sin intención, sin "qué te falta esta semana" y requiere Watch para Exercise/Stand | Shipped, solapa parcial |
| watchOS 26 (sep 2025), watchOS 27 (sep 2026) | Workout Buddy: "You're 18 minutes away from closing your Exercise ring. So far this week, you've run 6 miles." Español desde watchOS 27 | **Adyacente.** Comenta durante el entreno, no fija objetivos ni planifica | Shipped, adyacente |
| 14 sep 2026 | Readiness (Series 12 / Ultra 4): puntuación 0-10 diaria con recomendación de intensidad | Adyacente: "cuánto hoy", no "cuánto falta esta semana" | Shipped, adyacente |
| iOS 26 (sep 2025) | Workouts personalizados con objetivos por sesión en Fitness para iPhone | Adyacente | Shipped |
| **9 sep 2026** | **Rediseño de Salud con Apple Intelligence**: pestaña Insights con resumen actualizado durante el día y recomendaciones "For You" basadas en datos del usuario; Longevity (7 categorías incl. movimiento); Health Age; Movement Evaluations con "an exercise plan to help them improve their balance". En beta iOS 27.2; Apple dice que llega "later this year", solo inglés EE. UU. | **Señal concreta.** Apple pasa de mostrar datos a recomendar. Hoy las recomendaciones son cualitativas ("incorporar intervalos") sin objetivos numéricos semanales ni gap. Es el lugar natural donde Apple añadiría exactamente nuestro loop | **Riesgo concreto, 12-18 meses** |
| Feb-may 2026 (Bloomberg, secundario) | "Project Mulberry"/Health+ reducido; Eddy Cue lo juzgó "not competitive" vs Oura/WHOOP; funciones se integran por piezas en Salud durante el ciclo iOS 27 | Confirma dirección, descarta producto de coaching independiente a corto plazo | Secundario |
| WWDC26 (8 jun 2026) | Única sesión HealthKit: zonas de FC/potencia. Sin "What's new in HealthKit" desde WWDC22. Sin API de objetivos | Apple no abre APIs de objetivos a terceros | Verificado |
| 22 sep 2026 (Bloomberg) | Banda sin pantalla tipo WHOOP, no antes de 2028 | Teórico | Secundario |

### Lectura de red team

Apple **no** entrega hoy "intención → objetivos semanales medibles desde HealthKit → gap restante". Pero tiene todas las piezas (datos, anillos sugeridos, resumen semanal, Workout Buddy con cálculo de "te faltan 18 minutos", y ahora Insights/For You) y acaba de declarar públicamente que va a recomendar acciones a partir de datos. El riesgo no es que Apple copie una app pequeña; es que la función "For You" de iOS 27.x o iOS 28 incluya "esta semana te faltan 2 entrenamientos" como mejora obvia. Si eso ocurre, Health Goals queda relegado a usuarios sin Watch (donde Apple es más débil) y a quienes quieran objetivos semanales en vez de anillos diarios.

Diferenciación defendible hoy: (1) semanal vs diario; (2) workouts y pasos como unidades que el usuario entiende, no kcal; (3) usuarios sin Watch; (4) español e idiomas donde Apple va tarde (el rediseño de Salud sale solo en inglés EE. UU.); (5) el usuario decide el objetivo, Apple lo sugiere en su propia unidad.

---

## 11. Privacy y App Review

### 11.1 Publicidad: la pregunta crítica

**¿Podemos utilizar publicidad en una app con HealthKit?** Sí, sin targeting, con condiciones estrictas. Desaconsejado.

- Documentación HealthKit ("Protecting user privacy"), textual: "Note that you may still serve advertising in an app that uses the HealthKit framework, but you can't use data from the HealthKit store to serve ads."
- Prohibido por cuatro textos independientes usar datos de HealthKit para publicidad: 5.1.3(i), 5.1.2(vi), 2.5.18 ("may not engage in targeted or behavioral advertising based on sensitive user data such as health/medical data (e.g. from the HealthKit APIs)") y PLA 3.3.3(H) ("not for serving advertising").
- 2.5.18 además: anuncios solo en el binario principal (no widgets ni watchOS), mostrar al usuario toda la información usada para el targeting, botones de cierre, mecanismo para reportar anuncios.
- ATT obligatorio si el SDK usa IDFA o datos cross-app (5.1.2(i) y PLA 3.3.3(E)); no se puede condicionar funcionalidad al consentimiento.
- Apple: "Developers are responsible for all code included in their apps", incluido el SDK de anuncios.
- Data brokers: PLA 3.3.3(H): "You must not share or sell information collected through these APIs to advertising platforms, data brokers, or information resellers."

Riesgo práctico: cualquier señal derivada de HealthKit que llegue al SDK (pantalla "objetivo de peso", segmento "usuario activo") es uso de datos de HealthKit para publicidad. Un revisor no tiene forma de comprobarlo y puede rechazar por precaución. El One-Pager propone pago único; esta verificación lo refuerza. **Sin publicidad.**

### 11.2 Analytics

- 5.1.3(i) cubre "data gathered in the health, fitness, and medical research context" y prohíbe "use-based data mining purposes other than improving health management". PLA 3.3.3(H) solo permite revelar información obtenida vía HealthKit a terceros que presten un servicio de salud al usuario. Un proveedor de analytics no lo es.
- No hay texto de Apple sobre datos derivados o agregados [NO VERIFICADO]. Interpretación literal: "goal_accepted" sin valores es un evento de producto; "goal_accepted, target=3 workouts" ya es dato derivado de salud.
- Regla: eventos de interacción sin valores de salud; sin SDKs de analytics propiedad de redes publicitarias; consentimiento explícito; declarar "Health & Fitness" en la ficha de privacidad si algún atributo deriva de HealthKit.

### 11.3 Otros puntos verificados

- 5.1.1(ii): consentimiento para recoger datos de uso aunque sean anónimos; **"Paid functionality must not be dependent on or require a user to grant access to this data"**.
- 5.1.1(iii): minimización. Pedir solo los tipos necesarios para los objetivos que el usuario elige, no todo HealthKit en el arranque (HIG: "Request access to health data only when you need it").
- 5.1.2(iii): no reconstruir perfiles desde datos "anonymized" o "aggregated".
- 2.5.1: HealthKit debe usarse "for health and fitness purposes and integrate with the Health app".
- Política de privacidad obligatoria para toda app con HealthKit, con enlace en App Store Connect y en la app.
- Privacy label: los datos leídos de HealthKit entran en la categoría "Health" aunque sean de fitness. Si no salen del dispositivo, no se declaran.
- iCloud: ver sección 5. Sin CloudKit para objetivos ni snapshots en v1.

---

## 12. Riesgos críticos

| # | Riesgo | Prob. | Impacto | Mitigación |
|---|---|---|---|---|
| R1 | Apple añade objetivos semanales y gap en Salud "For You" (iOS 27.x / 28) | Media-alta | Letal para usuarios con Watch | Lanzar antes de WWDC27; posicionar en semanal, sin Watch, español; validar JTBD en ≤ 8 semanas |
| R2 | Usuario iOS 27 concede solo 30 días | Alta | Baseline degradado | Motor diseñado para 4 semanas; detectar con `getEarliestAuthorizedSampleDate`; explicar y permitir ampliar |
| R3 | Workouts duplicados (Strava + Watch) rompen el conteo "2/3" | Alta en usuarios activos | Pérdida de confianza inmediata | Heurística de solape; mostrar fusión; permitir corregir |
| R4 | Usuario sin Watch no tiene baseline de minutos ni energía | Alta (la mitad del target "ideally Apple Watch") | Producto reducido a pasos + distancia + workouts de terceros | Detectar Watch; adaptar métricas ofrecidas; no prometer minutos |
| R5 | Permiso denegado indistinguible de datos vacíos | Media | Onboarding roto en silencio | Rama "no veo datos" con instrucciones; nunca mostrar ceros como progreso |
| R6 | Widget/gap desactualizado de noche y con iPhone bloqueado | Certeza | Cifras falsas si no se marca | Timestamp visible; rangos; nunca inventar cero |
| R7 | Intent de peso arrastra a terreno médico / publicitario regulado | Media | Rechazo App Review, riesgo legal en España | Peso solo como tendencia; sin objetivos de kilos; vocabulario controlado |
| R8 | Guardado de objetivos en CloudKit interpretado como "health information in iCloud" | Baja-media | Rechazo | Local-only en v1 |
| R9 | Analytics con valores de salud a terceros | Media si se descuida | Rechazo o retirada (5.1.2) | Eventos sin valores; consentimiento |
| R10 | Statistics queries lentas con 8 semanas y muchas fuentes | Baja | UX del onboarding | Background thread, caché diaria, progreso visible |

---

## 13. Kill criteria

| Criterio propuesto en el brief | ¿Se cumple? | Evidencia |
|---|---|---|
| HealthKit no permite el flujo esperado | **No** | Lectura de histórico, agregados diarios, workouts, observers y background delivery están documentados y funcionan |
| Datos demasiado inconsistentes | **No**, con condición | Pasos/distancia coinciden con Salud si usamos statistics queries (Apple lo confirma). Workouts requieren dedup propia. Días en viaje no documentados: se absorbe con objetivos semanales |
| Background insuficiente | **No** | Best effort horario es suficiente para un loop semanal. Solo sería kill si el producto prometiera tiempo real |
| Goal engine entra en riesgo médico | **No**, si se excluyen objetivos numéricos de peso y referencias a enfermedad | FDA General Wellness ejemplo 2; MDCG 2019-11; App Review 1.4.1 |
| Apple ya proporciona el mismo loop | **No hoy.** Señal concreta para 2027 | Rediseño de Salud 9 sep 2026 es cualitativo. Sin API de objetivos para terceros |
| Monetización en conflicto con HealthKit/privacy | **No** con pago único. **Sí** si se insistiera en publicidad con cualquier señal de salud | Doc HealthKit permite ads no dirigidos; 2.5.18 y PLA 3.3.3(H) hacen el riesgo inaceptable |

**Kill criteria adicionales que sí deberían activar la cancelación durante el MVP:**

- Si en la prueba con usuarios reales más del 30% elige "Past 30 Days" y el motor con 4 semanas produce propuestas que los usuarios rechazan mayoritariamente.
- Si la tasa de workouts duplicados en usuarios con apps de terceros supera lo que la heurística corrige sin intervención manual (umbral sugerido: >10% de semanas con conteo corregido por el usuario).
- Si Apple anuncia en una beta de iOS 27.x objetivos semanales numéricos con gap restante en la pestaña Insights.

---

## 14. MVP técnico mínimo si sobrevive

Vertical slice, sin IA, iOS 26+ con rama iOS 27 para autorización limitada:

1. **Onboarding de intención:** 5 chips (moverme más, entrenar con regularidad, constancia, caminar más, actividad con tendencia de peso). Sin campo libre en v1.
2. **Autorización HealthKit:** pedir lectura solo de `stepCount`, `workoutType()` y, si se detecta Watch, `appleExerciseTime`. `bodyMass` solo si el usuario elige el quinto intent. Tras autorizar, en iOS 27 llamar a `earliestAuthorizedSampleDate` y fijar la ventana real (56 días o lo concedido).
3. **Baseline:** `HKStatisticsCollectionQuery` diaria `.cumulativeSum` para pasos (y minutos si aplica); `HKSampleQuery` de workouts del período con dedup por solape. Calcular media semanal, mediana y semanas con datos. Si menos de 2 semanas con datos, pasar a rama "no veo datos".
4. **Propuesta:** 2 métricas máximo (pasos/semana y workouts/semana). Regla transparente: baseline redondeado + incremento acotado; semana 1 = mantener. Pantalla "por qué te proponemos esto" con los datos del baseline.
5. **Aceptación:** el usuario edita los números. Guardado local (App Group).
6. **Progreso y gap:** cálculo semana en curso (lunes a domingo por calendario del usuario) con statistics queries; gap = objetivo − progreso; "por día restante" = gap / días restantes, mostrado como aproximado y con timestamp.
7. **Actualización:** `HKObserverQuery` + `enableBackgroundDelivery(.hourly)` para pasos y workouts; recalcular snapshot y `reloadTimelines`. `BGAppRefreshTask` como refuerzo.
8. **Widget:** sistema small/medium y accessory; dos estados; lectura directa de HealthKit en `getTimeline` con fallback a snapshot; `privacySensitive()`; botón "Actualizar".
9. **App Intent:** "¿Cómo voy esta semana?" devolviendo el snapshot como texto y snippet.
10. **Disclaimer global** en onboarding, Ajustes y ficha de App Store. Política de privacidad. Sin analytics con valores de salud. Sin CloudKit. Sin anuncios.

Instrumentación mínima para los KPIs del One-Pager, sin valores de salud: `healthkit_authorized_shown`, `limited_history_detected` (bool), `goal_proposed`, `goal_edited`, `goal_accepted`, `progress_viewed_midweek`, `widget_added`, `week_completed` (bool), `goal_continued`.

---

## 15. Afirmaciones no verificadas

Todo lo siguiente se ha usado con cautela y requiere comprobación empírica o fuente adicional:

1. Tope horario de background delivery para `distanceWalkingRunning`, `activeEnergyBurned` y `appleExerciseTime` en iOS. Apple solo nombra `stepCount` explícitamente.
2. Que un iPhone sin Watch genere `activeEnergyBurned` de forma fiable. Afirmado por un Frameworks Engineer en foro (iOS 16), no por la documentación.
3. Que `HKMetadataKeyTimeZone` sea nil en muestras del sistema. Informes de desarrolladores sin respuesta de Apple.
4. Cómo agrupa la app Salud los pasos por día durante cambios de huso horario, y cómo se comporta `anchorDate` con DST. No documentado.
5. Que no exista API para leer el orden de prioridad de fuentes de la app Salud. Ningún hilo con respuesta de Apple; ausencia en la documentación.
6. Magnitud del retraso de sincronización Watch → iPhone (~10 min). Informe de desarrollador.
7. Comportamiento de las opciones exactas del prompt de autorización limitada ("Past 30 Days"). Documentado como "recent limited window"; las etiquetas literales provienen de un hilo del foro sin respuesta de Apple.
8. Falsos positivos de guardrails de Foundation Models en prompts de fitness o peso. Sin informes específicos encontrados.
9. Que las recomendaciones "For You" del rediseño de Salud no incluyan objetivos numéricos al lanzarse. Basado en el texto de Apple del 9 sep 2026 y hands-on de la beta 27.2 (secundario); puede cambiar.
10. Que un objetivo semanal derivado de HealthKit sea o no "personal health information" a efectos de 5.1.3(ii). Apple no define el término.
11. Reglas de progresión segura (incrementos ≤ 20%). No verificado contra fuentes deportivas; es propuesta de red team.
12. Informe de 2026 sobre resultados inconsistentes de `HKStatisticsCollectionQueryDescriptor` en iOS 27. Hilo no leído.
13. MDR Recital 19 ("software intended for life-style and well-being purposes is not a medical device"). EUR-Lex no respondió; citado de memoria.

---

## 16. Fuentes primarias

### Apple Developer Documentation (HealthKit)
- https://developer.apple.com/documentation/healthkit
- https://developer.apple.com/documentation/healthkit/about-the-healthkit-framework
- https://developer.apple.com/documentation/healthkit/setting-up-healthkit
- https://developer.apple.com/documentation/healthkit/authorizing-access-to-health-data
- https://developer.apple.com/documentation/healthkit/protecting-user-privacy
- https://developer.apple.com/documentation/healthkit/reading-data-from-healthkit
- https://developer.apple.com/documentation/healthkit/executing-statistics-collection-queries
- https://developer.apple.com/documentation/healthkit/accessing-condensed-workout-samples
- https://developer.apple.com/documentation/healthkit/hkhealthstore/getearliestauthorizedsampledate(for:completion:)
- https://developer.apple.com/documentation/healthkit/hkhealthstore/earliestpermittedsampledate()
- https://developer.apple.com/documentation/healthkit/hkhealthstore/authorizationstatus(for:)
- https://developer.apple.com/documentation/healthkit/hkhealthstore/requestauthorization(toshare:read:completion:)
- https://developer.apple.com/documentation/healthkit/hkhealthstore/ishealthdataavailable()
- https://developer.apple.com/documentation/healthkit/hkhealthstore/enablebackgrounddelivery(for:frequency:withcompletion:)
- https://developer.apple.com/documentation/healthkit/hkupdatefrequency
- https://developer.apple.com/documentation/healthkit/hkerror/code/errordatabaseinaccessible
- https://developer.apple.com/documentation/healthkit/hkquantitytypeidentifier/stepcount
- https://developer.apple.com/documentation/healthkit/hkquantitytypeidentifier/appleexercisetime
- https://developer.apple.com/documentation/healthkit/hkquantitytypeidentifier/activeenergyburned
- https://developer.apple.com/documentation/healthkit/hkquantitytypeidentifier/distancewalkingrunning
- https://developer.apple.com/documentation/healthkit/hkquantitytypeidentifier/bodymass
- https://developer.apple.com/documentation/healthkit/hkworkout
- https://developer.apple.com/documentation/healthkit/hkworkout/totalenergyburned
- https://developer.apple.com/documentation/healthkit/hkworkout/totaldistance
- https://developer.apple.com/documentation/healthkit/hkworkout/statistics(for:)
- https://developer.apple.com/documentation/healthkit/hkworkoutactivity
- https://developer.apple.com/documentation/healthkit/hkstatistics
- https://developer.apple.com/documentation/healthkit/hkstatisticsoptions
- https://developer.apple.com/documentation/healthkit/hkstatisticscollectionquery
- https://developer.apple.com/documentation/healthkit/hkstatisticscollection/enumeratestatistics(from:to:with:)
- https://developer.apple.com/documentation/healthkit/hkanchoredobjectquery
- https://developer.apple.com/documentation/healthkit/hkdeletedobject
- https://developer.apple.com/documentation/healthkit/hksourcequery
- https://developer.apple.com/documentation/healthkit/hkdevice
- https://developer.apple.com/documentation/healthkit/hkmetadatakeywasuserentered
- https://developer.apple.com/documentation/healthkit/hkmetadatakeytimezone
- https://developer.apple.com/documentation/healthkit/hkmetadatakeysyncidentifier
- https://developer.apple.com/documentation/healthkit/hkactivitysummary
- https://developer.apple.com/documentation/healthkit/hkactivitysummary/ispaused
- https://developer.apple.com/documentation/healthkit/hkactivitysummaryquery
- https://developer.apple.com/documentation/healthkit/hkquery/predicateforactivitysummary(with:)
- https://developer.apple.com/documentation/healthkitui/hkactivityringview
- https://developer.apple.com/documentation/workoutkit
- https://developer.apple.com/documentation/bundleresources/entitlements/com.apple.developer.healthkit
- https://developer.apple.com/documentation/bundleresources/information-property-list/nshealthshareusagedescription

### Apple Developer Documentation (WidgetKit, BackgroundTasks, App Intents, ActivityKit, Foundation Models)
- https://developer.apple.com/documentation/widgetkit/keeping-a-widget-up-to-date
- https://developer.apple.com/documentation/widgetkit/adding-interactivity-to-widgets-and-live-activities
- https://developer.apple.com/documentation/widgetkit/timelinereloadpolicy
- https://developer.apple.com/documentation/backgroundtasks/choosing-background-strategies-for-your-app
- https://developer.apple.com/documentation/backgroundtasks/bgprocessingtask
- https://developer.apple.com/documentation/backgroundtasks/bgcontinuedprocessingtaskrequest
- https://developer.apple.com/documentation/backgroundtasks/performing-long-running-tasks-on-ios-and-ipados
- https://developer.apple.com/documentation/appintents/app-shortcuts
- https://developer.apple.com/documentation/appintents/appintentsextension
- https://developer.apple.com/documentation/appintents/appintent/supportedmodes
- https://developer.apple.com/documentation/activitykit/displaying-live-data-with-live-activities
- https://developer.apple.com/documentation/foundationmodels
- https://developer.apple.com/documentation/foundationmodels/generating-swift-data-structures-with-guided-generation
- https://developer.apple.com/documentation/foundationmodels/improving-the-safety-of-generative-model-output
- https://developer.apple.com/documentation/foundationmodels/supporting-languages-and-locales-with-foundation-models
- https://developer.apple.com/documentation/foundationmodels/systemlanguagemodel/availability-swift.enum/unavailablereason
- https://developer.apple.com/documentation/foundationmodels/languagemodelsession/generationerror/ratelimited(_:)
- https://developer.apple.com/documentation/technotes/tn3193-managing-the-on-device-foundation-model-s-context-window
- https://developer.apple.com/apple-intelligence/acceptable-use-requirements-for-the-foundation-models-framework/

### WWDC
- WWDC20 10664 "Getting started with HealthKit" (deduplicación): https://developer.apple.com/videos/play/wwdc2020/10664/
- WWDC22 10005 "What's new in HealthKit" (statistics solo con HKWorkoutBuilder): https://developer.apple.com/videos/play/wwdc2022/10005/
- WWDC23 10016 WorkoutKit: https://developer.apple.com/videos/play/wwdc2023/10016/
- WWDC25 286, 301, 248 Foundation Models: https://developer.apple.com/videos/play/wwdc2025/286/ , /301/ , /248/
- WWDC25 227 BackgroundTasks: https://developer.apple.com/videos/play/wwdc2025/227/
- WWDC26 207 "Deliver workout insights with HealthKit workout zones": https://developer.apple.com/videos/play/wwdc2026/207/
- WWDC26 241 "What's new in the Foundation Models framework": https://developer.apple.com/videos/play/wwdc2026/241/
- WWDC26 keynote: https://developer.apple.com/videos/play/wwdc2026/101/

### Apple Developer Forums (respuestas de Frameworks Engineer / DTS)
- 710937 (merge en statistics queries): https://developer.apple.com/forums/thread/710937
- 759709 (statistics = app Salud): https://developer.apple.com/forums/thread/759709
- 711396 (energía activa en iPhone sin Watch): https://developer.apple.com/forums/thread/711396
- 799086 (sharingDenied no informa de lectura): https://developer.apple.com/forums/thread/799086
- 694223 (sin callbacks con dispositivo bloqueado): https://developer.apple.com/forums/thread/694223
- 824819 (DTS, mayo 2026, lectura bloqueada): https://developer.apple.com/forums/thread/824819
- 653814 (HealthKit en widgets, error 111): https://developer.apple.com/forums/thread/653814
- 774953 y 823473 (sync Watch no es tiempo real): https://developer.apple.com/forums/thread/774953 , https://developer.apple.com/forums/thread/823473
- 732468 (Watch conserva ~1 semana): https://developer.apple.com/forums/thread/732468
- 732944 (iPadOS 17 y SDK): https://developer.apple.com/forums/thread/732944
- 756815 (isPaused): https://developer.apple.com/forums/thread/756815
- 797676 (duración Live Activity): https://developer.apple.com/forums/thread/797676
- 805378, 806542, 798113, 787736, 797955 (Foundation Models): https://developer.apple.com/forums/thread/805378 , /806542 , /798113 , /787736 , /797955
- 842499 (autorización limitada iOS 27, sin respuesta de Apple): https://developer.apple.com/forums/thread/842499

### App Review, PLA, privacidad
- App Store Review Guidelines (8 jun 2026): https://developer.apple.com/app-store/review/guidelines/
- Apple Developer Program License Agreement: https://developer.apple.com/support/terms/apple-developer-program-license-agreement/
- User privacy and data use: https://developer.apple.com/app-store/user-privacy-and-data-use/
- App privacy details: https://developer.apple.com/app-store/app-privacy-details/
- HIG HealthKit: https://developer.apple.com/design/human-interface-guidelines/healthkit
- Platform Security, health data: https://support.apple.com/guide/security/protecting-access-to-users-health-data-sec88be9900f/web
- Health Privacy Overview (mayo 2023): https://www.apple.com/privacy/docs/Health_Privacy_White_Paper_May_2023.pdf

### Apple Support / Newsroom
- Prioridad de fuentes en Salud: https://support.apple.com/en-us/108779
- Apple Intelligence, dispositivos e idiomas (14 sep 2026): https://support.apple.com/en-us/121115
- Objetivos de anillos: https://support.apple.com/guide/watch/adjust-your-activity-ring-goals-apd29b30023c/watchos
- Seguridad Apple Watch (no es dispositivo médico): https://support.apple.com/en-ca/guide/watch/apdcf2ff54e9/11.0/watchos/11.0
- Workout Buddy: https://support.apple.com/guide/watch/use-workout-buddy-apd65c7938e6/watchos
- Fitness+ Custom Plans: https://support.apple.com/guide/fitness-plus/use-custom-plans-apdf222051d8/ios
- Newsroom 9 sep 2026, rediseño de Salud: https://www.apple.com/newsroom/2026/09/apple-advances-health-and-fitness-capabilities-using-apple-intelligence/
- Newsroom 14 sep 2026, iOS 27: https://www.apple.com/newsroom/2026/09/major-updates-for-apples-software-platforms-are-now-available/
- Newsroom 14 sep 2026, Readiness: https://www.apple.com/newsroom/2026/09/apple-unveils-apple-watch-ultra-4/
- Newsroom jun 2025, watchOS 26: https://www.apple.com/newsroom/2025/06/watchos-26-delivers-more-personalized-ways-to-stay-active-and-connected/
- Newsroom jun 2024, watchOS 11: https://www.apple.com/newsroom/2024/06/watchos-11-brings-powerful-health-and-fitness-insights/

### Regulatorio
- FDA General Wellness: Policy for Low Risk Devices (6 ene 2026): https://www.fda.gov/media/90652/download
- MDCG 2019-11 (software como dispositivo médico): https://health.ec.europa.eu/system/files/2020-09/md_mdcg_2019_11_guidance_en_0.pdf
- Real Decreto 1907/1996 (publicidad con pretendida finalidad sanitaria): https://www.boe.es/buscar/act.php?id=BOE-A-1996-18085

### Secundarias (solo contexto de mercado, no base de afirmaciones técnicas)
- 9to5Mac 5 feb 2026 (Health+ reducido), 24 may 2026 (Mulberry retrasado), 16 sep 2026 (beta 27.2 Salud)
- MacRumors 16 sep 2026 (beta 27.2 Salud), 8 jun 2026 (recap WWDC26)
- Bloomberg 22 sep 2026 (banda sin pantalla)

---

## Resultado

# SÓLIDO CON RESTRICCIONES

Es viable si respetamos explícitamente estos límites:

1. Motor de objetivos diseñado para 4 semanas de histórico, con 8 como mejora, y detección de autorización limitada en iOS 27.
2. Métricas ofrecidas según dispositivo: sin Apple Watch, solo pasos, distancia y workouts de terceros.
3. Objetivos semanales, no diarios, para absorber latencia, sincronización y husos horarios.
4. Deduplicación de workouts propia, visible y corregible por el usuario.
5. Progreso y widget siempre con timestamp; nunca tiempo real; nunca cero por fallo de lectura.
6. Objetivos y snapshots solo en local; sin CloudKit en v1.
7. Peso únicamente como tendencia; sin objetivos de kilos; vocabulario sin referencias a adelgazar, enfermedad o medicina; disclaimer global.
8. Sin publicidad. Sin analytics con valores de salud. Premium no condicionado al permiso de HealthKit.
9. Sin Foundation Models en el MVP; si se añade, solo como clasificador cerrado con fallback.
10. Validar el JTBD en un plazo corto: la señal concreta del rediseño de Salud de Apple fija una ventana de 12-18 meses.
