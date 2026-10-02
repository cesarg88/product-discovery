# Mercado y competencia — Health Goals

*Fecha de análisis: 2 de octubre de 2026. Método: búsqueda web, fichas de App Store (API `itunes.apple.com/lookup`, RSS de reseñas) y documentación oficial. **No se instaló ni probó ninguna app.** "ND" = no documentado en las fuentes consultadas (no equivale a "No").*

---

## 1. Resumen ejecutivo

- **Ninguna app verificada documenta el paso clave del loop: "gap restante repartido en los días que quedan" apoyado en baseline de HealthKit** (el "necesitas ~6.850 pasos/día hasta el domingo"). Esto es ausencia de evidencia en fichas y documentación, no prueba de ausencia: falta probar las apps.
- **Cada pieza suelta ya existe.** Apple sugiere el objetivo Move cada semana según tu rendimiento previo y Workout Buddy verbaliza lo que te falta para cerrar un anillo. FitnessGoals propone objetivos desde tu media reciente. Gentler Streak, Bevel y Athlytic proponen un objetivo diario adaptativo desde tu baseline. Fitbit (Gemini) y Strava proponen objetivos semanales.
- **El gap semanal es una feature, no un producto.** Es aritmética sobre HealthKit; cualquiera de estos equipos la copia en días o semanas. Hoy no hay señal de que lo hayan hecho, pero el coste de hacerlo es mínimo.
- **Amenaza más seria: Apple y Google.** iOS 27 trae Insights, For You y Longevity; Health+ está fragmentado y retrasado, no cancelado de forma oficial. Fitbit/Google Health ya está en iOS con un coach que propone planes semanales y los ajusta por chat.
- **Monetización:** el gasto existe en Health & Fitness, pero los precios de este nicho (actividad + objetivos) son bajos: ~$20–40/año. Un pago único es plausible solo si el coste recurrente es ~0.
- **Veredicto: ESPACIO ESTRECHO.**

---

## 2. Mapa del mercado

| Capa | Productos | Qué prometen |
|---|---|---|
| Plataforma | Apple Health / Fitness / Watch | Tracking, anillos, sugerencia semanal de Move, Insights |
| Recovery / readiness adaptativo | Gentler Streak, Bevel, Athlytic, Pace by Athlytic, WHOOP, Oura | "Cuánto esfuerzo hoy" según tu baseline y recuperación |
| Objetivos desde tu media | FitnessGoals | Objetivo diario sugerido desde la media reciente |
| Contadores y hábitos | StepsApp, Pedometer++, Streaks, Habitify, Strides | Meta manual + racha |
| Ecosistema cerrado | Garmin Connect/Coach, Fitbit (Google Health), Strava | Planes y objetivos con datos propios |
| Coaches IA de entrenamiento | Fitbod, Ladder, Zing, Fit AI, SensAI | Plan de entrenos, mayormente fuerza |
| Analítica | HealthFit | Training load, exportación |

Dos ejes separan lo que existe de lo que propone Health Goals: (a) **objetivo diario/de capacidad** (recovery) frente a **objetivo semanal de comportamiento** (workouts, pasos, minutos); (b) **estado del día** frente a **esfuerzo restante**.

---

## 3. Apple

**Qué hace hoy (fuentes oficiales salvo indicación):**

