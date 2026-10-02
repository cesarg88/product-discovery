# **Health Goals — One-Pager**

**Estado:** Definición inicial de producto  
**Fecha:** Octubre de 2026  
**Nombre:** Provisional

---

## **Product Vision**

HealthKit contiene años de información sobre lo que una persona realmente hace:

* pasos;  
* entrenamientos;  
* minutos de actividad;  
* distancia;  
* peso;  
* frecuencia de actividad;  
* tendencias históricas.

Sin embargo, la mayoría de productos se concentran en responder:

> ¿Qué has hecho?

Health Goals quiere responder una pregunta diferente:

> **¿Qué quieres conseguir, dónde estás ahora y qué necesitas hacer desde hoy para acercarte a ello?**

La visión es convertir los datos pasivos que ya existen en el ecosistema Apple en un sistema personal de objetivos que requiera el mínimo esfuerzo manual posible.

El usuario no debería tener que convertirse en experto en métricas de fitness ni mantener otro habit tracker.

---

# **The concept**

El usuario comienza expresando una intención en lenguaje natural.

Por ejemplo:

> “Quiero volver a entrenar regularmente.”

> “Quiero moverme más.”

> “Quiero caminar más durante la semana.”

> “Quiero perder peso.”

> “Quiero dejar de ser tan sedentario.”

La aplicación interpreta esa intención y, con permiso del usuario, analiza su historial reciente de HealthKit.

En lugar de presentar inmediatamente un formulario con:

* pasos objetivo;  
* entrenamientos por semana;  
* minutos de actividad;

la aplicación primero intenta comprender **el punto de partida real**.

Ejemplo:

> Durante las últimas 8 semanas:

> * has realizado 1,8 entrenamientos por semana;  
> * caminas una media de 5.900 pasos al día;  
> * acumulas unos 80 minutos de actividad semanales.

A partir de ese baseline, la aplicación propone un conjunto pequeño de objetivos medibles.

Por ejemplo:

> Para empezar:

> * 3 entrenamientos por semana;  
> * 49.000 pasos semanales;  
> * 120 minutos de actividad semanal.

El usuario puede:

* aceptar;  
* ajustar;  
* eliminar;  
* sustituir cualquiera de ellos.

Una vez aceptados, comienza el seguimiento automático.

---

# **The Core Loop**

El producto se apoya en un loop recurrente.

### **1\. Intención**

El usuario expresa qué quiere conseguir.

> “Quiero ser más constante entrenando.”

### **2\. Baseline**

Health Goals utiliza el historial de HealthKit para entender lo que el usuario hace actualmente.

### **3\. Plan**

La aplicación transforma intención \+ baseline en un pequeño conjunto de objetivos concretos y medibles.

El usuario mantiene siempre la decisión final.

### **4\. Progress**

HealthKit actualiza automáticamente el progreso.

No hay que marcar:

> “Hoy he entrenado.”

si HealthKit ya sabe que hubo un workout.

### **5\. Gap**

La aplicación calcula continuamente:

> **¿Qué diferencia existe entre donde estás y donde quieres terminar esta semana?**

Ejemplo:

> Jueves

> 2 / 4 entrenamientos  
> 31.400 / 56.000 pasos

> Quedan 3 días.

### **6\. Next action**

En lugar de limitarse a mostrar barras de progreso:

> **Para completar tus objetivos esta semana te quedan:**

> * 2 entrenamientos;  
> * unos 8.200 pasos diarios de aquí al domingo.

### **7\. Adapt**

Cuando cambia el progreso, cambia también lo que queda por hacer.

Si el viernes el usuario camina 14.000 pasos, Health Goals recalcula automáticamente el resto de la semana.

El loop vuelve a empezar cada semana.

---

# **Value Proposition**

## **The promise**

> **Dime qué quieres conseguir. Yo utilizaré los datos que tu iPhone y Apple Watch ya tienen para ayudarte a convertirlo en objetivos realistas y decirte cómo vas y qué te queda.**

---

## **Para el usuario**

### **No necesito saber cuáles deberían ser mis métricas**

El usuario puede pensar en resultados humanos:

> “quiero volver a estar activo”

en lugar de configurar métricas técnicas desde cero.

### **No necesito registrar lo que ya sabe mi teléfono**

Siempre que HealthKit pueda verificar una actividad, el seguimiento debe ser automático.

### **Sé dónde estoy**

La aplicación utiliza el historial para establecer contexto.

No empieza con una pantalla vacía.

### **Sé qué me queda**

El producto no termina en:

> “62 % completado.”

Debe responder:

> “¿Qué significa eso para el resto de mi semana?”

### **Mis objetivos pueden evolucionar**

Cuando la consistencia cambia durante varias semanas, el producto puede sugerir revisar los objetivos.

Nunca debe modificarlos silenciosamente.

---

