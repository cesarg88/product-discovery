# Documentación del estado de la vivienda en check-in / check-out

> **Investigación de mercado — fase de discovery. 20 de septiembre de 2026.**
>
> Convención de etiquetado usada en todo el documento:
> - **[HECHO]** — dato de fuente primaria oficial (regulador, organismo estadístico, ley, informe auditado) o contenido verbatim verificado en la fuente.
> - **[FUENTE]** — afirmación de una persona o entidad concreta (post de foro, review, vendor, asociación gremial). Es real que lo dijeron; no está verificado de forma independiente.
> - **[INFERENCIA]** — cálculo o lectura propia a partir de datos etiquetados. Se muestra la aritmética.
> - **[HIPÓTESIS]** — no validado. Va a la sección 16.
> - **[SIN EVIDENCIA]** — se buscó y no se encontró dato publicable.
>
> **Limitación metodológica grave y declarada por adelantado:** Reddit resultó **completamente inaccesible** desde este entorno (`SITE_BLOCKED` en fetch, 403 del proxy en curl y en el navegador integrado; las búsquedas `site:reddit.com` devuelven ruido SEO). Ninguna evidencia de r/Landlord, r/HousingUK, r/PropertyManagement ni r/AusPropertyChat entra en este dossier. Es la mayor laguna del trabajo y está recogida en la sección 15. Tampoco fueron accesibles Quora, Whirlpool (AU), Forocoches, ni los hilos individuales del foro de LandlordZONE (404: el foro antiguo parece retirado). G2 no renderiza reviews individuales vía fetch. Todo lo que sigue procede de páginas efectivamente abiertas y leídas.

---

## 1. Executive summary

La evidencia confirma que el problema **existe, es antiguo y está bien documentado**: hay casos reales con dinero concreto (£820, £850, £1.000, £1.700, €475, $2.200) y sentencias que se deciden exactamente por la ausencia de inventario fotográfico. Pero la evidencia también dice, con la misma fuerza, que **el mercado ya está construido**: hay ≥8 proveedores dedicados solo en Reino Unido, ≥6 en Francia, el precio del software está anclado entre **£0,10 y £3,75 por informe**, y las dos mayores plataformas de landlords de EE. UU. (TurboTenant, 1M+ landlords; Zillow) **regalan la funcionalidad**. Los tres canales institucionales británicos (TDS, NRLA, mydeposits) ya tienen proveedor asignado, y uno de ellos tiene integración nativa en el portal de evidencias del adjudicador. El dolor agudo es **infrecuente por usuario**: solo el **1,00%** de las fianzas británicas llega a adjudicación formal, y el 45% de los landlords ingleses y el 93,4% de los propietarios españoles tienen una sola propiedad — un evento cada ~5 años. El contrapeso honesto: el **37%** de los arrendadores ingleses deduce algo de la fianza (37× la tasa de disputa formal), el **56%** de los inquilinos estadounidenses no recupera todo, y existen mercados con **mandato legal explícito** (Francia, Australia, 11 estados de EE. UU.) donde el trigger no depende de la disciplina del usuario. Las quejas que sí existen sobre los productos actuales son **de ejecución, no de concepto** (crashes, pérdida de fotos, sync), lo que describe deuda técnica de incumbentes, no un hueco de mercado. Los dos huecos que la evidencia sí señala son la **integridad probatoria y la custodia duradera del informe**, y el **lado del inquilino**, que hoy queda sin copia y sin poder.

---

## 2. Problem evidence

Catorce evidencias independientes verificadas. Todas las URLs fueron abiertas y leídas. Las citas están en su idioma original.

### E1 — Inquilino UK: no existe check-in report firmado; £820 retenidos de £950
- **Quién:** `Jamesingram1`, inquilino (Inglaterra).
- **Problema:** ni la agencia ni el inquilino tienen copia firmada del check-in report. El check-out sí existe, con fotos macro sin contexto espacial.
- **Consecuencia:** £820 retenidos de £950; £260 solo por "limpieza"; sin facturas aportadas.
- **Workaround:** fotos con el móvil en las primeras semanas + copias de cartas.
- **Cita [FUENTE]:** *"I have since found out, that the agent does not have a signed copy of the check-in report. I also don't have a check-in report."* / *"The checkout report has suspicious entries…stuff taken so close up you can't see where it is."*
- **Contrapunto en el mismo hilo** (`canaldumidi`): *"A check in report is not compulsory. It simply forms PART of the evidence…Yes, without it, it is harder for the LL to argue his case, but not impossible."*
- **Fuente:** MoneySavingExpert, 18 dic 2021 — https://forums.moneysavingexpert.com/discussion/6320840/landlord-withholding-deposit-inventory-not-signed

### E2 — Inquilina UK (Escocia): cero documentación por ambas partes; £850 en juego
- **Quién:** `sophsters`, inquilina, depósito en LPS.
- **Problema:** ni inventario ni fotos, ni al entrar ni al salir. El casero reclama la totalidad por moqueta, marcas y una encimera que ya estaba astillada.
- **Workaround:** ninguno. Es el caso puro de "no lo hice".
- **Cita [FUENTE]:** *"I'm worried they will ask for evidence but I didn't take photos on moving in or leaving which was stupid."*
- **Respuesta** (`greatcrested`): *"It's for the LL to justify the deduction, not you to justify the deposit return."*
- **Fuente:** MoneySavingExpert, 27 ene 2021 — https://forums.moneysavingexpert.com/discussion/6236107/rental-deposit-and-no-inventory

### E3 — El inventario existió y **se perdió** al cambiar de agencia (fallo de custodia, no de captura)
- **Quién:** inquilino UK tras 6+ años; la agencia original sí hizo inventario con fotos.
- **Problema:** el propietario cambió de agencia a mitad de contrato. *"He has contacted the first agent to ask for a copy but they say they no longer hold a copy."* / *"The second agent does not have one as they did not do another inventory when they took over."*
- **Consecuencia:** check-out con decenas de fotos de daños sin línea base con la que compararlas.
- **[INFERENCIA]** Modo de fallo distinto y poco señalado: el problema no es *no documentar*, sino **no tener un registro duradero, portátil e independiente de quién gestione la propiedad**.
- **Fuente:** MoneySavingExpert, 9 ene 2024 — https://forums.moneysavingexpert.com/discussion/6497386/reclaiming-deposit-with-change-of-agents-and-missing-inventory

### E4 — Inventario tan pobre que el check-out rellena los huecos
- **Quién:** `Davidlabomb`, inquilino UK.
- **Problema:** el inventario de entrada dice literalmente *"Fridge. White."*; el check-out describe como estado previo *"The fridge is clean throughout, the door functions well and the seal shows no sign of mold or wear."*
- **Cita [FUENTE]:** *"Almost comical! I have no clue where the estate agent / landlord is getting their 'previous state' comments from, and can only assume they are made up."*
- **Fuente:** MoneySavingExpert, 14 abr 2020 — https://forums.moneysavingexpert.com/discussion/6129206/check-out-report-does-not-match-inventory

### E5 — Septiembre de 2026: el estado del arte sigue siendo papel y bolígrafo
- **Quién:** `Monika17`, inquilina UK vía OpenRent.
- **Problema:** *"the inventory is a printed list with some comments written in pen"* y *"There was no photo."* La propietaria reclama **£1.000** por limpiar una mancha de moqueta; la prueba aportada es *"a photo of her handwritten comment that the carpet needs mild cleaning; there was no photo of the stain."*
- **[INFERENCIA]** Es la evidencia **más reciente** localizada (12–15 sept 2026) y demuestra que el problema no está resuelto en una parte real del mercado, aunque el software exista desde hace 15 años.
- **Fuente:** OpenRent Community, 12–15 sep 2026 — https://community.openrent.co.uk/t/openrent-made-it-difficult-to-dispute-landlords-claims-against-deposit/91494

### E6 — Propietario UK reclama vía TDS **sin inventario**: el foro le dice que no tiene caso
- **Quién:** `Zayk786`, **propietario**.
- **Workaround improvisado:** facturas de obras previas al contrato, fotos "antes y después", presupuestos, papeles de check-out que el inquilino se negó a firmar.
- **Respuesta [FUENTE]:** *"In the absence of knowing what condition things were in at the start there is very little basis on which to support your claims."*
- **Fuente:** MoneySavingExpert, 28 jun 2019 — https://forums.moneysavingexpert.com/discussion/6019116/missing-inventory-or-check-in-check-out-for-dispute-with-tds

### E7 — EE. UU.: propietaria pierde ~$2.200 por falta de move-in inspection
- **Quién:** `Petra Handrigan`, propietaria (BiggerPockets); cambio de property manager tras 7 años con el mismo inquilino.
- **Problema:** *"PM did not do a move-in inspection"*, *"do not have any documentation about move in condition"*.
- **Consecuencia:** $7.000 de reparaciones; ~$2.200 que cree imputables al inquilino; $1.200 de fianza inaplicables sin línea base.
- **Respuesta** (`Mike McCarthy`): *"7 years is a long time and a lot of standard wear and tear can happen."*
- **Fuente:** BiggerPockets, 28 ago 2019 — https://www.biggerpockets.com/forums/52/topics/747091-property-manager-did-not-keep-records-security-deposit-issues

### E8 — Australia (NSW): el ingoing report existía y fue **alterado**
- **Quién:** propietario NSW; responden un property manager de QLD y dos inversores.
- **Problema:** existía informe firmado, pero el inquilino presentó **una versión alterada** con fecha cambiada e ítems añadidos; *"all the alterations are not accompanied by any photo evidence or emails"*. El PM le advierte de que *"NCAT will rule in favour of the outgoing tenant"* porque el propietario no lo había firmado.
- **Cita reveladora del hueco de proceso** (`Propertunity`): *"As a LL in NSW I have never signed off on an ingoing report — the agent does this surely?"*
- **Fuente:** PropertyChat AU, 11 abr 2018 — https://www.propertychat.com.au/community/threads/ingoing-report-advice-needed-in-nsw.30712/

### E9 — Check-out ampliado a posteriori: >£1.000 añadidos después de que el casero entrara en la casa
- **Quién:** `NordicNoir`, inquilino UK.
- **Problema:** el check-out se hizo al día siguiente de la mudanza; **casi dos semanas después, tras haber estado el casero cuatro días dentro**, la agencia envió un inventario revisado con ítems extra. *"the lettings agent went back and added a whole host of extra issues, and sent a new inventory"* / *"We have no idea who has been in the house or what has happened to it in that time!"*
- **[INFERENCIA]** Aquí el fallo es la **ausencia de sellado temporal**: sin fecha inmutable, el informe es editable indefinidamente.
- **Fuente:** MoneySavingExpert, 9–15 ago 2022 — https://forums.moneysavingexpert.com/discussion/6377965/landlord-adding-items-after-checkout-inventory-completed

### E10 — El inventario profesional se pagó, pero nunca llegó al inquilino
- **Quién:** `Zoe28`, propietaria en OpenRent.
- **Problema:** descubre que *"the inventory report ordered via Openrent is not shared with the tenants and it's up to the landlord to do this"*. Pagó el informe y nunca lo envió, comprometiendo la deducción.
- **Fuente:** OpenRent Community, 13 feb – 16 may 2023 — https://community.openrent.co.uk/t/inventory-report-and-claiming-from-deposit/45099

### E11 — El inventario profesional pagado resulta inservible por compresión de imágenes
- **Quién:** varios propietarios y una property manager; responde staff de OpenRent.
- **Problema:** *"the format it displays in is very small pictures"*; el staff admite que *"sometimes send images compressed backed by originals"*.
- **Tensión clave sobre cadena de custodia** (`David122`): *"The issue is more how you prove to a deposit scheme/court that the photo you're now sending them is the one from the start"*.
- **Creencia de mercado, jurídicamente falsa pero operativa** (`Jessica27`, PM) **[FUENTE, disputada en el propio hilo]:** *"If you complete the inventory as the landlord yourself it will be null and void."*
- **Fuente:** OpenRent Community, 27 mar – 30 ago 2023 — https://community.openrent.co.uk/t/openrents-inventory-small-pictures-and-not-fit-for-purpose/46896

### E12 — Caso de adjudicación real (UK): el check-in vago hunde la reclamación
- **[HECHO]** Un adjudicador resolvió contra el propietario porque el check-in report de la agencia decía que los elementos estaban *"clean, bright and fresh unless otherwise stated"*, **sin detalle de decoración, sin indicar si algo era nuevo, sin confirmar limpieza profesional y sin ninguna fotografía**. El adjudicador *"could not be certain about the condition of the items claimed for at the start of the tenancy"*. El propietario tampoco aportó presupuestos ni facturas. El artículo no publica importes.
- **Fuente:** Property Industry Eye, 30 ene 2020 — https://propertyindustryeye.com/deposit-dispute-agents-vague-check-in-report-lacked-enough-evidence-to-help-landlord/

