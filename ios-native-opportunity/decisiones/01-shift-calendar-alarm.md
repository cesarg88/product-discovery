# Decisión 01 — Shift → Calendar → AlarmKit

**Fecha:** 21 de septiembre de 2026  
**Estado:** Decisión  
**Hipótesis actual:** Candidato #1 para validación  
**Repositorio:** `product-discovery`

---

## 1. Contexto

El proceso original de product discovery se diseñó deliberadamente para encontrar un negocio con suficiente potencial económico como para poder sustituir eventualmente un salario.

Ese proceso funcionó según lo previsto. Sacó a la superficie problemas con:

- consecuencias económicas claras;
- compradores identificables;
- willingness to pay demostrada;
- dolor operacional recurrente;
- mercados grandes o globales.

Sin embargo, la mayoría de los candidatos más fuertes estaban en dominios como construcción, conciliación de proveedores, hostelería, talleres y servicios profesionales.

El fundador podría construir técnicamente productos para esos mercados, especialmente con ayuda de agentes de IA, pero tendría una desventaja importante al evaluarlos.

El problema no era la capacidad de ingeniería.

El problema era el **criterio de producto**.

Sin conocimiento profundo del dominio, el fundador dependería demasiado de usuarios externos y agentes de IA para determinar si:

- un workflow es realista;
- una interacción propuesta tiene sentido;
- un edge case realmente importa;
- el producto resuelve el problema verdadero;
- una implementación está excesivamente complicada;
- la experiencia final es realmente buena.

Esto llevó a cambiar la estrategia de product discovery.

En lugar de preguntar:

> ¿Qué problema económicamente valioso podríamos resolver?

la nueva pregunta pasó a ser:

> ¿Qué producto pequeño, útil y monetizable puede aprovechar capacidades especialmente potentes del ecosistema Apple, de forma que la experiencia profunda en iOS constituya parte de la ventaja del fundador?

El objetivo ya no es identificar, antes de construir nada, el único negocio que algún día sustituirá un salario.

El objetivo inmediato es encontrar un producto que merezca:

- construirse;
- publicarse;
- cobrarse;
- aprender distribución con él;
- y mejorarse con feedback de usuarios reales.

---

## 2. Qué aprendimos del cruce entre modelos

Se realizaron cinco investigaciones independientes utilizando:

- ChatGPT;
- Claude;
- Claude Advanced;
- DeepSeek;
- Gemini.

Las investigaciones revelaron un patrón general especialmente interesante:

> **información existente → comprensión nativa de Apple → acción concreta del sistema**

Las mejores oportunidades no consistían normalmente en pedir al usuario que mantuviera otra base de datos.

Utilizaban información que ya estaba disponible mediante:

- HealthKit;
- Calendar;
- Photos;
- Location;
- audio;
- documentos;
- sensores;

y la convertían en algo inmediatamente útil mediante capacidades como:

- Vision;
- Foundation Models;
- Speech;
- Music Understanding;
- EventKit;
- AlarmKit;
- App Intents;
- Live Activities;
- Widgets.

También apareció una segunda conclusión metodológica importante.

Varias oportunidades aparentemente atractivas dependían de interpretaciones incorrectas de las APIs de Apple.

El contraste entre investigaciones eliminó propuestas basadas en capacidades como:

- borrado silencioso mediante PhotoKit;
- escritura de pautas de medicación en HealthKit;
- automatizaciones NFC completamente pasivas;
- generación dinámica de App Intents.

Esto confirmó que el conocimiento profundo de las plataformas Apple no solo es útil para implementar el producto.

También constituye un **filtro contra hipótesis de producto técnicamente inválidas**.

---

## 3. Por qué Music Practice deja de ser la primera opción

Music Practice apareció inicialmente como uno de los candidatos más atractivos.

Tres investigaciones independientes convergieron aproximadamente en la misma idea:

> Utilizar Music Understanding para identificar automáticamente la estructura musical y facilitar la práctica repetida de fragmentos concretos.

La oportunidad técnica es real.

