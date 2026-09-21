# Facturas de proveedores que no coinciden con lo recibido

## Problema canónico

Pequeños negocios pagan facturas de proveedores sin comprobar sistemáticamente si los productos, cantidades y precios facturados coinciden con lo realmente pedido y recibido.

## Research

# Discrepancias en Facturas de Proveedores (Three-Way Matching)

## 1. Executive summary

El problema de pagar por productos no recibidos o con precios incorrectos es estructural y muy doloroso en pequeñas empresas (especialmente hostelería, retail, logística y construcción). Conocido en finanzas como "Three-Way Matching" (cruzar orden de compra, albarán de entrega y factura), en el segmento SMB suele degradarse a un proceso manual caótico en Excel o simplemente se ignora asumiendo las pérdidas. Existe una clara disposición a pagar por herramientas verticales (como MarginEdge), pero estas suelen ser costosas y estar sobrecargadas de funciones. La oportunidad para un producto independiente radica en resolver exclusivamente el cruce de datos no estructurados (fotos de albaranes con correcciones a mano vs. PDFs de facturas) sin requerir un ERP ni órdenes de compra formales, aunque el mayor riesgo es la adopción del hábito de capturar el albarán por parte de los operarios.

## 2. Problem evidence

La frustración con este proceso está documentada por usuarios que recurren a flujos de trabajo muy ineficientes:

* **El caos manual:** "I run my own company, and I collect supplier invoices as PDFs... I do this manually with spreadsheets and sticky notes, and it's [hell]" (Usuario en foro de API Pulse, Enero 2026).
* **El tiempo invertido y la solución "casera":** Un administrador financiero describe su flujo antes de programar un script en Python: "The original hell was opening these one by one by hand and copying and pasting them. [...] It feels unbelievable that you used to spend 3 hours looking at everything" (Blog Note.com, Junio 2026).
* **Petición a software existente:** "We had this at MYOB and it... I do this manually and it takes too much time, please add this [to Xero]" (Foro de ideas de Xero, 2023).
* **La evaluación de riesgo vs. esfuerzo:** Un usuario en r/business explica por qué muchos no lo hacen: "If the EV [Expected Value] of the risk is lower than the overhead, you may find the 2-way match worthwhile. By not requiring the receiving match, you've reduced overhead at the cost of some risk" (Reddit, 2019).

## 3. Current workflow

Actualmente, el flujo de trabajo (workflow) en una pequeña empresa es profundamente ineficiente (el clásico *ugly workflow*):

1. **Recepción:** El camión llega. Un empleado (cocinero, jefe de obra, dependiente) recibe la mercancía junto con un albarán de papel (delivery note). Tacha con bolígrafo lo que falta, firma, y deja el papel arrugado en un cajón, pinchado en un clavo o le hace una foto por WhatsApp al dueño.
2. **Facturación:** Días o semanas después, el proveedor envía un PDF con la factura consolidada al email del dueño o de administración.
3. **Conciliación (o la falta de ella):**
* *La vía exhaustiva (Cara en tiempo):* El administrativo imprime la factura, busca los albaranes de papel y comprueba línea por línea con un marcador. O exporta a Excel y usa `VLOOKUP`/`XLOOKUP` para cruzar datos.
* *La vía de la resignación (Cara en dinero):* Si la factura "parece correcta" a simple vista, se envía a contabilidad para su pago. Se asume que el proveedor es honesto y que los errores ocasionales son un "coste de hacer negocios".



Los usuarios mantienen este workaround porque el software que automatiza esto requiere la emisión previa de Órdenes de Compra (Purchase Orders) formales, algo que las pequeñas empresas no hacen (suelen pedir por WhatsApp o teléfono).

## 4. Trigger and frequency

