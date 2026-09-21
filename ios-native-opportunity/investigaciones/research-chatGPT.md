# iOS-Native Opportunity Discovery

## 1\. Executive summary

La investigación cambia bastante la fotografía respecto a 2024–2025. En septiembre de 2026, el ecosistema Apple ofrece una combinación mucho más potente de **datos locales \+ comprensión semántica \+ acciones del sistema**. iOS 27 añade entrada multimodal a Foundation Models y el nuevo framework Music Understanding; iOS 26 había añadido AlarmKit, SpeechAnalyzer y acceso programático a Medication data en HealthKit. Algunas capacidades antes difíciles ahora pueden resolverse sin backend y preservando privacidad. :chatgpt-content-reference{index="0"}

Pero aparece una segunda conclusión igual de importante: **una API nueva no constituye una oportunidad de producto durante mucho tiempo**. En pocos meses han aparecido varias apps casi idénticas alrededor de AlarmKit, screenshot intelligence, inventarios con QR/NFC y extracción mediante IA. Por ejemplo, existen ya CalAlarms y CalendarWake para convertir Calendar en alarmas, ShotInbox/Chista/Screen Actions alrededor de screenshots, y múltiples productos para inventarios de cajas. :chatgpt-content-reference{index="1"}

La ventaja, por tanto, **no puede ser “sé utilizar AlarmKit” o “puedo llamar Foundation Models”**. La unidad interesante es:

> **problema muy específico \+ información que el usuario ya posee \+ interpretación local \+ acción fiable del sistema**

Los patrones de mayor interés que encontré son:

1. **Transformar documentos o imágenes existentes en una acción estructurada.** Un cuadrante laboral se convierte en eventos; una receta se convierte en una secuencia de timers; documentos de viaje se convierten en un pequeño paquete de información accesible offline.  
2. **Utilizar Apple como database implícita.** Location, HealthKit, Calendar, Photos o Music ya contienen la materia prima; la app debe responder una pregunta estrecha, no reconstruir otra base de datos.  
3. **Utilizar IA local para eliminar data entry, no como producto.** Foundation Models resulta especialmente interesante para extracción, clasificación y transformación de información privada; Apple advierte de que el modelo no debe tratarse como un motor de razonamiento complejo ni como una fuente de conocimiento mundial actual. :chatgpt-content-reference{index="2"}  
4. **Usar las system surfaces como parte del producto.** AlarmKit, App Intents, Live Activities, Widgets, Controls y Spotlight pueden hacer que una app pequeña se sienta integrada en iOS en lugar de ser otro destino que el usuario debe recordar abrir.  
5. **Buscar workflows caseros en Shortcuts.** Aquí aparecen algunos de los mejores indicadores de necesidad: usuarios dedicando horas a convertir screenshots de turnos a Calendar, a extraer timers de recetas o a lanzar recordatorios mediante NFC. :chatgpt-content-reference{index="3"}

Después de aplicar los filtros, **no veo quince ideas que merezcan ser construidas**. Veo quince candidatos suficientemente razonables para investigar y, de ellos, cinco que justifican una siguiente ronda de validación:

- **Recipe → Timers**: convertir cualquier receta en una secuencia fiable de timers contextuales.  
- **Shift → Calendar**: interpretar cuadrantes laborales difíciles, detectar cambios y sincronizarlos de forma segura.  
- **Offline Travel Rescue Pack**: convertir screenshots/documentos dispersos en una pequeña carpeta operativa que funciona sin red.  
- **Private Place Memory**: responder automáticamente “¿cuándo estuve aquí por última vez?”.  
- **Music Phrase Practice**: utilizar Music Understanding para eliminar la búsqueda manual de secciones y loops durante la práctica musical.

No interpretaría esta shortlist como una recomendación de empezar a programarlos. **El siguiente paso correcto es intentar matar los cinco de forma barata.**

---

# 2\. Apple capability map

Las clasificaciones *Alta / Media / Baja* de suitability son mi análisis; los hechos sobre acceso, permisos y restricciones proceden de documentación de Apple.