### E13 — España: sentencia de 2026 decidida exactamente por esto
- **[HECHO]** **SAP Barcelona (Sección 4ª) nº 39/2026, de 2 de febrero de 2026** (Roj: SAP B 375/2026; ECLI:ES:APB:2026:375). El propietario reclamaba rentas, suministros, desperfectos y desaparición de muebles. Sin inventario exhaustivo, sin reportaje fotográfico fechado y sin comunicación formal de las averías, *"la insuficiente identificación impidió demostrar la existencia de algunos bienes cuya desaparición se denunciaba"*. La Audiencia califica *"un inventario exhaustivo, firmado por ambas partes y complementado con reportaje fotográfico o videográfico"* como *"una de las pruebas más valiosas"*. El importe no consta en el comentario.
- **Segunda resolución en el mismo sentido:** SAP Barcelona de 10 de marzo de 2026, citada por Idealista (20 ago 2026).
- **Fuentes:** https://www.economistjurist.es/actualidad-juridica/jurisprudencia/sin-inventario-sin-fotografias-y-sin-avisar-de-los-desperfectos-la-audiencia-de-barcelona-recuerda-como-se-gana-o-se-pierde-un-pleito-entre-propietario-e-inquilino/ · https://www.idealista.com/news/inmobiliario/vivienda/2026/08/20/908816-las-pruebas-que-pueden-marcar-la-diferencia-al-reclamar-por-desperfectos-tras-el

### E14 — España: el patrón dominante no es la disputa probatoria, es que el dinero no vuelve
- **Quién:** múltiples inquilinos de habitaciones en Málaga, foro de idealista, 2024.
- **Casos [FUENTE]:** `Carmen Santana` (2 abr 2024): *"Me han robado 475€ de la fianza, después de rentar una habitación por 6 meses"*. `Sebitascyrus` (26 abr 2024): 10 meses sin devolución. `Valerivalsan` (25 may 2024) y `Andrea` (28 sep 2024): meses sin respuesta. Un usuario propone buscar afectados para una demanda conjunta.
- **[INFERENCIA]** En España el patrón no es *"discutimos con pruebas contradictorias"* sino *"el dinero no vuelve y no hay a quién acudir"*. Cambia la naturaleza del problema: la prueba sirve para un juicio, no para un arbitraje rápido.
- **Fuente:** https://www.idealista.com/news/foro/alquiler/816389-alguien-mas-ha-tenido-que-enfrentar-que-la-agencia-rent2be-malaga-te-robe-no-te-devuleva-la-fianza

### Falso positivo detectado — no usar
**[HECHO]** Property118, *"The missing inventory that cost a landlord thousands"* (30 oct 2025) aparece como primer resultado en varias búsquedas obvias y **no es un caso real**: el propio artículo declara pertenecer a la *"Property118 viral series for entertainment purposes"*. Contaminaría cualquier investigación rápida. https://www.property118.com/landlord-lessons-inventory-nightmare/

### Los cinco modos de fallo, no uno
**[INFERENCIA]** La formulación del problema ("no documentan de forma fiable") es más estrecha que la evidencia. Los modos de fallo observados son cinco:

| # | Modo de fallo | Evidencias |
|---|---|---|
| a | No se documentó nada | E2, E7 |
| b | Se documentó, pero sin fotos ni detalle utilizable | E4, E5, E12 |
| c | Se documentó bien y **se perdió** (cambio de gestor, empresa cerrada) | E3 |
| d | Se documentó bien pero el informe es **alterable a posteriori** | E8, E9 |
| e | Se documentó bien pero **nunca se compartió** con la otra parte | E10 |

Los modos (c), (d) y (e) son de **custodia e integridad**, no de captura, y son exactamente los que las herramientas actuales resuelven peor.

---

## 3. Current workflow

La mejor fuente única encontrada es el hilo *"DIY Inventory Recommendations"* de OpenRent (12–20 jun 2025), verificado dos veces, la segunda pidiendo transcripción literal: https://community.openrent.co.uk/t/diy-inventory-recommendations/83574

**Pregunta original [FUENTE]** (`Aysha11`): *"I'm trying to create my own inventory for a 3 bed house… Does anybody have a tried and tested way to do this yourself? Are there any apps you would recommend? Or is it worth getting it done professionally?"*

**Respuestas — el workflow real, con nombres y números [FUENTE]:**

| Actor | Workflow declarado |
|---|---|
| `David122` | **~200 fotos por inventario**, texto detallado, firmas de ambas partes **antes de la entrada** |
| `Nilesh` | Plantilla propia derivada de un informe de pago anterior, **~160 fotos con sello de fecha/hora**, PDF por email y *"email confirmation of acceptance"* |
| `tatemono` | **Google Photos compartido por código QR**, argumentando que los timestamps EXIF se manipulan pero las fechas de subida a un servicio en la nube no |
| `Ian43` | *"Download the smarter inventories app. It's a bit fiddly but it does the job."* |
| `A_Z` (sobre Inventory Hive) | *"you need a day to do your inventory. It's very thorough"* |
| `Karl11` | *"a couple of hours"*; *"if you can't spare that then you shouldn't be self managing"* |
| `mod_harry` (staff OpenRent) | Plantilla Word gratuita; sugiere meter las fotos *"under the column titled 'Condition'"* |
| `Allan6` / `Paul37` / `Blondie.1` | Vídeo subido a **YouTube** / **Dropbox** / inventario en vivo en **iPad** con el inquilino firmando el día de entrada |
| `Marcia Maynard` (US, BiggerPockets) | Formulario en papel con *"C & F = clean & functional"* preimpreso en cada línea; descriptores calibrados (*"dime size, nickel size, quarter size"*); firma antes de entregar llaves y **72 horas** para que el inquilino añada incidencias |
| `Colleen F.` (US) | Inventario por email antes de entrar **y una carpeta física dentro de la propiedad** |