* **Trigger externo:** La llegada de la factura del proveedor (generalmente por email a final de mes o semana) desencadena la necesidad de reconciliación.
* **Frecuencia:** Muy alta. Múltiples veces por semana dependiendo del número de proveedores (especialmente en restaurantes donde los productos frescos se entregan a diario).
* **Disciplina requerida (Fricción):** El usuario *necesita* mantener una disciplina estricta en el paso anterior (capturar el albarán en el momento de la descarga). Si el empleado no guarda el albarán, la factura no se puede comprobar cuando llega semanas después. Esto penaliza la adopción.

## 5. Economic impact

El impacto económico es directo, medible y afecta directamente al margen de beneficio:

* **Frecuencia de error:** Las auditorías internas en sectores como logística muestran que las facturas no coinciden con lo acordado entre un 8% y un 12% de las veces.
* **Pagos duplicados:** Se estima que los pagos duplicados representan entre el 0.5% y el 2% del gasto total en empresas sin sistemas automatizados de matching.
* **Fuga de márgenes (Margin Leakage):** Cargos adicionales no autorizados (fees, embalajes), precios no actualizados o artículos cobrados pero no entregados. Un error de 75$ en un albarán que pasa desapercibido es pérdida pura de margen.
* **Costes administrativos:** Horas de personal dedicadas exclusivamente a puntear albaranes contra facturas.

## 6. Buyer and willingness to pay

* **Quién sufre el problema:** El propietario (pierde margen) y el administrativo/contable (pierde horas en trabajo robótico).
* **Quién compra:** El propietario o el director financiero (CFO fraccional).
* **Evidencia de gasto:** Las empresas ya están pagando por software vertical de gestión de restaurantes (MarginEdge cuesta ~300$/mes), software de cuentas por pagar (Procurify cuesta miles de dólares) y herramientas de extracción OCR básicas (Dext, Hubdoc por 20$-50$/mes). Además, pagan tarifas por hora a contables externos (bookkeepers) para que resuelvan este caos a mano. La disposición a pagar es muy alta porque el ROI es evidente: descubrir una factura inflada paga el software de todo el año.

## 7. Existing market

* **Procurify:** Target: Mid-market / Enterprise. Propuesta: Procure-to-pay completo. Debilidad: Requiere flujos rígidos de Purchase Orders.
* **MarginEdge / xtraCHEF (Toast) / Ottimate:** Target: Restaurantes. Pricing: ~250$-400$/mes. Fortalezas: Integración profunda con POS, cálculo de escandallos (recipe costing). Debilidades: Excesivamente caros y complejos si solo buscas reconciliar facturas; inútiles fuera de la hostelería.
* **Dext Prepare / Hubdoc:** Target: SMBs generales. Pricing: ~25$-50$/mes. Fortalezas: Excelentes en extracción OCR para contabilidad. Debilidades: Solo hacen 2-way match (Factura a Contabilidad). *No* cruzan líneas de factura contra albaranes de entrega.
* **Parseur:** Target: Operaciones de cadena de suministro / Developers. Pricing: Basado en volumen. Propuesta: Extrae datos de PDFs y los manda vía webhook a un ERP.

## 8. Negative reviews and market gaps

Patrones de insatisfacción en las soluciones actuales:

* **Exceso de funcionalidades (Bloatware):** Para conseguir el "matching" automático en hostelería, el usuario es forzado a contratar módulos enteros de inventario y escandallos de recetas que requieren meses de configuración.
* **Falta de tolerancia a la informalidad:** El software empresarial exige que haya una Orden de Compra (PO) en el sistema. Los negocios pequeños piden por WhatsApp, por lo que el PO no existe digitalmente, haciendo que el 3-way matching de los grandes ERPs fracase.
* **Manejo de excepciones manuscritas:** La mayoría de OCRs fallan miserablemente cuando el repartidor tacha un "10" y escribe un "8" a bolígrafo en el albarán manchado de aceite.
* **Onboarding agotador:** Obligan al cliente a mapear manualmente el catálogo de artículos del proveedor con sus códigos internos antes de poder usar la herramienta.

## 9. Distribution

