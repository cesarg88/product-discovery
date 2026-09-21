## Problema a investigar
Freelancers y pequeñas agencias sufren retrasos en sus proyectos y cobros porque los clientes tardan en proporcionar materiales, accesos, información, feedback o aprobaciones necesarias para continuar el trabajo.

# Bloqueo por inputs del cliente (client input bottleneck)

> Investigación de product discovery. Fecha de la investigación: **20 de septiembre de 2026**.
> Problema investigado: *freelancers y pequeñas agencias sufren retrasos en sus proyectos y cobros porque los clientes tardan en proporcionar materiales, accesos, información, feedback o aprobaciones necesarias para continuar el trabajo.*
>
> **Limitación metodológica declarada:** Reddit y X/Twitter no fueron accesibles desde el entorno de investigación (bloqueo de egress y ausencia en el índice de búsqueda). Toda la evidencia comunitaria procede de foros web abiertos (SitePoint, Graphic Design Forums UK, Adobe Community), blogs de practicantes con nombre y apellidos, secciones de comentarios, reviews verificadas (G2, Capterra, Trustpilot, Software Advice), dev.to, Indie Hackers y AppSumo. Esto sesga la muestra hacia gente que publica públicamente (consultores, formadores, agencias que hacen marketing de contenidos) y minusvalora el desahogo anónimo. Se señala allí donde importa.

---

## 1. Executive summary

El fenómeno existe, está documentado de forma consistente entre 2010 y 2026, y cruza sectores (web, diseño gráfico, copywriting, maquetación editorial, contabilidad, hipotecas). Es un hecho observado, no una hipótesis.

Sin embargo, la evidencia económica se parte en dos: el **pago tardío de facturas ya emitidas** está cuantificado con datos gubernamentales de calidad (Reino Unido: ~£11.000M/año, 14.000 cierres/año, 86 horas/año por empresa persiguiendo cobros), mientras que el **retraso de proyecto causado por el cliente antes de facturar** no tiene ni un solo estudio independiente con metodología publicada. Las únicas cifras que existen proceden del vendor que vende la solución.

El workaround dominante no es software: es depósito por adelantado, cláusula de dormancy con restart fee, contenido placeholder y escribir el copy uno mismo y cobrarlo. Varios practicantes experimentados documentan públicamente que eso **neutraliza el daño económico sin comprar nada**.

El mercado ya se intentó. El líder de categoría (Content Snare, fundada en 2016, bootstrapped) se estima en ~$990K ARR y ha desplazado "Digital Agencies" al cuarto puesto de su propia página de casos de uso, por detrás de contabilidad, legal e hipotecas. GatherContent fue absorbida por Bynder, ProjectHuddle por Brainstorm Force, y Atarim pivotó a agentes de IA. El segmento adyacente se vende en AppSumo a $59 de por vida.

El patrón de queja más denso en reviews no es de funcionalidad: es que **el cliente final no adopta la herramienta** (12 productos, ~22 fuentes independientes). Y las dos dependencias estructurales del espacio —entregabilidad de email y, si se usa, WhatsApp Business API— tienen dueño ajeno y métricas en conflicto directo con la propuesta de valor.

---

## 2. Problem evidence

Clasificación usada: **[H]** hecho observado · **[A]** afirmación de una fuente (no auditada) · **[I]** inferencia · **[X]** hipótesis sin validar.

### 2.1 Evidencias cualitativas independientes