| Framework / API | Qué proporciona | Fuente / histórico | Passive vs active / background | Permission friction | Entitlements | Hardware / región | App Store risk | Indie suitability |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| **HealthKit** | Health samples, workouts, activity, sleep, heart data y numerosos tipos clínicos/fitness | Store persistente; pueden hacerse queries históricas y observer queries | Muchos datos se generan pasivamente; determinados cambios pueden despertar la app mediante background delivery, pero no es un daemon general | Alta | HealthKit capability \+ autorización granular por tipo | Watch/accesorios según dato | Medio-alto por privacidad y health claims | **Alta** para lectura/visualización muy enfocada :chatgpt-content-reference{index="4"} |
| **HealthKit Medications** | Medicaciones anotadas por el usuario y dose events | Datos existentes en Health | Pasivo una vez que Apple Health contiene la información | Alta | HealthKit \+ autorización correspondiente | iOS moderno | Alto si se hacen recomendaciones médicas | **Media/Alta** para companion, no diagnóstico :chatgpt-content-reference{index="5"} |
| **WorkoutKit** | Construcción, preview y scheduling de workouts sincronizables con Watch | No es un store histórico; HealthKit cubre resultados | Activo | Media | Capability estándar | Apple Watch para gran parte del valor | Bajo | **Alta** en nichos deportivos concretos :chatgpt-content-reference{index="6"} |
| **Core Motion** | Accelerometer, gyroscope, magnetometer, pedometer, activity y altitud/barometer según hardware | Algunos servicios mantienen datos agregados; no existe acceso general a un histórico infinito de sensores raw | Predominantemente sensor/system generated; background limitado según API | Baja/Media | Normalmente sin entitlement especial | Hardware correspondiente | Bajo | **Alta** si el job necesita movimiento real :chatgpt-content-reference{index="7"} |
| **Journaling Suggestions** | Lugares, fotos, personas, workouts, media y otros momentos que el sistema propone | No entrega un archivo general de la vida del usuario | **Activo:** el usuario selecciona explícitamente una suggestion antes de que la app reciba detalles | Baja desde UX, pero deliberada | Entitlement de Journaling Suggestions | Dispositivos compatibles | Bajo | **Media**; mucho menos “pasiva” de lo que parece :chatgpt-content-reference{index="8"} |
| **PhotoKit** | Assets, metadata, álbumes y cambios de la biblioteca autorizada | Histórico existente en Photos; puede ser acceso completo o limitado | Biblioteca pasiva; procesamiento lo inicia la app | Media/Alta | Sin entitlement gestionado; privacy usage descriptions | iPhone/iPad | Medio por sensibilidad | **Alta** si se evita pedir acceso total innecesariamente :chatgpt-content-reference{index="9"} |
| **EventKit** | Calendar events y Reminders | Histórico/futuro según store disponible | Datos existentes; background no garantiza ejecución continua | Media | iOS 17+: Calendar write-only o full access; Reminders full access | Sin dependencia especial | Bajo/Medio | **Muy alta** para workflows de acción; write-only reduce fricción :chatgpt-content-reference{index="10"} |
| **Contacts** | Contact store autorizado | Persistente | Datos existentes | Media | iOS moderno permite limited contact access | Sin hardware | Medio | **Media**; interesante como output más que como producto :chatgpt-content-reference{index="11"} |
| **Core Location** | Ubicación, heading, regions, beacons, significant changes y otros location updates | **No** expone un histórico secreto de todos los lugares donde estuvo el usuario; una app debe construir su propio histórico | Puede recibir ciertos updates en background bajo condiciones/capabilities | Alta para acceso persistente | Background Location cuando corresponde | GPS/device; disponibilidad normal global | Medio-alto si se abusa | **Alta** para un job realmente location-native :chatgpt-content-reference{index="12"} |
| **MapKit** | Mapas, POIs, búsqueda, routes, directions, ETA | Datos Apple actuales/remotos; no historial privado del usuario | Activo | Baja | Estándar | Cobertura varía | Bajo | **Alta** como componente |
| **MusicKit** | Apple Music catalog/playback y, con autorización, datos personalizados como recent/recommendations/favorites/playlists | Parte histórica/personalizada, no telemetría ilimitada | Uso activo | Media | Music user authorization | Apple Music/subscription según función | Medio por contenido/licencias | **Media**; no basaría un indie entero en dependencia de catálogo :chatgpt-content-reference{index="13"} |
| **Camera / VisionKit** | Camera capture, document scanner y DataScanner para texto/códigos | Live o contenido elegido por usuario | Activo | Media | Camera permission cuando corresponde | Cámara | Bajo | **Muy alta** para sustituir data entry :chatgpt-content-reference{index="14"} |
| **Vision** | OCR, barcodes, análisis visual y reconocimiento de estructura documental | Imagen/video proporcionados por app | On-device; activo | Baja adicional una vez obtenida imagen | Ninguno especial | Según feature | Bajo | **Muy alta**; iOS 26 mejoró document recognition :chatgpt-content-reference{index="15"} |
| **Core NFC** | NDEF y distintos tipos de tags/contactless | Live; sin histórico propio | Las lecturas de background muestran una notificación y requieren que el usuario la pulse; si está bloqueado debe desbloquear | Baja/Media | NFC capability/formats según uso | NFC-capable iPhone/tags | Bajo/Medio | **Media**; mucho menos “automático” de lo que suelen asumir las ideas NFC :chatgpt-content-reference{index="16"} |
| **Core Bluetooth** | Descubrimiento/comunicación BLE y accesorios | Live | Background posible bajo modos/reglas concretas, no arbitrario | Media | Background mode cuando aplique | Accesorio | Medio | **Media**: excelente si el accesorio ya existe, mala si hay que crear ecosistema |
| **Nearby Interaction / UWB** | Distance/direction ranging entre dispositivos/accesorios compatibles | Live | Foreground libre; background limitado a dispositivos BLE paired/connected o Live Activity desde iOS 18.4 con capability | Media | Uses Nearby Interaction | UWB compatible | Medio | **Media/Baja** sin hardware/distribución propia :chatgpt-content-reference{index="17"} |
| **Apple Watch** | Health sensors, workouts, complications/widgets, haptics y companion experiences | Depende de HealthKit/WorkoutKit/framework utilizado | Muy bueno para passive capture | Puede ser alta en Health | Watch app/capabilities | Apple Watch | Bajo | **Alta** cuando el Watch elimina interacción con el teléfono |
| **HomeKit / Matter** | Homes, rooms, accessories, characteristics, control de dispositivos autorizados | Estado del home; no hay un histórico universal de todo | Algunas events/automations, condicionado al ecosistema | Alta al pedir Home | HomeKit capability | Accesorios/Home Hub según workflow | Medio | **Media**; mercado fragmentado y dependiente de hardware :chatgpt-content-reference{index="18"} |
| **Speech / SpeechAnalyzer** | Transcripción de audio; SpeechAnalyzer introdujo arquitectura moderna on-device para long-form/live use | Audio proporcionado por la app | Live/file; no escucha background universal | Media por micrófono/audio | Standard privacy | Device/model assets | Medio por recording/privacy | **Alta** para captura de información muy concreta :chatgpt-content-reference{index="19"} |
| **Sound Analysis** | Clasificación de cientos de tipos de sonidos o modelos custom | Live/file | Puede analizar streams que posea la app | Media | Ninguno especial más allá del audio source | Micrófono si live | Medio | **Media**, salvo nicho claro :chatgpt-content-reference{index="20"} |
| **ShazamKit** | Matching acústico contra Shazam o custom catalogs | Live/file | Activo | Baja/Media | Normal | Audio source | Bajo | **Media**; muy potente pero jobs limitados :chatgpt-content-reference{index="21"} |
| **Music Understanding — iOS 27** | Key, beats, bars, BPM, phrases, segments, sections, pace, instrument activity y loudness | Analiza `AVAsset` o audio provider | On-device/offline | Baja una vez seleccionado el audio | Sin ML propio | OS compatible | Bajo | **Alta**, especialmente por ser nuevo :chatgpt-content-reference{index="22"} |
| **Foundation Models** | Summarization, extraction, classification, structured generation y desde iOS 27 multimodal input | Solo contexto que proporciona la app; no posee acceso mágico a datos privados | On-device; no background daemon | Baja | Apple Intelligence availability | Dispositivo Apple Intelligence compatible; modelos evolucionan con OS | Medio si se vende como output infalible | **Muy alta como componente**, baja como USP aislada :chatgpt-content-reference{index="23"} |
| **Core ML / Natural Language** | Inferencia local custom; NLP clásico como language/tokenization/NER | Input de la app | On-device | Baja | Ninguno especial | Neural Engine opcional | Bajo | **Alta** cuando se necesita comportamiento determinista/especializado :chatgpt-content-reference{index="24"} |
| **App Intents / Siri** | Expone acciones y entidades a Siri, Shortcuts, Spotlight, Controls y otras system experiences | Datos propios de la app | Invocación por usuario/sistema; no proporciona acceso privado adicional | Baja | Normal | Dependencia de surface | Bajo | **Muy alta** para distribución dentro del OS :chatgpt-content-reference{index="25"} |
| **Visual Intelligence** | Reconoce contenido visual/screen context y puede conectar acciones de apps mediante App Intents | Contexto capturado por usuario | Activo | Baja | App Intent integration | Apple Intelligence compatible | Bajo | **Alta como distribution surface; alta amenaza competitiva** para screenshot utilities :chatgpt-content-reference{index="26"} |
| **WidgetKit / Controls** | Home/Lock Screen widgets y Controls en Control Center/Lock Screen/Action button | Datos propios | System refresh limitado | Baja | Normal | Surface-compatible device | Bajo | **Alta** como retention surface :chatgpt-content-reference{index="27"} |
| **ActivityKit / Dynamic Island** | Live Activities en Lock Screen/Dynamic Island y otras surfaces | Estado propio | Puede actualizarse localmente o mediante push dentro del lifecycle permitido | Baja | Capability estándar | Hardware/surface varies | Bajo | **Alta** para procesos con principio y final :chatgpt-content-reference{index="28"} |
| **Core Spotlight** | Indexa **contenido de la propia app** para búsqueda semántica/system search | Histórico que la app ha indexado | System maintained | Baja | Normal | iOS moderno | Bajo | **Alta** para hacer útil una base local sin abrir la app :chatgpt-content-reference{index="29"} |
| **Notifications** | Local/remote notifications; Time Sensitive | Datos de la propia app | Sí, schedule/push | Media | Critical Alerts necesitan entitlement especial | Normal | Medio si se abusa | **Alta** como output; no constituyen una data source :chatgpt-content-reference{index="30"} |
| **AlarmKit — iOS 26+** | Alarmas reales, repeating/countdown, snooze, custom actions y system presentations | No histórico relevante | El sistema ejecuta el alarm aunque app no esté foreground | Media: autorización explícita | `NSAlarmKitUsageDescription`; no Critical Alerts entitlement | iOS compatible | Bajo si el job realmente necesita alarm | **Muy alta** como building block :chatgpt-content-reference{index="31"} |
| **BackgroundTasks** | App refresh, processing y continued processing | N/A | **No garantiza ejecución arbitraria ni permanente**; el sistema decide scheduling/interruption | Baja | Background capabilities según tipo | Normal | Bajo | **Media**; diseño debe sobrevivir a no ejecutarse :chatgpt-content-reference{index="32"} |
| **Share / Action extensions** | El usuario entrega explícitamente contenido desde otra app | Solo contenido compartido | User initiated | Baja | Extension | Normal | Bajo | **Muy alta** como mecanismo de ingestión sin pedir acceso global |
| **FamilyControls / DeviceActivity / ManagedSettings** | App blocking/monitoring y parental/digital-wellbeing primitives | Datos controlados/sandboxed | System-assisted | Alta | Family Controls entitlement para distribución | Dependencias de autorización | Medio-alto | **Media/Baja** por saturación y entitlement |
| **FamilyActivityData — iOS 27** | Con permiso, installed bundle IDs, visited web domains y activity categories | Datos del device expuestos por API; no asumir historial ilimitado | System-derived | **Alta** | `Family Controls App and Website Usage` entitlement \+ `approvedWithDataAccess` | **Customer use actualmente EU only** | Alto por privacidad | **Media como wildcard** :chatgpt-content-reference{index="33"} |
| **FinanceKit** | Datos financieros locales para productos compatibles | Histórico financiero soportado | System store | Muy alta | Entitlement concedido por Apple, bundle-specific | **US**: Apple Card/Cash/Savings; **UK**: open banking; no soporte documentado para España | Alto | **Baja para este proyecto** :chatgpt-content-reference{index="34"} |
| **PassKit / Wallet** | Passes permitidos a la app, payment/pass integrations | Persistente para sus pases | System managed | Media | Wallet/pass entitlements | Según feature/región | Medio | **Media**; **no** da acceso al Wallet completo ni a todo Apple Pay |
| **SensorKit** | Datasets de sensores de gran riqueza | Histórico según study/sensor | Passive | Muy alta | Apple solo concede reader entitlement a **approved research studies** | Research use | Muy alto para indie normal | **Baja / descartado** :chatgpt-content-reference{index="35"} |
| **WeatherKit** | Current/hourly/daily weather y considerable histórico climático | Incluye más de 50 años de determinadas series estadísticas/históricas | Remote Apple service | Baja | WeatherKit capability | Cobertura variable | Bajo | **Alta como contexto secundario** |
| **RoomPlan** | Room capture 3D, paredes, aperturas y categorías de muebles mediante camera/LiDAR | Scan creado por usuario | Activo | Media | Camera | LiDAR-capable hardware para experiencia completa | Bajo | **Media**: interesante, pero nicho/hardware limitan |
| **Wi-Fi Aware** | Secure peer-to-peer discovery/comms sin AP/internet | Live | No elimina reglas de background | Media | Wi-Fi Aware entitlement/capability | Hardware compatible | Medio | **Baja/Media** salvo job peer-to-peer claro |
| **EnergyKit** | Grid forecasts, tariffs/cleanliness context y energy load integration | Algunos datos históricos de energía | System/service based | Alta | Entitlements específicos | Fuertemente condicionado por región/partners; soporte inicial centrado en EEUU | Alto | **Baja actualmente** |
| **Trust Insights / Channel Sounding — iOS 27** | Señales de riesgo transaccional; ranging más preciso sobre Bluetooth compatible | Live/contextual | Específico | Alta | Entitlements/hardware relevantes | Casos específicos | Alto | **Baja** para un primer indie generalista |

### Conclusión del capability map

Hay cuatro errores particularmente peligrosos para idear productos Apple-native:

- **Journaling Suggestions no es una API pasiva de “la vida del usuario”.**  
- **Core Location no expone el historial completo de ubicaciones del iPhone.**  
- **NFC background no significa ejecutar silenciosamente cualquier workflow al tocar un tag.**  
- **BackgroundTasks no convierte una app iOS en un proceso permanente.**

Y varios terrenos aparentemente valiosos quedan fuera para un producto indie convencional: SensorKit requiere un research study aprobado; FinanceKit sigue restringido geográficamente y necesita entitlement; FamilyActivityData es novedoso pero, actualmente, EU-only y explícitamente autorizado. :chatgpt-content-reference{index="36"}

