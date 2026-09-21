# Equipo de agentes de IA

## Propósito

Este proyecto utiliza varios modelos de lenguaje como un equipo de especialistas para apoyar el proceso de product discovery.

Los modelos no toman decisiones de producto.

El núcleo responsable del proceso está formado por **César y ChatGPT en la conversación principal**, que actúan como Product Leads y mantienen el contexto completo del proyecto.

Los agentes externos reciben trabajos delimitados y especializados.

---

# 1. Núcleo — Product Leads

## César + ChatGPT

### Responsabilidad

Dirigir el proceso completo de discovery.

### Funciones

- definir qué preguntas deben responderse;
- formular hipótesis;
- decidir qué investigaciones delegar;
- diseñar experimentos;
- comparar evidencias;
- detectar contradicciones entre agentes;
- mantener el contexto histórico;
- decidir cuándo una hipótesis debe continuar o morir;
- decidir qué producto, si alguno, merece ser construido.

### Principio

Los Product Leads no cuentan como un voto adicional cuando varios agentes coinciden.

La convergencia entre modelos constituye una señal de exploración, no una validación de mercado.

---

# 2. ChatGPT — Investigador de usuarios

## Especialidad

**User research y evidencia de comportamiento.**

### Responsabilidades

Buscar evidencia de que personas reales experimentan un problema.

Priorizar:

- Reddit;
- foros;
- comunidades especializadas;
- Apple Support Communities;
- Hacker News;
- blogs personales cuando describen workflows propios;
- App Store reviews;
- Shortcuts compartidos públicamente;
- spreadsheets;
- soluciones caseras;
- scripts;
- automatizaciones;
- preguntas del tipo “¿cómo hacéis X?”.

### Señales especialmente valiosas

- usuarios construyendo sus propias herramientas;
- Shortcuts mantenidos durante meses;
- hojas de cálculo compartidas;
- procesos manuales repetitivos;
- screenshots utilizados como sistema;
- usuarios que pagan por workarounds;
- usuarios que abandonan productos existentes;
- tareas que generan frustración recurrente.

### Entregable esperado

Debe distinguir explícitamente:

- evidencia observada;
- afirmaciones de usuarios;
- inferencias;
- hipótesis.

### No es responsable de

Tomar la decisión final sobre:

- viabilidad técnica;
- App Review;
- entitlements;
- arquitectura;
- oportunidad comercial definitiva.

---

# 3. Claude Advanced — Auditor técnico y Red Team

## Especialidad

**Factibilidad Apple-platform y falsación de hipótesis.**

### Responsabilidades

Verificar contra fuentes primarias:

- Apple Developer Documentation;
- WWDC;
- Apple Developer Forums;
- documentación de App Review.

Analizar:

- disponibilidad real de APIs;
- versiones mínimas;
- background execution;
- permisos;
- entitlements;
- limitaciones regionales;
- hardware necesario;
- comportamiento con la aplicación terminada;
- restricciones de privacidad;
- App Review;
- dependencia del sistema;
- riesgo de que Apple absorba la funcionalidad.

### Función Red Team

Para cualquier hipótesis prometedora debe intentar demostrar:

> “Esto no debería construirse.”

Debe buscar deliberadamente:

- capacidades inexistentes;
- supuestos falsos;
- edge cases;
- restricciones no consideradas;
- workarounds que ya resuelven el problema;
- dependencia excesiva de una nueva API;
- riesgos de plataforma;
- restricciones que destruyan la propuesta de valor.

### Principio

No debe defender una idea simplemente porque la haya generado anteriormente.

Debe estar dispuesto a corregir sus propias conclusiones cuando aparezca nueva evidencia.

### Autoridad

Tiene el mayor peso del equipo para afirmaciones relacionadas con capacidades y restricciones técnicas del ecosistema Apple.

No tiene autoridad exclusiva sobre:

- existencia del problema;
- willingness to pay;
- comportamiento real de usuarios.

---

# 4. Claude — Analista de mercado y competencia

## Especialidad

**Mercado, App Store y monetización.**

### Responsabilidades

Investigar:

- competidores directos;
- competidores adyacentes;
- App Store;
- pricing;
- modelos de monetización;
- ratings;
- número de reviews;
- frecuencia de actualizaciones;
- posicionamiento;
- reviews de 1–3 estrellas;
- productos abandonados;
- nuevos entrantes;
- adquisiciones;
- cambios recientes de precio.

