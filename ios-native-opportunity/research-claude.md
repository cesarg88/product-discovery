# iOS-Native Opportunity Discovery

> Investigación realizada el 21 de septiembre de 2026, una semana después del lanzamiento público de iOS 27 (14 de septiembre de 2026). Todas las afirmaciones sobre APIs se apoyan en documentación oficial de Apple, sesiones de WWDC25/WWDC26 o respuestas de DTS en los Apple Developer Forums; la evidencia de problema procede de fichas de App Store, foros y comunidades. Donde una afirmación es inferencia propia, se marca como tal.

> Nota de alcance: esta investigación excluye deliberadamente ideas centradas en HealthKit y en limpieza inteligente de fotos, que ya fueron exploradas y descartadas en la fase anterior de discovery. HealthKit aparece en el mapa de capacidades por completitud, pero ningún candidato depende de él.

---

## 1. Executive summary

**Lo que ha cambiado en el ecosistema y abre ventanas reales (2025–2026):**

1. **AlarmKit (iOS 26)** permite por primera vez a terceros crear alarmas de sistema que rompen Silencio y Focus, con Live Activity, Dynamic Island y Apple Watch. Antes solo lo podía hacer Reloj. Es la ventana más limpia de "esto era imposible hace 15 meses".
2. **Foundation Models (iOS 27)** ya no es un modelo pequeño de texto: acepta imágenes, expone herramientas de Vision (OCR, códigos de barras) al modelo, y ofrece un modelo grande en **Private Cloud Compute (32K tokens, razonamiento) sin coste de API** para apps del Small Business Program con menos de 2M de descargas. Esto elimina el backend de IA como coste marginal para un indie.
3. **Music Understanding (iOS 27)** entrega, on-device, key, ritmo (beats, compases, BPM), estructura (frases, secciones), pace, actividad instrumental y loudness. Antes esto exigía DSP propio o servidores. Pero **no funciona sobre streams de Apple Music** (confirmado por DTS): solo sobre assets a los que la app tiene acceso directo.
4. **App Intents (iOS 27)**: entity/intent schemas llevan el contenido de tu app al índice semántico de Spotlight y a Siri sin frases predefinidas. Los widgets se personalizan vía App Intents. Es un multiplicador de distribución dentro del sistema, no un producto.
5. **Core Location** con `CLMonitor`, `CLVisit` y sesiones de background sigue siendo la fuente pasiva de datos más infrautilizada por indies fuera del fitness.

**Lo que NO está disponible y mata ideas recurrentes:** FinanceKit es solo EE. UU./Reino Unido, exige cuenta de organización y categoría Finanzas; los datos de Screen Time están sellados dentro del `DeviceActivityReport` (no llegan a tu proceso); SensorKit es solo investigación con entitlement; no hay acceso a AirTags vía Nearby Interaction; HomeKit no permite ejecución en background, así que cualquier "histórico de sensores" exige un dispositivo siempre encendido; no hay API de historial de notificaciones, mensajes, llamadas, Mail ni Safari.

**Hallazgo transversal:** casi ningún gap "obvio" está vacío. Lo que hay son decenas de apps pequeñas que resuelven el job a medias: con entrada manual, con IA en la nube, con suscripción injustificada, o construidas antes de que Apple abriera la API relevante (p. ej. apps de alarma por calendario anteriores a AlarmKit que avisan "la app debe abrirse para encontrar eventos nuevos"). La oportunidad indie está en **hacerlo bien con la API nueva, on-device, con precio honesto y un job estrecho**, no en descubrir un nicho virgen.

**Final five (diversos a propósito):**

| # | Oportunidad | Palanca nativa | Por qué sobrevive |
|---|---|---|---|
| 1 | Despertador que se calcula desde tu primer evento + tiempo de viaje | AlarmKit + EventKit + MapKit ETA (+ WeatherKit) | Ventana AlarmKit; job universal; evidencia de Shortcuts caseros y apps pre-AlarmKit limitadas |
| 2 | Contador pasivo de días por país (Schengen 90/180, residencia fiscal, segunda vivienda) | Core Location (CLVisit/CLMonitor) + WidgetKit + Watch | Trigger externo duro: EES operativo desde abril 2026; WTP demostrada (suscripciones de 3,99 $/mes) |
| 3 | Registro automático de km para autónomos europeos, on-device y sin suscripción cara | Core Location + Core Motion + CarPlay (driving task) + Live Activities | Dinero recurrente demostrado; MileIQ subió un 50 % su precio en 2026; competidores EU pequeños |
| 4 | Convertir cualquier tarjeta/carnet/entrada en un pase de Wallet en 20 segundos | Vision (barcode + documento) + Foundation Models multimodal + PassKit | Pass2U está en el top-60 de ingresos de Compras (EE. UU.) con 4,3★; Apple sigue sin permitir crear pases manualmente |
| 5 | Herramienta de práctica musical/dance con beat grid, secciones y tonalidad automáticas sobre grabaciones propias | Music Understanding + AVFoundation + BGContinuedProcessingTask | API nueva sin equivalente on-device; nicho apasionado que ya paga (Anytune ~15 $, Moises ~36 $/año) |

**Recomendación de orden:** validar primero la #1 (MVP pequeño, cero backend, riesgo técnico acotado a re-planificación en background) y la #2 (evidencia de pago más dura). La #3 es la de mayor dinero pero la más competida; la #4 es un negocio pequeño y sano de pago único; la #5 es la más interesante técnicamente pero con la restricción DRM como techo.

---

## 2. Apple capability map

Estado verificado a septiembre de 2026 (iOS 26.x / iOS 27.0). Abreviaturas: **Hist.** = acceso a histórico; **P/A** = pasivo/activo; **BG** = funciona sin la app abierta; **Fricción** = fricción de permiso; **Indie** = idoneidad para un producto indie.

### 2.1 Datos personales y contexto

| Framework | Qué obtiene la app | Fuente del dato | Hist. | P/A | BG | Fricción | Entitlement | Hardware | Regional | Riesgo App Store | Indie |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **HealthKit** | Lectura/escritura por tipo: actividad, HR, sueño, entrenos, medicación (iOS 26), etc. | Histórico almacenado + Watch | Sí, ilimitado (según tipo) | Pasivo (Watch) | Sí: `HKObserverQuery` con background delivery | Media–alta (diálogo por tipo) | Capability estándar | Watch para la mayoría | Ninguna | Guideline 5.1.3: sin usos publicitarios; categoría saturada | Alta técnicamente; **excluido de esta investigación** |
| **WorkoutKit** | Componer y programar entrenos en Watch | App → sistema | No | Activo | Sí (programación) | Media (HealthKit) | Estándar | Watch | Ninguna | Bajo | Media (fitness) |
| **Core Motion** | Pasos, actividad (andar/correr/coche/bici), altímetro, sensores brutos, movimiento de AirPods | Sensor live + caché de 7 días (pedómetro y actividad) | 7 días | Pasivo (histórico) / activo (sensores) | Parcial: histórico sí; sensores solo con modos BG | Baja–media (Motion & Fitness) | Estándar | Barómetro en iPhone 6+; altitud absoluta iPhone 12+ | Ninguna | Bajo | Alta |
| **Journaling Suggestions** | Sugerencias: entrenos, fotos, visitas, contactos, música, podcasts, reflexiones, estado de ánimo | Inferencia del sistema | Solo lo que el usuario elige en el picker | **Activo**: el usuario debe abrir el picker y elegir | No | Baja (no hay diálogo global; el picker es el permiso) | Capability estándar | iPhone; iPad/Mac desde 26 | Ninguna conocida | Bajo | Media: no hay acceso programático masivo ni pasivo |
| **PhotoKit** | Biblioteca completa o limitada, metadatos, ubicación, fechas, álbumes | Histórico almacenado | Sí | Pasivo | Sí con `BGProcessingTask` | Media (acceso completo) | Estándar | — | Ninguna | Bajo | Alta; **limpieza de fotos excluida** |
| **EventKit (Calendar/Reminders)** | Eventos pasados y futuros de todos los calendarios del dispositivo, asistentes, ubicación, alarmas; recordatorios | Histórico almacenado | Sí (consultas por rangos de hasta 4 años) | Pasivo | Lectura sí; **notificación de cambios (`EKEventStoreChanged`) solo con la app viva** | Media (iOS 17: acceso completo vs solo escritura) | Estándar | — | Ninguna | Bajo | **Alta**: datos ricos, ya existentes, cero data entry |
| **Contacts** | Contactos completos o selección limitada (iOS 18) | Histórico | Sí | Pasivo | Sí | Media–alta | Estándar | — | Ninguna | 5.1.2: no compilar perfiles | Media |
| **Core Location** | Posición, `CLVisit` (llegadas/salidas), `CLMonitor` (geocercas y beacons), actualizaciones significativas, sesiones BG con indicador | Sensor live | No (la app debe almacenar) | Pasivo con "Siempre" | **Sí**, con permiso Siempre + modo BG | **Alta** (permiso Siempre en dos pasos) | Estándar | — | Ninguna | Bajo si el uso es claro | **Alta** |
| **MapKit** | Búsqueda, ETA (`MKDirections`), Look Around, Place IDs | Servicio Apple | — | — | Sí (peticiones desde BG task) | Ninguna | Estándar | — | Cobertura variable | Bajo | Alta; sin coste |
| **MusicKit / Apple Music API** | Catálogo, biblioteca, recientes, playlists; reproducción | Servicio Apple + biblioteca | Solo "recientes"; no hay scrobble histórico | Pasivo | Reproducción sí | Media (Media & Apple Music) | Estándar | — | Catálogo por país | Bajo | Media: sin PCM ni historial completo |

### 2.2 Mundo físico y sensores

| Framework | Qué obtiene la app | Fuente | Hist. | P/A | BG | Fricción | Entitlement | Hardware | Regional | Riesgo App Store | Indie |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **AVFoundation (cámara)** | Captura foto/vídeo, profundidad, Center Stage frontal (27) | Sensor live | No | Activo | No | Media | Estándar | Modelos | Ninguna | Bajo | Alta |
| **Vision** | Texto, documentos (`RecognizeDocumentsRequest`, 26), barcodes, poses, detección de mancha en lente (26), saliency | Inferencia on-device | — | Activo | Sí (procesado en BG task) | Ninguna adicional | Estándar | Neural Engine | Idiomas OCR | Bajo | **Alta** |
| **VisionKit** | `DataScannerViewController`, Live Text, escáner de documentos | Cámara + inferencia | — | Activo | No | Cámara | Estándar | — | — | Bajo | Alta |
| **Core NFC** | Lectura/escritura NDEF en primer plano; **lectura en background de tags NDEF con URL** (lanza la app vía universal link) | Tag externo | — | Activo (tap) | Parcial (background tag reading, iPhone XS+) | Baja | Estándar; ISO 7816/HCE requieren entitlements específicos | iPhone 7+ (lectura), XS+ (BG) | HCE limitado a ciertas regiones | Bajo | Alta para logs/triggers; **Shortcuts ya ofrece automatizaciones NFC gratis** |
| **Core Bluetooth** | Periféricos BLE (GATT), BG con periféricos conectados | Accesorio | — | Activo/pasivo | Sí (modos BG) | Baja–media | Estándar | Accesorio | — | Bajo | Media (depende de accesorio) |
| **Nearby Interaction (UWB)** | Distancia/dirección a otros iPhones o accesorios U1/U2 de terceros | Sensor | — | Activo | No | Media | Estándar | iPhone 11+, accesorio UWB | UWB restringido en algunos países | Bajo | **Baja**: sin acceso a AirTags |
| **HomeKit** | Leer/controlar accesorios, escenas, automatizaciones | Hub/accesorios | **No hay histórico** | Pasivo | **No hay ejecución en BG** (solo notificaciones de característica con la app viva) | Alta | Capability estándar | Home hub | — | Bajo | **Baja–media**: el histórico exige un dispositivo dedicado siempre encendido (así lo hace Controller for HomeKit con su "Hub") |
| **Matter (MatterSupport)** | Onboarding de accesorios Matter a ecosistemas | Accesorio | — | Activo | No | Media | Entitlement estándar | — | — | Bajo | Baja |
| **Barómetro / acelerómetro / giroscopio / magnetómetro / pedómetro** | Vía Core Motion (`CMAltimeter`, `CMMotionManager`, `CMPedometer`) | Sensor | Pedómetro 7 días | — | Solo con modo BG | Baja | Estándar | — | — | Bajo | Alta |
| **AccessorySetupKit / Wi-Fi Aware (26)** | Emparejamiento simplificado y comunicación directa con accesorios | Accesorio | — | Activo | Parcial | Baja | Estándar | Accesorio | — | Bajo | Baja (requiere hardware propio o de partner) |
| **RoomPlan / ARKit** | Escaneo 3D de habitaciones, plano | LiDAR | — | Activo | No | Cámara | Estándar | **Modelos Pro** | — | Bajo | Media |

### 2.3 Audio

