# iOS-Native Opportunity Discovery

> Investigación realizada el **21 de septiembre de 2026**.
> Línea base de plataforma: **iOS 26** (septiembre 2025, base instalada real) e **iOS 27** (publicado el **14 de septiembre de 2026**, adopción ≈ 0 % en el momento de escribir).
> Perfil del fundador: Senior iOS Engineer, solo, tiempo parcial, sin conocimiento sectorial profundo, sin equipo, sin inversión.

**Limitaciones metodológicas que debes conocer antes de leer nada más.** Reddit (`reddit.com`), los cuerpos de los hilos de `discussions.apple.com` y las páginas de RoutineHub estuvieron **bloqueados** durante toda la investigación. Eso elimina la fuente más densa de testimonio en primera persona ("construí un Shortcut para…", "lo llevo en una hoja de cálculo"). La evidencia de abajo procede de: documentación oficial de Apple, WWDC, Apple Developer Forums, foros MacRumors, Hacker News (vía API de Algolia, con puntuaciones y fechas), la API de búsqueda de GitHub (estrellas como proxy de dolor compartido), fichas de App Store (precio, IAP, nota, nº de valoraciones, última actualización), tableros de feature-request con recuento de votos, y foros verticales (Reef2Reef, Cloudy Nights, Intervals.icu, AppleVis, DJ TechTools, Home Assistant, ScubaBoard, BirdForum). Donde la evidencia es débil, está marcado como **débil**. Donde no pude verificar algo, lo digo.

---

## 1. Executive summary

**Conclusión corta:** sí hay oportunidades reales, pero casi ninguna está donde la gente espera. La mayoría del espacio "HealthKit + gráficas bonitas" acaba de ser absorbido por Apple este mismo mes. Las oportunidades que sobreviven al escrutinio tienen una de estas tres formas:

1. **Contar algo que el iPhone ya sabe y que cuesta dinero equivocarse.** Días de presencia por jurisdicción (Schengen 90/180, residencia fiscal), coste real de una carga eléctrica en casa para reembolso. Core Location genera el dato sin que el usuario introduzca nada; el error tiene consecuencia económica; la gente paga por adelantado y sin discutir. Es el patrón con mejor evidencia de todo el informe.
2. **Aprovechar una primitiva que Apple acaba de regalar y que antes costaba un equipo de DSP o una nube.** `SpeechAnalyzer`/`SpeechTranscriber` (transcripción larga on-device, iOS 26), **Music Understanding** (beats, tonalidad, estructura de canción, actividad por instrumento, on-device, iOS 27), `BGContinuedProcessingTask` (trabajo pesado en segundo plano con GPU, iOS 26). Los titulares de estos mercados cobran suscripción porque procesan en servidor; tú puedes cobrar una vez porque no tienes servidor.
3. **Ocupar un nicho apasionado que mantiene hojas de cálculo y cuyo titular está podrido.** Acuarios de arrecife, cuadernos de campo, práctica instrumental. Mercados pequeños (1–3 k €/mes techo realista) pero con competidores abandonados, pilas de peajes ("paga 10 $ por la app, 10 $/año por la sincronización y 10 $ por el almacenamiento") y soporte muerto.

**Lo que hay que evitar, con evidencia:**

- **Salud "estadísticas y tendencias hechas bien"**: Apple reescribió la app Salud en **septiembre de 2026** añadiendo Insights, Longevity, Health Age y evaluaciones de movimiento por cámara, con un agente de IA de salud y un rumoreado nivel "Health+" en camino. Es literalmente la tesis de producto de Bevel, Athlytic y Gentler Streak. No entres en una categoría que el dueño de la plataforma anunció hace tres días.
- **Trackers de garantías y recibos**: nueve o más apps en la tienda, **ninguna** con suficientes valoraciones para que Apple muestre una media. Eso no es un mercado abierto; es ausencia de demanda demostrada repetidamente.
- **Organizadores de capturas de pantalla**: 15 repos de GitHub creados en 2026, todos con 0–5 estrellas, y la app líder de la categoría con **1,0 estrellas**. Apple es dueña del punto de entrada (la hoja de acciones de la captura, con Visual Intelligence). Techo de precio observado: 2,99 $.
- **Aves**: Merlin de Cornell es gratis, 4,9 estrellas, 112 000 valoraciones y está financiada por una universidad. No se compite contra eso.
- **Puentes de sincronización hacia plataformas de entrenamiento**: precio 15–50 $/año y Strava, Garmin, Peloton o Fitbit pueden borrarte el producto (la última nota de versión de RunGap es literalmente *"Retired Fitbit integration"*).

**Lo que Apple simplemente no permite, y que mata ideas enteras antes de dibujarlas:** no hay API para leer notificaciones de otras apps, ni transacciones de Apple Pay, ni pases de Wallet de otros desarrolladores, ni los Health Records FHIR (analíticas, diagnósticos), ni para escribir dosis de medicación en Salud, ni para editar muestras que escribió otra fuente. FinanceKit exige cuenta de desarrollador **de organización**, categoría Finanzas y distribución en EE. UU. o Reino Unido. SensorKit exige aprobación de un comité de ética. NFC HCE exige entidad establecida en el EEE y un acuerdo con una entidad licenciada. La sección 10 recoge la lista completa.

**Realidad económica, para calibrar expectativas.** Según el informe *State of Subscription Apps 2026* de RevenueCat (115 000+ apps, 16 000 M$ de ingresos analizados): la mediana de ingresos un año después del lanzamiento es **≈ 72 $/mes**; solo el **17,3 %** de las apps llega a 1 000 $/mes en dos años y el **4,6 %** a 10 000 $/mes; las apps lanzadas antes de 2020 concentran el **69 %** de todos los ingresos por suscripción; y se lanzan **14 700 apps de suscripción al mes** frente a 2 000 en 2022. El buen resultado realista para una app de nicho bien ejecutada en 2026 es **500–5 000 €/mes en 12–24 meses**. Eso encaja exactamente con el objetivo que has definido, y es una razón más para elegir el modelo de pago que mejor convierte: **muro de pago duro o pago por adelantado** (conversión mediana a día 35 del **10,7 %** frente al **2,1 %** del freemium, y 8× los ingresos por instalación a día 60).

**Los cinco finalistas** (detalle en la sección 8): contador automático de días por jurisdicción; estudio de práctica instrumental on-device; transcripción y resumen largos 100 % locales; diario de parámetros de acuario con captura por cámara; e informe de salud listo para la consulta médica.

---

## 2. Apple capability map

Todas las filas verificadas contra `developer.apple.com` salvo donde se indica. Leyenda de **Entitlement**: *ninguno* / *capability en Xcode* (autoservicio) / *solicitud a Apple* (formulario) / *gestionado* (contrato, caso por caso).

### 2.1 Datos personales y contexto

| Framework | Qué obtiene realmente una app de terceros | Fuente del dato | Histórico | Pasivo/activo | Background | Fricción de permiso | Entitlement | Hardware | Región | Riesgo App Review | Indie suitability |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **HealthKit** | Lectura/escritura por tipo: quantity, category, workout, characteristic | histórico almacenado + inferencia del sistema | **Cambio en iOS 27**: el usuario elige *ventana reciente* o *histórico completo* en la autorización | pasivo tras autorizar | sí, `HKObserverQuery` + `enableBackgroundDelivery` | **alta** (dos hojas, toggles por tipo) | HealthKit = capability; **background delivery = `com.apple.developer.healthkit.background-delivery`**, también capability | iPhone; algunos tipos solo Watch | Clinical Records limitado por país | **alto** (guía 5.1.3) | **Alta** |
| **WorkoutKit** | Crear y sincronizar planes de entrenamiento a la app Entreno del Watch | autoría de la app | — | activo | no | media | ninguno | Apple Watch | — | bajo | Alta |
| **Core Motion** | Acelerómetro, giroscopio, magnetómetro, `CMDeviceMotion`, tipo de actividad | sensor en vivo | solo en vivo | pasivo | solo bajo un background mode permitido | media (`NSMotionUsageDescription`) | ninguno | coprocesador de movimiento | — | medio | Alta |
| **CMPedometer** | Pasos, distancia, pisos, cadencia, eventos | inferencia del coprocesador | **exactamente 7 días** en caché | pasivo | consulta al abrir; en vivo requiere bg mode | media | ninguno | coprocesador M | — | medio | Alta |
| **CMAltimeter** | Altitud relativa + presión; altitud absoluta (iOS 15+) | sensor en vivo | solo en vivo | pasivo | requiere bg mode | media | ninguno | barómetro | — | bajo | Alta |
| **Journaling Suggestions** | Eventos de vida que el usuario **selecciona** en el picker: lugares, entrenos, fotos, canciones, contactos, estado de ánimo | inferencia del sistema, elegido por el usuario | "reciente", ventana no documentada | **activo** (el usuario elige) | no | baja (la selección *es* el consentimiento) | `com.apple.developer.journal.allow` — la documentación actual dice **capability en Xcode**; ⚠️ no encontré ningún testimonio de indie que lo confirme | iPhone, iPadOS 26+ | — | medio | Media |
| **PhotoKit / PhotosUI** | Biblioteca completa o *limitada*; `PHPickerViewController` es fuera de proceso y **no pide ningún permiso** | contenido elegido por el usuario / histórico | toda la biblioteca si hay acceso | ambos | observadores solo en ejecución | PHPicker **baja**; PhotoKit completo **alta** | ninguno | — | — | **alto si pides acceso total** (5.1.1 prefiere pickers) | Alta |
| **EventKit (Calendario)** | Solo-escritura **o** acceso completo. **No hay nivel de solo-lectura.** El editor de EventKitUI funciona con cero permisos | histórico almacenado | toda la base | ambos | no despierta la app | escritura media; completo **alta** | ninguno | — | — | medio | Alta |
| **EventKit (Recordatorios)** | Solo acceso completo | histórico almacenado | completo | ambos | no | alta | ninguno | — | — | medio | Media |
| **Contacts** | Completo **o limitado** (el usuario elige contactos); `ContactAccessButton` concede contactos concretos **sin alerta** | histórico almacenado | toda la agenda | ambos | no | completo alta; ContactAccessButton **baja** | ninguno | — | — | **alto** (5.1.1 prohíbe construir bases de datos de contactos) | Media |
| **Core Location** | Coordenadas gruesas/precisas, rumbo, *visits*, monitorización de regiones y balizas | sensor en vivo + inferencia | *visits* solo en vivo, no consultable hacia atrás | ambos | **sí, varias vías** (ver 2.5) | *when-in-use* media; **Always alta** | Background Modes → Location (capability) | GPS | — | **alto** para Always + background | Alta |
| **MapKit** | Render de mapa, `MKLocalSearch`, geocoding, direcciones, Look Around | servicio Apple | — | activo | no | ninguna | ninguno (con throttling) | — | cobertura variable | bajo | Alta |
| **MusicKit** | Catálogo, biblioteca del usuario, reproducciones recientes, recomendaciones, reproducción | servicio Apple + histórico | ventana de "recientes" no documentada | ambos | solo bg de audio | media | servicio MusicKit en el portal (autoservicio) | — | según storefront | bajo | Media — **ver la advertencia de DRM en 2.6** |
| **WeatherKit** | Actual, minuto a minuto, horaria, diaria, alertas, sol/luna, medias históricas | servicio Apple | previsión + medias; sin archivo observado profundo | activo | no | ninguna | capability + servicio en el portal | — | precipitación al minuto y alertas limitadas | bajo, **atribución obligatoria** | Alta — 500 000 llamadas/mes incluidas en la cuota de desarrollador |

**Cambio crítico de iOS 27 en HealthKit.** Tras la hoja de permisos por tipo, aparece **una segunda hoja** donde la persona concede *histórico limitado* o *histórico completo*. `HKHealthStore.getEarliestAuthorizedSampleDate(for:)` te lo dice, pero Apple advierte: *"la autorización limitada es el único estado que tu app puede identificar positivamente"* — denegado y acceso completo son indistinguibles, y *"evita interpretar la ausencia de muestras antiguas como prueba de que no existen"*. **Cualquier producto cuya propuesta sea "analiza tus últimos cinco años de X" tiene ahora que detectar la concesión limitada, degradar con elegancia y convencer al usuario de ampliarla.** Esto es nuevo, tiene exactamente una semana, y es un detalle de UX que casi ninguna app competidora habrá resuelto todavía.

**Límites exactos de background delivery de HealthKit** (importan mucho para diseñar): el entitlement es obligatorio desde iOS 15; `HKCorrelationType` no está soportado; en iOS `stepCount` está limitado a **frecuencia horaria** pidas lo que pidas; en watchOS el presupuesto es de **4 actualizaciones/hora** compartidas con `WKApplicationRefreshBackgroundTask`; y **tres fallos consecutivos en llamar al completion handler y HealthKit deja de enviarte actualizaciones**.

### 2.2 Mundo físico y sensores

| Framework | Qué obtiene | Histórico | Background | Fricción | Entitlement | Hardware | Región | App Review | Indie |
|---|---|---|---|---|---|---|---|---|---|
| **AVFoundation cámara** | Grafo de captura completo, multi-cam, profundidad, RAW, ProRes | — | **no** (salvo extensión Locked Camera Capture) | media | ninguno | según lentes | — | medio (2.5.14 exige indicador de grabación) | Alta |
| **Vision** | Texto, caras, pose corporal/manos, saliencia, códigos, clasificación, **`RecognizeDocumentsRequest` (iOS 26: párrafos, listas y tablas, no solo líneas de OCR)** | — | sí dentro de `BGContinuedProcessingTask` | ninguna | ninguno | Neural Engine acelera | idiomas variables | bajo | **Alta** |
| **VisionKit `DataScannerViewController`** | Texto en vivo desde cámara con `TextContentType` (URL, teléfono, email, dirección, fecha, vuelo, moneda), códigos, `capturePhoto()` | — | no | media (cámara) | ninguno | `isSupported` filtra modelos viejos | idiomas variables | bajo | **Alta** |
| **Core NFC (lectura)** | NDEF, ISO7816/15693/FeliCa/MIFARE; hoja modal del sistema | — | no | baja | `com.apple.developer.nfc.readersession.formats` (capability) | iPhone 7+ | — | bajo | Alta |
| **Core NFC HCE** | Emulación de tarjeta ISO 7816-4 | — | no, ventana de 60 s | media | **gestionado por Apple**, contrato | iPhone | **solo EEE** | muy alto | **Nula** |
| **Core Bluetooth** | Central y periférico GATT, canales L2CAP, restauración de estado | — | sí (`bluetooth-central`/`peripheral` + state restoration) | media, o **baja vía AccessorySetupKit** | ninguno | BLE | — | medio | Alta |
| **Channel Sounding** ⚡ (iOS 27) | **Distancia con precisión métrica a cualquier periférico BLE 6.3** | continuo | no documentado | baja (picker de ASK) | ninguno más allá de ASK | **iPhone 17+** y periférico BLE 6.3 | — | bajo | Media (hardware) |
| **Nearby Interaction (UWB)** | Distancia y dirección entre iguales; accesorios de terceros | — | solo con par BLE conectado, **o desde iOS 18.4 si inicias una Live Activity al pasar a background** | media | ninguno | U1/U2, iPhone 11+ | UWB deshabilitado en algunas jurisdicciones (⚠️ sin lista verificada) | bajo | Media |
| **HomeKit** | Descubrir y añadir accesorios, leer/escribir características, automatizaciones `HMEventTrigger` que corren en el hub | persistente | las automatizaciones corren en el **hub**, no en tu app | media | `com.apple.developer.homekit` (capability) | hub para remoto | — | medio | Media |
| **MatterSupport** | Comisionar accesorios Matter en tu propio ecosistema | — | no | media | extensión + entitlement (⚠️ cadena exacta no verificada) | Thread/Matter | — | medio | Media |
| **Apple Watch — `HKWorkoutSession`** | **La concesión de background más potente de watchOS**: ejecución continua durante el entrenamiento, HR de alta frecuencia, movimiento, ubicación | — | **sí** | media | HealthKit | Apple Watch | — | alto si simulas entrenamientos para robar runtime | Alta |
| **Apple Watch — `WKExtendedRuntimeSession`** | Cuatro tipos con topes duros: self care (10 min), mindfulness (1 h), physical therapy (1 h), smart alarm (30 min, programable hasta 36 h antes). **Un solo tipo por app** | — | parcial | baja | Background Modes → tipo de sesión | Apple Watch | — | **alto si el tipo no encaja con tu app** | Media |
| **SensorKit** | Luz ambiente, PPG, ECG, temperatura de muñeca, uso de dispositivo, métricas de teclado, voz y cara | — | gestionado por el sistema | alta | **solicitud a Apple, solo investigación con aprobación de comité de ética** | iPhone + Watch | — | — | **Nula** |
| **AccessorySetupKit** (iOS 18) | Emparejar un accesorio Bluetooth/Wi-Fi concreto **sin la alerta de permiso de Bluetooth** | — | — | **baja** | ninguno | — | — | bajo | **Alta** |

Dos trampas de AccessorySetupKit que ahorran un día de depuración: las sesiones de Channel Sounding **solo funcionan con dispositivos emparejados vía ASK**, y si instancias `CBCentralManager` *antes* de que ASK termine, disparas la alerta de Bluetooth y **el picker de ASK ya no aparece**.

### 2.3 Audio

| Framework | Qué obtiene | Background | Fricción | Entitlement | Región/idioma | App Review | Indie |
|---|---|---|---|---|---|---|---|
| **`SFSpeechRecognizer`** (legado) | STT de forma corta, on-device o servidor | limitado | media-alta (**dos** prompts) | ninguno | lista de locales | bajo | Media |
| **`SpeechAnalyzer` + `SpeechTranscriber`** ⚡ (iOS 26) | **Transcripción larga on-device**, basada en actores, `AsyncSequence` de entrada y salida, fichero o captura en vivo, resultados volátiles → finalizados, sesgo de vocabulario vía `AnalysisContext`, modelos descargados con `AssetInventory` | no es un bg mode; combínalo con `BGContinuedProcessingTask` para ficheros | media (micro) | ninguno | `supportedLocales` / `installedLocales` | bajo | **Alta** |
| **Sound Analysis** | Clasificador integrado (`SNClassifierIdentifier.version1`) con ~300 clases (enumera con `knownClassifications`), **o tu propio modelo Core ML**; analizador de fichero y de stream | corre donde corra tu sesión de audio; con bg mode `audio`, clasificación continua | media (micro) | ninguno | etiquetas en inglés | **medio-alto** — micrófono siempre activo es bandera roja | Media |
| **ShazamKit** | Reconocimiento contra el catálogo Shazam **o contra tu propio `SHCustomCatalog`**; escritura en la biblioteca Shazam del usuario | con bg de audio | media | `com.apple.developer.shazamkit` — servicio en el portal (autoservicio, pero paso real de aprovisionamiento) | metadatos según storefront | bajo | Alta |
| **Music Understanding** ⚡⚡ **(iOS 27, nuevo)** | Análisis on-device de cualquier `AVAsset` o stream de PCM: **Rhythm** (beats, compases, BPM), **Key** (tónica y modo **a lo largo del tiempo**), **Loudness** (ITU-R BS.1770), **Pace**, **Structure** (secciones, segmentos, frases), **Instrument Activity** (qué instrumento, cuándo, con qué intensidad) | no documentado | **ninguna para entrada de fichero** | ninguno encontrado | todas las plataformas, **incluido watchOS 27** | bajo | **Alta** |

### 2.4 Inteligencia local

**Foundation Models** — el resumen honesto:

| | iOS 26 | iOS 27 |
|---|---|---|
| Modelo on-device | ≈3 B parámetros, QAT de 2 bits | **AFM 3 Core** (3 B denso) y **AFM 3 Core Advanced** (20 B disperso, **requiere ≥12 GB de memoria unificada**, en la práctica iPhone 17 Pro / Air) |
| Ventana de contexto | **4096 tokens** — instrucciones + prompt + definiciones de tools + esquemas `@Generable` + toda la respuesta | 4 K on-device; **32 K vía Private Cloud Compute** |
| Multimodal | no | **sí, imagen + texto** (`Attachment(cgImage)`), más `Vision.OCRTool` y `Vision.BarcodeReaderTool` como tools |
| Modelo en servidor para terceros | no | **Private Cloud Compute**, un cambio de una línea |
| Modelos propios/OSS | no | **Core AI**: exporta un modelo OSS a `.aimodel` y cárgalo con `CoreAILanguageModel` — **la vía de escape al requisito de Apple Intelligence** |
| Razonamiento | ninguno | solo en PCC (`.light`/`.moderate`/`.deep`) |