* **Asesores y Bookkeepers (B2B2B):** Los contables externos odian perseguir a los clientes para que les expliquen discrepancias. Un programa de referidos o versión "Accountant" es el canal más potente.
* **App Stores de Ecosistemas:** Xero App Store, QuickBooks App Store. Los usuarios buscan allí "invoice automation" o "AP automation".
* **Comunidades:** Subreddits como `r/restaurantowners`, `r/smallbusiness`, `r/Bookkeeping`, `r/freightbrokers`.
* **SEO:** Búsquedas long-tail enfocadas en el dolor de la conciliación manual: "how to match delivery notes to invoices", "supplier overcharge software", "automate three way matching excel".
* **Viabilidad de adquisición:** El CAC mediante SEO y partnerships con contables es muy viable y escalable para un equipo pequeño.

## 10. Market size

* **Orden de magnitud:** Cientos de miles a millones de negocios globalmente.
* **Desglose:** Cualquier negocio físico que compre inventario y reciba albaranes y facturas por separado (hostelería, retail, talleres, construcción, pequeñas manufacturas, logística).
* **Accesibilidad indie:** El mercado accesible (negocios ya digitalizados que usan software de contabilidad en la nube pero sufren con los albaranes) está en el rango de los cientos de miles. Un pequeño negocio SaaS B2B rentable solo necesita capturar entre 300 y 1.000 clientes pagando ~50$-99$/mes para ser financieramente independiente y altamente rentable.

## 11. Global portability

* **Alta.**
* *Explicación:* El problema subyacente es universal ("Cantidad pedida = Cantidad recibida = Cantidad facturada"). Aunque las normativas fiscales (IVA, Sales Tax) y la facturación electrónica cambien por país, el acto de verificar *qué* te están cobrando a nivel de línea de artículo frente a lo que entró por la puerta es agnóstico a la regulación. Solo requiere adaptar los modelos de IA/OCR a distintos idiomas y formatos de moneda.

## 12. External dependencies

* **Modelos de Visión Artificial / LLMs (Dependencia Crítica):** El producto depende absolutamente de la capacidad de APIs externas (como OpenAI GPT-4o, Google Document AI, AWS Textract) para leer albaranes arrugados y con correcciones a mano. Si los costes de inferencia suben o la fiabilidad baja, el producto muere.
* **APIs de Contabilidad (Integración Conveniente):** Xero, QuickBooks. No son estrictamente necesarias para realizar el "matching" y alertar al usuario de la discrepancia, pero son obligatorias para completar el flujo de trabajo (exportar la factura aprobada).

## 13. Incumbent risk

* **Alto / Medio.**
* *El riesgo:* Plataformas que ya poseen el flujo de entrada de facturas (Hubdoc de Xero, Dext) podrían decidir implementar el cruce contra albaranes. Los gigantes verticales de POS (Square, Toast) siguen comprando startups del sector (Toast adquirió xtraCHEF).
* *La defensa:* Los incumbentes se centran en la conciliación bancaria y la extracción de totales para los impuestos. Extraer líneas de detalle de fotos de albaranes sucios y aplicar lógicas difusas de coincidencia de nombres de artículos es un problema de UX y de IA que las grandes plataformas contables suelen evitar por ser un "borde irregular" (edge case masivo).

## 14. Evidence against the opportunity

La razón principal para **NO** perseguir este mercado es el *comportamiento humano in situ*. El sistema requiere que el empleado (que muchas veces tiene prisa, frío en un muelle de carga, o las manos manchadas) se acuerde de fotografiar el albarán en el momento en que se entrega la mercancía.
Si el albarán se pierde antes de ser digitalizado, el software no tiene contra qué comparar la factura, volviéndose inútil. Muchas empresas toleran el margen de pérdida (overcharging) porque la alternativa implica disciplinar a empleados de baja cualificación/alta rotación para que usen una app, lo cual consideran una batalla perdida.

## 15. Unknowns