| Framework | Qué obtiene la app | Fuente | Hist. | P/A | BG | Fricción | Entitlement | Hardware | Regional | Riesgo | Indie |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Speech (`SpeechAnalyzer`/`SpeechTranscriber`, 26)** | Transcripción on-device rápida, con marcas de tiempo | Micro/archivo | — | Activo | Con modo audio BG | Media (micro + reconocimiento) | Estándar | Modelos recientes para on-device | Idiomas | Bajo | Alta |
| **Sound Analysis** | Clasificador de 300+ sonidos + modelos Core ML propios | Micro/archivo | — | Activo | Con modo audio BG | Media | Estándar | — | — | Bajo | Media (Apple ya ofrece Reconocimiento de sonidos como accesibilidad con automatizaciones) |
| **ShazamKit** | Identificación contra catálogo Shazam o catálogos propios | Micro + servicio Apple | — | Activo | No | Media | Estándar | — | — | Bajo | Baja–media |
| **Music Understanding (27)** | Key, ritmo (beats/compases/BPM), estructura (frases/secciones), pace, actividad instrumental, loudness; time-stamped; on-device | Asset de audio (`AVAsset` o buffers PCM propios) | — | Activo | Sí (procesado largo con `BGContinuedProcessingTask`) | Ninguna adicional | Estándar | Neural Engine | Ninguna | Bajo | **Alta con techo**: **no funciona con streams/descargas de Apple Music (DRM)**, confirmado por DTS |
| **NowPlaying (27)** | Integración de tu reproductor con Lock Screen, Control Center, Dynamic Island, CarPlay | App | — | — | Sí | Ninguna | Estándar | — | — | Bajo | Alta (habilitador) |

### 2.4 Inteligencia local

| Framework | Qué obtiene la app | Fuente | Hist. | P/A | BG | Fricción | Entitlement | Hardware | Regional | Riesgo | Indie |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **Foundation Models (26 → 27)** | 26: modelo on-device ~3B, ~4K tokens, guided generation, tools, streaming. **27**: modelo on-device reconstruido, **entrada de imágenes**, herramientas Vision (OCR/barcode) para el modelo, Dynamic Profiles, búsqueda semántica integrada, **`PrivateCloudComputeLanguageModel` (32K, razonamiento)**, protocolo `LanguageModel` para Claude/Gemini/MLX/Core AI, Evaluations framework | Inferencia on-device / PCC | — | Activo | Sí (BG task) | **Ninguna** para on-device | On-device: estándar. **PCC: entitlement `com.apple.developer.private-cloud-compute`**, gratis con Small Business Program y <2M descargas | Dispositivos Apple Intelligence (iPhone 15 Pro / 16 en adelante) | Idiomas/regiones de Apple Intelligence | Bajo (guías sobre IA en el acuerdo actualizado) | **Alta**: elimina el servidor de IA |
| **Core AI (27)** | Ejecutar modelos propios on-device con API Swift, especialización por hardware | On-device | — | — | Sí | Ninguna | Estándar | Apple Silicon | — | Bajo | Media (para quien ya tiene modelos) |
| **Core ML / Create ML** | Modelos propios | On-device | — | — | Sí | Ninguna | Estándar | — | — | Bajo | Alta |
| **Natural Language** | Tokenización, entidades, sentimiento, embeddings contextuales | On-device | — | — | Sí | Ninguna | Estándar | — | Idiomas | Bajo | Alta |
| **App Intents (26 → 27)** | Acciones/entidades para Shortcuts, Siri, Spotlight, Focus filters, Controls, widgets. **27**: entity/intent schemas → índice semántico de Spotlight y Siri; View Annotations; App Intents Testing. **26**: integración con Visual Intelligence (`IntentValueQuery`) | App | — | — | Sí | Ninguna | Estándar | — | Idiomas de Siri | Bajo | **Alta (habilitador de distribución)** |

### 2.5 Surfaces del sistema

| Framework | Qué obtiene la app | BG | Fricción | Entitlement | Hardware | Riesgo | Indie |
|---|---|---|---|---|---|---|---|
| **WidgetKit** | Widgets Home/Lock/StandBy/Watch; interactivos (17); **Controls** en Control Center y Action button (18); **personalización vía App Intents y estilos dinámicos (27)**; RelevanceKit para Smart Stack de Watch (26) | Timelines refrescadas por el sistema (presupuesto) | Ninguna | Estándar | — | Bajo | Alta |
| **ActivityKit (Live Activities)** | Lock Screen, Dynamic Island, StandBy; **Watch Smart Stack y CarPlay (26)**; actualizaciones locales (app viva/BG) o por push (requiere servidor) | Parcial | Ninguna | Estándar | — | Bajo | Alta si no necesita push |
| **AlarmKit (26)** | Alarmas y temporizadores de sistema: rompen Silencio y Focus, Live Activity de cuenta atrás, snooze, botón custom con App Intent, StandBy y Watch; programación fija o relativa (repetición semanal) | **Sí**: el sistema dispara la alarma; la app no necesita estar viva | Media (diálogo `NSAlarmKitUsageDescription`) | Estándar | iOS 26+ | Bajo | **Alta (ventana nueva)**. Límite: la alarma es un instante fijo; recalcularla exige que la app corra (BG task, apertura) |
| **UserNotifications** | Locales, time-sensitive; **Critical Alerts requiere entitlement raro** | Sí | Baja | Estándar / especial | — | Bajo | Alta |
| **BackgroundTasks** | `BGAppRefreshTask` (oportunista, no garantizado), `BGProcessingTask`, **`BGContinuedProcessingTask` (26)** para continuar trabajo largo iniciado por el usuario con progreso visible | Sí | Ninguna | Estándar | — | Bajo | Alta |
| **Share / Action extensions, Core Spotlight** | Entrada desde otras apps; indexación (27: "LLM search using Core Spotlight") | — | Ninguna | Estándar | — | Bajo | Alta |
| **WeatherKit** | Condiciones, previsiones horarias/diarias, alertas; 500K llamadas/mes incluidas en el Developer Program; cobertura variable por región | Sí | Ninguna (atribución obligatoria) | Estándar | — | Bajo | Alta |

### 2.6 Capacidades restringidas (investigadas expresamente)

| Framework | Realidad en 2026 | Veredicto indie |
|---|---|---|
| **FamilyControls / DeviceActivity / ManagedSettings** | Entitlement de distribución solicitado a Apple, **por bundle ID incluyendo cada extensión** (Monitor, Report, Shield); colas de semanas documentadas en los foros. Los datos de uso solo se renderizan dentro del `DeviceActivityReport` en un sandbox que **no puede pasar datos a la app** (DTS confirma que es por diseño). Tokens opacos, no bundle IDs | Viable solo para bloqueadores (categoría saturada: Opal, one sec, Brick, Foqos open source). **Imposible** para analítica personal de pantalla |
| **FinanceKit** | Apple Card/Cash/Savings en **EE. UU.**; open banking en **Reino Unido** (iOS 18.4+). Entitlement gestionado, **solo cuentas de organización**, app en categoría Finanzas, distribuida en US/UK | **Descartado** para un fundador en España |
| **PassKit / Wallet** | Añadir pases `.pkpass` firmados con certificado Pass Type ID (la firma puede hacerse en servidor mínimo o embebiendo el certificado, con riesgo); seguimiento de pedidos; **IdentityDocumentServices (26)** para verificación de identidad, EE. UU. | Alta para creación de pases; baja para identidad |
| **SensorKit** | Entitlement solo para estudios de investigación con IRB | **Descartado** |
| **Nearby Interaction con AirTag** | No existe API pública | **Descartado** |
| **Notificaciones de otras apps, iMessage/SMS, WhatsApp, Mail, historial de llamadas, Safari** | Sin API pública (CallKit permite bloqueo/identificación, no historial; IdentityLookup filtra SMS de desconocidos sin exponer historial) | **Descartado** |
| **EnergyKit (26)** | Previsiones de red eléctrica para cargar en horas limpias; utilities limitadas en EE. UU. | Descartado por región |

---

## 3. Particularly interesting or underused capabilities

1. **AlarmKit (iOS 26).** La única forma pública de alertar rompiendo Silencio/Focus sin el entitlement de Critical Alerts. Su limitación central es también su oportunidad: una alarma es un instante fijo, así que cualquier producto cuya alarma dependa de datos cambiantes (calendario, tráfico, tiempo) tiene que resolver bien la **re-planificación** (BG refresh + recálculo al abrir + widget). Los primeros entrantes (Unmissable, VariAlarm, Shift Worker Calendar & Alarm) son apps de un desarrollador con pocas reseñas; Supershift ya absorbió el caso "alarma por turno".

2. **Foundation Models con Private Cloud Compute gratis (iOS 27).** Para un indie del Small Business Program, el coste marginal de IA seria (32K, razonamiento, imágenes) es cero. Esto convierte "extracción estructurada de una foto de un documento" en una función barata y privada, sin servidor. La contrapartida: exige entitlement (cola de aprobación abierta) y dispositivos Apple Intelligence.

3. **Music Understanding (iOS 27).** Beat grid, compases, frases y secciones con timestamps, on-device. Es exactamente la capa que Moises vende en la nube. El techo es duro y está confirmado por Apple: no sobre Apple Music. Funciona sobre grabaciones propias, compras DRM-free, importaciones y audio del propio usuario (ensayos, clases, coreografías).

4. **App Intents schemas → Spotlight semántico y Siri (iOS 27).** Cualquier app pequeña puede hacer que "sus cosas" aparezcan en Siri con atribución. Es la primera vez que una app indie puede ganar distribución *dentro* del sistema sin que el usuario la abra. No es un producto; es lo que puede hacer que un producto pequeño se sienta parte del sistema.

5. **`CLVisit` + `CLMonitor` + `CLBackgroundActivitySession`.** Detección pasiva de "estuve en X" con bajo consumo. Fuera del fitness y del mileage, apenas hay productos de consumo construidos sobre esto en el App Store europeo.

6. **`BGContinuedProcessingTask` (iOS 26).** Permite que un análisis largo iniciado por el usuario (procesar 200 grabaciones con Music Understanding, OCR de 50 documentos) continúe en background con progreso visible. Habilita productos on-device que antes exigían servidor por pura ergonomía.

7. **Visual Intelligence app integration (iOS 26).** Con `IntentValueQuery` una app puede aparecer como resultado cuando el usuario apunta la cámara o hace captura. Poco explotado por indies porque exige tener contenido/catálogo propio.

**Capacidades que investigué y donde NO veo oportunidad indie ahora:** Journaling Suggestions (solo picker; Apple Journal ya hace el resumen), HomeKit (sin BG ni histórico), Nearby Interaction (sin AirTags), FinanceKit (región/organización), SensorKit (investigación), ShazamKit custom catalogs (dos lados: venues + usuarios), Sound Analysis para electrodomésticos (Apple ya lo resuelve con Reconocimiento de sonidos + automatizaciones).

---

## 4. Problems and signals found in the wild

Señales reales encontradas (con URL). Se distingue **evidencia** (texto de usuarios, fichas, reviews) de **inferencia**.