Lo que **no** hace bien, con evidencia: el conocimiento del mundo es fino y caducado (pruebas independientes sitúan el corte de entrenamiento alrededor de octubre de 2023; no sabe con fiabilidad la fecha de hoy); no hay búsqueda web, ni ejecución de código, ni autocorrección agéntica; el razonamiento multi-paso y la aritmética son poco fiables. **El encuadre correcto es: motor de transformación de texto (resumir, extraer, clasificar, etiquetar, reescribir, generar estructura), no motor de conocimiento.** Todos los ejemplos públicos de apps que lo han enviado en 2025-26 encajan con eso: MoneyCoach (sugerencia de categoría), Tasks (etiquetas), Day One (títulos), Crouton (etiquetado de recetas), SmartGym (descripción → rutina estructurada), LookUp (frases de ejemplo).

Tres límites operativos que condicionan el diseño:

- **Desbordamiento de contexto**: al pasar de 4096 tokens lanza `contextSizeExceeded` y **la sesión deja de responder permanentemente**; hay que crear una nueva. En CJK y vietnamita la relación es de ~1 carácter por token, es decir se agota **3–4× antes** que en alfabeto latino.
- **Rate limiting en segundo plano**: la documentación de Apple es explícita — *"este error solo ocurrirá si tu app se ejecuta en segundo plano y supera el límite de tasa definido por el sistema"*. Un ingeniero de Apple añadió en los foros que aplica con el dispositivo a batería y el proceso en background, y que `streamResponse()` consume más y llega antes al límite que `respond()`. Un desarrollador de extensión de Safari lo alcanzó tras **4 peticiones a intervalos de 30 segundos**. **Las extensiones cuentan como background.** Conclusión de producto: **no diseñes nada cuyo bucle principal sea procesamiento de IA por lotes en segundo plano.**
- **Requisito de dispositivo**: solo dispositivos con Apple Intelligence (iPhone 16 en adelante, iPhone 15 Pro/Pro Max, iPads y Macs M1+). Todo lo anterior a 15 Pro no recibe nada. Toda función basada en Foundation Models necesita una ruta alternativa.

**Private Cloud Compute (iOS 27) merece un párrafo propio porque está explícitamente diseñado a favor de los indies.** Elegibilidad: estar inscrito en el **App Store Small Business Program**, tener **menos de 2 millones de descargas de primera vez** en todas tus apps, y el entitlement gestionado `com.apple.developer.private-cloud-compute` (formulario de solicitud). **Sin coste de API, sin claves, sin servidor.** El coste se traslada al usuario: cada persona tiene una cuota diaria que amplía **suscribiéndose a iCloud+**, y tu app debe mostrar el estado con `model.quotaUsage`. Riesgo de producto evidente: construyes una función cuyo techo de uso lo fija Apple y cuya monetización va a la suscripción de Apple, no a la tuya.

### 2.5 Contexto del sistema y superficies

| Superficie | Capacidad | Mecanismo de actualización | Entitlement | Notas duras |
|---|---|---|---|---|
| **WidgetKit** | Inicio, Bloqueo, StandBy, Smart Stack del Watch; configuración por App Intent; widgets interactivos desde iOS 17 | timelines con presupuesto, **+ push de widget** (`WidgetPushHandler`, capability de Push en la extensión; `apns-push-type: widgets`) | ninguno | Los push broadcast **no** están soportados |
| **ActivityKit / Live Activities** | Pantalla de bloqueo, Dynamic Island, banner de inicio, **Smart Stack del Watch, barra de menús de Mac, pantalla de inicio de CarPlay** | local o vía APNs; no se puede iniciar desde background salvo con un `LiveActivityIntent` | `NSSupportsLiveActivities` | **8 h activa, 12 h máximo absoluto. Payload ≤ 4 KB. No tiene acceso a red ni recibe ubicación.** Es un destino de render, no un canal de datos |
| **App Intents** | Siri, Spotlight, Atajos, botón de Acción, Centro de Control; App Shortcuts; **snippets interactivos** | iOS 27 `LongRunningIntent` rompe el techo de 30 s | ninguno | Mientras un snippet es visible, **el sistema mantiene tu app viva en segundo plano con todo en memoria** |
| **Visual Intelligence** ⚡ (iOS 26) | Tu contenido aparece como resultado al apuntar la cámara al mundo o al buscar dentro de una captura, vía `SemanticContentDescriptor` + `IntentValueQuery` | — | ninguno documentado | **Superficie de descubrimiento completamente nueva y casi inexplotada** |
| **Core Spotlight** | `CSSearchableItem`; `IndexedEntity` puentea entidades de App Intents; **iOS 27: los esquemas de entidad alimentan el índice semántico y `SpotlightSearchTool` permite que un `LanguageModelSession` busque en Spotlight como herramienta** | — | ninguno | — |
| **UserNotifications** | Locales y remotas; triggers de tiempo, calendario y **ubicación**; extensión de servicio; **autorización `provisional` = sin prompt** | — | Critical Alerts = **solicitud a Apple**, poco probable para un indie | — |
| **BackgroundTasks** | `BGAppRefreshTask` (segundos, oportunista), `BGProcessingTask` (minutos, cargando e inactivo), **`BGContinuedProcessingTask` (iOS 26)** | — | GPU requiere `...continued-processing.gpu`; **iOS 27 restringe también el Neural Engine** con `...continued-processing.inference` | `BGContinuedProcessingTask`: **iniciado por el usuario**, progreso mostrado en una Live Activity del sistema que el usuario puede cancelar, `ProgressReporting` obligatorio, **muere en silencio si el usuario descarta la app** |
| **Control Center (`ControlWidget`)** (iOS 18) | Botones y toggles colocables en Centro de Control, pantalla de bloqueo y **botón de Acción** | interacción, recarga o **APNs** | ninguno | — |

### 2.6 Advertencia verificada sobre MusicKit y Music Understanding

**El audio del catálogo de Apple Music está protegido por DRM y no se puede obtener como PCM.** En los foros de desarrolladores de Apple: *"según mi experiencia con MusicKit, no hay forma de obtener audio en bruto porque Apple Music aparentemente usa DRM"*, y el FAQ de la Apple Music API afirma explícitamente **"no hay soporte actualmente para apps de estilo DJ"**. Consecuencia directa: **Music Understanding es utilizable sobre ficheros propios del usuario, grabaciones y entrada de micrófono, no sobre canciones en streaming.** Cualquier candidato de la sección 5 que dependa de análisis musical está diseñado bajo esa restricción. Lo mismo vale para Spotify, que cerró su API de reproducción a terceros en 2022.

---

## 3. Particularly interesting or underused capabilities

Ordenadas por "esto era difícil o imposible hace dos o tres años, y casi nadie lo ha usado todavía".

**1. `SpeechAnalyzer` / `SpeechTranscriber` (iOS 26).** La primera API de Apple diseñada para transcripción **larga** on-device, con streaming de resultados volátiles y sesgo de vocabulario. `SFSpeechRecognizer` nunca fue viable para audio de una hora. Esto convierte "transcribe esta reunión de 90 minutos sin subirla a ningún sitio" en un problema de tarde de trabajo, y lo hace exactamente en el momento en que todo competidor cobra suscripción porque procesa en servidor. **Es la palanca más infravalorada del ecosistema ahora mismo.**

**2. Music Understanding (iOS 27).** Rejilla de beats, tonalidad variable en el tiempo, **estructura de canción** y **actividad por instrumento**, gratis, on-device, offline, y disponible incluso en watchOS. La disposición a pagar ya está demostrada (Mixed In Key, Moises, Anytune, Capo, Soundslice, Transcribe!) y la debilidad de los titulares está documentada desde 2017 hasta 2026. Lo verdaderamente nuevo no es BPM ni tonalidad (eso existía): es **estructura + instrumentos**, que permite "repite el segundo estribillo" o "aísla dónde está el solo" sin que el usuario arrastre marcadores.

**3. `BGContinuedProcessingTask` (iOS 26).** La primera primitiva de propósito general de "termina este trabajo largo después de que el usuario se vaya", con acceso a GPU vía entitlement y una Live Activity del sistema que muestra el progreso. Exportación de vídeo, ML por lotes y pipelines de medios pasan a ser viables dentro de una app. Apple menciona Vision explícitamente como caso de uso.

**4. `Vision.RecognizeDocumentsRequest` (iOS 26).** Comprensión estructurada de documentos — párrafos, **tablas**, listas, códigos — no solo líneas de OCR. Combinada con Foundation Models para extracción de campos, cubre el 90 % de los productos de "fotografía esto y conviértelo en un registro" sin nube.

**5. Visual Intelligence como canal de distribución (iOS 26).** El contenido de una app de terceros puede aparecer como resultado de apuntar la cámara al mundo o de buscar dentro de una captura. Para un indie cuyo mayor problema es la distribución, **una superficie de descubrimiento nueva y vacía es más valiosa que una API de datos nueva**. Nadie la está usando.

**6. Snippets interactivos de App Intents (iOS 26).** Interacción multi-paso desde Spotlight, el botón de Acción o Siri, **con el sistema manteniendo tu app viva en memoria mientras el snippet es visible**. Permite productos cuya superficie principal no es una app que se abre.

**7. AccessorySetupKit (iOS 18) y Channel Sounding (iOS 27).** El primero elimina por completo la alerta de permiso de Bluetooth. El segundo da **distancia con precisión métrica a cualquier periférico BLE 6.3** sin hardware UWB — pero requiere iPhone 17 o posterior, lo que lo convierte en apuesta de 2027.

**8. `ContactAccessButton` y acceso limitado a Contactos (iOS 18).** Obtener contactos concretos **sin ninguna alerta de permiso**. Elimina la fricción más odiada de cualquier app que toque la agenda.

**9. `FamilyActivityData` (iOS 26.4) — pero solo en la UE.** Expone **identificadores de bundle reales, dominios reales y categorías reales**, con entitlement de **autoservicio en Xcode**. Es claramente una concesión de interoperabilidad de la DMA: *"las instalaciones de clientes solo pueden usar esta clase en dispositivos ubicados en la UE con una cuenta Apple de un país de la UE"*. Ver wildcard 2.

**Capacidades sobre las que concluí que no hay oportunidad interesante para este fundador**, y lo digo explícitamente porque lo pediste: **HomeKit/Matter** (la fiabilidad es el problema y no la puedes arreglar desde una app; lo único construible es observabilidad, y el mercado que la pagaría ya está en Home Assistant); **Nearby Interaction/UWB** (sin un accesorio propio, el caso de uso entre iPhones no resuelve ningún trabajo recurrente que encontrara con evidencia); **ShazamKit con catálogo propio** (técnicamente precioso, no encontré ningún job recurrente que lo justifique fuera de instalaciones y museos, que es un negocio de venta B2B); **Journaling Suggestions** (el usuario debe elegir en el picker cada vez, lo que rompe el principio de "cero data entry" — sirve como acelerador de captura, no como base de producto); y **PassKit** (crear pases es trivial pero solo tiene valor si ya eres el emisor del billete o la tarjeta).

---

## 4. Problems and signals found in the wild

Solo señales con fuente. Clasificadas por fuerza de evidencia.

### 4.1 "Mis datos están dentro pero no puedo sacarlos en forma útil" — FUERTE

- La exportación de Salud es un XML gigante: *"la exportación integrada de Apple da un blob XML gigante que atraganta a la mayoría de herramientas, si es que consigues exportarlo"* (Hacker News, 11 mar 2026). Típicamente **800 MB – 2 GB**.
- **Al menos 15 repos de GitHub** existen solo para parsear esa exportación: `k0rventen/apple-health-grafana` (583 ★), `neiltron/apple-health-mcp` (568 ★), `krumjahn/applehealth` (457 ★), `dogsheep/healthkit-to-sqlite` (250 ★), `jameno/Simple-Apple-Health-XML-to-CSV` (196 ★).
- **El caso más elocuente**: un usuario de MacRumors (9 ago 2024) quería llevar tensión arterial, pulso y peso a su médico; probó la exportación XML, Withings Health Mate y Atajos (un moderador le avisó de timeouts con conjuntos grandes). **Resolución final: hizo capturas de pantalla de sus lecturas y las imprimió.**
- Siete o más hilos distintos en Apple Support sobre el mismo problema de exportación; hilos duplicados en MacRumors desde 2019.
- Hoja de cálculo en libertad: en MacPowerUsers Talk (29 oct 2024), *"quiero acceder a estos datos en Google Sheets con la menor interacción manual posible"*, y tras ser dirigido a Health Auto Export: *"parece que necesitará bastante configuración; esto es complicado"*. Otro participante admitió hacer **copiar y pegar manual**.

### 4.2 "Apple calcula el número mal y no me enseña el correcto" — MEDIA-FUERTE

- Dr. Drang (1 nov 2024) documenta que las Tendencias de Salud **no ajustan una recta a los datos, ajustan una función escalón**; que Salud considera tendencia una variación de 6000 pasos y descarta una de 10 lpm en recuperación cardíaca; y que **Salud y Fitness definen la semana de forma distinta** (dom-sáb frente a lun-dom). Su solución fue rehacerlo con mínimos cuadrados en Wolfram.
- Proyecto en Hacker News (29 ago 2025, 22 puntos): *"Apple Health te miente sobre tu media de sueño de seis meses"*.
- Pasos duplicados entre iPhone y Watch: hilos en MacRumors, en Apple Support y hasta en **Apple Developer Forums** (`thread/759709`, "Step Data Duplication Issue").

### 4.3 Atletas serios que se van a Garmin — FUERTE, con recuento de votos

- **TrainingPeaks UserVoice: "Support Metrics from Apple Health" — 243 votos.** Abierto en agosto de 2022, marcado "Planned" en 2024, "Started" en nov 2024, y con comentarios de 2025-2026 quejándose de que sigue sin avanzar. El solicitante original usa HealthFit como parche pero *"los datos no se agregan a una métrica diaria por día"*.
- Foro de Intervals.icu (7 ene 2022, más de 20 respuestas): el consenso es pagar **HealthFit**; un usuario objeta *"no quiero pagar otra app"*.
- **Navegación GPX en el Watch**: un ultrafondista en Apple Support explica que compró un Ultra por la batería, que los recorridos vienen en GPX y que *"no entiendo cómo un reloj diseñado para ultra no soporta probablemente la función más importante y básica del ultrafondo"*. El hilo de **WorkOutDoors en MacRumors va por la página 206+** — que una sola app de un desarrollador solitario sostenga un hilo de más de 200 páginas es una señal de demanda inusualmente fuerte.
- **Natación en aguas abiertas**: un nadador de maratón (MacRumors, jul-sep 2023) documenta un nado de 7 km registrado como 8,5 km, con *"bucles y giros aleatorios aunque no me detengo y nado en línea recta"*, **más del 50 % de las sesiones mal**, en **tres unidades Ultra distintas** y varias versiones de watchOS. Se pasó a Garmin.
- **Natación en piscina**: hilo abierto en feb 2025 con respuestas hasta **mayo de 2026** documentando que las distancias por brazada son correctas pero **el total sale 200 m corto**, y que el ritmo de las series automáticas contradice al ritmo global.

### 4.4 "Hoja de cálculo en libertad" en nichos apasionados — FUERTE

Es la señal de JTBD más fiable de toda la investigación.

- **Acuarios de arrecife.** Hilo literalmente titulado **"¿Qué usáis realmente para registrar vuestros parámetros de agua? Me sorprende lo malas que son las opciones"** (Reef2Reef, 23 feb 2026, **cuatro páginas**). El autor, con un acuario de 280 litros, desmonta las tres apps que probó: *"Aquarimate: pagué 10 $, la interfaz parecía diseñada en 2012, no conseguí borrar una entrada errónea"*; *"AquaticLog: bien, pero ¿necesitas el plan pro de 25 $/año solo para tener recordatorios? ¿Para recordatorios?"*; *"Aquarium Note: decente pero solo Android"*. Hay además múltiples plantillas de Excel compartidas por la comunidad.
- **Astrofotografía.** En Cloudy Nights (27 mar 2026), un usuario mantiene **más de 560 filas en unas 280 noches con "algo así como 40 columnas de datos"** en una hoja de cálculo, y su dolor principal es *"tengo problemas para saber cuándo fotografié un objetivo concreto anteriormente"*.
- **Apicultura, masa madre, cerveza casera, carpintería**: cuadernos de papel vendidos en Amazon, plantillas imprimibles gratuitas y hilos recurrentes de "¿cómo lleváis el registro?". **Donde un cuaderno de papel tiene mercado, una buena app tiene mercado.**

### 4.5 Conteo con dinero en juego — FUERTE

- **Schengen y residencia fiscal.** Quince o más repos de "calculadora Schengen" en GitHub, **nueve de ellos actualizados en 2026**. Cuatro o más apps comerciales de iOS lanzadas en 2026 (Nomad Tracker, Flamingo Compliance, Travel Days Tracker). Comentario en HN (4 nov 2025) sobre construirse uno propio para *"ventana móvil 90/180 de Schengen más residencia fiscal en un par de países"*.
- **Coste de carga del coche eléctrico en casa**, columna editorial de Electrek (22 mar 2026): *"estás intentando separar lo que cuesta cargar el coche de lo que cuesta tener las luces encendidas, y tu compañía eléctrica no lo pone nada fácil"*. Cinco o más apps recientes en la tienda.

### 4.6 La cámara es el dispositivo de captura, pero nada recoge lo capturado — FUERTE como fricción, DÉBIL como negocio

- *"Básicamente has convertido tu carrete en una lista de tareas sin tareas"* … *"Tus capturas no son aleatorias. Son **decisiones sin terminar**"* (TechTiff, 2 ene 2026). Múltiples ensayos en primera persona en Substack y Medium.
- Pero: **15 repos de GitHub creados en 2026 para organizar capturas, todos con 0–5 estrellas**, y la app líder de App Store con **1,0 estrellas**. Altísima comezón de constructor, cero tracción. La lectura correcta es que la gente quiere que esto sea invisible o nativo, no otra app que abrir — y Apple ya ocupa el punto de entrada con Visual Intelligence.

### 4.7 Muros de plataforma que matan ideas — FUERTE, y son la lista de exclusión

- **Los tipos de medicación de HealthKit son de solo lectura** para terceros; lo confirma Apple Worldwide Developer Relations en `developer.apple.com/forums/thread/803954`. Puedes leer el registro de medicación de Apple; **no puedes contribuir a él**. Eso explica por qué hay decenas de apps de pastillas que viven completamente fuera de Salud.
- **Health Records (FHIR: analíticas, diagnósticos, vacunas, alergias) no está expuesto a desarrolladores.** Hilo "Health Records – API Where Art Thou?" con múltiples "me too" y sin resolución.
- **Una app no puede editar ni borrar muestras escritas por otra fuente**, incluidos los entrenamientos del Watch de Apple.
- **No hay API para leer notificaciones de otras apps.** Apple, en los foros: *"en general, no hay API pública para descubrir nada sobre otras apps instaladas en el dispositivo. Sería un gran fallo de privacidad"*. **Cualquier idea con forma de "agrega, tría o resume todas tus notificaciones" es inconstruible en iOS.**
- **La extensión de DeviceActivityReport es un agujero negro**: entran datos, no sale nada. Sin red, sin notificaciones Darwin, sin escritura al App Group. Solo puede renderizar una vista SwiftUI. **No puedes leer los minutos de uso del usuario dentro de tu propia app.**
- **Los `ApplicationToken` de Family Controls son opacos**: `bundleIdentifier` y `localizedDisplayName` devuelven `nil` por diseño, incluso con autorización `.individual`. No puedes saber qué app eligió el usuario (salvo en la UE desde iOS 26.4).
- **Fiabilidad de NFC**: *"normalmente me hacen falta **2 o 3 intentos** para que una etiqueta NFC registre en mi iPhone 15 … de las 8 que probé, todas me dan problemas"* (Home Assistant Community, 12 ene 2025, con cinco hilos hermanos). No es arreglable desde software.

### 4.8 Accesibilidad: hueco de ejecución, no de API — MEDIA