---

# 3\. Particularly interesting or underused capabilities

### 3.1 Foundation Models multimodal \+ Vision

Esta combinación es probablemente el cambio horizontal más importante.

La oportunidad no es:

> “analizar fotos con IA”.

Es:

> **usuario ya posee un documento imperfecto → Vision conserva estructura → multimodal model interpreta semántica → API nativa ejecuta una acción.**

Foundation Models en iOS 27 admite experiencias multimodales mediante `DynamicProfile` y Apple ha mejorado el modelo on-device. Apple avisa además de que el modelo puede cambiar con nuevas versiones del OS: prompts y comportamiento deben volver a probarse. :chatgpt-content-reference{index="37"}

Eso favorece productos pequeños alrededor de documentos **semiestructurados**, especialmente cuando la exactitud puede verificarse antes de actuar.

### 3.2 AlarmKit

AlarmKit elimina una limitación histórica: una aplicación normal puede programar una **alarma real**, previa autorización, sin necesitar el entitlement extremadamente restringido de Critical Alerts. :chatgpt-content-reference{index="38"}

Pero el mercado ya demuestra que:

> `Calendar + AlarmKit` no es moat.

CalAlarms cuesta 1,99 € y CalendarWake es gratuita; ambas convierten directamente eventos en alarmas. :chatgpt-content-reference{index="39"}

La oportunidad está **upstream**: comprender cuándo debe existir la alarma.

### 3.3 Music Understanding

Este es uno de los frameworks con mejor combinación de:

- nuevo;  
- totalmente on-device;  
- sin backend;  
- output estructurado;  
- valor observable inmediatamente;  
- posibilidades que anteriormente requerían DSP/ML especializado.

Puede devolver beat/bar timestamps, BPM, phrases, segments, sections, key, pace, instrument activity y loudness. :chatgpt-content-reference{index="40"}

La advertencia es que la ventana ya se está cerrando: Music Looper ofrece estructura automática, BPM, loops y práctica; productos establecidos como Moises y Anytune ya monetizan intensamente el workflow del músico. :chatgpt-content-reference{index="41"}

### 3.4 HealthKit Medications

El valor especial no sería construir **otra base de datos de medicamentos**. Sería utilizar la que el usuario ya mantiene en Apple Health para responder un job estrecho.

Ya hay evidencia de edge cases poco elegantes, como usuarios con medicación alterna que quieren que Apple Watch muestre exactamente la pastilla que corresponde ese día. :chatgpt-content-reference{index="42"}

Es técnicamente interesante, pero lo mantendría fuera de la primera apuesta por el coste adicional de privacidad, seguridad y conocimiento del dominio.

### 3.5 FamilyActivityData

Es una novedad importante: con permiso explícito puede devolver bundle identifiers instalados, visited web domains y categorías. En septiembre de 2026 su disponibilidad para consumidores está limitada a dispositivos en la UE con Apple Account de región UE. :chatgpt-content-reference{index="43"}

Precisamente por ser nueva merece observación. Sin embargo, el mercado de screen-time/blockers es extremadamente competitivo y el entitlement convierte la API en una base menos segura para un primer producto.

### 3.6 Visual Intelligence como amenaza competitiva

Visual Intelligence ya puede extraer información visual y, en iOS 27, crear múltiples eventos de Calendar a partir de información detectada. Apple también abre integración mediante App Intents. :chatgpt-content-reference{index="44"}

Por tanto:

> **“foto → Calendar” deja de ser producto.**

Pero:

> **“comprender correctamente un cuadrante laboral, comparar la versión nueva contra la anterior, detectar vacaciones/turnos overnight y sincronizar solo cambios confirmados” todavía puede ser producto.**

Ese contraste aparece varias veces en los candidatos.

---

# 4\. Problems and signals found in the wild

| Señal observada | Evidencia | Qué sugiere |
| :---- | :---- | :---- |
| Trabajadores fotografían su cuadrante porque su sistema no sincroniza Calendar | Un usuario de Amazon Flex describe exactamente este proceso y pasó tres horas intentando automatizarlo; otro usuario en agosto de 2026 sigue intentando interpretar un PDF-tabla con iOS 27 :chatgpt-content-reference{index="45"} | El job existe y sobrevive a Apple Intelligence genérico |
| Los Shortcuts de “schedule screenshot → Calendar” se comparten dentro de comunidades laborales | El Shortcut de Starbucks recibió “life changing”; el autor siguió corrigiéndolo en 2026 :chatgpt-content-reference{index="46"} | Excelente señal de ugly workflow |
| Las tablas destruyen OCR naive | Usuario muestra cómo el OCR pierde la relación espacial turno/día :chatgpt-content-reference{index="47"} | El problema real es interpretación estructural, no OCR |
| Personas extraen manualmente timers de recetas | Un Shortcut escanea recetas HelloFresh, extrae tiempos con regex y genera labels mediante ChatGPT :chatgpt-content-reference{index="48"} | Existe un micro-job claro y repetitivo |
| Usuarios convierten screenshots en reminders/actions | Shortcut de 2026: screenshot → OCR → model → Reminder; el autor afirma usarlo frecuentemente y otros poseen workflows similares :chatgpt-content-reference{index="49"} | Demanda real, pero ya muy competida |
| Viajeros capturan absolutamente todo antes de viajar | Thread de marzo de 2026: \+2.300 votos; boarding passes, hoteles, visas, direcciones, emails porque apps/red fallan :chatgpt-content-reference{index="50"} | Fuerte job de reliability/offline |
| Otros viajeros todavía construyen “offline folders” manuales | Thread de agosto de 2026 describe explícitamente la misma preparación :chatgpt-content-reference{index="51"} | No es comportamiento aislado |
| Usuarios quieren responder “¿cuándo estuve aquí?” | QuantifiedSelf: usuario venía de Excel/Google Maps y quiere controlar su propio histórico para preguntas concretas :chatgpt-content-reference{index="52"} | Job estrecho y Apple-native |
| NFC aparece repetidamente para laundry workflows | Ejemplos de 2025–26 usan tarjetas/tags NFC para timers o persistent nags :chatgpt-content-reference{index="53"} | Hay señal, pero también una gran objeción UX |
| Usuarios de medication tracking encuentran edge cases que Apple no cubre | Caso de schedule alterno/Watch complication :chatgpt-content-reference{index="54"} | HealthKit podría ser database, no competitor |
| Inventarios de cajas generan hacks y gasto | Cajas tiene una review donde el usuario afirma haber probado decenas de apps y haber comprado lifetime casi inmediatamente :chatgpt-content-reference{index="55"} | Existe willingness-to-pay, pero el mercado ya está saturándose |

Un resultado especialmente útil de esta fase es que **Shortcuts no solo revela problemas: también revela cuándo una app es innecesaria**.

En un antiguo thread sobre NFC \+ lavadora, muchos usuarios respondieron esencialmente “dile a Siri que ponga un timer”; ese rechazo es evidencia tan importante como los threads positivos. :chatgpt-content-reference{index="56"}

---

# 5\. Fifteen candidate opportunities

## Candidate 1 — Recipe → reliable timer sequence

**Usuario:** personas que cocinan recetas con múltiples tiempos superpuestos.

**Problema:** encontrar cada duración, recordar qué estaba cronometrando cada timer y activar el siguiente paso interrumpe continuamente la cocina.

**Current workaround:** releer receta, Siri/Clock, varios timers manuales o Shortcuts artesanales.

**Evidencia:** existe un Shortcut explícitamente diseñado para OCR de recetas HelloFresh/Marley Spoon, extracción mediante regex y generación de nombres de timers. :chatgpt-content-reference{index="57"}

**Native Apple leverage:** `Vision/VisionKit + Foundation Models + AlarmKit + ActivityKit + App Intents`.

**What already exists:** Cooking Timer – Step by Step importa recetas web y ofrece multiple timers; Cooking Timer+ cuesta 0,99 €; Recipe Keeper tiene 409 valoraciones en España y 4,7/5, aunque es fundamentalmente un gestor de recetas. :chatgpt-content-reference{index="58"}

**Why Apple doesn't solve it:** Clock resuelve timers; Visual Intelligence entiende contenido; ninguno convierte sistemáticamente una receta arbitraria en un **execution plan temporal verificable**.

**Why an indie could compete:** producto deliberadamente más pequeño que un recipe manager: *“comparte cualquier receta y cocina sus pasos temporizados”*.

**Data entry burden:** **Nulo/Bajo**.  
**Time-to-value:** **inmediato**.  
**Backend:** **Ninguno**.  
**Third-party dependency:** **Baja** si acepta text/photo/web share sin depender de recipe APIs.  
**Monetization:** lifetime unlock o freemium; existe gasto demostrado en cooking utilities y recipe managers.  
**MVP:** import/share; extracción de pasos temporizados; review; start/next timer; Live Activity.  
**Solo-developer feasibility:** **Alta**.  
**Estimated scope:** **Pequeño/Medio**.  
**Would I personally understand this product?:** **Alta**.

**Estado:** **sobrevive**.

---

## Candidate 2 — Work rota → operational calendar

**Usuario:** retail, hospitality, logistics, nurses y otros trabajadores que reciben cuadrantes como screenshot/PDF/table.

**Problema:** el horario existe digitalmente pero no como Calendar data fiable.

**Current workaround:** entrada manual o Shortcut.

**Evidencia:** Amazon Flex, Starbucks y otros usuarios describen exactamente ese workflow; problemas recurrentes incluyen tablas, shifts overnight, days off, duplicates y cambios de formato. :chatgpt-content-reference{index="59"}