| Señal | Tipo | Fuente |
|---|---|---|
| Usuarios construyen Shortcuts para "poner una alarma antes del siguiente evento del calendario" | Evidencia (Shortcut casero) | https://www.goodreads.com/author_blog_posts/22144390-hey-siri-let-s-nap |
| Script de Google Apps + MacroDroid para sincronizar alarma matinal con eventos de calendario (Android) | Evidencia (ugly workflow) | https://github.com/bsodium/alarm-calendar-sync |
| App de pago "Calarm" (1,99 $) que despierta antes del primer evento, pero advierte "App must be opened to find new calendar events" (limitación pre-AlarmKit) | Evidencia (competidor + limitación) | https://apps.apple.com/app/id509840570 |
| Apps recién nacidas sobre AlarmKit: Unmissable, VariAlarm, Never Forget Alarm, Shift Worker Calendar & Alarm (requiere iOS 26.1) | Evidencia (entrada de mercado 2025–2026) | https://apps.apple.com/us/app/-/id6752518796 · https://apps.apple.com/app/id6757322888 · https://apps.apple.com/us/app/shift-worker-calendar-alarm/id6759396502 |
| Supershift añade "Smart Shift Alarms" ("Stop setting alarms manually every Sunday night") | Evidencia (incumbente absorbe el job de turnos) | https://apps.apple.com/us/app/supershift-shift-calendar/id1104165041 |
| r/shortcuts: usuario monta con tags NFC un "days since I last watered the plant" usando Reminders/Notes como base de datos | Evidencia (ugly workflow) | https://lr.ggtyler.dev/r/shortcuts/comments/1f1zuei/building_a_days_since_last_time_of_watering_plant |
| Spreadsheet público para contar días de oficina vs casa con umbrales 40 %/60 % | Evidencia (spreadsheet) | https://github.com/RogerHowellDfE/Office-Work-Tracker |
| Blind: empresas con dashboard de cumplimiento RTO de 3 días; "they check your badging history" | Evidencia (trigger externo) | https://www.teamblind.com/post/whats-micron-current-rto-policy-lb63rsvl |
| Apps manuales de "office days": Lanyard (1,99 $, 31 valoraciones), HybridWorkTracker, Office Attendance, Where I Worked Today (0,99 $) | Evidencia (demanda modesta, WTP baja) | https://apps.apple.com/us/app/id6455731792 · https://apps.apple.com/app/id6755990197 |
| EES operativo en todas las fronteras Schengen desde el 9–10 de abril de 2026; prensa balear advierte de "trampa" para propietarios británicos de segunda vivienda | Evidencia (trigger legal) | https://amp.majorcadailybulletin.com/news/local/2025/10/14/137267/spain-travel-how-avoid-the-new-european-union-entry-and-exit-scheme.html · https://www.mallorca.com/es/consejos/vivir-en-mallorca/visado-residencia/regla-90-180-dias-espana |
| Apps de conteo de días con suscripción: TrackingDays (3,99 $/mes, desde 2013), Staywise, Days Monitor, Tax Residency Tracker, Days of Stay | Evidencia (WTP + competencia) | https://apps.apple.com/us/app/trackingdays/id657769643 · https://apps.apple.com/us/app/staywise-country-days-tracker/id6749697652 · https://taxresidencytracker.com/ |
| MileIQ subió de 5,99 $ a 8,99 $/mes en 2026; usuarios buscan alternativas | Evidencia (precio + churn) | https://www.triplog.net/es/blog/mileiq-alternatives · https://sparkreceipt.com/es-us/blog/mejores-apps-registrar-millas/ |
| Apps EU on-device: Magica (14,99 $/año, "sin servidores"), Fahrtenbuch (GoBD alemán, CarPlay) | Evidencia (competidores locales) | https://apps.apple.com/us/app/-/id1341304115 · https://mwm.ai/es/apps/fahrtenbuch/286070473 |
| Pass2U Wallet: 2,8K reviews, 4,3★, #60 top-grossing Shopping (US, mar-2026); review: "it asked me to create an account… I no longer had the ability to edit my previous cards" | Evidencia (WTP + fricción) | https://apppricinglab.com/app/apple/1142473931 · https://apps.apple.com/us/app/pass2u-wallet-create-and-put-cards-into-wallet/id1142473931 |
| "Apple doesn't let you manually add passes to Wallet… Unlike Google Wallet" | Evidencia (gap Apple) | https://walletwallet.alen.ro/blog/create-apple-wallet-pass-free/ |
| DTS: Music Understanding no puede analizar streams de Apple Music; djay documenta que ningún tercero puede cargar pistas de Apple Music | Evidencia (restricción) | https://developer.apple.com/forums/thread/829763 · https://help.algoriddim.com/topic/music-streaming/drm-protected-songs |
| Moises vende "Sections" (secciones automáticas) como función Premium en la nube; Anytune exige marcar secciones a mano; Anytune Pro ~15 $ pago único | Evidencia (competencia y precios) | https://moises.ai/blog/moises-news/new-song-sections-feature/ · https://www.songscription.ai/blog/best-apps-to-slow-down-music |
| Apps de "analítica de calendario" pequeñas y antiguas: Timeview, Calendar Statistics, Calendar Insights; Calendar.com añade analítica de personas | Evidencia (demanda tibia) | https://apps.apple.com/us/app/timeview-calendar-statistics/id1439197028 · https://www.calendar.com/analytics/ |
| Controller for HomeKit: "Without a Controller Hub, there is no continuous history" | Evidencia (restricción HomeKit) | https://controllerforhomekit.com/features/charts |
| Google movió Timeline a on-device (jun-2025) borrando historial >90 días para muchos; Arc Timeline cobra 4,99 $/mes o 179,99 $ lifetime (427 valoraciones) | Evidencia (demanda + WTP) | https://tech.yahoo.com/general/articles/google-puts-date-maps-timelines-230941507.html · https://apps.apple.com/us/app/arc-timeline-trips-places/id1063151918 |
| Decenas de apps "photo/PDF → calendar" con IA en la nube, suscripción y 2,6–3,0★ | Evidencia (categoría llena de wrappers) | https://apps.apple.com/app/id6746355733 · https://alternativeto.net/software/piccal-calendar-scanner/ |
| Foros Apple: desarrolladores intentando sacar el total de Screen Time del `DeviceActivityReport` sin éxito ("Is Screen Time trapped… on purpose?") | Evidencia (restricción) | https://developer.apple.com/forums/tags/family-controls?page=5 |
| Brick (59 $, hardware NFC) genera clones software con tags baratos; Foqos gratis y open source (500+ stars) | Evidencia (saturación) | https://www.bgr.com/2235201/phone-blocking-app-brick-alternatives/ · https://gittrend.io/repo/awaseem/foqos |

**Patrones observados:**
- Los ugly workflows más frecuentes son **Shortcuts + Notes/Reminders como base de datos** (NFC, alarmas por calendario) y **spreadsheets de conteo de días** (oficina, países).
- Cuando Apple abre una API (AlarmKit), en 12 meses aparecen 3–6 apps de un desarrollador con <50 reseñas y un incumbente de la categoría adyacente que absorbe el caso principal. La ventana existe pero es corta y hay que entrar con el job mejor definido, no con la API.
- Las categorías con IA "foto → X" están inundadas de wrappers en la nube con suscripción y malas valoraciones: la oportunidad está en on-device + pago único + un job estrecho, no en "otra app de IA".

---

## 5. Fifteen candidate opportunities

Formato común: Usuario · Problema · Current workaround · Evidencia · Native Apple leverage · What already exists · Why Apple doesn't solve it · Why an indie could compete · Data entry · Time-to-value · Backend · Third-party dependency · Monetization hypothesis · MVP · Solo-dev feasibility · MVP scope · "Would I personally understand this product?"

### Candidate 1 — El despertador se calcula solo desde el primer evento y el tiempo de viaje

- **Usuario:** cualquier persona cuyo primer compromiso del día cambia (reuniones tempranas, vuelos, clases, guardias) y que hoy reajusta la alarma a mano cada noche.
- **Problema:** "Cada noche miro el calendario, calculo cuánto tardo en llegar y muevo la alarma; si el evento cambia, la alarma no."
- **Current workaround:** alarma fija + ajuste manual; Shortcuts caseros que leen el siguiente evento y crean una alarma en Reloj; Sleep Schedule de Apple con hora fija.
- **Evidencia:** Shortcut "Hey Siri, Let's nap" que crea alarma antes del siguiente evento (goodreads.com/author_blog_posts/22144390); script Google Apps + MacroDroid (github.com/bsodium/alarm-calendar-sync); Calarm (1,99 $) con la limitación explícita "App must be opened to find new calendar events"; entrada de apps AlarmKit en 2025–26 (Unmissable, VariAlarm). **Inferencia:** el volumen de apps nuevas sugiere que varios desarrolladores han detectado el mismo hueco tras AlarmKit.
- **Native Apple leverage:** `AlarmKit` (alarma de sistema que rompe Silencio/Focus, Watch, StandBy) + `EventKit` (primer evento con ubicación) + `MapKit MKDirections` (ETA a la hora prevista) + `WeatherKit` (opcional: margen extra si llueve/nieva) + `BackgroundTasks` para re-planificar + `WidgetKit` (mostrar "mañana suenas a las 6:40 por X").
- **What already exists:** Calarm (1,99 $, pre-AlarmKit, "designed for iPad", exige abrir la app); Unmissable (AlarmKit, alarma *en el evento*, no despertador con viaje; freemium); VariAlarm (plantillas + Shortcuts; freemium); Supershift (alarma por tipo de turno; suscripción; solo turnos definidos en la propia app); Alarmy/Sleep Cycle (no leen calendario). Google/Pixel ofrece "Bedtime" con primer evento, no en iOS.
- **Why Apple doesn't already solve it:** Sleep Schedule usa horas fijas por día de la semana; Calendar ofrece "Time to Leave" como notificación, no como alarma; Reloj no lee calendarios.
- **Why an indie could compete:** job estrecho ("dime a qué hora sonar mañana y por qué"), cross-framework (Calendar × Maps × AlarmKit), cero cuenta, cero servidor, nicho demasiado pequeño para Apple pero universal.
- **Data entry:** **Nulo** (elige calendarios, hora de preparación y hora mínima/máxima una vez).
- **Time-to-value:** **primer día** (la primera noche ya muestra la hora calculada y por qué).
- **Backend requirement:** **Ninguno**.
- **Third-party dependency:** **Baja** (calendarios de Google/Exchange llegan vía EventKit).
- **Monetization hypothesis:** pago único (5–8 €) o lifetime unlock; comparables cobran (Calarm 1,99 $, Supershift suscripción). Sin evidencia de WTP para suscripción en este job.
- **MVP:** (1) permiso Calendar + AlarmKit; (2) regla: primer evento de mañana − ETA − preparación, con topes; (3) programación nocturna vía BGAppRefresh + recálculo al abrir + Live Activity de "próxima alarma"; (4) widget con hora y motivo; (5) día sin eventos → alarma por defecto o ninguna.
- **Solo-developer feasibility:** **Alta**.
- **Estimated MVP scope:** **pequeño**.
- **Would I personally understand this product?** **Alta**: el fundador es el usuario.
- **Riesgo técnico clave:** `BGAppRefreshTask` no está garantizado; si el usuario mueve la reunión a las 23:30 y no abre la app, la alarma puede quedar desactualizada. Mitigación: programar siempre una alarma "conservadora" la noche anterior y refinarla; mostrar en widget/Live Activity la hora vigente; ofrecer "revisar" con un tap. Hay que validar la fiabilidad real del refresh nocturno en dispositivos reales durante semanas.

### Candidate 2 — Contador pasivo de días en la oficina (hybrid work / RTO)

- **Usuario:** empleado híbrido con cuota de días presenciales (3/semana, 8/mes, 50 %/trimestre).
- **Problema:** "No sé cuántos días de oficina me faltan este mes y lo llevo en una hoja."
- **Current workaround:** spreadsheet (github.com/RogerHowellDfE/Office-Work-Tracker), apps de marcado manual, mirar el dashboard de RR. HH. de la empresa.
- **Evidencia:** spreadsheet público con umbrales 40 %/60 %; Blind sobre dashboards de cumplimiento y "badging history"; 4–5 apps manuales con pocas valoraciones (Lanyard 1,99 $/31 valoraciones; Where I Worked Today 0,99 $; Hybrid Office Tracker con "optional location detection").
- **Native Apple leverage:** `CLMonitor` (geocerca de la oficina) + `CLVisit` (confirmación de estancia) + `WidgetKit` (progreso del mes) + `EventKit` (festivos/vacaciones como excepciones) + Watch complication.
- **What already exists:** ver arriba; todas manuales o con localización opcional y UX pobre; ninguna con tracción visible.
- **Why Apple doesn't already solve it:** no existe el concepto "cuota de presencia" en el sistema; Screen Time/Health no aplican.
- **Why an indie could compete:** una métrica, un usuario, cero entrada; explicable en una frase.
- **Data entry:** **Nulo** tras marcar la oficina en el mapa.
- **Time-to-value:** **primer día de oficina**.
- **Backend requirement:** **Ninguno**.
- **Third-party dependency:** **Baja**.
- **Monetization hypothesis:** pago único bajo (2–4 €); los comparables cobran 0,99–1,99 $. **Sin evidencia** de WTP superior.
- **MVP:** (1) marcar oficina(s); (2) permiso Siempre + geocerca; (3) regla de cuota (semana/mes/trimestre, %); (4) widget; (5) exportar CSV.
- **Solo-developer feasibility:** **Alta**. **MVP scope:** **pequeño**.
- **Would I personally understand this product?** **Alta**.
- **Debilidad principal:** WTP baja y el empleador ya tiene la "verdad" (fichajes). Valor real: planificación personal, no prueba. Comparte motor con el Candidate 3.

### Candidate 3 — Contador pasivo de días por país (Schengen 90/180, residencia fiscal, segunda vivienda)