**El debate sobre inmutabilidad — hilo "Inventory Video", OpenRent, 2–8 mar 2024** (https://community.openrent.co.uk/t/inventory-video/61968 y su página 2):
- `Chris` **[FUENTE]:** *"You are taking high definition photos that are date stamped using your smartphone camera which is exactly what is required by the deposit schemes."*
- `David122` **[FUENTE]** — el requisito mejor formulado de toda la investigación: ***"The key issue is that neither you nor the tenant should be able to add, change or delete photos once you've both signed."***
- `tatemono` **[FUENTE]** admite que **su propio workaround está roto**: *"image EXIF data is very easy to change."* / *"the photos, not to mention the upload details, will be post the date of signing so inadmissable if I attempt to use them in a dispute."*

**Australia — property managers digitalizando** (PropertyChat, may 2019, https://www.propertychat.com.au/community/threads/condition-report.38889/):
- `Tom Rivera` (PM) **[FUENTE]:** *"We've got plenty of options for digital signature, but not for tenants to fill out the forms digitally."* — hueco de proceso declarado por un profesional.
- `Dan Wood`, como inquilino: *"my previous agency had a simple web form on their iPad, filled things in and asked me to sign at the bottom."*

**Servicio humano como workflow alternativo:** en Reino Unido existe una industria consolidada de *inventory clerks* independientes que acuden físicamente, con asociación gremial propia (AIIC, fundada 1996) y precios de lista públicos (§5).

### ¿Existe un ugly workflow real?
**Sí, pero con matices importantes [INFERENCIA]:**
- Es **ugly en el segmento self-managed**: 200 fotos sueltas, plantillas Word, PDFs por email, Google Photos, YouTube, papel con bolígrafo (E5, sep 2026).
- **No es ugly en el segmento profesional**: agencias y clerks ya usan herramientas verticales maduras con firma, plantillas y sync.
- **Corrección a la hipótesis de partida:** en ~20 páginas de foros leídas, **nadie mencionó WhatsApp** como canal de documentación del estado, y **nadie mencionó Excel**. El canal recurrente es **email con PDF adjunto**, seguido de Dropbox / Google Photos / YouTube. Si una hipótesis de producto asume "WhatsApp + fotos", esta investigación **no la respalda**.

### ¿Por qué siguen usando el workaround?
1. **[HECHO]** El coste del clerk (£85–£170 por acto; ciclo completo ≈ £312 con IVA) equivale al **22–27% de la fianza media británica (£1.175)** que protege. El ratio explica que el 20% de arrendadores ingleses no haga inventario alguno (EPLS 2024).
2. **[FUENTE]** Creencia extendida de que el móvil ya basta: *"all this stuff about tenant having to sign ect, what a nonsense, its evidence full stop"* (`Leslie1`, 6 mar 2024).
3. **[FUENTE]** Existe al menos un caso de propietario que **ganó en juicio con sus propias fotos**: `Geoff` presentó *"original pictures I took at the start of their tenancy and images at the end"* y obtuvo compensación completa.
4. **[INFERENCIA]** El workaround falla de forma **silenciosa y diferida**: el usuario no descubre que su prueba era inválida hasta 12–36 meses después, cuando ya no puede corregirlo. Eso destruye el bucle de aprendizaje que normalmente empuja a comprar una herramienta.

---

## 4. Trigger and frequency

### Trigger externo
**[HECHO]** El trigger es inequívoco, externo y con fecha: **la entrega de llaves** (check-in) y **la devolución de llaves** (check-out). No depende de disciplina sostenida ni de un hábito: ocurre o no ocurre en un día concreto. En jurisdicciones con mandato legal el trigger está además reforzado por un plazo:

| Jurisdicción | Plazo legal asociado al trigger |
|---|---|
| Victoria (AU) | 2 copias antes de ocupar; el inquilino devuelve firmada **en 5 días hábiles**; el arrendador completa la de salida **en 10 días** |
| NSW (AU) | Entregada antes o al firmar; el inquilino devuelve **en 7 días** |
| Michigan (US) | El inquilino devuelve el checklist **en 7 días** |
| Massachusetts (US) | Statement de condición al recibir la fianza o **en 10 días** |
| Kansas (US) | Inventario conjunto **en 5 días** |
| Wisconsin (US) | Al menos **7 días** para inspeccionar antes de aceptar la fianza |

**[HECHO]** Reino Unido y España **no tienen mandato legal**, por lo que el trigger es puramente operativo y evitable.

### Frecuencia
**Rotación anual del parque de alquiler — tres fuentes independientes, tres continentes, convergencia notable:**

| Mercado | Rotación anual | Base del cálculo |
|---|---|---|
| Victoria (AU) | **33,9%** | [INFERENCIA] 249.891 bonds devueltos / 736.352 en custodia (RTBA 2024-25) |
| Escocia | **36,8%** | [INFERENCIA] 98.220 devoluciones / 267.227 depósitos (FOI Gobierno escocés 202500459983) |
| España | **30–40%** | [HECHO] Banco de España DO 2432: *"los nuevos contratos suponen… entre un 30% y un 40% del parque de vivienda arrendada"* (2011-2022) |
| EE. UU. | 22% de hogares en alquiler se mudó en el último año | [HECHO] Zillow 2025 (mide mudanzas de hogares, no ciclos de fianza) |

**[INFERENCIA]** Una rotación del 30–37% es la asunción más defendible para dimensionar el volumen de eventos. En Inglaterra y Gales eso daría **~1,7 millones de ciclos check-in/check-out al año**; en España, **1,08–1,44 millones de nuevos contratos anuales** (3,6M viviendas × 30–40%).

### El problema de la frecuencia POR USUARIO — y es el argumento más fuerte en contra
**[HECHO]** Distribución de cartera:
- Inglaterra (EPLS 2024): **45% de los landlords tiene 1 propiedad** (21% de los tenancies); 38% tiene 2–4; **17% tiene 5+ y concentra el 49% de los tenancies**.
- España (Observatorio del Alquiler, INE EPF 2023 + ECV 2024): **93,4% de los propietarios tiene un solo inmueble adicional**.
- Duración media de residencia de un inquilino privado inglés: **4,7 años** (EHS 2024-25).

**[INFERENCIA]** Un landlord con una propiedad vive el trigger **una vez cada ~4,7 años** y una disputa formal **una vez cada ~50 años de alquiler** (1% × ~5 años/ciclo). Eso es un evento de tipo seguro, no un uso recurrente. Explica de forma económica por qué todas las aplicaciones B2C de este espacio tienen 9, 29 o 37 reviews.

### ¿Valor inmediato o disciplina diferida?
**[INFERENCIA]** Éste es el punto que la pauta de discovery del usuario penaliza explícitamente, y hay que ser claro: **el usuario NO obtiene valor inmediato**. El valor se materializa 12–36 meses después, condicionado a que ocurra una disputa (1% formal, 37% deducción). El trigger de captura es externo e inevitable; el **beneficio** no lo es. Es el perfil económico de un seguro vendido a alguien que no ha tenido nunca un siniestro.

---

## 5. Economic impact

### Reino Unido — el único mercado con datos auditados
**[HECHO]** TDS Group, *Statistical Briefing 2024/25*, datos a 31 mar 2025 (agregado de los tres esquemas autorizados, recopilado por MHCLG):

| Jurisdicción | Depósitos protegidos | Valor protegido | Depósito medio | Disputas 12m | % disputas |
|---|---|---|---|---|---|
| Inglaterra y Gales | **4.706.470** | **£5.528.788.498** | **£1.175** | **46.950** | **1,00%** |
| Escocia | 243.283 | £215.523.853 | £885,90 | 5.951 | **2,44%** |
| Irlanda del Norte | 72.790 | £51.644.311 | £709,50 | 358 | 0,49% |
| **Total UK [INFERENCIA]** | **5.022.543** | **£5.795.956.662** | — | **53.259** | **1,06%** |

**Serie temporal [HECHO]** (Inglaterra y Gales): disputas 29.967 (2021) → 42.242 (2024) → 46.950 (2025); tasa 0,70% → 0,91% → **1,00%**.
**[INFERENCIA]** Entre 2023-24 y 2024-25 los depósitos crecieron +1,78% y las disputas **+11,15%**. La tasa de disputa ha subido un **43% relativo en cuatro años**. Es la tendencia más favorable a la tesis del problema que aparece en todo el dossier.

**Causas de reclamación [HECHO]** (Ing. y Gales 2024-25, acumulables): **limpieza 54%**, **daños 49%**, redecoración 31%, jardinería 14%, rentas impagadas 10%. Las dos dominantes son exactamente disputas sobre estado documentado o no documentado.

**El dato que mejor dimensiona el problema real [HECHO]** — English Private Landlord Survey 2024 (MHCLG, >9.000 arrendadores, 1,3M de depósitos representados):

| Resultado de la fianza | % |
|---|---|
| Devuelta íntegra | **59%** |
| Devuelta parcialmente | **22%** |
| Retenida en su totalidad | **15%** |
| Hicieron inventario de mobiliario/enseres | **80%** |

**[INFERENCIA] El 37% de los arrendadores dedujo algo.** Con tasa de disputa formal del 1,00%, **por cada disputa formal hay ~37 deducciones no disputadas**. El volumen del problema es ~37× el de la adjudicación. Y **1 de cada 5 arrendadores no hace inventario alguno**.

**Tiempos y resultado [FUENTE — mydeposits, operador del esquema, ago 2025]:** 90% de inquilinos recupera *"todo o parte"* en insured, >80% en custodial; el arrendador se lleva el 100% de lo reclamado en <20% (custodial) y 7% (insured); resolución custodial 15 días, insured 55 días. ⚠️ *"Todo o parte"* es una métrica diseñada para parecer favorable: un inquilino que recupera el 5% cuenta como éxito.

**Coste de la documentación profesional [FUENTE — precios de lista de proveedores]:**
- OpenRent: Inventory **desde £95** (IVA incl.), Inventory + Check-In **£145**, Check-Out **£85**; +£20 amueblado, +£20 por dormitorio adicional.
- InventoryFlex (Londres, clerks AIIC): estudio £110 → 5 dorm. £160 (inventario); check-out £100–£150. Sin IVA.
- AIIC (guía de precios a sus miembros, oct 2024): casa de 3 dorm. sin amueblar = **£230** inventario + check-in.
- **[INFERENCIA]** Ciclo completo de un 2 dormitorios ≈ **£260 + IVA ≈ £312**, es decir **22–27% de la fianza media** que protege.

### Estados Unidos — el dato de outcome más sólido del dossier
**[HECHO]** Zillow *Consumer Housing Trends Report 2024 — Renters* (campo mar–jul 2024, **>36.000 inquilinos**, seis encuestas nacionalmente representativas). Entre inquilinos recientes que venían de otro alquiler:

| Resultado | % |
|---|---|
| Depósito devuelto **íntegro** | **40%** |
| La mayor parte | 18% |
| Parte | 9% |
| **Nada** | **24%** |
| Nunca pagó fianza | 9% |

**[INFERENCIA]** Excluyendo al 9% que no pagó: **44% recupera íntegro, 56% no recupera todo, 26,4% no recupera nada.** Zillow es un marketplace sin producto de fianza que vender — es la fuente menos interesada disponible.

**[HECHO]** Zillow 2025: 83% de los inquilinos recientes pagó fianza; **mediana $795**, **media $1.324**. Census HVS Q2 2026: **46.827.000 hogares en alquiler** (31,3% del parque).

⚠️ **[HECHO] La cifra de "$45 mil millones retenidos en fianzas en EE. UU." es marketing.** Su origen es **Rhino** (2019), aseguradora que vende el sustitutivo de la fianza, en su propuesta "Renter's Choice"; documentado por Shelterforce. **No existe ninguna estadística oficial estadounidense del stock de fianzas** (ni Census, ni HUD, ni CFPB). Una estimación propia da un rango defendible de **$31–62 mil millones**, que contiene la cifra pero no la valida.

### España
**[HECHO]** LAU art. 36: fianza obligatoria de **una mensualidad** en vivienda; el saldo devenga **interés legal** transcurrido un mes desde la entrega de llaves. Garantías adicionales limitadas a dos mensualidades.
**[HECHO]** Cataluña (INCASÒL, vía *Público*, jul 2026): saldo de fianzas depositadas **>2.000 millones €** en 2024, frente a 1.103 M€ en 2013; generación neta ≈ **120 M€/año**. Cataluña Q3 2025: 26.962 contratos registrados → **~108.000/año**.
**[HECHO]** Banco de España DO 2432: **3,6 millones de viviendas en alquiler** (2023), 18,7% de los hogares. INE ECV 2024: 20,4% de hogares en alquiler.
**[FUENTE — OCU, 3 oct 2025]** 4.773 consultas y reclamaciones sobre alquiler en el primer semestre; **13% de los inquilinos** reporta que el arrendador se niega a devolver la fianza alegando desperfectos; **9% de los arrendadores** reporta conflicto sobre el estado al fin del contrato. ⚠️ Base autoseleccionada, no tasa poblacional.
**[SIN EVIDENCIA]** No existe estadística nacional agregada de fianzas depositadas en España, ni desglose judicial de reclamaciones de fianza (el CGPJ no lo desagrega; sus ficheros de arrendamientos urbanos llegan a 2020).

### Australia (Victoria) — el mejor dato de outcome del mundo
**[HECHO]** RTBA Annual Report 2024-25: **736.352 bonds** en custodia, **A$1.545 millones**, bond medio ≈ A$2.098; 245.125 depositados y 249.891 devueltos en el año; **96% de las reclamaciones se resuelven de acuerdo**, 4% por VCAT.

| Destino de la fianza | % |
|---|---|
| Íntegra al inquilino | **65%** |
| Repartida | **25%** |
| Íntegra al arrendador | **10%** |

**[INFERENCIA] Convergencia notable:** el 35% de Victoria, el 37% de Inglaterra (EPLS) y el 56% de EE. UU. (sin depositario neutral) sugieren que **entre el 35% y el 40% de las fianzas sufre alguna deducción** en un mercado maduro con custodia pública.

### Irlanda y Nueva Zelanda
**[HECHO]** RTB Ireland 2024: 9.564 solicitudes de disputa; **19% por retención de fianza ≈ 1.817 casos**; parque registrado 327.992 → tasa de disputa por fianza 0,55%.
**[HECHO]** Tenancy Services NZ Q2 2026: *"refund bond"* aparece en el **43,26%** de todas las solicitudes al Tribunal (segundo motivo tras impagos).

### Lo que NO se pudo cuantificar
**[SIN EVIDENCIA]:** importe medio en disputa en UK; reparto agregado de la adjudicación entre landlord y tenant; coste medio de la reparación reclamada en cualquier jurisdicción; tamaño de la industria de inventory clerks; número de états des lieux realizados al año en Francia; horas ahorradas (las únicas cifras de esfuerzo son autodeclaradas y contradictorias: *"a couple of hours"* vs *"a day"* vs ~200 fotos).

---

## 6. Buyer and willingness to pay

### Quién sufre, quién usa, quién paga

| Rol | Segmento |
|---|---|
| **Sufre** | Ambas partes, asimétricamente. El arrendador pierde la reclamación sin prueba; el inquilino pierde la fianza sin prueba. En España y Francia la presunción legal ante la ausencia de documento **perjudica al inquilino** (art. 1562 CC / art. 1731 CC francés); en UK y en la mayoría de estados de EE. UU. perjudica a quien reclama, es decir **al arrendador** |
| **Usa** | Quien está físicamente en la vivienda el día de la entrega: el landlord self-managed, el comercial de la agencia, el clerk, o —en el modelo de RentCheck— el propio inquilino |
| **Compra** | El arrendador o la agencia. **Nunca el inquilino**, que es quien más se beneficia de la prueba en España y Francia |
| **Autoridad** | Sin fricción: el landlord individual decide solo. En agencia decide el director de lettings |

**[INFERENCIA] Desalineación de go-to-market en España y Francia:** el beneficiario legal de la documentación es el inquilino, pero quien tiene el presupuesto, el acceso a la vivienda y la relación comercial es el propietario. El inquilino no tiene ni el momento ni la autoridad para imponer el proceso.

### Evidencia de gasto actual (la señal más importante)
**[HECHO] Sí existe gasto real alrededor del problema, y es sustancial en el lado humano:**

| Concepto | Precio verificado |
|---|---|
| Inventory clerk UK (inventario) | **£95–£160** |
| Inventory clerk UK (check-out) | **£85–£150** |
| État des lieux Francia — **tope legal** imputable al inquilino | **3 € TTC/m²** (60 m² → 180 €), y el propietario debe pagar al menos otro tanto → acto de hasta **~360 € TTC** |
| Constat por *commissaire de justice* (FR) | **158,58 € – 256,89 € TTC** según superficie, repartido 50/50 |
| Software vertical UK | **£10–£45/mes**, o **£0,10–£3,75 por informe** |
| Software específico consumidor ES (Acta Entrega) | **9 € por PDF** |
| Software FR (homePad, 2016, cifra del vendor) | **3–5 € por acto** |

**[INFERENCIA] Éste es el hallazgo económico central del dossier: el mercado paga £85–£170 por acto a un humano y £0,10–£3,75 por acto al software.** La brecha de ~40× no es ineficiencia a capturar: es el precio de que alguien **acuda físicamente y asuma responsabilidad como tercero independiente**. El software de este espacio no vende documentación, vende **productividad al clerk**. Un producto nuevo que solo documente mejor compite en el lado de £0,20, no en el de £120.

### Evidencia de que la disposición a pagar ya fue destruida una vez
**[FUENTE]** Un property manager en UK Business Forums: *"We can all do it on an ipad now for 12 pounds wheres years ago we would be paying a company 50 plus"*. Contrapunto en el mismo hilo: *"producing an inventory carried out by yourself doesn't carry anywhere as near as much weight as if you used an independent inventory clerk"*.
**[FUENTE]** En OpenRent, la referencia de precio que los propios landlords manejan es **£35/año** (Inventory Hive, una propiedad) y **~£5/inventario** (Smarter Inventories).

### Evidencia de que hay quien claramente NO pagaría
**[FUENTE]** `Leslie1`, propietario: *"I agree you should take pics, all this stuff about tenant having to sign ect, what a nonsense, its evidence full stop"*; *"Most images are date stamped, proof."* Es el perfil que cree que el móvil ya resuelve el problema probatorio y que califica las reclamaciones de fianza de *"a lot of hassle"*.

---

## 7. Existing market

**[HECHO] El mercado está poblado, maduro y con precios comprimidos. No es un espacio vacío.** Todos los precios de la tabla fueron abiertos y verificados en la página del proveedor.

### Software vertical de inventario / inspección

| Producto | Mercado | Target | Pricing verificado | Plataforma | Tracción verificada |
|---|---|---|---|---|---|
| **Inventory Hive** (inventoryhive.co.uk) | UK | Agencias, clerks, landlords | **£300/año o £30/mes +IVA** (hasta 50 props, 1 usuario, informes y almacenamiento ilimitados); branding propio £385/año; tier Worker 50+ con usuarios ilimitados, POA | iOS/Android/web, offline | 37 ratings iOS (4,1); 29 Android (3,7), 5k+ installs; 17 reviews Trustpilot. **Partnership formal con TDS** |
| **InventoryBase** (inventorybase.co.uk) | UK | Clerks profesionales | Solo **£35/mes o £350/año**; Duo £45; Team £75; Pro £349. Extra prop 20p; transcripción 35p/min | iOS/Android/web | 51 reviews Android (3,3), 10k+ installs; **3 reviews Capterra** |
| **Property Inspect** (propertyinspect.com) | UK + intl | Agencias, PM comercial | **£45/mes** (1 user/100 props) → **£245** (10/500) | iOS/Android/web | 42 reviews Android (3,4), 10k+ installs; **1 review Capterra**. Mismo grupo que InventoryBase (Radweb) |
| **Kaptur** (No Letting Go) | UK | Agencias + red de clerks | **£45 / £75 / £150 mes** por volumen | iOS/Android/web | Brazo software del mayor proveedor de clerks UK: integración vertical servicio+software |
| **Imfuna Let/Rent** | UK + US | Agencias, clerks | **£35/£60/£85 mes** por volumen; AI speech-to-text £20/user/mes | iOS/Android/web | 🚩 **100+ instalaciones en Google Play**; 8 reviews Capterra; 11 Trustpilot |
| **Smarter Inventories** | UK | Clerks pequeños | Packs prepago **£2,33–£3,75 por informe**; anual 300 informes/£299 | iOS/Android/web | Micro-vendor |
| **TouchRight** | UK | Agencias | desde **£15/mes** | — | No verificada |
| **Inventorai** (inventorai.co.uk) | UK | Todos | **£25/mes + 20p/propiedad** (→10p a partir de 1.001) | Web + móvil | 🆕 Pre-lanzamiento |
| **RentCheck** (getrentcheck.com) | EE. UU. | PM multifamily/SFR | **$1 / $1,25 / $1,75 por unidad/mes** | iOS/Android/web | 🏆 **18.000–20.000 ratings iOS (4,8); 100k+ installs; 6.590 reviews Android**. Funding $3,6M |
| **zInspector** | EE. UU. | PM | Portal de precios bloqueado — **no verificable** | iOS/Android/web | 261 reviews Android (4,8), 10k+ installs; 10 Capterra |
| **SnapInspect** | NZ/AU/US | PM | **"Contact sales"** — sin cifras públicas | iOS/Android/web | **58 reviews Capterra, 5,0** (57×5★) |
| **HappyCo** | EE. UU. | Multifamily enterprise | Quote only. **Mínimo 500 unidades** | iOS/Android/web | 68 reviews Capterra (4,6). Motor de inspecciones de Buildium |
| **Chapps Rental Inspector** | BE/EU | Agencias, PM | **€7,50 por informe** (PAYG) o **€260/usuario/año** | iOS/Android/web | 23 reviews Android (3,9), 1k+ installs; **2 Capterra** |
| **Acta Entrega** (actaentrega.com) 🇪🇸 | **España** | Landlord/inquilino individual | **€9 por PDF final**, sin registro | Web | Micro-producto. Único competidor directo español encontrado |
| **MoveProof** | Intl | Individual | Freemium; Pro compra única (importe no publicado) | Android | 🚩 **50+ instalaciones, 9 reviews** |
| **homePad, Immopad, Check&Visit, Startloc, Nockee, Leasy Peasy** 🇫🇷 | **Francia** | Agencias, propietarios | homePad **3–5 €/acto** [FUENTE: vendor, 2016] | — | **[INFERENCIA]** ≥6 proveedores especializados compitiendo en un solo país es la señal más fuerte de que el mercado francés está monetizado |

### PMS con inspecciones incluidas (competencia de bundle)

| Producto | Pricing verificado | Inspecciones |
|---|---|---|
| **Buildium** | Essential **desde $62/mes**; Growth $192; Premium $400 | ✅ En los 3 planes. Motor: **HappyCo**. Essential añade $99 setup + $40-95/mes |
| **DoorLoop** | Starter $99/mes; Pro $189; Premium $239 | ⚠️ "AI Inspections" solo en el AI Add-On (Pro/Premium) |
| **TenantCloud** | Starter $18/mes; Growth $35; Pro $60 | ✅ 15 / 50 / custom inspecciones. **Starter no las incluye** |
| **Landlord Studio** | Go gratis (3 uds); Pro $12/mes + $1,20/unidad | ❌ No aparecen inspecciones en la página de precios; **0 menciones en 150 reviews de Capterra** |
| **AppFolio / Yardi Breeze** | Quote + mínimos de unidades | ✅ Inspecciones móviles nativas |
| **Goodlord** 🇬🇧 | No verificado | ✅ Módulo de inventory management con firma electrónica |

### Competidores gratuitos — el verdadero techo de precio
**[HECHO] TurboTenant** ofrece *Condition Reports* **completamente gratis**: personalizables por estancia, fotos, **firma electrónica**, y **el inquilino puede completarlo sin tener cuenta**. TurboTenant declaró **>1.000.000 de landlords** en feb 2026.
**[HECHO] Zillow Rental Manager** tiene *Property Condition Report* en producción: planos, valoración ítem por ítem, **hasta 8 fotos por ítem**, envío para firma. Disponible en **24 estados**; el roadmap declarado incluye que el inquilino pueda completarlo solo. Zillow: 214M usuarios únicos/mes.
**[HECHO]** En España, **Idealista, Fotocasa y Habitaclia solo publican contenido editorial** ("cómo hacer un inventario fotográfico"). No se encontró ninguna herramienta de inventario en los portales españoles.

### Servicio humano — el precio de referencia real
**[HECHO]** OpenRent vende el servicio con clerk acreditado (£95/£145/£85). **No Letting Go** es la mayor red nacional del Reino Unido y está **integrada verticalmente** con su propio software (Kaptur). **AIIC** opera desde 1996 con formación y respaldo en disputas.

### Productos muertos: no hay cadáveres, hay zombis
**[HECHO]** Se verificó el historial de versiones de las apps candidatas a abandono y **casi todas siguen activas**: Inventory Hive (actualizada hace días), InventoryBase (dic 2025), Property Inspect (dic 2025), Imfuna (sep 2026), Property Inspection Manager AU (sep 2026, añadiendo "AI Notes from Video"). **[INFERENCIA]** El hallazgo es más incómodo que encontrar muertos: el espacio está lleno de productos mantenidos durante años que **nunca superan las decenas de reviews**. Eso no describe un mercado que mata productos, sino un mercado con **techo de ingresos bajo por cliente y crecimiento plano**, donde un equipo de 2–5 personas sobrevive indefinidamente sin escalar nunca.

**[HECHO]** Product Hunt: no se encontró ningún lanzamiento significativo ni con tracción medible en esta categoría. **[INFERENCIA]** El espacio no atrae a la comunidad early-adopter.

**[HECHO] Los informes de "market size" del sector no son utilizables.** El más citado (HTF Market Intelligence: *Property Inspection Software*, $1,2B→$2,6B, CAGR 11,8%) lista como vendors a **Inspectorio** (control de calidad textil), **SiteSpect** (A/B testing web) y **iAuditor** (auditorías de seguridad laboral). La categoría que miden no existe. Hay al menos 6 informes más con cifras distintas y las mismas listas recicladas.

---

## 8. Negative reviews and market gaps

Quejas verbatim verificadas en Trustpilot, Capterra, Software Advice, App Store y Google Play. Reddit no fue accesible, lo que sesga esta sección hacia plataformas donde los vendors influyen en la recogida de reseñas.

### Patrones, ordenados por peso de evidencia

**P1 — Pérdida de datos y crashes a mitad de inspección** (5 productos distintos; el patrón más fuerte)
- Imfuna (1★, 11 abr 2025): *"Spend over an hour creating a detailed inspection only for the App to closedown and lose all the information I've entered"* / *"After sending the Inspection to the PC the images are either missing or corrupted"*
- InventoryBase (Google Play, 26 sep 2024): *"The app constantly keeps crashing. Since 0800 I've had the app crashing on me at least about 70-80 times minimum."*
- Inventory Hive (4★, App Store): *"having the app crash on you when you're bedroom no.2 into an inventory and it crashes isn't fun."*
- RentCheck (1★, 6 jun 2025): *"I loose total progress and the pictures I had on RentCheck disappear… I'm left with 1/4 of the photos I documented"*
- AppFolio: *"app constantly freezes, and won't save narratives"*
- Chapps (30 mar 2026): *"glitches every 5 secs"*

**P2 — Fotos: subida lenta, calidad degradada, cámara rota**
- AppFolio: *"it usually takes several attempts to upload photos to each section, often timing out"* / *"My inspection photos look like they were taken on an old flip phone"* / *"The camera in this app is horrendous…it's all blurry"*
- RentCheck: *"It's just a black screen with the shutter button"*
- Imfuna: *"takes too long to add the pictures and for the app to respond"*
- SnapInspect: falta de zoom en las fotos; *"get rid of the 'upload' aspect"*

**P3 — Sincronización y modo offline**
- HappyCo: *"Sometimes inspections trouble with syncing/freezing during picture uploads"*; *"the occasional issue with lack of cell signal coverage"*
- Imfuna: *"can be very slow unless you turn off the live sync"*
- Inventory Hive: *"Triggering offline mode on both ipad and iPhone devices is also a little tedious"*

**P4 — El inquilino queda sin copia / desequilibrio de poder** ⭐ *el hueco más claro y el menos atendido*
- Inventory Hive (1★, 2 oct 2025): *"There is no way to download the signed inventory so, as a tenant, one ends up with NO copies of what has been said. Typical con to give all the power to the landlords and leave the tenant with no proof whatsoever."*
- RentCheck (1★): limitación a **un solo usuario por vivienda** — los compañeros de piso no pueden participar; e imposibilidad de subir fotos externas.
- RentCheck (1★, 1 mar 2026): *"RentCheck takes more than an hour to complete. If you met with a real person to check out of your apartment instead of RentCheck, it would take 15 minutes."*
- RentCheck (5★ (!), 2 ago 2026) — la crítica más lúcida viene dentro de una review positiva: *"seems to place a lot of documentation work on the tenant. passed on from the landlord or property management team."*

**P5 — Integridad probatoria y durabilidad del informe** ⭐ *infraexplorado y crítico*
- AppFolio (Capterra, 4★): *"Once an inspection is completed any user can delete it. It needs to be non-modifiable once completed."*
- Inventory Hive (1★, 7 sep 2024): *"The inventory co I used closed. The inventories provided using Inventory Hive also stopped working so inventories inc photos could not be opened properly at the end of the tenancy. Caused so much stress and difficulty making any deposit deductions."* → **riesgo de lock-in: tu prueba vive en el SaaS de un tercero que puede desaparecer** (coincide con E3).
- Coherente con el requisito formulado por un usuario en OpenRent: *"neither you nor the tenant should be able to add, change or delete photos once you've both signed."*

**P6 — Pensado para grandes gestoras, no para landlords pequeños**
- Inventory Hive (1★): *"You'd think they would open it to a bigger market, eg, smaller landlords. They would make more money. Seems like a no brainer"*
- AppFolio (5★): *"There is a minimum number of units we had to maintain in order to begin using AppFolio."*
- HappyCo: mínimo de **500 unidades**.
- SnapInspect: *"pricing could always be lower for a small business!"*

**P7 — Precio y prácticas comerciales**
- InventoryBase: *"while not inexpensive, alternatives that are more intuitive to learn will save money in the long run"*; un usuario migró a otro producto por *"cheaper, more comprehensive, and more robust"*.
- RentCheck: *"they require 30 days' notice to cancel"* / *"There's no cancellation button under your account"* / *"you have to chat with one of their reps, who tries to convince you to stay"* — patrón oscuro de cancelación.

**P8 — Soporte** (InventoryBase: *"Customer support was rubbish"*; HappyCo: *"Telephone support is low"*; RentCheck: *"I was told the problem was me"*).
**P9 — UI y complejidad** (InventoryBase: *"confusing user experience"*; zInspector: *"There seem to be too many options which causes confusion"*, *"Editing the rooms is difficult. If you missed something you can not go back and take more pictures"*).
**P10 — Marca y exportación** (InventoryBase: *"Inventorybase branding in your face on reports"*; AppFolio: *"It can export CSV files, but not import them"*; HappyCo: *"No cover page for condition reports"*).
**P11 — Paridad Android/iOS** (HappyCo: *"the drastic difference between the android version was disappointing"*).
**P12 — Integraciones** (RentCheck↔AppFolio: *"it doesn't integrate well with Appfolio"*; Buildium↔HappyCo: *"They changed their application. I cannot get the same reports as before."*).

### Patrones buscados que NO aparecieron
**[SIN EVIDENCIA]:** "PDF feo o pesado" (solo indirectas); onboarding difícil (una sola queja); "obliga al inquilino a crearse cuenta" (ninguna cita directa); producto abandonado (ninguno: todos actualizados en 2025-2026); **"no lo acepta el esquema de depósitos"** (ninguna cita real — dato relevante en contra de la tesis de cumplimiento normativo).

### Gaps del mercado que la evidencia soporta
1. **Integridad y durabilidad de la prueba** (P5 + E3 + E8 + E9): informe sellado, no alterable, que sobreviva al cambio de gestor y al cierre del proveedor.
2. **Simetría entre las partes** (P4 + E10 + E1): que el inquilino tenga su copia y pueda participar sin que se le traslade todo el trabajo.
3. **Acceso del landlord pequeño autogestionado** (P6): declarado por usuarios de dos productos distintos.

⚠️ **No convertir automáticamente estos gaps en features.** Son huecos observados, no demanda validada.

---

## 9. Distribution

### Dónde están y cuántos son

| Comunidad | Tamaño verificado |
|---|---|
| **BiggerPockets** | **3.000.000+** miembros |
| **NRLA** (landlords UK) | **100.000–110.000** miembros |
| **OpenRent** (plataforma) | declara >7 millones de landlords e inquilinos |
| **Propertymark** (agentes UK) | **18.711** miembros individuales (jun 2025) |
| **ARLA Propertymark** | 10.219 sucursales, 2.258.399 propiedades gestionadas ⚠️ **dato de 2020, probablemente obsoleto** |
| **NARPM** (US) | **>6.000** miembros |
| r/realestateinvesting / r/RealEstate / r/Landlord / r/PropertyManagement | 1,96M / 2,5M / ~210k / 67,3k ⚠️ vía agregadores terceros, no verificado en Reddit |
| **AIIC** (inventory clerks UK) | **[SIN EVIDENCIA]** — no publica censo de miembros |

### SEO: el canal está ocupado por contenido gratuito con autoridad
**[SIN EVIDENCIA] No se pudieron obtener volúmenes de búsqueda:** el proxy bloquea Ahrefs, Google Trends, Google Suggest y Ubersuggest. **Cualquier cifra de volumen que aparezca sin acceso a una herramienta de pago debe considerarse inventada.**

**[HECHO] Lo que sí se verificó — la composición del SERP, que es evidencia más dura que el volumen.** Para `landlord inventory template UK` / `property inventory template`, la primera página está enteramente ocupada por **plantillas gratuitas usadas como lead magnet** por empresas adyacentes: Simply Business (aseguradora), Rocket Lawyer, Zervant, Lendlord, SelfLandlord, AssetsForLife, Leasense, RentalDocs, InventoryFlex. Y, de forma más grave, **mydeposits (el propio esquema de depósitos) publica un checklist de inventario gratuito distribuido por la NRLA**. En España el patrón es idéntico: actaentrega.com, roomix.ai, vesta-crm.com, wonder.legal, seag.es.

**[INFERENCIA]** Cuando una institución (mydeposits, NRLA, NSW Fair Trading) regala la plantilla, no es solo competencia de producto: es **competencia de distribución con autoridad de dominio inalcanzable**. El SEO de plantillas no es un canal de entrada viable.

### Los canales institucionales ya tienen partner
**[HECHO]**
- **TDS ↔ Inventory Hive:** partnership formal desde 2020, 10% de descuento para agentes TDS, y —lo más relevante— **las imágenes 360° de Inventory Hive están integradas y son aceptadas en el portal de evidencias de disputas de TDS**. Promoción activa en sep 2025.
- **mydeposits ↔ NRLA ↔ No Letting Go:** checklist gratuito distribuido vía NRLA; guía conjunta de gestión de inventarios con No Letting Go (propietaria de Kaptur).
- **NRLA** recomienda contratar miembros de la AIIC.
- **DPS:** **[SIN EVIDENCIA]** no se encontró herramienta propia ni partnership de inventario.

**[INFERENCIA]** El esquema de depósitos no construye la app: **certifica a un proveedor y le da integración en el portal de evidencias**. Eso es peor para un entrante que si la construyera, porque significa competir contra *"la herramienta que el adjudicador ya sabe leer"*.

### Naturaleza de la venta
**[INFERENCIA]** Ambos caminos son incómodos:
- **Self-serve a landlords:** CAC alto (SERP ocupado, subreddits con baja tolerancia a autopromoción, asociaciones con partner ya elegido), LTV bajo (45% tiene una propiedad, evento cada 4,7 años) y precio ancla en **£0** (TurboTenant, Zillow, plantillas institucionales).
- **B2B a agencias y clerks:** ciclo largo, integración con CRM de lettings, aceptación por el esquema de depósitos, y 8 incumbentes establecidos.
- **La única cuña que la evidencia señala:** landlords con **5+ propiedades que autogestionan** (≈17% × 52% × 2,86M ≈ **253.000 en UK**) — demasiado grandes para una plantilla de Word, demasiado pequeños para una agencia, y con frecuencia de evento suficiente para justificar una suscripción.

---

## 10. Market size

### Orden de magnitud de usuarios/negocios afectados

| Mercado | Base | Cifra | Fuente |
|---|---|---|---|
| UK | Hogares en alquiler privado (Inglaterra) | **4,7 M (19%)** | EHS 2024-25 |
| UK | Landlords que declaran renta a HMRC | **2,86 M** | HMRC 2023-24 |
| UK | Depósitos protegidos | **5,02 M** | TDS Briefing 2024/25 |
| EE. UU. | Hogares en alquiler | **46,83 M** | Census HVS Q2 2026 |
| EE. UU. | Unidades en propiedades de 1–4 unidades | **22,6 M (45,6%)** [INFERENCIA sobre RHFS 2021] | Census RHFS |
| EE. UU. | Empresas de gestión residencial | **245.484** | IBISWorld 2025 |
| España | Viviendas en alquiler | **3,6 M** | Banco de España DO 2432 |
| España | Propietarios con ≥1 inmueble adicional | **2,49 M** (93,4% con uno solo) | Observatorio del Alquiler |
| España | Empresas CNAE 6831 (intermediación) | **35.870** | eInforma, balances 2024 |
| Francia | Viviendas de bailleurs privados | **~7,2 M** (22,8% de residencias principales) | INSEE Focus 359 |
| Australia (Victoria) | Bonds en custodia | **736.352** | RTBA 2024-25 |
| Irlanda | Tenencias registradas | **327.992** | RTB 2024 |

**Orden de magnitud del problema: decenas de millones de viviendas afectadas globalmente; millones de ciclos check-in/check-out al año.** El problema es grande.

### TAM teórico vs. mercado realmente accesible para un producto indie
**[INFERENCIA con supuestos explícitos y discutibles]**

**Escenario A — UK, self-serve a £10/mes (£120/año):**

| Paso | Cálculo | Resultado |
|---|---|---|
| Landlords UK (HMRC) | — | 2.860.000 |
| × autogestionan (EPLS: 52% no usa agente) | ×0,52 | 1.487.200 |
| × con 2+ propiedades (los de 1 tienen un evento cada 4,7 años) | ×0,55 | 817.960 |
| × digitalmente activos y dispuestos a pagar por software de gestión — **supuesto: 15%** | ×0,15 | **122.694 compradores plausibles** |
| × cuota alcanzable sin canal institucional — **supuesto: 0,5–2%** | — | **613 – 2.454 clientes** |
| **ARR** | | **£73.000 – £294.000** |

**Escenario B — UK, B2B a agencias/clerks a £300–800/año:**

| Paso | Cálculo | Resultado |
|---|---|---|
| Sucursales de lettings (proxy ARLA 2020) + clerks independientes estimados | ~10.219 + ~3.000 | ~13.000 |
| × no cubiertos por los ≥8 incumbentes — **supuesto: 30% greenfield** | ×0,30 | 3.900 |
| × cuota alcanzable sin equipo comercial — **supuesto: 3–8%** | — | **117 – 312 cuentas** |
| **ARR** | | **£35.000 – £250.000** |

**Escenario C — EE. UU. self-serve:** el cálculo se rompe en el primer paso. TurboTenant (1M+ landlords) y Zillow ofrecen la funcionalidad **gratis**. El precio de referencia es **$0**.

**[INFERENCIA] Conclusión del dimensionado:** el techo realista de un producto indie de propósito único en este espacio es del orden de **£50k–300k ARR en Reino Unido a tres años**, apoyado en dos supuestos frágiles (15% de disposición a pagar y 0,5–2% de cuota sin canal). Es un nicho de decenas de miles de compradores plausibles, no de millones. Puede sostener a una persona **si y solo si** se resuelve el problema de distribución, que es el cuello de botella real, no el producto.

---

## 11. Global portability

### **Clasificación: MEDIA**

El *core problem* es idéntico en todos los mercados estudiados: documentar el estado para evitar una disputa al final del contrato. **Lo que no es portable es el vehículo legal, el custodio del dinero y la vía de resolución** — y eso es exactamente lo que determina si alguien paga.

| País | ¿Informe obligatorio? | Custodia del depósito | Resolución | ¿A quién perjudica la ausencia? | Portabilidad |
|---|---|---|---|---|---|
| 🇫🇷 **Francia** | **SÍ** (loi 89-462 art. 3-2), entrada y salida, formato electrónico admitido, contenido mínimo prescrito | Arrendador | Comisión de conciliación → tribunal; *commissaire de justice* si hay negativa | **Al inquilino** (art. 1731 CC), salvo si el propietario obstruyó su realización | **Media-alta** |
| 🇦🇺 **Victoria / NSW / QLD / TAS / ACT** | **SÍ** (RTA 1997 Vic s.35 — 25 penalty units; RTA 2010 NSW s.29 — 20 penalty units) | Bond boards estatales | VCAT / NCAT / QCAT | Al arrendador (el inquilino puede hacerla él mismo) | **Alta** |
| 🇬🇧 **Reino Unido** | **NO**, pero de facto obligatorio: el adjudicador decide solo con la evidencia aportada | 3 esquemas obligatorios (54% custodial / 46% insured) | **ADR gratuita y vinculante** — 53.259 casos/año | Al arrendador (es quien reclama) | **Alta** |
| 🇺🇸 **11 estados** (MA, MD, WA, KY, MI, GA, MT, AZ, KS, NV, WI) | **SÍ**, con sanción de hasta 3× el depósito | Arrendador | Small claims | Al arrendador | Problema alto / **negocio bajo** |
| 🇺🇸 resto (~39 estados) | NO | Arrendador | Small claims | — | Problema alto / **negocio bajo** |
| 🇮🇪 Irlanda | NO | RTB | RTB (9.564 disputas/año) | — | Alta (presunta) |
| 🇪🇸 **España** | **NO.** Ni la LAU ni ninguna norma autonómica lo exigen | Organismos autonómicos, **y solo obligatorio en 12 de 19 territorios** | **Solo vía judicial. No hay ADR ni arbitraje de consumo** entre particulares | **Al inquilino** (presunción art. 1562 CC) | **Baja** |
| 🇩🇪 Alemania | NO (*Übergabeprotokoll* es costumbre, no ley) ⚠️ no verificado en fuente primaria | Cuenta separada del arrendador (§551 BGB) | Tribunal | — | Media (no verificada) |
| 🇳🇱 Países Bajos | **[SIN EVIDENCIA]** | Arrendador, máx. 2 meses | — | — | No verificada |
| 🌎 LatAm | Sin institución de depósito comparable; alta informalidad | — | — | — | **Baja** |

### Justificación de "Media"
1. **Lo que sí es portable:** el objeto (una vivienda), el momento (entrega de llaves), el artefacto (fotos + descripción por estancia + firma + fecha), el idioma y la moneda. Un producto central podría servir en UK, Irlanda, Australia y Nueva Zelanda cambiando poco más que terminología.
2. **Lo que NO es portable y obliga a reconstruir por país:**
   - **El formato legal:** Francia prescribe contenido mínimo (relevés de compteurs, descripción por estancia, firmas) y tiene un tope de honorarios regulado (3 €/m² TTC al inquilino); un informe genérico no sirve.
   - **El árbitro:** en UK hay que ser legible por el adjudicador del esquema (y un competidor ya está integrado en su portal de evidencias). En España no hay árbitro, solo juzgado.
   - **La dirección de la presunción legal:** en España y Francia la ausencia de documento perjudica al **inquilino**; en UK, EE. UU., Victoria y NSW perjudica al **arrendador**. Esto invierte quién es el comprador natural y obliga a cambiar todo el mensaje de venta, no solo el idioma.
   - **El custodio del dinero:** tres esquemas privados en UK, bond boards estatales en Australia, organismos autonómicos en España, el propio arrendador en Francia, Alemania y EE. UU.
3. **[INFERENCIA] Distinción clave:** *portabilidad del problema* ≠ *portabilidad del negocio*. EE. UU. tiene el problema idéntico y el negocio cerrado por gratuidad. España tiene el negocio abierto y el problema sin forzador legal ni árbitro. **Solo UK, Australia/NZ e Irlanda combinan forzador institucional + disposición a pagar + un árbitro que consume evidencia estructurada.**

---

## 12. External dependencies

### Dependencias estructurales (peligrosas)
1. **Reguladores y esquemas de depósito.** El valor probatorio del output depende de que el adjudicador (TDS/DPS/mydeposits), el tribunal (VCAT, NCAT, juzgado español) o el marco legal francés lo acepten. Un cambio de criterio, de formato exigido o de portal de evidencias afecta directamente al producto. **[HECHO]** TDS ya integró el formato 360° de un competidor en su portal de disputas — es un precedente de que el esquema **elige formatos**.
2. **Legislación.** **[HECHO]** La Renters' Rights Act 2025 (Royal Assent 27 oct 2025; "big bang" **1 mayo 2026**) reescribe el mercado británico sin tocar los depósitos ni introducir obligación de documentar. Francia regula el precio máximo del acto por decreto. Andalucía suprimió la obligación de depósito de fianza desde el 24 ene 2026. El marco puede moverse por debajo del producto en cualquier dirección.
3. **Plataformas de distribución de apps.** Dependencia habitual de App Store / Play Store si el producto es móvil; para este caso concreto es inevitable, porque el trabajo se hace con una cámara en la mano dentro de una vivienda.
4. **PMS y CRM de lettings.** **[HECHO]** RentCheck vende la integración con AppFolio solo en su tier más caro; Properly existe para integrarse con Guesty/Hostaway; zInspector sincroniza con Propertyware. Y la queja *"it doesn't integrate well with Appfolio"* muestra el coste de esa dependencia. **[INFERENCIA]** En el segmento profesional, no integrarse es quedar fuera; integrarse es quedar a merced del roadmap ajeno.

### Dependencias convenientes (no estructurales)
- **Almacenamiento en la nube y CDN:** commodity, sustituible.
- **Firma electrónica:** existen múltiples proveedores y alternativas propias.
- **OCR / transcripción de voz / visión por computador:** varios productos lo están añadiendo en 2026 (Inventorai, SnapInspect "AI", Property Inspection Manager "AI Notes from Video"). Sustituible entre proveedores; no es un punto único de fallo.
- **Geolocalización y hora del dispositivo:** conveniente para el sellado, pero el propio mercado sabe que **EXIF es trivialmente manipulable** (*"image EXIF data is very easy to change"*), lo que convierte la confianza en el dispositivo en un problema de diseño, no en una dependencia externa.

### El riesgo de dependencia invertido: **el producto como dependencia del cliente**
**[HECHO]** El caso más ilustrativo de todo el dossier va en dirección contraria: *"The inventory co I used closed. The inventories provided using Inventory Hive also stopped working so inventories inc photos could not be opened properly at the end of the tenancy."* **[INFERENCIA]** Un informe cuya legibilidad depende de que el SaaS siga vivo es, para el cliente, una dependencia estructural inaceptable en un artefacto probatorio con vida útil de 3 a 10 años.

---

## 13. Incumbent risk

### **Nivel: ALTO, y ya materializado.** No es una amenaza futura; ya ocurrió.

| Actor | Qué ya tiene | Precio |
|---|---|---|
| **TurboTenant** (1M+ landlords) | Condition Reports con fotos, firma electrónica y participación del inquilino **sin cuenta** | **Gratis** |
| **Zillow Rental Manager** (214M usuarios/mes) | Property Condition Report: planos, ítem por ítem, 8 fotos por ítem, envío para firma. **24 estados**, con expansión y roadmap de autoservicio para el inquilino | Gratis (comercializado dentro de una suite gratuita) |
| **Buildium** | Mobile Property Inspection App **powered by HappyCo**: offline, fotos, plantillas, sync | Incluido en los 3 planes |
| **AppFolio** | Mobile Inspections nativas | Incluido |
| **Goodlord** (UK) | Módulo de inventory management con firma electrónica y gestión de check-out | Incluido |
| **TenantCloud / DoorLoop** | Inspecciones move-in/out por tier | Incluido a partir del segundo tier |
| **OpenRent** (UK) | Vende el **servicio humano** con clerk acreditado | £95 / £145 / £85 |
| **TDS (esquema de depósitos)** | No construye la app: **certifica un proveedor y lo integra en su portal de evidencias** | — |

### ¿Qué ventaja tendría un producto independiente?
**Las que la evidencia soporta [INFERENCIA]:**
- **Neutralidad entre las partes.** Ningún incumbente puede ser creíblemente neutral: Zillow y TurboTenant venden al landlord; el PMS trabaja para el gestor; el esquema de depósitos es juez, no parte. La queja P4 (*"all the power to the landlords…the tenant with no proof whatsoever"*) describe un hueco que un incumbente del lado del landlord **no tiene incentivo para cerrar**.
- **Durabilidad e independencia del proveedor.** Ningún incumbente resuelve que la prueba sobreviva al cambio de agencia (E3) o al cierre del proveedor (P5). Para ellos es *anti*-feature: el lock-in les beneficia.
- **Calidad de ejecución móvil.** Todas las quejas P1–P3 son deuda técnica. Un iOS engineer senior compite bien ahí. ⚠️ Pero eso es una ventaja de ejecución, no un foso: es copiable y no es un problema no resuelto, sino mal resuelto.

**Las que NO tendría:**
- **Distribución:** ninguna. Los tres canales institucionales británicos están ocupados, el SERP está saturado y las plataformas con el usuario ya dentro lo regalan.
- **Precio:** el suelo es £0 en EE. UU. y £10–15/mes en UK.
- **Aceptación por el árbitro:** un competidor ya está integrado en el portal de evidencias del TDS.

### ¿Puede un incumbente absorberlo trivialmente?
**[HECHO] Sí, y varios ya lo hicieron.** Es una feature, no un producto, para cualquiera que ya posea la relación con el landlord. **El dato más elocuente [HECHO]:** en **2.234 reviews de Capterra de Buildium hay UNA sola mención a inspecciones**; en **150 reviews de Landlord Studio, cero**; en 334 de Yardi Breeze, prácticamente ninguna. **[INFERENCIA]** Nadie compra un PMS por sus inspecciones — pero una vez dentro, nadie paga aparte por ellas. Ése es el mecanismo principal de muerte para un producto standalone en este espacio.

### El vector adyacente: deposit replacement
**[HECHO]** Reposit: +58% de ventas en H1 2026 (BTR +103%), 195 agentes partner, £34M de cobertura. Pero **[FUENTE — encuesta de Zero Deposit, parte interesada, sep 2026]**: si se abolieran los esquemas insured, **solo el 9% de los landlords pasaría a alternativas**; el 64% iría a custodial tradicional. **[INFERENCIA]** El depósito no desaparece en el horizonte relevante; y aunque desapareciera, el problema no cambia (el asegurador exige prueba del daño igual o más). Lo que cambiaría es **quién compra**: de millones de compradores atomizados a ~5 compradores B2B. Eso es peor para un indie, no mejor.

---

## 14. Evidence against the opportunity

La mejor evidencia encontrada para **NO** perseguir este mercado, ordenada por fuerza:

1. **[HECHO] El evento de dolor agudo ocurre en el 1% de los contratos.** 46.950 adjudicaciones formales sobre 4,71M de depósitos protegidos (Inglaterra y Gales, 12 meses a marzo 2025). El 99% de los alquileres termina sin disputa formal. Combinado con que el **45% de los landlords ingleses y el 93,4% de los propietarios españoles tienen una sola propiedad**, y con una estancia media de **4,7 años**, el comprador típico vive el evento una vez cada media década y la disputa una vez en la vida. **Nadie compra un seguro contra un siniestro que no ha tenido.**

2. **[HECHO] El precio ya está en el suelo y hay competidores gratuitos con distribución masiva.** TurboTenant (1M+ landlords) y Zillow (214M usuarios/mes) regalan la funcionalidad en EE. UU.; el suelo británico es £10–15/mes con al menos un tier gratuito; el software vertical cobra **£0,10–£3,75 por informe**. No hay espacio para entrar "más barato" ni argumento claro para entrar "más caro".

3. **[HECHO] Las quejas de los productos existentes son de ejecución, no de concepto.** Nadie dice *"esta categoría de producto no resuelve mi problema"*; dicen *"la cámara va lenta"*, *"se me cayó la app"*. Y las valoraciones agregadas son altas (zInspector 4,8–4,93; SnapInspect 5,0 con 57 de 58 reviews en 5★; RentCheck 4,8 sobre 18.000 ratings). Un entrante compite contra un problema de ingeniería resuelto a medias, no contra un hueco de mercado.

4. **[HECHO] Los canales de distribución ya están adjudicados.** TDS↔Inventory Hive con **integración en el portal de evidencias del adjudicador**; NRLA↔mydeposits/No Letting Go; el SERP de plantillas ocupado por aseguradoras, legaltechs y **el propio esquema de depósitos regalando el checklist**. Ninguna cifra de CAC — pero la estructura del canal es observable y está cerrada.

5. **[HECHO] El módulo de inspecciones es invisible en la conversación de los PMS.** Una mención en 2.234 reviews de Buildium; cero en 150 de Landlord Studio. Si los gestores sufrieran con el check-in/check-out, aparecería. No aparece.

6. **[INFERENCIA] El espacio está lleno de zombis, no de cadáveres.** Ocho o más vendors británicos activos, mantenidos durante años, con 9, 23, 29, 37 o 51 reviews. Eso describe un techo de ingresos bajo y crecimiento plano, no un mercado insatisfecho. Y **Product Hunt no registra lanzamientos con tracción** en esta categoría.

7. **[HECHO] El único caso de tracción masiva no se ganó documentando mejor.** RentCheck (18.000–20.000 ratings, 100k+ installs, $3,6M de funding) escaló **trasladando el trabajo al inquilino** — y sus quejas dominantes son exactamente eso: *"takes more than an hour"*, *"places a lot of documentation work on the tenant"*.

8. **[HECHO] Buena parte del conflicto no es probatorio, es valorativo.** Una propietaria con inventario completo de entrada y salida que *"clearly shows the damage"* acaba igualmente en arbitraje TDS, discutiendo *betterment* (repintar una pared o todas) y wear-and-tear. **Documentar mejor no toca esa mitad del problema.**

9. **[HECHO] El mercado español es estructuralmente más débil, no una oportunidad virgen.** No hay obligación legal de inventario, no hay ADR ni arbitraje de consumo entre particulares, no hay adjudicador que exija pruebas, el depósito de fianza ni siquiera es obligatorio en 7 comunidades, y el conflicto es estadísticamente invisible. Está vacío **porque la demanda es débil**, no porque nadie se haya dado cuenta.

10. **[HECHO] El Gobierno británico modela MENOS rotación tras la Renters' Rights Act, no más.** El Impact Assessment de MHCLG (nov 2024) cuantifica un beneficio de **£28/hogar/año por evitar mudanzas** y un coste de **~£1.700/agente/año** derivado de *"cambios en el número de mudanzas"*. Si la tesis fuera "la RRA multiplica los check-in/check-out", el propio regulador modela lo contrario.

11. **[HECHO] Escepticismo con el árbitro, no con la documentación.** Comentaristas del sector llaman al esquema *"a broken model"* y a los adjudicadores *"biased"*, y al menos uno relata que le rechazaron una reclamación **pese a tener prueba fotográfica**. Si el usuario cree que el árbitro está sesgado, más evidencia no le parece que aumente su probabilidad de ganar.

12. **[HECHO] La disposición a pagar ya fue destruida una vez.** *"We can all do it on an ipad now for 12 pounds wheres years ago we would be paying a company 50 plus"*. Las apps ya comoditizaron el acto; un entrante llega después de esa compresión, no antes.

---

## 15. Unknowns

Preguntas importantes que esta investigación online **no ha podido responder**:

1. **Toda la evidencia de Reddit.** Bloqueo total del entorno (WebFetch, curl, navegador integrado). r/Landlord, r/HousingUK, r/PropertyManagement y r/AusPropertyChat son probablemente la mayor concentración pública de este dolor. **Repetir esta parte desde un entorno con acceso.**
2. **Importe medio en disputa y reparto de la adjudicación en UK.** Ningún esquema lo publica. Sin esto, no se puede cuantificar cuánto dinero cambia de manos por falta de prueba.
3. **Coste medio de la reparación reclamada** en cualquier jurisdicción.
4. **El diferencial de éxito con y sin inventario fotográfico.** El TDS afirma que es *"the single most effective way to support a claim"*, pero **no existe ningún estudio que lo cuantifique**. Es la afirmación central del sector y no está medida.
5. **Efecto real de la Renters' Rights Act sobre el número de check-in/check-out.** No hay ninguna estimación, oficial ni privada, en ninguna dirección.
6. **Tamaño de la industria de inventory clerks en UK** (número de clerks activos, informes/año, facturación). La AIIC no publica censo.
7. **Número de états des lieux realizados al año en Francia**, y quién los hace (agencia, propietario, huissier). Tampoco hay tasa de rotación francesa.
8. **Volúmenes de búsqueda SEO** de los términos relevantes en cualquier idioma. El proxy bloqueó todas las herramientas de keyword data.
9. **Churn y retención.** No se encontró **ni un solo caso** de alguien que pagara por un producto de inventario digital y lo abandonara, ni ningún hilo de *"we switched from X because"*. La retención de esta categoría es una incógnita total.
10. **Estadística nacional española de fianzas** y desglose judicial de reclamaciones (el CGPJ no lo desagrega; sus ficheros llegan a 2020).
11. **Agregados de NSW Fair Trading**, que publica la **proporción del bond reembolsada a cada parte por código postal** en ficheros XLSX no extraíbles. Es la fuente más rica sin explotar del dossier.
12. **Censo de competidores locales en Francia y España.** Se identificaron nombres pero no se verificó tracción, precio real ni tamaño.
13. **Si Zillow cobra por el Property Condition Report.** La página de producto no lo menciona y el help center no lo aclara.
14. **Países Bajos y Alemania:** obligación de documentar y plazos de devolución no verificados en fuente primaria.
15. **Qué acepta realmente un adjudicador.** No se encontró ninguna confirmación de que un vídeo haya ganado un arbitraje, ni ninguna queja real de que un formato concreto fuera rechazado por un esquema.

---

## 16. Hypotheses to validate in interviews

Formuladas como afirmaciones falsables sobre el comportamiento actual, no como deseos de producto.

1. **Un landlord autogestionado con 5 o más propiedades en Reino Unido realiza al menos 3 ciclos de check-in/check-out al año y ya ha sufrido al menos una deducción disputada en los últimos 24 meses.** *(Si es falso, el único segmento con frecuencia suficiente desaparece y el escenario A de la §10 se cae.)*
2. **El propietario o la agencia decide y paga la herramienta de documentación sin aprobación de terceros, y el inquilino no interviene en esa decisión ni en ningún momento.** *(Si es falso — si el inquilino puede imponer o vetar el proceso — el comprador cambia y el canal también.)*
3. **En Reino Unido, quien hoy contrata a un inventory clerk por £95–£170 lo hace por la responsabilidad de tercero independiente, no por la calidad del documento; y no sustituiría al clerk por software propio a ningún precio.** *(Es la hipótesis que decide si la brecha de 40× entre servicio y software es capturable o es el precio de otra cosa.)*
4. **Las agencias de letting españolas no pagan hoy nada por documentar el estado de entrada y salida: lo hace el comercial con su móvil, sin herramienta, y sin coste asignado.** *(Si se confirma, el mercado español no existe al precio necesario para sostener un negocio, con independencia de que el problema sea real.)*
5. **Al menos uno de cada tres profesionales entrevistados ha perdido, no ha podido abrir o no ha podido localizar un informe de entrada cuando lo necesitó al final del contrato** (cambio de agencia, cierre del proveedor, email perdido, fotos comprimidas). *(Valida o destruye el gap de custodia/integridad, que es el más defendible que encontró esta investigación.)*
6. **Un adjudicador de TDS, DPS o mydeposits, o un abogado de arrendamientos español, ha rechazado o devaluado prueba fotográfica por falta de fecha fiable, por sospecha de alteración o por no estar firmada por ambas partes, en un caso concreto que puede describir.** *(Valida si la integridad probatoria es un problema real del árbitro o solo una preocupación de foro.)*
7. **El landlord que ya usa fotos del móvil + PDF por email no percibe su método como defectuoso y no ha cambiado de método tras perder una disputa.** *(Si se confirma, el workaround gratuito es suficientemente bueno y no hay conversión posible.)*
8. **Quien contrató un producto de este espacio y lo dejó lo hizo por precio, por fricción móvil o porque su PMS ya lo incluía** — y no por falta de la funcionalidad que sea. *(Ataca directamente la laguna nº 9 de la §15: no hay ni un dato de churn en toda la investigación.)*
9. **En Francia, el état des lieux se realiza en la práctica en más del 90% de los contratos y ya está cubierto por una herramienta o por la agencia; el propietario particular francés no busca alternativa.** *(Francia es el mercado con el trigger legal más fuerte; si ya está cubierto, el forzador legal no es una oportunidad.)*
10. **El inquilino que perdió parte de su fianza por falta de prueba estaría dispuesto a pagar de su bolsillo, antes de entrar en la vivienda, por documentar el estado — y no solo a decir que le habría gustado tenerlo.** *(Es la hipótesis de willingness-to-pay del lado que más se beneficia legalmente en España y Francia, y de la que esta investigación no encontró ni una sola evidencia de gasto real.)*

---

## 17. Sources

### Estadísticas oficiales y reguladores
| Fuente | URL | Fecha | Qué respalda |
|---|---|---|---|
| TDS Group — Statistical Briefing 2024/25 | https://www.tdsgroup.uk/statistical-briefing · [PDF](https://7fb334f1-4cb2-487c-a4bf-6cbf5bf762cb.usrfiles.com/ugd/7fb334_0e2b37ea7946459b93512a57d5904ca0.pdf) | mar 2025 | Depósitos protegidos, valor, depósito medio, nº y % de disputas, causas |
| TDS — Statistical Briefing 2023-24 | https://www.tdsgroup.uk/_files/ugd/48110f_f2e6548e7ca14d109c494d4d9792ecf1.pdf | mar 2024 | Serie temporal de disputas |
| House of Commons Library SN02121 | https://researchbriefings.files.parliament.uk/documents/SN02121/SN02121.pdf | 22 jul 2022 | Datos 2021 de la serie |
| English Private Landlord Survey 2024 | https://www.gov.uk/government/statistics/english-private-landlord-survey-2024-main-report/english-private-landlord-survey-2024-main-report | 5 dic 2024 | 59/22/15% de devolución; 80% hace inventario; distribución de cartera |
| English Housing Survey 2024-25 | https://www.gov.uk/government/statistics/english-housing-survey-2024-to-2025-private-rented-sector-pre-renters-rights-act-overview/english-housing-survey-2024-to-2025-private-rented-sector-pre-renters-rights-act-overview | 2025 | 4,7M hogares PRS; estancia media 4,7 años |
| ONS — Private rented sector statistics 2025 | https://www.ons.gov.uk/peoplepopulationandcommunity/housing/articles/privaterentedsectorstatisticsfromacrosstheuk/2025 | 25 sep 2025 | 19% de hogares en PRS |
| Gobierno de Escocia — FOI 202500459983 | https://www.gov.scot/publications/foi-202500459983/ | 2025 | 267.227 depósitos / 98.220 devoluciones → rotación 36,8% |
| Renters' Rights Bill Impact Assessment (MHCLG) | https://assets.publishing.service.gov.uk/media/67405a2353373262c0d825c5/Renters__Rights_Bill_Impact_assessment.pdf | nov 2024 | El Gobierno modela MENOS mudanzas, no más |
| GOV.UK — Guide to the Renters' Rights Act | https://www.gov.uk/government/publications/guide-to-the-renters-rights-act/guide-to-the-renters-rights-act | 2025-26 | Calendario; sin cambios en depósitos |
| Gowling WLG — countdown a 1 may 2026 | https://gowlingwlg.com/en/insights-resources/articles/2025/renters-rights-act-2025-the-countdown-to-1-may-2026-begins | 2025 | Fechas de entrada en vigor |
| U.S. Census — Housing Vacancy Survey Q2 2026 | https://www.census.gov/housing/hvs/files/currenthvspress.pdf | 28 jul 2026 | 46,83M hogares en alquiler |
| U.S. Census — Rental Housing Finance Survey 2021 | https://www.census.gov/content/dam/Census/library/visualizations/2021/econ/2021-RHFS-Infographic-tagged.pdf | 2021 | Distribución de propiedades 1-4 unidades |
| RTBA Victoria — Annual Report 2024-25 | https://www.consumer.vic.gov.au/library/publications/about-us/rtba/rtba-annual-report-202425.pdf | jun 2025 | 736.352 bonds; 65/25/10%; 96% de acuerdo |
| RTA 1997 (Vic) s.35 | https://www5.austlii.edu.au/au/legis/vic/consol_act/rta1997207/s35.html | — | Condition report obligatoria; 25 penalty units |
| RTA 2010 (NSW) s.29 | https://www5.austlii.edu.au/au/legis/nsw/consol_act/rta2010207/s29.html | — | Condition report obligatoria; 7 días; 20 penalty units |
| NSW — rental bond data | https://www.nsw.gov.au/housing-and-construction/rental-forms-surveys-and-data/rental-bond-data | ago 2026 | Fuente sin explotar (XLSX) |
| Tenancy Services NZ — data & statistics | https://www.tenancy.govt.nz/about-tenancy-services/data-and-statistics/ | Q2 2026 | "Refund bond" en 43,26% de solicitudes |
| RTB Ireland — Annual Report 2024 | https://rtb.ie/wp-content/uploads/2025/09/2024-RTB-Annual-Report-and-Accounts.pdf | sep 2025 | 9.564 disputas; 19% por fianza |
| Banco de España — DO 2432 | https://www.bde.es/f/webbe/SES/Secciones/Publicaciones/PublicacionesSeriadas/DocumentosOcasionales/24/Fich/do2432.pdf | 2024 | 3,6M viviendas en alquiler; rotación 30-40% |
| MIVAU — depósito de fianzas por CCAA | https://www.mivau.gob.es/vivienda/alquila-bien-es-tu-derecho/alquiler/deposito-de-fianzas | 2026 | Qué CCAA exigen depósito |
| INSEE Focus nº 359 — Parc de logements 2025 | https://www.insee.fr/fr/statistiques/8640662 | 17 sep 2025 | 22,8% de residencias principales en alquiler privado |
| Légifrance — Décret 2014-890 | https://www.legifrance.gouv.fr/loda/id/JORFTEXT000029337625 | 1 ago 2014 | Tope de 3 €/m² TTC |
| DGCCRF — facturation des états des lieux | https://www.economie.gouv.fr/dgccrf/les-fiches-pratiques/location-facturation-des-etats-des-lieux | — | El propietario paga al menos lo mismo que el inquilino |
| Service-Public — état des lieux | https://www.service-public.gouv.fr/particuliers/vosdroits/F31270 | — | Obligatoriedad; presunción art. 1731 CC y su excepción |
| ANIL — coût du constat par huissier | https://www.anil.org/aj-cout-constat-des-lieux-etabli-par-huissier-de-justice/ | 2021 | 158,58–256,89 € TTC |
| HMRC — Property Rental Income Statistics | https://gov.uk/government/statistics/property-rental-income-statistics/property-rental-income-statistics-2024 | sep 2025 | 2,86M landlords no incorporados |

### Legislación y jurisprudencia
| Fuente | URL | Qué respalda |
|---|---|---|
| LAU art. 36 (BOE-A-1994-26003) | https://ley-de-arrendamientos-urbanos.com.es/articulo-36-ley-arrendamientos-urbanos-fianza/ | Fianza de 1 mensualidad; interés legal tras un mes |
| SAP Barcelona 39/2026 (comentario E&J) | https://www.economistjurist.es/actualidad-juridica/jurisprudencia/sin-inventario-sin-fotografias-y-sin-avisar-de-los-desperfectos-la-audiencia-de-barcelona-recuerda-como-se-gana-o-se-pierde-un-pleito-entre-propietario-e-inquilino/ | Sentencia decidida por falta de inventario y fotos |
| Idealista — pruebas para reclamar desperfectos | https://www.idealista.com/news/inmobiliario/vivienda/2026/08/20/908816-las-pruebas-que-pueden-marcar-la-diferencia-al-reclamar-por-desperfectos-tras-el | 20 ago 2026; SAP Barcelona 10 mar 2026; inventario no obligatorio |
| Consumo Responde — reclamaciones de alquiler | https://www.consumoresponde.es/artículos/reclamaciones_en_materia_de_alquiler_de_viviendas | No hay arbitraje de consumo entre particulares |
| MA c.186 §15B | https://malegislature.gov/Laws/GeneralLaws/PartII/TitleI/Chapter186/Section15B | Statement de condición; daños 3× |
| MI MCL 554.608 | https://law.justia.com/codes/michigan/chapter-554/act-348-of-1972/section-554-608/ | Inventory checklist obligatorio, 7 días |
| WA RCW 59.18.260 | https://app.leg.wa.gov/RCW/default.aspx?cite=59.18.260 | Checklist firmado; responsabilidad por el depósito íntegro |
| KY KRS 383.580 | https://law.justia.com/codes/kentucky/chapter-383/section-383-580/ | Listado inicial y final; forfeiture total |
| GA OCGA 44-7-33 | https://law.justia.com/codes/georgia/title-44/chapter-7/article-2/section-44-7-33/ | Lista de daños; ámbito limitado (>10 unidades) |
| MT MCA 70-25-206 | https://law.justia.com/codes/montana/title-70/chapter-25/part-2/section-70-25-206/ | Inversión de la carga de la prueba |
| AZ ARS 33-1321 | https://www.azleg.gov/ars/33/01321.htm | Move-in form; daños dobles |
| KS KSA 58-2548 | https://ksrevisor.gov/statutes/chapters/ch58/058_025_0048.html | Inventario conjunto en 5 días |
| NV NRS 118A.200 | https://law.justia.com/codes/nevada/chapter-118a/statute-118a-200/ | Record de inventario en el contrato |
| WI — guía DATCP (ATCP 134.06) | https://datcp.wi.gov/Documents/LT-LandlordTenantGuide497.pdf | 7 días para inspeccionar; daños dobles |
| MD RP §8-203.1 | https://law.justia.com/codes/maryland/real-property/title-8/subtitle-2/section-8-203-1/ | Derecho a inspección a petición; 3× |

### Evidencia cualitativa (foros y comunidades)
| Fuente | URL | Fecha | Evidencia |
|---|---|---|---|
| MoneySavingExpert | https://forums.moneysavingexpert.com/discussion/6320840/landlord-withholding-deposit-inventory-not-signed | 18 dic 2021 | E1 |
| MoneySavingExpert | https://forums.moneysavingexpert.com/discussion/6236107/rental-deposit-and-no-inventory | 27 ene 2021 | E2 |
| MoneySavingExpert | https://forums.moneysavingexpert.com/discussion/6497386/reclaiming-deposit-with-change-of-agents-and-missing-inventory | 9 ene 2024 | E3 |
| MoneySavingExpert | https://forums.moneysavingexpert.com/discussion/6129206/check-out-report-does-not-match-inventory | 14 abr 2020 | E4 |
| MoneySavingExpert | https://forums.moneysavingexpert.com/discussion/6019116/missing-inventory-or-check-in-check-out-for-dispute-with-tds | 28 jun 2019 | E6 |
| MoneySavingExpert | https://forums.moneysavingexpert.com/discussion/6377965/landlord-adding-items-after-checkout-inventory-completed | ago 2022 | E9 |
| OpenRent Community | https://community.openrent.co.uk/t/openrent-made-it-difficult-to-dispute-landlords-claims-against-deposit/91494 | sep 2026 | E5 |
| OpenRent Community | https://community.openrent.co.uk/t/diy-inventory-recommendations/83574 | jun 2025 | Workflow actual (§3) |
| OpenRent Community | https://community.openrent.co.uk/t/inventory-video/61968 (y `?page=2`) | mar 2024 | Debate sobre inmutabilidad; evidencia contraria C2/C3 |
| OpenRent Community | https://community.openrent.co.uk/t/inventory-report-and-claiming-from-deposit/45099 | 2023 | E10 |
| OpenRent Community | https://community.openrent.co.uk/t/openrents-inventory-small-pictures-and-not-fit-for-purpose/46896 | 2023 | E11 |
| OpenRent Community | https://community.openrent.co.uk/t/deposit-dispute-what-can-we-claim-for/87912 | dic 2025 | Documentar bien no evita la disputa |
| BiggerPockets | https://www.biggerpockets.com/forums/52/topics/747091-property-manager-did-not-keep-records-security-deposit-issues | ago 2019 | E7 |
| BiggerPockets | https://www.biggerpockets.com/forums/52/topics/127917-move-in-inspection-checklist---streamlining-the-process-what-do-you-do | 2014-15 | Workflow manual US |
| PropertyChat AU | https://www.propertychat.com.au/community/threads/ingoing-report-advice-needed-in-nsw.30712/ | abr 2018 | E8 |
| PropertyChat AU | https://www.propertychat.com.au/community/threads/condition-report.38889/ | may 2019 | Hueco declarado por un PM |
| Property Industry Eye | https://propertyindustryeye.com/deposit-dispute-agents-vague-check-in-report-lacked-enough-evidence-to-help-landlord/ | 30 ene 2020 | E12; escepticismo con el adjudicador |
| idealista foro | https://www.idealista.com/news/foro/alquiler/816389-alguien-mas-ha-tenido-que-enfrentar-que-la-agencia-rent2be-malaga-te-robe-no-te-devuleva-la-fianza | 2024 | E14 |
| idealista foro | https://www.idealista.com/news/foro/alquiler/546737-no-nos-devuelven-la-fianza-por-una-humedad-en-una-habitacion-que-podemos-hacer | nov 2012 | Patrón antiguo (€1.700) |
| UK Business Forums | https://www.ukbusinessforums.co.uk/threads/property-services-inventory-clerk-business.302623/ | 2013-18 | Comoditización del clerk por el iPad |
| Property118 | https://www.property118.com/landlord-able-provide-inventory-deposit-withheld-pi-given/ | abr 2014 | Caso real de inventario inexistente |
| Property118 ⚠️ **ficción** | https://www.property118.com/landlord-lessons-inventory-nightmare/ | 30 oct 2025 | **Falso positivo — no usar** |

### Competencia, precios y reviews
| Fuente | URL | Qué respalda |
|---|---|---|
| Inventory Hive — pricing | https://www.inventoryhive.co.uk/pricing | £300/año o £30/mes |
| InventoryBase — pricing | https://inventorybase.co.uk/pricing/ | £35/mes; 20p/prop extra |
| Imfuna Let — pricing | https://www.imfuna.com/let-uk/pricing/ | £35/£60/£85 mes |
| Property Inspect | https://propertyinspect.com/uk/ | £45–£245/mes |
| Kaptur | https://kaptursoftware.co.uk/pricing-property-inventory-and-reporting-software/ | £45/£75/£150 mes |
| RentCheck — pricing | https://www.getrentcheck.com/plan-pricing | $1–$1,75/unidad/mes |
| Chapps — pricelist | https://www.chapps.com/pricelist/rental-inspector-app/ | €7,50/informe o €260/user/año |
| Smarter Inventories | https://smarterinventories.com/plans.aspx | £2,33–£3,75/informe |
| Inventorai | https://inventorai.co.uk/ | £25/mes + 20p/propiedad |
| Acta Entrega 🇪🇸 | https://actaentrega.com/guias/como-hacer-acta-entrega-alquiler | €9 por PDF |
| ThePropertyAI — comparativa 2026 | https://thepropertyai.co.uk/property-news/inventory-hive-alternatives-in-2026-7-top-uk-property-inventory-tools | Censo de ≥8 vendors UK y su suelo de precio |
| Buildium — pricing / inspections | https://www.buildium.com/pricing/ · https://www.buildium.com/features/mobile-property-inspection-app/ | Inspecciones powered by HappyCo |
| DoorLoop / TenantCloud / Landlord Studio | https://www.doorloop.com/pricing · https://www.tenantcloud.com/pricing · https://www.landlordstudio.com/pricing | Inspecciones por tier |
| TurboTenant — Condition Reports | https://www.turbotenant.com/condition-reports/ · https://support.turbotenant.com/en/articles/9160431-condition-reports-for-landlords | **Gratis**, con firma y sin cuenta para el inquilino |
| TurboTenant — 1M landlords | https://finance.yahoo.com/news/turbotenant-surpasses-1-million-landlords-140000806.html | 24 feb 2026 |
| Zillow — Property Condition Report | https://help.zillowrentalmanager.com/hc/en-us/articles/20445146080787-Common-questions-about-the-property-condition-report | 24 estados; 8 fotos/ítem |
| Goodlord — plataforma | https://www.goodlord.com/platform | Inventory management con firma |
| OpenRent — inventory services | https://www.openrent.co.uk/landlord-inventory-and-check-in-services | £95 / £145 / £85 |
| InventoryFlex — tarifas | https://inventoryflex.co.uk/pricing | £110–£170 |
| AIIC — guía de precios | https://theaiic.co.uk/blog/2024/10/how-should-i-price-my-inventory-reports/ | £230 (3 dorm., inv.+check-in) |
| Inventory Hive — Trustpilot | https://uk.trustpilot.com/review/inventoryhive.co.uk | P4, P5 |
| Inventory Hive — App Store / Play | https://apps.apple.com/gb/app/inventory-hive/id1096620891 · https://play.google.com/store/apps/details?id=uk.co.inventoryhive | P1, P3, P6 |
| InventoryBase — Play / Capterra | https://play.google.com/store/apps/details?id=com.radweb.ib · https://www.capterra.com/p/146502/InventoryBase/reviews/ | P1, P7, P8, P9, P10 |
| Imfuna — Trustpilot / Capterra | https://www.trustpilot.com/review/imfuna.com · https://www.capterra.com/p/171900/Imfuna-Rent/reviews/ | P1, P2, P3 |
| RentCheck — Trustpilot / App Store / Play | https://ca.trustpilot.com/review/getrentcheck.com · https://apps.apple.com/us/app/rentcheck/id1134017691 · https://play.google.com/store/apps/details?id=com.rentcheck.app | P1, P2, P4, P7, P8 |
| HappyCo — Capterra / Software Advice | https://www.capterra.com/p/145455/Inspector/reviews/ · https://www.softwareadvice.com/inspection/happyco-profile/reviews/ | P3, P8, P10, P11 |
| zInspector — Capterra / Play | https://www.capterra.com/p/176250/zInspector/reviews/ · https://play.google.com/store/apps/details?id=com.zinspector3 | P9, P12 |
| SnapInspect — Capterra / Software Advice | https://www.capterra.com/p/151590/SnapInspect/reviews/ · https://www.softwareadvice.com/inspection/snapinspect-profile/reviews/ | P2, P6; 5,0 con 58 reviews |
| AppFolio — Capterra / reviews negativas | https://www.capterra.com/p/92228/AppFolio-Property-Manager/reviews/ · https://appsupports.co/1057763031/appfolio-property-manager/negative-reviews | P1, P2, P5, P6, P10 |
| Buildium / Yardi Breeze / Landlord Studio — Capterra | https://www.capterra.com/p/47428/Buildium-Property-Management-Software/reviews/ · https://www.capterra.com/p/164741/Yardi-Breeze/reviews/ · https://www.capterra.com/p/182473/Landlord-Studio/reviews/ | 1 mención de inspecciones en 2.234 reviews; 0 en 150 |
| HappyCo — mínimo de 500 unidades | https://rapideyeinspections.com/blog/happyco-inspections-review/ | ⚠️ fuente vendor |
| HTF Market Intelligence ⚠️ | https://www.htfmarketintelligence.com/report/global-property-inspection-software-market | Informe de mercado **no utilizable** (vendors mal clasificados) |

### Mercado, distribución y actores
| Fuente | URL | Qué respalda |
|---|---|---|
| NRLA — "What 2025 taught us about deposit disputes" | https://www.nrla.org.uk/news/what-2025-taught-us-about-deposit-disputes | 1% de adjudicación; causas; cita del equipo del TDS |
| NRLA — crítica del Impact Assessment | https://www.nrla.org.uk/news/renters-rights-impact-assessments-will-figures-add-up | Menos rotación esperada |
| NRLA — guía de inventario (checklist de mydeposits) | https://www.nrla.org.uk/news/complete-guide-to-inventory-for-landlords | Canal institucional ocupado |
| TDS ↔ Inventory Hive | https://www.tenancydepositscheme.com/newsstory-the-dispute-service-and-inventory-hive-announce-joint-working-plans/ · https://www.tenancydepositscheme.com/newsstory-inventory-hive-360-image-feature-integrates-with-tds-deposit-dispute-portal/ | Integración en el portal de evidencias del adjudicador |
| TDS — plazos de adjudicación | https://www.tenancydepositscheme.com/how-long-adjudication/ | ~28 días |
| The Negotiator — datos de mydeposits | https://thenegotiator.co.uk/news/rental-market/80-to-90-of-tenants-get-their-rental-deposit-back-claims-new-data/ | ⚠️ métrica "todo o parte" |
| Generation Rent — encuesta | https://www.generationrent.org/2025/04/07/one-in-four-renters-struggles-to-retrieve-full-deposit-after-tenancy/ | ⚠️ muestra autoseleccionada |
| Zillow Consumer Housing Trends 2024 / 2025 | https://www.zillow.com/research/renters-housing-trends-report-2024-34387/ · https://www.zillow.com/research/renters-housing-trends-report-2025-35647/ | 40% íntegro / 24% nada; fianza mediana |
| Shelterforce — desmontaje de los $45 bn | http://shelterforce.org/2020/12/10/security-deposit-alternatives-the-misleading-marketing-of-renters-choice/ | La cifra es marketing de Rhino |
| OCU — nota de prensa | https://www.ocu.org/organizacion/prensa/notas-de-prensa/2025/fincontratoalquiler031025 | 3 oct 2025; 13% de conflictos por fianza |
| Público — fianzas del INCASÒL | https://www.publico.es/sociedad/gran-interrogante-incasol-cientos-millones-fianzas-decada-practicamente-construir-vivienda-publica.html | jul 2026; >2.000 M€ |
| Idealista — INE ECV 2024 | https://www.idealista.com/news/inmobiliario/vivienda/2025/02/17/832437-las-viviendas-en-alquiler-ya-suponen-mas-del-20-de-los-hogares-en-espana | 20,4% de hogares en alquiler |
| Observatorio del Alquiler — perfil del propietario | https://observatoriodelalquiler.org/perfil-del-propietario-de-viviendas-en-alquiler-en-espana | 93,4% con un solo inmueble adicional |
| eInforma — CNAE 6831 | https://www.einforma.com/informes-sectoriales/cnae-6831-empresas-servicios-de-intermediacion-para-actividades-inmobiliarias | 35.870 empresas |
| IBISWorld — residential property managers US | https://www.ibisworld.com/united-states/number-of-businesses/residential-property-managers/6136/ | 245.484 empresas |
| NARPM | https://www.narpm.org/about/ | >6.000 miembros |
| BiggerPockets — about | https://www.biggerpockets.com/about-us | 3M+ miembros |
| Propertymark — membresía | https://propertyindustryeye.com/propertymark-sees-significant-revenue-rise-as-membership-18700-agents/ | 18.711 miembros (jun 2025) |
| PropertyWire — Reposit H1 2026 | https://www.propertywire.com/company-news/deposit-replacement-firm-reports-58-sales-rise-in-h1-2026/ | +58% de ventas |
| The Intermediary — encuesta Zero Deposit | https://theintermediary.co.uk/2026/09/only-9-of-landlords-would-switch-to-deposit-alternatives-if-insured-schemes-were-abolished-zero-deposit/ | ⚠️ solo 9% cambiaría |
| Journal de l'Agence — homePad ⚠️ | https://www.journaldelagence.com/1120985-avec-homepad-letat-des-lieux-devient-complet-et-plus-fiable | ⚠️ cifras del vendor, 2016 |
| Immopad / Nockee (comparativas FR) | https://immopad.com/ · https://www.nockee.fr/blog/logiciel-etat-des-lieux | ≥6 proveedores franceses |

### Cifras identificadas como marketing y descartadas como hecho
| Cifra | Emisor | Por qué se descarta |
|---|---|---|
| "$45 mil millones retenidos en fianzas en EE. UU." | Rhino (2019), reatribuida a Roost | Vende el sustitutivo de la fianza; sin metodología publicada |
| "90% de los inquilinos recupera todo o parte" | mydeposits | Operador del esquema; "todo o parte" está diseñado para parecer favorable |
| "130.000 états des lieux/año", "70% de ahorro de tiempo", "99% de retención" | homePad (2016) | Declaraciones del director de marketing; 10 años de antigüedad |
| "59% no espera reembolso íntegro", "40% impugna cargos" | Roost | Vendor cuyo producto resuelve lo que la encuesta describe |
| "23 estados con requisito de checklist" | RapidEye Inspections | Mezcla "puedes" con "debes"; el recuento verificado es 11 |
| "evita el 80% de las discusiones por la fianza" | Acta Entrega | Claim de marketing sin respaldo |
| "56% recuperó la fianza íntegra" | Generation Rent | Muestra autoseleccionada de 1.375 simpatizantes |
| "13% problemas con la fianza" | OCU | Base de consultas recibidas, no muestra poblacional |
| $1,2B → $2,6B "property inspection software market" | HTF Market Intelligence | Lista como vendors a empresas de otros sectores |

Investigado por: Claude