# **Diferencia respecto a un fitness dashboard**

Un dashboard tradicional sigue principalmente este flujo:

> dato → visualización

Health Goals:

> **intención → baseline → objetivo → progreso → gap → acción**

El dato no es el producto.

El dato es la materia prima.

---

# **Ejemplo completo**

El usuario escribe:

> **“Quiero volver a estar en forma. Últimamente casi no entreno.”**

Health Goals analiza las últimas ocho semanas.

Encuentra:

* media de 1,6 workouts semanales;  
* 5.850 pasos diarios;  
* 75 minutos semanales de actividad.

La aplicación responde:

> **No partes de cero.**

> Durante las últimas semanas entrenaste aproximadamente 1–2 veces por semana y caminaste unos 5.850 pasos diarios.

> Para empezar, te proponemos:

> * 3 entrenamientos por semana;  
> * 49.000 pasos semanales;  
> * 120 minutos de actividad.

> Puedes cambiar cualquier objetivo antes de empezar.

El usuario acepta.

El jueves:

> **Esta semana vas algo por debajo del ritmo.**

> ✓ 1/3 entrenamientos  
> ✓ 28.500/49.000 pasos  
> ✓ 62/120 minutos

> Quedan 3 días.

> Para completar la semana:

> * 2 entrenamientos;  
> * \~6.850 pasos/día;  
> * 58 minutos de actividad.

El sábado, después de entrenar:

> **Vuelves a estar en camino.**

> Te queda 1 entrenamiento y aproximadamente 8.000 pasos antes del domingo por la noche.

---

# **Alcance de la primera versión**

La primera versión debe ser deliberadamente pequeña.

## **Intenciones soportadas**

Inicialmente:

### **Moverme más**

Principalmente pasos y actividad.

### **Entrenar con más regularidad**

Workouts por semana.

### **Ser más constante**

Combinación pequeña de actividad \+ entrenamientos.

### **Caminar más**

Pasos o distancia.

### **Mejorar mi actividad mientras intento perder peso**

Puede utilizar:

* actividad;  
* workouts;  
* pasos;  
* tendencia de peso si existe.

Pero con una frontera explícita:

**Health Goals no prescribe dietas, déficit calórico ni promete una determinada pérdida de grasa.**

Puede ayudar a convertir una intención relacionada con peso en hábitos de actividad medibles y hacer seguimiento de tendencias, pero no sustituye asesoramiento médico o nutricional.

---

# **Métricas iniciales**

Intentaremos comenzar con muy pocas:

* workouts por semana;  
* pasos semanales;  
* minutos de actividad;  
* distancia caminada/corrida;  
* opcionalmente tendencia de peso.

No incluir inicialmente:

* HRV;  
* VO₂ max;  
* sueño;  
* frecuencia cardíaca en reposo;  
* recuperación;  
* readiness;  
* calorías ingeridas;  
* nutrición;  
* diagnósticos;  
* interpretaciones clínicas.

Estas métricas podrán investigarse posteriormente si existe un job concreto.

---

# **Goal Engine**

Una pieza central del producto será el motor que transforma:

> baseline → propuesta de objetivos

No debe funcionar como una caja negra.

Los objetivos deben ser:

* explicables;  
* conservadores;  
* modificables;  
* reproducibles;  
* testeables.

Cuando sea posible, el usuario podrá preguntar:

> ¿Por qué me propones esto?

Y recibir una explicación concreta:

> “Durante las últimas semanas has hecho aproximadamente dos entrenamientos semanales. Te proponemos tres como siguiente objetivo.”

No:

> “La IA considera que tres entrenamientos son óptimos.”

---

# **Papel de la IA**

La IA puede ser útil, pero no constituye la propuesta de valor.

Puede utilizarse para interpretar lenguaje como:

> “Quiero volver al gimnasio y moverme más entre semana.”

y convertirlo en una intención estructurada.

Pero decisiones numéricas importantes deberían proceder de lógica explícita utilizando:

* baseline;  
* progresión;  
* reglas del producto;  
* objetivos aceptados por el usuario.

Foundation Models podría permitir que esa interpretación se realice on-device.

---

# **Product principles**

## **Zero logging whenever possible**

Si HealthKit ya conoce el dato, no preguntárselo de nuevo al usuario.

## **Explain everything**

Toda recomendación debe poder explicar de dónde sale.

## **User owns the goal**

La aplicación propone.

El usuario decide.

## **Progress, not perfection**

No convertir un fallo semanal en castigo o pérdida de una streak artificial.

## **Weekly over daily**

Para muchos objetivos, una semana proporciona más flexibilidad que obligar a cumplir exactamente lo mismo cada día.

## **Action over analytics**

Antes de añadir otra gráfica preguntarse:

> ¿Esto ayuda al usuario a decidir qué hacer?

Si no, probablemente no pertenece al producto.

---