**Native Apple leverage:** `Vision document recognition + Foundation Models multimodal + EventKit + AlarmKit + App Intents`.

**What already exists:** ShiftInbox ya importa imágenes/PDF/text/ICS, hace OCR on-device, muestra diffs y sincroniza solo cambios aprobados; modelo gratis \+ lifetime IAP. :chatgpt-content-reference{index="60"}

**Why Apple doesn't solve it:** iOS 27 puede detectar eventos visualmente, pero los reports de usuarios muestran que las tablas completas continúan fallando. :chatgpt-content-reference{index="61"}

**Why an indie could compete:** únicamente especializándose aún más: schedules laborales, reglas conocidas, cambios entre versiones, overnight shifts, vacaciones y confidence/review.

**Data entry burden:** **Nulo/Bajo**.  
**Time-to-value:** **primer uso**.  
**Backend:** **Ninguno**.  
**Dependency:** **Baja**.  
**Monetization:** lifetime purchase parece plausible; ShiftInbox ya utiliza ese modelo.  
**MVP:** screenshot/PDF; parser; validation UI; dedupe/diff; EventKit export.  
**Solo feasibility:** **Alta**.  
**Scope:** **Medio** por long tail de formatos.  
**Founder understanding:** **Alta**.

**Estado:** **sobrevive, pero con una advertencia seria: ya existe un competidor extremadamente cercano.**

---

## Candidate 3 — Screenshot → one next action

**Usuario:** quien utiliza screenshots como “recordármelo luego”.

**Problema:** capturar información es fácil; convertirla en Reminder/Event/contact/action requiere trabajo posterior.

**Evidence:** un Shortcut de marzo de 2026 automatiza precisamente screenshot → OCR → model → Reminder y su creador dice utilizarlo frecuentemente. :chatgpt-content-reference{index="62"}

**Native leverage:** `PhotoKit/Vision/Foundation Models/EventKit/App Intents`.

**Competition:** ShotInbox, Chista y Screen Actions cubren ya screenshots → extraction → Calendar/Reminders/actions. :chatgpt-content-reference{index="63"}

**Apple gap:** se reduce rápidamente por Visual Intelligence.

**Data entry:** **Nulo**.  
**Time-to-value:** **inmediato**.  
**Backend:** **Ninguno** posible.  
**Dependency:** **Baja**.  
**Monetization:** IAP/freemium demostrada por competidores.  
**MVP:** muy pequeño.  
**Solo feasibility:** **Alta**.  
**Founder understanding:** **Alta**.

**Estado:** **no pasa la criba final.** El job es real; la oportunidad diferencial ya no está clara.

---

## Candidate 4 — Calendar event that must actually ring

**Usuario:** personas que pierden citas porque una notification no basta.

**Problema:** algunos eventos merecen una alarma, no otra notificación.

**Native leverage:** `EventKit + AlarmKit`.

**Competition:** CalAlarms cuesta 1,99 € y hace exactamente esto; CalendarWake ofrece una variante gratuita con prep times/Live Activity. :chatgpt-content-reference{index="64"}

**Apple gap:** AlarmKit deja la policy a terceros, pero la solución se replica fácilmente.

**Data entry:** **Nulo**.  
**Time-to-value:** **inmediato**.  
**Backend:** **Ninguno**.  
**Dependency:** **Baja**.  
**Monetization:** pago único probado.  
**Scope:** **Pequeño**.  
**Solo feasibility:** **Muy alta**.  
**Founder understanding:** **Alta**.

**Estado:** **descartado por commoditization**.

---

## Candidate 5 — Calendar-aware wake / leave-by alarm

**Usuario:** quien calcula manualmente cuándo levantarse/prepararse/salir para una cita.

**Problema:** el evento contiene cuándo llegar pero no cuándo comenzar a prepararse.

**Native leverage:** `EventKit + MapKit + WeatherKit + AlarmKit + Live Activities`.

**Competition:** Departd ya promete wake/get-ready/leave times ajustados por tráfico y clima y utiliza AlarmKit. :chatgpt-content-reference{index="65"}

**Data entry:** **Bajo**.  
**Time-to-value:** **primer día**.  
**Backend:** **Mínimo**.  
**Dependency:** **Baja/Media**.  
**Scope:** **Medio**.  
**Founder fit:** **Alta**.

**Estado:** **descartado**: producto atractivo, pero un competidor reciente ya está directamente ocupando el espacio y la fiabilidad background/traffic eleva mucho el coste de soporte.

---

## Candidate 6 — Return deadline rescue

**Usuario:** compradores online que pierden plazos de devolución.

**Problema:** el deadline está enterrado en order pages/screenshots y tiene consecuencias económicas.

**Native leverage:** `Share Extension/Vision/Foundation Models + AlarmKit/Reminders`.

**Competition:** Return Before ya procesa screenshots con fechas explícitas, programa reminders y utiliza AlarmKit para el último día; cobra mediante suscripción. :chatgpt-content-reference{index="66"}

**Data entry:** **Bajo**.  
**Time-to-value:** **inmediato**.  
**Backend:** **Ninguno/Mínimo**.  
**Dependency:** **Baja** si no se scrappean retailers.  
**Scope:** **Pequeño**.  
**Founder fit:** **Alta**.

**Estado:** **descartado como idea independiente**. El job es bueno; la oportunidad ya está explícitamente explotada.

---

## Candidate 7 — Offline travel rescue pack

**Usuario:** viajeros que dependen de 4–8 apps, emails, PDFs y screenshots durante el viaje.

**Problema:** la información crítica existe pero puede ser imposible de encontrar justamente cuando no hay red o una app deja de responder.

**Current workaround:** screenshots, álbum separado, Files, Notes, papel o incluso un WhatsApp consigo mismo/la pareja. :chatgpt-content-reference{index="67"}

**Evidence:** el thread “I started screenshotting EVERYTHING” superó 2.300 votos; otro de agosto de 2026 recomienda explícitamente una offline folder con hotel, tickets, insurance y transport info. :chatgpt-content-reference{index="68"}

**Native leverage:** `Share Extension + Vision/Foundation Models + local persistence + MapKit + EventKit + Spotlight`.

**Competition:** Travel Binder ofrece funcionamiento offline/no-account y trip timeline; otra app TravelBinder cuesta 2,99 €. :chatgpt-content-reference{index="69"}

**Why Apple doesn't solve it:** Wallet cubre determinados passes, Files documentos y Calendar eventos; nadie garantiza un *operational view* sobre todo ese material heterogéneo.

**Potential indie gap:** **no construir un travel planner**. Solo *“lo que necesito cuando todo falla”*: QR, confirmation, local-language address, phone, time, map location.

**Data entry:** **Bajo**, vía Share.  
**Time-to-value:** **antes/primer día del viaje**.  
**Backend:** **Ninguno**.  
**Dependency:** **Baja**.  
**Monetization:** lifetime/trip unlock plausible; competidores ya cobran.  
**MVP:** trip; share screenshot/PDF; extract 4–5 entity types; offline cards; Spotlight/quick access.  
**Solo feasibility:** **Alta**.  
**Scope:** **Medio**.  
**Founder understanding:** **Alta**.

**Estado:** **sobrevive**, siempre que se mantenga mucho más estrecho que “trip planner”.

---

## Candidate 8 — Private place memory

**Usuario:** alguien que quiere recordar restaurantes, tiendas, viajes o cuándo visitó un lugar sin check-ins manuales.

**Problema:** “sé que estuve aquí antes, pero ¿cuándo?”

**Current workaround:** Google Maps, photos, Excel, Swarm o varias apps.

**Evidence:** un usuario de QuantifiedSelf describe exactamente “when was the last time I've been here?” y comenta que antes llevaba datos en Excel; otros utilizan varias apps simultáneamente. :chatgpt-content-reference{index="70"}

**Native leverage:** `Core Location + MapKit + local persistence + Spotlight/App Intents`.

**Competition:** Last Time I Was Here ya promete exactamente esta pregunta y ofrece optional background capture; está disponible gratis \+ IAP. :chatgpt-content-reference{index="71"}

**Apple gap:** Apple Maps/Photos recuerdan lugares bajo sus propios modelos de UX, pero no proporcionan una query-first personal place ledger.

**Indie gap:** privacidad, on-device, cero social graph, query simple.

**Data entry:** **Nulo** después del onboarding.  
**Time-to-value:** idealmente **primera semana**, aunque esta es una debilidad frente a otros candidatos.  
**Backend:** **Ninguno**.  
**Dependency:** **Baja**.  
**Monetization:** one-time/lifetime plausible.  
**MVP:** automatic visits; place resolution; timeline; “last here”; hide home/work.  
**Solo feasibility:** **Media/Alta**.  
**Scope:** **Medio** por location heuristics/battery.  
**Founder understanding:** **Alta**.

**Estado:** **sobrevive por el patrón, no porque esté desocupado.**

---

## Candidate 9 — Photo-first box inventory

**Usuario:** quien se muda o guarda objetos en trastero/cajas.

**Problema:** saber qué está dentro de una caja cerrada.

**Native leverage:** `Camera + Vision/Foundation Models multimodal + QR/NFC + Spotlight`.

**Competition:** MOVINGBOXES, Cajas, Scan Your Boxes, Boxy y SmartBox ya cubren el espacio; varias han añadido AI photo recognition, QR, NFC, Spotlight y Siri. Boxy cobra 2,99 €/mes, 22,99 €/año o 59,99 € lifetime. :chatgpt-content-reference{index="72"}