**E1 — Katelyn Dekle, diseñadora web Squarespace en solitario (EE.UU.)**
Proyectos parados al 80% esperando contenido. **[A]** Declara 4-5 h de email por proyecto y "40-50 horas al mes persiguiendo contenido"; menciona clientes que tardaron **2 años** en entregar y proyectos congelados **10 meses**.
Cita: *"This is quite literally the biggest operational nightmare in the entire web design industry."*
Workaround actual: Kitchen.co (pago único $299) + Tally.so (gratis) + Dubsado.
Herramientas descartadas: Notion, ClickUp, Asana (*"aren't we all sick to death of needing another damn bill to pay?"*) y **Content Snare, descartada explícitamente por precio**.
Fuente: [launchthedamnthing.com](https://launchthedamnthing.com/blog/website-content-collection-system-clients-actually-love) — 25 jun 2025.

**E2 — "Aysha", The CX Toolbox, diseñadora web (probablemente UK)**
Cliente que no firmaba la aprobación de la web porque esperaba una sesión de fotos de marca. **[A]** Consecuencia con cifra: **dos meses parada y "£3,000 of my income sat stuck in limbo"**.
Workaround: milestone billing 40/40/20 atado a *sign-off* y no a fechas; depósito no reembolsable presentado como "booking fee"; **cláusula de dormancy — 30+ días sin contacto → restart fee del 10-25%**; escalado a día 30/45/60; Dubsado para pausar workflows.
Fuente: [thecxtoolbox.com](https://thecxtoolbox.com/client-experience/website-design-payment-terms/) — 9 feb 2026.
*Es la evidencia más limpia del vínculo bloqueo → cobro, con dinero concreto.*

**E3 — Kevin Geary, fundador de agencia web (EE.UU.)**
Publica su política literal: *"A project is considered delayed if our request for assets, information, feedback, approvals, etc., goes without sufficient response for more than five business days."* 45 días → suspendido y se factura el saldo restante; 90 días → abandonado; reactivation fee del 10%.
**[H] Declara que el problema le afectó durante años y que sigue ocurriendo, pero que "ya no nos perjudica económicamente"** — y su solución es 100% contractual, sin software.
Fuente: [geary.co](https://geary.co/how-to-handle-delayed-web-design-projects/) — 18 feb 2023.

**E4 — Hilo de foro SitePoint, "When clients delay the project"**
Discusión entre pares, no marketing. **Blog_Guy [A]**: más del *70% de sus clientes incumplen plazos*, retrasando proyectos "weeks or months". **twyst**: *"I write into my contract that if a project must be delayed but for less than 90 days, I'll charge a restart fee of 20%"*. **jmweb7**: proyecto de 10 meses. **samanime**: *"For every day a client is late, the date when I deliver also delayed"*. **Sega**: usa un cuestionario previo como filtro y admite perder volumen de negocio por ello. **Pedro_Monteiro**: *"there is no real effective way to prevent this, just accept as part of the job"*.
Fuente: [sitepoint.com](https://www.sitepoint.com/community/t/when-clients-delay-the-project/6388) — jul 2010 – feb 2011.

**E5 — Hilo SitePoint, "What to Do if the Client Won't Give Content"**
Workaround dominante y repetido por varios participantes: **escribir contenido placeholder para que el cliente lo corrija** — *"People are much quicker to correct information than fill up blank space."* **muaysteve**: al presionar al cliente, este mató el proyecto. **DCrux**: *"People say a lot of things. You have to plan your business around what they actually do."*
**Dato incómodo:** el propio autor del hilo se auto-refuta después — *"The real issue ended up being me – I said something she didn't understand."*
Fuente: [sitepoint.com](https://www.sitepoint.com/community/t/what-to-do-if-the-client-wont-give-content/61011) — jun-jul 2010.

**E6 — Graphic Design Forums (UK), "How to deal with clients who waste your time"**
Diseñadora gráfica UK: cliente que encargó una web **hace seis meses** y no ha entregado fotos, copy ni ilustraciones. Workarounds del hilo: aparcar el proyecto, sistema de slots con pérdida de turno, 50% por adelantado, contratar copywriters. Un participante señala una palanca específica del sector web: controlar dominio y hosting da *"pretty much absolute power"* ante el impago.
Fuente: [graphicdesignforums.co.uk](https://www.graphicdesignforums.co.uk/threads/how-to-deal-with-clients-who-waste-your-time.10731/) — abr-jun 2014.

**E7 — Adobe Community, maquetadora freelance (InDesign)**
Cliente desapareció en 2019 tras pagar **50% de depósito** y reaparece **5,5 años después** con un Word lleno de cambios.
Fuente: [community.adobe.com](https://community.adobe.com/questions-91/client-disappeared-for-five-and-a-half-years-wants-to-finish-the-project-now-1500144) — 11 mar 2025.
**[I]** El depósito del 50% fue exactamente lo que evitó la pérdida total: refuerza que la mitigación efectiva es financiera, no operativa.

**E8 — Jennifer Bourn, brand strategist (EE.UU.)**
El protocolo más formalizado encontrado: *Dormancy Clause* (30 días → archivado, reactivation fee de $500 en su ejemplo), *Dormancy Cancellation* (45 días → contrato auto-terminado, sin reembolso ni entregables), *Expiration Date Clause*. Protocolo de seguimiento manual en **días 7, 14, 21, 25, 30, 42 y 45**, incluyendo llamada, buzón de voz y **carta certificada**.
Fuente: [jenniferbourn.com](https://jenniferbourn.com/managing-clients-who-disappear/) — 26 oct 2020 (act. 1 mar 2023).
**[I]** Una secuencia manual de 7 pasos a lo largo de 45 días es exactamente el tipo de proceso que la gente dice olvidar.

**E9 — Caroline Gibson, copywriter freelance (Londres)**
Cláusula literal: *"Should you for any reason fail to maintain communication with me for 21 days, I reserve the right to invoice for all work to date."* Reserva solo el **10%** para la factura final "para minimizar el impacto si hay retrasos".
**Matiz honesto:** en su otro post **no** vincula directamente retraso del cliente con impago; separa los dos problemas.
Fuente: [carolinegibson.co.uk](https://www.carolinegibson.co.uk/copywriting-project-delays/) — 10 abr 2019.

**E10 — Web Designer Academy (formadora, EE.UU.), testimonios de dos alumnas**
*Coleman*: el cliente entrega tarde y, cuando llega, ya ha cambiado de dirección → **rehacer trabajo ya hecho, sin cobrar**. *Megan*: pidió contenido "about a million times" por email sin respuesta; tras diseñar dos páginas, el cliente tardó y dijo que ya no encajaba con su visión.
Fuente: [webdesigneracademy.com](https://webdesigneracademy.com/the-web-designers-guide-to-dealing-with-difficult-clients/) — 18 mar 2026.

**E11 — Chris Key, estudio web Rubber Duckers (Winchester, UK)**
*"The agency can't progress because there's nothing to put in the templates. The whole project sits there bleeding momentum."* **[A]** Afirma, sin fuente, que una decisión cambiada en la semana 6 cuesta "roughly ten times" más que en la semana 1 y que el scope creep añade "20 to 30 percent" al tiempo de build. **Trátese como afirmación de marketing, no como dato.**
Fuente: [rubberduckers.co.uk](https://rubberduckers.co.uk/why-web-design-projects-run-late/) — 3 jul 2026.

**E12 — Reviews verificadas de Content Snare (quién paga por esto, y en qué sector)**
Jordan P., broker hipotecario comercial: antes, *"collecting documents meant endless email chains, missing attachments, and constantly following up with clients"*. Ewen F., contabilidad: *"cut down our administration time on collecting information requests by 75%"*. Lee C., contabilidad: reporta -80% de emails diarios. Fredinand Silot (Trustpilot, 3 jun 2026): *"my biggest challenge is usually chasing clients for content and information"*.
Fuentes: [Capterra](https://www.capterra.com/p/167019/Content-Snare/reviews/) · [G2](https://www.g2.com/products/content-snare/reviews) · [Trustpilot](https://www.trustpilot.com/review/contentsnare.com).
**Señal a la contra en la misma fuente:** el perfil de Trustpilot tiene **9 reseñas en total y 1 en los últimos 12 meses** — volumen bajísimo para una categoría descrita como el mayor cuello de botella de una industria.

**E13 — Heidi Turner, escritora freelance**
Se incluye deliberadamente porque **refina el enunciado**: su problema es impago tras entregar, no bloqueo antes de entregar. Revista que no pagó 2 de 3 ediciones, *"it wasn't enough money to go after in small claims court"*; retraso de un año de otro cliente. Solución: depósito, copyright condicionado al pago, suspender trabajo.
Fuente: [happyfreelancing.substack.com](https://happyfreelancing.substack.com/p/client-ghosting-my-journey-through) — 30 may 2024.

### 2.2 Qué se puede afirmar y qué no

- **[H]** El fenómeno existe, es transversal a sectores y persiste durante 16 años de registro público.
- **[H]** Existe un conjunto reconocible de respuestas contractuales estandarizadas (dormancy, restart fee, depósito, facturar a los 21-45 días de silencio) que múltiples practicantes independientes han convergido en adoptar.
- **[A/X]** Las cifras de horas y de proyectos parados son todas autorreportadas o de vendor. **No hay evidencia suficiente para afirmar una magnitud media del problema.**
- **[H]** El vínculo retraso → impago **no es automático**: varios practicantes (Geary, Gibson, Brunton) lo rompen deliberadamente desacoplando el calendario de cobro del de entregables del cliente.

---

## 3. Current workflow

### 3.1 El stack real

| Capa | Herramienta dominante | Evidencia |
|---|---|---|
| Petición inicial | Email + checklist en Word/PDF; Google Forms, Tally.so, Jotform | E1, E5, E14 |
| Recepción de archivos | Google Drive, Dropbox, WeTransfer | E1; Paige Brunton usa Google Drive |
| Seguimiento | **Email manual + recordatorio mental + llamada** | E4, E8, E9 |
| Registro de estado | Hoja de cálculo o checklist propio; a veces nada | E4; comentario citado en dev.to: *"I always wonder if I could've just managed it in a fucking spreadsheet"* |
| Desbloqueo | **Contenido placeholder / lorem ipsum** para provocar corrección | E5, comentarios Elegant Themes |
| Mitigación económica | Depósito 25-50%, milestone billing desacoplado, dormancy + restart fee | E2, E3, E8, E9 |
| Eliminación del problema | **Vender el contenido como servicio**: escribir el copy, hacer las fotos, subcontratar copywriter | Comentarios Elegant Themes; Pressable |

### 3.2 ¿Hay un ugly workflow real?

Sí, pero con un matiz decisivo. El *ugly workflow* existe (email + hoja de cálculo + memoria + carta certificada en el caso extremo de E8), pero **no es el único estado estable**. Hay un segundo estado estable, también documentado, en el que el freelancer ha resuelto el problema por contrato y ya no percibe dolor operativo (E3, Paige Brunton). Es decir: no todo el mercado está en el estado feo, y salir del estado feo no requiere comprar software.

### 3.3 Por qué siguen usando el workaround

1. **Es gratis y ya está instalado.** Google Forms + Drive + email es el sustituto por defecto, y es suficientemente bueno para el caso medio.
2. **Precio.** E1 descarta Content Snare explícitamente por coste, y elige un pago único de $299.
3. **El cliente no adopta la herramienta** — ver sección 8. El email es el único canal con adopción del 100% garantizada.
4. **Heterogeneidad.** Recogido en la discusión sectorial: *"agency workflows are messy and full of exceptions. Client onboarding isn't the same for every client"* (r/DigitalMarketing, citado vía [dev.to](https://dev.to/lisasakura/why-agency-owners-complain-about-onboarding-but-never-fix-it-3m5m), 14 may 2026).
5. **Marco mental.** Varios lo enmarcan como problema humano, no de herramientas: *"Tools and process do not fix human problems"* ([Medium](https://evatorium.medium.com/tools-and-process-do-not-fix-human-problems-62a5d4c7b6ae), 22 jun 2020).

---

## 4. Trigger and frequency

### 4.1 Triggers externos identificados

| Trigger | Naturaleza | Inevitable |
|---|---|---|
| Firma del contrato → kickoff y petición de materiales/accesos | Por proyecto | Sí |
| Fin de la fase de diseño → se necesita contenido real | Por proyecto | Sí |
| Entrega de una versión → se espera feedback | Por ronda de revisión (múltiple por proyecto) | Sí |
| Cierre de fase → se espera *sign-off* para facturar el hito | Por hito | Sí, si se factura por hitos |
| Silencio del cliente durante N días | Continuo | Sí |
| Vencimiento de la factura | Por factura | Sí |

**[H]** Todos los triggers son externos e inevitables mientras exista el modelo de proyecto por hitos. Esto es favorable: el usuario no tiene que "acordarse" de que el problema existe; el problema le llega solo.

### 4.2 Frecuencia

**[I]** Una agencia de 2-20 personas con 3-10 proyectos activos y 2-4 rondas de revisión por proyecto genera del orden de varios triggers por semana. Un freelancer solo, con 2-4 proyectos, probablemente uno o dos por semana. **No hay evidencia externa que confirme estas frecuencias**; son una inferencia a partir de los ciclos descritos en E1-E11.

### 4.3 Valor inmediato vs. disciplina sostenida — la penalización

Aquí hay un desdoblamiento que conviene no esconder:

- **Valor inmediato: parcial.** Enviar una petición estructurada da un beneficio el mismo día (el freelancer deja de redactar el email). Esto es bueno.
- **Disciplina sostenida: alta, y en el lado equivocado.** El valor real (menos proyectos parados, cobros más rápidos) solo aparece si (a) el freelancer configura y mantiene el sistema en *todos* sus proyectos, y (b) **el cliente entra y lo usa**. La segunda condición no está bajo control del usuario que paga.

**[I]** Esto debe penalizarse doblemente respecto a un problema con trigger externo y valor inmediato unilateral: no basta con la disciplina del comprador, hace falta la cooperación de un tercero que no paga, no eligió la herramienta y ya está demostrando que no coopera. Es el mismo defecto estructural que hunde a los portales de cliente (sección 8).

---

## 5. Economic impact

### 5.1 Lo que sí está cuantificado: pago tardío de facturas emitidas

| Cifra | Fuente | Calidad |
|---|---|---|
| Los pagos tardíos cuestan **~£11.000M/año** a la economía británica (~0,4% del PIB) | DBT / Office of the Small Business Commissioner, estudio de London Economics, encuesta n=1.455 (ene-feb 2025) | **Primario gubernamental** |
| **14.000 empresas cierran al año** en RU por esta causa (38/día, ~40.000 empleos) | Ídem | Primario gubernamental |
| **86 horas/año por empresa afectada** persiguiendo cobros; 133M horas agregadas; el 22% de las empresas declara dedicar tiempo a esto | Ídem | Primario gubernamental |
| El componente "tiempo de personal persiguiendo cobros" vale **£2.259M/año** | Ídem | Primario gubernamental |
| **PMP España = 80,5 días** (>20 días sobre el máximo legal de 60); sector servicios 70,6 días | CEPYME, Observatorio de la Morosidad, 2º sem. 2025 | Primario (panel de facturas); patronal con interés de lobby |
| Solo el **30,4%** del importe facturado en España se cobra puntualmente o por anticipado | Ídem | Ídem |
| Coste financiero de la morosidad en microempresas españolas: **€611M** (4T 2025, baja desde €715M en 2024) | Ídem | Ídem |
| Retraso medio **real** sobre vencimiento: RU 8,0 d · EEUU 7,8 d · Canadá 9,7 d · Australia 6,6 d | Xero Small Business Insights, trim. dic 2025 | **Primario transaccional**, sobre facturas reales |
| **59%** de pymes de EEUU con facturas vencidas >30 días (47% en 2025); importe medio adeudado **$17.700**; **39%** dice que un solo pago tardío dificultó cubrir nóminas | Intuit QuickBooks, Small Business Late Payments Report 2026 | Encuesta; **Intuit vende facturación y cobros** |
| **50%** de freelancers tuvo problemas de cobro en un año; media de ingresos impagados **$5.968 (13% de sus ingresos anuales)**; espera máxima media 98 días; solo 28% usaba contrato escrito | Freelancers Union, *The Costs of Nonpayment*, n=5.358 | Primario y sin sesgo comercial, pero **de 2015** |

**Discrepancia importante que no conviene ocultar:** las encuestas de percepción (Intrum: brecha de 20 días, 12% de ingresos cobrados tarde; Atradius: 47% de facturas vencidas) describen un problema mucho más severo que los datos transaccionales de Xero (7,8-9,7 días de retraso medio). **[I]** Ambas pueden ser ciertas si la distribución tiene cola larga: la media se aplasta con muchas facturas casi puntuales, y el dolor está en la cola. Anclar un caso de negocio solo en las encuestas sobreestimaría el problema. Nota adicional: **Intrum es la mayor empresa de recobro de Europa**; su negocio depende de que esto se perciba como grave.

### 5.2 Lo que NO está cuantificado: el retraso causado por el cliente antes de facturar

**Este es el hueco central de toda la investigación, y es un hallazgo, no un fallo de búsqueda.**

No existe ningún estudio independiente, con muestra representativa y metodología publicada, que cuantifique cuántos días o cuánto dinero pierden freelancers y agencias por esperar materiales, accesos, feedback o aprobaciones. Lo que hay:

- **Content Snare, encuesta a sus propios clientes de pago**: 25 h/mes → 5,1 h/mes recopilando información (-71%); **75% de proyectos "en el limbo"** → 20%; turnaround 3 → 1,5 semanas; ahorro mediano $500/mes; ROI 23,9x. Fuente: [contentsnare.com/results-survey](https://contentsnare.com/results-survey/) (6 ago 2021, act. 2 sep 2024). **Tasa de respuesta ~1 de cada 10, muestra autoseleccionada, diseño pre/post basado en recuerdo. No es evidencia de mercado.**
- **HubSpot, Marketing Agency Growth Report** (n=763, dic 2017-ene 2018), encuesta independiente aunque antigua: 43% de agencias dice no tener tiempo para tareas administrativas; 57% tiene menos de 3 meses de caja. Pero **el 85% declara que el trabajo de cliente se entrega a tiempo de forma consistente** — dato que contradice la hipótesis, o al menos indica que las agencias no perciben el retraso del cliente como un fallo propio de entrega.
- **PMI Pulse of the Profession 2025** (n=2.841): no desglosa scope creep ni retrasos imputables al cliente.
- **Promethean Research, State of Digital Services 2026** (n=119 líderes de agencia): da tamaño medio (31 empleados), crecimiento 7,5% y margen neto 13%, pero **ningún dato de retrasos de cliente**.
- **Parakeeto / Productive.io**: no se localizó ningún benchmark primario publicado de utilización o tiempo no facturable. Todo lo que circula es contenido SEO sin fuente trazable.

**Conclusión de la sección: no hay evidencia suficiente para afirmar el tamaño del daño económico del problema tal y como está enunciado.** Sí la hay para el problema adyacente del pago tardío.

---

## 6. Buyer and willingness to pay

### 6.1 Quién sufre, quién usa, quién compra

- **Sufre:** el freelancer solo, o el PM / account manager de una agencia pequeña. Es quien persigue.
- **Usa:** el mismo, **más el cliente final**, que es usuario obligatorio y no paga (ver sección 8 — esto es el defecto estructural del espacio).
- **Compra:** en freelance solo, la misma persona (bueno: ciclo corto, sin aprobación). En agencia de 10-20, el socio/dueño. Hay evidencia directa del split: *"los PMs sufren el dolor diario pero no deciden la compra; los socios aprueban el gasto pero no ven la fricción"* ([Indie Hackers](https://www.indiehackers.com/post/i-built-an-ai-tool-for-agencies-spent-40-days-on-seo-and-community-and-still-have-zero-paying-strangers-heres-what-i-m-seeing-c9d36140dd), jun 2026).

### 6.2 Evidencia de gasto actual

**[H]** Hay gasto real, verificado en páginas de pricing el 20-sep-2026:

- Intake: Content Snare **$35-$215+/mes** (sin plan gratis).
- Aprobación: Filestage y Ziflow **$199/mes** de entrada de pago; ReviewStudio $12-15/usuario; Pastel $29-35; BugHerd $50; Markup.io $79.
- CRM de cliente: HoneyBook $29/mes, Dubsado $335/año, Bonsai $9-49/usuario, Moxie $10/mes, Plutio $19/mes.
- Portales: SuiteDash $19/mes, ManyRequests $59/mes, Wayfront (ex-SPP) **$129/mes**, Clinked $239/mes de segundo escalón.
- Cobro: Stripe Invoicing 0,4% por factura pagada; Anchor $0/mes + **$5 por cobro**; Ignition desde ~$39/mes (cifra vía G2, **no verificada en la web oficial**).
- Servicios humanos: contratar copywriter, hacer las fotos uno mismo y cobrarlas, personal administrativo (E6, E14).

### 6.3 Las tres señales que limitan la willingness to pay

1. **El líder de categoría factura poco.** Content Snare, fundada en 2016, bootstrapped, se estima en **~$990K ARR, $83,3K MRR, 9 empleados** ([GetLatka](https://getlatka.com/companies/contentsnare.com), hito jul-2025; **estimación de tercero, no auditada**). Contexto cualitativo del propio fundador vía [Starter Story](https://www.starterstory.com/content-snare-breakdown) (22 dic 2024): estaban *"stuck at $300k ARR"* antes de pivotar hacia contables.
2. **El precio ancla del segmento está roto.** Todo el espacio adyacente se ha vendido en AppSumo como *lifetime deal* a $59: OkaySend ($59, antes $300), Sinosend ($59), Client Portal, ClientVenue, ClientFol.io, Sizle, AgencyPro ($59-799, **empresa fundada en julio de 2025 y ya en AppSumo**). Ratings basados en 3-97 reseñas: productos diminutos. Fuente: [AppSumo](https://appsumo.com/search/?query=client%20portal). **[I]** Un mercado sano no se vende a $59 de por vida; la LTD indica retención mala y necesidad de caja adelantada.
3. **Nadie publica números.** No se localizó **ninguna** declaración pública de MRR/ARR de los fundadores de Content Snare, Pastel, ManyRequests o Wayfront en Indie Hackers, Baremetrics Open Startups, MicroConf o X, pese a que James Rose (Content Snare) es una figura pública activa en el ecosistema bootstrapped. **[I]** En una escena que celebra el build-in-public, el silencio suele significar que las cifras no son celebrables.

### 6.4 Dónde sí hay dinero

**[H]** El mismo producto, aplicado a **contabilidad, legal e hipotecas**, es donde el líder ha ido a buscar ingresos: la página de casos de uso de Content Snare lista hoy, en orden: *Accounting & Bookkeeping, Legal, Mortgage & Finance, Digital Agencies*, y reconoce que el producto se diseñó originalmente para recoger contenido web ([contentsnare.com/uses](https://contentsnare.com/uses/), verificado 20-sep-2026). Ahí el trigger es una obligación documental regulada, el coste del retraso recae en un profesional facturando por hora, y el cliente final **tiene que** entregar.

---

## 7. Existing market

### 7.1 Mapa por categorías (precios verificados el 20-sep-2026)

| Producto | Categoría | Target | Entrada | Gratis | Madurez |
|---|---|---|---|---|---|
| **Content Snare** | Intake | Agencias, contables, legal, hipotecas | $35/mes anual ($42 mensual) | No | PYME bootstrapped, ~$990K ARR est. |
| **Ahsuite** | Portal | Freelance, agencias pequeñas | $6,50/mes anual | **Sí (10 portales)** | Indie (19 reviews Capterra) |
| **Kitchen.co** | Portal | Agencias pequeñas | $29/usuario/mes | **Sí (2 users)** | Indie; LTD "retiring soon" |
| **SuiteDash** | Portal todo-en-uno | PYME, agencias | $19/mes · lifetime $2.240 | No | PYME (619 reviews G2) |
| **Assembly** (ex-Copilot) | Portal | Firmas de servicios | $20/mes anual (web nueva) | Sí | VC Series A (YC Continuity) |
| **Wayfront** (ex-Service Provider Pro) | Portal | Agencias productizadas | **$129/mes** ($99 anual) | No | PYME bootstrapped, rebrand en curso |
| **ManyRequests** | Portal + proofing | Agencias productizadas | $59/mes ($39 anual) | No | Indie (**1 review en G2**) |
| **Clinked** | Portal | PYME → enterprise | $11/usuario → $239/mes | No | PYME, deriva enterprise |
| **Filestage** | Aprobación | Equipos creativos mid-market | **$199/mes** | Sí | VC semilla; ~$4M ARR est. |
| **Ziflow** | Aprobación | Agencias → enterprise | **$199/mes** anual | Sí | VC Series A; ~$22,5M ingresos est. (2024) |
| **BugHerd** | Feedback web | Agencias web | $50/mes (5 users) | No | PYME consolidada |
| **Pastel** | Feedback web | Diseñadores, agencias | $29/mes anual | Sí | PYME |
| **Markup.io** | Aprobación | Equipos medianos | **$79/mes** | **No (eliminado)** | PYME; free killed, subida ~2,7x |
| **Frame.io** | Aprobación vídeo | Creativos → enterprise | $15/miembro/mes | Sí | **Parte de Adobe** |
| **ReviewStudio** | Aprobación | Agencias pequeñas | $12-15/usuario/mes | Sí | Indie, baja notoriedad |
| **GoVisually** | Aprobación | Agencias → **CPG compliance** | $16/usuario/mes | No | PYME pequeña, pivotando |
| **HoneyBook** | CRM cliente | Solopreneurs | $29/mes anual | No | **VC, ~$2,4B valoración** |
| **Dubsado** | CRM cliente | Freelance creativo | $335/año | No | PYME consolidada |
| **Bonsai** | CRM cliente | Freelance → agencias | $9/usuario/mes anual | No | PYME/VC |
| **Moxie** | CRM cliente | Freelance solo | $10/mes anual | No | Indie |
| **Plutio** | CRM cliente | Freelance, agencias | $19/mes (9 clientes activos) | No | Indie; producto activo pero reputación dañada |
| **Anchor** | Cobro automático | Contables, agencias | **$0/mes + $5 por cobro** | Sí | VC; sesgo EE.UU. (ACH) |
| **Stripe Invoicing** | Cobro | Cualquiera | 0,4% por factura pagada | — | Gigante — **es el suelo de precio** |
| ~~Optimi~~ | — | — | **Dominio a la venta ($4.999)** | — | **No existe** |
| ~~WeTransfer Portals~~ | Intake | — | **Cerrado 22-dic-2025** | — | **Muerto** |

### 7.2 Movimientos estructurales del mercado (verificados)

- **WeTransfer Portals cerró.** Creación bloqueada el 22-oct-2025, subidas el 22-nov-2025, **borrado total de contenido el 22-dic-2025** ([help center oficial](https://wetransfer.com/help-center/troubleshooting/reviews-portals-sunset)). Contexto: Bending Spoons compró WeTransfer en 2024. Demanda huérfana.
- **Markup.io eliminó su plan gratis y subió Pro de ~$29 a $79/mes**; el precio actual está verificado en su web, el histórico procede de un análisis de terceros (marklayer.app, ago 2026). Abandono explícito del segmento pequeño.
- **Service Provider Pro → Wayfront**, con precio de entrada ahora en $129/mes. **Copilot → Assembly**, con dos páginas de pricing incoherentes entre sí (rebrand a medias).
- **GatherContent fue adquirida por Bynder** (3 mar 2022) y absorbida como "Content Workflow by Bynder": dejó de existir como producto independiente para agencias.
- **ProjectHuddle** fue adquirido por Brainstorm Force (2021) y renombrado **SureFeedback** (7 nov 2023): módulo de una suite.
- **Atarim**, el player más visible de feedback visual en WordPress, tiene **solo 1.000+ instalaciones activas** y se ha reposicionado como *"AI Agency for WordPress"*.

**[I]** Tres de los cuatro referentes históricos de la categoría han sido absorbidos, han pivotado o han cambiado de ICP. El cuarto sigue independiente a ~$1M ARR. Eso no es un mercado emergente; es un mercado que ya se intentó y no compuso.

### 7.3 Nadie ha unido las cuatro piezas

Content Snare persigue materiales pero no aprueba ni cobra. Filestage/Ziflow aprueban pero no persiguen ni cobran. HoneyBook/Dubsado cobran pero no persiguen. Anchor cobra automáticamente pero no recoge nada. **ManyRequests y Kitchen.co son los únicos que cruzan intake + proofing + cobro, y ambos son indies diminutos.** **[X]** Que nadie lo haya unido puede significar que hay hueco, o que unirlo no aumenta la disposición a pagar. No hay evidencia que discrimine entre las dos.

---

## 8. Negative reviews and market gaps

Agrupación por patrón, con número de productos afectados y de fuentes independientes localizadas.

### Patrón 1 — El cliente final no adopta la herramienta (12 productos, ~22 fuentes) — **el más denso**

Casi nadie escribe "mi cliente se niega a usar el portal". Se expresa indirectamente, como carencia del producto:

- **Content Snare** (la mayor densidad, paradójicamente el producto más específico): *"A few clients still felt this was an extra step they didn't want to use"* (Philip M., jun 2020); *"clients found it very frustrating to use"* (John C., nov 2019); *"clients have had difficulty 'signing up'"* (Alan H., oct 2017); *"Some of our clients find it difficult to use, especially if they are only working from their phones"* y *"clients complaining about the constant reminders"* (Lynn B., 12 jun 2026); un cliente lo percibe *"more impersonal than emailing"* (Mai P., nov 2024). El propio vendor publica un artículo de ayuda titulado *"What if my client doesn't know how to use Content Snare?"*.
- **Plutio** — la cita más directa del corpus: *"I don't see myself being able to get my clients onboard with using the software with me on projects"* (Melissa D., feb 2019, [Software Advice](https://www.softwareadvice.com/business-management/plutio-profile/reviews/)); canceló dos veces.
- **ReviewStudio**: *"Some of our clients have a higher barrier to entry and feel hesitant to try a new tool"* (Marin H., ago 2023).
- **BugHerd**: clientes *"hesitant or don't know how to install the Chrome extension"* (Daniel T., jun 2026).
- **Ahsuite**: *"there doesn't seem to be a way to just send a link and get it started for them"* (Anthony N., ene 2023); usuarios que rara vez entran y obligan a follow-up manual por Teams/email — **vuelta al canal informal**.
- **Assembly (ex-Portal)**: *"It's not mobile-friendly, so our clients can't use it on their phones"* (Paul C., ago 2026).
- **Frame.io, Filestage, Ziflow, SuiteDash, Dubsado, HoneyBook**: variantes de "el cliente necesita formación/guía".

**Fricción concreta más citada: el alta y el login del cliente**, no la UI. Sign-up (Content Snare), añadir usuarios (ReviewStudio), instalar extensión (BugHerd), magic links sin instrucciones (Assembly), no poder "solo mandar un link" (Ahsuite).

**Evidencia de apoyo, no orgánica (marcada como tal):** un caso publicado por una agencia describe una clínica que invirtió $12.000 en un portal de pacientes y **solo el 30% entró más de una vez**, con las llamadas aumentando y *"Most still email documents directly instead of using the upload feature"* ([digitalsage.agency](https://digitalsage.agency/why-client-portals-systems-fail-businesses/), 2 jul 2025). Contenido de vendor, pero coherente con las reviews.

**Evidencia en contra del patrón (obligatoria):** Filestage tiene una review que valora justo lo opuesto — para el revisor externo *"no need for him to sign up, which makes it really easy to use"* (Paul H., jul 2017). La revisión de 22 portales de E1 no contiene quejas de clientes que rechacen portales. Y Content Snare mantiene **4,9/5 con 101 reviews en Capterra**: el patrón existe pero es minoritario en volumen dentro de cada producto.

### Patrón 2 — Precio: subidas abruptas y modelo por asiento (9 productos, ~14 fuentes)

- **Markup.io**: *"Markup.io just went up 280% from last year to this year"* + *"Pay the 280% upgrade, or they DELETE your entire space"* (Verified Reviewer, 6 ago 2025, **1 estrella**).
- **Filestage**: *"subscription was changed to a plan with a 76% price increase without our explicit consent"* (ago 2026).
- **HoneyBook**: *"Honeybook went from $200 to over $600"* (Chelsea Walker, ~17 sep 2026, 1 estrella, Trustpilot).
- **Jotform**: *"They renewed my annual subscription at triple the price...after giving me no warning"* (Leona Oates, 1 sep 2026, 1 estrella).
- Por asiento: Ziflow, BugHerd, Frame.io, Assembly, Bonsai, ManyRequests.

### Patrón 3 — App móvil inexistente o mala (9 productos, ~11 fuentes)

Dubsado, Bonsai, Assembly, Ahsuite, BugHerd, HoneyBook, Filestage (*"Theres no iOS and Android apps. Relying on web browser makes it clunky"*), Frame.io, Moxie. **Cruce relevante:** la review de Content Snare que reporta fallo de clientes lo atribuye precisamente a clientes *"only working from their phones"*.

### Patrón 4 — Recordatorios mal calibrados en ambas direcciones (6 productos, ~8 fuentes)

El mecanismo diseñado para perseguir al cliente genera su propia queja. **Exceso:** Content Snare (*"clients complaining about the constant reminders"*, *"auto reminders should be off by default"*). **Defecto:** Ahsuite (sin alertas automáticas), ReviewStudio (*"Workflow notifications sometimes don't get delivered"*), Filestage (notificaciones tardías), GoVisually (*"a spam of emails"*, y el reviewer dice que por eso **no lo usa con clientes freelance**).

### Patrones 5-9 (menor densidad)

Curva de aprendizaje para el propio freelancer (7 productos; SuiteDash y Dubsado los peores); bugs y fiabilidad (8); soporte malo o robotizado (8); facturación abusiva o imposible de cancelar (5, con Frame.io y HoneyBook/BBB como casos graves); integraciones frágiles (5); producto abandonado (Plutio, 5 fuentes independientes en Trustpilot); features retiradas sin aviso (HoneyBook, SuiteDash, Jotform).

### Gaps de mercado identificados (no son propuestas de features)

1. **Hueco de precio real entre $0 y $199** en la categoría de aprobación: Filestage y Ziflow saltan de gratis a $199/mes. Solo ReviewStudio y Pastel ocupan esa franja, ambos con poca notoriedad.
2. **Aprobación por externos sin cuenta**: Figma Buzz exige que *"Reviewers must already have access to the file"*; Canva apunta a Enterprise. Nadie grande ha resuelto la aprobación de alguien que no tiene cuenta en nada.
3. **Subida de archivos en formularios públicos gratuitos**: la documentación de Notion Forms no la menciona.
4. **Demanda huérfana**: cierre de WeTransfer Portals, subida de Markup.io, desaparición de Optimi.

**[I]** Los gaps 2 y 3 son huecos *de feature*, no de categoría, y ambos los puede cerrar Notion o HoneyBook en un sprint.

---

## 9. Distribution

### 9.1 Comunidades: audiencia grande, canal cerrado

Tamaños (vía [The Hive Index](https://thehiveindex.com/platforms/reddit/), directorio de terceros; **Reddit no fue accesible directamente**): r/entrepreneur 5,3M · r/webdev 3,3M · r/smallbusiness 2,5M · r/marketing 2,0M · r/web_design ~977K · r/freelance 699K · r/DigitalMarketing 464K · r/Upwork 198K.

Reglas de autopromoción, según un estudio de terceros que dice haber extraído las reglas en vivo de 49 subreddits ([OneUp, 13 jul 2026](https://oneup.today/blogs/reddit-selfpromo-rules-study-2026)): **39% prohíben la autopromoción; 61% la prohíben o la restringen fuertemente**. r/freelance: prohibida. r/Entrepreneur: prohibida. r/marketing: "zero tolerance". r/smallbusiness: solo hilo semanal.

Comunidades de pago: **Agency Hackers (UK)** cuesta £250-450/mes y su página de membresía dice explícitamente *"Membership isn't open to people who mostly supply services to agencies"*, remitiendo a su página de partnerships comerciales. **The Futur** tiene 2M de suscriptores en YouTube pero su Pro Group son ~900 miembros y su negocio es vender formación. **Agency Mavericks** ya ha hecho contenido con el fundador de Content Snare: el incumbente tiene la relación.

**[I]** Las comunidades con los compradores correctos o prohíben a los vendors o monetizan el acceso. Eso convierte la distribución comunitaria en publicidad, no en un growth loop. Presupuéstese como CAC.

### 9.2 SEO: el head lo posee el incumbente, el long-tail no convierte

SERPs reales consultadas el 20-sep-2026:

- *"how to get content from clients"* → resultado #1: **Content Snare**.
- *"client content collection"* → **Content Snare** + listicles de agregadores.
- *"client won't send content"* → gana un hosting ([Pressable](https://pressable.com/blog/i-built-the-site-but-the-client-hasnt-delivered-content-now-what/)), no una herramienta. SERP floja = hueco, pero es una consulta de desahogo.
- *"website content gathering template"* → dominan **plantillas gratis** (incluida una plantilla Notion gratuita distribuida vía Figma Community). Intención "dame algo gratis".
- *"client portal for freelancers"* y *"client approval software"* → SERPs saturadas de vendors pequeños y **granjas de listicles auto-generadas**.

**Indicador revelador:** existe un enjambre de micro-competidores que ya solo se atacan entre sí con páginas "X alternative" — Huddlekit vs Superflow/Feedbucket/Pastel/SureFeedback, Reviso vs SureFeedback/Feedbucket, Feedbucket vs Atarim, y media docena publicando "alternativas a Content Snare". **[I]** Eso es el aspecto de un mercado comoditizado, con barrera de entrada nula y sin ganador fuera del incumbente informacional.

**No se citan volúmenes de búsqueda**: no hubo acceso a herramientas SEO. Todo lo anterior es análisis de SERP.

### 9.3 Marketplaces

- **AppSumo**: la señal más dura. Todo el espacio se ha vendido como lifetime deal (ver §6.3).
- **WordPress**: el plugin "Client Portal" tiene 3.000+ instalaciones activas; Atarim, 1.000+. Escala irrelevante.
- **Shopify**: el proofing que existe resuelve merchant ↔ consumidor, no agencia ↔ cliente. **Mismatch estructural**: la app se instalaría en la tienda del cliente, pero quien paga sería el freelancer. Además, el nuevo Dev Dashboard (ene 2026) rompió el permiso de colaborador "Develop apps".
- **Webflow Marketplace**: revisión de 10-15 días hábiles, sitio publicado, vídeo demo, credenciales para revisores. Legítimo pero lento y de audiencia estrecha.

### 9.4 Evaluación cualitativa

| Criterio | Evaluación |
|---|---|
| ¿Fáciles de identificar? | **Sí.** Directorios, marketplaces de partners, LinkedIn. |
| ¿Están agrupados? | **Sí**, pero en espacios cerrados o de pago para vendors. |
| ¿Buscan activamente soluciones? | **Parcial.** Buscan plantillas gratis y consejos; la búsqueda transaccional está saturada. |
| ¿SEO viable? | **Difícil.** Head ocupado por el incumbente desde hace años; long-tail de desahogo, no de compra. |
| ¿Requiere venta B2B? | En freelance solo, no. En agencias de 10+, sí (split buyer/user documentado). |
| ¿CAC problemático? | **No se estima un CAC** por falta de datos. Pero todos los canales identificados son de pago o requieren años de presencia orgánica. |

---

## 10. Market size

### 10.1 Datos primarios oficiales

**Autónomos, UE-27, 2025** (Eurostat, EPA, `lfsa_esgan`): 26,07M autónomos totales (12,9% del empleo), de los cuales **17,68M sin asalariados**. España: 3,03M totales, **2,14M sin asalariados**.

**EE.UU.**: el 28% de los *knowledge workers* trabaja de forma independiente, generando $1,5 billones en 2024 (Upwork Research Institute, n=3.000, metodología declarada y anclada en BLS; **Upwork es parte interesada**).

**Agencias pequeñas, UE-27, 2023** (Eurostat SBS `sbs_sc_ovw`):

| NACE | 0-1 persona | 2-9 | 10-19 | 20-49 |
|---|---|---|---|---|
| M73.1 Publicidad | 267.284 | 60.996 | 6.203 | 3.130 |
| M74.1 Diseño especializado | 260.326 | 26.613 | 1.600 | 651 |

### 10.2 Orden de magnitud

- **Universo teórico (TAM):** millones. 17,7M de autónomos sin asalariados en la UE, más el equivalente estadounidense.
- **ICP verificado de agencias de 2-19 personas, solo en publicidad y diseño especializado, UE-27: ~95.400 empresas.** Es un **suelo**: excluye desarrollo web y software (J62), consultoría de marketing (M70.2) y producción audiovisual (J59). Con esos códigos incluidos, el orden de magnitud realista para la UE estaría en **cientos de miles**.
- Más un universo adyacente de **~527.600 operadores de 0-1 persona** solo en esos dos códigos.

**Mercado realmente accesible para un producto indie: decenas de miles de compradores, no cientos de miles.** El razonamiento: el canal de adquisición está cerrado o es de pago (§9), el ARPU observado en el segmento freelance está entre $10 y $40/mes, y el precio ancla está contaminado por lifetime deals de $59. Con ~$1M ARR para el líder de categoría tras 10 años, la conversión efectiva del universo teórico al negocio real es de aproximadamente **1 de cada 1.000**.

**No verificado:** número de agencias pequeñas en EE.UU. (la API del Census requiere clave y los ficheros SUSB estaban bloqueados) y número de freelancers en Reino Unido. La ruta para obtener el dato estadounidense es CBP 2023, NAICS 541810 / 541430 / 541511 / 541613, cruzando por `EMPSZES`.

---

## 11. Global portability

### **ALTA para el núcleo del problema.**

Justificación:

- **[H]** El fenómeno está documentado en EE.UU. (E1, E8, E10), Reino Unido (E2, E6, E9, E11), Australia (origen de Content Snare), Nueva Zelanda (Katrina Pace) y Filipinas (review de Trustpilot). Es un problema de coordinación entre dos partes, no de cumplimiento normativo local.
- **[H]** No hay licencias, fuentes de datos nacionales, sistemas administrativos ni procedimientos legales que condicionen la recogida de materiales o la aprobación de un diseño.
- Lo que cambia entre mercados es **idioma, moneda, formato de fecha y zona horaria**.

**Los dos matices que rebajan la nota:**

1. **Si el producto toca cobro o facturación, la portabilidad cae a Media.** Ahí sí hay regulación local: la Directiva 2011/7/UE y la Ley 3/2004 española (30 días por defecto, **máximo 60 sin excepción**, interés = BCE + 8 pp, €40 mínimo de compensación), el régimen británico de *Reporting on Payment Practices*, y la *Freelance Isn't Free Act* del estado de Nueva York (en vigor desde el 28 ago 2024: contrato escrito obligatorio ≥$800, pago en 30 días a falta de pacto, **conservación de registros 6 años y presunción a favor del freelance si el contratante no puede producir el contrato**). El cobro automatizado de Anchor, por ejemplo, depende de ACH y tiene sesgo EE.UU. explícito.
2. **El canal de mensajería difiere culturalmente.** WhatsApp es el canal de facto en España y Latinoamérica; email y SMS lo son en EE.UU. Cualquier producto que dependa de un canal concreto hereda esa fragmentación (y sus costes — ver §12).

**Nota regulatoria con relevancia estratégica:** el **Real Decreto 238/2026** (BOE, 31 mar 2026, en vigor 20 abr 2026) desarrolla la facturación electrónica obligatoria B2B en España y obliga a comunicar, en un máximo de 4 días naturales, la aceptación o rechazo comercial con su fecha y **"el pago efectivo completo de la factura y su fecha efectiva de pago"**. Es decir, España está creando por ley un registro estructurado y auditable de fecha de vencimiento contra fecha real de pago para todas las empresas y autónomos. *(Hay discrepancia entre el cómputo del BOE —12 meses para facturación >€8M, 24 para el resto— y fechas de 2027/2028 citadas por proveedores; confirmar contra la disposición final cuarta antes de usar fechas concretas.)* Y la propuesta de Reglamento europeo de morosidad **no está retirada**: está en *"Awaiting Council's 1st reading position"* tras la minoría de bloqueo liderada por Alemania y Austria en junio de 2024.

---

## 12. External dependencies

### 12.1 ESTRUCTURAL — Entregabilidad de email

Es la dependencia crítica y no negociable, porque la propuesta de valor **es** recordar algo a gente que no quiere ser recordada, por un canal que no se controla.

Requisitos verificados en [las directrices oficiales de Gmail](https://support.google.com/mail/answer/81126?hl=en) (vigentes desde el 1 feb 2024, sin cambios documentados para 2025-2026): SPF o DKIM para todos; **SPF y DKIM, DMARC con política aplicada, alineación del dominio From: y desuscripción en un clic** para remitentes de 5.000+ mensajes/día; **spam rate objetivo <0,10% y límite duro 0,30%**. Microsoft añadió requisitos propios para remitentes de alto volumen a Outlook en mayo de 2025 (*existencia confirmada; el cuerpo del anuncio no pudo extraerse*).

Por qué es estructural aquí y no cosmético:

1. **El recordatorio tiene que parecer del freelancer**, lo que obliga a alineación SPF/DKIM sobre su dominio → onboarding con registros DNS → fricción alta para alguien que no sabe qué es un registro TXT. La alternativa mata la credibilidad del recordatorio.
2. **Insistir a quien ignora es, por definición, un generador de quejas de spam.** La métrica de producto (insistir más) choca frontalmente con la métrica de supervivencia (spam rate <0,10%).
3. **IPs compartidas**: con miles de usuarios pequeños nadie tiene volumen para IP dedicada; la reputación es colectiva.
4. **Evidencia de mercado:** Content Snare incluye **cuota de SMS en todos sus planes** (40/100/200/400 SMS/mes). **[I]** Eso no es una feature bonita: es el incumbente pagando por un canal alternativo porque el email solo no basta.

### 12.2 ESTRUCTURAL (si se usa) — WhatsApp Business API

Verificado en la [documentación oficial de Meta](https://developers.facebook.com/docs/whatsapp/pricing/): desde el 1 jul 2025 el precio es **por mensaje**, no por conversación, con categorías Marketing / Utility / Authentication y tiers mensuales. Cambios de tarifas 1-oct-2025, MXN en ene-2026, ocho divisas nuevas en abr-2026.

**Cambio inminente:** según [Courier](https://www.courier.com/blog/whatsapp-pricing-changes-october-2026) (**fuente secundaria, confirmar contra el changelog de Meta**), el **1 de octubre de 2026** dejan de ser gratis los mensajes de servicio dentro de la ventana de 24 h y las plantillas Utility dentro de esa ventana. Su ejemplo brasileño estima +14% de factura.

**[I]** Un producto cuya propuesta sea "perseguimos a tu cliente por WhatsApp" tiene un coste marginal por unidad de valor entregado, denominado en una moneda que Meta cambia unilateralmente cada ~12 meses, con un ACV de $20-70/mes. Eso es margen bruto erosionándose sin capacidad de reacción. Meta controla además la aprobación y categorización de plantillas.

### 12.3 ESTRUCTURAL (si es parte del núcleo) — Google Drive

Los scopes de Drive son **restricted scopes**: verificación obligatoria, **evaluación de seguridad CASA** si los datos pasan por servidores propios, verificación completa que *"puede tardar varias semanas"*, y **re-verificación anual obligatoria** ([Google](https://developers.google.com/identity/protocols/oauth2/production-readiness/restricted-scope-verification)). Coste de CASA no publicado y no verificado. "Conectar con Drive" no es un sprint: es un compromiso de compliance recurrente con riesgo de desconexión.

### 12.4 Conveniente, no estructural

- **Stripe**: sustituible; solo se vuelve estructural si el producto intermedia pagos (marketplace/Connect), lo que añade KYC y riesgo de fraude.
- **Slack**: conveniente y, además, **mal encajado con el ICP** — el problema no es que el freelancer no vea las tareas, es que el cliente PYME no vive en Slack.
- **APIs de CMS** (WordPress/Webflow/Shopify): coste de mantenimiento permanente; multiplicar CMS multiplica superficie de rotura sin multiplicar WTP.
- **Almacenamiento de archivos**: no es dependencia de plataforma, pero sí de unit economics. Content Snare raciona explícitamente el storage (20/50/100/200+ GB) y limita *active requests* en lugar de clientes. **[I]** Ese diseño no es casual: es la única forma de que el coste de almacenar vídeos y PSDs no se coma un plan de $35/mes.

---

## 13. Incumbent risk

### 13.1 Movimientos reales verificados (2024-2026)

| Incumbente | Movimiento | Riesgo |
|---|---|---|
| **HoneyBook** | [Actualizaciones feb-2026](https://www.honeybook.com/blog/product-updates-february-2026): vista Kanban, **saltar pasos individuales dentro de una automatización**, recordatorios automáticos, adjuntar archivos a emails de proyecto. Además [HoneyBook MCP como conector de Claude](https://www.globenewswire.com/news-release/2026/08/19/3347702/0/en/honeybook-mcp-debuts-as-a-claude-connector-for-client-pipelines-invoices-and-contracts.html) (19 ago 2026). Ya tienen portal de cliente, contrato y pago. | **ALTO** |
| **Dubsado** | [Dubsado 3.0](https://www.dubsado.com/three-point-o): reconstrucción completa con **Flows** (automatizaciones por nodos), Messages, portales y formularios, AI Email Intelligence. 2.0 se apaga en 2026. | **ALTO** |
| **Notion** | [Notion Forms](https://www.notion.com/help/forms): compartibles **con cualquiera por enlace, sin cuenta Notion**, con **automatizaciones al recibir respuesta**, en **todos los planes incluido el gratuito**. Más Custom Agents (feb 2026), Developer Platform (may 2026), External Agents (jul 2026). | **ALTO y subestimado.** Un formulario público + automatización + agente de seguimiento es buena parte del producto, gratis, dentro de la herramienta donde el freelancer ya lleva el proyecto. |
| **Bonsai** | Client Portal + CRM en producto; renombrado "Clients" → "Companies" (movimiento hacia equipos). | ALTO |
| **ClickUp** | Super Agents (ene 2026), Brain² (jun 2026); los agentes pueden crear, resumir, actualizar o completar recordatorios. Sin portal de cliente ni aprobaciones en entradas recientes. | MEDIO-ALTO (vía agentes genéricos) |
| **Google Workspace** | [9 sep 2026](https://workspaceupdates.googleblog.com/2026/09/create-content-schedule-events-and-coordinate-tasks-across-Workspace-regardless-of-what-app-you-are-in.html): Gemini transversal — redactar emails desde notas, registrar recordatorios en Tasks, tarjeta de confirmación previa. | MEDIO. No construirá un portal para freelancers, pero erosiona "escribir el email de seguimiento". |
| **Canva** | [Design approval](https://www.canva.com/help/design-approval-for-enterprise/) ya es producto, pero para organizaciones/Enterprise. | MEDIO |
| **Webflow** | [Client payments enhancements](https://webflow.com/updates/client-payments-enhancements) (28 ago 2025): traspaso de facturación y de sitios al workspace del cliente. Se están comiendo la relación de facturación agencia↔cliente. | MEDIO |
| **Figma** | [Approvals en Figma Buzz](https://help.figma.com/hc/en-us/articles/39288847137815-Use-approvals-in-Figma-Buzz) (Beta), pero **"Reviewers must already have access to the file"** → los externos sin Figma no pueden aprobar. Solo Organization/Enterprise. | **BAJO** para este caso de uso — y es el hueco real |
| **Adobe / Frame.io** | No se verificaron changelogs en fuente primaria. Frame.io es literalmente review & approval con externos, en vídeo. | Desconocido |
| **Slack, Stripe, Intuit, monday, Asana, Squarespace** | No verificados en esta área. | Desconocido — no asumir que no hay movimientos |

### 13.2 ¿Qué ventaja tendría un producto independiente?

**[I]** Las ventajas defendibles serían: (a) que el cliente final no necesite cuenta en nada, que es justo donde Figma se ha quedado corta y donde los portales fallan; (b) foco en el caso concreto frente a suites que lo tratan como una feature más; (c) precio y simplicidad frente a los $199/mes de Filestage y Ziflow.

**Las desventajas son mayores:** HoneyBook, Dubsado y Bonsai **ya poseen la relación completa** (portal + contrato + factura + pago) y solo tendrían que añadir una automatización más a un motor que ya existe. Notion ya tiene el formulario público, gratis, con automatizaciones y agentes. Un producto independiente entraría como la quinta suscripción de alguien que ya se queja de *"needing another damn bill to pay"*.

---

## 14. Evidence against the opportunity

Esta es la sección con la evidencia más fuerte de toda la investigación. Ordenada por peso.

**1. El líder de categoría salió del segmento.** Content Snare, tras ~10 años y sin financiación externa, se estima en ~$990K ARR, y su propia página de casos de uso pone hoy **Accounting & Bookkeeping, Legal y Mortgage & Finance por delante de Digital Agencies**, reconociendo que el producto nació para recoger contenido web. Es la *revealed preference* de la única empresa del espacio con datos reales: freelancers y agencias pequeñas no pagan lo suficiente; los sectores con recogida documental obligatoria sí. **Entrar por ahí es entrar por la puerta por la que el incumbente salió.**

**2. Los referentes históricos fueron absorbidos o pivotaron.** GatherContent → Bynder (2022). ProjectHuddle → SureFeedback, módulo de suite (2023). Atarim → "AI Agency for WordPress", con 1.000+ instalaciones. Optimi no existe (dominio a la venta). WeTransfer Portals cerró. **La categoría no ha producido ningún negocio independiente grande en una década.**

**3. El precio ancla está roto.** Todo el espacio adyacente se vende en AppSumo a $59 de por vida, incluida una empresa fundada en julio de 2025. Un mercado con buena retención no hace eso.

**4. El daño económico se neutraliza gratis, por contrato.** Kevin Geary: *"it no longer affects us negatively"* — con cláusulas, no con software. Paige Brunton declara un registro casi perfecto de cobros y de entrega de contenido usando Google Drive. Caroline Gibson reserva solo el 10% para la factura final. **[I]** Si el dolor monetario se elimina con tres párrafos en un contrato, la disposición a pagar mensualmente por software cae mucho.

**5. La barrera no es recolectar, es la adopción del cliente.** Patrón 1 de la sección 8: 12 productos, ~22 fuentes. Cualquier solución que exija al cliente entrar a un sitio nuevo hereda exactamente el problema que pretende resolver. El caso del portal de $12.000 con 30% de entrada recurrente lo ilustra.

**6. Se quejan pero no compran.** Análisis publicado de hilos de comunidades de agencias concluye que la conversación está en fase de normalización y desahogo, no de búsqueda de solución: los hilos terminan en *"is this just me?"*, no en "¿qué herramienta uso?" ([dev.to](https://dev.to/lisasakura/why-agency-owners-complain-about-onboarding-but-never-fix-it-3m5m), 14 may 2026). Caso concreto: un fundador construyó una herramienta de IA para briefs de agencia, dedicó 40 días a SEO y comunidad, y obtuvo 1.050 impresiones, 6 clics y **cero clientes de pago fuera de su red** ([Indie Hackers](https://www.indiehackers.com/post/i-built-an-ai-tool-for-agencies-spent-40-days-on-seo-and-community-and-still-have-zero-paying-strangers-heres-what-i-m-seeing-c9d36140dd), jun 2026). Comentario en ese hilo: *"Agencies do not buy tools, they buy margin or billable hours."*

**7. Las agencias no reportan el problema como fallo de entrega.** HubSpot Agency Growth Report: **85% declara que el trabajo de cliente se entrega a tiempo de forma consistente**. Si el retraso fuera sistémico y grave, ese número debería ser mucho más bajo.

**8. No hay canal de adquisición barato.** r/freelance, r/Entrepreneur y r/marketing prohíben vendors. Agency Hackers excluye explícitamente a proveedores de agencias y los remite a partnerships de pago. El head de SEO lo posee Content Snare desde hace años. El long-tail donde hay hueco es de desahogo, no de compra.

**9. Dos dependencias estructurales con dueño ajeno**, una de ellas con la métrica de producto en conflicto directo con la métrica de supervivencia (§12.1), y otra subiendo precios el 1 de octubre de 2026 (§12.2). **Esto colisiona frontalmente con la restricción explícita de no depender estructuralmente de terceros.**

**10. Split comprador/usuario en el segmento con dinero.** En agencias de 10+, quien sufre (PM) no compra y quien compra (socio) no sufre. En freelance solo no hay split, pero tampoco hay presupuesto.

**11. Valor condicionado a la cooperación de un no-comprador.** El producto solo funciona si el cliente final —que no paga, no eligió y ya está demostrando que no coopera— entra y participa.

**12. El fenómeno lleva 16 años documentado sin cambiar.** Los hilos de SitePoint de 2010 y el post de Rubber Duckers de julio de 2026 describen exactamente lo mismo, con exactamente los mismos workarounds. **No se ha encontrado ninguna evidencia de que algo haya cambiado en 2026 que haga que este segmento empiece a pagar más de lo que pagaba.**

---

## 15. Unknowns

Preguntas importantes que la investigación online no ha podido responder:

1. **¿Cuántos días al año está realmente bloqueado un proyecto esperando input del cliente?** No existe ninguna medición independiente. Es el hueco central.
2. **¿Qué porcentaje de freelancers y agencias ha resuelto ya el problema por contrato** (depósito + dormancy + restart fee) y por tanto no tiene dolor monetario residual?
3. **¿Existe algún post-mortem de abandono?** Se encontraron rechazos *previos a la compra* (precio, complejidad) y un churn por caída de servicio, pero **ningún caso documentado de alguien que diga "usé Content Snare/Filestage seis meses y volví al email"**. Ese sería el dato más valioso que falta.
4. **¿Cuál es la tasa real de adopción del cliente final** en Content Snare, Filestage o un portal cualquiera? Ningún vendor la publica.
5. **¿Cuánto factura realmente el líder?** Todas las cifras son estimaciones de GetLatka; no hay confirmación del fundador pese a ser figura pública en el ecosistema bootstrapped.
6. **Reddit entero.** Hilos identificados por título y no verificados: r/agency *"4hrs in client onboarding setup - every stupid damn time"* (38 upvotes, 71 comentarios), r/startups *"onboarding clients is actual hell"*.
7. **Vídeo y fotografía**: sin evidencia sólida. Habría que ir a grupos cerrados de Facebook de videógrafos, Creative COW o REDUSER.
8. **Número de agencias pequeñas en EE.UU.** (Census CBP/SUSB, requiere clave de API) y de freelancers en Reino Unido (ONS).
9. **Coste real de la evaluación CASA** de Google y confirmación en fuente primaria del cambio de precios de WhatsApp del 1-oct-2026.
10. **Movimientos de Adobe/Frame.io, Slack, Intuit, monday, Asana y Squarespace** en recogida y aprobaciones 2024-2026.
11. **Calendario exacto del RD 238/2026** (discrepancia entre BOE y proveedores) y estado de leyes tipo *Freelance Isn't Free* fuera de Nueva York.

---

## 16. Hypotheses to validate in interviews

Formuladas para poder ser falsadas hablando con usuarios. Las tres primeras son las que, si fallan, matan la oportunidad.

1. **Una agencia de 2-20 personas tiene, en un mes normal, al menos 3 proyectos simultáneamente bloqueados esperando input del cliente durante más de 5 días hábiles.**
   *(Si la respuesta mediana es 0 o 1, el problema no tiene la frecuencia necesaria.)*

2. **El bloqueo por input del cliente retrasa el cobro de un hito ya devengado en al menos el 30% de los proyectos.**
   *(Es el vínculo que la evidencia online no consigue probar. Si el entrevistado factura por calendario y no por hitos dependientes del cliente, el vínculo no existe para él.)*

3. **Quien ya tiene cláusula de dormancy o restart fee en su contrato declara no tener dolor monetario residual por este problema.**
   *(Si se confirma, el mercado con disposición a pagar se reduce a quien aún no ha profesionalizado su contrato — un segmento que, por definición, tampoco paga software.)*

4. **El cliente final ha rechazado, ignorado o abandonado al menos una herramienta que el freelancer intentó imponerle en los últimos 12 meses, volviendo a email o WhatsApp.**

5. **El dueño de una agencia de 2-20 personas decide la compra de una herramienta de <$50/mes sin aprobación de terceros y en menos de una semana.**
   *(Contrasta con el split comprador/usuario documentado. Si el PM que sufre tiene que pedir permiso, el ciclo de venta mata el modelo indie.)*

6. **El freelancer conoce su propia cifra: sabe cuántos días estuvo parado el último proyecto y cuánto le costó.**
   *(Si no la sabe ni la ha calculado nunca, el ROI no es demostrable y la venta se apoya solo en frustración.)*

7. **Email + recordatorio manual no es suficientemente bueno**, y la razón que da el entrevistado es concreta y repetible, no genérica ("se me olvida" no basta: ¿cuántas veces, con qué consecuencia?).

8. **El entrevistado ha pagado alguna vez por una herramienta de este espacio y sigue pagándola hoy.**
   *(Distinguir entre "la probé", "la compré en AppSumo" y "la renuevo".)*

9. **Los profesionales de sectores con recogida documental obligatoria (contabilidad, legal, hipotecas, seguros) describen el mismo problema con mayor intensidad económica y mayor obligación de cooperación por parte del cliente.**
   *(Hipótesis de reubicación del ICP, sugerida por el movimiento del incumbente. Merece ser probada en las mismas entrevistas.)*

10. **Existe un momento del año o del ciclo en el que el dolor se concentra** (cierre fiscal, renovaciones, campaña de temporada) que actúe como trigger de compra y no solo de queja.

---

## 17. Sources

### Evidencia del problema (comunidades, foros y practicantes)

| Fuente | URL | Fecha | Qué respalda |
|---|---|---|---|
| Launch The Damn Thing — sistema de recogida de contenido | https://launchthedamnthing.com/blog/website-content-collection-system-clients-actually-love | 25 jun 2025 | E1: horas perdidas autorreportadas; Content Snare descartada por precio |
| Launch The Damn Thing — review de 22 portales de cliente | https://launchthedamnthing.com/blog/web-designer-client-portals-options | feb 2025 | Saturación de la categoría; criterio decisor = precio + adopción |
| The CX Toolbox — condiciones de pago en diseño web | https://thecxtoolbox.com/client-experience/website-design-payment-terms/ | 9 feb 2026 | E2: £3.000 bloqueados 2 meses; cláusula de dormancy y restart fee |
| Geary.co — cómo gestionar proyectos retrasados | https://geary.co/how-to-handle-delayed-web-design-projects/ | 18 feb 2023 | E3: política 5/45/90 días; el problema neutralizado sin software |
| SitePoint — "When clients delay the project" | https://www.sitepoint.com/community/t/when-clients-delay-the-project/6388 | jul 2010 – feb 2011 | E4: >70% de clientes incumplen plazos; restart fees; "accept as part of the job" |
| SitePoint — "What to Do if the Client Won't Give Content" | https://www.sitepoint.com/community/t/what-to-do-if-the-client-wont-give-content/61011 | jun-jul 2010 | E5: workaround de contenido placeholder; auto-refutación del OP |
| Graphic Design Forums UK | https://www.graphicdesignforums.co.uk/threads/how-to-deal-with-clients-who-waste-your-time.10731/ | abr-jun 2014 | E6: seis meses esperando materiales; palanca de dominio/hosting |
| Adobe Community | https://community.adobe.com/questions-91/client-disappeared-for-five-and-a-half-years-wants-to-finish-the-project-now-1500144 | 11 mar 2025 | E7: cliente desaparecido 5,5 años; el depósito evitó la pérdida |
| Jennifer Bourn — clientes que desaparecen | https://jenniferbourn.com/managing-clients-who-disappear/ | 26 oct 2020 (act. 2023) | E8: dormancy clause, $500 reactivation, secuencia manual de 7 pasos |
| Caroline Gibson — retrasos en proyectos de copywriting | https://www.carolinegibson.co.uk/copywriting-project-delays/ | 10 abr 2019 | E9: cláusula de 21 días; separa retraso de impago |
| Web Designer Academy | https://webdesigneracademy.com/the-web-designers-guide-to-dealing-with-difficult-clients/ | 18 mar 2026 | E10: rehacer trabajo por entrega tardía |
| Rubber Duckers | https://rubberduckers.co.uk/why-web-design-projects-run-late/ | 3 jul 2026 | E11: "bleeding momentum"; cifras 10x y 20-30% **sin fuente** |
| Elegant Themes — comentarios de practicantes | https://www.elegantthemes.com/blog/tips-tricks/how-to-get-your-web-design-clients-to-send-you-content | 21 oct 2016 | Workarounds: lorem ipsum, hacer las fotos, GatherContent |
| Pressable — "I built the site but the client hasn't delivered content" | https://pressable.com/blog/i-built-the-site-but-the-client-hasnt-delivered-content-now-what/ | 15 mar 2019 (act. 2025) | Backlog + restart fee de $250; rankea #1 en su keyword |
| Happy Freelancing (Heidi Turner) | https://happyfreelancing.substack.com/p/client-ghosting-my-journey-through | 30 may 2024 | E13: impago post-entrega ≠ bloqueo pre-entrega |
| Medium — "Tools and process do not fix human problems" | https://evatorium.medium.com/tools-and-process-do-not-fix-human-problems-62a5d4c7b6ae | 22 jun 2020 | Evidencia contraria: marco de problema humano |
| dev.to — por qué las agencias se quejan del onboarding pero no lo arreglan | https://dev.to/lisasakura/why-agency-owners-complain-about-onboarding-but-never-fix-it-3m5m | 14 may 2026 | Evidencia contraria: desahogo ≠ búsqueda de solución; hilos de Reddit citados |
| Indie Hackers — ReqBrief, 40 días sin clientes de pago | https://www.indiehackers.com/post/i-built-an-ai-tool-for-agencies-spent-40-days-on-seo-and-community-and-still-have-zero-paying-strangers-heres-what-i-m-seeing-c9d36140dd | jun 2026 | Evidencia contraria: fallo real de GTM; split comprador/usuario |
| Digital Sage — por qué fallan los portales de cliente | https://digitalsage.agency/why-client-portals-systems-fail-businesses/ | 2 jul 2025 | Portal de $12.000 con 30% de uso recurrente (**contenido de agencia**) |

### Reviews y quejas

| Fuente | URL | Qué respalda |
|---|---|---|
| Capterra — Content Snare | https://www.capterra.com/p/167019/Content-Snare/reviews/ | Patrón 1 (adopción del cliente), recordatorios excesivos; 4,9/5 con 101 reviews |
| G2 — Content Snare | https://www.g2.com/products/content-snare/reviews | 4,7/5, 54 reviews; quejas de impersonalidad y de caída de servicio |
| Trustpilot — Content Snare | https://www.trustpilot.com/review/contentsnare.com | *"chasing clients for content"*; **solo 9 reseñas en total** |
| Software Advice — Plutio | https://www.softwareadvice.com/business-management/plutio-profile/reviews/ | La cita más directa de no-adopción del cliente |
| Capterra — ReviewStudio | https://www.capterra.com/p/146845/ReviewStudio/reviews/ | *"higher barrier to entry"* |
| G2 — BugHerd | https://www.g2.com/products/bugherd/reviews | Fricción de instalar extensión |
| G2 — Ahsuite | https://www.g2.com/products/ahsuite/reviews | Clientes que no entran; falta de alertas |
| G2 — Assembly (ex-Portal/Copilot) | https://www.g2.com/products/copilotplatforms/reviews | No mobile-friendly; precio por usuario |
| G2 — Filestage | https://www.g2.com/products/filestage/reviews | Subida de precio del 76%; formación necesaria |
| Capterra — Markup.io | https://www.capterra.com/p/206850/Markup/reviews/ | Subida del 280%; comentarios perdidos |
| Trustpilot — HoneyBook | https://www.trustpilot.com/review/honeybook.com | *"went from $200 to over $600"*; features retiradas |
| Trustpilot — Jotform | https://www.trustpilot.com/review/jotform.com | Renovación al triple sin aviso; cuenta suspendida |
| Trustpilot — Plutio | https://www.trustpilot.com/review/plutio.com | Producto abandonado (5 fuentes independientes) |
| Trustpilot — Frame.io | https://www.trustpilot.com/review/frame.io | Imposibilidad de cancelar; soporte tras la adquisición |
| Capterra — SuiteDash | https://www.capterra.com/p/154949/SuiteDash/reviews/ | Curva de aprendizaje; componentes retirados |

### Mercado, precios y tracción

| Fuente | URL | Qué respalda |
|---|---|---|
| Content Snare — pricing | https://contentsnare.com/pricing/ | $35-$215+/mes; sin plan gratis; cuota de SMS en todos los planes |
| **Content Snare — casos de uso** | https://contentsnare.com/uses/ | **Digital Agencies en 4ª posición, tras contabilidad, legal e hipotecas** (verificado 20-sep-2026) |
| Content Snare — encuesta a clientes | https://contentsnare.com/results-survey/ | Única cuantificación del problema; **vendor, muestra autoseleccionada** |
| GetLatka — Content Snare | https://getlatka.com/companies/contentsnare.com | ~$990K ARR, 9 empleados (**estimación de tercero**) |
| Starter Story — Content Snare | https://www.starterstory.com/content-snare-breakdown | *"stuck at $300k ARR"* antes del pivot a contables |
| Filestage / Ziflow / BugHerd / Pastel / Markup.io / Frame.io / ReviewStudio / GoVisually — pricing | filestage.io/pricing · ziflow.com/pricing · bugherd.com/pricing · usepastel.com/plans · markup.io/pricing · frame.io/pricing · reviewstudio.com/pricing · govisually.com/pricing | Precios verificados; hueco de $0 a $199 |
| HoneyBook / Dubsado / Bonsai / Moxie / Plutio — pricing | honeybook.com/pricing · dubsado.com/pricing · hellobonsai.com/pricing · withmoxie.com/pricing · plutio.com/pricing | Precios del segmento CRM de cliente |
| Ahsuite / Kitchen.co / SuiteDash / Clinked / Wayfront / ManyRequests / Assembly — pricing | ahsuite.com/subscribe · kitchen.co/pricing · suitedash.com/pricing · clinked.com/pricing · wayfront.com/pricing · manyrequests.com/pricing · assembly.com/pricing | Precios de portales; rebrands en curso |
| Stripe Invoicing / Anchor / FreshBooks — pricing | stripe.com/invoicing/pricing · sayanchor.com/pricing · freshbooks.com/pricing | Suelo de precio; modelo de $5 por cobro |
| WeTransfer — cierre de Portals | https://wetransfer.com/help-center/troubleshooting/reviews-portals-sunset | Cierre definitivo el 22 dic 2025 |
| AppSumo — búsqueda "client portal" | https://appsumo.com/search/?query=client%20portal | Lifetime deals a $59; precio ancla roto |
| Bynder adquiere GatherContent | https://www.bynder.com/en/press-media/bynder-acquires-content-operations-platform-gathercontent/ | 3 mar 2022; absorción del referente histórico |
| ProjectHuddle → SureFeedback | https://surefeedback.com/projecthuddle-now-surefeedback/ | 7 nov 2023; absorción en suite |
| Atarim en wordpress.org | https://wordpress.org/plugins/atarim-visual-collaboration/ | 1.000+ instalaciones; pivot a "AI Agency" |

### Datos económicos y de mercado

| Fuente | URL | Fecha | Qué respalda |
|---|---|---|---|
| DBT / OSBC — *Late Payments Research* (London Economics) | https://assets.publishing.service.gov.uk/media/688a089a6478525675738ff9/late_payments_research_impact_on_uk_economy.pdf | 2025 | £11.000M/año, 14.000 cierres, 86 h/año persiguiendo cobros |
| CEPYME — Observatorio de la Morosidad | https://cepyme.es/category/morosidad/ | 2º sem. 2025 | PMP 80,5 días; 30,4% cobrado puntualmente; €611M microempresas |
| Xero Small Business Insights | https://blog.xero.com/data-insights/small-business-insights-data-late-payment-results/ | 3 mar 2026 | Retraso real 7,8-9,7 días (dato transaccional) |
| Intuit QuickBooks — Late Payments Report 2026 | https://quickbooks.intuit.com/r/small-business-data/small-business-late-payments-report-2026/ | 2026 | 59% de pymes con facturas >30 días; $17.700 medios |
| Intrum — European Payment Report 2026 | https://www.intrum.com/insights/publications/epr-2026/ | 2026 | 12% de ingresos cobrados tarde (**empresa de recobro**) |
| Atradius — Payment Practices Barometer | https://group.atradius.com/knowledge-and-research/reports/b2b-payment-practices-trends-western-europe-2025 | 2025 | 47% de facturas B2B vencidas (**aseguradora de crédito**) |
| Freelancers Union — *The Costs of Nonpayment* | https://www.onlabor.org/wp-content/uploads/2017/05/FU_NonpaymentReport_r3.pdf | 2015 | $5.968 impagados de media (13% de ingresos); **dato antiguo** |
| HubSpot — Marketing Agency Growth Report | https://cdn2.hubspot.net/hubfs/53/Agency%20Research%20Report%202018/2018%20Agency%20Growth%20Report%20(final).pdf | 2018 | **85% declara entregar a tiempo** — evidencia contraria |
| Promethean Research — State of Digital Services 2026 | https://prometheanresearch.com/2026-state-of-digital-services-digital-agency-industry-research/ | feb 2026 | Tamaño y márgenes de agencia; **sin datos de retrasos** |
| Eurostat — `lfsa_esgan` | https://ec.europa.eu/eurostat/databrowser/view/lfsa_esgan/default/table?lang=en | 2025 | 17,68M autónomos sin asalariados en UE-27 |
| Eurostat — `sbs_sc_ovw` | https://ec.europa.eu/eurostat/databrowser/ | 2023 | ~95.400 empresas de 2-19 personas en M73.1 + M74.1 |
| Upwork Research Institute | https://investors.upwork.com/news-releases/news-release-details/upwork-study-finds-1-4-us-skilled-knowledge-workers-now-work | 2025 | 28% de knowledge workers independientes en EE.UU. |

### Distribución, dependencias y regulación

| Fuente | URL | Qué respalda |
|---|---|---|
| The Hive Index — Reddit y comunidades | https://thehiveindex.com/platforms/reddit/ | Tamaños de subreddits y comunidades (**tercero**) |
| OneUp — estudio de reglas de autopromoción | https://oneup.today/blogs/reddit-selfpromo-rules-study-2026 | 61% de subreddits prohíben o restringen vendors (**tercero, 13 jul 2026**) |
| Agency Hackers — membresía | https://www.agencyhackers.com/membership/ | £250-450/mes; excluye proveedores de agencias |
| Gmail — directrices para remitentes | https://support.google.com/mail/answer/81126?hl=en | SPF/DKIM/DMARC; spam rate <0,10% objetivo, 0,30% límite |
| Microsoft — remitentes de alto volumen | https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/strengthening-email-ecosystem-outlook%e2%80%99s-new-requirements-for-high%e2%80%90volume-senders/4399730 | Existencia confirmada (may 2025); **cuerpo no extraído** |
| Meta — pricing de WhatsApp Business | https://developers.facebook.com/docs/whatsapp/pricing/ | Precio por mensaje desde jul 2025; cambios de tarifas |
| Courier — cambios de WhatsApp de octubre 2026 | https://www.courier.com/blog/whatsapp-pricing-changes-october-2026 | Fin de la ventana gratuita el 1 oct 2026 (**fuente secundaria**) |
| Google — verificación de restricted scopes | https://developers.google.com/identity/protocols/oauth2/production-readiness/restricted-scope-verification | CASA obligatorio y re-verificación anual para Drive |
| HoneyBook — actualizaciones feb 2026 | https://www.honeybook.com/blog/product-updates-february-2026 | Automatizaciones granulares; riesgo de incumbente |
| HoneyBook MCP como conector | https://www.globenewswire.com/news-release/2026/08/19/3347702/0/en/honeybook-mcp-debuts-as-a-claude-connector-for-client-pipelines-invoices-and-contracts.html | 19 ago 2026 |
| Dubsado 3.0 | https://www.dubsado.com/three-point-o | Flows, portales, AI Email Intelligence |
| Notion Forms | https://www.notion.com/help/forms | Formularios públicos sin cuenta + automatizaciones, en plan gratuito |
| Figma Buzz — approvals | https://help.figma.com/hc/en-us/articles/39288847137815-Use-approvals-in-Figma-Buzz | *"Reviewers must already have access to the file"* → hueco de externos |
| Canva — design approval | https://www.canva.com/help/design-approval-for-enterprise/ | Aprobaciones solo en Enterprise |
| Webflow — client payments | https://webflow.com/updates/client-payments-enhancements | 28 ago 2025; incumbente ocupando la relación de facturación |
| Google Workspace — actualización de Gemini | https://workspaceupdates.googleblog.com/2026/09/create-content-schedule-events-and-coordinate-tasks-across-Workspace-regardless-of-what-app-you-are-in.html | 9 sep 2026; erosión del email de seguimiento |
| Parlamento Europeo — procedimiento 2023/0323(COD) | https://oeil.europarl.europa.eu/oeil/en/procedure-file?reference=2023%2F0323%28COD%29 | Reglamento de morosidad **no retirado**, bloqueado en Consejo |
| BOE — Ley 3/2004 | https://www.boe.es/buscar/act.php?id=BOE-A-2004-21830 | Máximo 60 días; interés BCE + 8 pp; €40 |
| BOE — Real Decreto 238/2026 | https://www.boe.es/buscar/act.php?id=BOE-A-2026-7295 | Obligación de comunicar la fecha efectiva de pago en 4 días |
| UK Gov — respuesta a la consulta sobre morosidad | https://assets.publishing.service.gov.uk/media/69c2c7c413f1436476e443a2/late-payments-consultation-response.pdf | mar 2026; tope de 60 días, interés obligatorio, poderes sancionadores |
| Epstein Becker Green — NY Freelance Isn't Free Act | https://www.ebglaw.com/workforce-bulletin/freelance-isnt-free-act-soon-takes-effect-throughout-new-york-state | Contrato escrito ≥$800; 6 años de conservación; presunción a favor del freelance |

---

*Documento generado el 20 de septiembre de 2026. Todas las páginas de pricing fueron consultadas ese día. Las cifras marcadas como estimación de tercero (GetLatka, Crunchbase, The Hive Index) no están auditadas. Donde no se pudo verificar, el documento lo dice explícitamente en lugar de rellenar el hueco.*

**Investigado por:** Claude