Music Understanding proporciona información on-device como:

- beats;
- compases;
- frases;
- secciones;
- tonalidad;
- actividad instrumental.

Sin embargo, el análisis cruzado detectó un problema metodológico.

Los tres modelos habían seguido esencialmente este camino:

> nueva API interesante de Apple → buscar un problema al que aplicarla

en lugar de:

> problema fuerte observado en usuarios → descubrir que una API de Apple permite resolverlo mejor.

La convergencia representaba por tanto principalmente **convergencia técnica**, no evidencia independiente de mercado.

Además aparecieron tres riesgos estructurales importantes.

### Adopción de plataforma

Music Understanding depende actualmente de una versión muy reciente del sistema operativo.

Esto limita mucho la base instalada disponible a corto plazo.

### Respuesta de incumbentes

Productos existentes como Anytune, Capo o Moises reciben acceso a la misma capacidad de Apple.

El framework no constituye por sí solo una ventaja exclusiva para un nuevo producto.

### DRM y propiedad de los archivos

El workflow de consumo más atractivo sería permitir trabajar directamente con la música que el usuario ya escucha habitualmente.

El contenido protegido mediante streaming no proporciona el acceso PCM necesario para este tipo de análisis.

Esto reduce considerablemente el universo de contenido compatible.

### Decisión

Music Practice **no se descarta**.

Pasa a estado de observación.

Debe reconsiderarse si:

- los incumbentes no adoptan Music Understanding;
- crece suficientemente la base instalada compatible;
- aparece evidencia de que músicos y estudiantes siguen practicando habitualmente con grabaciones propias o archivos locales.

---

## 4. Hipótesis actual #1

# Shift → Calendar → AlarmKit

### Problema canónico

Trabajadores reciben frecuentemente sus horarios laborales mediante screenshots, fotografías, PDFs u otros documentos digitales poco estructurados.

Después deben interpretar manualmente esos horarios, copiar los turnos a su calendario personal y configurar por separado alarmas o recordatorios para llegar al trabajo a tiempo.

Cuando el horario original cambia, aumenta el riesgo de que Calendar y las alarmas ya no correspondan con la última versión.

---

## 5. Por qué este candidato sobrevive

### 5.1 Evidencia conductual fuerte

La evidencia más importante no consiste en personas diciendo:

> “Ojalá existiera una app para esto.”

Los usuarios ya están **construyendo y manteniendo su propio software** para resolverlo.

Las investigaciones encontraron ejemplos como:

- un trabajador de Amazon Flex que dedicó aproximadamente tres horas a construir una automatización;
- usuarios intentando interpretar automáticamente horarios tabulares en PDF;
- un Shortcut para trabajadores de Starbucks descrito por otro usuario como “life changing”;
- el autor de ese Shortcut continuando su mantenimiento y corrigiendo edge cases meses después.

Este comportamiento es una señal mucho más fuerte que una simple feature request.

Los usuarios ya están pagando con:

- tiempo;
- esfuerzo técnico;
- mantenimiento recurrente;

para resolver el problema por sí mismos.

---

### 5.2 AlarmKit aumenta materialmente el valor del workflow

Una versión básica del producto sería:

> cuadrante → Calendar

Ese workflow ya tiene competencia y cada vez más soporte de plataforma.

El workflow potencialmente más interesante es:

> **cuadrante → turnos estructurados → Calendar → alarma fiable**

AlarmKit cambia el último paso.

Permite utilizar una alarma real del sistema en lugar de depender únicamente de notificaciones ordinarias.

Eso hace que el job sea considerablemente más importante.

El usuario no quiere solamente que su turno aparezca en Calendar.

El resultado final que busca se parece más a:

> “Haz que mi iPhone sepa cuándo trabajo y me despierte cuando corresponde.”

---

### 5.3 Ventaja iOS real

El workflow potencial utiliza directamente capacidades de Apple:

- Vision;
- Foundation Models;
- EventKit;
- AlarmKit;
- App Intents;
- Widgets;
- potencialmente Live Activities.