**Data entry:** **Medio**, incluso usando reconocimiento visual.  
**Time-to-value:** **primer día**.  
**Backend:** **Ninguno/Mínimo**.  
**Dependency:** **Baja**.  
**Monetization:** claramente probada.  
**Solo feasibility:** **Alta**.  
**Scope:** **Medio**.  
**Founder understanding:** **Alta**.

**Estado:** **descartado**: buena necesidad, mala ventana competitiva y uso episódico.

---

## Candidate 10 — Warranty evidence pack

**Usuario:** consumidor que pierde receipt/warranty/serial justo cuando algo falla.

**Problema:** los documentos existen pero se encuentran dispersos.

**Native leverage:** `VisionKit + Vision + Foundation Models + Spotlight + Reminders`.

**Competition:** existe un número considerable de warranty trackers con receipt scanning, OCR, serials y reminders; algunos cobran aproximadamente $1.99/mes o $14.99/año. :chatgpt-content-reference{index="73"}

**Data entry:** **Bajo/Medio** por cada compra.  
**Time-to-value:** débil: el payoff puede tardar meses/años.  
**Backend:** **Ninguno**.  
**Dependency:** **Baja** si no se interpretan políticas externas.  
**Founder fit:** **Alta** técnicamente, **Media** como product judge si se intenta interpretar cobertura legal.

**Estado:** **descartado principalmente por time-to-value y hábito de captura**.

---

## Candidate 11 — Expiry/date capture

**Usuario:** quien gestiona productos/documentos con caducidad.

**Problema:** el dato está impreso pero el teléfono no recuerda la fecha.

**Native leverage:** `Vision + Reminders`.

**Competition:** ExpiryGuard y numerosas variantes hacen date tracking; incluso la versión simple obliga a crear cada item/cantidad/categoría. :chatgpt-content-reference{index="74"}

**Data entry:** **Medio** recurrente.  
**Time-to-value:** **días/semanas**.  
**Backend:** **Ninguno**.  
**Scope:** **Pequeño**.  
**Founder understanding:** **Alta**.

**Estado:** **descartado**. El coste continuo de alimentar la database viola una de las hipótesis centrales de esta investigación.

---

## Candidate 12 — Spoken commitment → system action

**Usuario:** quien sale de una reunión/llamada con varios “yo hago X el jueves”.

**Problema:** commitments pronunciados se pierden entre transcript y task manager.

**Native leverage:** `SpeechAnalyzer + Foundation Models + EventKit/Reminders + App Intents`.

**Competition:** en 2026 ya existen múltiples transcription/task extractors; además Apple usa SpeechAnalyzer en sus propias experiencias de Notes/Voice Memos/Journal. :chatgpt-content-reference{index="75"}

**Data entry:** **Nulo** durante la conversación.  
**Time-to-value:** **inmediato**.  
**Backend:** **Ninguno** técnicamente.  
**Dependency:** **Baja**.  
**Scope:** **Medio**.  
**Founder fit:** **Alta**.

**Estado:** **descartado como producto genérico**. Podría reabrirse únicamente alrededor de un workflow muchísimo más estrecho.

---

## Candidate 13 — Medication schedule edge-case companion

**Usuario:** alguien que ya utiliza Apple Health Medications pero posee schedules alternos/variables que la UX estándar representa mal.

**Problema:** Apple almacena el tratamiento, pero determinados usuarios siguen sin poder responder fácilmente “¿qué exactamente me toca ahora?”.

**Evidence:** usuario con dos medicamentos en días alternos quiere que Watch muestre la pastilla correcta en vez del primer item del log. :chatgpt-content-reference{index="76"}

**Native leverage:** `HealthKit Medications + Apple Watch + Widgets/App Intents`.

**Competition:** Cadence ofrece medicamentos ilimitados gratis y un Pro de pago único, con Watch/Health-oriented functionality. :chatgpt-content-reference{index="77"}

**Why interesting:** a diferencia de trackers tradicionales, podría **no mantener otra drug database** y apoyarse en el dato existente.

**Data entry:** **Nulo/Bajo** si HealthKit realmente contiene lo necesario.  
**Time-to-value:** **inmediato** para el usuario objetivo.  
**Backend:** **Ninguno**.  
**Dependency:** **Baja**.  
**Permission friction:** **Alta**.  
**App Store/domain risk:** **Alto**.  
**Solo feasibility:** técnica **Alta**, producto **Media**.  
**Founder understanding:** **Media/Baja** por dominio health.

**Estado:** **wildcard, no finalist**.

---

## Candidate 14 — Music phrase practice map

**Usuario:** instrumentistas/cantantes/bailarines que practican repetidamente fragmentos específicos.

**Problema:** durante el ensayo se pierde tiempo localizando, marcando y repitiendo manualmente verse/chorus/phrase/bar.

**Native leverage:** `Music Understanding + AVFoundation + App Intents/Watch/Controls`.

Music Understanding puede proporcionar beats, bars, phrases, segments y sections totalmente on-device. :chatgpt-content-reference{index="78"}

**Competition:** Moises tiene 1,9k ratings en España, 4,7/5 y Premium de 6,99 €/mes o 49,99 €/año; Anytune tiene 559 ratings y 4,7/5; Music Looper ya ofrece automatic song structure y loops. :chatgpt-content-reference{index="79"}

**Why Apple doesn't solve it:** Apple proporciona el análisis; no una focused rehearsal UX.

**Indie angle:** no stems, no social, no “AI coach”: seleccionar audio → recibir phrase map → practicar inmediatamente.

**Data entry:** **Bajo**.  
**Time-to-value:** **inmediato**.  
**Backend:** **Ninguno**.  
**Dependency:** **Baja** usando audio importado; DRM/licensing limita ciertos sources.  
**Monetization:** el mercado musical demuestra willingness-to-pay significativa.  
**MVP:** import; analyze; waveform/sections; tap section to loop; speed.  
**Solo feasibility:** **Alta**.  
**Scope:** **Medio**.  
**Founder understanding:** **Media**: se necesita bastante user discovery con músicos.

**Estado:** **sobrevive fundamentalmente por la nueva capability window**.

---

## Candidate 15 — Physical-object reminder trigger

**Usuario:** personas que olvidan tareas posteriores a iniciar una máquina/proceso: lavadora, dishwasher, fermentación, riego, etc.

**Problema:** al iniciar algo físico también hay que acordarse de una acción futura.

**Current workaround:** Siri, timer, Reminder o NFC Shortcuts.

**Evidence:** hay múltiples ejemplos de NFC en washing machines para crear timers/reminders y usuarios intentando conseguir persistent nags. :chatgpt-content-reference{index="80"}

**Native leverage:** `NFC/App Intents + AlarmKit`.

**But:** Core NFC background scanning no permite la fantasía de “tap → app ejecuta silenciosamente”; el sistema presenta una notification y el usuario debe entrar. :chatgpt-content-reference{index="81"}

Además, otro thread desmonta brutalmente la proposition: muchos usuarios consideran más fácil decir simplemente “Siri, timer 60 minutes”. :chatgpt-content-reference{index="82"}

**Data entry:** **Bajo**, pero requiere setup físico.  
**Time-to-value:** **inmediato**.  
**Backend:** **Ninguno**.  
**Dependency:** **Baja**.  
**Scope:** **Pequeño**.  
**Founder understanding:** **Alta**.

**Estado:** **descartado como standalone app**. Puede ser una feature excelente, no veo todavía producto.

---

# 6\. Candidates rejected early

### Real-time sleep-stage → HomeKit automation

Atractiva técnicamente, pero la premisa de disponer de una señal HealthKit fiable y continua del sleep stage durante la propia noche no está suficientemente respaldada para basar un producto consumer en ella. **Kill.**

### Generic Screen Time blocker

La nueva FamilyActivityData es interesante, pero blockers como categoría están extremadamente explotados; además el nuevo data access requiere permiso explícito, entitlement y actualmente es EU-only. :chatgpt-content-reference{index="83"}

### FinanceKit personal finance app para España

No. FinanceKit documenta actualmente EEUU y Reino Unido, con entitlement concedido por Apple. **No hay base pública documentada para construir el producto para España.** :chatgpt-content-reference{index="84"}

### Consumer product sobre SensorKit

No. Apple concede el reader entitlement únicamente a research studies aprobados. :chatgpt-content-reference{index="85"}

### “Passive life journal” basado en Journaling Suggestions

No funciona como se suele imaginar. El usuario debe abrir el picker y seleccionar la suggestion; la aplicación no recibe silenciosamente un feed de la vida de la persona. :chatgpt-content-reference{index="86"}

### Full Wallet / Apple Pay transaction analyzer

No existe una API pública general que permita a una app indie leer todo Wallet o todas las transacciones Apple Pay. PassKit está deliberadamente scopeado. **Kill.**

### WhatsApp / iMessage / Mail / notification history personal assistant

No existe acceso público general al contenido de otras apps, historial global de notifications, WhatsApp, iMessage o Mail. Share extensions pueden recibir lo que el usuario comparta explícitamente; eso es un modelo de producto distinto.

### Parking-sign AI lawyer

Vision puede leer signs, pero interpretar legalmente restricciones variables por municipio/jurisdicción convierte un agradable computer-vision demo en un producto de fiabilidad/legal-domain mucho más complicado. Además ya existen apps dedicadas.

### Generic photo organizer

Vision \+ Foundation Models hacen muy sencilla la demo y muy difícil el moat. Photos ya tiene enormes ventajas de integración y corpus histórico.

### “AI meeting notes”

SpeechAnalyzer \+ Foundation Models lo hacen técnicamente fácil; precisamente por ello está muy competido. Sin un job posterior extremadamente concreto no cumple el filtro.