- **Objetivo Move:** cada lunes el Watch notifica los logros de la semana y sugiere objetivos "based on your previous performance"; el usuario puede cambiar hoy o el diario, con personalización por día. No describe auto-ajuste sin aceptación. [Apple Watch User Guide](https://support.apple.com/guide/watch/adjust-your-activity-ring-goals-apd29b30023c/watchos). No pude verificar si Exercise y Stand se sugieren igual.
- **Workout Buddy (watchOS 26/27):** usa Apple Intelligence con tu historial y puede decir "estás a 18 minutos de cerrar tu anillo de Exercise" o resumir el kilometraje semanal. [Newsroom 2025](https://www.apple.com/newsroom/2025/06/watchos-26-delivers-more-personalized-ways-to-stay-active-and-connected/), [guía](https://support.apple.com/guide/watch/use-workout-buddy-apd65c7938e6/watchos). En watchOS 27 funciona sin iPhone cercano y compara con tu historial; requiere iPhone con Apple Intelligence, y no está disponible inicialmente en la UE. [apple.com/os/watchos](https://www.apple.com/os/watchos/)
- **Training Load, Vitals, Sleep score:** [Training Load](https://support.apple.com/guide/watch/track-your-training-load-apde4c07a6cf/watchos) (7 días vs 28 previos), [Vitals](https://support.apple.com/guide/watch/vitals-apd15aa7ed96/watchos), [Sleep score](https://support.apple.com/en-us/123002).
- **Readiness Score (Series 12 / Ultra 4):** 0–10 con Recover / Pace Yourself / Ready / Go For It, tras ≥7 noches de baseline. Adapta la capacidad del día, no un objetivo del usuario. [Newsroom sept 2026](https://www.apple.com/newsroom/2026/09/introducing-apple-watch-series-12-with-the-all-new-health-sensing-system/), [soporte](https://support.apple.com/en-euro/guide/watch/flx4gnzby346/watchos).
- **App Salud rediseñada (iOS 27, "later in 2026", inglés EE. UU. primero):** pestañas Insights (resumen con Apple Intelligence), For You (recomendaciones personalizadas) y Longevity con Health Age. La nota de prensa no menciona chatbot de coaching ni suscripción. [Newsroom sept 2026](https://www.apple.com/newsroom/2026/09/apple-advances-health-and-fitness-capabilities-using-apple-intelligence/). Cobertura de 9to5Mac sobre iOS 27.2: [artículo](https://9to5mac.com/2026/09/16/ios-27-2-introduces-apple-health-app-overhaul-heres-whats-new/) (no menciona objetivos ni planes).
- **Metas distintas por día y pausa de anillos:** [Tom's Guide](https://www.tomsguide.com/phones/iphones/how-to-adjust-your-daily-move-goal-in-the-ios-18-fitness-app) (snippet), [soporte](https://support.apple.com/HT205406).

**Rumores (prensa, no oficial):** Project Mulberry / Health+ recortado y troceado en funciones sueltas ([Business Standard](https://www.business-standard.com/technology/tech-news/apple-ai-health-coach-shelved-project-mulberry-features-arrive-updates-126020601028_1.html), [PYMNTS](https://www.pymnts.com/apple/2026/apple-scales-back-ai-health-coach-plans)); no llegó con watchOS 27 y podría aparecer en iOS 27.x ([9to5Mac](https://9to5mac.com/2026/05/24/apple-improving-heart-rate-tracking-in-watchos-27-mulberry-health-coach-delays/)). A fecha de hoy no hay servicio Health+ anunciado oficialmente.

**APIs para terceros:** confirmadas zonas de entrenamiento en HealthKit ([WWDC26 sesión 207](https://developer.apple.com/videos/play/wwdc2026/207/)), Foundation Models en watchOS ([guía](https://developer.apple.com/wwdc26/guides/watchos/)) y calendario de entrenos en WorkoutKit ([developer.apple.com/health-fitness](https://developer.apple.com/health-fitness/)). **No encontré** API pública para leer o escribir el objetivo Move sugerido ni para leer Readiness, Health Age o Insights: tratarlo como inexistente hasta demostrar lo contrario. No verificado: `HKStatisticsCollectionQuery` / background delivery (conocimiento previo, hay que contrastar con documentación) ni novedades de App Intents, widgets y Live Activities.

**Valoración (inferencia mía, no hecho verificado):**

| Lo que Apple absorbe fácilmente | Lo que probablemente no |
|---|---|
| Sugerir objetivo desde historial (ya lo hace para Move); extenderlo a pasos o minutos es incremental | Objetivos propios multi-métrica fuera de los anillos |
| "Te faltan X" por voz o widget (Workout Buddy ya lo hace para anillos) | Redistribución del gap por día restante: hoy el Move no se redistribuye y no hay señal de que vaya a hacerse |
| Narrativa de tendencias con IA (Insights, For You) | Objetivos ligados a una intención declarada ("quiero volver a entrenar") con ajuste conversacional |

Apple ha mostrado una pauta: lanza funciones genéricas y cautelosas (anillos, readiness) y deja el coaching personalizado a terceros; pero cualquier extensión de Workout Buddy o Insights puede cubrir el "te faltan X" sin aviso.

---

## 4. Competidores especializados

### FitnessGoals: Health Progress (indie)
Objetivo diario de pasos, energía activa o stand "from your own recent average", editable; tracking automático desde Apple Health; anillo, rachas, vistas día/semana/mes; sin cuenta. Gap restante y redistribución: ND. Premium $3,99/mes o $22,99/año. **0 valoraciones**; versión del 30-sep-2026. Requiere iOS 26. [Ficha](https://apps.apple.com/us/app/fitnessgoals-health-progress/id6504627557), [lookup](https://itunes.apple.com/lookup?id=6504627557&country=us). **Es el competidor conceptualmente más cercano en "objetivo desde baseline" y cuesta menos que cualquier plan de Health Goals plausible.**

### Gentler Streak — 4,71 (8.822 valoraciones)
"Activity Path": banda diaria calculada con historial de entrenos, recuperación y estado manual (Active / On a Break / Sick / Injured), con mensaje diario explicativo. Dice no empujar a perseguir metas de pasos. Widgets, Live Activity, App Intents (v5.13). Anunciada una capa "how you feel" para finales de octubre. Gap restante: no documentado. Precio: $8,99/mes, $39,99/año, lifetime desde $59,99 (las fuentes discrepan hasta $179,99). [Ficha](https://apps.apple.com/us/app/gentler-streak-workout-tracker/id1576857102), [docs](https://docs.gentler.app/understanding-your-activity-path/what-is-the-activity-path), [9to5Mac](https://9to5mac.com/2026/09/14/gentler-streak-and-the-outsiders-ios-27-updates-add-siri-ai-onscreen-awareness-support-more/), [review](https://www.healthappinsider.com/en/reviews/gentler-streak-review).

### Bevel — 4,85 (16.644)
"Target Strain" diario desde tu strain típico y recuperación; chat con IA; Pro $14,99/mes o $99,99/año más créditos de IA. Gap semanal: ND. [Ficha](https://apps.apple.com/us/app/bevel-ai-health-coach/id6456176249), [help](https://help.bevel.health/en/articles/11251073).

### Athlytic — 4,79 (11.060)
"Target Exertion" y "Target Sleep" diarios según Recovery; sugerencias de entreno; $4,99/mes o $29,99/año; sin lifetime. [Ficha](https://apps.apple.com/us/app/athlytic-fitness-recovery/id1543571755), [FAQ lifetime](https://athlyticapp.helpscoutdocs.com/article/29-does-athlytic-have-a-lifetime-subscription-or-offer-discounts).

### Pace by Athlytic (nuevo, 4,54 con 57 valoraciones)
Lo verifiqué directamente en la API de App Store hoy. Es sobre todo una app de **insights de salud en lenguaje llano** (35+ señales, baselines a 60 días, alertas, patrones, IA on-device). En actividad, la ficha dice solo "Steps with personalized pacing and goal tracking" y, en Premium, "Step goal celebrations with streak tracking" y "Step pacing". No detalla cómo se calcula el pacing ni si hay gap restante o redistribución. **Es la señal más próxima a tu idea y la que más conviene probar a mano.** [Ficha](https://apps.apple.com/us/app/pace-by-athlytic/id6755126439), [lookup](https://itunes.apple.com/lookup?id=6755126439&country=us).

### WHOOP, Oura, Fitbit/Google Health, Garmin, Strava
- **WHOOP** (4,81; 83.091 valoraciones): Weekly Plan con objetivo elegido, Strain Target diario con "cuánto te falta" en vivo, objetivo de fuerza desde feb-2026. Requiere su hardware; datos de search, WHOOP.com dio 403. [lookup](https://itunes.apple.com/lookup?id=933944389&country=us), [novedades 2026](https://www.whoop.com/us/en/thelocker/2026-whats-new/).
- **Oura Advisor** (4,86; 306.519): planes en chat para metas; requiere anillo; $5,99/mes. [Oura blog](https://ouraring.com/blog/oura-advisor/).
- **Fitbit / Google Health coach (Gemini)** (4,47; 702.293): conversación de onboarding, planes multisemana y objetivos semanales, ajustes por lenguaje natural; en iOS desde feb-2026; $9,99/mes. Críticas de calidad ("unhinged advice", dificultad para fijar metas: solo vi el titular). [Google blog abril 2026](https://blog.google/products-and-platforms/devices/fitbit/personal-health-coach-updates/), [TechCrunch](https://techcrunch.com/2026/05/07/googles-9-99-per-month-ai-health-coach-launches-may-19/), [MacRumors](https://www.macrumors.com/2026/02/10/google-fitbit-ai-health-coach-ios/), [TechRadar](https://www.techradar.com/ai-platforms-assistants/fitbits-gemini-ai-coach-is-giving-users-unhinged-fitness-advice-heres-why-users-are-saying-they-cannot-wait-for-my-trial-to-end). Que ingiera Apple Health: solo fuente secundaria ([SensAI](https://www.sensai.fit/blog/google-health-premium-fitbit-ai-coach-2026)).
- **Garmin Coach / Daily Suggested Workouts / Connect+**: planes adaptativos con Training Status y Readiness, con explicación (frases enlatadas según The 5K Runner); datos propios, no HealthKit; Connect+ $6,99/mes o $69,99/año. La ficha de iOS critica que fijar y seguir metas solo está en la web. [Garmin Rumors](https://garminrumors.com/garmin-expands-garmin-coach-with-adaptive-running-cycling-and-strength-training-plans/), [The 5K Runner](https://the5krunner.com/2024/11/12/garmin-adaptive-plans-get-improved-explanations/), [DC Rainmaker](https://www.dcrainmaker.com/2025/03/garmin-connect-plus-subscription-walkthrough.html), [ficha](https://apps.apple.com/us/app/garmin-connect/id583446403).
- **Strava** (4,8; 376K): metas por periodo (semanal/mensual/anual) y métrica; ofrece metas sugeridas según tu actividad; solo suscriptores. Gap explícito y redistribución: ND. [Soporte Strava](https://support.strava.com/en-us/articles/15401694-goals-on-the-strava-app), [ficha](https://apps.apple.com/app/strava/id426826309).

### Contadores y hábitos
- **StepsApp** (4,8; 299K): meta diaria manual; una reseña de 2024 dice que no se ajusta dinámicamente. [Ficha](https://apps.apple.com/us/app/stepsapp-pedometer/id1037595083), [review](https://mostly.media/stepsapp-full-app-review/).
- **Pedometer++** (4,8; 183K): meta diaria manual en pasos de 100; importa histórico de Health pero no lo usa para proponer meta. [FAQ](https://pedometer.app/faq), [ficha](https://apps.apple.com/us/app/pedometer/id712286167).
- **Streaks** (4,8; 27K): meta manual, frecuencia tipo "3 días/semana", tareas ligadas a Health se completan solas; $5,99 pago único. [Ficha](https://apps.apple.com/us/app/streaks/id963034692), [MacStories](https://www.macstories.net/reviews/achieving-personal-goals-with-streaks/).
- **Habitify** (4,6; 7,1K): hábitos manuales; Apple Health solo en plan Pro ($49,99/año). [Ficha](https://apps.apple.com/us/app/habitify-habit-tracker/id1111447047).
- **Strides** (4,8; 19K): cuatro tipos de tracker (Streak, Milestone, Average, Target), manual + Health; lifetime $149,99. Gap en el tracker Target: ND. [Ficha](https://apps.apple.com/us/app/strides-habit-tracker-goals/id672401817).
- **HealthFit** (4,6; 903): analítica de entrenamiento, $6,99 pago único; no es app de objetivos. [Ficha](https://apps.apple.com/us/app/healthfit/id1202650514).
- **Otros:** *Goals: Fitness Accountability* (5,0; 6 valoraciones; compromiso semanal con dinero en juego, objetivo elegido por el usuario) [ficha](https://apps.apple.com/us/app/goals-fitness-accountability/id6744724683); *Paceline* (4,78; 18.704; 150 min/semana fijos) [ficha](https://apps.apple.com/us/app/paceline-fitness-rewards/id1491824216); *Steps Widget* muestra "steps remaining" (solo snippet, no verificado) [web](https://stepswidget.app/). Coaches de fuerza (Fitbod, Ladder, Zing, Fit AI, SensAI) cubren planes de gimnasio, no actividad diaria: [Fitbod](https://itunes.apple.com/lookup?id=1041517543&country=us), [Ladder](https://itunes.apple.com/lookup?id=1502936453&country=us), [Zing](https://itunes.apple.com/lookup?id=1552207792&country=us), [Fit AI](https://apps.apple.com/us/app/fit-ai-workout-planner/id6763371107), [SensAI](https://www.sensai.fit/blog/best-ai-workout-app) (blog del propio vendor).

*Límites de cobertura:* no pude abrir WHOOP.com, Forbes ni Wareable (403), ni el cuerpo del artículo de TechRadar; la ficha de Gentler Streak dio 429 en un intento. No hay citas de Reddit (bloqueado).

---

## 5. Comparación del core loop

Leyenda: **S** sí · **P** parcial · **N** no · **ND** no documentado. Es una lectura de fichas y documentación, no de uso real.

| Producto | Intención | Baseline histórico | Propuesta de objetivo | Aceptación / ajuste | Tracking auto | Progress | Gap restante | Redistribución dinámica | Adaptación futura |
|---|---|---|---|---|---|---|---|---|---|
| **Apple (Move + Workout Buddy)** | N | S (historial) | P (solo Move, semanal) | S (aceptar/editar) | S | S | P (por voz para anillos) | N | P |
| FitnessGoals | ND | S (media reciente) | S | S | S | S | ND | ND | ND |
| Gentler Streak | P (estado manual) | S | S (banda diaria) | P | S | S | N | N | S (diaria) |
| Bevel | ND | S | S (Target Strain) | ND | S | S | ND | ND | S (diaria) |
| Athlytic | ND | S (HRV/FC) | S (Target Exertion) | ND | S | S | ND | ND | P |
| Pace by Athlytic | ND | S (60 días) | P ("step pacing") | ND | S | P | ND | ND | P |
| WHOOP | P | S (su hardware) | S | S | S | S | P (strain en vivo) | ND semanal | S (diaria) |
| Oura Advisor | S (chat) | S (su anillo) | S | S | S | S | ND | ND | ND |
| Fitbit / Google coach | S | P (HealthKit sin confirmar) | S | S (lenguaje natural) | P | ND | ND | ND | S |
| Garmin Coach | P | P (datos propios) | S | P | S | S | ND | P | S |
| Strava | S (manual) | P (actividad pasada) | P (sugerida) | S | S | S | ND | N | ND |
| StepsApp / Pedometer++ | S (meta diaria manual) | N / P (importa, no usa) | N | Manual | S | S | N | N | N |
| Streaks / Habitify / Strides | S (manual) | N | N | Manual | P | S | N / ND | N | N |

**Lectura:** la columna "Gap restante" + "Redistribución" es la única con ceros o ND en casi toda la tabla, salvo la voz de Workout Buddy para anillos y el "strain en vivo" de WHOOP. Pero el resto del loop (baseline + propuesta + tracking + progress) está cubierto por varios productos. El diferencial de Health Goals se reduce a combinar estos pasos **en objetivos semanales de comportamiento** (workouts, pasos, minutos) con cálculo del restante.

---

## 6. Reseñas y problemas recurrentes

Muestra reciente del feed RSS de App Store EE. UU. (no estadística), obtenida por el subagente de coaching: [Gentler Streak](https://itunes.apple.com/us/rss/customerreviews/page=1/id=1576857102/sortby=mostrecent/json), [Bevel](https://itunes.apple.com/us/rss/customerreviews/page=1/id=6456176249/sortby=mostrecent/json), [Athlytic](https://itunes.apple.com/us/rss/customerreviews/page=1/id=1543571755/sortby=mostrecent/json).

| Patrón | Evidencia (parafraseada) |
|---|---|
| **Recomendaciones que contradicen al usuario** | Gentler Streak, 28-may-2026: tras caminar 30 min le dice que descanse 3 días. Bevel, 2-sep-2026: "siempre dice que me quede en cama". Athlytic, 7-ago-2026: recovery 30–45 % cuando se siente genial |
| **Baseline que no refleja al usuario** | Gentler Streak, 8-jul-2026: no reconoce el entreno de fuerza como bueno. Athlytic, 16-may-2026: no sirve para fuerza. Bevel, 13-sep-2026: recomendaciones con datos viejos |
| **Dashboard sin acción** | Gentler Streak, 18-may-2026: "nada que no vea en Apple Health". Bevel, 3-sep-2026: sin insight revolucionario |
| **Paywall y suscripción** | Gentler Streak 8-jun-2026 y 22-mar-2026; Bevel 5 y 7-sep-2026 (anuncio "free" frente a trial y $14,99/mes); Athlytic 7-jun-2026 ("paywalled desde el 4 de junio"); Habitify y StepsApp (funciones movidas a paywall, fuente secundaria) |
| **Rechazo a la IA / ansiedad** | Gentler Streak, 17 y 29-sep-2026; Bevel, 10-sep-2026 |
| **Metas rígidas de anillos** | Fortune, 24-ene-2025 ([artículo](https://www.fortune.com/well/2025/01/24/apple-watch-bullied-burn-calories-close-rings-obsession-fitness-trackers-notifications)): "random numbers every single day". Apple Community: sugerencias de subir Move que no se pueden desactivar ([hilo](https://discussions.apple.com/thread/254891566)) |

**Qué NO encontré:** una queja verificable sobre falta de objetivos semanales, de "remaining effort", de logging manual o de objetivos arbitrarios en apps de pasos. Esto es relevante en las dos direcciones: o el dolor no existe, o no se expresa con esas palabras. **No hay evidencia de demanda explícita para el gap semanal.**

---

## 7. Monetización

- **Gasto real en la categoría:** RevenueCat 2026 da para Health & Fitness 6,9 % de download-to-trial, 37,7 % trial-to-paid y 2,9 % download-to-paid a 35 días; la propia fuente mostró cifras distintas en otro resumen (3,5 % y 35,0 %), discrepancia no resuelta. LTV mediano por pagador: $24,23 al mes 1 y $35,64 al año 1. [RevenueCat](https://www.revenuecat.com/state-of-subscription-apps). Adapty: LTV de instalación a un año de $1,21, el más alto entre categorías. [Adapty](https://adapty.io/blog/health-fitness-app-subscription-benchmarks/)
- **Retención:** un resumen de búsqueda de RevenueCat sitúa a Health & Fitness en 30,3 % de retención a la primera renovación (último lugar; no leído en la página).
- **Mix:** anuales ≈ 68 % de las suscripciones vendidas; precio anual mediano $39,94; 60 % de las apps muestra dos planes. [RevenueCat](https://www.revenuecat.com/state-of-subscription-apps). Anuales caros generan ~4,5× más por usuario que baratos [Adapty](https://adapty.io/blog/health-fitness-app-subscription-benchmarks/).
- **Hard paywall vs freemium (cifra general, no solo H&F):** 10,7 % vs 2,1 % de conversión a 35 días según Adapty, vía snippet. [Adapty](https://adapty.io/state-of-in-app-subscriptions/)
- **Precios observados en actividad + objetivos:**

| App | Precio |
|---|---|
| FitnessGoals | $3,99/mes · $22,99/año |
| StepsApp | $19,99–$29,99/año |
| Pedometer++ | $3,99/mes · $29,99/año |
| Athlytic | $4,99/mes · $29,99/año |
| Gentler Streak | $8,99/mes · $39,99/año · lifetime promo |
| Bevel | $14,99/mes · $99,99/año |
| Streaks | $5,99 único |
| Strides | lifetime $149,99 |
| Strava | ~$79,99/año (fuentes discrepan) |
| Fitbit / Google Health | $9,99/mes |
| Garmin Connect+ | $6,99/mes · $69,99/año |

- **¿Pago único?** Funciona para utilidades sin coste recurrente (Streaks, HealthFit) pero el mercado empuja a suscripción: Pillow retiró lifetime a clientes nuevos y Gentler Streak lo mantiene como promoción (snippets; confirmar en fichas). No encontré cifras de peso de lifetime/one-time en RevenueCat ni Adapty (no verificado). Mi inferencia: con IA en servidor un pago único no se sostiene; con lógica 100 % on-device (como Pace) sí es plausible.
- **Conclusión:** hay gasto en la categoría, pero el techo de precio en "contador + objetivos" es bajo (~$20–40/año), y la competencia directa más barata (FitnessGoals) ya está en $22,99.

---

## 8. Gap real, si existe

Formulado con la regla "el producto actual hace X pero sistemáticamente no hace Y":

| Hipótesis | Veredicto | Evidencia |
|---|---|---|
| **Targets arbitrarios** | **Falsa en parte** | Apple sugiere Move desde rendimiento; FitnessGoals desde media; Gentler/Bevel/Athlytic desde baseline. Los contadores clásicos (StepsApp, Pedometer++) sí son manuales |
| **Goals introducidos manualmente** | Cierta solo en contadores y hábitos | Pedometer++ importa histórico pero no propone meta (FAQ) |
| **Dashboards sin acción** | **Parcialmente cierta** | Reseñas "nada que no vea en Apple Health", pero no hay datos de magnitud |
| **Daily goals demasiado rígidos** | Parcialmente cierta | Quejas anecdóticas de anillos; Apple ya permite metas por día y pausas |
| **Ausencia de weekly goals** | **Falsa** | Apple (revisión semanal de Move), Garmin (150 min/semana), Strava (periodos semanales), Fitbit, Streaks (X días/semana) |
| **Ausencia de "remaining effort"** | **Posible gap, sin verificar** | No documentado en las fichas de Streaks, Strides, FitnessGoals, Gentler, Bevel, Athlytic; presente en voz (Workout Buddy), widgets de terceros (Steps Widget) y en vivo (WHOOP strain). **Falta probar Pace by Athlytic y Strides Target** |
| **Redistribución dinámica del restante** | **Posible gap, sin verificar** | No lo documenta ningún producto revisado, y no encontré quejas por su ausencia |
| **Recomendaciones sin baseline personal** | **Falsa** | La mayoría usa baseline; la queja real es que el baseline no refleja al usuario (fuerza, estado subjetivo) |
| **Logging manual** | Falsa para casi todos | Tracking automático es estándar; Strides y Habitify mezclan manual |

**El único gap defendible es estrecho:** *ningún producto revisado documenta que, dado un objetivo semanal de comportamiento aceptado, recalcule a diario lo que falta y lo reparta entre los días restantes.* Es un gap de **cálculo y presentación**, no de dato ni de tecnología.

---

## 9. Riesgo de commoditización

**¿El cálculo del gap semanal se copia en una semana?** Sí. Es `(objetivo − acumulado) / días restantes` sobre `HKStatisticsCollectionQuery`. Candidatos con la distribución y el motivo para añadirlo: Gentler Streak (ya tiene widgets, Live Activities, App Intents y capa semanal), Pace by Athlytic (ya anuncia "step pacing"), FitnessGoals (ya tiene vistas semanales y objetivos), StepsApp (299K valoraciones), Strava, Fitbit y Apple (Workout Buddy ya habla del restante).

**Lo que tendría que ser el producto para seguir teniendo sentido** (sin inventar un moat):

1. **Intención → objetivos, no solo gap.** El valor está en traducir "quiero volver a entrenar" en 2–3 objetivos razonables y defendibles contra la propia historia. Ninguna ficha revisada lo describe de forma conversacional salvo Fitbit (en su ecosistema) y Oura/WHOOP (su hardware).
2. **Calibración honesta del objetivo.** Las quejas dominantes son recomendaciones que contradicen al usuario (descanso excesivo, fuerza ignorada). Un producto que propone objetivos *alcanzables* y explica el porqué con sus datos tiene un hueco, pero hay que demostrar que se calibra mejor que las bandas diarias.
3. **Superficie de bajo esfuerzo:** widget / Live Activity / Siri con el "qué hago hoy", no una app que haya que abrir. Esto es ejecución, no defensa; Gentler y Pace ya compiten ahí.
4. **Sin dependencia de hardware o cuenta**, procesamiento on-device. Pace ya lo hace; no es diferencial, es requisito.

Ninguno de estos es un moat; son una **formulación**. La ventaja, si existe, es de tiempo y de ejecución durante unos meses.

---

## 10. Evidencia en contra

El caso "X ya hace casi todo esto con buena UX y miles de usuarios satisfechos":

- **Gentler Streak** (4,71; 8.822 valoraciones; premiada por Apple): baseline propio, objetivo diario adaptativo, explicación, estado manual, widgets, Live Activity, App Intents y roadmap hacia "how you feel". Le falta el objetivo semanal con restante. Es el producto al que habría que ganar, y puede añadirlo.
- **FitnessGoals**: objetivo sugerido desde tu media + vistas semanales por $22,99/año. Hoy sin tracción (0 valoraciones), pero demuestra que la mitad barata del loop se construye con poco.
- **Apple Move + Workout Buddy + Insights**: la sugerencia semanal y el "estás a X minutos" ya existen y son gratis en el sistema. La ausencia de API pública para el objetivo Move deja a los terceros sin extender el anillo, pero también significa que Apple puede decidir cubrirlo sin competir con nadie.
- **Fitbit/Google Health coach**: onboarding por intención, plan semanal, ajuste por lenguaje natural, en iOS, $9,99/mes y 702K valoraciones. Sus críticas de calidad son la señal de que la ejecución IA aún es difícil, no de que el loop esté vacío.
- **Falta de dolor documentado:** no encontré quejas verificables sobre "falta de restante" ni de objetivos semanales. Las quejas reales son otras (IA que ansía, paywalls, recomendaciones erróneas).

---

## 11. Conclusión

El loop completo **Intención → Baseline → Plan → Progress → Gap → Adapt** no lo resuelve **de extremo a extremo** ningún producto que haya podido verificar, pero sí cada tramo por separado y por varios actores. Las fichas no documentan el tramo "Gap + Redistribución" para objetivos semanales de comportamiento, pero (a) es copiable en días, (b) Apple ya cubre su versión para anillos y (c) no hay quejas verificadas que indiquen demanda.

Hay un producto posible solo si se formula como: **"objetivos semanales razonables, calibrados con tu historia real y explicados, con el restante siempre a la vista en widget / Siri / Live Activity"**, para quien hoy usa anillos o un contador y no sabe qué objetivo fijarse. Por encima de eso (más métricas, más IA, más dashboard) cae en terreno de Gentler/Bevel/Athlytic/Apple, que son más fuertes en esa liza.

**Antes de construir (barato y decisivo):**
1. Instalar y probar a mano Pace by Athlytic, FitnessGoals y Gentler Streak con una cuenta de HealthKit con historial real; confirmar si muestran "te faltan X" y cómo.
2. Buscar en reseñas y foros con las palabras exactas del usuario ("how many steps do I need", "behind on my goal", "catch up this week") para medir el dolor.
3. Revisar el cambio de Apple en iOS 27.x (¿Workout Buddy o Insights ampliados al restante semanal?).
4. Fijar la apuesta de precio: con FitnessGoals a $22,99/año y Pedometer++ a $29,99/año, cobrar >$30 exige un valor claramente mayor.

---

**ESPACIO ESTRECHO**
Hay producto posible, pero requiere una formulación muy concreta.

---

## 12. Fuentes

**Apple y desarrolladores:** [Ajustar objetivos de anillos](https://support.apple.com/guide/watch/adjust-your-activity-ring-goals-apd29b30023c/watchos) · [Workout Buddy](https://support.apple.com/guide/watch/use-workout-buddy-apd65c7938e6/watchos) · [watchOS 26 newsroom](https://www.apple.com/newsroom/2025/06/watchos-26-delivers-more-personalized-ways-to-stay-active-and-connected/) · [watchOS 27](https://www.apple.com/os/watchos/) · [Health y Fitness con Apple Intelligence (sept 2026)](https://www.apple.com/newsroom/2026/09/apple-advances-health-and-fitness-capabilities-using-apple-intelligence/) · [Watch Series 12](https://www.apple.com/newsroom/2026/09/introducing-apple-watch-series-12-with-the-all-new-health-sensing-system/) · [Readiness](https://support.apple.com/en-euro/guide/watch/flx4gnzby346/watchos) · [Training Load](https://support.apple.com/guide/watch/track-your-training-load-apde4c07a6cf/watchos) · [Vitals](https://support.apple.com/guide/watch/vitals-apd15aa7ed96/watchos) · [Sleep score](https://support.apple.com/en-us/123002) · [Pausar anillos](https://support.apple.com/HT205406) · [WWDC26 sesión 207](https://developer.apple.com/videos/play/wwdc2026/207/) · [guía watchOS WWDC26](https://developer.apple.com/wwdc26/guides/watchos/) · [Health & Fitness developers](https://developer.apple.com/health-fitness/)

**Prensa y análisis:** [9to5Mac iOS 27.2 Health](https://9to5mac.com/2026/09/16/ios-27-2-introduces-apple-health-app-overhaul-heres-whats-new/) · [9to5Mac Mulberry retrasos](https://9to5mac.com/2026/05/24/apple-improving-heart-rate-tracking-in-watchos-27-mulberry-health-coach-delays/) · [Business Standard](https://www.business-standard.com/technology/tech-news/apple-ai-health-coach-shelved-project-mulberry-features-arrive-updates-126020601028_1.html) · [PYMNTS](https://www.pymnts.com/apple/2026/apple-scales-back-ai-health-coach-plans) · [MacRumors iOS 27 Health](https://www.macrumors.com/guide/ios-27-health-app-new-features/) · [MacRumors recorte](https://www.macrumors.com/2026/02/05/apple-reportedly-scales-back-ios-27-feature/) · [Sahha WWDC 2026](https://sahha.ai/blog/wwdc-2026-apple-health-developers/) (vendor) · [Fortune](https://www.fortune.com/well/2025/01/24/apple-watch-bullied-burn-calories-close-rings-obsession-fitness-trackers-notifications) · [Tom's Guide Move](https://www.tomsguide.com/phones/iphones/how-to-adjust-your-daily-move-goal-in-the-ios-18-fitness-app) · [Apple Community](https://discussions.apple.com/thread/254891566) · [MacStories Streaks](https://www.macstories.net/reviews/achieving-personal-goals-with-streaks/) · [Mostly Media StepsApp](https://mostly.media/stepsapp-full-app-review/) · [Health App Insider Gentler](https://www.healthappinsider.com/en/reviews/gentler-streak-review) · [9to5Mac Gentler iOS 27](https://9to5mac.com/2026/09/14/gentler-streak-and-the-outsiders-ios-27-updates-add-siri-ai-onscreen-awareness-support-more/) · [TechCrunch Google coach](https://techcrunch.com/2026/05/07/googles-9-99-per-month-ai-health-coach-launches-may-19/) · [MacRumors Fitbit iOS](https://www.macrumors.com/2026/02/10/google-fitbit-ai-health-coach-ios/) · [TechRadar Fitbit](https://www.techradar.com/ai-platforms-assistants/fitbits-gemini-ai-coach-is-giving-users-unhinged-fitness-advice-heres-why-users-are-saying-they-cannot-wait-for-my-trial-to-end) · [DC Rainmaker Connect+](https://www.dcrainmaker.com/2025/03/garmin-connect-plus-subscription-walkthrough.html) · [The 5K Runner](https://the5krunner.com/2024/11/12/garmin-adaptive-plans-get-improved-explanations/) · [Garmin Rumors](https://garminrumors.com/garmin-expands-garmin-coach-with-adaptive-running-cycling-and-strength-training-plans/) · [Strava soporte](https://support.strava.com/en-us/articles/15401694-goals-on-the-strava-app)

**Benchmarks de monetización:** [RevenueCat State of Subscription Apps](https://www.revenuecat.com/state-of-subscription-apps) · [Adapty H&F](https://adapty.io/blog/health-fitness-app-subscription-benchmarks/) · [Adapty state of in-app subscriptions](https://adapty.io/state-of-in-app-subscriptions/)

**Fichas de App Store y APIs (consultadas 2-oct-2026):** [FitnessGoals](https://apps.apple.com/us/app/fitnessgoals-health-progress/id6504627557) · [Gentler Streak](https://apps.apple.com/us/app/gentler-streak-workout-tracker/id1576857102) · [Bevel](https://apps.apple.com/us/app/bevel-ai-health-coach/id6456176249) · [Athlytic](https://apps.apple.com/us/app/athlytic-fitness-recovery/id1543571755) · [Pace by Athlytic](https://apps.apple.com/us/app/pace-by-athlytic/id6755126439) · [Streaks](https://apps.apple.com/us/app/streaks/id963034692) · [Habitify](https://apps.apple.com/us/app/habitify-habit-tracker/id1111447047) · [Strides](https://apps.apple.com/us/app/strides-habit-tracker-goals/id672401817) · [StepsApp](https://apps.apple.com/us/app/stepsapp-pedometer/id1037595083) · [Pedometer++](https://apps.apple.com/us/app/pedometer/id712286167) · [HealthFit](https://apps.apple.com/us/app/healthfit/id1202650514) · [Garmin Connect](https://apps.apple.com/us/app/garmin-connect/id583446403) · [Strava](https://apps.apple.com/app/strava/id426826309) · [Google Health (Fitbit)](https://apps.apple.com/us/app/google-health-fitbit/id462638897) · [Paceline](https://apps.apple.com/us/app/paceline-fitness-rewards/id1491824216) · [Goals: Fitness Accountability](https://apps.apple.com/us/app/goals-fitness-accountability/id6744724683)

**Fuentes secundarias de menor fiabilidad (marcadas como tal en el texto):** [SensAI blog](https://www.sensai.fit/blog/best-ai-workout-app) · [SensAI Google Health](https://www.sensai.fit/blog/google-health-premium-fitbit-ai-coach-2026) · [Pedometer++ FAQ](https://pedometer.app/faq) · [Gentler docs](https://docs.gentler.app/understanding-your-activity-path/what-is-the-activity-path) · [Bevel help](https://help.bevel.health/en/articles/11251073) · [WHOOP 2026](https://www.whoop.com/us/en/thelocker/2026-whats-new/) · [Oura Advisor](https://ouraring.com/blog/oura-advisor/) · [Steps Widget](https://stepswidget.app/) · [Athlytic lifetime FAQ](https://athlyticapp.helpscoutdocs.com/article/29-does-athlytic-have-a-lifetime-subscription-or-offer-discounts)

*Precios y cifras de blogs de comparativas y snippets de buscador (Pillow, Streaks de terceros, lifetime de Gentler hasta $179,99, precios de Strava, WHOOP, Withings, Zing) no se han verificado en fichas oficiales: confirmar antes de usarlos en decisiones.*