- **Usuario:** británicos y otros no-UE con segunda vivienda en España/Portugal/Francia; nómadas digitales; expatriados que deben demostrar días (183, UK SRT, 90/180).
- **Problema:** "Tengo que saber cuántos días me quedan en Schengen en esta ventana de 180 y no me puedo equivocar."
- **Current workaround:** spreadsheet, calculadoras web de Schengen, sellos de pasaporte (que desaparecen con EES), apps manuales.
- **Evidencia:** EES operativo en toda Schengen desde abril de 2026, con fin del sellado y control algorítmico (mallorca.com; Majorca Daily Bulletin: "very nasty trap for British… second home owners"); TrackingDays cobra 3,99 $/mes desde 2013 y lista explícitamente "Snowbirds and overseas homeowners"; 4+ apps nuevas en 2025–26 con tracking automático (Staywise, Days Monitor, Tax Residency Tracker, Days of Stay).
- **Native Apple leverage:** `CLVisit` + actualizaciones significativas (bajo consumo) + reverse-geocoding on-device del país + `WidgetKit`/Watch ("87/90 · próximo reset 12 nov") + `UserNotifications` (aviso a 80 días) + exportación PDF firmada con fechas.
- **What already exists:** TrackingDays (veterana, suscripción mensual, UI anticuada), Staywise (2025, "battery-friendly", guarda solo países), Tax Residency Tracker (2025, freemium, modos de conteo), Days Monitor, Days of Stay. **Competencia real y reciente.**
- **Why Apple doesn't already solve it:** Significant Locations es privado y no exportable; Apple no entra en compliance legal.
- **Why an indie could compete:** los competidores son genéricos ("todas las reglas del mundo"); espacio para un producto **excelente en un caso** (p. ej. segunda vivienda británica en España tras EES: widget, Watch, reglas 90/180 + 183 fiscal + aviso de ventana móvil) con distribución en comunidades muy concretas. Privacidad on-device como argumento (los datos de ubicación de compliance son sensibles).
- **Data entry:** **Nulo/Bajo** (importar viajes pasados a mano la primera vez).
- **Time-to-value:** **inmediato** si importa el histórico; **primera semana** si empieza de cero.
- **Backend requirement:** **Ninguno**.
- **Third-party dependency:** **Baja**.
- **Monetization hypothesis:** suscripción anual moderada o lifetime; evidencia de pago clara (3,99 $/mes en TrackingDays).
- **MVP:** (1) permiso Siempre + detección de país por visitas; (2) regla 90/180 móvil con proyección; (3) importación manual de viajes previos; (4) widget + notificación de umbral; (5) exportar informe PDF.
- **Solo-developer feasibility:** **Alta**. **MVP scope:** **pequeño–medio** (la lógica de ventanas móviles y bordes de medianoche/zona horaria exige tests serios).
- **Would I personally understand this product?** **Media–alta**: el conteo es simple; la interpretación legal (día de llegada cuenta, tránsito, medianoche) exige leer las reglas, pero **no** convertirse en asesor fiscal. El producto debe contar, no aconsejar.
- **Riesgo:** detección pasiva de cruces de frontera terrestres poco fiable con visitas; un error de un día tiene coste legal para el usuario → necesita revisión/edición fácil y disclaimers.

### Candidate 4 — "¿A dónde se van mis horas?" Auditoría del calendario

- **Usuario:** profesional con calendario denso (ingeniería, gestión) que quiere saber horas en reuniones, con quién, y cuánto tiempo de foco le queda.
- **Problema:** "Siento que vivo en reuniones pero no tengo el número."
- **Current workaround:** contar a mano, Clockwise/Reclaim (Google Calendar, web), Timing en Mac.
- **Evidencia:** Timeview ("EXACTLY what I needed… how many hours are already booked"), Calendar Statistics (2011, aún vendida), Calendar Insights (2025), Calendar.com añade "People Analytics". Apple Support Communities: usuario pregunta si Calendar suma horas por actividad; respuesta: no.
- **Native Apple leverage:** `EventKit` (histórico de años, asistentes, duración) + `Contacts` (mapear asistentes) + `Foundation Models` on-device (clasificar títulos de eventos en categorías) + `WidgetKit` (horas de reunión esta semana) + `App Intents` (Siri: "¿cuántas horas de reunión tengo mañana?").
- **What already exists:** ver evidencia; apps pequeñas, antiguas, sin analítica de personas ni categorización inteligente.
- **Why Apple doesn't already solve it:** Calendar es un visor; Screen Time mide pantalla, no tiempo humano.
- **Why an indie could compete:** datos ya existen (años de histórico → valor inmediato); categorización on-device es nueva; una métrica clara.
- **Data entry:** **Nulo**.
- **Time-to-value:** **inmediato** (abre y ve el año).
- **Backend requirement:** **Ninguno**. **Third-party dependency:** **Baja**.
- **Monetization hypothesis:** pago único; comparables 2–5 $. **WTP dudosa**: el "aha" es fuerte una vez y débil semanalmente.
- **MVP:** (1) permiso Calendar; (2) horas/reuniones por semana/mes con tendencia; (3) top personas; (4) categorización automática con corrección manual; (5) widget semanal.
- **Solo-developer feasibility:** **Alta**. **MVP scope:** **pequeño**.
- **Would I personally understand this product?** **Alta**.
- **Debilidad:** frecuencia de uso baja; riesgo de "producto-curiosidad".

### Candidate 5 — Histórico y gráficas de sensores HomeKit

- **Usuario:** usuario de Apple Home con sensores de temperatura/humedad/calidad de aire que quiere ver tendencias.
- **Problema:** "Home me enseña el valor de ahora; quiero ver la noche entera."
- **Current workaround:** Eve app (solo dispositivos Eve), Controller for HomeKit con "Controller Hub" (dispositivo dedicado), Home Assistant.
- **Evidencia:** Controller for HomeKit: "Without a Controller Hub, there is no continuous history for Charts"; comunidades Homebridge implementan históricos "FakeGato" solo visibles en Eve.
- **Native Apple leverage:** `HomeKit` + `Swift Charts`.
- **What already exists:** Controller for HomeKit (suscripción, hub), Home+ (pago único), Eve.
- **Why Apple doesn't already solve it:** Home no almacena histórico para terceros.
- **Why an indie could compete:** no puede sin dispositivo dedicado: **la plataforma no permite ejecución en background de apps HomeKit**, así que el logging continuo exige un iPad/Apple TV/Mac siempre encendido corriendo tu app (o backend propio conectado a un hub, que HomeKit no ofrece).
- **Data entry:** Nulo. **Time-to-value:** días. **Backend:** Ninguno pero **hardware dedicado**. **Dependency:** Baja.
- **Monetization hypothesis:** pago único (Home+ ~15 €).
- **MVP / feasibility / scope:** no relevante: **descartado por restricción de plataforma** (ver sección 6).
- **Would I personally understand this product?** Media.

### Candidate 6 — Práctica musical y de baile con beat grid, secciones y tonalidad automáticas sobre grabaciones propias

- **Usuario:** músicos que aprenden canciones de oído, bandas que graban ensayos, profesores y alumnos de baile que cuentan "ochos" sobre su música.
- **Problema:** "Quiero saltar al estribillo, repetir el compás 33–36 al 70 % y saber la tonalidad, sin marcar todo a mano."
- **Current workaround:** Anytune (marcar secciones manualmente), Moises (sube el audio a la nube; Sections es Premium), Amazing Slow Downer, GarageBand.
- **Evidencia:** Moises vende Sections como diferenciador Premium; reviews destacan "Song Sections… game-changer"; Anytune Pro ~15 $ pago único con secciones manuales; PracticeSession (39 $) presume de "auto-generate regions" desde Guitar Pro porque el audio no se lo permite.
- **Native Apple leverage:** `MusicUnderstanding` (beats, compases, frases, secciones, key, loudness, on-device) + `AVFoundation` (time-stretch con `AVAudioUnitTimePitch`) + `BGContinuedProcessingTask` (analizar una biblioteca de ensayos) + `WidgetKit`/Live Activity (loop actual) + `Files`/Share extension para importar.
- **What already exists:** Anytune (iOS/macOS, pago único, muy consolidada), Moises (suscripción 3,99 $/mes, nube, stems), Capo (suscripción), AudioStretch. **Ninguna** puede analizar Apple Music tampoco.
- **Why Apple doesn't already solve it:** Music/GarageBand no ofrecen práctica por secciones; Apple publica el framework para que terceros lo hagan.
- **Why an indie could compete:** la parte difícil (análisis) la regala el sistema; offline y privado; pago único frente a suscripción; posible foco en **baile** (conteo de 8, marcadores por frase), que las apps de músicos no atienden.
- **Data entry:** **Bajo** (importar archivo).
- **Time-to-value:** **inmediato** (analiza y muestra secciones en segundos).
- **Backend requirement:** **Ninguno**. **Third-party dependency:** **Baja**.
- **Monetization hypothesis:** pago único 10–20 € (Anytune) o freemium por número de canciones.
- **MVP:** (1) importar audio (Files/Share); (2) análisis MU → beat grid, secciones, key; (3) loop por sección/compás con tempo; (4) marcadores editables; (5) procesado en background de varias pistas.
- **Solo-developer feasibility:** **Alta**. **MVP scope:** **medio** (UI de forma de onda y transporte de audio de calidad).
- **Would I personally understand this product?** **Media**: depende de si el fundador toca o baila; si no, hay que reclutar 3–5 usuarios expertos desde el día uno.
- **Techo:** iOS 27+ y sin Apple Music. El usuario tiene que tener el archivo.

### Candidate 7 — Registro automático de kilómetros para autónomos y profesionales europeos, on-device

- **Usuario:** autónomos, comerciales, sanitarios a domicilio, técnicos; en España, quien deduce desplazamientos (0,26 €/km exento en empleados; gastos reales en autónomos).
- **Problema:** "Tengo que justificar cada desplazamiento con fecha, origen, destino, km y motivo, y no lo hago."
- **Current workaround:** libreta, Excel, MileIQ (EE. UU.-céntrico, 8,99 $/mes), apps locales.
- **Evidencia:** MileIQ +50 % de precio en 2026 y artículos de "alternativas"; TripLog responde con automático gratis; Magica (14,99 $/año, on-device) y Fahrtenbuch (GoBD alemán) existen; guías de tarifas 2026 en España (Magica).
- **Native Apple leverage:** `Core Location` (detección de viaje con visitas/significativas + trazado) + `Core Motion` (`CMMotionActivity.automotive`) + `CarPlay` categoría *driving task* (clasificar el viaje al aparcar) + Live Activity ("viaje en curso") + `WidgetKit` + exportación PDF/CSV con formato fiscal local + on-device FM para sugerir "motivo" a partir del destino recurrente.
- **What already exists:** MileIQ, Everlance, TripLog, Hurdlr (EE. UU., suscripciones), MileageWise, Magica, Fahrtenbuch, Motolog. **Categoría con dinero y competencia.**
- **Why Apple doesn't already solve it:** Maps guarda "coche aparcado", no libro de viajes.
- **Why an indie could compete:** localización europea seria (tarifas, formatos, idioma, autónomos), on-device sin cuenta, precio honesto en un momento de subida de precios de los líderes, integración CarPlay/Watch/Live Activity de primer nivel.
- **Data entry:** **Bajo** (clasificar viaje con un swipe; el resto automático).
- **Time-to-value:** **primer viaje**.
- **Backend requirement:** **Ninguno**.
- **Third-party dependency:** **Baja**.
- **Monetization hypothesis:** suscripción anual barata (15–30 €) o lifetime; comparables cobran de 15 a 108 $/año.
- **MVP:** (1) detección automática de viajes; (2) clasificación con swipe + CarPlay; (3) informe mensual PDF/CSV con campos exigibles; (4) frecuentes: auto-clasificación por par origen-destino; (5) Live Activity durante el viaje.
- **Solo-developer feasibility:** **Alta** (la detección fiable de inicio/fin de viaje y el consumo de batería son el trabajo duro).
- **MVP scope:** **medio**.
- **Would I personally understand this product?** **Media–alta**: la parte fiscal es un checklist de campos, no un dominio profundo; el producto es "log fiable y exportable".

### Candidate 8 — Cualquier tarjeta, carnet o entrada convertido en pase de Wallet

- **Usuario:** quien tiene tarjetas de fidelidad, carnets de gimnasio/biblioteca/socio, entradas con QR en PDF o captura, y quiere tenerlos en Wallet con Face ID y doble clic.
- **Problema:** "Apple no me deja añadir mi tarjeta del gimnasio a Wallet; la busco en Fotos en la puerta."
- **Current workaround:** capturas en un álbum, apps de fidelización (Stocard/Klarna), Pass2U.
- **Evidencia:** Pass2U 2,8K reviews, 4,3★, #60 top-grossing Shopping (US); guía 2026: "Apple doesn't let you manually add passes to Wallet… Unlike Google Wallet"; review de Pass2U sobre fricción de cuenta y edición.
- **Native Apple leverage:** `Vision` (barcode + `RecognizeDocumentsRequest` para texto) + `Foundation Models` multimodal (extraer nombre, número, vencimiento de una foto) + `PassKit` (`PKAddPassesViewController`) + Share extension (desde un PDF o captura) + geolocalización del pase (Wallet lo muestra en la puerta).
- **What already exists:** Pass2U (freemium, templates, cuenta para templates), MakePass, Pass2Wallet, WalletWallet (web), Stocard (solo fidelidad, gratis, datos).
- **Why Apple doesn't already solve it:** los pases deben ir firmados por un emisor con certificado; Apple no ofrece "crear pase" al usuario.
- **Why an indie could compete:** onboarding de 20 s con extracción automática on-device, sin cuenta, pago único; diseño que los actuales no tienen.
- **Data entry:** **Bajo** (una foto).
- **Time-to-value:** **inmediato**.
- **Backend requirement:** **Mínimo** (firma del `.pkpass` con Pass Type ID; hacerlo on-device embebiendo la clave es posible pero inseguro; un endpoint de firma sin estado es lo razonable).
- **Third-party dependency:** **Baja**.
- **Monetization hypothesis:** pago único o freemium por número de pases (Pass2U cobra funciones Pro; está en top-grossing).
- **MVP:** (1) escaneo/foto → barcode + campos; (2) plantillas de color/logo; (3) firma y añadir a Wallet; (4) edición y re-emisión; (5) Share extension desde PDF/captura.
- **Solo-developer feasibility:** **Alta**. **MVP scope:** **pequeño–medio**.
- **Would I personally understand this product?** **Alta**.
- **Debilidad:** frecuencia de uso de la app baja (la frecuencia está en Wallet); riesgo de que Apple abra la creación manual de pases algún día.