---

# 7\. Comparative analysis

| Candidate | Evidencia | Apple-native leverage | Data entry | Competencia | Backend | Time-to-value | Solo dev | Principal problema |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| Recipe → timers | **Buena** | **Muy alta** | Bajo | Media | Ninguno | Inmediato | Alta | Evitar convertirse en recipe manager |
| Shift → calendar | **Muy buena** | **Muy alta** | Bajo | **Alta/directa** | Ninguno | Inmediato | Alta | ShiftInbox \+ Apple encroachment |
| Screenshot → action | Muy buena | Alta | Nulo | **Muy alta** | Ninguno | Inmediato | Alta | Commoditized |
| Calendar → alarm | Buena | Alta | Nulo | **Muy alta** | Ninguno | Inmediato | Muy alta | Feature, no moat |
| Smart leave/wake | Buena | Muy alta | Bajo | Alta | Mínimo | Primer día | Media | Departd \+ reliability |
| Return deadline | Buena | Alta | Bajo | Alta | Ninguno | Inmediato | Alta | Direct competitor |
| Offline travel rescue | **Muy buena** | Alta | Bajo | Media/Alta | Ninguno | Inmediato en viaje | Alta | Debe evitar feature creep |
| Private place memory | Buena | **Muy alta** | Nulo | Media/Alta | Ninguno | Semana | Media/Alta | Location/battery \+ direct apps |
| Box inventory | Buena | Alta | **Medio** | **Muy alta** | Ninguno | Primer día | Alta | Episódico \+ crowded |
| Warranty pack | Media | Alta | Bajo/Medio | Alta | Ninguno | Lento | Alta | Delayed payoff |
| Expiry capture | Media | Media | **Medio repetido** | Alta | Ninguno | Lento | Alta | Otra database |
| Spoken commitments | Buena | Alta | Nulo | **Muy alta** | Ninguno | Inmediato | Alta | Generic AI utility |
| Medication edge cases | Buena pero estrecha | **Muy alta** | Nulo | Media | Ninguno | Inmediato | Media | Health/safety/domain |
| Music phrase practice | Media/Buena | **Muy alta y nueva** | Bajo | Alta | Ninguno | Inmediato | Alta | Competitors moving fast |
| NFC physical reminder | Buena | Alta | Bajo | Siri/Shortcuts | Ninguno | Inmediato | Muy alta | Existing UX may be better |

### Qué cambia después de aplicar los kill criteria

La mayoría de los candidatos que parecían atractivos técnicamente mueren por uno de cuatro motivos:

1. **La feature ya se ha commoditizado.** AlarmKit → Calendar alarm.  
2. **Apple absorbe rápidamente el primitive.** Visual Intelligence → screenshot/calendar.  
3. **La fricción de data entry reaparece.** Expiry/warranty/inventory.  
4. **La tecnología es más interesante que el problema.** NFC household automation.

Eso deja como oportunidades más interesantes aquellas donde la dificultad está en **interpretar correctamente un objeto existente** o **crear una experiencia especializada alrededor de un dato que Apple ya recoge**.

---

# 8\. Final five

No considero este orden un ranking. Los cinco merecen una siguiente investigación por motivos distintos.

## Finalist 1 — Recipe → Timers

### Problem in one sentence

Una receta contiene todos los tiempos necesarios, pero durante la cocina el usuario todavía debe encontrarlos, interpretarlos y crear/recordar timers manualmente.

### Why this survived

Es pequeño, fácil de explicar, recurrente, cero-backend, consume información existente y proporciona valor en la primera sesión.

### Native advantage

`Vision + Foundation Models + AlarmKit + Live Activities + App Intents`.

AlarmKit es especialmente importante porque el output del parsing se convierte en una primitive fiable del sistema, no en notifications improvisadas. :chatgpt-content-reference{index="87"}

### Existing evidence

Ya hay usuarios construyendo exactamente la parte difícil mediante OCR \+ regex \+ ChatGPT en Shortcuts. :chatgpt-content-reference{index="88"}

### Existing competitors

Cooking Timer – Step by Step ya importa una receta web y gestiona varios timers; Recipe Keeper y numerosos cooking tools cubren áreas adyacentes. :chatgpt-content-reference{index="89"}

### Why there may still be room

La oportunidad no es guardar recetas.

El posicionamiento sería:

> **“Send me the recipe. I’ll handle the timing.”**

Sin cookbook, meal planning, shopping lists ni social.

Especialmente interesante sería admitir **foto/screenshot/papel**, donde los recipe managers basados en URL pierden ventaja.

### Main risk

Que Siri \+ multiple timers sea “suficientemente bueno” para la mayoría y que el parsing automatizado ahorre menos esfuerzo del esperado.

### Cheapest validation

No programaría AlarmKit todavía.

Tomaría 30 recetas reales —web, screenshot y papel— y construiría manualmente un prototype que:

1. devuelve únicamente timed steps;  
2. muestra cómo se solapan;  
3. permite iniciar la ejecución.

Después probaría el concepto con 10–15 personas que cocinen varias veces por semana.

La pregunta es:

> “¿Quieres volver a utilizar esto en tu próxima receta?”

No “¿te parece buena idea?”.

### MVP shape

- Share/photo recipe.  
- Extract timed steps locally.  
- Review/edit.  
- Run named timer queue.  
- Live Activity con qué ocurre ahora y qué viene después.

### Monetization evidence

Cooking utilities cobran; Cooking Timer+ cuesta 0,99 €, Recipe Keeper monetiza mediante IAP y productos más complejos del espacio cobran mucho más. :chatgpt-content-reference{index="90"}

La hipótesis más coherente para un micro-producto sería **free limited usage \+ lifetime unlock**, no subscription artificial.

### First 100 users

- Publicar inicialmente el workflow/prototype en `r/shortcuts`, donde ya existe la necesidad.  
- `r/Cooking`, bread/baking communities y meal-prep communities.  
- Vídeos cortos mostrando: *photo recipe → timers ready in 5 seconds*.  
- Contactar directamente a quienes mantienen Shortcuts similares.

### Founder fit

Muy alto. No exige ser chef profesional para distinguir:

- parsing correcto;  
- timer equivocado;  
- step ordering;  
- UX demasiado lenta;  
- alert que llega tarde;  
- error recoverability.

Es principalmente un problema de producto mobile y sistemas.

---

## Finalist 2 — Shift → Calendar

### Problem in one sentence

Miles de trabajadores reciben un horario digital que su teléfono no puede utilizar como calendario operativo.

### Why this survived

La evidencia de problema es extraordinariamente concreta. Los usuarios no solo se quejan: **construyen y mantienen software casero para resolverlo.**

Amazon Flex, Starbucks y otros empleados publican Shortcuts y vuelven meses después para reparar nuevos edge cases. :chatgpt-content-reference{index="91"}

### Native advantage

`Vision document structure + Foundation Models multimodal + EventKit + AlarmKit`.

### Existing evidence

Un ejemplo de agosto de 2026 es especialmente revelador: el usuario afirma que iOS 27 puede acercarse usando screenshots parciales, pero sigue fallando con el PDF tabular original. :chatgpt-content-reference{index="92"}

Eso identifica exactamente dónde está el gap entre **general intelligence** y **productized workflow**.

### Existing competitors

ShiftInbox ya hace una gran parte de la tesis: images/PDF/text/ICS, OCR local, review y diff de changes. :chatgpt-content-reference{index="93"}

### Why there may still be room

Esta es precisamente la pregunta que necesita validación.

Las posibles wedges serían:

- un vertical laboral concreto;  
- parsing mucho más robusto de roster grids;  
- shift changes;  
- alarm/wake setup;  
- shared/family calendar;  
- recurring roster-format learning.

Pero **no asumiría** que esas ventajas bastan.

### Main risk

ShiftInbox puede significar que llegamos tarde, no que hemos encontrado mercado.

Además, Apple continuará mejorando Visual Intelligence.

### Cheapest validation

Antes de código de producción:

- recopilar 50 cuadrantes anonimizados de 5–10 employers/sistemas;  
- medir cuánto falla Visual Intelligence/iOS 27;  
- probar ShiftInbox contra esos mismos documentos;  
- entrevistar a usuarios que ya mantienen un Shortcut.

Solo seguiría si aparece una **clase repetible de fallo que ShiftInbox tampoco resuelva bien**.

### MVP shape

Un único vertical inicialmente:

> screenshot/PDF → candidate shifts → review → Calendar.

Nada de timesheets, payroll, teams o employee management.

### Monetization evidence

ShiftInbox ya utiliza free trial/imports \+ lifetime Pro, demostrando al menos que un developer considera plausible monetización directa en este workflow. :chatgpt-content-reference{index="94"}

### First 100 users

No intentaría ASO genérico.

Elegiría **un employer/ecosystem concreto** cuya aplicación no exporta Calendar y distribuiría directamente en su subreddit/Facebook group/community.

El Starbucks Shortcut es un ejemplo de cómo un micro-nicho puede diseminar el workflow orgánicamente. :chatgpt-content-reference{index="95"}

### Founder fit

**Muy alto.** Parsing, calendar semantics, diffing, review UX, edge cases y system integration son problemas que un Senior iOS Engineer puede juzgar directamente.

---

## Finalist 3 — Offline Travel Rescue Pack

### Problem in one sentence

Cuando un viajero necesita urgentemente una reserva, QR, dirección o confirmation code, esa información suele estar repartida entre apps que pueden no cargar.

### Why this survived

Aquí encontramos uno de los comportamientos manuales más evidentes de toda la investigación: **la gente ya construye el producto con screenshots y carpetas.**