En AppleVis, un usuario ciego pide una app de registro de entrenamiento donde se puedan editar repeticiones, series y pesos porque *"la mayoría carecen de soporte adecuado de VoiceOver para ajustar parámetros"*. La única respuesta: usa la app Salud de Apple, *"la encuentro muy accesible con VoiceOver; incluso hay gráficos de audio"*. La pregunta se repite en varios hilos a lo largo de los años. **La API de Audio Graphs de Apple es pública y casi nadie la usa.**

### 4.9 Cuidado a distancia con forma de hoja de cálculo — MEDIA

En AgingCare (ene 2024), cuidadores describen llevar la vida de sus padres en **una hoja de Excel** con nombres de cuentas, teléfonos y contraseñas; en Family Wall a 45 $/año; en recordatorios de Alexa; y en **PDFs descargables comprados en Etsy**. Un participante responde sin más: **"¡¡¡No hay ninguna!!!"**. Siete hilos distintos en Apple Support sobre monitorizar a un mayor, incluido *"Apple Health Data Sharing Delayed"*. Dato relevante: **la detección de caídas no avisa al familiar con quien compartes datos**, solo a contactos de emergencia y servicios.

---

## 5. Fifteen candidate opportunities

Formato fijo por candidato. "Evidencia" distingue explícitamente lo observado de lo inferido.

---

### Candidate 1 — Informe de salud listo para la consulta médica

**Usuario.** Personas con una condición que siguen en casa (tensión, peso, glucosa introducida a mano, ritmo cardíaco) y que van al médico cada pocos meses. Y sus cuidadores.

**Problema.** No hay forma razonable de llevarle al médico "estas cuatro métricas, de estas fechas, en una hoja".

**Current workaround.** Exportación XML de 800 MB–2 GB que no abre en Excel; Atajos que dan timeout; y, documentado literalmente, **capturas de pantalla impresas**.