### Candidate 9 — "Días desde la última vez" con etiquetas NFC pegadas en las cosas

- **Usuario:** hogares que quieren saber cuándo cambiaron el filtro del agua, regaron una planta, dieron la pastilla al perro, pusieron la lavadora.
- **Problema:** "No me acuerdo de cuándo lo hice por última vez y no quiero abrir una app para apuntarlo."
- **Current workaround:** Shortcuts NFC + Notes/Reminders como base de datos (r/shortcuts), apps de "days since" manuales.
- **Evidencia:** hilo r/shortcuts "Building a Days since last time of watering plant" con tags NFC; artículos de uso doméstico de NFC; SlashGear: "set timers for scheduled maintenance tasks, such as cleaning the air filter".
- **Native Apple leverage:** `Core NFC` background tag reading (URL universal → la app registra el evento sin abrirse del todo) + `App Intents` (para que Shortcuts/Action button también logueen) + `WidgetKit` (lista de "días desde") + `UserNotifications` (vencimientos).
- **What already exists:** Shortcuts (gratis, ya lo hace, aunque con UX frágil); apps "Last Time", "Days Since" (manuales); Sweepy/Tody (tareas del hogar, suscripción).
- **Why Apple doesn't already solve it:** Reminders no tiene "hecho hace X días" como métrica; Shortcuts exige montar la lógica.
- **Why an indie could compete:** empaquetar el ugly workflow con onboarding de 1 minuto y buena visualización.
- **Data entry:** **Bajo** (un tap físico).
- **Time-to-value:** **primera semana** (necesita acumular eventos).
- **Backend requirement:** **Ninguno**. **Third-party dependency:** **Baja** (tags genéricos).
- **Monetization hypothesis:** pago único bajo; **sin evidencia** de WTP.
- **MVP:** (1) crear ítem y escribir tag; (2) registrar evento al acercar; (3) lista "días desde"; (4) umbral y aviso; (5) widget.
- **Solo-developer feasibility:** **Alta**. **MVP scope:** **pequeño**.
- **Would I personally understand this product?** **Alta**.
- **Debilidad:** Apple ya lo resuelve gratis con Shortcuts para el usuario avanzado, y el usuario no avanzado no compra tags NFC. Job real pero pequeño y difícil de monetizar.

### Candidate 10 — Timeline personal local (el "Google Timeline" que Google desmanteló)

- **Usuario:** quien quiere un registro automático de dónde estuvo (memoria, viajes, justificación de gastos, curiosidad).
- **Problema:** "Perdí mi historial de Google Timeline y en iPhone no hay nada equivalente."
- **Current workaround:** Google Maps Timeline on-device (limitado), Arc Timeline (suscripción), Photos Places (solo fotos).
- **Evidencia:** Google movió Timeline a dispositivo en junio de 2025 con pérdida de datos >90 días para muchos usuarios; Arc cobra 4,99 $/mes, 44,99 $/año, 179,99 $ lifetime con 427 valoraciones.
- **Native Apple leverage:** `CLVisit` + `CLMonitor` + `Core Motion` (modo de transporte) + `PhotoKit` (fotos por visita) + `Foundation Models` (resumen del día on-device) + `App Intents` schemas (Siri: "¿dónde estuve el martes?").
- **What already exists:** Arc Timeline (indie consolidado, potente, complejo, batería), Dawarich (self-hosted), Rewind-style apps.
- **Why Apple doesn't already solve it:** Significant Locations es privado y no navegable; Journal lo usa como sugerencias, no como timeline.
- **Why an indie could compete:** Arc es "todo" (transporte, salud, fotos); un producto simple, privado y de pago único podría diferenciarse.
- **Data entry:** **Nulo**. **Time-to-value:** **primera semana**.
- **Backend requirement:** **Ninguno**. **Third-party dependency:** **Baja**.
- **Monetization hypothesis:** suscripción anual o lifetime (Arc lo demuestra).
- **MVP:** (1) visitas pasivas con permiso Siempre; (2) vista día/mapa; (3) nombres de lugar on-device; (4) búsqueda; (5) exportación.
- **Solo-developer feasibility:** **Alta**. **MVP scope:** **medio** (consumo de batería y clasificación de visitas son el trabajo).
- **Would I personally understand this product?** **Alta**.
- **Debilidad:** job difuso ("memoria"); WTP recurrente débil para la mayoría; Arc ocupa el espacio del entusiasta. Los Candidates 2 y 3 son este mismo motor con un job concreto.

### Candidate 11 — Foto/PDF de horario, cuadrante o calendario escolar → eventos de Calendar

- **Usuario:** padres con calendarios escolares y de actividades en PDF/foto; trabajadores con cuadrantes mensuales; estudiantes.
- **Problema:** "Me pasan el cuadrante en una foto y paso 20 minutos metiendo turnos a mano."
- **Current workaround:** entrada manual; apps IA en la nube; Visual Intelligence de Apple para eventos sueltos.
- **Evidencia:** decenas de apps "photo/PDF to calendar" con suscripción y 2,6–3,0★; Supershift y "Shift Clock – AI Shift Alarm" incorporan reconocimiento de cuadrante por foto.
- **Native Apple leverage:** `Foundation Models` multimodal (27) con herramientas Vision (OCR) + `EventKit` (crear eventos con revisión) + Share extension (desde Fotos/Files/Mail).
- **What already exists:** PDF to Calendar Converter, PCalendar, Calendar Capture (Gemini), PicCal, Smart Calendars AI; Apple Visual Intelligence (iOS 26) para "añadir al calendario" desde capturas.
- **Why Apple doesn't already solve it:** Visual Intelligence extrae un evento, no un cuadrante mensual completo ni series recurrentes.
- **Why an indie could compete:** on-device/PCC gratis → sin coste marginal, sin subir la foto de tus hijos a un servidor, pago único.
- **Data entry:** **Bajo**. **Time-to-value:** **inmediato**.
- **Backend requirement:** **Ninguno** (PCC gratis para SBP). **Third-party dependency:** **Baja**.
- **Monetization hypothesis:** pago único / por conversión.
- **MVP:** (1) importar imagen/PDF; (2) extracción estructurada con guided generation; (3) revisión tabular; (4) escribir a Calendar; (5) detección de recurrencias.
- **Solo-developer feasibility:** **Alta**. **MVP scope:** **pequeño**.
- **Would I personally understand this product?** **Alta**.
- **Debilidad:** **es un wrapper de IA** con un job razonable; la categoría está inundada; Apple está absorbiendo el caso sencillo. Solo tiene sentido como *función* dentro de otro producto (p. ej. cuadrante → Candidate 1).

### Candidate 12 — Captura por voz → recordatorios/eventos estructurados, on-device (Watch / Action button)

- **Usuario:** quien captura tareas andando, conduciendo, con niños.
- **Problema:** "Dicto una nota y luego tengo que convertirla en tareas con fechas."
- **Current workaround:** Siri + Reminders, Voice Memos con transcripción, apps de voz-a-tarea con suscripción.
- **Evidencia (inferencia + observación de mercado):** categoría con muchos entrantes desde 2023; Apple añadió transcripción a Voice Memos y Siri crea recordatorios.
- **Native Apple leverage:** `SpeechAnalyzer` (26) + `Foundation Models` (extracción estructurada) + `EventKit` + `App Intents` (Action button, Watch complication).
- **What already exists:** decenas; Apple Reminders/Siri cubren el 80 %.
- **Why Apple doesn't already solve it / why indie:** Apple ya resuelve el caso base; el diferencial ("varias tareas en una frase") es fino.
- **Data entry:** Bajo. **Time-to-value:** inmediato. **Backend:** Ninguno. **Dependency:** Baja.
- **Monetization:** suscripción (comparables) — dudoso.
- **Feasibility:** Alta. **Scope:** pequeño. **Understand:** Alta.
- **Veredicto:** **saturado + Apple lo resuelve suficientemente**. Se documenta para justificar el descarte.

### Candidate 13 — Bloqueo físico de apps con tag NFC (software-only Brick)

- **Usuario:** quien quiere fricción física para dejar de doomscrollear.
- **Evidencia:** Brick (59 $ hardware) demuestra WTP; Foqos gratis/open source; clones en App Store.
- **Native Apple leverage:** `FamilyControls` + `ManagedSettings` + `Core NFC`.
- **Why not:** entitlement gestionado con colas de semanas por extensión; categoría saturada con una alternativa gratuita y open source con 500+ stars; diferencial nulo.
- **Veredicto:** **descartado en criba**.

### Candidate 14 — Guardián meteorológico de eventos al aire libre del calendario

- **Usuario:** padres con partidos/entrenos, corredores, ciclistas, organizadores.
- **Problema:** "¿Va a llover en el partido del sábado a las 10 en ese campo?"
- **Current workaround:** mirar el tiempo la víspera; Fantastical/Carrot muestran tiempo en el calendario.
- **Evidencia (inferencia):** Fantastical vende previsión por evento como función Premium; no encontré evidencia espontánea fuerte del job específico.
- **Native Apple leverage:** `EventKit` (eventos con ubicación) + `WeatherKit` (previsión horaria en esa ubicación) + `WidgetKit` + Live Activity ("lluvia en 40 min sobre el campo").
- **What already exists:** Fantastical (suscripción), Carrot Weather, Apple Weather (no lee calendario).
- **Data entry:** Nulo. **Time-to-value:** primer evento. **Backend:** Ninguno. **Dependency:** Baja.
- **Monetization:** pago único bajo; WTP dudosa.
- **Feasibility:** Alta. **Scope:** pequeño. **Understand:** Alta.
- **Veredicto:** job real pero **estrecho y absorbido** por calendarios premium; utilidad como función del Candidate 1 (margen extra si llueve).

### Candidate 15 — Contexto de personas antes de una reunión (con quién, cuándo fue la última vez, qué hablamos)

- **Usuario:** profesionales con muchas reuniones externas.
- **Problema:** "Entro a la reunión sin recordar qué acordamos la última vez con esta persona."
- **Current workaround:** buscar en Mail/Notas; CRMs personales (Clay, Dex) con suscripción y entrada manual.
- **Evidencia:** categoría "personal CRM" existente y de pago; Calendar.com añade "People Analytics".
- **Native Apple leverage:** `EventKit` (asistentes históricos) + `Contacts` + notas propias + `Foundation Models` (resumir notas) + widget "próxima reunión: última vez con X hace 3 meses".
- **Why not:** el valor depende de **notas escritas por el usuario** (data entry **Medio–Alto**); sin ellas, solo queda "última vez que os visteis", que es un dato curioso, no un job.
- **Veredicto:** **descartado por data entry**.

---

## 6. Candidates rejected early

| Idea aparentemente atractiva | Por qué se descarta |
|---|---|
| Cualquier producto centrado en HealthKit (sueño, HR, entrenos, medicación, hidratación) | Excluido por decisión previa del fundador; además la categoría está saturada y Apple la absorbe cada año (Workout Buddy, Medications, Sleep Score). |
| Limpieza inteligente de fotos / triaje de capturas de pantalla como inbox de tareas | Excluido por decisión previa; además Visual Intelligence (iOS 26) ya ofrece "añadir al calendario / buscar / preguntar" sobre capturas, absorbiendo el caso base. |
| Presupuesto/gasto con FinanceKit | Solo EE. UU./Reino Unido, entitlement gestionado, **solo cuentas de organización**, categoría Finanzas. Inviable desde España. |
| Analítica personal de Screen Time / "cuánto uso cada app" | Los datos viven sellados en `DeviceActivityReport`; no pueden salir a tu app (DTS lo confirma como diseño). Solo caben bloqueadores, y ese espacio está saturado. |
| Histórico de sensores HomeKit | Sin ejecución en background; exige dispositivo dedicado; Controller for HomeKit ya lo vende con su Hub. |
| "Precision finding" mejorado para AirTags | No hay API pública de Nearby Interaction para AirTags. |
| Seguimiento de paquetes con Live Activities (estilo Parcel) | Depende de APIs de transportistas que cambian o cierran; viola la restricción de dependencia externa del fundador. |
| Estadísticas de escucha de Apple Music (Last.fm nativo) | MusicKit no expone historial completo; observar Now Playing exige la app viva. Apple Replay mensual cubre el caso casual. |
| Aviso de lavadora terminada por sonido | Apple Reconocimiento de sonidos (accesibilidad) ya detecta electrodomésticos y dispara automatizaciones de Shortcuts. |
| Recordatorio de dónde aparqué | Apple Maps con CarPlay/Bluetooth lo hace. |
| Ubicación de hijos / familia | Find My; sin API. |
| Transcripción de reuniones | Voice Memos y Notes transcriben; categoría saturada; es un wrapper. |
| Lectura de notificaciones/mensajes de otras apps para "resumir el día" | Sin API. Descartado por principio. |
| Identificación visual de colecciones (LEGO, monedas, juegos de mesa) | Requiere catálogo de terceros (BGG, Brickset, etc.) → dependencia externa crítica. Se recupera parcialmente como wildcard por la integración con Visual Intelligence. |
| Escáner de recibos para garantías / inventario del hogar para seguros | Frecuencia anual, data entry alto, valor emocional bajo hasta el siniestro. |
| Cuenta regresiva/recordatorio de documentos (pasaporte, ITV, seguro) | Problema anual; los recordatorios de Calendar bastan. |
| Alarma "de misión" (resolver un puzle para apagar) sobre AlarmKit | AlarmKit permite parar la alarma con los botones del sistema; el patrón Alarmy no es reproducible fielmente (queja en foros de developers en beta). |
| Mapa de calor de Wi-Fi en casa | iOS no expone RSSI ni escaneo de redes a terceros. |
| Salud de la batería / uso de almacenamiento | Sin API. |