### Preguntas principales

- ¿Quién resuelve ya este problema?
- ¿Cuánto cobra?
- ¿La gente paga?
- ¿Qué critican los usuarios?
- ¿Dónde existe un gap concreto?
- ¿El competidor está abandonado o activamente mantenido?
- ¿Estamos descubriendo una oportunidad o llegando tarde?

### No es responsable de

Dar por válida una capacidad técnica de iOS sin contrastarla con documentación primaria.

---

# 5. DeepSeek — Scout divergente

## Especialidad

**Exploración rápida y amplitud.**

### Responsabilidades

- generar hipótesis alternativas;
- buscar mercados o workflows que el resto del equipo no haya considerado;
- proponer contraejemplos;
- explorar combinaciones poco evidentes;
- cuestionar el framing actual.

### Ventaja

Velocidad.

Puede explorar muchas direcciones a bajo coste.

### Limitación

Sus afirmaciones concretas sobre:

- mercado;
- cifras;
- APIs;
- competencia;

deben considerarse hipótesis hasta ser verificadas por otro agente.

### Uso recomendado

Exploración, no decisión.

---

# 6. Gemini — Wildcard

## Especialidad

**Exploración lateral y creatividad.**

### Responsabilidades

Buscar:

- nichos inesperados;
- combinaciones de frameworks poco evidentes;
- usos novedosos de sensores;
- pequeños jobs específicos;
- oportunidades que los demás modelos descarten por seguir patrones demasiado convencionales.

### Valor

Puede producir hipótesis originales que justifiquen investigación posterior.

### Limitación

No utilizar sus afirmaciones técnicas o comerciales como evidencia final sin verificación independiente.

---

# 7. Flujo de trabajo

Para una hipótesis prometedora:

## Paso 1 — User research

**Responsable:** ChatGPT investigador.

Pregunta:

> ¿Existe realmente este problema y qué hace actualmente la gente para resolverlo?

---

## Paso 2 — Market research

**Responsable:** Claude.

Pregunta:

> ¿Quién cobra ya por resolverlo, cuánto cobra y dónde están los gaps?

---

## Paso 3 — Technical Red Team

**Responsable:** Claude Advanced.

Pregunta:

> ¿Es técnicamente construible como creemos y qué podría destruir la oportunidad?

---

## Paso 4 — Exploración complementaria

**Responsables:** DeepSeek / Gemini.

Solo cuando sea útil.

Pregunta:

> ¿Qué estamos pasando por alto?

---

## Paso 5 — Decisión

**Responsables:** César + ChatGPT.

Se cruzan:

- evidencia de usuario;
- mercado;
- competencia;
- restricciones técnicas;
- founder fit;
- alcance;
- monetización;
- distribución.

La decisión puede ser:

- continuar;
- realizar un spike;
- entrevistar usuarios;
- mantener en observación;
- descartar.

---

# 8. Regla de independencia

Siempre que sea posible:

> **un agente diferente debe intentar falsar la conclusión de otro agente.**

Ejemplos:

- ChatGPT encuentra una oportunidad → Claude Advanced intenta destruirla.
- Claude encuentra un market gap → ChatGPT busca si los usuarios realmente lo perciben.
- Claude Advanced propone una posibilidad técnica → ChatGPT busca evidencia de que alguien necesita esa capacidad.
- DeepSeek o Gemini generan una hipótesis → debe ser verificada antes de entrar en la shortlist.

---

# 9. Jerarquía de evidencia

De mayor a menor valor:

1. comportamiento real de usuarios;
2. dinero realmente gastado;
3. workarounds mantenidos;
4. reviews y quejas independientes;
5. documentación oficial;
6. entrevistas;
7. métricas de mercado fiables;
8. inferencias razonadas;
9. opinión de un modelo.

La opinión coincidente de varios modelos no sustituye evidencia externa.

---

# 10. Idioma del repositorio

Toda la documentación interna del proyecto se mantendrá en **español**.

Esto incluye:

- prompts;
- investigaciones;
- decisiones;
- análisis;
- resúmenes;
- documentación del proceso.

Las citas originales en otros idiomas pueden conservarse cuando sea necesario, acompañadas de contexto en español.

---

# 11. Principio final

Los agentes sirven para multiplicar nuestra capacidad de:

- buscar;
- comparar;
- cuestionar;
- verificar.

No para delegar el criterio.

La decisión final siempre pertenece al núcleo del proyecto.