El thread de marzo de 2026 obtuvo más de 2.300 votos y comentarios describiendo exactamente el mismo workaround. :chatgpt-content-reference{index="96"}

### Native advantage

`Share Extension + Vision/Foundation Models + offline local storage + Spotlight + MapKit`.

La integración iOS podría ser mejor que un travel SaaS: compartir desde cualquier app y desaparecer.

### Existing competitors

Travel Binder ofrece timeline, documents, QR codes y offline/no-account; hay además otros travel organizers recientes. :chatgpt-content-reference{index="97"}

### Why there may still be room

La mayor posibilidad de diferenciación consiste precisamente en **eliminar features**.

No sería:

> “planifica tus vacaciones”.

Sería:

> **“Guarda aquí lo que no puede fallar cuando llegues.”**

Ese cambio permitiría onboarding cero y un UX centrado en recuperación:

- código;  
- hora;  
- nombre;  
- dirección;  
- QR;  
- contacto.

### Main risk

Que “álbum de screenshots” sea ya suficientemente eficaz y cualquier clasificación adicional constituya overengineering.

### Cheapest validation

Crear un prototype estático de “Travel Rescue” utilizando **los screenshots reales de 10 viajeros**.

Pedirles que busquen:

> “la dirección del hotel”,  
> “el booking reference”,  
> “el QR del tren”

primero en su teléfono normal y después en el prototype.

Aquí se puede medir literalmente tiempo y errores.

### MVP shape

- Trip.  
- Share screenshot/PDF.  
- Local extraction.  
- Five card types.  
- Offline quick screen.

Nada de recommendations, booking, itinerary planning, expense tracking ni email scraping.

### Monetization evidence

TravelBinder se vende por 2,99 €; Travel Binder utiliza free \+ Pro. :chatgpt-content-reference{index="98"}

Pago único o “unlock unlimited trips” tendría más sentido que subscription inicialmente.

### First 100 users

- `r/travel`, `r/TravelHacks`, `r/onebag`.  
- Responder a threads donde ya recomiendan screenshot folders.  
- Vídeo demostrando una búsqueda en airplane mode.  
- Viajeros frecuentes / digital-nomad communities.

### Founder fit

Alto. No exige expertise en airlines: el producto no interpreta fares, visas ni reglas legales. Organiza información explícita que el usuario ya posee.

Ese boundary es fundamental.

---

## Finalist 4 — Private Place Memory

### Problem in one sentence

El teléfono sabe dónde está ahora, pero no existe una experiencia Apple enfocada en responder de forma privada y directa “¿cuándo estuve en este sitio por última vez?”.

### Why this survived

El problema tiene una forma extraordinariamente sencilla y la captura puede ser pasiva.

### Native advantage

`Core Location + MapKit + Spotlight/App Intents`.

No tendría sentido igual como web app.

### Existing evidence

Usuarios de quantified-self construyen historial propio para poder responder precisamente ese tipo de pregunta y algunos recurren a varias apps simultáneamente. :chatgpt-content-reference{index="99"}

### Existing competitors

Aquí apareció una señal que reduce considerablemente mi entusiasmo: **Last Time I Was Here** ya hace exactamente esto, incluyendo optional background capture. :chatgpt-content-reference{index="100"}

También existen productos más amplios de automatic-life logging.

### Why there may still be room

Solo si entrevistas muestran problemas fuertes con:

- battery;  
- incorrect place matching;  
- privacy;  
- clutter;  
- inability to query naturally;  
- data portability;  
- historical import from Photos.

Si no, hay que matarlo.

### Main risk

Que el problema exista pero sea demasiado pequeño para sostener comportamiento recurrente y monetización, y que la solución directa ya esté suficientemente cubierta.

### Cheapest validation

Instalar los principales competidores y utilizarlos durante dos semanas antes de escribir código.

Después entrevistar a 15 usuarios de quantified-self / location-history sobre **la última vez que realmente necesitaron buscar un lugar histórico**.

Frecuencia importa muchísimo aquí.

### MVP shape

- automatic meaningful visits;  
- place grouping;  
- “last here”;  
- searchable timeline;  
- privacy exclusions.

### Monetization evidence

Last Time I Was Here utiliza IAP; apps más antiguas de automatic location tracking también han monetizado premium functionality. :chatgpt-content-reference{index="101"}

### First 100 users

`r/QuantifiedSelf`, privacy/self-tracking communities y personas migrando de Google Timeline-type workflows.

### Founder fit

Alto técnicamente y alto conceptualmente. La principal dificultad está precisamente en mobile product engineering: battery, heuristics, permission education y privacy UX.

---

## Finalist 5 — Music Phrase Practice

### Problem in one sentence

El músico quiere practicar el mismo fragmento veinte veces, pero todavía dedica demasiados gestos a encontrar, marcar y volver al fragmento correcto.

### Why this survived

No porque la competencia sea baja —no lo es— sino porque **la plataforma acaba de cambiar**.

Apple proporciona por primera vez análisis musical on-device de alto nivel, incluyendo beat/bar timestamps y estructura jerárquica de phrases/segments/sections. :chatgpt-content-reference{index="102"}

Hace dos años construir esto bien exigía considerable signal-processing/ML work o una dependencia externa.

### Native advantage

`Music Understanding + AVFoundation + Apple Watch/App Intents`.

### Existing competitors

Este es el riesgo central:

- Moises: 4,7/5, \~1.900 ratings en España; 6,99 €/mes o 49,99 €/año Premium. :chatgpt-content-reference{index="103"}  
- Anytune: 4,7/5 y 559 ratings; loops, slow-down, markers y practice tooling. :chatgpt-content-reference{index="104"}  
- Music Looper ya añadió automatic song structure, BPM y named loops. :chatgpt-content-reference{index="105"}

La ventana técnica es real y los competidores también lo saben.

### Why there may still be room

No intentar competir contra Moises.

Producto hipotético:

> **“Open a track. Tap the phrase. Practice.”**

La apuesta es que una herramienta mucho más pequeña puede ganar un microsegmento que considera Moises excesivo.

### Main risk

Que automatic phrase detection sea una feature y no un producto, especialmente porque las apps incumbentes pueden incorporar el mismo framework.

### Cheapest validation

No construir una library, account ni practice tracker.

Hacer un prototype capaz de analizar diez canciones y probar con:

- profesores de instrumento;  
- cantantes;  
- guitarristas;  
- pianistas;  
- bailarines.

Comparar número de gestos/tiempo para establecer un loop contra Anytune/Moises.

### MVP shape

- File import.  
- Automatic structure.  
- Tap-to-loop.  
- Slow-down.  
- Save 3–5 practice regions.

### Monetization evidence

Aquí es particularmente fuerte: Moises demuestra subscription spend considerable y Anytune lleva años vendiendo advanced practice functionality. :chatgpt-content-reference{index="106"}

Para el micro-producto probaría **one-time unlock**, no intentaría copiar los economics de Moises.

### First 100 users

Una disciplina primero, no “músicos”:

> por ejemplo, guitarristas que aprenden solos de oído.

Después:

- subreddit correspondiente;  
- profesores de YouTube;  
- music-teacher communities;  
- TestFlight compartido por teachers con alumnos.

### Founder fit

**Media**, no alta. Técnicamente encaja perfectamente; para juzgar la calidad del producto hace falta convivir con músicos reales.

Esto es exactamente lo que la fase de validation debe resolver.

---

# 9\. Three wildcards

## Wildcard 1 — HealthKit Medication Companion

Está a punto de quedar descartada por health-domain risk, pero tiene una propiedad extraordinariamente interesante:

> **la database compleja ya existe y la mantiene Apple Health.**

La app podría atacar únicamente edge cases como schedules alternos, “qué me toca ahora”, travel/timezone display o una mejor Watch surface, sin convertirse en medication database.

HealthKit ha abierto APIs específicas alrededor de medicamentos y dose events, y existen usuarios que todavía encuentran problemas muy concretos en la UX estándar. :chatgpt-content-reference{index="107"}

**Por qué no olvidarla:** combinación excepcional de existing data \+ Watch \+ immediate value.

**Por qué no la construiría todavía:** health/safety/privacy y founder-domain fit.

---

## Wildcard 2 — EU personal digital-activity lens

No construiría otro app blocker.

Pero `FamilyActivityData` merece ser vigilada porque representa una ampliación real de lo que una consumer app puede conocer: con autorización puede acceder a installed applications, visited web domains y categories; actualmente el customer API es EU-only. :chatgpt-content-reference{index="108"}

Una futura oportunidad podría ser un job muchísimo más concreto que “usa menos el móvil”, por ejemplo responder una pregunta privada y puntual a partir de esos datos.

**Por qué no olvidarla:** capability nueva, geográficamente interesante y aún en fase temprana de product discovery.

**Por qué no finalista:** entitlement risk \+ privacy \+ crowded digital-wellbeing market.

---

## Wildcard 3 — Physical trigger → persistent real-world follow-up

Los NFC laundry hacks llevan años apareciendo y continúan en 2025–26. :chatgpt-content-reference{index="109"}

AlarmKit arregla una parte que anteriormente era bastante incómoda: después de iniciar un proceso físico puede existir ahora una alarma del sistema fiable. :chatgpt-content-reference{index="110"}

No veo todavía un standalone product, porque Siri suele ser más rápida y Core NFC background tiene interacción adicional. :chatgpt-content-reference{index="111"}

**Por qué no olvidarla:** puede aparecer un job físico donde NFC no sea gimmick —especialmente cuando el objeto identifica automáticamente *qué workflow* debe comenzar— y entonces `physical object → intent → AlarmKit` se vuelve una arquitectura interesante.