---

## 7. Comparative analysis

Comparación cualitativa (sin fórmula). Escala: ●●● fuerte · ●● medio · ● débil · ✕ descartado.

| # | Candidato | Claridad problema | Evidencia | Frecuencia | Time-to-value | Data entry | Ventaja iOS | Explicable | Competencia (menos es mejor) | Gap vs Apple | Gap vs indies | Monetización | Dependencia ext. | Backend | Riesgo App Review | Hardware mín. | Portabilidad intl. | Distribución | Solo dev | Fundador juzga | MVP pequeño | Evolución |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Despertador por calendario+viaje | ●●● | ●● | ●●● diaria | ●●● | ●●● nulo | ●●● AlarmKit | ●●● | ●● (pequeños) | ●●● | ●● | ●● pago único | ●●● | ●●● | ●●● | iOS 26+ | ●●● | ●● | ●●● | ●●● | ●●● | ●● |
| 2 | Días de oficina | ●●● | ●● | ●●● | ●●● | ●●● | ●●● | ●●● | ●● | ●●● | ●● | ● | ●●● | ●●● | ●●● | — | ●●● | ●● | ●●● | ●●● | ●●● | ●● (→ #3) |
| 3 | Días por país | ●●● | ●●● | ●●● | ●● | ●●● | ●●● | ●●● | ● (varios recientes) | ●●● | ●● | ●●● | ●●● | ●●● | ●●● | — | ●●● | ●●● (comunidades) | ●●● | ●● | ●● | ●●● |
| 4 | Auditoría de calendario | ●● | ●● | ● | ●●● | ●●● | ●● | ●●● | ●● | ●●● | ●● | ● | ●●● | ●●● | ●●● | — | ●●● | ● | ●●● | ●●● | ●●● | ● |
| 5 | Histórico HomeKit | ●●● | ●●● | ●●● | ● | ●●● | ✕ sin BG | ●●● | ● | ●●● | ● | ●● | ●●● | ✕ hw dedicado | ●●● | Hub | ●●● | ●● | ● | ●● | ✕ | ● |
| 6 | Práctica musical/dance MU | ●●● | ●● | ●● | ●●● | ●● | ●●● API nueva | ●● | ● (Anytune, Moises) | ●●● | ●● | ●●● | ●●● | ●●● | ●●● | iOS 27+, sin Apple Music | ●●● | ●● | ●● | ● / ●● | ●● | ●● |
| 7 | Kilometraje EU | ●●● | ●●● | ●●● | ●●● | ●● | ●● | ●●● | ● (muchos) | ●●● | ●● | ●●● | ●●● | ●●● | ●●● | — | ●● (fiscalidad local) | ●● | ●● | ●● | ●● | ●●● |
| 8 | Pases Wallet | ●●● | ●●● | ● | ●●● | ●● | ●●● PassKit | ●●● | ●● | ●●● | ●● | ●●● | ●●● | ●● mínimo | ●● (firma) | — | ●●● | ●● | ●●● | ●●● | ●●● | ● |
| 9 | NFC días desde | ●● | ●● | ●● | ● | ●● | ●● | ●●● | ●● | ● (Shortcuts) | ●● | ● | ●●● | ●●● | ●●● | tags | ●●● | ● | ●●● | ●●● | ●●● | ● |
| 10 | Timeline local | ● difuso | ●●● | ●●● | ● | ●●● | ●●● | ●● | ● (Arc) | ●●● | ● | ●● | ●●● | ●●● | ●●● | — | ●●● | ● | ●● | ●●● | ●● | ●● |
| 11 | Foto→Calendar | ●● | ●● | ● | ●●● | ●● | ●● | ●●● | ✕ inundado | ● | ● | ● | ●●● | ●●● | ●● | AI devices | ●●● | ● | ●●● | ●●● | ●●● | ● |
| 12 | Voz→tareas | ● | ● | ●● | ●●● | ●● | ●● | ●● | ✕ | ✕ | ● | ● | ●●● | ●●● | ●●● | AI devices | ●●● | ● | ●●● | ●●● | ●●● | ● |
| 13 | NFC Brick | ●●● | ●●● | ●●● | ●●● | ●● | ●● | ●●● | ✕ | ●● | ✕ (Foqos gratis) | ● | ●●● | ●●● | ● entitlement | tags | ●●● | ● | ●● | ●●● | ●● | ● |
| 14 | Tiempo en eventos | ●● | ● | ●● | ●● | ●●● | ●● | ●●● | ●● | ●● | ● | ● | ●●● | ●●● | ●●● | — | ●●● | ● | ●●● | ●●● | ●●● | ● |
| 15 | Contexto de personas | ●● | ● | ●● | ● | ✕ alto | ●● | ●● | ●● | ●● | ● | ●● | ●●● | ●●● | ●●● | — | ●●● | ● | ●●● | ●●● | ●● | ●● |

**Lectura de la tabla:**
- **Sobreviven con claridad:** 1, 3, 7, 8, 6 (por diversidad y ventana técnica).
- **Sobreviven pero como wildcards o modos de otro producto:** 2 (mismo motor que 3; fundador-usuario; WTP baja), 4 (curiosidad más que hábito), 10 (job difuso; 2 y 3 son su versión concreta), 14 y 11 (funciones, no productos).
- **Mueren:** 5 (plataforma), 9 (Shortcuts lo resuelve, sin WTP), 12 (Apple + saturación), 13 (saturación + gratis), 15 (data entry).

**Tensiones honestas:**
- Los dos candidatos con mejor evidencia de dinero (3 y 7) son también los más competidos. El argumento indie es "hacerlo bien para un mercado concreto (España/UE) con on-device y precio honesto", no "nadie lo hace".
- El candidato con la ventana técnica más limpia (1) tiene el riesgo técnico más específico (re-planificación en background) y la WTP menos probada.
- El candidato técnicamente más interesante (6) tiene un techo estructural (sin Apple Music) que limita el mercado a quienes poseen archivos.

---

## 8. Final five

### Finalist 1 — Despertador que se calcula desde el primer evento y el tiempo de viaje

- **Problem in one sentence:** Cada noche recalculo y muevo la alarma según mi primer compromiso y cuánto tardo en llegar, y si el evento cambia la alarma no se entera.
- **Why this survived:** job diario, universal, explicable en una frase; data entry nulo; datos ya existen (Calendar + Maps); la API que lo hace posible tiene 15 meses; los primeros entrantes son apps de un desarrollador con pocas reseñas o construidas antes de AlarmKit.
- **Native advantage:** solo iOS 26+ puede hacerlo con una alarma de sistema real (rompe Silencio/Focus, suena en Watch, StandBy, Dynamic Island). Un web app o Android no tienen esta combinación con el calendario del sistema y ETA de Maps sin coste.
- **Existing evidence:** Shortcuts caseros y scripts Android para el mismo job; Calarm (1,99 $) con limitación "must be opened"; Supershift absorbe el subcaso de turnos; Unmissable/VariAlarm confirman que otros desarrolladores ven el hueco.
- **Existing competitors:** Calarm, Unmissable, VariAlarm, Supershift (turnos), Sleep Cycle/Alarmy (sin calendario), Apple Sleep Schedule (fijo).
- **Why there may still be room:** ninguno combina *primer evento + ETA real + condiciones (tiempo, día sin eventos) + explicación ("suenas a las 6:40 porque tienes X a las 8:15 en Y, 35 min en coche")* con alarma de sistema y widget. Es un producto de una pantalla.
- **Main risk:** re-planificación. Si el calendario cambia tarde y el sistema no concede el `BGAppRefreshTask`, la alarma programada queda vieja. Segundo riesgo: WTP; el usuario puede sentir que "una alarma no se paga".
- **Cheapest validation:** (a) publicar un Shortcut gratuito que haga el cálculo básico y medir instalaciones/feedback en r/shortcuts y r/ios; (b) landing con lista de espera "Wake up by calendar" en comunidades de productividad; (c) prototipo TestFlight de 2 semanas midiendo cuántas noches la alarma calculada coincide con la que el usuario habría puesto y cuántas veces hubo que corregir a mano.
- **MVP shape:** una pantalla de reglas (calendarios, preparación, tope mínimo/máximo, modo de transporte), una tarjeta "mañana", widget, Live Activity de cuenta atrás nocturna, alarma AlarmKit con botón secundario "ver evento". Cero cuentas, cero servidor.
- **Monetization evidence:** Calarm cobra 1,99 $; Supershift monetiza alarmas por turno dentro de una suscripción; Alarmy/Sleep Cycle demuestran que hay gasto en la categoría alarma (aunque con otro job).
- **First 100 users:** r/shortcuts y r/ios (compartiendo el Shortcut gratuito como gancho), comunidades de opositores y estudiantes con horarios variables, enfermería y turnos (cross-post con la función "importa tu cuadrante" del Candidate 11), MacStories/9to5Mac "AlarmKit apps" roundups, Product Hunt.
- **Founder fit:** el fundador vive el problema, entiende Calendar/Maps/AlarmKit a nivel de API y puede juzgar si el cálculo es correcto y si la UX de "por qué suena a esta hora" es honesta.

### Finalist 2 — Contador pasivo de días por país (Schengen 90/180, 183 fiscal, segunda vivienda)

- **Problem in one sentence:** Necesito saber con certeza cuántos días he pasado y me quedan en Schengen (o en un país) en una ventana móvil, sin llevar una hoja de cálculo.
- **Why this survived:** trigger externo duro y reciente (EES operativo en toda Schengen desde abril de 2026; fin de sellos; sanciones automáticas), consecuencia económica clara (multas, prohibición de entrada, residencia fiscal), datos pasivos (ubicación), WTP demostrada por competidores que cobran suscripción desde hace años.
- **Native advantage:** `CLVisit` + actualizaciones significativas permiten contar países con consumo mínimo y sin servidor; widget/Watch con "días restantes"; privacidad on-device (solo se almacena país+fecha) es un argumento de venta real para datos de compliance.
- **Existing evidence:** prensa balear y guías 2026 sobre la "trampa" del EES para británicos con segunda vivienda; TrackingDays (3,99 $/mes) apuntando a "snowbirds and overseas homeowners"; oleada de apps automáticas en 2025–26.
- **Existing competitors:** TrackingDays, Staywise, Days Monitor, Tax Residency Tracker, Days of Stay, calculadoras web.
- **Why there may still be room:** los competidores son "todas las reglas del mundo" con UIs genéricas; ninguno es excelente para **un** caso (p. ej. propietario británico en España tras EES: 90/180 + 183 fiscal + aviso de ventana móvil + informe imprimible) ni tiene una distribución local. El producto no aconseja; cuenta y avisa.
- **Main risk:** mercado ya servido por 5+ apps recientes; detección pasiva imperfecta en fronteras terrestres; responsabilidad percibida si el conteo falla. Puede acabar siendo un producto de 300–800 €/mes en un nicho geográfico, no más.
- **Cheapest validation:** entrevistar/encuestar en grupos de Facebook de "Brits in Spain/Costa Blanca/Mallorca" y r/digitalnomad: cómo cuentan hoy, cuánto pagan, qué les asusta del EES; probar una landing en inglés con precio anual visible y medir conversión a lista de espera.
- **MVP shape:** permiso Siempre, detección de país por visitas, importación manual de viajes previos, regla 90/180 con proyección "puedes quedarte hasta el X", aviso a 80 días, widget, PDF. Sin cuenta, sin servidor.
- **Monetization evidence:** TrackingDays 3,99 $/mes; Tax Residency Tracker freemium; Monaeo (B2B) en el extremo caro del mismo job.
- **First 100 users:** grupos de Facebook y foros de expatriados británicos en España (Costa del Sol, Mallorca, Alicante), r/digitalnomad, r/expats, newsletters de asesorías de extranjería, posts SEO en inglés sobre EES + 90/180 (búsqueda muy activa en 2026).
- **Founder fit:** el conteo, las ventanas móviles y la geolocalización son problemas de ingeniería que el fundador domina; el dominio legal se acota a "reglas de conteo publicadas" y se delega la interpretación al usuario/asesor. Puede juzgar si el producto es fiable, que es lo que importa.

### Finalist 3 — Registro automático de kilómetros para autónomos y profesionales europeos, on-device

- **Problem in one sentence:** Tengo que justificar desplazamientos profesionales con fecha, origen, destino, km y motivo, y no llevo el registro porque es tedioso.
- **Why this survived:** dinero recurrente demostrado en la categoría; el líder subió precios un 50 % en 2026 y hay búsqueda activa de alternativas; el job es pasivo; el mercado europeo está servido por apps pequeñas con localización desigual.
- **Native advantage:** detección de viaje con Core Location + Core Motion sin servidor; **CarPlay categoría driving task** para clasificar el viaje al aparcar; Live Activity durante el viaje; Watch; exportación local. Un web app no puede detectar viajes; Android existe pero la ejecución premium en el ecosistema Apple es diferenciadora.
- **Existing evidence:** MileIQ 8,99 $/mes con "más de 80.000 reseñas de cinco estrellas"; TripLog gratis ilimitado como respuesta; Magica (14,99 $/año, "sin servidores", con guía de tarifas 2026 en España); Fahrtenbuch (GoBD, CarPlay, Watch).
- **Existing competitors:** MileIQ, Everlance, TripLog, Hurdlr, MileageWise, Magica, Fahrtenbuch, Motolog, Driversnote.
- **Why there may still be room:** localización fiscal seria por país (España: campos, 0,26 €/km, IVA en estimación directa; Francia: barème; Alemania: GoBD), on-device sin cuenta, precio honesto, y una ejecución CarPlay/Live Activity/Watch que los pequeños europeos no tienen.
- **Main risk:** categoría muy competida con jugadores financiados y apps locales ya "on-device"; la detección fiable de inicio/fin de viaje y la batería son difíciles y se juzgan en reviews de 1★; el diferencial puede acabar siendo solo precio.
- **Cheapest validation:** hablar con 10 autónomos/comerciales españoles: qué usan, cuánto pagan, qué exige su gestoría; revisar reviews 1–3★ de Magica, Fahrtenbuch y MileIQ en las tiendas ES/DE/FR para listar fallos repetidos; landing en español con precio.
- **MVP shape:** detección automática, clasificación por swipe y desde CarPlay, informe PDF/CSV con campos exigibles, auto-clasificación de trayectos frecuentes, Live Activity. Sin cuenta.
- **Monetization evidence:** suscripciones de 15 a 108 $/año en toda la categoría.
- **First 100 users:** comunidades de autónomos en España (foros, grupos de Telegram/Facebook, r/autonomos), asesorías/gestorías como prescriptores (una gestoría con 200 clientes es un canal), agentes inmobiliarios y comerciales farmacéuticos, YouTube en español de fiscalidad para autónomos.
- **Founder fit:** el núcleo es un problema de sensores, batería y fiabilidad, que el fundador puede juzgar mejor que un fundador de negocio; la fiscalidad es un checklist de campos verificable con dos gestorías. Riesgo de fit: si el fundador no conduce por trabajo, necesita usuarios de referencia desde el día uno.

### Finalist 4 — Cualquier tarjeta, carnet o entrada convertido en pase de Wallet

- **Problem in one sentence:** Tengo tarjetas y carnets que ningún emisor pone en Wallet y los busco en Fotos en la puerta del gimnasio.
- **Why this survived:** gap real de Apple (no se pueden crear pases manualmente), competidor con ingresos demostrados (Pass2U top-60 de Compras en EE. UU.) y fricción visible en reviews, backend mínimo, time-to-value inmediato, explicable en una frase.
- **Native advantage:** Wallet es el destino (doble clic, Face ID, geolocalización del pase, Watch); Vision + Foundation Models multimodal extraen número, nombre y caducidad de una foto on-device; Share extension desde PDF/captura.
- **Existing evidence:** Pass2U 2,8K reviews, 4,3★, ranking de ingresos; guía 2026 "Apple doesn't let you manually add passes"; review sobre fricción de cuenta.
- **Existing competitors:** Pass2U, MakePass, Pass2Wallet, WalletWallet (web), Stocard (fidelidad).
- **Why there may still be room:** los actuales son de 2016, con plantillas, cuentas y UX de herramienta; hay hueco para un flujo de 20 segundos, sin cuenta, con extracción automática y diseño cuidado, a pago único.
- **Main risk:** frecuencia de uso de la app baja (se usa Wallet, no la app), lo que limita retención y boca a boca; Apple podría añadir creación manual de pases; la firma exige un pequeño servicio (o riesgo de clave embebida).
- **Cheapest validation:** revisar las 1–3★ de Pass2U/MakePass para listar fricciones; preguntar en r/AppleWallet y r/ios qué tarjetas quieren y no pueden añadir; landing con vídeo de 20 s.
- **MVP shape:** cámara → barcode + OCR + extracción FM → previsualización → firmar → añadir a Wallet; edición; Share extension. Endpoint de firma sin estado (Cloudflare Worker o similar).
- **Monetization evidence:** Pass2U cobra Pro y aparece en top-grossing.
- **First 100 users:** r/AppleWallet, r/iphone, TikTok/Reels "cómo meter tu tarjeta del gimnasio en Wallet" (formato muy visual), Product Hunt, foros de gimnasios/bibliotecas.
- **Founder fit:** producto que el fundador usa y entiende; el trabajo difícil (barcodes, PassKit, firma, extracción) es ingeniería Apple.

### Finalist 5 — Práctica musical y de baile con beat grid, secciones y tonalidad automáticas

- **Problem in one sentence:** Quiero practicar una parte concreta de una grabación (mi ensayo, mi clase, una canción que tengo) en bucle y más lenta sin marcar compases y secciones a mano.
- **Why this survived:** Music Understanding entrega on-device justo lo que Moises vende en la nube y Anytune obliga a hacer a mano; nicho apasionado que ya paga; cero backend; ventana técnica de meses.
- **Native advantage:** análisis on-device gratis y privado con timestamps de beats/compases/frases/secciones; `BGContinuedProcessingTask` para procesar bibliotecas; AVFoundation para time-stretch; Live Activity con el loop actual.
- **Existing evidence:** Moises monetiza "Sections" como Premium; Anytune (~15 $ pago único) exige marcado manual; PracticeSession vende "auto-generate regions" desde archivos de notación porque no puede desde audio.
- **Existing competitors:** Anytune, Moises, Capo, Amazing Slow Downer, AudioStretch.
- **Why there may still be room:** foco en **grabaciones propias** (ensayos, clases de baile, coros) donde el DRM no aplica; posible especialización en baile (conteo de 8, marcadores por frase, tempo por sección), un usuario que las apps de músicos ignoran.
- **Main risk:** el techo DRM (nada de Apple Music) reduce el mercado casual; Anytune puede adoptar Music Understanding en semanas; iOS 27+ solo.
- **Cheapest validation:** prototipo con el sample "Music Understanding Lab" sobre 20 grabaciones reales de ensayo/clase y comprobar si secciones y compases son fiables en audio no de estudio; entrevistas con 5 profesores de baile y 5 músicos amateurs sobre cómo practican hoy.
- **MVP shape:** importar audio → análisis → línea de compases y secciones → loop por sección con velocidad → marcadores editables → biblioteca. Sin cuenta.
- **Monetization evidence:** Anytune pago único, Moises 36 $/año, Capo suscripción.
- **First 100 users:** escuelas y profesores de baile (Instagram/TikTok), r/Guitar, r/piano, r/drums, r/WeAreTheMusicMakers, coros y bandas amateurs, foros de Anytune/Moises.
- **Founder fit:** **el más débil de los cinco**: si el fundador no toca ni baila, no puede juzgar si la sección detectada "suena bien" ni qué controles importan. Se compensa con usuarios expertos, pero es un coste real.

---

## 9. Three wildcards

### Wildcard A — Contador de días de oficina (RTO) como primer experimento del "motor de presencia"

Casi descartado por WTP baja (comparables 0,99–1,99 $). Propiedad extraordinaria: **el fundador es el usuario**, el MVP cabe en dos semanas, no tiene backend, y es exactamente el mismo motor (`CLMonitor` + `CLVisit` + widget + reglas de cuota) que el Finalist 2. Merece no olvidarse como **producto-laboratorio**: permite aprender permisos de ubicación Siempre, consumo de batería, fiabilidad de geocercas, pricing y ASO con riesgo mínimo, y su código migra al contador de países. Evidencia: spreadsheets públicos, dashboards de cumplimiento corporativo, 4–5 apps manuales sin tracción.

### Wildcard B — Una app cuyo "interfaz" es Siri y Spotlight (App Intents schemas, iOS 27)

Casi descartada por especulativa. Propiedad extraordinaria: iOS 27 permite que las entidades de una app entren en el índice semántico de Spotlight y que Siri actúe sobre ellas sin frases predefinidas. Un producto minúsculo de "hechos personales" (dónde dejé el pasaporte, qué talla de filtro usa la campana, cuándo cambié las ruedas, medidas de las ventanas) cuyo valor sea **responder por Siri/Spotlight**, no abrirse. Es la primera vez que un indie puede vivir dentro del sistema. Riesgo: depende de la adopción real de Siri conversacional y de que Apple no lo absorba en Notes. Validación barata: prototipo con 20 entidades y probar si Siri las devuelve de forma fiable en español.

### Wildcard C — Identificador de colección para Visual Intelligence (iOS 26) con catálogo propio

Casi descartada por dependencia de catálogos externos. Propiedad extraordinaria: con `IntentValueQuery` una app aparece como resultado cuando el usuario apunta la cámara a un objeto. Si el catálogo es **del usuario** (su colección de vinilos, juegos de mesa, libros, vinos ya catalogados) y no de un tercero, la dependencia desaparece: "apunta y te dice si ya lo tienes, qué pagaste y dónde está". Riesgo: la superficie es nueva y Apple controla cuándo aparece tu app; el data entry inicial (catalogar) es medio. Merece seguimiento porque nadie indie está construyendo para esa superficie todavía.

---

## 10. Important platform constraints discovered

1. **AlarmKit es un instante, no una regla.** La alarma se programa con fecha fija o repetición semanal. Cualquier producto "inteligente" debe recalcular con `BGAppRefreshTask` (no garantizado) y al abrir. Las alarmas se detienen con botones del sistema; no cabe el patrón "misión para apagar". Requiere `NSAlarmKitUsageDescription` y autorización explícita.
2. **Music Understanding no ve Apple Music.** Confirmado por DTS: requiere acceso directo al asset; MusicKit no lo proporciona. Solo archivos propios/DRM-free.
3. **Foundation Models en PCC exige entitlement** (`com.apple.developer.private-cloud-compute`) y la aprobación es hoy el cuello de botella; gratis solo dentro del Small Business Program y <2M descargas. On-device requiere dispositivos Apple Intelligence; no se puede impedir la descarga en dispositivos no compatibles (hay que degradar con `Availability`).
4. **Screen Time está sellado.** `DeviceActivityReport` no puede exportar datos a la app; tokens opacos; entitlement por bundle ID incluyendo extensiones, con colas.
5. **FinanceKit: US/UK, organización, Finanzas.** No aplica a un indie español.
6. **HomeKit sin background.** No hay histórico ni ejecución continua; el logging exige hardware dedicado.
7. **EventKit notifica cambios solo con la app viva.** Un producto reactivo al calendario debe combinar BG refresh, recálculo al abrir y widgets.
8. **Core Location "Siempre" es la fricción más alta del sistema** (dos pasos y recordatorios periódicos del sistema). Los productos pasivos de ubicación deben justificarlo en la primera pantalla y mostrar valor antes de pedirlo.
9. **Journaling Suggestions es solo picker.** No hay acceso programático ni pasivo; no sirve como fuente de datos automática.
10. **Live Activities remotas necesitan servidor.** Sin APNs, solo se actualizan con la app viva o en BG; para productos sin backend, diseñar Live Activities locales (cuenta atrás, viaje en curso).
11. **PassKit exige firma con certificado.** Crear pases implica un componente de firma; on-device con clave embebida es inseguro.
12. **Nearby Interaction no incluye AirTags; SensorKit es solo investigación; EnergyKit es EE. UU.**
13. **Ventanas cortas.** Tras AlarmKit (jun-2025) aparecieron 4–6 apps en 12 meses y un incumbente absorbió el subcaso principal. Con Music Understanding y FM multimodal (sep-2026) pasará lo mismo: la ventana útil es de 6–12 meses.

---

## 11. What I would investigate next

1. **Fiabilidad real de la re-planificación nocturna (Finalist 1).** Prototipo de 2 semanas con `BGAppRefreshTask` + `BGProcessingTask` en 3 dispositivos con uso normal: % de noches en que la alarma se actualizó sin abrir la app. Este número decide el producto.
2. **Detección pasiva de país (Finalist 2).** Prototipo con `CLVisit` + significativas: viaje real con cruce terrestre (Portugal/Francia) y vuelo; medir latencia de detección, falsos positivos y batería; comparar contra `CLMonitor` con geocercas de país (inviable por tamaño) o rejilla.
3. **Reviews 1–3★ de competidores locales (Finalists 2, 3, 4).** Extraer fallos repetidos de TrackingDays, Staywise, Magica, Fahrtenbuch, Pass2U en las tiendas ES/UK/DE.
4. **Entrevistas cortas (5–10 por finalista):** británicos con segunda vivienda en España; autónomos con coche; profesores de baile; usuarios de Shortcuts con alarmas por calendario.
5. **Music Understanding sobre audio "sucio".** Probar el sample Music Understanding Lab con grabaciones de ensayo y clase (reverb, ruido, tempo variable) y medir si secciones/compases son útiles. Si no lo son, el Finalist 5 muere.
6. **Cola del entitlement PCC.** Solicitarlo ya para cualquier producto que use FM multimodal; el tiempo de aprobación condiciona el roadmap.
7. **Pricing.** Tests de landing con precio visible (pago único vs anual) para 1 y 2; el objetivo es aprender WTP antes de escribir la app.
8. **Siri en español (Wildcard B).** Comprobar cobertura idiomática de intent schemas en iOS 27 antes de invertir.

---

## 12. Sources

### Apple (documentación, WWDC, foros oficiales)

- What's new in iOS 27 (Foundation Models, App Intents schemas, Core AI, Music Understanding, NowPlaying, widgets vía App Intents): https://developer.apple.com/ios/whats-new/
- WWDC26 241 — What's new in the Foundation Models framework (PCC 32K, razonamiento, imágenes): https://developer.apple.com/videos/play/wwdc2026/241/
- WWDC26 339 — Bring an LLM provider to the Foundation Models framework: https://developer.apple.com/videos/play/wwdc2026/339/
- Foundation Models documentation (adding server-side intelligence with PCC, multimodal prompting, dynamic profiles): https://developer.apple.com/documentation/FoundationModels
- WWDC25 Group Lab — Apple Intelligence (contexto ~4K tokens en iOS 26, disponibilidad): https://developer.apple.com/forums/thread/792763
- WWDC26 253 — Meet the Music Understanding framework: https://developer.apple.com/videos/play/wwdc2026/253/
- Apple DTS: Music Understanding no soporta streams de Apple Music/MusicKit: https://developer.apple.com/forums/thread/829763 · https://developer.apple.com/forums/thread/829739
- WWDC25 230 — Wake up to the AlarmKit API: https://developer.apple.com/videos/play/wwdc2025/230
- AlarmKit (foro: limitaciones en beta): https://developer.apple.com/forums/thread/792846
- WWDC24 — Meet FinanceKit: https://developer.apple.com/videos/play/wwdc2024/2023/
- Get started with FinanceKit (requisitos US/UK, entitlement): https://developer.apple.com/financekit
- Family Controls — foros (sandbox del DeviceActivityReport, entitlement por extensión): https://developer.apple.com/forums/tags/family-controls?page=5 · https://developer.apple.com/forums/thread/813073 · https://developer.apple.com/forums/thread/824645
- Wi-Fi Aware / AccessorySetupKit (DTS): https://developer.apple.com/forums/thread/734344
- Lista de frameworks del sistema por versión (IdentityDocumentServices 26, etc.): https://theapplewiki.com/wiki/Frameworks

> Nota: las rutas canónicas de documentación de Apple para frameworks estables citados en el mapa (Core Location `CLMonitor`/`CLVisit`, EventKit, PhotoKit, Core NFC, Nearby Interaction, WeatherKit, BackgroundTasks, ActivityKit, WidgetKit, PassKit, SensorKit, HomeKit, Speech, Sound Analysis, ShazamKit, Vision/VisionKit, Core Motion) están en `https://developer.apple.com/documentation/<framework>`; no todas fueron descargadas en esta sesión y sus capacidades se describen a partir de conocimiento de plataforma verificado hasta iOS 26. Conviene re-verificar cada una antes de comprometer un roadmap.

### Análisis y prensa técnica sobre iOS 27

- Ivan Magda — Foundation Models, Year Two: https://ivanmagda.dev/posts/wwdc26-foundation-models-year-two/
- Blake Crosley — Apple Foundation Models framework (tipos beta 27, entitlement PCC): https://blakecrosley.com/blog/apple-foundation-models-framework
- The Swift Dev — Build music-aware apps with Music Understanding: https://www.theswift.dev/posts/build-music-aware-apps-with-music-understanding/
- Synthtopia — Apple intros Music Understanding framework: https://www.synthtopia.com/content/2026/06/23/apple-intros-music-understanding-framework-at-wwdc/
- MacRumors — 250 cambios de iOS 27 / lanzamiento 14-sep-2026: https://www.macrumors.com/2026/06/10/apple-lists-250-changes-ios-27-and-more/
- mjtsai — iOS 26: AlarmKit (limitaciones): https://mjtsai.com/blog/2025/06/20/ios-26-alarmkit/
- Nil Coalescing — Countdown timer with AlarmKit: https://nilcoalescing.com/blog/CountdownTimerWithAlarmKit
- drobinin — Screen Time & Family Controls consulting (sandbox del report): https://drobinin.com/consulting/screen-time-family-controls/

### Evidencia de problema y competencia — Finalist 1 (alarma por calendario)

- Shortcut "Hey Siri, Let's Nap": https://www.goodreads.com/author_blog_posts/22144390-hey-siri-let-s-nap
- alarm-calendar-sync (Google Apps Script + MacroDroid): https://github.com/bsodium/alarm-calendar-sync
- Calarm (1,99 $): https://apps.apple.com/app/id509840570
- Unmissable (AlarmKit): https://apps.apple.com/us/app/-/id6752518796
- VariAlarm: https://apps.apple.com/app/id6757322888
- Never Forget Alarm: https://apps.apple.com/us/app/id6752827034
- Shift Worker Calendar & Alarm: https://apps.apple.com/us/app/shift-worker-calendar-alarm/id6759396502
- Supershift (Smart Shift Alarms): https://apps.apple.com/us/app/supershift-shift-calendar/id1104165041 · https://supershift.app/
- Shift Clock – AI Shift Alarm: https://apps.apple.com/py/app/shift-clock-ai-shift-alarm/id6744865353

### Evidencia — Finalist 2 y Wildcard A (días por país / oficina)

- Majorca Daily Bulletin — EES "very nasty trap" para propietarios de segunda vivienda: https://amp.majorcadailybulletin.com/news/local/2025/10/14/137267/spain-travel-how-avoid-the-new-european-union-entry-and-exit-scheme.html
- mallorca.com — Regla 90/180 y EES (9-abr-2026): https://www.mallorca.com/es/consejos/vivir-en-mallorca/visado-residencia/regla-90-180-dias-espana · https://www.mallorca.com/es/consejos/vivir-en-mallorca/visado-residencia/ees-etias-espana-2026
- Beancount — EES y nómadas digitales (10-abr-2026): https://beancount.io/zh/blog/2026/07/21/eu-entry-exit-system-schengen-90-180-day-rule-digital-nomad-guide
- TrackingDays (3,99 $/mes): https://apps.apple.com/us/app/trackingdays/id657769643 · https://www.trackingdays.com/
- Staywise: https://apps.apple.com/us/app/staywise-country-days-tracker/id6749697652
- Tax Residency Tracker: https://apps.apple.com/us/app/tax-residency-tracker/id6753808152 · https://taxresidencytracker.com/
- Days Monitor: https://daysmonitor.com/daysmonitorapp/
- Days of Stay: https://apps.apple.com/us/app/days-of-stay-tax-schengen/id6753990603
- Office-Work-Tracker spreadsheet: https://github.com/RogerHowellDfE/Office-Work-Tracker
- Blind — RTO compliance dashboards: https://www.teamblind.com/post/whats-micron-current-rto-policy-lb63rsvl
- Lanyard (1,99 $): https://apps.apple.com/us/app/id6455731792 · HybridWorkTracker: https://apps.apple.com/us/app/hybridworktracker/id6743126246 · Office Attendance: https://apps.apple.com/us/app/id6477813730 · Hybrid Office Tracker: https://apps.apple.com/us/app/-/id6754510381 · Where I Worked Today: https://apps.apple.com/app/id6755990197
- Arc Timeline (pricing): https://apps.apple.com/us/app/arc-timeline-trips-places/id1063151918
- Google Maps Timeline shutdown (jun-2025): https://tech.yahoo.com/general/articles/google-puts-date-maps-timelines-230941507.html · https://www.techradar.com/phones/google-maps-will-soon-delete-your-location-history-unless-you-tell-it-not-to

### Evidencia — Finalist 3 (kilometraje)

- TripLog — MileIQ alternatives (subida a 8,99 $/mes): https://www.triplog.net/es/blog/mileiq-alternatives
- SparkReceipt — mejores apps de millas 2026: https://sparkreceipt.com/es-us/blog/mejores-apps-registrar-millas/
- ZeoRoutePlanner — apps para repartidores 2026: https://zeorouteplanner.com/es/best-mileage-tracking-apps/
- Magica (14,99 $/año): https://apps.apple.com/us/app/-/id1341304115 · tarifas 2026 España: https://magica-app.com/es/tarifas-kilometricas-2026-en-espana-guia-completa-para-autonomos-y-empresas/
- Fahrtenbuch (GoBD): https://mwm.ai/es/apps/fahrtenbuch/286070473
- Motolog: https://motolog.app/es/

### Evidencia — Finalist 4 (pases Wallet)

- Pass2U Wallet (ficha, reviews): https://apps.apple.com/us/app/pass2u-wallet-create-and-put-cards-into-wallet/id1142473931
- Pass2U ranking top-grossing Shopping #60 (mar-2026), 2,8K reviews: https://apppricinglab.com/app/apple/1142473931
- Guía 2026 "How to create an Apple Wallet pass for free": https://walletwallet.alen.ro/blog/create-apple-wallet-pass-free/
- Pass2Wallet: https://apps.apple.com/qa/app/pass2wallet-add-card-to-wallet/id6541762088

### Evidencia — Finalist 5 (práctica musical)

- Moises — Sections feature: https://moises.ai/blog/moises-news/new-song-sections-feature/ · pricing 2026: https://www.chartlex.com/blog/marketing/moises-ai-review-2026
- Anytune (~15 $ Pro): https://www.songscription.ai/blog/best-apps-to-slow-down-music · https://www.anytune.app/
- PracticeSession vs Anytune vs ASD: https://www.practicesession.app/blog/practice-session-vs-amazing-slow-downer-vs-anytune/
- Algoriddim — DRM y Apple Music en djay: https://help.algoriddim.com/topic/music-streaming/drm-protected-songs

### Evidencia — candidatos descartados y otros

- r/shortcuts — NFC "days since watering plant": https://lr.ggtyler.dev/r/shortcuts/comments/1f1zuei/building_a_days_since_last_time_of_watering_plant
- Usos domésticos de NFC: https://www.slashgear.com/1990543/useful-nfc-automations-for-home/ · https://appleinsider.com/articles/22/05/09/how-to-make-nfc-automations-to-use-with-your-iphone
- Brick y alternativas (Foqos open source): https://www.bgr.com/2235201/phone-blocking-app-brick-alternatives/ · https://gittrend.io/repo/awaseem/foqos · https://goodmorningamerica.com/shop/story/brick-review-134547488
- Controller for HomeKit — Charts requiere Controller Hub: https://controllerforhomekit.com/features/charts
- Timeview: https://apps.apple.com/us/app/timeview-calendar-statistics/id1439197028 · Calendar Statistics: https://apps.apple.com/dk/app/calendar-statistics/id447994595 · Calendar Insights: https://apps.apple.com/us/app/calendar-insights-time-stats/id6745164900 · Calendar.com analytics: https://www.calendar.com/analytics/
- Apple Support Communities — sumar horas en Calendar: https://discussions.apple.com/thread/253114325
- Apps foto→calendario (wrappers): https://apps.apple.com/app/id6746355733 · https://apps.apple.com/us/app/id6751649479 · https://alternativeto.net/software/piccal-calendar-scanner/
- Moneko — FinanceKit en presupuestos 2026: https://moneko.io/blogs/apple-wallet-sync-2026
- MacStories — FinanceKit (iOS 17.4): https://www.macstories.net/linked/financekit-opens-real-time-apple-card-apple-cash-and-apple-savings-transaction-data-to-third-party-apps/