**Evidencia.** Hilo de MacRumors del 9 ago 2024 cuya resolución fue imprimir capturas (https://forums.macrumors.com/threads/apple-health-print-spreadsheet.2433283/); siete o más hilos duplicados en Apple Support; hilo de 2019 con 10 respuestas (https://forums.macrumors.com/threads/how-can-i-get-health-data-from-apple-watch-for-doctor.2182240/). **Evidencia, no inferencia.**

**Native Apple leverage.** `HealthKit` + `PDFKit` + Swift Charts. Todo local. Opcionalmente `Vision` para incorporar una foto de un aparato de tensión.

**What already exists.** *Heart Reports* (4,4 con **412 valoraciones**, 3,99 $ de desbloqueo, **última actualización feb 2023 — abandonada hace tres años y medio**). *Simple Health Export CSV* (4,1, 31 valoraciones, **abandonada desde oct 2022**). *vitalina* (4,8, 24 valoraciones, 4,99 $ vitalicio, lanzada mar 2026, se actualiza a diario). *Health Auto Export* (4,3, 395 valoraciones, hasta 24,99 $ vitalicio) y *HealthFit* (4,6, 901 valoraciones, 6,99 $ de pago único) son excelentes pero están orientadas a CSV/atletas, no a la consulta médica. *QS Access* lleva muerta desde iOS 13.

**Why Apple doesn't already solve it.** La exportación de Salud lleva **once años** siendo un volcado XML. La reescritura de septiembre de 2026 añadió Insights, Longevity y Health Age, y **no tocó la exportación**. Once años de indiferencia es una señal fiable de prioridad.

**Why an indie could compete.** El titular natural del nicho está muerto desde 2023 y sigue acumulando valoraciones. Las quejas de 1-3 estrellas del líder actual son una especificación de producto gratuita: marcas de tiempo de tensión exportadas como `00:00:00`, una fila por minuto aunque no haya dato, categorías no marcadas que generan ficheros igualmente, sueño solo en horas sin opción de minutos, y un nivel gratuito que no exporta nada en una app llamada "Export".

**Data entry burden.** Nulo.

**Time-to-value.** Inmediato: primer PDF en la primera sesión.

**Backend requirement.** Ninguno.

**Third-party dependency.** Baja (ninguna).

**Monetization hypothesis.** Pago único o desbloqueo vitalicio. El mercado ya fijó el techo: **5–25 $**. Comparables que cobran: HealthFit 6,99 $ con 901 valoraciones (#5 de pago en Salud y Forma Física), Heart Reports 3,99 $, vitalina 4,99 $, Health Auto Export 24,99 $ vitalicio.

**MVP.**
1. Selector de métricas y rango de fechas sobre HealthKit.
2. Detección y manejo correcto de la **autorización de histórico limitado de iOS 27**.
3. PDF de una o dos páginas: tabla + gráfico por métrica, con unidades, fuente del dato y notas de calidad.
4. Exportación CSV correcta (sin filas fantasma, marcas de tiempo reales).
5. Compartir a Mail, Archivos e Imprimir.

**Solo-developer feasibility.** Alta.
**Estimated MVP scope.** Pequeño.
**Would I personally understand this product?** **Alta.** El usuario es cualquiera, el flujo es transparente y la calidad se juzga mirando el PDF.

---

### Candidate 2 — Auditor de datos de Salud: duplicados, fuentes y medias correctas

**Usuario.** Gente que mira sus números de Salud y ve algo que no cuadra: pasos duplicados, un entrenamiento contado dos veces, una media que no coincide con los datos.

**Problema.** Salud mezcla fuentes y calcula agregados de forma opaca, y el usuario no tiene forma de auditar qué dato viene de dónde ni de corregir las duplicidades.

**Current workaround.** Borrar muestras a mano una a una en Salud; usar Pedometer+ para fusionar fuentes de pasos; recalcular en una hoja.

**Evidencia.** Análisis de Dr. Drang sobre las Tendencias como función escalón (https://leancrew.com/all-this/2024/11/apple-health-trends/); proyecto `reschandreas/saverage` en HN (22 puntos, 29 ago 2025); hilos de pasos duplicados en MacRumors (https://forums.macrumors.com/threads/does-health-app-duplicate-the-step-count-of-aw-and-phone-in-some-instances.2338067/) y en Apple Developer Forums (`thread/759709`); cinco o más hilos de Apple Support sobre medias mal calculadas.

**Native Apple leverage.** `HealthKit` (prioridad de fuentes, `HKSourceQuery`, muestras crudas) + Swift Charts + `WidgetKit`.

**What already exists.** *Health Stats* (4,1 con 1600 valoraciones — la peor satisfacción del grupo), *Pedometer++* (4,8, 182 000 valoraciones, David Smith), *Training Today* (4,6, 2600), *Bevel* (4,8, 16 000, **99,99 $/año**), *Gentler Streak* (4,7, 8800), *Athlytic*. *Cardiogram*, la original de YC, **está muerta**: lo que hay hoy en la tienda con ese nombre es un homónimo con 3,5 estrellas y 12 valoraciones.

**Why Apple doesn't already solve it.** No lo resuelve porque no considera que sea un problema: la app Salud está diseñada para mostrar, no para auditar. Pero **acaba de reescribirla**.

**Why an indie could compete.** Podría, sobre el papel: "enséñame de dónde sale cada número" es un job concreto que ninguno de los grandes hace. **Pero ver "Main risk".**

**Data entry burden.** Nulo. **Time-to-value.** Inmediato. **Backend.** Ninguno. **Third-party dependency.** Baja.

**Monetization hypothesis.** Desbloqueo único 9,99–19,99 $. El espacio demuestra dinero a lo grande (Bevel a 99,99 $/año con 16 000 valoraciones).

**MVP.** (1) Vista por fuente de cada tipo de dato; (2) detector de solapes y duplicados con explicación; (3) medias y tendencias calculadas correctamente, con el método a la vista; (4) exportación del informe de auditoría; (5) widget con la métrica corregida.

**Solo-developer feasibility.** Alta. **Estimated MVP scope.** Pequeño-medio. **Would I personally understand this product?** Alta.

**Main risk (adelantado aquí porque es descalificante).** Apple reescribió la app Salud **en septiembre de 2026** con Insights, Longevity y Health Age, y hay un agente de IA de salud y un posible nivel "Health+" en camino. Entrar aquí es apostar contra la hoja de ruta del dueño de la plataforma con un anuncio de hace tres días. **Lo incluyo entre los 15 por completitud y lo descarto en la sección 7.**

---

### Candidate 3 — Contador automático de días por jurisdicción (Schengen 90/180 + residencia fiscal)

**Usuario.** Nómadas, jubilados con segunda residencia, trabajadores remotos transfronterizos, personas con obligaciones fiscales en dos o más países, y titulares de visados con límites de presencia.

**Problema.** "¿Cuántos días he estado realmente en cada país, y cuántos me quedan antes de meterme en un problema?"

**Current workaround.** La calculadora web oficial de la Comisión Europea (sin almacenamiento, sin planificación), hojas de cálculo, sellos de pasaporte y memoria.

**Evidencia.** **Quince o más repos de "calculadora Schengen" en GitHub, nueve actualizados en 2026** (https://api.github.com/search/repositories?q=schengen+calculator&sort=stars). Cuatro o más apps comerciales lanzadas en 2026. Comentario en HN (4 nov 2025) de alguien construyéndose el suyo para *"ventana móvil 90/180 más residencia fiscal en un par de países"*. El titular, **Schengen Simple**, tiene **4,8 con 2500 valoraciones** con un modelo de **pago único de 7,99–14,99 £**.

**Native Apple leverage.** `CoreLocation` (`CLMonitor`, cambios significativos de ubicación, `startMonitoringVisits`) + `EventKit` (viajes ya en el calendario) + `WidgetKit` + `ActivityKit` para la cuenta atrás durante un viaje + App Intents/Siri ("¿cuántos días Schengen me quedan?"). **Esta es la razón por la que tiene sentido como producto Apple-native: el teléfono ya sabe la respuesta y la competencia hace que el usuario teclee las fechas.**

**What already exists.** *Schengen Simple* (4,8 / 2500, 7,99–14,99 £ de pago único, modo "Control de pasaportes", sincronización iPhone/iPad/Mac con una sola compra, soporte que responde en horas, **y en su ficha de App Store no aparece ni una sola reseña de 1-3 estrellas**). *Nomad Tracker* (lanzada feb 2026, 3,99 £/mes hasta **129,99 £ vitalicio**, sin valoraciones suficientes). *Flamingo Compliance* (posicionada en residencia fiscal, precios no publicados). *90 Days in Europe* (9,99–14,99 $/año). *Days Monitor* (7,99 £/año).

**Why Apple doesn't already solve it.** Nunca lo hará. No es una función de sistema operativo.

**Why an indie could compete.** **No en Schengen — está resuelto y querido.** El hueco está al lado: **el test de residencia fiscal multi-jurisdicción** (Statutory Residence Test británico, substantial presence test estadounidense, reglas de 183 días en varios países a la vez, reglas estatales de EE. UU.) **con evidencia auditable en PDF**. Mayor consecuencia económica, sin marca dominante, y soporta un precio 5–10× superior: Nomad Tracker ya está probando 129,99 £ vitalicio.

**Data entry burden.** Bajo, y es precisamente el eje competitivo: la versión automática por ubicación es estrictamente mejor que la versión que se teclea.

**Time-to-value.** Primer día (con importación de viajes desde el calendario, inmediato).

**Backend requirement.** Ninguno (iCloud/CloudKit para sincronizar).

**Third-party dependency.** Baja (ninguna).

**Monetization hypothesis.** Pago por adelantado o **muro de pago duro**, 19,99–49,99 € según alcance, con nivel vitalicio superior para el módulo fiscal. El perfil de compra es exactamente el que RevenueCat documenta como mejor convertidor: una compra motivada por miedo a una sanción (multas de 500 $–3000 € y prohibiciones de entrada), con conversión mediana del 10,7 % a día 35 frente al 2,1 % del freemium.

**MVP.**
1. Registro automático de país por día usando `CLMonitor` y visitas, con corrección manual fácil.
2. Motor de reglas para Schengen 90/180 **y** el conteo de días de una o dos jurisdicciones fiscales.
3. Planificador: "si viajo estas fechas, ¿qué pasa?".
4. Exportación PDF con la evidencia día a día.
5. Widget y Live Activity con "días restantes".

**Solo-developer feasibility.** Alta técnicamente. **Media** en la parte de reglas: no requiere ser asesor fiscal, pero sí leer bien la normativa de cada jurisdicción y ser muy explícito sobre que no es asesoramiento legal.

**Estimated MVP scope.** Medio.

**Would I personally understand this product?** **Alta para Schengen, media para fiscal.** La lógica es un problema de fechas y de reglas escritas, no de intuición sectorial; un ingeniero puede leer la regla y verificar el cálculo. Es exactamente el tipo de dominio que un desarrollador puede auditar por sí mismo.

---

### Candidate 4 — Navegación GPX en el Apple Watch que sí cierra los anillos

**Usuario.** Ultrafondistas, senderistas y ciclistas que compraron un Apple Watch Ultra y descubrieron que no sigue recorridos.

**Problema.** La app Entreno nativa no sigue un GPX; la mejor alternativa de terceros no escribe en la app Entreno, así que tus anillos no se cierran.

**Current workaround.** WorkOutDoors, más un GPX creado en otro sitio, más aceptar que la actividad no cuenta para los anillos.

**Evidencia.** Hilo de Apple Support de un ultrafondista: *"no entiendo cómo un reloj diseñado para ultra no soporta la función más importante y básica del ultrafondo"*. **El hilo de WorkOutDoors en MacRumors va por la página 206+** (https://forums.macrumors.com/threads/workoutdoors-new-workout-features.2134687/page-206). Quejas de 1-3 estrellas de WorkOutDoors: consumo de batería (*"después de una carrera de 3 horas, la batería estaba al 30 %"* en un Watch SE), **no alimenta la app Entreno nativa, así que los anillos no se cierran**, y no permite crear rutas dentro de la app.

**Native Apple leverage.** `HKWorkoutSession` (la mejor concesión de background de watchOS), `HKWorkoutRoute`, MapKit en watchOS, `CoreLocation`, `WKExtendedRuntimeSession`.

**What already exists.** *WorkOutDoors* (4,7 / **1700 valoraciones**, **8,99 $ de pago único sin suscripción**, un desarrollador solo, el caso canónico de éxito indie en watchOS). *Footpath* (4,8 / **22 000 valoraciones**, 3,99 $/mes o 23,49 $/año). *WristTopo* (4,8 / 66, 9,99 $ Pro o 29,99 $ vitalicio). *Gaia GPS* (39,99 $/año, Outside Inc.). *Komoot* (ahora de Bending Spoons, empujando suscripción). *Pedometer++* añadió mapas completos en el Watch en 2026.

**Why Apple doesn't already solve it.** Apple no ha enviado seguimiento de GPX en la app Entreno. Strava lanzó navegación de rutas en el Watch en enero de 2026 **sin indicaciones giro a giro, con vibración de cruce "extremadamente débil", sin audio, sin recálculo y con renderizado lento**.

**Why an indie could compete.** Solo atacando la lista de quejas, no la categoría.

**Data entry burden.** Bajo. **Time-to-value.** Primer día. **Backend.** Ninguno. **Third-party dependency.** Baja.

**Monetization hypothesis.** Pago único 8,99–14,99 $. Dinero demostrado: Footpath con 22 000 valoraciones a 23,49 $/año, WorkOutDoors con 1700 a 8,99 $.

**MVP.** (1) Importar GPX; (2) seguir el recorrido en el Watch con avisos de desvío; (3) **escribir el entrenamiento en HealthKit para que cuenten los anillos**; (4) perfil de batería agresivamente eficiente y medido; (5) dibujo de ruta básico en el iPhone.

**Solo-developer feasibility.** **Baja-media.** David Smith dedicó **seis años** a construir el motor de mapas de Pedometer++ (renderizador SwiftUI propio, un cartógrafo contratado, varias reescrituras). Alcanzar la paridad de calidad de mapa es un proyecto de años, no de meses.

**Estimated MVP scope.** Grande.
**Would I personally understand this product?** Alta si eres corredor o senderista; media si no. Evaluar la calidad exige salir al campo.

---

### Candidate 5 — Corrección posterior de tracks de natación en aguas abiertas

**Usuario.** Nadadores de aguas abiertas y triatletas con Apple Watch.

**Problema.** El GPS de muñeca en natación produce tracks con bucles y giros inventados, y por tanto distancias y ritmos falsos.

**Current workaround.** Aceptar el dato malo, recortar a mano en otra app, o cambiarse a Garmin.

**Evidencia.** Nadador de maratón en MacRumors (jul-sep 2023): 7 km registrados como 8,5 km, *"bucles y giros aleatorios aunque no me detengo y nado en línea recta"*, **más del 50 % de las sesiones erróneas en tres unidades Ultra distintas**; Apple Turquía respondió "no reproducible"; se pasó a Garmin. Otros usuarios en el mismo hilo reportan lo mismo desde watchOS 9.5.2. **Ninguna app conocida hace esta corrección.** (https://forums.macrumors.com/threads/apple-watch-ultra-open-water-swim-wrong-distance-faulty-gps-track.2395116/)

**Native Apple leverage.** `HealthKit` (`HKWorkoutRoute` con las localizaciones crudas y su precisión horizontal) + `CoreMotion`/cadencia de brazada del entreno + suavizado y reestimación de distancia + `MapKit` para visualizar antes/después. Escritura de una versión corregida como entrenamiento propio (no se puede editar la muestra original de Apple — ver la restricción en 10).

**What already exists.** No encontré ninguna app que haga exactamente esto. *HealthFit* y *RunGap* exportan; no corrigen. Las herramientas de suavizado que existen son de escritorio y para ciclismo.

**Why Apple doesn't already solve it.** Porque el problema es la calidad de la señal bajo el agua, que Apple no puede resolver en hardware a corto plazo, y admitir el fallo con una corrección post hoc no es una jugada que Apple haga.

**Why an indie could compete.** Nicho demasiado pequeño para Apple; problema muy concreto; una sola métrica; usuarios intensamente motivados que ya están comparando con Garmin.

**Data entry burden.** Nulo. **Time-to-value.** Inmediato (aplícalo a un nado pasado en la primera sesión). **Backend.** Ninguno. **Third-party dependency.** Baja.

**Monetization hypothesis.** Pago único 9,99–14,99 $. Sin comparable directo, lo que es **señal ambigua**: puede ser hueco o puede ser ausencia de demanda. Ver el análisis honesto en la sección 7.

**MVP.** (1) Leer nados de aguas abiertas de HealthKit con su ruta; (2) mostrar track crudo frente a track corregido con distancia y ritmo recalculados; (3) algoritmo de suavizado configurable con explicación de qué descartó y por qué; (4) escribir el entrenamiento corregido en Salud como fuente propia; (5) exportar GPX/FIT.

**Solo-developer feasibility.** Alta. **Estimated MVP scope.** Pequeño. **Would I personally understand this product?** Media-alta: se juzga mirando el mapa y comparando con la distancia real conocida de una travesía.

---

### Candidate 6 — Estudio de práctica instrumental on-device: stems y bucles automáticos por estructura

**Usuario.** Músicos que aprenden canciones de oído: guitarristas, bajistas, bateristas, cantantes, estudiantes con profesor semanal.

**Problema.** Para practicar un pasaje necesitas ralentizarlo sin cambiar el tono, repetirlo en bucle y bajar el volumen del instrumento que estás tocando — y hoy eso implica o arrastrar marcadores a mano o pagar una suscripción a un servicio en la nube.

**Current workaround.** Amazing Slow Downer, Anytune, Transcribe!, Moises, Audacity, y ponerse a marcar tiempos a mano.

**Evidencia.** Hilos perennes de recomendación: TheGearPage *"app preferida para aprender temas: ralentizar, repetir secciones"*; TalkBass (19 respuestas) con las recomendaciones repartidas entre cuatro herramientas distintas. Del lado de la tonalidad y el beat, la queja está documentada desde 2017 hasta 2026: *"el análisis de Rekordbox difiere de la etiqueta (diferencia entre mayor y menor)"* (DJ TechTools, 13 ene 2017) y artículos de 2026 sobre cómo evitar el mal análisis de tonalidad en Rekordbox, Serato y Traktor.

**Native Apple leverage.** **Music Understanding (iOS 27)** para rejilla de beats, tonalidad en el tiempo, **estructura** (secciones y frases) y **actividad por instrumento** + un modelo Core ML de separación de fuentes ejecutado on-device + `BGContinuedProcessingTask` (iOS 26) con entitlement de GPU para el análisis pesado + `AVAudioUnitTimePitch` para el cambio de velocidad sin tono. **Lo genuinamente nuevo es que "repite el segundo estribillo" y "enséñame dónde está el solo de guitarra" dejan de requerir que el usuario marque nada.**

**What already exists.** *Anytune Pro+* (**4,9 / 8300 valoraciones**, 14,99 $ de pago único). *Amazing Slow Downer* (**3,9 / 452**, 14,99 $, y su nota de versión más reciente dice literalmente *"el soporte para iOS 12 estaba roto"* — **el titular más podrido de todo el informe**). *Capo* (39,99–49,99 $/año). *Transcribe!* (39 $, escritorio, desde 1998). *Moises* (3,99–11,99 $/mes, **separación de stems en la nube**, empresa financiada). *Soundslice* (5 $/mes). *forScore* (**4,8 / 43 000**, 24,99 $ de pago único + Pro opcional a 14,99 $/año + pase de 30 días a 2,99 $ — **el mejor modelo de monetización de todo este informe**).

**Why Apple doesn't already solve it.** Apple envía la API, no el producto. GarageBand no hace nada de esto.

**Why an indie could compete.** El mercado paga **14,99 $ una vez** por la función de ralentizar, y **paga suscripción solo donde hay coste de servidor**. Music Understanding y Core ML eliminan el coste de servidor. Nadie ocupa hoy la casilla **"19,99 $ una vez, corre en el Neural Engine, sin subida, sin cuenta, funciona con tus propios ficheros"**. Y el líder de la categoría de pago único está a 3,9 estrellas y hablando de iOS 12.

**Data entry burden.** Nulo (importas un fichero y el análisis es automático).

**Time-to-value.** Inmediato: importas una canción y ves los compases, la tonalidad y las secciones sin tocar nada.

**Backend requirement.** Ninguno.

**Third-party dependency.** Baja — **con una restricción estructural importante**: el catálogo de Apple Music y de Spotify está protegido por DRM y **no se puede analizar**. El producto funciona sobre ficheros del usuario, grabaciones propias y entrada de micrófono. Esto limita el TAM, pero afecta igual a todos los competidores desde 2022.

**Monetization hypothesis.** El modelo forScore: **24,99 $ de pago único** + capa Pro anual opcional. Dinero demostrado a escala real: forScore 43 000 valoraciones, Anytune 8300.

**MVP.**
1. Importar audio propio (Archivos, biblioteca local, grabación).
2. Análisis con Music Understanding: rejilla de beats, tonalidad, secciones.
3. Bucle por sección con un toque ("repite el estribillo 2") y cambio de velocidad sin alterar el tono.
4. Atenuación de un instrumento usando separación de fuentes on-device.
5. Guardar puntos de práctica por canción.

**Solo-developer feasibility.** Alta para 1-3 y 5; **media** para 4 (integrar y optimizar un modelo de separación es trabajo real, aunque hay modelos abiertos convertibles a Core ML).

**Estimated MVP scope.** Medio.

**Would I personally understand this product?** **Alta si tocas un instrumento; media si no.** Es imprescindible ser usuario: la calidad se juzga con el oído.

**Riesgo temporal que hay que decir en voz alta.** Music Understanding es **iOS 27**, publicado hace una semana. Un producto que lo exija tiene la base instalada casi vacía hoy y razonable a mediados de 2027. Mitigación: la v1 puede usar detección de beats propia o iOS 26 y adoptar Music Understanding como mejora.

---

### Candidate 7 — Herramienta de tonalidad y transposición para directores musicales

**Usuario.** Directores de música de iglesias, directores de coros, líderes de bandas de versiones: gente que cada semana decide en qué tono se canta algo y reparte partituras transpuestas.

**Problema.** "La grabación de referencia está en Si bemol, mi vocalista necesita Sol, ¿qué cejilla y qué partitura le doy a cada uno?"

**Current workaround.** Detectar el tono de oído o con una app de DJ, transponer a mano, mantener PDFs y hojas de cálculo por canción y por vocalista, y usar Planning Center u OnSong.

**Evidencia.** Volumen constante de contenido especializado sobre transposición y elección de tonalidad (worshiptutorials.com, worshipartistry.com, markcole.ca), varias apps nuevas en 2026 (Resonate, id6761076221), y una señal comercial muy concreta: **OnSong abandonó su modelo de compra única y movió a toda su base a suscripción (23,99 $/año en solo, hasta 799 $/año en campus)**, dejando a los compradores antiguos con la versión de 2020.

**Native Apple leverage.** **Music Understanding** (tonalidad detectada **a lo largo del tiempo**, no solo global — importa porque muchas canciones modulan) + `PDFKit` + `WidgetKit` + Live Activity durante el ensayo o el directo.

**What already exists.** *Planning Center Services* (gratis 1 tipo de servicio → 14–99 $/mes, dueño del presupuesto institucional). *OnSong* (suscripción 23,99–799 $/año). *forScore* (4,8 / 43 000, 24,99 $). *Resonate* (gratis, sin IAP, sin valoraciones suficientes — una app regalada por un ministerio, no un negocio).

**Why Apple doesn't already solve it.** Es un flujo de trabajo profesional de nicho. Apple nunca lo tocará.

**Why an indie could compete.** El hueco es del lado del **músico individual**, no de la organización: "mi tono frente al tono de la banda", cejillas, notas de ensayo, setlist en el Watch con indicaciones. Planning Center posee el lado de la institución para siempre; pero acaba de haber una migración forzosa a suscripción que ha dejado a mucha gente resentida.

**Data entry burden.** Bajo. **Time-to-value.** Primer día. **Backend.** Ninguno. **Third-party dependency.** Baja (mismo límite de DRM que el candidato 6).

**Monetization hypothesis.** Pago único 24,99 $ estilo forScore. Dinero demostrado: las iglesias aprueban 299 $/año por una banda de diez personas sin pestañear.

**MVP.** (1) Importar grabación de referencia y detectar tonalidad; (2) tabla de tonos por vocalista con cálculo de cejilla y transposición; (3) setlist por servicio con el tono decidido; (4) exportar PDF transpuesto o la hoja de acordes; (5) vista en el Watch durante el ensayo.

**Solo-developer feasibility.** Alta. **Estimated MVP scope.** Medio.
**Would I personally understand this product?** **Media.** El dominio es poco profundo (teoría musical básica) pero requiere hablar con tres o cuatro directores musicales antes de escribir una línea.

---

### Candidate 8 — Biblioteca musical por BPM y estructura para profesores de baile

**Usuario.** Profesores de salsa, bachata, swing, tango y baile de salón; y bailarines que practican solos.

**Problema.** "Necesito quince canciones a 180-190 BPM para la clase del martes, y necesito saber dónde empieza y acaba cada sección para montar la coreografía."

**Current workaround.** Tablas de tempos publicadas, hojas de cálculo con BPM anotados a mano, contar pulsos con un cronómetro, y preguntar en foros.

**Evidencia.** Hilos recurrentes de "¿a qué BPM va esto?" en salsaforums.com y dance-forums.com; las tablas de tempo de baile de salón existen precisamente porque es una consulta constante; apps puntuales como "Bachata Speed" y packs de música ordenados por BPM vendidos en Gumroad. **Evidencia MEDIA: real pero sin ningún hilo con volumen alto.**

**Native Apple leverage.** **Music Understanding** (rhythm y structure) sobre la biblioteca local + `MusicKit` para la biblioteca del usuario + listas generadas + App Intents ("Siri, pon algo a 185 BPM").

**What already exists.** Prácticamente nada específico y con tracción. Los DJs usan Rekordbox y Mixed In Key (escritorio, caros). **La ausencia de competencia aquí es ambigua y probablemente signifique mercado pequeño, no hueco.**

**Why Apple doesn't already solve it.** Apple Music tiene listas por "ambiente", no por tempo medido.

**Why an indie could compete.** Nicho demasiado pequeño para cualquiera; la experiencia puede ser extremadamente enfocada.

**Data entry burden.** Nulo. **Time-to-value.** Inmediato tras el primer análisis de biblioteca. **Backend.** Ninguno. **Third-party dependency.** Baja, con el límite de DRM.

**Monetization hypothesis.** Pago único 9,99–19,99 $. **No encontré comparables que demuestren disposición a pagar en este segmento concreto.** Eso es una debilidad real, no un detalle.

**MVP.** (1) Análisis por lotes de la biblioteca local con `BGContinuedProcessingTask`; (2) filtro y ordenación por BPM; (3) listas por rango de tempo; (4) marcadores de sección automáticos; (5) exportar a Música.

**Solo-developer feasibility.** Alta. **Estimated MVP scope.** Pequeño.
**Would I personally understand this product?** **Baja-media** salvo que bailes. Es el candidato con peor founder fit de los tres musicales.

---

### Candidate 9 — Diario de parámetros de acuario con captura por cámara

**Usuario.** Acuaristas de arrecife y de agua dulce avanzados que miden calcio, alcalinidad, magnesio, nitratos, fosfatos y pH varias veces por semana.

**Problema.** Apuntar cinco números a mano tras cada test, con las manos mojadas, y luego no poder ver si algo está derivando.

**Current workaround.** Cuaderno de espiral, pizarra, papel resistente al agua, plantillas de Excel compartidas en el foro, y tres apps que el usuario prueba y abandona.

**Evidencia.** **La mejor cita de toda la investigación.** Hilo titulado literalmente *"¿Qué usáis realmente para registrar vuestros parámetros de agua? Me sorprende lo malas que son las opciones"*, Reef2Reef, 23 feb 2026, **cuatro páginas** (https://www.reef2reef.com/threads/what-do-you-actually-use-to-track-your-water-parameters-im-shocked-by-how-bad-the-options-are.1149384/). Desglose del autor: *"Aquarimate: pagué 10 $, la interfaz parecía diseñada en 2012, no conseguí borrar una entrada errónea"*; *"AquaticLog: bien, pero ¿el plan pro de 25 $/año solo para recordatorios? ¿Para recordatorios?"*. Plantillas de Excel de la comunidad en Reef2Reef, WAMAS y BettaFish. **Contrapunto honesto de la misma comunidad:** una parte de los acuaristas experimentados rechaza las apps por principio — *"sé que no voy a registrar cosas en el móvil con las manos mojadas"*.

**Native Apple leverage.** `VisionKit DataScannerViewController` para **leer el display digital de un comprobador Hanna o de un fotómetro con la cámara** (este es el 10× real: no teclear) + `Vision` + `HealthKit` no aplica + `WidgetKit` para el último valor y la próxima tarea + App Intents/Siri para dictar un valor con las manos ocupadas + Swift Charts + CloudKit.

**What already exists.** *Aquarimate* (4,4 / **625 valoraciones**, **9,99 $ de compra + 9,99 $/año de sincronización + 9,99 $ de almacenamiento**, **última actualización junio de 2025**). *AquaticLog* (4,2 / 401, gratis con 1 acuario, luego 4,99 $/mes, 39,99 $/año o 149,99 $ vitalicio; el desarrollador sí está activo). *Reef Diary* (lanzada may 2025, **1,0 con 1 valoración**). *Aquarium Pulse* (3,3 con 3 valoraciones). Quejas de 1-3 estrellas de Aquarimate: el muro de pago por capas es la queja número uno — reseñas que lo llaman *"engañoso y deshonesto en su marketing"*; *"múltiples tickets de soporte sin respuesta"*; pérdida de datos al actualizar la suscripción; hay que reintroducir los parámetros por acuario.

**Why Apple doesn't already solve it.** Obviamente nunca.

**Why an indie could compete.** Es el campo más limpio del informe: el titular lleva quince meses sin actualizar, tiene un peaje de tres capas odiado y el soporte muerto; el número dos cobra 39,99 $/año por un cuaderno de hobby; y los dos entrantes de 2025-26 tienen 1 y 3 valoraciones. La lista de quejas es la especificación del producto.

**Data entry burden.** **Bajo, y bajarlo es la propuesta de valor**: lectura por cámara del display, dictado por Siri, widget de entrada rápida, app de Watch.

**Time-to-value.** Primera medición.

**Backend requirement.** Ninguno (CloudKit).

**Third-party dependency.** Baja.

**Monetization hypothesis.** **Pago único 14,99–19,99 $, con sincronización incluida y sin cobrar aparte** — posicionándose explícitamente contra las capas de Aquarimate. La comunidad expresa preferencia por compra única frente a suscripción de forma repetida.

**MVP.** (1) Registro rápido de parámetros con objetivos por acuario y rangos ideales; (2) captura por cámara del display del comprobador; (3) gráficas de tendencia por parámetro con detección de deriva; (4) recordatorios de test y de dosificación **sin coste adicional**; (5) sincronización iCloud e importación/exportación CSV.

**Solo-developer feasibility.** **Alta.**
**Estimated MVP scope.** Pequeño.
**Would I personally understand this product?** **Alta.** El dominio se aprende en una tarde (una lista de parámetros y sus rangos), la comunidad es extremadamente conversadora y el juicio de calidad es de UX pura.

**Limitación honesta del tamaño.** 625 + 401 valoraciones es **todo el mercado visible en EE. UU.**. Incluso ganándolo entero, hablamos de **1 000–3 000 €/mes**. Para el objetivo declarado ("cientos de euros al mes ya es un éxito si enseña distribución y monetización") eso es exactamente adecuado; para sustituir un salario, no.

---

### Candidate 10 — Cuaderno de campo por voz, offline y con las manos ocupadas

**Usuario.** Apicultores inspeccionando colmenas con guantes, viveristas, técnicos de campo, biólogos de campo, gestores forestales, controladores de plagas.

**Problema.** Tomar notas estructuradas en el sitio es imposible con guantes, sin cobertura y con las dos manos ocupadas, así que la gente apunta en papel y lo pasa a limpio después (o no lo pasa).

**Current workaround.** Cuadernos de papel vendidos como producto en Amazon, listas de comprobación imprimibles, notas de voz sin transcribir, y hojas de cálculo posteriores.

**Evidencia.** Industria artesanal completa de cuadernos y checklists de apicultura en papel (beekeepinglikeagirl.com, foxhoundbeecompany.com, carolinahoneybees.com); hilo "Log book, record keeping, notes" en BeeSource; varias apps recientes con poca tracción (ApiNote, HiveMind). **Evidencia MEDIA-DÉBIL**: el patrón de "papel vendible" es sólido, el testimonio directo es escaso porque las comunidades relevantes quedaron fuera de alcance.

**Native Apple leverage.** **`SpeechTranscriber`/`SpeechAnalyzer` (iOS 26): transcripción larga on-device y offline**, con sesgo de vocabulario vía `AnalysisContext` para el argot del dominio (nombres de reina, estado de cría, variedades) + **Foundation Models** para convertir la transcripción en un registro estructurado (`@Generable`) + `Core NFC` (una etiqueta por colmena o por parcela) + `CoreLocation` + fotos. **Sin nube, sin cobertura, sin suscripción: esa es la propuesta entera.**

**What already exists.** Apps verticales pequeñas sin tracción visible. Las herramientas de dictado generales existen pero no producen registros estructurados offline.

**Why Apple doesn't already solve it.** Dictado produce texto plano, no un registro tipado que va a una base de datos local.

**Why an indie could compete.** La combinación offline + estructurado + específico de dominio no existía técnicamente hace dos años. Y el usuario ya paga por papel.

**Data entry burden.** Bajo (hablar es el data entry). **Time-to-value.** Primera inspección. **Backend.** Ninguno. **Third-party dependency.** Baja.

**Monetization hypothesis.** Pago único 19,99–29,99 $ por vertical. **Sin comparables que demuestren disposición a pagar en digital** — solo la venta de cuadernos de papel, que es una señal indirecta.

**MVP.** (1) Plantilla de inspección configurable; (2) grabación y transcripción on-device offline; (3) extracción a campos estructurados con Foundation Models, editable; (4) etiqueta NFC o QR por unidad inspeccionada; (5) exportación a CSV/PDF del histórico.

**Solo-developer feasibility.** Alta. **Estimated MVP scope.** Medio.
**Would I personally understand this product?** **Media.** El flujo (hablar → registro) es juzgable por cualquiera; la plantilla correcta requiere hablar con practicantes. Riesgo de elegir el vertical equivocado.

---

### Candidate 11 — Informe fotográfico de visita técnica generado en el dispositivo

**Usuario.** Autónomos y micro-empresas que visitan un sitio y tienen que entregar un informe con fotos: instaladores, peritos, tasadores, mantenimiento, reformas, control de plagas.

**Problema.** Las fotos de la visita se quedan en el carrete y montar el informe para el cliente cuesta una hora por la tarde.

**Current workaround.** Fotos en el carrete, WhatsApp al cliente, y un documento montado a mano; o CompanyCam a 63–249 $/mes.

**Evidencia.** Categoría editorial entera sobre "del caos en obra al informe instantáneo" (photoidapp.net, 2026); argumentario comercial sobre fotos de antes y después para ganar trabajos (bellafsm.com). **CompanyCam cobra 63–79 $/mes para 1-2 usuarios y 199–249 $/mes en el nivel Scale**, y en 2026 eliminó el mínimo de tres usuarios, abriendo un camino real de una sola licencia. Quejas documentadas de CompanyCam: *"casos sin resolver durante más de dos meses"*, y ausencia de planificación, despacho y facturación.

**Native Apple leverage.** `PhotoKit` + `Vision` (anotación y detección automática) + **Foundation Models on-device para redactar el texto del informe a partir de las etiquetas y del dictado** + `PDFKit` + `CoreLocation` (sello de ubicación y hora) + `SpeechTranscriber` para dictar la nota de cada foto.

**What already exists.** *CompanyCam* (empresa, 63–249 $/mes). *Spectacular Inspection System* (4,6 / **60 valoraciones**, gratis con informe a 14,99 $ — modelo de pago por informe muy interesante). *PhotoReport*, *Inspect*, *PHOTO iD*.

**Why Apple doesn't already solve it.** Es software de negocio.

**Why an indie could compete.** El nivel de precio de CompanyCam deja un hueco enorme debajo, y el modelo de **14,99 $ por informe** de Spectacular es una cuña de bajo compromiso. Foundation Models hace gratis la parte que antes exigía una API de IA de pago.

**Data entry burden.** Bajo. **Time-to-value.** Primera visita. **Backend.** Mínimo (idealmente ninguno). **Third-party dependency.** Baja.

**Monetization hypothesis.** Pago por informe o suscripción baja (9,99–19,99 $/mes). **Es el único nicho del informe con ingresos por cliente realmente altos.**

**MVP.** (1) Proyecto por visita con captura rápida; (2) nota dictada por foto, transcrita on-device; (3) borrador de informe generado localmente y editable; (4) PDF con logotipo, fecha y ubicación; (5) compartir por Mail o enlace.

**Solo-developer feasibility.** Alta técnicamente.
**Estimated MVP scope.** Medio.
**Would I personally understand this product?** **Media.** El producto es juzgable (¿el PDF es presentable?), pero **Spectacular tiene 60 valoraciones**: esto no se vende por descubrimiento en App Store, se vende por asociaciones gremiales, boca a boca en obra y llamadas de onboarding. Es un negocio con ventas y soporte, no una app indie. RevenueCat confirma la forma: **Business es la categoría más lenta en llegar a 1 000 $/mes, 113 días de mediana.**

---

### Candidate 12 — Transcripción y resumen largos, 100 % en el dispositivo

**Usuario.** Gente que graba conversaciones largas y no quiere subirlas a ningún servidor: consultores, periodistas, investigadores, estudiantes, abogados, cualquiera sujeto a confidencialidad, y cualquiera con una grabadora llena de notas de voz sin escuchar.

**Problema.** Transcribir y resumir una hora de audio hoy significa o subirla a un servicio de terceros con una suscripción mensual, o no hacerlo.

**Current workaround.** Otter, servicios basados en Whisper en la nube, notas de voz que nunca se vuelven a abrir.

**Evidencia.** **Indirecta pero amplia**: interés sostenido en HN por herramientas de transcripción local y por benchmarks de OCR/VLM frente a herramientas tradicionales (146 puntos en un benchmark de OCR); el grueso del mercado (Otter, Moises, etc.) es de suscripción precisamente porque procesa en servidor. **Marcada como MEDIA: no encontré un hilo único de alto volumen que sea la "cita bala".**

**Native Apple leverage.** Esta es la combinación más pura del informe: **`SpeechAnalyzer` + `SpeechTranscriber` (iOS 26)** para transcripción larga on-device con resultados en streaming y sesgo de vocabulario + **`BGContinuedProcessingTask` (iOS 26)** con acceso a GPU para que el procesado de un fichero largo continúe cuando el usuario sale de la app, con progreso visible y cancelable + **Foundation Models** para resumen, extracción de acuerdos y temas (uso legítimo: transformación de texto, no conocimiento) + `Core Spotlight` para hacer buscable el corpus + App Intents. Nada sale del dispositivo.

**What already exists.** Muchas apps de transcripción; casi todas con nube y suscripción. La casilla vacía es **"pago único, no sube nada, funciona en avión"**.

**Why Apple doesn't already solve it.** Notas de Voz transcribe pero no resume ni estructura ni gestiona un corpus; la app Notas transcribe llamadas en contextos limitados. Ninguna ofrece un archivo buscable de sesiones largas.

**Why an indie could compete.** El coste marginal de la competencia es su servidor; el tuyo es cero. Puedes cobrar una vez donde ellos cobran cada mes, y la privacidad es una propuesta verificable, no un eslogan.

**Data entry burden.** Nulo. **Time-to-value.** Inmediato (transcribe una nota de voz existente en la primera sesión). **Backend.** Ninguno. **Third-party dependency.** Baja.

**Monetization hypothesis.** Pago único 24,99–39,99 $ o muro de pago duro. Comparable de disposición a pagar: todo el mercado de suscripción existente.

**MVP.** (1) Importar audio o grabar; (2) transcripción on-device con marcas de tiempo, continuando en background; (3) resumen y puntos de acción con Foundation Models, con degradación elegante en dispositivos sin Apple Intelligence; (4) búsqueda en todo el archivo, integrada con Spotlight; (5) exportar texto, Markdown y PDF.

**Solo-developer feasibility.** Alta.
**Estimated MVP scope.** Medio.
**Would I personally understand this product?** **Alta.** Eres exactamente el usuario, y la calidad se juzga leyendo la transcripción.

**Restricciones reales que hay que respetar.** Los Foundation Models están **limitados por tasa en segundo plano** (un desarrollador alcanzó el límite con cuatro peticiones a intervalos de 30 s en una extensión), así que el resumen debe hacerse en primer plano o a demanda, no por lotes nocturnos. La ventana de 4096 tokens obliga a resumen por trozos (map-reduce), que Apple documenta. Y solo funciona en dispositivos con Apple Intelligence: la transcripción debe funcionar sin él y el resumen debe ser la capa opcional.

---

### Candidate 13 — Coste real de carga del coche eléctrico en casa

**Usuario.** Conductores de coche eléctrico que cargan en casa y necesitan justificar el gasto: autónomos que se lo deducen, empleados que lo reclaman a la empresa, o simplemente gente con tarifa horaria que quiere saber qué le cuesta.

**Problema.** La factura de la luz no distingue el coche del resto de la casa, y la compañía eléctrica no lo pone fácil.

**Current workaround.** Estimaciones a ojo, capturas de la app del cargador, hojas de cálculo.

**Evidencia.** Columna editorial de Electrek (22 mar 2026) planteando exactamente la pregunta: *"conduzco mi eléctrico por trabajo pero cargo en casa, ¿cómo registro el coste de carga?"* (https://electrek.co/2026/03/22/evq-i-drive-my-ev-for-work-but-charge-at-home-how-do-i-track-charging-costs/). Cinco o más apps recientes en App Store (EEVEE, EVTracker, EV Charge Tracker, EV Efficiency Tracker). **Evidencia MEDIA: una fuente editorial buena, mucha app nueva, ningún hilo de comunidad con volumen.**

**Native Apple leverage.** `CoreLocation` (geocerca en casa) + detección de conexión a CarPlay o al Bluetooth del coche como disparador + `Core NFC` (una etiqueta en el garaje, un toque para abrir la sesión) + tarifa horaria configurable + `WidgetKit` y **Live Activity durante la carga** + App Intents para Atajos + `PDFKit` para el informe mensual de reembolso.

**What already exists.** Las cinco apps citadas, ninguna con tracción visible destacable. Los fabricantes de cargadores tienen sus propias apps, pero no calculan coste con tarifa horaria ni generan un justificante.

**Why Apple doesn't already solve it.** Nunca lo hará.

**Why an indie could compete.** Es un conteo con dinero en juego (mismo patrón que el candidato 3) y el teléfono ya conoce la ubicación y el momento. Pero la energía consumida hay que introducirla o inferirla, lo cual es la debilidad.

**Data entry burden.** **Medio** — y es su mayor problema. Sin un cargador con API, los kWh los mete el usuario o se estiman.

**Time-to-value.** Primera carga. **Backend.** Ninguno. **Third-party dependency.** Baja si evitas integrar cargadores; **alta** si los integras.

**Monetization hypothesis.** Pago único 9,99–14,99 $ o suscripción muy barata. Sin comparables fuertes.

**MVP.** (1) Detección automática de sesión de carga en casa; (2) tarifa horaria/por tramos configurable; (3) estimación de kWh por duración y potencia, corregible; (4) informe mensual en PDF para reembolso; (5) Live Activity y widget.

**Solo-developer feasibility.** Alta. **Estimated MVP scope.** Pequeño.
**Would I personally understand this product?** **Media-alta**, especialmente si tienes coche eléctrico. El dominio (tarifas eléctricas) es aprendible.

---

### Candidate 14 — Registro de entrenamiento de fuerza diseñado desde cero para VoiceOver

**Usuario.** Personas ciegas y con baja visión que entrenan en gimnasio.

**Problema.** Ajustar series, repeticiones y peso en las apps de entrenamiento existentes es inutilizable con VoiceOver, así que la comunidad se recomienda entre sí usar la app Salud de Apple.

**Current workaround.** La app Salud de Apple, que es accesible pero no es un registro de fuerza; o memoria; o notas de voz.

**Evidencia.** AppleVis (11 sep 2023): un usuario pide una app gratuita de registro de entrenamiento donde se puedan añadir ejercicios y editar repeticiones, series y pesos, porque *"la mayoría carecen de soporte adecuado de VoiceOver para ajustar parámetros"*; la única respuesta es usar la app nativa, *"muy accesible con VoiceOver; incluso hay gráficos de audio"* (https://www.applevis.com/forum/ios-ipados/free-accessible-app-tracking-workouts). La pregunta reaparece en varios hilos ("Seeking health and fitness app recommendations", "Can anyone suggest a good health and fitness tracker?"). El foro de watchOS de AppleVis tiene **645 temas y 2814 mensajes**. **Evidencia MEDIA: la recurrencia es la señal, no ningún hilo individual (uno de ellos tiene una sola respuesta).**

**Native Apple leverage.** `HealthKit` (escritura de entrenamientos de fuerza — **nota: HealthKit no tiene tipo para series y repeticiones**, así que el detalle vive en tu app) + **Audio Graphs (`AXChart`), una API pública que casi nadie usa** + VoiceOver rotor personalizado + `WatchKit` con corona digital para contar + App Intents y Siri para "añade una serie de 80 kilos por ocho".

**What already exists.** Decenas de apps de fuerza (Strong, Hevy, GymLogger, Reps) ninguna de las cuales está diseñada primero para VoiceOver. Nadie ocupa este puesto.

**Why Apple doesn't already solve it.** La app Salud es accesible pero no es un registro de entrenamiento de fuerza; la app Entreno del Watch registra un bloque de calorías, no series.

**Why an indie could compete.** Es un **hueco de ejecución puro**, no de API. Un ingeniero iOS senior tiene exactamente la habilidad que falta.

**Data entry burden.** Medio por naturaleza (registrar series es teclear), pero minimizable con corona, voz y plantillas.

**Time-to-value.** Primera sesión. **Backend.** Ninguno. **Third-party dependency.** Baja.

**Monetization hypothesis.** Pago único barato o freemium con precio justo. **Advertencia honesta: el mercado es pequeño y una parte relevante de la comunidad espera que la accesibilidad sea gratuita.** Esto es más un proyecto de reputación y aprendizaje de distribución que un negocio.

**MVP.** (1) Registro de ejercicio, serie, repeticiones y peso completamente navegable por VoiceOver; (2) contador por corona digital en el Watch; (3) Audio Graphs para la progresión; (4) entrada por voz vía App Intents; (5) escritura del entrenamiento en HealthKit.

**Solo-developer feasibility.** Alta. **Estimated MVP scope.** Pequeño.
**Would I personally understand this product?** **Media-alta.** La accesibilidad es una competencia de iOS, no un dominio ajeno; pero hay que probar con usuarios reales de VoiceOver desde el primer día, y AppleVis es un canal directo para hacerlo.

---

### Candidate 15 — Vigilancia doméstica ligera de un familiar mayor

**Usuario.** Hijos adultos que han puesto un Apple Watch a un padre o madre mayor, típicamente con deterioro cognitivo incipiente.

**Problema.** El Watch detecta caídas y avisa a emergencias, **pero no te avisa a ti**, y no hay forma de saber si ha salido de casa, si el reloj está cargado o si está puesto.

**Current workaround.** Hojas de Excel con cuentas y contraseñas, Family Wall a 45 $/año, recordatorios de Alexa, PDFs comprados en Etsy, llamar por teléfono.

**Evidencia.** Hilo de AgingCare (ene 2024) con cuidadores describiendo exactamente eso, incluido un *"¡¡¡No hay ninguna!!!"* (https://www.agingcare.com/questions/what-digital-tools-are-helpful-as-you-manage-caregiving-or-care-navigation-485081.htm). Siete hilos distintos en Apple Support sobre monitorizar a un mayor, incluido *"Apple Health Data Sharing Delayed"*, y uno específico sobre que **la detección de caídas no notifica al familiar con quien compartes datos**.

**Native Apple leverage.** App de watchOS en el reloj del mayor (`CoreLocation` con geocercas vía `CLMonitor`, estado de batería, detección de muñeca, `HKWorkoutSession` no aplica) + app de iPhone para el cuidador + notificaciones. **Requiere backend propio**, porque HealthKit es local al dispositivo y el compartir de Apple no cubre estos eventos.

**What already exists.** *BoundaryCare* (4,1 / **110 valoraciones**, niveles de 9,99 / 34,99 / 89,99 / 149,99 $, precios **no publicados** en su web — la compra pasa por una evaluación previa). *Peace of Mind* y *WatchRx*: no pude verificar fichas ni precios actuales.

**Why Apple doesn't already solve it.** Apple ha tomado la capa de **seguridad** (caídas, choques, SOS, Check In, Buscar, compartir Salud) y la regala. Lo que queda son geocercas de deambulación específicas de demencia, paneles para el cuidador, adherencia a medicación y **configuración remota de un dispositivo que el portador no sabe manejar** — nada de eso es prioridad de Apple.

**Why an indie could compete.** 110 valoraciones para el líder de categoría significa que casi nadie lo ha resuelto, y la disposición a pagar es de las más altas del software de consumo: un hijo comprando para su madre no regatea.

**Data entry burden.** Nulo. **Time-to-value.** Primer día. **Backend requirement.** **Moderado-alto** — es el único candidato de la lista que lo exige, y es un punto en su contra según tus propios criterios. **Third-party dependency.** Baja.

**Monetization hypothesis.** Suscripción 9,99–14,99 $/mes. Dinero claramente presente (el nivel de 149,99 $ de BoundaryCare lo confirma).

**MVP.** (1) App de Watch que reporta ubicación, batería y detección de muñeca; (2) geocercas con aviso al cuidador; (3) notificación al cuidador ante caída detectada por el sistema (dentro de lo que las API permiten); (4) panel en el iPhone del cuidador; (5) configuración remota mínima.

**Solo-developer feasibility.** **Media-baja.**
**Estimated MVP scope.** Grande.
**Would I personally understand this product?** **Media.** Entiendes la tecnología perfectamente; no entiendes por defecto la relación cuidador-cuidado, y **el coste de un fallo es una alerta perdida en una emergencia real**. Hay responsabilidad legal y reputacional seria. **No es un primer proyecto.**

---

## 6. Candidates rejected early

Ideas que parecían atractivas y que descarté antes de darles ficha completa. La razón importa tanto como la lista.

**Inconstruibles por falta de API pública** (esto es la parte más importante de esta sección: cada una de estas se propone constantemente y ninguna es posible):

| Idea descartada | Por qué es imposible |
|---|---|
| Triaje, resumen o agregación de **notificaciones de otras apps** | No existe API. Apple, en los foros: *"no hay API pública para descubrir nada sobre otras apps instaladas en el dispositivo. Sería un gran fallo de privacidad"*. `UNUserNotificationCenter` es estrictamente por app |
| Asistente de finanzas personales sobre **transacciones de Apple Pay** | No existe API. FinanceKit solo cubre Apple Card, Apple Cash, Savings y open banking del Reino Unido — y exige **cuenta de organización**, categoría Finanzas y distribución en EE. UU. o Reino Unido |
| "Una app para ver todos tus pases de Wallet" (billetes, entradas, tarjetas de fidelidad) | `PKPassLibrary.passes()` devuelve **solo los pases cuyo identificador de tipo está en tu propio entitlement**, es decir, los que tú emitiste |
| "Prepara mis analíticas para la consulta" usando **Health Records / FHIR** | Los tipos clínicos anunciados en 2018 **no están expuestos en las cabeceras de HealthKit**. Hilo sin resolución desde entonces |
| Un tracker de medicación mejor **que alimente la app Salud** | Los tipos de medicación de HealthKit son **de solo lectura** para terceros; confirmado por Apple WWDR |
| Deduplicar o corregir los entrenamientos que escribió el Apple Watch | Una app **no puede editar ni borrar muestras de otra fuente** |
| Panel de Salud en el **Mac** | **No hay HealthKit en macOS**, ni API en la nube. Exigiría una app companion en el iPhone que empuje los datos |
| Convertir el Apple Watch en **pulsómetro para un ciclocomputador** | No hay rol público de periférico BLE de ritmo cardíaco en watchOS |
| App de buceo usando profundidad y presión | El entitlement de profundidad sumergida es de **solicitud a Apple** con reportes de **más de cinco meses sin respuesta** y prácticamente ningún concesionario conocido fuera de fabricantes de hardware |
| Cualquier cosa con **pagos, llaves de coche o billetes NFC** | HCE exige establecimiento en el EEE, cuenta de organización, compromisos PCI DSS/EMVCo y un acuerdo con una entidad licenciada |
| Cualquier cosa con **SensorKit** (PPG en bruto, ECG, luz ambiente, uso del dispositivo) | Requiere propuesta de investigación y **aprobación de comité de ética (IRB)**; la app debe publicarse bajo la cuenta de la institución |
| App de control parental / Screen Time **fuera de la UE** con nombres de app reales | Los `ApplicationToken` son opacos por diseño; **la extensión DeviceActivityReport no tiene red ni puede escribir al App Group**, así que no puedes leer los minutos de uso dentro de tu app. Además: el desarrollador de *one sec* publicó en abril de 2026 una lista de radares de producción sin resolver (umbrales que no disparan, datos corruptos con dominios a 20 h/día, regresión en iOS 26 con `didReachThreshold` disparando inmediatamente) |
| Cualquier app cuyo bucle central sea **procesamiento de IA por lotes en segundo plano** | Foundation Models está limitado por tasa en background con el dispositivo a batería; un desarrollador llegó al límite con 4 peticiones a 30 s de intervalo |
| App de DJ o de análisis del **catálogo de Apple Music / Spotify** | Audio con DRM, sin acceso a PCM. El FAQ de la Apple Music API dice explícitamente *"no hay soporte actualmente para apps de estilo DJ"* |
| Una alarma o alerta que **atraviese el modo No molestar** como mecánica central | Critical Alerts requiere solicitud a Apple; las concesiones se agrupan en médico, seguridad pública y emergencias. Un indie de productividad debe asumir denegación |

**Descartadas por mercado, no por tecnología:**

- **Trackers de garantías y recibos.** Nueve o más apps en la tienda; **ninguna con suficientes valoraciones para que Apple muestre una media**. No es "mercado abierto", es ausencia de demanda demostrada repetidamente. El usuario registra una garantía una vez y no vuelve. El único dinero es B2B (Sortly 288–1788 $/año), que no tiene forma de app indie. Además Apple erosiona el caso con seguimiento de pedidos en Wallet y resumen de recibos en Mail.
- **Organizadores de capturas de pantalla.** Genuinamente sin competencia — y sin valor: techo de precio observado **2,99 $**, líder de categoría con **1,0 estrellas**, 15 repos de GitHub en 2026 con 0-5 estrellas, y Apple dueña del punto de entrada con Visual Intelligence (buscar en la web desde la captura, crear eventos de calendario desde una captura). *Abierto pero sin valor* es una categoría real y esta es su ejemplo perfecto.
- **Aves (identificación y registro).** Merlin de Cornell: **gratis, 4,9, 112 000 valoraciones**, financiada por una universidad y es el estándar científico. Birda demuestra que la capa social se puede monetizar (2200 valoraciones, hasta 59,99 $/año) pero es una empresa financiada construyendo efecto de red, que es justamente lo que un solo desarrollador no puede arrancar. La única grieta (eBird tiene 3,8 estrellas) no te sirve, porque los datos viven en eBird.
- **Puentes de sincronización hacia plataformas de entrenamiento.** Hay demanda medida (**243 votos** en TrainingPeaks UserVoice) y titulares vivos y queridos (RunGap 4,8 con 5900 valoraciones, HealthFit a 6,99 $ único). Pero el precio es de 15-50 $/año, la carga de mantenimiento es de N integraciones y **cada una de esas empresas puede borrarte el producto**. RunGap acaba de publicar *"Retired Fitbit integration"*.
- **"Estadísticas y tendencias de Salud hechas bien".** Ver candidato 2. Apple reescribió Salud este mes con Insights, Longevity y Health Age.
- **Cuidado de plantas de interior.** Cinco o más entrantes en 2025-26 sobre PictureThis, Planta y Greg. Categoría de granja de suscripciones.
- **Registro de kilometraje, escáner de tarjetas de visita, aparcamiento, registros genéricos de buceo y de juegos de mesa.** Decenas de competidores, sin defensibilidad.
- **Un "coach de fitness con IA".** Lo excluiste tú explícitamente y la investigación lo confirma: es un envoltorio de IA sin job concreto, y además cae en la restricción de rate limiting si intenta procesar en segundo plano.
- **Astrofotografía (cuaderno de sesiones).** Evidencia de dolor excelente (560 filas, 40 columnas, 280 noches) pero exige conocimiento real del dominio (cabeceras FITS, SIMBAD/VizieR, WCS), tiene forma de escritorio y no de iPhone, y el mercado es diminuto. **Lo descarto por founder fit, no por falta de problema** — y es un descarte ajustado.

---

## 7. Comparative analysis

Comparación cualitativa, sin puntuación numérica falsa. Las columnas son las de tu lista de 22 criterios, agrupadas.

| # | Candidato | Claridad y evidencia del problema | Frecuencia | Data entry | Ventaja iOS | Gap vs Apple | Competencia | Monetización plausible | Dependencia externa | Backend | Riesgo App Review | Viable en solitario | Founder fit | Veredicto |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Informe de salud para el médico | **Fuerte** (captura impresa documentada) | trimestral | Nulo | Alta | 11 años de indiferencia | Contestada, titular muerto | 5-25 $ único, techo bajo | Baja | Ninguno | Medio (5.1.3) | **Alta** | **Alta** | **Finalista** |
| 2 | Auditor de datos de Salud | Media-fuerte | semanal | Nulo | Alta | **Apple acaba de reescribir Salud** | Muy poblada | Buena en teoría | Baja | Ninguno | Medio | Alta | Alta | **Descartado** |
| 3 | Días por jurisdicción | **Fuerte** (9 repos en 2026, 4 apps nuevas) | diaria pasiva, consulta mensual | Bajo y automatizable | **Muy alta** (ubicación) | Apple nunca lo hará | Schengen contestada, **fiscal abierta** | **20-130 €, miedo a sanción** | Baja | Ninguno | Bajo | Alta | Alta / media | **Finalista #1** |
| 4 | GPX en el Watch | **Fuerte** (hilo de 206 páginas) | por salida | Bajo | **Muy alta** | Apple no envía GPX | **Brutal** (6 años de motor de mapas) | Demostrada a escala | Baja | Ninguno | Bajo | **Baja-media** | Media | Descartado por coste |
| 5 | Corrección de nados | Fuerte (testimonio detallado) | semanal en temporada | Nulo | Alta | Apple no admite el fallo | **Ninguna — ambiguo** | Sin comparable | Baja | Ninguno | Bajo | Alta | Media-alta | Casi finalista |
| 6 | Estudio de práctica musical | Media-fuerte + **API nueva** | diaria | Nulo | **Muy alta** (Music Understanding) | Apple no envía producto | Contestada, **titular a 3,9★** | **Demostrada: 43 k y 8,3 k valoraciones** | Baja (con límite DRM) | Ninguno | Bajo | Media-alta | **Alta si tocas** | **Finalista #2** |
| 7 | Tonalidad para directores musicales | Media | semanal | Bajo | Alta | Apple nunca | Planning Center domina la institución | Buena (presupuesto de iglesia) | Baja | Ninguno | Bajo | Alta | Media | Casi finalista |
| 8 | BPM para profesores de baile | **Media-débil** | semanal | Nulo | Alta | Apple nunca | **Ausencia ambigua** | **Sin comparable** | Baja | Ninguno | Bajo | Alta | **Baja-media** | Descartado |
| 9 | Diario de acuario | **Fuerte** (4 páginas, cita literal) | 2-3 veces/semana | Bajo, y es el eje | Alta (cámara + Siri + Watch) | Apple nunca | **Abierta: titular a 15 meses** | 15-20 $ único; techo 1-3 k€/mes | Baja | Ninguno | Bajo | **Alta** | **Alta** | **Finalista #4** |
| 10 | Cuaderno de campo por voz | Media-débil | por inspección | Bajo (hablar) | **Muy alta** (SpeechTranscriber offline) | Dictado no estructura | Escasa | Sin comparable digital | Baja | Ninguno | Bajo | Alta | Media | Wildcard mental |
| 11 | Informe fotográfico de visita | Media | diaria laboral | Bajo | Alta | Apple nunca | Contestada, CompanyCam caro | **La más alta por cliente** | Baja | Mínimo | Bajo | Alta técnica | **Media** | Descartado: es un negocio de ventas |
| 12 | Transcripción larga on-device | Media (indirecta pero amplia) | semanal | Nulo | **Muy alta** (3 APIs nuevas) | Notas de Voz no resume ni archiva | Poblada en la nube, **vacía en local** | **Todo el mercado de suscripción** | Baja | Ninguno | Bajo | **Alta** | **Alta** | **Finalista #3** |
| 13 | Coste de carga del VE | Media | diaria pasiva | **Medio** ← problema | Alta | Apple nunca | 5 apps sin tracción | Sin comparable fuerte | Baja | Ninguno | Bajo | Alta | Media-alta | Descartado por data entry |
| 14 | Fuerza accesible con VoiceOver | Media (recurrencia) | 3-4 veces/semana | Medio | Alta (Audio Graphs) | App Salud no es un log de fuerza | **Nadie ocupa el puesto** | **Débil: mercado pequeño** | Baja | Ninguno | Bajo | Alta | Media-alta | Descartado por tamaño |
| 15 | Vigilancia de familiar mayor | Media-fuerte | continua | Nulo | Alta | Apple tomó la seguridad, no el cuidado | **Abierta: líder con 110 valoraciones** | **Alta disposición a pagar** | Baja | **Moderado-alto** ← | Medio | **Media-baja** | Media | Descartado como primer proyecto |

**Cómo se aplicaron los kill criteria, explícitamente:**

- *"Apple ya lo resuelve suficientemente bien"* → mata el candidato 2 (reescritura de Salud de septiembre de 2026) y refuerza el descarte de los organizadores de capturas (Visual Intelligence).
- *"Hay que alimentar manualmente otra base de datos"* → penaliza el 13 (kWh a mano) y el 14 (series y repeticiones), y es la razón por la que el 3, el 5, el 6 y el 12 suben: en todos ellos el dato ya existe o se genera solo.
- *"Requiere backend complejo desde v1"* → mata el 15.
- *"Depende de una API externa crítica"* → mata toda la categoría de puentes de sincronización, y es exactamente el fallo que ya conoces de tu proyecto anterior con TMDB.
- *"Requiere conocimiento sectorial profundo"* → mata astrofotografía y penaliza el 11 y el 7.
- *"App Store discovery es la única estrategia"* → penaliza el 11 (Spectacular: 60 valoraciones en años) y el 8.
- *"Es simplemente un wrapper de IA"* → ninguno de los finalistas usa Foundation Models como propuesta de valor; en el 12 la propuesta es *que no sube nada a un servidor* y el modelo es una pieza interna.

**El patrón que emerge.** Los cinco que sobreviven comparten tres propiedades: el dato lo genera el sistema o el usuario ya lo tiene; el valor se percibe en la primera sesión; y **ninguno necesita servidor**, lo que permite cobrar una vez donde el competidor cobra cada mes. Esa última propiedad es la ventaja estructural más limpia que tiene hoy un desarrollador indie de Apple, y es directamente consecuencia de las APIs on-device que Apple ha ido enviando entre iOS 26 y iOS 27.

---

## 8. Final five

Seleccionados por diversidad de dominio y por supervivencia a la criba, no por tamaño de mercado.

---

### Finalist 1 — Contador automático de días por jurisdicción

**Problem in one sentence.** Saber automáticamente cuántos días has estado en cada país y cuántos te quedan antes de incumplir Schengen o de activar una residencia fiscal.

**Why this survived.** Es el único candidato que puntúa alto en todo a la vez: evidencia fuerte y reciente, dato generado por el sistema sin data entry, consecuencia económica que motiva la compra inmediata, cero dependencia de terceros, cero backend, cero riesgo de que Apple lo absorba, y un titular que demuestra el dinero con un modelo de pago único.

**Native advantage.** Core Location con `CLMonitor` y monitorización de visitas atribuye días a países **sin que el usuario haga nada**. Esa es exactamente la diferencia entre este producto y una hoja de cálculo o una calculadora web, y no es replicable en web. Añade EventKit para importar viajes ya planificados, Live Activity con los días restantes durante el viaje, widget y App Intents para preguntárselo a Siri.

**Existing evidence.** **Nueve repos nuevos de calculadora Schengen en GitHub solo en 2026** sobre quince o más totales. Cuatro o más apps comerciales lanzadas en 2026. Comentario en Hacker News (nov 2025) de alguien construyéndose el suyo por necesitar Schengen **y** residencia fiscal simultáneamente. El titular, Schengen Simple, acumula **2500 valoraciones con 4,8** cobrando **7,99-14,99 £ una sola vez**.

**Existing competitors.** Schengen Simple (fuerte, querido, respuesta de soporte en horas, sin reseñas negativas visibles); Nomad Tracker (feb 2026, suscripción y **129,99 £ vitalicio**); Flamingo Compliance (fiscal, precios no públicos); 90 Days in Europe (9,99-14,99 $/año); Days Monitor.

**Why there may still be room.** **No en Schengen: ahí llegas tarde y el titular es bueno.** El hueco está en la capa fiscal — Statutory Residence Test del Reino Unido, substantial presence test de EE. UU., reglas de 183 días en varias jurisdicciones a la vez, y reglas estatales. Mayor consecuencia, sin marca dominante, y soporta precio 5-10× superior. Nomad Tracker ya está probando ese precio.

**Main risk.** Que Schengen Simple añada el módulo fiscal antes que tú — tiene la base de usuarios, la marca y la confianza. Riesgo secundario real: la exactitud de las reglas fiscales es responsabilidad tuya de facto aunque pongas un descargo, y equivocarte con un usuario le cuesta dinero de verdad.

**Cheapest validation.** Una página de aterrizaje con las tres jurisdicciones concretas que soportarías y un formulario de lista de espera, difundida en r/digitalnomad (cuando tengas acceso), Nomad List, Hacker News y foros de expatriados británicos y estadounidenses en España y Portugal. Objetivo: 200 correos en cuatro semanas. En paralelo, una **prueba técnica de dos días**: dejar corriendo `CLMonitor` con geocercas de país y medir cuántos cruces reales detecta y con cuánta latencia. Si la atribución automática de país no es fiable, el producto no tiene ventaja sobre la competencia y deberías abandonarlo ahí.

**MVP shape.** Registro automático de país por día corregible a mano; motor de reglas para Schengen 90/180 y **una** jurisdicción fiscal; planificador de "¿qué pasa si viajo estas fechas?"; exportación PDF con evidencia día a día; widget de días restantes. Muro de pago duro.

**Monetization evidence.** Schengen Simple: 2500 valoraciones a 7,99-14,99 £ de pago único. Nomad Tracker: hasta 129,99 £ vitalicio. Y el perfil de compra (evitar una multa de 500 $-3000 € y una prohibición de entrada) es el que RevenueCat documenta con mejor conversión en muro de pago duro: **10,7 % a día 35 frente al 2,1 % del freemium**.

**First 100 users.** Foros de expatriados (British Expats, Expat Forum, r/AmerExit, r/digitalnomad, r/ExpatFIRE); comunidades de nómadas (Nomad List, Remote Year); grupos de Facebook de "británicos en España" y "americanos en Portugal" tras el Brexit; SEO de cola larga en consultas muy específicas ("UK statutory residence test calculator app", "cuántos días puedo estar en España sin ser residente fiscal"); Product Hunt; y, muy concretamente, **contactar a los autores de los nueve repos de GitHub de 2026** — son usuarios cualificados que ya intentaron resolvérselo solos.

**Founder fit.** Alta. El producto es un motor de reglas sobre un flujo de eventos de ubicación: un ingeniero senior puede auditar la corrección línea a línea, escribir tests con casos límite reales (el día de llegada cuenta, la ventana móvil se recalcula cada día) y detectar de inmediato si la atribución automática está fallando. No hace falta ser asesor fiscal para leer una norma de 183 días; sí hace falta disciplina para no dar la impresión de estar dando asesoramiento.

---

### Finalist 2 — Estudio de práctica instrumental on-device

**Problem in one sentence.** Aprender un pasaje de una canción exige ralentizarlo, repetirlo en bucle y bajar un instrumento, y hoy eso significa marcar tiempos a mano o pagar una suscripción a un servicio en la nube.

**Why this survived.** Es el mejor ejemplo de "una primitiva nueva de Apple convierte un negocio de suscripción en un producto de pago único". La disposición a pagar está demostrada a escala real, el titular de la casilla exacta que atacarías tiene 3,9 estrellas y habla de iOS 12 en su changelog, no hay backend, y Music Understanding elimina de un golpe el trabajo de DSP que hasta ahora era la barrera.

**Native advantage.** Music Understanding (iOS 27) da rejilla de beats, tonalidad variable en el tiempo, **estructura de canción** y **actividad por instrumento** on-device y gratis. `BGContinuedProcessingTask` con acceso a GPU permite analizar un fichero largo mientras el usuario hace otra cosa. Un modelo de separación de fuentes en Core ML corre en el Neural Engine. **Todo el competidor relevante que hace esto lo hace en servidor y cobra mensualmente por ello.**

**Existing evidence.** Hilos perennes de recomendación en TheGearPage y TalkBass donde las respuestas se reparten entre cuatro herramientas distintas, señal clásica de que ninguna resuelve el trabajo entero. Quejas documentadas de precisión de detección de tonalidad en Rekordbox, Serato y Traktor desde 2017 hasta artículos de 2026. Y el mercado: forScore con **43 000 valoraciones**, Anytune con **8300**.

**Existing competitors.** Anytune Pro+ (4,9 / 8300, 14,99 $ único, fuerte); **Amazing Slow Downer (3,9 / 452, 14,99 $, changelog sobre iOS 12 — el titular más podrido del informe)**; Capo (39,99-49,99 $/año); Transcribe! (39 $, escritorio, desde 1998); Moises (3,99-11,99 $/mes, stems en la nube, empresa financiada); Soundslice (5 $/mes).

**Why there may still be room.** Nadie ocupa la casilla **"pago único, separación de stems en el Neural Engine, sin subida, sin cuenta, funciona sin conexión"**, y nadie usa estructura e instrumentos para generar los bucles automáticamente. Moises posee la versión en la nube; la versión local no tiene dueño.

**Main risk.** **Music Understanding es iOS 27, publicado hace una semana: la base instalada es prácticamente cero hoy.** Un producto que lo exija no tiene mercado hasta bien entrado 2027. Riesgo secundario: la separación de fuentes on-device con calidad comparable a Moises es trabajo de ingeniería real, no una integración de tarde. Riesgo terciario: el techo de mercado está limitado por el DRM — solo ficheros propios.

**Cheapest validation.** Dos días: coge un modelo abierto de separación de fuentes, conviértelo a Core ML, y mide **calidad y tiempo de proceso de una canción de cuatro minutos en un iPhone 15 Pro**. Si tarda más de un par de minutos o la separación suena a lata, el producto no existe. En paralelo, una prueba de Music Understanding sobre veinte canciones propias para ver si la detección de estructura es lo bastante buena como para que "repite el estribillo 2" funcione sin que el usuario corrija.

**MVP shape.** Importar audio propio; análisis automático de beats, tonalidad y secciones; bucle por sección con un toque y cambio de velocidad sin alterar el tono; atenuación de un instrumento; puntos de práctica guardados por canción. Pago único con capa Pro opcional, modelo forScore.

**Monetization evidence.** forScore: 24,99 $ de pago único, **más** una capa Pro genuinamente opcional a 14,99 $/año, **más** un pase de 30 días a 2,99 $ para el músico que lo necesita una semana concreta — con 43 000 valoraciones y 4,8 estrellas. **Es el mejor modelo de monetización de todo este informe y merece copiarse estructuralmente sea cual sea el nicho que elijas.** Anytune confirma que el pago único de 14,99 $ sostiene 8300 valoraciones.

**First 100 users.** Subreddits de instrumento (r/guitar, r/bass, r/drums, r/piano) cuando tengas acceso; TalkBass, TheGearPage, Ultimate Guitar; profesores particulares de música, que son multiplicadores naturales (un profesor lo recomienda a veinte alumnos); YouTubers de "aprende esta canción"; y la comunidad de desarrolladores de Apple, porque "corre entero en el Neural Engine, no sube nada" es una historia que se cuenta sola en Hacker News y en el blog del propio autor.

**Founder fit.** **Alta si tocas un instrumento, media si no.** Es condición casi necesaria: la calidad se juzga con el oído y las decisiones de producto (¿cuántos compases de preroll antes del bucle? ¿la atenuación o el mute?) solo las acierta alguien que practique. Si no tocas, este candidato baja varios puestos.

---

### Finalist 3 — Transcripción y resumen largos, 100 % en el dispositivo

**Problem in one sentence.** Transcribir y resumir una hora de conversación hoy obliga a subir el audio a un servicio de terceros con suscripción mensual.

**Why this survived.** Reúne tres capacidades nuevas de Apple en un producto de una frase, no necesita servidor, el fundador es literalmente el usuario, y el argumento de privacidad es verificable en lugar de ser marketing. Es el candidato con mejor relación entre novedad técnica y comprensibilidad para el usuario.

**Native advantage.** `SpeechAnalyzer` y `SpeechTranscriber` (iOS 26) son la primera API de Apple diseñada para transcripción **larga** on-device, con resultados en streaming y sesgo de vocabulario; `BGContinuedProcessingTask` (iOS 26) permite que un fichero largo termine de procesarse cuando el usuario sale de la app, con progreso visible y cancelable; Foundation Models resume y extrae acuerdos sin enviar nada. `Core Spotlight` hace buscable el archivo completo desde el sistema. **Nada de esto era posible con calidad en 2023.**

**Existing evidence.** **Es la evidencia más débil de los cinco finalistas y hay que decirlo.** Es indirecta: el mercado entero (Otter y sucedáneos) es de suscripción porque procesa en servidor, y hay interés sostenido en Hacker News por herramientas locales y por benchmarks de reconocimiento. No encontré un hilo único de alto volumen que sea la cita definitiva, en parte por el bloqueo de Reddit.

**Existing competitors.** Muchas apps de transcripción, casi todas con nube y suscripción. Notas de Voz de Apple transcribe pero no resume, no estructura y no gestiona un archivo buscable.

**Why there may still be room.** La casilla vacía es precisa: **"pago único, no sube nada, funciona en avión"**. Tu coste marginal es cero y el del competidor es su factura de GPU, así que puedes cobrar una vez donde ellos cobran cada mes sin perder margen.

**Main risk.** Que Apple lo absorba. Notas de Voz ya transcribe, Notas transcribe llamadas, y añadir "resume esta grabación" con Apple Intelligence es un paso pequeño y muy probable. **Este es el finalista con mayor riesgo de plataforma.** Riesgo secundario: la limitación de tasa de Foundation Models en segundo plano obliga a hacer el resumen en primer plano, lo que empeora la experiencia frente a "déjalo procesando toda la noche".

**Cheapest validation.** Una tarde: transcribe con `SpeechTranscriber` una grabación real de 60 minutos en un iPhone 15 Pro y mide **tiempo de proceso, tasa de error y consumo de batería**. Después mide el resumen por trozos con Foundation Models y comprueba si el resultado es útil o genérico. Si la transcripción de una hora tarda más que la grabación, o el resumen es plano, el producto no se sostiene y lo sabes en un día.

**MVP shape.** Importar o grabar; transcripción on-device con marcas de tiempo que continúa en segundo plano; resumen y puntos de acción con degradación elegante en dispositivos sin Apple Intelligence; búsqueda sobre todo el archivo integrada con Spotlight; exportación a texto, Markdown y PDF.

**Monetization evidence.** Todo el mercado de suscripción de transcripción demuestra disposición a pagar; tu apuesta es capturarla con un pago único de 24,99-39,99 $ o un muro de pago duro. Referencia estructural: de nuevo el modelo forScore.

**First 100 users.** Comunidades de privacidad (Hacker News, Lobsters, r/privacy); comunidades Apple que celebran las apps locales (Mac Power Users, MacStories, Six Colors, el newsletter de Federico Viticci); investigadores cualitativos y consultores; y un artículo técnico propio sobre "cómo transcribir una hora de audio sin salir del iPhone", que es exactamente el tipo de contenido que se difunde solo entre desarrolladores y luego entre usuarios.

**Founder fit.** **Alta.** Eres el usuario, el dominio no existe (no hay sector que aprender) y la calidad se evalúa leyendo la transcripción y comparándola con lo que se dijo.

---

### Finalist 4 — Diario de parámetros de acuario con captura por cámara

**Problem in one sentence.** Los acuaristas miden cinco parámetros varias veces por semana y apuntarlos con las manos mojadas es tan incómodo que acaban en un cuaderno o en una hoja de cálculo.

**Why this survived.** Es el campo más limpio del informe: la mejor cita de evidencia, un titular con quince meses sin actualizar y un muro de pago de tres capas que sus propios usuarios llaman deshonesto, soporte muerto, cero riesgo de plataforma, alcance de MVP pequeño y founder fit alto. Es el candidato con mayor probabilidad de **terminarse y publicarse**, que para un primer producto vale más que el tamaño del mercado.

**Native advantage.** `DataScannerViewController` leyendo el display digital de un comprobador Hanna o un fotómetro con la cámara — **ese es el 10× real: no teclear**. Más Siri y App Intents para dictar un valor con las manos ocupadas, widget de entrada rápida, app de Watch, Swift Charts y CloudKit. Una app web no puede hacer nada de esto.

**Existing evidence.** Hilo de Reef2Reef del 23 feb 2026 titulado literalmente *"me sorprende lo malas que son las opciones"*, **cuatro páginas**, con un desglose punto por punto de las tres apps del mercado. Plantillas de Excel compartidas en Reef2Reef, WAMAS y BettaFish.

**Existing competitors.** Aquarimate (4,4 / **625**, 9,99 $ **más** 9,99 $/año de sincronización **más** 9,99 $ de almacenamiento, última actualización jun 2025); AquaticLog (4,2 / 401, hasta 149,99 $ vitalicio, desarrollador activo); Reef Diary (**1,0 con 1 valoración**); Aquarium Pulse (3,3 con 3).

**Why there may still be room.** Las quejas de 1-3 estrellas del titular son la especificación completa del producto: peaje por capas, soporte sin respuesta, pérdida de datos al actualizar la suscripción, imposibilidad de borrar una entrada errónea, parámetros que hay que reintroducir por acuario. Y nadie está usando la cámara para eliminar el tecleo.

**Main risk.** **El tamaño.** 625 + 401 valoraciones es todo el mercado visible en EE. UU.; incluso ganándolo entero hablamos de 1000-3000 €/mes. Y hay un contrapunto de la propia comunidad: una parte de los acuaristas experimentados rechaza las apps por principio — *"sé que no voy a registrar cosas en el móvil con las manos mojadas"*. Si ese segmento es mayoritario, la captura por cámara es justamente la respuesta, pero conviene validarlo antes que después.

**Cheapest validation.** Publicar en ese mismo hilo de Reef2Reef, que sigue vivo, un mockup de la lectura por cámara del comprobador Hanna y preguntar dos cosas: si pagarían 15-20 $ una vez con sincronización incluida, y si la captura por cámara cambiaría su comportamiento. La comunidad es extremadamente conversadora y te responderá en horas. Coste: una tarde de Figma.

**MVP shape.** Registro rápido con objetivos y rangos por acuario; captura por cámara del display del comprobador; gráficas de tendencia con detección de deriva; recordatorios de test y dosificación **incluidos sin coste extra**; sincronización iCloud e importación/exportación CSV.

**Monetization evidence.** Aquarimate sostiene 625 valoraciones cobrando 9,99 $ más extras; AquaticLog vende un vitalicio de 149,99 $. El dinero existe. **El posicionamiento correcto es explícitamente contra las capas: un precio, todo incluido.**

**First 100 users.** Reef2Reef (el hilo de febrero sigue abierto), r/ReefTank y r/Aquariums cuando tengas acceso, WAMAS y clubs locales de acuariofilia, grupos de Facebook de arrecife, YouTubers del nicho (BRStv y equivalentes), y la propia lista de gente que se quejó en ese hilo — son cien usuarios cualificados con nombre y apellidos.

**Founder fit.** **Alta.** El dominio se aprende en una tarde (una lista de parámetros y sus rangos ideales), no hay legislación ni medicina de por medio, y la calidad del producto se juzga íntegramente por UX: ¿puedo registrar cinco valores en veinte segundos con las manos mojadas?

---

### Finalist 5 — Informe de salud listo para la consulta médica

**Problem in one sentence.** Llevarle al médico cuatro métricas de Salud en un rango de fechas, en una hoja legible, es hoy imposible sin recurrir a capturas de pantalla impresas.

**Why this survived.** La evidencia es de las más fuertes y más humanas del informe, el titular natural del nicho lleva tres años y medio muerto acumulando valoraciones, el alcance es pequeño, no hay backend y Apple ha demostrado once años de indiferencia hacia la exportación. **Lo incluyo sabiendo que el techo es bajo**, porque encaja exactamente con tu objetivo declarado de aprender distribución y monetización con un producto terminable.

**Native advantage.** HealthKit es la única vía de acceso a esos datos, punto. No hay API en la nube y no hay HealthKit en macOS: **el iPhone es el único lugar del mundo donde este producto puede existir**. Añade PDFKit y Swift Charts y no necesitas nada más.

**Existing evidence.** El hilo de MacRumors de agosto de 2024 cuya resolución documentada fue imprimir capturas de pantalla de las lecturas de tensión. Siete o más hilos duplicados en Apple Support sobre exportación. Quince repos de GitHub, algunos con más de 500 estrellas, dedicados solo a parsear el volcado XML.

**Existing competitors.** Heart Reports (4,4 / **412**, 3,99 $, **abandonada desde febrero de 2023**); Simple Health Export CSV (abandonada desde 2022); QS Access (muerta desde iOS 13); vitalina (4,8 / 24, 4,99 $ vitalicio, lanzada marzo de 2026, muy activa); Health Auto Export (4,3 / 395, hasta 24,99 $) y HealthFit (4,6 / 901, 6,99 $), ambas excelentes pero orientadas a CSV y atletas.

**Why there may still be room.** El sub-nicho concreto ("PDF para el médico", no "CSV para mi hoja de cálculo") es la parte menos poblada de la categoría, y su titular está muerto. Además hay una **ventana temporal de una semana**: el cambio de iOS 27 a autorización de histórico limitado frente a completo es nuevo, y ninguna app competidora lo maneja todavía con elegancia. Quien lo haga bien tendrá durante meses la única app que explica al usuario por qué faltan datos antiguos y cómo ampliarlo.

**Main risk.** **El techo de precio, que el mercado ya ha fijado en 5-25 $ de pago único.** Con 400-900 valoraciones por app en el nicho, incluso liderándolo hablamos de cientos de euros al mes, no de miles. Riesgo secundario: hay una oleada visible de entrantes con sabor a IA en 2026 (vitalina y tres o cuatro más) que puede saturar el hueco en doce meses. Riesgo terciario y no trivial: la guía 5.1.3 de App Review es estricta con datos de salud, y la 1.4.1 exige advertencias sobre consultar al médico.

**Cheapest validation.** Pregunta directa en comunidades de pacientes crónicos y de cuidadores: "¿cómo le llevas tus datos al médico?" y "¿pagarías 6 € por un PDF de una página?". Coste cero. En paralelo, comprueba en el simulador y en dispositivo cómo se comporta realmente la doble hoja de autorización de iOS 27 y qué devuelve `getEarliestAuthorizedSampleDate` — es la parte del producto que nadie ha resuelto.

**MVP shape.** Selector de métricas y rango; manejo correcto de la autorización limitada de iOS 27; PDF de una o dos páginas con tabla, gráfico, unidades y fuente del dato; CSV correcto sin filas fantasma ni marcas de tiempo a cero; compartir e imprimir.

**Monetization evidence.** HealthFit a 6,99 $ con 901 valoraciones y puesto 5 en apps de pago de Salud y Forma Física; Health Auto Export con vitalicio de 24,99 $ y 395 valoraciones; vitalina a 4,99 $ con 4,8 estrellas tras seis meses. Además, Salud y Forma Física es la categoría con **mejor ingreso por instalación (0,48 $ a día 14) y mejor conversión de descarga a pago (2,9 %)** de todo el conjunto de RevenueCat.

**First 100 users.** Comunidades de pacientes (hipertensión, fibrilación auricular, diabetes tipo 2) y de cuidadores; grupos de Facebook de pacientes; foros de Apple Watch donde la pregunta "cómo le llevo esto al médico" reaparece cada año; ASO sobre consultas muy explícitas ("export health data to PDF for doctor", "informe tensión arterial para el médico"); y contenido propio respondiendo esa pregunta, que tiene búsqueda constante y competencia editorial débil.

**Founder fit.** **Alta.** No hay dominio médico que aprender: no diagnosticas nada, solo presentas datos que el usuario ya tiene. La calidad se juzga mirando el PDF y preguntándose si un médico con siete minutos de consulta lo entendería de un vistazo.

---

## 9. Three wildcards

Tres que estuve a punto de descartar y que no conviene olvidar.

### Wildcard 1 — Bluetooth Channel Sounding: medir distancias reales sin hardware especial

**Qué es.** iOS 27 expone Channel Sounding: **distancia con precisión métrica a cualquier periférico Bluetooth 6.3**, mediante `CBChannelSoundingSessionConfiguration`, con los resultados en `CBChannelSoundingProcedureResults.distance`. Combinado con `NINearbyAccessoryConfiguration(bluetoothChannelSoundingIdentifier:)` añade ángulo horizontal con asistencia de cámara.

**Por qué merece no olvidarse.** Hasta ahora, medir distancia con precisión exigía UWB, que exige un accesorio con chip U1/U2 o un iPhone en el otro extremo. Channel Sounding lo abre a **cualquier periférico BLE 6.3 barato**, y el ecosistema de esos periféricos va a existir en 2027. Eso habilita toda una clase de productos —localización fina dentro de casa o de un almacén, "¿a qué distancia está esto?", juegos de proximidad, seguimiento de un objeto etiquetado en un espacio cerrado— que hace dos años exigían hardware propietario.

**Por qué no es finalista.** Requiere **iPhone 17 o posterior** y periféricos que todavía no están en el mercado en volumen. Y no encontré un job concreto con evidencia: es capacidad buscando problema, que es exactamente lo que pediste evitar. Pero es la clase de ventana que se abre una vez cada varios años, y conviene tenerla en la cabeza cuando aparezca el problema adecuado.

### Wildcard 2 — Screen Time con nombres reales de apps, solo para la UE

**Qué es.** `FamilyControls.FamilyActivityData` (iOS 26.4) expone `installedApplications`, `visitedWebDomains` y `activityCategories` **con identificadores de bundle reales, dominios reales y nombres de categoría reales**. El entitlement, `com.apple.developer.family-controls.app-and-website-usage`, es **autoservicio en Xcode, sin formulario**. Requiere estado de autorización `.approvedWithDataAccess`.

**Por qué merece no olvidarse.** Toda la categoría de control de tiempo de pantalla es inútil precisamente porque los tokens son opacos: no puedes decirle al usuario "has pasado tres horas en Instagram" porque no sabes que era Instagram. Esta API rompe esa restricción. Es claramente una concesión de interoperabilidad de la DMA, y **tú estás en la UE**, que es exactamente donde funciona.

**Por qué no es finalista.** La restricción regional es dura: *"las instalaciones de clientes solo pueden usar esta clase en dispositivos ubicados en la UE con una cuenta Apple de un país de la UE"*. Un producto construido sobre esto funciona para usuarios europeos y se degrada en silencio en todas partes. Y el resto de la API sigue siendo un campo de minas: la extensión de informes no tiene red ni puede escribir al App Group, el entitlement de distribución tarda semanas con escalado vía soporte técnico, y el desarrollador de *one sec* publicó en abril de 2026 una lista de radares de producción sin resolver durante años. **Además queda por verificar si `.approvedWithDataAccess` desbloquea también los minutos de uso o solo la identidad de las apps** — es una prueba de dos horas en dispositivo y decide si esto es una oportunidad o una curiosidad.

### Wildcard 3 — Visual Intelligence y App Intents como canal de distribución

**Qué es.** Desde iOS 26, el contenido de una app de terceros puede aparecer como **resultado de apuntar la cámara al mundo o de buscar dentro de una captura de pantalla**, mediante `SemanticContentDescriptor` entregado a un App Intent de tipo `IntentValueQuery`. Y desde iOS 27, los esquemas de entidad de App Intents alimentan el **índice semántico de Spotlight**, y `SpotlightSearchTool` permite que un `LanguageModelSession` busque en Spotlight como herramienta.

**Por qué merece no olvidarse.** Tu problema real, según tus propios criterios, no es construir: es **distribución**, y "lo publicaré y la gente lo encontrará" no es una estrategia. Esto es una superficie de descubrimiento **nueva, del sistema, y prácticamente vacía**. Una app que se convierta en el resultado por defecto cuando alguien apunta la cámara a un objeto de su dominio —una etiqueta de vino, una planta, una pieza de recambio, una partitura— tiene un canal que sus competidores no están usando. Y los snippets interactivos de App Intents permiten algo más raro todavía: un producto cuya superficie principal no sea una app que se abre, sino una respuesta que aparece en Spotlight o en el botón de Acción, con el sistema manteniendo tu proceso vivo en memoria mientras el snippet está visible.

**Por qué no es finalista.** No es un producto, es una táctica. Pero es la táctica que más deberías incorporar a cualquiera de los cinco finalistas, y merece un día de experimentación por sí sola.

---

## 10. Important platform constraints discovered

Lista de trabajo. Cada línea mata o reconfigura una clase entera de ideas.

**Acceso a datos que no existe.** No hay API para: notificaciones de otras apps; iMessage o SMS (salvo filtrado de remitentes desconocidos vía `ILMessageFilterExtension`, que **no puede acceder a la red directamente ni escribir a contenedores compartidos con la app contenedora**, y nunca ve iMessage ni contactos); historial de llamadas; Safari; contenido de otras apps; transacciones de Apple Pay; pases de Wallet de otros desarrolladores; Health Records FHIR; Screen Time detallado fuera de la extensión de informes. **No hay extensiones de Mail en iOS** — MailKit es solo macOS.

**HealthKit, los detalles que cambian el diseño.**
- iOS 27 introduce autorización de **histórico limitado frente a completo**. Denegado y acceso completo son **indistinguibles**; solo la concesión limitada es detectable, vía `getEarliestAuthorizedSampleDate(for:)`. Aplica solo a tipos de muestra.
- Los tipos de **medicación son de solo lectura** para terceros.
- Una app **no puede editar ni borrar muestras escritas por otra fuente**.
- **No hay tipo de HealthKit para series y repeticiones** de fuerza; ese detalle vive siempre siloado en cada app.
- Background delivery requiere el entitlement `com.apple.developer.healthkit.background-delivery`; `stepCount` está capado a frecuencia horaria en iOS; en watchOS son 4 actualizaciones/hora compartidas; y **tres fallos en llamar al completion handler cortan las actualizaciones**.
- **No hay HealthKit en macOS y no hay API en la nube.**
- Guía 5.1.3: los datos de HealthKit y Motion & Fitness no pueden usarse para publicidad ni minería de datos, no pueden compartirse con terceros salvo investigación con consentimiento e IRB, y **no pueden almacenarse en iCloud**.

**Live Activities son un destino de render, no un canal.** Máximo **8 horas activas y 12 horas absolutas**; payload total **≤ 4 KB**; **sin acceso a red y sin recibir actualizaciones de ubicación**; no soportadas en visionOS; no se pueden iniciar desde background salvo mediante un `LiveActivityIntent`.

**Background.** `BGContinuedProcessingTask` (iOS 26) es la novedad importante, pero: debe iniciarla el usuario, exige `ProgressReporting`, muestra una Live Activity del sistema que el usuario puede cancelar, y **muere en silencio si el usuario descarta la app en el conmutador**. La GPU requiere entitlement, y **iOS 27 añade la misma restricción al Neural Engine** (`...continued-processing.inference`).

**Foundation Models.** Ventana de **4096 tokens** que incluye instrucciones, esquemas y herramientas; al desbordarse la sesión **deja de responder permanentemente**. **Limitación de tasa en segundo plano** con el dispositivo a batería, y las extensiones cuentan como segundo plano. Solo en dispositivos con Apple Intelligence (iPhone 15 Pro en adelante). Conocimiento del mundo con corte alrededor de octubre de 2023. **Los guardarraíles solo funcionan en los idiomas soportados**, y los falsos positivos de seguridad sobre contenido benigno están documentados en los foros. Las versiones del modelo están ancladas a versiones del sistema operativo: 26.0-26.3, 26.4 y 27.0 se comportan de forma distinta con el mismo prompt.

**Private Cloud Compute (iOS 27).** Gratis, sin claves y sin servidor, **pero** exige estar en el Small Business Program, tener menos de 2 millones de descargas de primera vez, y solicitar el entitlement gestionado. La cuota de uso es **del usuario** y se amplía comprando iCloud+. Estás construyendo una función cuyo techo fija Apple y cuya monetización va a la suscripción de Apple.

**Entitlements, escalera de dificultad real.**
- *Ninguno*: Vision, VisionKit, Sound Analysis, **Music Understanding**, MapKit, PHPicker, Core Motion, App Intents, WidgetKit, ActivityKit, ControlWidget, Core Spotlight, Visual Intelligence, Nearby Interaction, **SpeechAnalyzer**.
- *Capability en Xcode*: HealthKit y su background delivery, HomeKit, lectura de etiquetas NFC, WeatherKit, Background Modes, Background GPU, Background Inference, Locked Camera Capture, **Family Controls (desarrollo)**, **`family-controls.app-and-website-usage`**.
- *Servicio en el portal*: MusicKit, ShazamKit.
- *Solicitud a Apple*: **Family Controls (distribución)** — obtenible pero lento y opaco, con escalado vía petición de soporte técnico; Journaling Suggestions (⚠️ la documentación actual dice capability, sin confirmar con testimonios); Critical Alerts; profundidad sumergida (más de cinco meses sin respuesta reportados); **Private Cloud Compute**; SensorKit (solo investigación con IRB).
- *Gestionado, efectivamente cerrado a un indie*: **FinanceKit** (cuenta de organización, categoría Finanzas, EE. UU. o Reino Unido), **NFC HCE** (EEE, organización, PCI DSS/EMVCo, acuerdo con entidad licenciada), **Verify with Wallet**.

**Family Controls, la letra pequeña que mata productos.** Tokens opacos (`bundleIdentifier` y `localizedDisplayName` devuelven `nil`) salvo en la UE desde iOS 26.4. **La extensión `DeviceActivityReport` no tiene red, no puede notificar y no puede escribir al App Group**: solo renderiza una vista SwiftUI, así que no puedes leer los minutos de uso en tu propia app. No hay API para saber qué apps están bloqueadas ahora mismo. Bloquear una app no bloquea su web. Y la guía **2.5.1** rechaza apps que referencien la API de Screen Time sin el entitlement aprobado, detectándolo desde el binario y desde las capabilities del App ID.

**Reproducción y análisis de música.** Catálogo de Apple Music y de Spotify con **DRM, sin acceso a PCM**; el FAQ de la Apple Music API dice explícitamente que **no hay soporte para apps de estilo DJ**. Spotify cerró su API de reproducción a terceros en 2022. Todo producto de análisis musical trabaja sobre ficheros del usuario, grabaciones propias o micrófono.

**Fiabilidad física de NFC.** Dos o tres intentos por lectura es lo habitual según usuarios, con múltiples hilos convergentes. No es arreglable desde software. Si diseñas un producto sobre "toca la etiqueta", ten siempre un camino alternativo con widget o Atajos.

**AccessorySetupKit.** Las sesiones de Channel Sounding **solo** funcionan con dispositivos emparejados vía ASK, y **instanciar `CBCentralManager` antes de que ASK termine impide que aparezca el picker**.

**watchOS.** `WKExtendedRuntimeSession` permite **un solo tipo por app**, con topes de 10 minutos a 1 hora, y elegir un tipo que no corresponde con tu app es motivo de rechazo. `HKWorkoutSession` es la concesión de background más potente — y simular entrenamientos para conseguir tiempo de ejecución es rechazo seguro.

**Calendario y contactos.** EventKit **no tiene nivel de solo-lectura**: o escritura, o acceso total. Contactos sí tiene acceso limitado desde iOS 18, y `ContactAccessButton` concede contactos concretos **sin ninguna alerta** — úsalo siempre que puedas, porque la guía 5.1.1 prefiere explícitamente los pickers fuera de proceso frente al acceso total, y lo mismo vale para PHPicker frente a PhotoKit.

**Adopción.** iOS 27 tiene una semana. Cualquier cosa exclusiva de iOS 27 es un producto de 2027. iOS 26 lleva un año y es el objetivo razonable hoy — y casualmente contiene las tres palancas más interesantes (`SpeechAnalyzer`, `BGContinuedProcessingTask`, `RecognizeDocumentsRequest`).

---

## 11. What I would investigate next

Ordenado por coste ascendente. Los cinco primeros son pruebas de un día o menos que pueden matar un finalista entero, y por eso van primero.

**Pruebas técnicas que deciden si un finalista existe:**

1. **Atribución automática de país con `CLMonitor`** (finalista 1). Dos días dejando geocercas de país activas durante un viaje o simulando cruces. Mide detección y latencia. **Si la atribución no es fiable, el finalista 1 pierde su única ventaja real sobre una calculadora web y hay que abandonarlo.**
2. **Separación de fuentes on-device** (finalista 2). Convierte un modelo abierto a Core ML y mide calidad y tiempo sobre una canción de cuatro minutos en un iPhone 15 Pro. Si tarda más de un par de minutos o suena mal, no hay producto.
3. **Transcripción de una hora con `SpeechTranscriber`** (finalista 3). Mide tiempo, tasa de error y batería en el dispositivo mínimo soportado. Después mide el resumen por trozos con Foundation Models: ¿es útil o es genérico?
4. **La doble hoja de autorización de HealthKit en iOS 27** (finalistas 1 y 5). Comprueba en dispositivo el comportamiento real de `getEarliestAuthorizedSampleDate` y cómo diseñar la petición de ampliación a histórico completo. **Nadie lo ha resuelto todavía; hacerlo bien es una ventaja de meses.**
5. **`DataScannerViewController` sobre un display digital real** (finalista 4). Un comprobador Hanna, una báscula, un medidor de tensión. Si no lee fiablemente números de siete segmentos, la propuesta de valor del finalista 4 se cae y vuelve a ser otro formulario.

**Verificaciones de plataforma pendientes de este informe:**

6. Si `.approvedWithDataAccess` con `FamilyActivityData` (iOS 26.4, UE) desbloquea también **duraciones de uso** o solo identidad de apps y dominios. Dos horas. Decide si el wildcard 2 es una oportunidad.
7. Si el entitlement de **Journaling Suggestions** es realmente autoservicio en Xcode hoy. Cinco minutos abriendo el panel de capabilities.
8. Latencia real de Foundation Models en un iPhone 15 Pro (el dispositivo suelo). Apple no publica cifras.
9. El presupuesto de memoria real de la extensión `ILMessageFilterExtension` y de `DeviceActivityReport` — las cifras que circulan (≈6 MB y ≈100 MB) vienen de blogs, no de Apple.

**Investigación de mercado que este informe no pudo completar:**

10. **Rehacer la fase B con acceso a Reddit.** Es la laguna más grande. Objetivos concretos: r/shortcuts ordenado por top del último año buscando duplicación de atajos para la misma fricción; r/digitalnomad y r/ExpatFIRE para el finalista 1; r/ReefTank para el 4; r/guitar, r/bass y r/drums para el 2; r/AgingParents para el candidato 15.
11. **Abrir los ~25 hilos de `discussions.apple.com`** cuyos identificadores quedaron recogidos durante la investigación pero cuyo cuerpo estaba bloqueado. Es barato y convertiría varias señales medias en fuertes.
12. **Leer reseñas de 1-3 estrellas a escala** de los titulares de los cinco finalistas. App Store ordena por "más útiles" y sesga hacia lo positivo; hace falta otra vía.
13. **Validar el segmento del finalista 1**: ¿cuánta gente tiene simultáneamente el problema Schengen y el problema de residencia fiscal? Es la hipótesis central y descansa sobre un solo comentario de Hacker News.
14. **Hablar con tres o cuatro directores musicales** antes de descartar definitivamente el candidato 7, que quedó muy cerca del corte.

**Decisión de secuencia que te corresponde a ti.** Los finalistas 4 y 5 son pequeños, terminables en semanas y enseñan el ciclo completo de publicar, cobrar y dar soporte con riesgo bajo. Los finalistas 1, 2 y 3 son de alcance medio y tienen techo real. Dado que trabajas a tiempo completo y con responsabilidades familiares, **el orden defendible es: uno pequeño primero para aprender distribución con consecuencias bajas, y el grande después, con lo aprendido.** El finalista 1 es el que mejor combina evidencia y economía; el 4 es el que con más probabilidad terminas y publicas.

---

## 12. Sources

### Documentación de Apple (primaria)

- What's New / iOS 27 — https://developer.apple.com/whats-new/ · https://developer.apple.com/ios/whats-new/ · https://developer.apple.com/documentation/ios-ipados-release-notes/ios-ipados-27-release-notes
- HealthKit, autorización e histórico — https://developer.apple.com/documentation/healthkit/authorizing-access-to-health-data
- HealthKit background delivery — https://developer.apple.com/documentation/healthkit/hkhealthstore/enablebackgrounddelivery(for:frequency:withcompletion:)
- Core Location en background — https://developer.apple.com/documentation/corelocation/handling-location-updates-in-the-background · https://developer.apple.com/documentation/corelocation/monitoring-location-changes-with-core-location
- WeatherKit y precios — https://developer.apple.com/weatherkit/
- MusicKit — https://developer.apple.com/documentation/musickit · ShazamKit — https://developer.apple.com/documentation/shazamkit · https://developer.apple.com/help/account/services/shazamkit/
- SpeechAnalyzer / SpeechTranscriber — https://developer.apple.com/documentation/speech/speechanalyzer · https://developer.apple.com/documentation/Speech/SpeechTranscriber
- Sound Analysis — https://developer.apple.com/documentation/soundanalysis/snclassifysoundrequest
- **Music Understanding** — https://developer.apple.com/documentation/MusicUnderstanding
- Vision / VisionKit — https://developer.apple.com/documentation/vision · https://developer.apple.com/documentation/visionkit/datascannerviewcontroller
- BackgroundTasks — https://developer.apple.com/documentation/backgroundtasks/performing-long-running-tasks-on-ios-and-ipados · https://developer.apple.com/documentation/backgroundtasks/bgcontinuedprocessingtask
- App Intents — https://developer.apple.com/documentation/appintents/displaying-static-and-interactive-snippets · https://developer.apple.com/documentation/appintents/indexedentity · https://developer.apple.com/documentation/AppIntents/LongRunningIntent
- ActivityKit — https://developer.apple.com/documentation/activitykit/displaying-live-data-with-live-activities
- WidgetKit push y controles — https://developer.apple.com/documentation/WidgetKit/Updating-widgets-with-widgetkit-push-notifications · https://developer.apple.com/documentation/widgetkit/creating-controls-to-perform-actions-across-the-system
- Visual Intelligence — https://developer.apple.com/documentation/visualintelligence
- Foundation Models — https://developer.apple.com/documentation/FoundationModels/managing-the-context-window · https://developer.apple.com/documentation/FoundationModels/analyzing-images-with-multimodal-prompting · https://developer.apple.com/documentation/FoundationModels/adding-server-side-intelligence-with-private-cloud-compute · https://developer.apple.com/documentation/FoundationModels/running-a-core-ai-model-in-a-foundation-models-session · https://developer.apple.com/documentation/foundationmodels/languagemodelsession/generationerror/ratelimited(_:) · https://developer.apple.com/private-cloud-compute/
- AccessorySetupKit y Channel Sounding — https://developer.apple.com/documentation/AccessorySetupKit · https://developer.apple.com/documentation/CoreBluetooth/measuring-distance-between-devices-using-channel-sounding
- Nearby Interaction — https://developer.apple.com/documentation/nearbyinteraction · WatchKit sesiones extendidas — https://developer.apple.com/documentation/watchkit/using-extended-runtime-sessions
- FinanceKit — https://developer.apple.com/documentation/financekit · https://developer.apple.com/financekit · https://developer.apple.com/contact/request/financekit/
- SensorKit — https://developer.apple.com/documentation/sensorkit · https://developer.apple.com/documentation/bundleresources/entitlements/com.apple.developer.sensorkit.reader.allow
- Family Controls / DeviceActivity / ManagedSettings — https://developer.apple.com/documentation/FamilyControls/requesting-the-family-controls-entitlement · https://developer.apple.com/documentation/deviceactivity · https://developer.apple.com/documentation/managedsettings · https://developer.apple.com/documentation/ManagedSettings/Application · **https://developer.apple.com/documentation/FamilyControls/FamilyActivityData** · https://developer.apple.com/documentation/bundleresources/entitlements/com.apple.developer.family-controls.app-and-website-usage
- PassKit — https://developer.apple.com/documentation/passkit/pkpasslibrary · Wallet Verify — https://developer.apple.com/wallet/get-started-with-verify-with-wallet/
- Journaling Suggestions — https://developer.apple.com/documentation/journalingsuggestions · https://developer.apple.com/documentation/bundleresources/entitlements/com.apple.developer.journal.allow
- Message Filter — https://developer.apple.com/documentation/IdentityLookup/sms-and-mms-message-filtering · Call Directory — https://developer.apple.com/documentation/CallKit/identifying-and-blocking-calls · MailKit (solo macOS) — https://developer.apple.com/documentation/mailkit/build-mail-app-extensions
- NFC HCE — https://developer.apple.com/support/hce-transactions-in-apps
- App Store Review Guidelines — https://developer.apple.com/app-store/review/guidelines/
- Small Business Program — https://developer.apple.com/app-store/small-business-program/

### WWDC

- WWDC26 253 — Meet the Music Understanding framework — https://developer.apple.com/videos/play/wwdc2026/253/
- WWDC26 369 — Channel Sounding — https://developer.apple.com/videos/play/wwdc2026/369/
- WWDC26 345 — App Intents — https://developer.apple.com/videos/play/wwdc2026/345/
- WWDC21 10036 — Sound Analysis — https://developer.apple.com/videos/play/wwdc2021/10036/

### Apple Developer Forums

- Medicación en HealthKit es de solo lectura (respuesta de Apple WWDR) — https://developer.apple.com/forums/thread/803954
- Health Records sin API — https://developer.apple.com/forums/thread/95920
- Duplicación de datos de pasos — https://developer.apple.com/forums/thread/759709
- No hay API para conocer otras apps ni sus notificaciones — https://developer.apple.com/forums/thread/710167
- MusicKit y AVAudioEngine: el audio de Apple Music tiene DRM; "no hay soporte para apps de estilo DJ" — https://developer.apple.com/forums/thread/94329
- Family Controls: entitlement de distribución, retrasos y escalado — https://developer.apple.com/forums/thread/818553 · https://developer.apple.com/forums/thread/820811 · https://developer.apple.com/forums/thread/806301
- Family Controls: radares de producción sin resolver (desarrollador de *one sec*) — https://developer.apple.com/forums/thread/819997
- Tokens opacos — https://developer.apple.com/forums/thread/782492 · https://developer.apple.com/forums/thread/764988
- Rechazo 2.5.1 por referencias a Screen Time — https://developer.apple.com/forums/thread/822078
- Foundation Models: guardarraíles y límites de tasa — https://developer.apple.com/forums/thread/789788
- FinanceKit: clave de Info.plist mal documentada — https://developer.apple.com/forums/thread/757973
- Profundidad sumergida: meses sin respuesta — https://developer.apple.com/forums/thread/737204 · https://developer.apple.com/forums/thread/735296

### Evidencia de problema (comunidades)

- **Acuarios**: https://www.reef2reef.com/threads/what-do-you-actually-use-to-track-your-water-parameters-im-shocked-by-how-bad-the-options-are.1149384/ · https://www.reef2reef.com/threads/best-aquarium-log-app.1111023/ · https://www.reef2reef.com/threads/whats-your-favorite-app-to-track-your-tank.956948/ · https://www.reef2reef.com/threads/parameter-tracking-spreadsheet-with-formatting-for-ideal-ranges.1079236/
- **Salud, exportación y médico**: https://forums.macrumors.com/threads/apple-health-print-spreadsheet.2433283/ · https://forums.macrumors.com/threads/how-can-i-get-health-data-from-apple-watch-for-doctor.2182240/ · https://talk.macpowerusers.com/t/how-best-to-automate-export-from-apple-watch-into-google-sheets/38865 · https://news.ycombinator.com/item?id=47340298 · https://news.ycombinator.com/item?id=40277434 · https://applehealthdata.com/blog/best-apple-health-export-apps.html
- **Tendencias mal calculadas**: https://leancrew.com/all-this/2024/11/apple-health-trends/ · https://github.com/reschandreas/saverage
- **Pasos duplicados**: https://forums.macrumors.com/threads/does-health-app-duplicate-the-step-count-of-aw-and-phone-in-some-instances.2338067/
- **Atletas y sincronización**: https://peaksware.uservoice.com/forums/106657-trainingpeaks-customer-feedback/suggestions/42858291-allow-import-sleep-data-from-apple-watch (243 votos) · https://forum.intervals.icu/t/best-way-to-integrate-apple-watch-apple-health-data-into-intervals-icu/5776 · https://forum.intervals.icu/t/hrv-from-apple-watch-via-heart-rate-analyzer/129050
- **Navegación y natación**: https://forums.macrumors.com/threads/workoutdoors-new-workout-features.2134687/page-206 · https://forums.macrumors.com/threads/apple-watch-ultra-open-water-swim-wrong-distance-faulty-gps-track.2395116/ · https://forums.macrumors.com/threads/apple-watch-for-lap-swimming.2449519/ · https://the5krunner.com/2026/01/26/strava-routes-apple-watch-review/
- **Sueño y batería**: https://forums.macrumors.com/threads/sleep-tracking-without-a-sleep-schedule.2361714/ · https://news.ycombinator.com/item?id=32754513
- **Accesibilidad**: https://www.applevis.com/forum/ios-ipados/free-accessible-app-tracking-workouts · https://www.applevis.com/forum/ios-ipados/can-any-one-suggest-good-health-fitness-tracker · https://www.applevis.com/apps/ios/apps-for-blind-or-low-vision-users
- **Cuidadores**: https://www.agingcare.com/questions/what-digital-tools-are-helpful-as-you-manage-caregiving-or-care-navigation-485081.htm
- **Husos horarios y anillos**: https://forums.macrumors.com/threads/apple-watch-workouts-different-time-zones-while-travelling.2380303/
- **NFC**: https://community.home-assistant.io/t/nfc-tag-reliability-difficulty-reading-tags-on-first-try/827236 · https://community.home-assistant.io/t/nfc-tag-automations-being-lost-overwritten/749835
- **Música y DJ**: https://forum.djtechtools.com/t/thoughts-on-rekordbox-key-detection/75462 · https://musicianstool.com/blog/2026-01-15-avoid-bad-key-analysis-rekordbox-serato-traktor · https://www.thegearpage.net/board/index.php?threads/prefered-app-for-learning-tunes-i-e-slow-it-down-loop-sections-etc.2051439/ · https://www.talkbass.com/threads/these-transcribe-slow-down-learning-apps-questions.1197577/
- **Baile**: https://www.salsaforums.com/threads/average-salsa-song-speed-bpm-salsa-beat-machine-question.19237/ · https://www.ballroompages.com/ballroom-music/tempo-chart/
- **Worship**: https://worshiptutorials.com/blog/5-reasons-you-should-transpose-your-songs · https://worshipartistry.com/greenroom/musicianship/skill-building/how-to-transpose-a-song-in-under-5-minutes
- **Astrofotografía**: https://www.cloudynights.com/forums/topic/996443-what-would-you-like-to-see-in-an-astrophotography-logbook/ · https://www.cloudynights.com/forums/topic/864968-how-do-you-log-your-astrophotography-sessions/
- **Aves**: https://www.birdforum.net/threads/review-of-birding-apps-i-use-on-android.447551/
- **Capturas de pantalla**: https://techtiff.substack.com/p/your-camera-roll-is-a-to-do-list · https://medium.com/@jessiontheinternet/i-screenshot-everything-and-then-forget-about-it-28e872345b55
- **Nómadas y días**: https://90daysineurope.com/2026/03/27/best-schengen-calculator-apps-tools-compared-2026-find-your-perfect-90-180-day-tracker/
- **Coche eléctrico**: https://electrek.co/2026/03/22/evq-i-drive-my-ev-for-work-but-charge-at-home-how-do-i-track-charging-costs/
- **Inspección de campo**: https://photoidapp.net/field-inspection-report-automation-from-on-site-chaos-to-instant-reports/
- **Apicultura**: https://beekeepinglikeagirl.com/beekeeping-log-book/ · https://carolinahoneybees.com/bee-hive-record-keeping/

### Competencia y precios (fichas de App Store consultadas el 21 sep 2026)

- HealthFit — https://apps.apple.com/us/app/healthfit/id1202650514 · Health Auto Export — https://apps.apple.com/us/app/health-auto-export-json-csv/id1115567069 · Heart Reports — https://apps.apple.com/us/app/heart-reports/id1448243870 · Simple Health Export CSV — https://apps.apple.com/us/app/simple-health-export-csv/id1535380115 · vitalina — https://apps.apple.com/us/app/health-data-exporter-vitalina/id6759179139
- Bevel — https://apps.apple.com/us/app/bevel-longevity-performance/id6456176249 · Gentler Streak — https://apps.apple.com/us/app/gentler-streak-workout-tracker/id1576857102 · Training Today — https://apps.apple.com/us/app/training-today/id1507992127 · Health Stats — https://apps.apple.com/us/app/health-stats-fitness-tracker/id1543220823 · Pedometer++ — https://apps.apple.com/us/app/pedometer-step-counter/id712286167
- RunGap — https://apps.apple.com/us/app/rungap-workout-data-manager/id534460198 · FitnessSyncer — https://www.fitnesssyncer.com/go-pro
- WorkOutDoors — https://apps.apple.com/us/app/workoutdoors/id1241909999 · Footpath — https://apps.apple.com/us/app/footpath-route-planner/id634845718 · WristTopo — https://apps.apple.com/us/app/wristtopo-maps-for-watch/id6739765329 · https://tomsguide.com/wellness/smartwatches/i-run-marathons-and-this-apple-watch-running-app-is-the-best-usd8-ive-ever-spent
- Aquarimate — https://apps.apple.com/us/app/aquarimate/id587215055 · reseñas — https://justuseapp.com/en/app/587215055/aquarimate/reviews · AquaticLog — https://apps.apple.com/us/app/aquaticlog/id583895470
- Schengen Simple — https://apps.apple.com/gb/app/schengen-simple/id1637045933 · Nomad Tracker — https://apps.apple.com/gb/app/nomad-tracker-schengen-visa/id6756324053 · Flamingo — https://flamingotracker.com/
- forScore — https://apps.apple.com/us/app/forscore/id363738376 · Anytune — https://apps.apple.com/us/app/anytune-pro-studio-tools/id478293637 · Amazing Slow Downer — https://apps.apple.com/us/app/amazing-slow-downer/id308998718 · Moises — https://aisotools.com/pricing/moises · Soundslice — https://www.soundslice.com/plans/
- OnSong — https://onsongapp.com/pricing/ · Planning Center — https://churchmemberpro.com/blog/planning-center-pricing-guide/
- Merlin — https://apps.apple.com/us/app/merlin-bird-id-by-cornell-lab/id773457673 · eBird — https://apps.apple.com/us/app/ebird-by-cornell-lab/id988799279 · Birda — https://apps.apple.com/us/app/birda-bird-id-birding/id1564130920
- CompanyCam — https://roofingsoftwareguide.com/guides/companycam-pricing/ · Spectacular — https://apps.apple.com/us/app/spectacular-inspection-system/id542218862
- BoundaryCare — https://apps.apple.com/us/app/boundarycare-watch-based-gps/id1474130809 · https://www.boundarycare.com/our-services/order/
- Sortly — https://www.sortly.com/pricing/

### Economía indie

- **RevenueCat, State of Subscription Apps 2026** — https://www.revenuecat.com/state-of-subscription-apps · https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026 · https://www.subscriptioninsider.com/blog/revenuecat-data-shows-subscription-app-growth-concentrating-at-the-top-news
- David Smith, Widgetsmith a los cinco años — https://www.david-smith.org/blog/2025/09/18/widgetsmith-at-five/ · mapas en watchOS (seis años de trabajo) — https://www.david-smith.org/blog/2026/04/29/maps-on-watchos/
- Muky, de pago único a suscripción (HN, ene 2026) — https://news.ycombinator.com/item?id=46705676
- Apple Foundation Models, informes técnicos — https://machinelearning.apple.com/research/apple-foundation-models-2025-updates · https://machinelearning.apple.com/research/introducing-third-generation-of-apple-foundation-models
- Cómo desarrolladores usan los modelos locales de Apple — https://techcrunch.com/2025/10/03/how-developers-are-using-apples-local-ai-models-with-ios-26/
- Reescritura de la app Salud (sep 2026) — https://www.theapplepost.com/2026/09/18/72511/everything-you-need-to-know-about-apples-new-health-app/ · https://www.wareable.com/health-and-wellbeing/apple-health-ios-26-4-update-nutrition-tracking-health-plus-tier
- Visual Intelligence sobre capturas — https://www.macrumors.com/guide/ios-26-visual-intelligence/

### Afirmaciones explícitamente no verificadas

1. Si el entitlement de Journaling Suggestions es hoy autoservicio (la documentación lo sugiere; no hay testimonio de indie que lo confirme).
2. Presupuesto de memoria de `ILMessageFilterExtension` (≈6 MB) y de la extensión `DeviceActivityReport` (≈100 MB): ambos de blogs, no de Apple.
3. Si `.approvedWithDataAccess` con `FamilyActivityData` desbloquea duraciones de uso además de identidad de apps.
4. Latencia real de Foundation Models en dispositivo: Apple no publica cifras.
5. Ingresos de WorkOutDoors: **no existe ninguna cifra pública**. Cualquier estimación es inferencia.
6. Cadena exacta del entitlement de `MatterSupport`.
7. Ventana de "reproducciones recientes" de MusicKit y profundidad del archivo histórico observado de WeatherKit.
8. Lista de jurisdicciones donde UWB está deshabilitado.
9. Precios reales de BoundaryCare (no publicados), de Flamingo Compliance, y fichas actuales de Peace of Mind y WatchRx.
10. La ausencia de reseñas negativas de Schengen Simple debe leerse como *no surgieron en la ficha*, no como *no existen*: App Store ordena por "más útiles" y sesga hacia lo positivo.