# **Native Apple advantage**

Health Goals debería sentirse como un producto del ecosistema Apple, no como una web envuelta en SwiftUI.

### **HealthKit**

Fuente principal de datos y baseline histórico.

### **WidgetKit**

El widget puede convertirse en una superficie fundamental:

> **ON TRACK**

o:

> **2 workouts \+ 12.400 pasos restantes**

sin necesidad de abrir la aplicación.

### **App Intents**

Consultas o acciones rápidas como:

> “¿Cómo voy esta semana?”

> “Cambiar mi objetivo de entrenamientos a cuatro.”

### **Apple Watch**

Potencialmente una superficie posterior para consultar progreso y gap.

No es requisito para v1.

### **Foundation Models**

Interpretación on-device de intenciones cuando aporte valor.

---

# **Target user inicial**

No intentaremos servir a “todo el mundo que quiere estar sano”.

El usuario inicial probablemente es:

> **Una persona con iPhone —idealmente también Apple Watch— que ya genera datos de actividad automáticamente, quiere mejorar o mantener determinados hábitos físicos y no quiere registrar manualmente cada comportamiento.**

No necesita ser atleta.

Tampoco buscamos inicialmente usuarios que necesiten:

* preparación deportiva profesional;  
* rehabilitación;  
* tratamiento médico;  
* planes nutricionales;  
* coaching deportivo especializado.

---

# **Lo que NO es**

Health Goals no es:

* otro Apple Health;  
* otro activity dashboard;  
* una app médica;  
* un entrenador personal generado por IA;  
* una app de dieta;  
* un habit tracker manual;  
* una red social fitness;  
* una aplicación de planes de entrenamiento.

Su trabajo es mucho más pequeño:

> **convertir una intención personal en objetivos medibles y mantener al usuario informado automáticamente de su progreso y de lo que aún necesita hacer.**

---

# **MVP**

El MVP debe demostrar únicamente este loop:

1. El usuario explica qué quiere conseguir.  
2. Autoriza HealthKit.  
3. Analizamos un periodo histórico.  
4. Proponemos 1–3 objetivos.  
5. El usuario acepta o ajusta.  
6. Mostramos progreso semanal.  
7. Calculamos automáticamente el gap.  
8. Mostramos qué queda por hacer.  
9. Widget con el estado actual.

Si ese loop no aporta valor, añadir más HealthKit metrics no salvará el producto.

---

# **KPIs iniciales**

No optimizar todavía por revenue.

Primero necesitamos saber si el loop crea comportamiento.

## **Activation**

* % que conecta HealthKit.  
* % que acepta al menos un objetivo.  
* % que completa el onboarding.

## **Engagement**

* usuarios que consultan progreso durante la semana;  
* apertura del widget/app después del primer día;  
* consultas al “qué me queda”.

## **Goal engagement**

* % de semanas donde el usuario mantiene objetivos activos;  
* % que modifica un objetivo;  
* % que acepta continuar otra semana.

## **Retention**

Especialmente:

* semana 2;  
* semana 4;  
* semana 8\.

La señal más importante sería que el usuario siga queriendo que Health Goals gestione sus objetivos una vez desaparece la novedad inicial.

---

# **Monetización — hipótesis inicial**

No definir todavía el pricing final.

Una estructura plausible sería:

### **Free**

* un número pequeño de objetivos simultáneos;  
* tracking y progreso básicos.

### **Premium**

Pago único inicialmente preferible a una suscripción artificial.

Podría desbloquear:

* objetivos ilimitados;  
* múltiples tipos de objetivos;  
* historial;  
* insights de progreso;  
* widgets avanzados;  
* personalización.

La monetización deberá validarse después del core loop.

---

# **Principal riesgo**

El mayor riesgo no es técnico.

Es que el usuario considere:

> “Apple Fitness ya me muestra suficiente información.”

Para sobrevivir, Health Goals debe conseguir que la diferencia entre:

> **ver mis datos**

y:

> **saber qué necesito hacer ahora**

sea suficientemente valiosa como para crear un hábito.

---

# **Pregunta que debe resolver el producto**

Toda decisión futura debería poder relacionarse con esta pregunta:

> **Con lo que ya sabe HealthKit sobre mí y con lo que quiero conseguir, ¿qué necesito hacer desde ahora para terminar el periodo cumpliendo mi objetivo?**

Si una feature no ayuda a responderla, probablemente no pertenece al MVP.

---

# **Próximo JTBD**

Antes de construir la aplicación completa necesitamos validar:

> **Como persona que quiere mejorar su actividad física, quiero convertir una intención general en objetivos realistas basados en mi actividad actual, y después saber automáticamente durante la semana si voy en camino y qué me queda por hacer, sin registrar manualmente mis hábitos.**

El siguiente trabajo de discovery debe concentrarse exclusivamente en este JTBD.