---

# 10\. Important platform constraints discovered

### No existe acceso general al contenido “porque está en el iPhone”

No basaría ninguna idea en leer pasivamente:

- iMessage/SMS;  
- WhatsApp;  
- Mail;  
- notification history de otras apps;  
- Safari history;  
- contenido arbitrario de otras apps;  
- Wallet completo;  
- Apple Pay transaction history universal.

Share extensions y explicit user selection son mecanismos válidos; acceso silencioso no.

### Visual Intelligence está absorbiendo la capa más sencilla

Screenshots → events/actions será cada vez menos defendible como aplicación independiente. La oportunidad debe estar en el **domain-specific interpretation/workflow** posterior. :chatgpt-content-reference{index="112"}

### Foundation Models no debe convertirse en source of truth

Apple posiciona el modelo para language understanding/generation y ahora multimodality, pero sus propias recomendaciones remarcan limitaciones en complex reasoning y knowledge. Además el modelo cambia con nuevas versiones del OS. :chatgpt-content-reference{index="113"}

Para cualquier candidato final:

> **deterministic parsing where possible → model interpretation where useful → user verification before destructive/external action.**

### Background execution debe diseñarse defensivamente

`BGAppRefreshTask` es corto y `BGProcessingTask` es oportunista/interrumpible. No construiría ninguna proposition que dependa de ejecutar exactamente cada N minutos. :chatgpt-content-reference{index="114"}

### AlarmKit no equivale a Critical Alerts

Eso es una ventaja. AlarmKit tiene su propia authorization/usage description; Critical Alerts sigue siendo un entitlement especial. :chatgpt-content-reference{index="115"}

### NFC no es magic automation

Background tag reading muestra una system notification; el usuario debe tocarla, y un dispositivo bloqueado debe desbloquearse. :chatgpt-content-reference{index="116"}

### FamilyActivityData es excepcional, pero restringida

Necesita explicit authorization \+ entitlement y el customer-facing API está limitado actualmente a UE. :chatgpt-content-reference{index="117"}

### FinanceKit no es una base apropiada para un producto español hoy

La disponibilidad documentada sigue limitada a productos de EEUU y open banking del Reino Unido. :chatgpt-content-reference{index="118"}

### SensorKit debe considerarse fuera de alcance

Es para research studies aprobados por Apple, no una API consumer general. :chatgpt-content-reference{index="119"}

### La compatibilidad Apple Intelligence reduce el mercado inicial

Las features basadas estrictamente en Foundation Models/Visual Intelligence implican requisitos de hardware y OS. Por tanto, para un micro-producto conviene decidir explícitamente si:

- iOS 27 \+ Apple Intelligence es baseline;  
- existe fallback mediante Vision/Core ML;  
- o el mercado objetivo puede aceptar esa restricción.

---

# 11\. What I would investigate next

No empezaría todavía un proyecto Xcode completo.

Haría una **segunda ronda exclusivamente de falsificación**, distinta para cada finalista.

### A. Recipe → Timers

Objetivo: averiguar si la molestia es suficientemente grande para usar una app repetidamente.

Investigar:

- 30–50 recetas de fuentes distintas;  
- frecuencia de timed steps múltiples;  
- cómo expresar overlaps;  
- si users quieren timers completos automáticamente o progresive execution;  
- comparación contra Siri/Clock.

**Kill condition:** la mayoría prefiere decirle dos frases a Siri.

### B. Shift → Calendar

Aquí la pregunta no es si hay problema. Está demostrado.

La pregunta es:

> **¿queda un gap después de ShiftInbox \+ iOS 27?**

Construir un benchmark con cuadrantes reales y comparar:

- Apple Visual Intelligence;  
- ShiftInbox;  
- prototype experimental.

**Kill condition:** ShiftInbox resuelve correctamente casi todo el corpus.

### C. Offline Travel Rescue

La incógnita es si organizar automáticamente supera realmente a un álbum.

Haría task-based usability testing:

> “Encuentra tu booking reference ahora.”

Medir tiempo y errores.

**Kill condition:** Photos search/album tarda prácticamente lo mismo.

### D. Private Place Memory

Antes de programar: utilizar competidores intensivamente y entrevistar quantified-self users.

La pregunta crítica es **frecuencia**, no desirability.

**Kill condition:** “¿cuándo estuve aquí?” sucede tres veces al año.

### E. Music Phrase Practice

Haría discovery con un solo segmento musical y un prototype técnico mínimo alrededor de Music Understanding.

La pregunta:

> “¿La estructura detectada por Apple coincide suficientemente bien con cómo un músico piensa las regiones que quiere practicar?”

No está garantizado que *section/segment/phrase* computacional equivalga a *practice unit*.

**Kill condition:** los músicos siguen ajustando manualmente casi todos los boundaries.

---

### Qué investigaría primero

Si el objetivo inmediato es encontrar **una app pequeña que merezca ser construida y cobrada**, dedicaría la siguiente ronda a dos hipótesis principalmente:

**Recipe → Timers**, porque combina problema legible, zero backend, instant value, native leverage y scope reducido.

**Shift → Calendar**, porque tiene la evidencia conductual más fuerte de todas, aunque precisamente necesita un benchmark competitivo antes de escribir una sola feature debido a ShiftInbox y al avance de Visual Intelligence.

A las otras tres les dedicaría validation ligera en paralelo, no desarrollo.

Y mantendría un pequeño **technology watchlist** sobre:

- Music Understanding;  
- HealthKit Medications;  
- FamilyActivityData;  
- nuevas acciones de Visual Intelligence;  
- nuevas capabilities de Foundation Models.

La conclusión general no es que haya aparecido una “killer app escondida” en una API de Apple.

Es algo más útil:

> **En 2026 hay una nueva categoría de micro-productos viables en los que iOS puede tomar información que el usuario ya posee, entenderla localmente y convertirla en una acción fiable del sistema.**

Ese patrón sí parece suficientemente fértil para continuar investigándolo.

---

# 12\. Sources

### Apple platform documentation

- [Foundation Models updates — Apple Developer](https://developer.apple.com/documentation/Updates/FoundationModels?utm_source=chatgpt.com)  
- [Meet the Music Understanding framework — WWDC26](https://developer.apple.com/videos/play/wwdc2026/253/)  
- [AlarmKit scheduling — Apple Developer](https://developer.apple.com/documentation/AlarmKit/scheduling-an-alarm-with-alarmkit?utm_source=chatgpt.com)  
- [FamilyActivityData — Apple Developer](https://developer.apple.com/documentation/familycontrols/familyactivitydata)  
- [FinanceKit — Apple Developer](https://developer.apple.com/financekit/?utm_source=chatgpt.com)  
- [SensorKit project configuration — Apple Developer](https://developer.apple.com/documentation/sensorkit/configuring-your-project-for-sensor-reading?utm_source=chatgpt.com)  
- [Core NFC background tag reading — Apple Developer](https://developer.apple.com/documentation/corenfc/adding-support-for-background-tag-reading)  
- [Nearby Interaction — Apple Developer](https://developer.apple.com/documentation/nearbyinteraction?utm_source=chatgpt.com)

### High-signal user evidence

- [Amazon Flex schedule screenshot → Calendar Shortcut](https://www.reddit.com/r/shortcuts/comments/1q7vh3n/shortcut_to_add_work_schedule_from_screenshot_to/)  
- [iOS 27 PDF work schedule → Calendar problem](https://www.reddit.com/r/shortcuts/comments/1vsx1rb/request_help_getting_my_work_schedule_into/)  
- [Starbucks shift screenshot → Calendar Shortcut](https://www.reddit.com/r/starbucksbaristas/comments/1nc5qf3/shortcut_for_adding_shifts_to_calender_app_ios/)  
- [Recipe → cooking timers Shortcut](https://www.reddit.com/r/shortcuts/comments/15f6cee)  
- [Screenshot → Reminder workflow](https://www.reddit.com/r/shortcuts/comments/1rqwb6n/screenshot_to_reminder_ocrmodel/)  
- [Travel screenshots as offline backup](https://www.reddit.com/r/travel/comments/1s8je84/i_started_screenshotting_everything_before_trips/)  
- [Quantified-self personal location history discussion](https://www.reddit.com/r/QuantifiedSelf/comments/1s0tig8/do_you_track_your_location_too_places_youve/)  
- [NFC washing-machine timer workflow](https://www.reddit.com/r/shortcuts/comments/1p8yjp3/nfc_washing_machine_timer/)

### Representative App Store competition

- ShiftInbox :chatgpt-content-reference{index="136"}  
- Cooking Timer – Step by Step :chatgpt-content-reference{index="137"}  
- ShotInbox / Chista / Screen Actions :chatgpt-content-reference{index="138"}  
- CalAlarms / CalendarWake :chatgpt-content-reference{index="139"}  
- Departd :chatgpt-content-reference{index="140"}  
- Travel Binder :chatgpt-content-reference{index="141"}  
- Last Time I Was Here :chatgpt-content-reference{index="142"}  
- MOVINGBOXES / Cajas / Boxy :chatgpt-content-reference{index="143"}  
- Moises / Anytune / Music Looper :chatgpt-content-reference{index="144"}  
- Cadence medication reminder :chatgpt-content-reference{index="145"}

**Una limitación importante de la investigación competitiva:** muchas de las apps más interesantes son lanzamientos de 2026 con muy pocas valoraciones. En esos casos no hay aún volumen suficiente de reviews 1–3 estrellas para extraer patrones de queja estadísticamente útiles. He preferido no inventarlos ni extrapolar unas pocas reviews a toda la base de usuarios.

&nbsp;