Una aplicación web podría reproducir partes del flujo, pero no la integración completa con el sistema.

Existe por tanto una razón legítima para que el producto sea Apple-native.

---

### 5.4 Founder fit alto

El fundador no necesita convertirse en especialista en:

- contabilidad;
- medicina;
- construcción;
- procurement;
- seguros;
- inmigración;
- legislación fiscal.

Las preguntas difíciles son principalmente preguntas de producto e ingeniería mobile:

- ¿Se ha interpretado correctamente el turno?
- ¿Qué debemos hacer cuando la confianza de extracción es baja?
- ¿Cómo deben representarse los turnos nocturnos?
- ¿Qué ocurre si cambia el cuadrante?
- ¿Debe actualizarse automáticamente el evento existente?
- ¿Qué ocurre con una alarma ya programada?
- ¿Puede el usuario entender claramente por qué existe una determinada alarma?
- ¿Cómo mostramos los fallos?
- ¿Qué operaciones pueden realizarse de forma fiable en background?

Estas son preguntas que un Senior iOS Engineer puede razonar, probar y discutir directamente.

---

### 5.5 Backend mínimo o inexistente

El núcleo del producto podría funcionar completamente on-device.

Esto implica:

- arquitectura más sencilla;
- menor coste operativo;
- mejor privacidad;
- mantenimiento más viable para una sola persona;
- ausencia de dependencia crítica de un proveedor externo de contenido.

Esto evita directamente uno de los principales riesgos identificados en proyectos anteriores dependientes de APIs de terceros.

---

### 5.6 MVP estrecho

El producto no necesita convertirse en:

- workforce management;
- payroll;
- timesheets;
- planificación de equipos;
- software de RR. HH.

El job inicial puede mantenerse extremadamente concreto:

> **Importa correctamente mi horario y consigue que mi iPhone sea operacionalmente consciente de mis turnos.**

---

## 6. Riesgos principales

Este candidato todavía **no está validado**.

Hay varios descubrimientos que podrían matarlo rápidamente.

### Competencia existente

ShiftInbox ya resuelve una parte significativa del workflow de importación de horarios.

Si procesa correctamente la mayoría de cuadrantes reales y ofrece una experiencia suficientemente buena, el gap restante podría ser demasiado pequeño.

---

### Apple encroachment

Visual Intelligence y Foundation Models seguirán mejorando.

Si Apple empieza a convertir de manera fiable cualquier cuadrante en eventos de Calendar, la extracción de horarios pasará de producto a feature.

---

### Fiabilidad del parsing

Un producto de horarios no puede inventar silenciosamente turnos.

Una extracción incorrecta puede ser peor que obligar al usuario a introducir la información manualmente.

La gestión de:

- confidence;
- ambigüedad;
- revisión humana;
- correcciones;

puede resultar fundamental.

---

### Willingness to pay

Actualmente existe mejor evidencia de **necesidad** que de **pago**.

Que alguien dedique varias horas a crear un Shortcut demuestra dolor.

No demuestra automáticamente que pagará por una aplicación comercial.

---

### Cambios posteriores del cuadrante

El problema más importante podría no estar en la importación inicial.

Podría ser:

> “Mi empresa cambió mi turno después de haberlo importado.”

Detectar, reconciliar y actualizar correctamente:

- EventKit;
- alarmas;
- expectativas del usuario;

puede convertirse tanto en la mayor diferenciación del producto como en la complejidad que lo mate.

---

### Fiabilidad de AlarmKit

AlarmKit es fiable una vez que el sistema ha recibido una alarma programada.

La dificultad está en garantizar que la aplicación haya podido recalcular correctamente esa alarma cuando el horario cambia.

Esto requiere validación técnica específica.

---

## 7. Siguiente paso de validación

**No construir todavía el producto.**

El siguiente paso es crear un corpus real de evidencia.

### Conseguir entre 20 y 30 cuadrantes reales

Idealmente incluyendo:

- screenshots;
- fotografías de horarios en papel;
- PDFs;
- tablas tipo Excel;
- horarios semanales;
- rotaciones;
- turnos nocturnos;
- turnos partidos;
- modificaciones escritas a mano;
- diferentes idiomas;
- layouts ambiguos.

La información personal debe anonimizarse cuando sea necesario.

---

## 8. Probar tres sistemas contra exactamente el mismo corpus

### 1. Capacidades actuales de Apple

Medir qué puede extraer ya iOS / Visual Intelligence.

---

### 2. Producto especialista existente

Probar ShiftInbox contra exactamente los mismos documentos.

---

### 3. Spike técnico propio

Construir el experimento mínimo posible utilizando:

> Vision + Foundation Models → `[Shift]` estructurados

Conceptualmente:

```swift
struct Shift {
    let start: Date
    let end: Date
    let role: String?
    let location: String?
    let confidence: Double
}
```

El spike no es una aplicación.

Su objetivo es medir:

- precisión de extracción;
- turnos omitidos;
- turnos inventados;
- fechas ambiguas;
- overnight shifts;
- calibración de confidence.

---

## 9. Kill criteria

La oportunidad debe dejar de investigarse si se cumple cualquiera de estas condiciones:

1. Apple ya extrae horarios arbitrarios con suficiente fiabilidad.
2. ShiftInbox resuelve aproximadamente el 80–90 % del corpus real con buena UX.
3. Foundation Models no consigue una precisión suficiente para un workflow sensible como el calendario laboral.
4. Los usuarios consideran que introducir los eventos manualmente en Calendar es suficientemente sencillo.
5. Existe una resistencia clara a pagar incluso una cantidad pequeña mediante pago único.
6. Reconciliar cambios de horario de forma fiable resulta impracticable debido a las restricciones de background de iOS.

Matar rápidamente la hipótesis se considera un resultado satisfactorio del proceso de discovery.

---

## 10. Solo si el parsing sobrevive

Investigar la segunda mitad del job:

> **Calendar → AlarmKit**

Preguntas principales:

- ¿Cómo se calcula la hora de despertarse?
- ¿Debe existir un tiempo global de preparación o uno específico por turno?
- ¿Qué ocurre cuando cambia el evento en EventKit?
- ¿Qué ocurre si vuelve a importarse el cuadrante original?
- ¿Cómo diferenciamos un cambio real de una diferencia de parsing?
- ¿Puede reprogramarse siempre una alarma existente de forma segura?
- ¿Qué garantías existen cuando la aplicación no está ejecutándose?
- ¿Cómo explicamos al usuario por qué una alarma está programada a una hora determinada?

Esta fase podría revelar que el verdadero producto diferencial no es el OCR del cuadrante.

Podría ser:

> **mantener sincronizados de forma operativa los turnos, Calendar y las alarmas cuando el horario cambia.**

---

## 11. Candidatos conservados para investigaciones posteriores

### Candidatos secundarios fuertes

- Despertador calculado según Calendar y tiempo de desplazamiento.
- HealthKit → informe conciso para una consulta médica.
- Recipe → timers inteligentes.
- Productos de nicho donde la cámara elimine un workflow manual repetitivo.

### En observación

- Music Practice mediante Music Understanding.
- Conteo automático de días por jurisdicción.
- Registro profesional de kilometraje para Europa.

### Despriorizados actualmente

- Transcripción genérica.
- Insights genéricos sobre HealthKit.
- IA genérica sobre fotografías.
- Gestores de automatizaciones NFC.
- Generadores genéricos de pases Wallet.
- Productos B2B de field reporting que requieran un esfuerzo comercial significativo.

---

## 12. Decisión

El proyecto **no se compromete todavía a construir Shift → Calendar → AlarmKit**.

La decisión actual es deliberadamente más limitada:

> **Shift → Calendar → AlarmKit se convierte en la primera hipótesis iOS-native que recibirá validación empírica y técnica en profundidad.**

El objetivo de la siguiente fase no es demostrar que la idea es buena.

El objetivo es determinar, de la forma más barata posible, si merece convertirse en un producto.