* ¿Con qué precisión real pueden los modelos Vision actuales leer correcciones manuscritas (tachones) en albaranes impresos con mala calidad?
* ¿Qué porcentaje de proveedores pequeños sigue entregando notas de entrega únicamente a mano y sin identificadores (SKUs) claros?
* ¿Están dispuestos los dueños de negocios a usar una herramienta *standalone* (independiente) solo para matching, o exigen que esté dentro de su sistema de control de stock?

## 16. Hypotheses to validate in interviews

1. Los dueños de pequeños negocios asumen un porcentaje mensual de pérdida por errores de proveedores porque verificar a mano les cuesta más tiempo que el dinero recuperado.
2. Más del 50% de los pedidos de reposición en pequeñas empresas se hacen sin una Orden de Compra (PO) formal (ej. por WhatsApp o teléfono).
3. Los empleados de recepción (cocina, almacén) pierden, manchan o archivan mal el albarán físico en al menos el 15% de las entregas antes de que llegue a administración.
4. Los contables y bookkeepers externos no pueden auditar discrepancias porque no tienen acceso a los albaranes físicos de sus clientes, solo a la factura final.
5. El principal motivo por el que los usuarios rechazan herramientas como MarginEdge es que les obligan a configurar módulos de inventario y recetas que no necesitan, solo para poder validar facturas.
6. La persona que autoriza el pago de la factura es diferente a la persona que recibe la mercancía, lo que genera un cuello de botella de comunicación por WhatsApp/papel.

## 17. Sources

* **Purchase Order Receiving Software - Procurify**: [https://www.procurify.com/procure-to-pay/procurement/receiving-inventory/](https://www.procurify.com/procure-to-pay/procurement/receiving-inventory/?utm_source=gemini) - *Respalda la definición del problema (3-way match) y la existencia de soluciones enterprise pesadas.*
* **Automotive Supply Chain Software Is Only As Fast As Its Slowest PDF**: Parseur, 08/09/2026. [https://parseur.com/blog/optimizing-automotive-supply-chain](https://parseur.com/blog/optimizing-automotive-supply-chain?utm_source=gemini) - *Respalda cómo el long-tail de pequeños proveedores genera un caos de PDFs y keying manual, causando discrepancias y capital inmovilizado.*
* **Invoice vs. PO: Differences, Matching Process & Mismatch Causes**: SourceDay, 26/03/2026. [https://sourceday.com/blog/invoice-vs-purchase-order/](https://sourceday.com/blog/invoice-vs-purchase-order/?utm_source=gemini) - *Respalda que las discrepancias no son aleatorias, sino fallos en el proceso de actualización del PO frente a la realidad de la entrega.*
* **Freight Invoice Reconciliation Process: Checklist & Steps**: Laneproof, 16/03/2026. [https://www.laneproof.com/blog/freight-invoice-reconciliation-process](https://www.laneproof.com/blog/freight-invoice-reconciliation-process?utm_source=gemini) - *Respalda cifras concretas: los invoices no coinciden el 8-12% de las veces, y las facturas duplicadas suman 0.5-2% del gasto.*
* **The Complete Procedure to Automate Invoice Reconciliation from 3**: Blog personal en Note.com, 17/06/2026. [https://note.com/tender_clam9623/n/n26e9378e6b47?hl=en](https://note.com/tender_clam9623/n/n26e9378e6b47?hl=en&utm_source=gemini) - *Respalda el workflow doloroso actual (trabajador invirtiendo 3 horas en copiar/pegar en Excel y buscar excepciones).*
* **Reddit - r/business**: [https://www.reddit.com/r/business/comments/c0kcnx/can_someone_please_explain_the_difference_between/](https://www.reddit.com/r/business/comments/c0kcnx/can_someone_please_explain_the_difference_between/?utm_source=gemini) - *Respalda la percepción del usuario sobre asumir el riesgo de no verificar albaranes ("2-way match") si el overhead de hacerlo es mayor que el beneficio esperado.*

**Investigado por:** Gemini

&nbsp;