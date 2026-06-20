# Capítulo VIII: Experiment-Driven Development

## 8.1. Experiment Planning

### 8.1.1. As-Is Summary.

El estado actual de la gestión de inventarios para los segmentos objetivos se caracteriza por una dependencia crítica en procesos manuales y registros fragmentados. La información reside en cuadernos físicos, archivos de Excel desactualizados y chats de WhatsApp, lo que genera una visibilidad nula del stock en tiempo real. Esta desorganización provoca errores constantes en el control de fechas de vencimiento y una alta carga de ansiedad operativa. Aunque ya se ha definido un stack tecnológico (Spring Boot/Angular) y una arquitectura de software , el estado actual del negocio sigue siendo reactivo e intuitivo, lo que plantea la necesidad de cuestionar si la digitalización propuesta es lo suficientemente simple y óptima para ser adoptada por usuarios con fatiga laboral y baja alfabetización digital.

Problemas identificados:

- Rendimiento: La aplicación presenta demoras en el filtrado de productos por nombre.
- Experiencia de usuario: Formato con bajo contraste para la generación de reportes.
- Funcionalidad: Ausencia de módulo para ver el historial de lotes.
- Usabilidad: Falta de traducción para usuarios de diferentes lenguas.

Objetivos de mejora:

Para abordar estos problemas, se han establecido los siguientes objetivos de mejora:

- Reducir el tiempo de búsqueda de productos a menos de 2 segundos.
- Mejorar la legibilidad de los reportes con un nuevo diseño de alto contraste.
- Implementar un módulo de historial de lotes para seguimiento detallado.
- Añadir soporte multilingüe para ampliar la accesibilidad.

### 8.1.2. Raw Material: Assumptions, Knowledge Gaps, Ideas, Claims.

Esta sección consolida las fuentes de inspiración derivadas de la investigación de usuarios, el diseño de interfaces y la arquitectura del sistema:

- **Assumptions (Suposiciones):** Son creencias o expectativas que se tienen sobre el comportamiento de los usuarios, el mercado o la tecnología, que aún no han sido validadas:
  - Mejora de eficiencia de busqueda: Se asume que los usuarios valoran más la rapidez en la búsqueda de productos por nombre común cuando manejan una gran cantidad de SKUs.
  - Reportes de alto contraste: Se asume que el rediseño de los reportes con un formato de alto contraste mejorará la legibilidad y reducirá los errores de interpretación.
  - Módulo de historial de lotes: Se asume que la implementación de un módulo de historial de lotes permitirá a los usuarios realizar un seguimiento detallado de los movimientos de inventario, reduciendo las pérdidas por vencimiento en un 20%.
  - Soporte multilingüe: Se asume que la adición de soporte multilingüe aumentará la accesibilidad de la aplicación, permitiendo a usuarios de diferentes lenguas utilizarla sin dificultades, lo que se traducirá en un aumento del 15% en la adopción por parte de usuarios no hispanohablantes.

- **Knowledge Gaps (Brechas de Conocimiento):** Son áreas donde se carece de información o comprensión suficiente, lo que requiere investigación adicional para validar o refutar las suposiciones:
  - No sabemos cuál es el tiempo máximo que un bodeguero está dispuesto a dedicar diariamente al ingreso de datos en la aplicación.
  - No sabemos qué tan dispuestos están los usuarios a ingresar el SKU de cada producto frente a búsquedas por nombre común.
  - No sabemos en qué medida el costo de la suscripción es una barrera frente a las pérdidas actuales por productos vencidos no detectados.
  - No sabemos qué tan importante es para los usuarios tener acceso a reportes visuales de alto contraste en comparación con reportes tradicionales.
  - No sabemos qué tan relevante es para los usuarios contar con un módulo de historial de lotes para su gestión diaria de inventarios.
  - No sabemos qué tan importante es para los usuarios tener soporte multilingüe en la aplicación, considerando la diversidad lingüística en el mercado objetivo.

- **Ideas:** Son propuestas de funcionalidades o mejoras basadas en la investigación y el diseño, que aún no han sido validadas:
  - Implementación de flujos de registro de entrada/salida optimizados para dispositivos móviles (Mobile-first) para permitir el conteo a pie de estantería.
  - Centralización de la gestión de proveedores vinculada directamente a la reposición de lotes para automatizar la cadena de suministro.

- **Claims (Afirmaciones):** Son declaraciones hechas sobre el producto ya sea por stakeholders o usuarios.
  - La aplicación es fácil de usar y mejora significativamente la gestión de inventarios en comparación con los métodos manuales anteriores.
  - La función de búsqueda por nombre común es esencial para manejar grandes catálogos de productos, ya que los usuarios no recuerdan los SKUs.
  - Los reportes de alto contraste son cruciales para mejorar la legibilidad y reducir errores en la interpretación de datos.
  - El módulo de historial de lotes es una herramienta indispensable para el seguimiento detallado de los movimientos de inventario y la reducción de pérdidas por vencimiento.
  - El soporte multilingüe es fundamental para ampliar la accesibilidad de la aplicación a usuarios de diferentes lenguas, aumentando su adopción.

### 8.1.3. Experiment-Ready Questions.

En esta etapa, transformamos las suposiciones y brechas de conocimiento en preguntas concretas que guiarán nuestros experimentos. Estas se dividen en dos categorías principales para asegurar tanto la validación de nuestras premisas como el descubrimiento de nuevas oportunidades.

#### Preguntas Impulsadas por Creencias (Belief-led)
Estas preguntas buscan validar o refutar una premisa específica que el equipo considera verdadera pero que carece de evidencia empírica.
* **BC1:** ¿El uso de un diseño de alto contraste en los reportes reduce realmente los errores de interpretación de datos en un 30% durante jornadas nocturnas?
* **BC2:** ¿La implementación del historial de lotes es el factor determinante para que un usuario decida pagar por la suscripción mensual en lugar de seguir usando Excel?
* **BC3:** ¿Es la búsqueda por nombre común más rápida que el escaneo de SKU para usuarios que manejan menos de 50 productos distintos?

#### Preguntas Exploratorias
Diseñadas para generar conocimiento en áreas donde no tenemos creencias previas o el comportamiento del usuario es incierto.
* **EX1:** ¿Qué criterios específicos utiliza un dueño de bodega para decidir qué productos merecen un seguimiento por lotes y cuáles no?
* **EX2:** ¿Cómo varía la tolerancia a la latencia de búsqueda cuando el usuario está atendiendo a un cliente en paralelo frente a cuando realiza inventario a puerta cerrada?
* **EX3:** ¿Qué otros idiomas o modismos regionales son críticos para que la aplicación se sienta "local" en mercados fuera de la capital?

#### Técnica de las "Cinco Ws (y una H)" para el Descubrimiento de Premisas
Utilizamos esta técnica para profundizar en el problema central de la **gestión manual de vencimientos** y descubrir necesidades ocultas de usuarios como Carla Rodríguez.

| Dimensión | Pregunta | Hallazgo / Premisa Oculta |
|:---|:---|:---|
| **Who (Quién)** | ¿Quién es el responsable de verificar los vencimientos? | Generalmente es el dueño; si lo delega, pierde confianza por falta de un sistema de control. |
| **What (Qué)** | ¿Qué sucede exactamente cuando un producto vence? | Se genera una pérdida neta o se intenta devolver al proveedor, lo cual genera fricción y pérdida de tiempo. |
| **Where (Dónde)**| ¿Dónde ocurre la verificación? | En el almacén físico, a menudo con poca iluminación y espacio reducido (necesidad de movilidad y contraste). |
| **When (Cuándo)** | ¿Cuándo se dan cuenta del vencimiento? | Generalmente cuando el cliente ya tiene el producto en la mano o durante un conteo físico aleatorio. |
| **Why (Por qué)** | ¿Por qué no usan herramientas digitales hoy? | Porque el Excel requiere una computadora y tiempo de oficina que no tienen durante la operación. |
| **How (Cómo)** | ¿Cómo calculan hoy cuándo reponer? | Basándose en la memoria visual de los estantes ("ojímetro"), lo cual es propenso a errores humanos. |

A partir de este análisis, surge la pregunta lista para experimento: *¿Podemos automatizar la "confianza" del dueño mediante alertas preventivas que lleguen directamente a su WhatsApp?*

### 8.1.4. Question Backlog.

Esta sección presenta el backlog como una lista priorizada de preguntas de investigación. El sistema de puntuación evalúa cada pregunta del 1 al 5 en cuatro criterios: **Confianza (C)** (qué tan seguros estamos del conocimiento actual), **Riesgo (R)** (qué tan crítico es equivocarnos en este punto), **Impacto (I)** (cuánto valor aporta resolverlo) e **Interés (In)** (relevancia para los stakeholders). En caso de empate en la puntuación total, se prioriza la pregunta con mayor puntaje en **Riesgo**.

#### Broad Backlog (Preguntas de Negocio y Adopción)

Estas preguntas abordan la propuesta de valor y el modelo de negocio de manera general.

| ID | Pregunta de Investigación | El "Por qué" (Motivación) | C | R | I | In | Total |
|:---|:---|:---|:---:|:---:|:---:|:---:|:---:|
| QB1 | ¿En qué medida el costo de la suscripción es una barrera frente a las pérdidas actuales por productos vencidos no detectados? | Si el costo supera la percepción de ahorro por mermas, el modelo de negocio no será sostenible para pymes. | 2 | 5 | 5 | 5 | **17** |
| QB2 | ¿Qué tan relevante es el soporte multilingüe para la adopción en mercados con diversidad lingüística? | Validar si el esfuerzo técnico de internacionalización justifica el crecimiento esperado en nuevos segmentos. | 3 | 2 | 2 | 3 | **10** |

#### Deep Backlog (Preguntas de Ejecución y UX)

Estas preguntas profundizan en funcionalidades específicas y la interacción técnica del usuario.

| ID | Pregunta de Investigación | El "Por qué" (Motivación) | C | R | I | In | Total |
|:---|:---|:---|:---:|:---:|:---:|:---:|:---:|
| QD1 | ¿La implementación de un historial de lotes reduce efectivamente las pérdidas por vencimiento en un 20% como se supone? | Es el núcleo de la propuesta de valor para bodegas de consumo masivo; fallar aquí invalida la utilidad del módulo. | 4 | 5 | 5 | 3 | **17** |
| QD2 | ¿Cuál es el umbral de tiempo máximo de búsqueda por nombre común que el usuario tolera antes de frustrarse? | La latencia en la búsqueda impacta directamente en la productividad diaria del bodeguero. | 3 | 4 | 4 | 4 | **15** |
| QD3 | ¿Mejora significativamente el diseño de alto contraste la velocidad de interpretación de reportes en entornos de baja iluminación? | Muchos bodegueros operan en almacenes con luz limitada o fatiga visual tras jornadas largas. | 4 | 2 | 3 | 3 | **12** |

**Análisis de Priorización:**
1. **QB1 y QD1 (Empate - 17 pts):** Ambas representan el mayor riesgo estratégico (5). Se abordarán en paralelo ya que QB1 valida la viabilidad comercial y QD1 la viabilidad técnica de la solución.
2. **QD2 (15 pts):** Crucial para la retención del usuario a largo plazo.
3. **QD3 (12 pts):** Mejora incremental de accesibilidad.
4. **QB2 (10 pts):** Considerada de baja prioridad hasta consolidar el mercado local.

### 8.1.5. Experiment Cards.

En esta sección se detallan las Tarjetas de Experimento para las preguntas de mayor prioridad. Estas tarjetas actúan como el contrato del experimento antes de su ejecución.

#### Tarjeta de Experimento 01: Viabilidad de Suscripción (QB1)

**Lado Frontal: El Qué y el Por Qué**
*   **Pregunta:** ¿En qué medida el costo de la suscripción es una barrera frente a las pérdidas actuales por productos vencidos?
*   **Why?:** Si el costo de StockTrack supera la percepción de ahorro por reducción de mermas, los usuarios como Carla no adoptarán la solución a largo plazo.
*   **Hypothesis:** Creemos que los dueños de bodegas aceptarán un costo mensual de $15 USD si el sistema demuestra mediante un reporte inicial que sus pérdidas por vencimiento superan los $50 USD mensuales.
*   **What:** Un prototipo de alta fidelidad en Figma que simula un "Calculador de Retorno de Inversión (ROI)" donde el usuario ingresa sus mermas estimadas y ve el costo de la App contrastado.

**Lado Posterior: Configuración**
*   **Medidas:** Porcentaje de usuarios que hacen clic en el botón "Adquirir Plan" tras interactuar con la calculadora de ahorro.
*   **Condiciones:** Entrevistas guiadas con 10 dueños de bodegas (Segmento 1) utilizando el prototipo.
*   **Escala:** El experimento se considera exitoso si al menos 7 de cada 10 usuarios consideran que el precio es "Justo" o "Barato" en relación al valor percibido de ahorro.

---

#### Tarjeta de Experimento 02: Eficacia del Historial de Lotes (QD1)

**Lado Frontal: El Qué y el Por Qué**
*   **Pregunta:** ¿La implementación de un historial de lotes reduce efectivamente las pérdidas por vencimiento?
*   **Why?:** Validar que la funcionalidad técnica realmente soluciona el problema de negocio de Andrés (pérdida de dinero por stock "olvidado").
*   **Hypothesis:** Creemos que proporcionar una vista de "Lotes Próximos a Vencer" con alertas de 7 días de anticipación permitirá a los usuarios realizar ventas de liquidación, reduciendo las pérdidas físicas en un 20%.
*   **What:** Un MVP funcional (módulo de lotes) conectado a una base de datos real con 20 productos de prueba para un usuario seleccionado.
*   **Type:** Experiment-Ready (Ready to build).

**Lado Posterior: Configuración**
*   **Medidas:** Cantidad de productos que llegaron a su fecha de vencimiento sin ser vendidos/devueltos comparado con el registro manual del mes anterior.
*   **Condiciones:** Uso de la funcionalidad por parte de 5 usuarios "Early Adopters" durante un ciclo de inventario (15 días).
*   **Escala:** Éxito si se registra una reducción de al menos el 15% en mermas reales durante el periodo de prueba.

---

#### Tarjeta de Experimento 03: Tolerancia a Latencia de Búsqueda (QD2)

**Lado Frontal: El Qué y el Por Qué**
*   **Pregunta:** ¿Cuál es el umbral de tiempo máximo de búsqueda por nombre común que el usuario tolera antes de frustrarse?
*   **Why?:** La fluidez en la atención al cliente depende de la rapidez de la App; una búsqueda lenta obliga al usuario a volver al cuaderno físico.
*   **Hypothesis:** Creemos que una respuesta de búsqueda superior a los 2 segundos provocará que el usuario abandone el uso de la App en momentos de alta afluencia de clientes.
*   **What:** Un prototipo funcional que permite ajustar artificialmente el tiempo de respuesta del buscador (0.5s, 1.5s, 3s) para observar reacciones.

**Lado Posterior: Configuración**
*   **Medidas:** Tasa de abandono de la tarea de búsqueda y nivel de frustración reportado (Escala Likert).
*   **Condiciones:** Pruebas de usabilidad con 8 usuarios simulando una situación de "atención bajo presión".
*   **Escala:** El experimento identifica el "punto de quiebre". Se define éxito técnico si logramos mantener la latencia por debajo del umbral identificado (objetivo < 1.5s).

---

#### Tarjeta de Experimento 04: Impacto del Alto Contraste (QD3)

**Lado Frontal: El Qué y el Por Qué**
*   **Pregunta:** ¿Mejora significativamente el diseño de alto contraste la velocidad de interpretación de reportes?
*   **Why?:** Los almacenes de las bodegas suelen tener iluminación deficiente y los usuarios (como Carla) presentan fatiga visual tras jornadas largas.
*   **Hypothesis:** Creemos que un diseño de alto contraste reducirá el tiempo de identificación de productos críticos en un 25% bajo condiciones de poca luz.
*   **What:** Test A/B con dos versiones del dashboard de reportes: una estándar y otra con paleta de colores de alto contraste.

**Lado Posterior: Configuración**
*   **Medidas:** Tiempo (segundos) requerido para encontrar la fecha de vencimiento de un producto específico en el reporte.
*   **Condiciones:** Pruebas controladas con 6 usuarios en una habitación con iluminación reducida (< 100 lux).
*   **Escala:** Éxito si la versión de alto contraste muestra una mejora del 20% en la velocidad de lectura frente a la versión estándar.

---

#### Tarjeta de Experimento 05: Soporte Multilingüe / Localización (QB2)

**Lado Frontal: El Qué y el Por Qué**
*   **Pregunta:** ¿Qué tan relevante es el soporte multilingüe para la adopción en mercados con diversidad lingüística?
*   **Why?:** Queremos validar si el esfuerzo técnico de internacionalización justifica el crecimiento esperado en nuevos segmentos o si el español es suficiente para la fase de tracción.
*   **Hypothesis:** Creemos que ofrecer la interfaz con terminología localizada (o idiomas originarios según la región) incrementará la confianza del usuario en un 15%, ya que reduce la barrera de "tecnología ajena".
*   **What:** Una "Landing Page" de registro y una pantalla de inventario traducidas a un segundo idioma (ej. Quechua o inglés técnico para exportadores) para medir el interés mediante registros.

**Lado Posterior: Configuración**
*   **Medidas:** Tasa de conversión (sign-up) en la versión localizada frente a la versión estándar.
*   **Condiciones:** Campaña de anuncios segmentada o visitas presenciales a 10 negocios en zonas con bilingüismo predominante.
*   **Escala:** Éxito si al menos el 20% de los nuevos interesados optan por la versión localizada al momento del registro.

## 8.2. Experiment Design

### 8.2.1. Hypotheses.

En esta sección, transformamos las 5 tarjetas de experimentación mencionadas en el punto 8.1.5 en hipótesis rigurosas y cuantificables. Para cada una, definimos el cuestionamiento central, los supuestos que dieron origen a la prueba, la hipótesis de trabajo y la correspondiente hipótesis nula, la cual servirá para determinar si los resultados obtenidos invalidan nuestra premisa inicial.

| Question | Belief (Creencia) | Hypothesis (Hipótesis) | Null Hypothesis (Hipótesis Nula) |
| :--- | :--- | :--- | :--- |
| ¿En qué medida el costo de la suscripción es una barrera frente a las pérdidas actuales por productos vencidos? | Creemos que los dueños de bodega no perciben el verdadero costo de sus mermas actuales, por lo que el precio de suscripción se siente como un gasto adicional y no como una inversión. Si logramos visibilizar la pérdida real frente al costo del software, el usuario reevaluará su disposición a pagar. | Los dueños de bodegas aceptarán un costo mensual de $15 USD si el sistema demuestra, mediante un reporte inicial, que sus pérdidas por vencimiento superan los $50 USD mensuales. Al menos el 70% de los usuarios (7 de 10) calificarán el precio como "Justo" o "Barato" tras interactuar con la calculadora de ROI, y harán clic en "Adquirir Plan". Mediremos esto con 10 dueños de bodega en una entrevista guiada con prototipo. | El costo de suscripción seguirá percibido como una barrera independientemente de la comparativa de ahorro presentada. Menos del 70% de los usuarios calificará el precio como "Justo" o "Barato", o no harán clic en "Adquirir Plan" pese a ver el ahorro proyectado, indicando que el precio (o el modelo de negocio) no es viable en su forma actual. |
| ¿La implementación de un historial de lotes reduce efectivamente las pérdidas por vencimiento? | Creemos que los bodegueros pierden dinero por productos vencidos porque no tienen un sistema de alerta temprana; dependen de la memoria visual ("ojímetro") para detectar productos próximos a vencer, lo cual falla sistemáticamente. Dar visibilidad proactiva de los lotes permitirá actuar a tiempo (liquidación o devolución) antes de que el producto se pierda. | Proporcionar una vista de "Lotes Próximos a Vencer" con alertas de 7 días de anticipación permitirá a los usuarios realizar ventas de liquidación, reduciendo las pérdidas físicas en al menos 15-20% respecto al registro manual del mes anterior. Mediremos esto con 5 usuarios "Early Adopters" durante un ciclo de inventario completo (15 días), usando un MVP funcional conectado a una base de datos real con 20 productos de prueba. | El historial de lotes no reducirá significativamente las mermas reales. La reducción observada será menor al 15%, indicando que las alertas no son suficientes para cambiar el comportamiento del usuario, o que el problema de raíz no es la falta de visibilidad sino la falta de tiempo/incentivo para actuar sobre la alerta. |
| ¿Qué tan relevante es el soporte multilingüe para la adopción en mercados con diversidad lingüística? | Creemos que parte de la resistencia a adoptar herramientas digitales en mercados con diversidad lingüística viene de que la tecnología se siente "ajena" cuando no refleja la terminología local. Ofrecer una versión localizada reducirá esa barrera de confianza y aumentará el interés real en registrarse. | Ofrecer la interfaz con terminología localizada (o idiomas originarios según la región) incrementará la tasa de registro en al menos un 20% frente a la versión estándar, y aumentará la confianza percibida del usuario en un 15%. Mediremos esto publicando una landing page y una pantalla de inventario traducidas, midiendo conversión en 10 negocios de zonas con bilingüismo predominante. | La localización no producirá una diferencia significativa en la tasa de registro (menos del 20% elige la versión localizada) ni en la confianza percibida, indicando que el idioma no es una barrera crítica de adopción frente a otros factores como precio o funcionalidad. |
| ¿Cuál es el umbral de tiempo máximo de búsqueda por nombre común que el usuario tolera antes de frustrarse? | Creemos que la fluidez en la atención al cliente depende directamente de la rapidez de la app; si la búsqueda es lenta, el usuario abandona la herramienta y vuelve al cuaderno físico, especialmente bajo presión de atención al cliente. | Una respuesta de búsqueda superior a 2 segundos provocará abandono de tarea, y manteniendo la latencia por debajo de 1.5 segundos se minimizará la frustración reportada (≤2/5 en escala Likert) y la tasa de abandono. Mediremos esto con 8 usuarios bajo tres escalones de latencia simulada (0.5s/1.5s/3s) en un escenario de "atención bajo presión". | La latencia de búsqueda no tiene un efecto medible sobre el abandono de tarea ni la frustración reportada dentro del rango probado (0.5s-3s); los usuarios toleran tiempos de respuesta más altos de lo esperado, o abandonan independientemente de la velocidad por otras razones (ej. interfaz confusa). |
| ¿Mejora significativamente el diseño de alto contraste la velocidad de interpretación de reportes? | Creemos que los almacenes de las bodegas suelen tener iluminación deficiente y los usuarios presentan fatiga visual tras jornadas largas, lo cual genera errores de interpretación en reportes con bajo contraste. Un rediseño visual de alto contraste debería reducir significativamente el tiempo y los errores de lectura bajo estas condiciones. | Un diseño de alto contraste reducirá el tiempo de identificación de productos críticos en al menos un 20-25% bajo condiciones de poca luz (<100 lux), y reducirá la tasa de error de lectura a ≤5%. Mediremos esto con un Test A/B con 6 usuarios comparando la versión estándar vs. la versión de alto contraste del dashboard de reportes. | El diseño de alto contraste no produce una mejora medible en el tiempo de identificación (mejora <20%) ni en la tasa de error de lectura frente a la versión estándar, bajo las mismas condiciones de iluminación reducida. |


---

**Nota sobre Hipótesis Nulas:**
 
Las hipótesis nulas son críticas para diseño experimental riguroso. Nos permiten definir claramente qué constituye un **fracaso del experimento**. Si los resultados se acercan más a la hipótesis nula que a la hipótesis principal, debemos:
 
1. **Rechazar la funcionalidad** (no promoverla a producción), o
2. **Pivotar el diseño** (rediseñar la UX, simplificar el flujo, añadir features faltantes), o
3. **Cuestionar las asunciones** (quizás el pain point no era tan crítico como se pensaba)
> **Nota de trazabilidad:** las hipótesis 4 y 5 formalizan las Tarjetas de Experimento 03 (QD2) y 04 (QD3) respectivamente, que ya contaban con una hipótesis de trabajo implícita en su "Lado Frontal" pero no estaban numeradas en la versión anterior de esta sección.

### 8.2.2. Domain Business Metrics

Esta sección define las métricas de negocio a nivel de dominio que se verán impactadas por los experimentos planificados. Estas métricas son de alto nivel y reflejan los objetivos estratégicos del negocio (StockTrack), alineados con los problemas identificados en el As-Is (8.1.1) y las Tarjetas de Experimento (8.1.5).
 
#### Métricas de Dominio Identificadas
 
**1. Tasa de Merma (Merchandise Shrinkage Rate)**
 
**Definición:** Porcentaje de inventario perdido por vencimiento sobre el inventario total gestionado.
 
**Indicadores clave:**
 
- Número de unidades vencidas no vendidas/devueltas por ciclo de inventario
- Valor monetario de la pérdida mensual por vencimiento
**Experimentos relacionados:** Hipótesis 2 (Eficacia del Historial de Lotes)
 
**Baseline actual (As-Is):** Sin visibilidad de fechas de vencimiento centralizada; el control depende de la memoria visual del dueño ("ojímetro"), generando pérdidas no cuantificadas con precisión.
 
**Objetivo (To-Be):** Reducir las mermas reales en al menos 15-20% mediante alertas preventivas de 7 días antes del vencimiento.
 
---
 
**2. Percepción de Valor del Precio (Price Value Perception / CAC Viability)**
 
**Definición:** Relación entre el costo de la suscripción y el valor (ahorro por reducción de mermas) que el usuario percibe al adquirirla.
 
**Indicadores clave:**
 
- Tasa de conversión tras ver la comparativa de ahorro (calculadora de ROI)
- Porcentaje de usuarios que califican el precio como "Justo" o "Barato"
**Experimentos relacionados:** Hipótesis 1 (Viabilidad del Modelo de Suscripción)
 
**Baseline actual (As-Is):** El usuario no tiene forma de cuantificar cuánto pierde hoy por mermas, por lo que el precio de suscripción se percibe como gasto adicional y no como ahorro.
 
**Objetivo (To-Be):** Lograr que ≥70% de los usuarios piloto perciban el precio como "Justo" o "Barato" tras ver la comparativa de ahorro proyectado.
 
---
 
**3. Eficiencia Operativa de Búsqueda (Search Task Efficiency)**
 
**Definición:** Capacidad del usuario para encontrar un producto o lote específico dentro del sistema sin fricción perceptible, incluso bajo presión operativa.
 
**Indicadores clave:**
 
- Tiempo de respuesta del buscador (ms/segundos)
- Tasa de abandono de la tarea de búsqueda
**Experimentos relacionados:** Hipótesis 4 (Tolerancia a Latencia de Búsqueda)
 
**Baseline actual (As-Is):** Búsqueda manual en cuaderno físico o Excel, sin tiempo estandarizado pero con alta fricción reportada durante la atención al cliente.
 
**Objetivo (To-Be):** Tiempo de respuesta <1.5 segundos, con abandono de tarea minimizado bajo presión operativa.
 
---
 
**4. Confianza y Legibilidad de Reportes (Report Trust & Readability)**
 
**Definición:** Grado en que el usuario puede leer e interpretar correctamente los reportes de inventario y vencimientos, incluso en condiciones de baja iluminación o fatiga visual.
 
**Indicadores clave:**
 
- Tiempo de identificación de un dato crítico en el reporte
- Tasa de error de lectura bajo baja iluminación
**Experimentos relacionados:** Hipótesis 5 (Impacto del Alto Contraste)
 
**Baseline actual (As-Is):** Reportes con bajo contraste, generando errores de interpretación reportados por usuarios con fatiga visual o en almacenes con poca luz.
 
**Objetivo (To-Be):** Mejora ≥20% en velocidad de lectura y tasa de error ≤5% con el rediseño de alto contraste.
 
---
 
**5. Alcance y Adopción Multilingüe (Localized Market Reach)**
 
**Definición:** Grado en que usuarios de mercados con diversidad lingüística adoptan la plataforma cuando se les ofrece una versión adaptada a su idioma/región.
 
**Indicadores clave:**
 
- Porcentaje de registros en versión localizada vs. estándar
- Puntuación de confianza percibida (Likert) en mercados bilingües
**Experimentos relacionados:** Hipótesis 3 (Adopción por Localización)
 
**Baseline actual (As-Is):** 100% de la interfaz en español estándar; no existe dato sobre demanda real de soporte multilingüe, solo la suposición del equipo.
 
**Objetivo (To-Be):** ≥20% de los nuevos interesados en zonas bilingües optan por la versión localizada al momento del registro.
 
---
 
#### Alineación con Objetivos de Negocio
 
Estas métricas de dominio se alinean con los objetivos estratégicos de StockTrack:
 
- **Tasa de Merma → Propuesta de Valor Central:** Reducir mermas es el argumento de venta principal frente a Excel/cuaderno; valida si el producto resuelve el dolor #1 del usuario.
- **Percepción de Valor del Precio → Viabilidad del Modelo de Negocio:** Sin disposición a pagar, ninguna otra mejora del producto sostiene el negocio a largo plazo.
- **Eficiencia Operativa de Búsqueda → Retención Diaria:** Una búsqueda lenta empuja al usuario de vuelta al cuaderno físico; es la funcionalidad de uso más frecuente.
- **Confianza y Legibilidad de Reportes → Reducción de Errores Operativos:** Reportes mal leídos generan las mismas pérdidas que se busca evitar con el módulo de lotes.
- **Alcance y Adopción Multilingüe → Expansión de Mercado:** Determina si vale la pena invertir en internacionalización antes o después de consolidar el mercado local.

### 8.2.3. Measures.

Esta sección define las métricas específicas que se utilizarán para medir el éxito de cada una de las 5 hipótesis formuladas en la sección 8.2.1. Cada métrica es medible, cuantificable, y directamente relacionada con los criterios de éxito establecidos en las Tarjetas de Experimento.
 
---
 
#### Hipótesis 1: Viabilidad del Modelo de Suscripción
 
**Question:** ¿En qué medida el costo de la suscripción es una barrera frente a las pérdidas actuales por productos vencidos?
 
**Métricas:**
 
- **Tasa de Conversión Percibida (Perceived Conversion Rate):** Porcentaje de usuarios que hacen clic en "Adquirir Plan" tras interactuar con la calculadora de ROI. **Criterio de éxito: ≥70%** (7 de 10 usuarios).
- **Índice de Justicia de Precio (Price Fairness Score):** Porcentaje de usuarios que califican el precio como "Justo" o "Barato" frente al ahorro proyectado. **Criterio de éxito: ≥70%.**
---
 
#### Hipótesis 2: Eficacia del Historial de Lotes
 
**Question:** ¿La implementación de un historial de lotes reduce efectivamente las pérdidas por vencimiento?
 
**Métricas:**
 
- **Reducción de Mermas Reales (Shrinkage Reduction Rate):** Comparación de productos vencidos sin vender/devolver durante el ciclo de prueba (15 días) frente al registro manual del mes anterior. **Criterio de éxito: reducción ≥15%.**
- **Tasa de Acción sobre Alertas (Alert Action Rate):** Porcentaje de alertas de "7 días para vencer" que derivan en una acción del usuario dentro de las 48 horas siguientes. **Criterio de éxito: ≥60%.**
---
 
#### Hipótesis 3: Adopción por Localización
 
**Question:** ¿Qué tan relevante es el soporte multilingüe para la adopción en mercados con diversidad lingüística?
 
**Métricas:**
 
- **Tasa de Registro Localizado (Localized Sign-up Rate):** Porcentaje de nuevos interesados que optan por la versión localizada al momento del registro. **Criterio de éxito: ≥20%.**
- **Puntuación de Confianza Percibida (Trust Perception Score):** Escala Likert 1-5 sobre "siento que esta aplicación fue hecha para mi negocio". **Criterio de éxito: incremento ≥15% frente a la versión estándar.**
---
 
#### Hipótesis 4: Tolerancia a la Latencia de Búsqueda
 
**Question:** ¿Cuál es el umbral de tiempo máximo de búsqueda por nombre común que el usuario tolera antes de frustrarse?
 
**Métricas:**
 
- **Tiempo de Respuesta de Búsqueda (Search Response Time):** Tiempo en segundos desde que el usuario ingresa el término hasta que ve resultados. **Criterio de éxito: <1.5 segundos.**
- **Tasa de Abandono de Tarea (Task Abandonment Rate):** Porcentaje de búsquedas interrumpidas bajo el escenario "atención bajo presión". **Criterio de éxito: abandono significativamente menor en el escalón de 1.5s frente a 3s.**
- **Nivel de Frustración (Frustration Score):** Escala Likert 1-5 reportada tras cada escalón de latencia probado. **Criterio de éxito: ≤2/5 en el escalón de 1.5s.**
---
 
#### Hipótesis 5: Impacto del Alto Contraste
 
**Question:** ¿Mejora significativamente el diseño de alto contraste la velocidad de interpretación de reportes?
 
**Métricas:**
 
- **Tiempo de Identificación (Identification Time):** Segundos requeridos para localizar la fecha de vencimiento de un producto en el reporte. **Criterio de éxito: mejora ≥20% frente a la versión estándar.**
- **Tasa de Error de Lectura (Reading Error Rate):** Porcentaje de respuestas incorrectas al identificar un dato bajo iluminación reducida (<100 lux). **Criterio de éxito: ≤5% en la versión de alto contraste.**
---
 
**Resumen de Métricas por Tipo:**
 
- **Métricas de Eficiencia:** Search Response Time, Identification Time
- **Métricas de Calidad:** Reading Error Rate, Task Abandonment Rate
- **Métricas de Adopción:** Perceived Conversion Rate, Localized Sign-up Rate, Alert Action Rate
- **Métricas de Satisfacción:** Price Fairness Score, Trust Perception Score, Frustration Score
- **Métricas de Impacto Operativo:** Shrinkage Reduction Rate

### 8.2.4. Conditions.

| Question | ¿En qué medida el costo de la suscripción es una barrera frente a las pérdidas actuales por productos vencidos? |
| :--- | :--- |
| **Condición Experimental** | El usuario interactúa con una calculadora de ROI que proyecta el ahorro mensual frente al costo del servicio. |
| **Condición de Control** | El usuario visualiza únicamente el precio de la suscripción sin información comparativa sobre ahorro de mermas. |

---

| Question | ¿La implementación de un historial de lotes reduce efectivamente las pérdidas por vencimiento? |
| :--- | :--- |
| **Condición Experimental** | Los usuarios tienen acceso al módulo de "Lotes Próximos a Vencer" con alertas proactivas configuradas. |
| **Condición de Control** | Los usuarios gestionan sus inventarios sin alertas, confiando en registros manuales o memoria visual. |

---

| Question | ¿Qué tan relevante es el soporte multilingüe para la adopción en mercados con diversidad lingüística? |
| :--- | :--- |
| **Condición Experimental** | Los usuarios acceden a una versión de la interfaz con terminología localizada (ej. idiomas originarios o inglés técnico). |
| **Condición de Control** | Los usuarios acceden a la versión estándar de la aplicación exclusivamente en español. |

---

| Question | ¿Cuál es el umbral de tiempo máximo de búsqueda por nombre común que el usuario tolera antes de frustrarse? |
| :--- | :--- |
| **Condición Experimental** | Los usuarios realizan búsquedas con una latencia optimizada de 1.5 segundos. |
| **Condición de Control** | Los usuarios realizan búsquedas con una latencia artificial elevada de 3 segundos para medir la fricción. |

---

| Question | ¿Mejora significativamente el diseño de alto contraste la velocidad de interpretación de reportes? |
| :--- | :--- |
| **Condición Experimental** | Los usuarios interactúan con el dashboard mediante una paleta de colores de alto contraste bajo iluminación reducida. |
| **Condición de Control** | Los usuarios interactúan con el diseño estándar del dashboard bajo las mismas condiciones de baja iluminación. |

### 8.2.5. Scale Calculations and Decisions.

Para cada hipótesis, definimos una escala de decisión basada en las métricas clave identificadas en la sección 8.2.3. Esta escala determina si los resultados son **ideales** (validan completamente la hipótesis), **aceptables** (validan parcialmente, requieren refinamiento), o **desfavorables** (invalidan la hipótesis, requieren rediseño o descarte de la funcionalidad).
 
---
 
#### Hipótesis 1: Viabilidad del Modelo de Suscripción
 
| Métrica de la Hipótesis | Desfavorable (Fracaso) | Aceptable (Mejora Mínima) | Ideal (Éxito de la Hipótesis) |
| --- | --- | --- | --- |
| **Índice de Justicia de Precio** | < 60% califica "Justo/Barato" | 60-79% | **≥ 80%** |
| **Tasa de Conversión Percibida** | < 50% (menos de 5 de 10) hace clic en "Adquirir Plan" | 50-69% (5-6 de 10) | **≥ 70% (7 de 10)** |
 
**Decisión:**
 
- **Ideal:** El precio se valida tal como está planteado; se aprueba avanzar directamente al desarrollo del flujo de pago.
- **Aceptable:** El precio es viable pero requiere reforzar la narrativa de ahorro (ej. mejorar la calculadora de ROI, agregar testimonios) antes de lanzar el cobro real.
- **Desfavorable:** Se rechaza el precio actual; se requiere replantear el modelo (ej. plan freemium, precio escalonado por tamaño de bodega) antes de continuar.
---
 
#### Hipótesis 2: Eficacia del Historial de Lotes
 
| Métrica de la Hipótesis | Desfavorable (Fracaso) | Aceptable (Mejora Mínima) | Ideal (Éxito de la Hipótesis) |
| --- | --- | --- | --- |
| **Reducción de Mermas Reales** | < 15% | 15-19% | **≥ 20%** |
| **Tasa de Acción sobre Alertas** | < 40% | 40-59% | **≥ 60%** |
 
**Decisión:**
 
- **Ideal:** El módulo de lotes se valida como núcleo de la propuesta de valor; se aprueba para producción sin cambios mayores.
- **Aceptable:** El módulo ayuda, pero no es suficiente por sí solo; se recomienda añadir un canal de alerta más agresivo (ej. notificación a WhatsApp) antes de producción.
- **Desfavorable:** Se rechaza la hipótesis; el problema de raíz no es la visibilidad de fechas sino la falta de tiempo/incentivo para actuar. Requiere rediseño del flujo de alertas o investigación adicional.
---
 
#### Hipótesis 3: Adopción por Localización
 
| Métrica de la Hipótesis | Desfavorable (Fracaso) | Aceptable (Mejora Mínima) | Ideal (Éxito de la Hipótesis) |
| --- | --- | --- | --- |
| **Tasa de Registro Localizado** | < 20% | 20-29% | **≥ 30%** |
| **Incremento en Confianza Percibida** | < 10% | 10-14% | **≥ 15%** |
 
**Decisión:**
 
- **Ideal:** La localización es un driver de adopción claro; se prioriza la internacionalización completa en el roadmap.
- **Aceptable:** Existe interés moderado; se pospone la inversión completa, pero se mantiene la opción de idioma como mejora incremental.
- **Desfavorable:** El idioma no es una barrera crítica; se descarta la internacionalización como prioridad y se reasignan recursos a otras funcionalidades (ej. H1, H2).
---
 
#### Hipótesis 4: Tolerancia a la Latencia de Búsqueda
 
| Métrica de la Hipótesis | Desfavorable (Fracaso) | Aceptable (Mejora Mínima) | Ideal (Éxito de la Hipótesis) |
| --- | --- | --- | --- |
| **Tiempo de Respuesta de Búsqueda** | > 1.5 segundos | 1 - 1.5 segundos | **< 1 segundo** |
| **Nivel de Frustración (escalón 1.5s)** | > 3/5 | 2 - 3/5 | **≤ 2/5** |
 
**Decisión:**
 
- **Ideal:** El rendimiento actual del buscador es suficiente; no se requiere optimización adicional antes del lanzamiento.
- **Aceptable:** El rendimiento es tolerable, pero se recomienda optimizar índices de búsqueda en backend antes de escalar a más usuarios.
- **Desfavorable:** Bloqueante; se requiere rediseño técnico del motor de búsqueda (ej. índices, caché) antes de cualquier lanzamiento, dado que la latencia empuja al usuario de vuelta al cuaderno físico.
---
 
#### Hipótesis 5: Impacto del Alto Contraste
 
| Métrica de la Hipótesis | Desfavorable (Fracaso) | Aceptable (Mejora Mínima) | Ideal (Éxito de la Hipótesis) |
| --- | --- | --- | --- |
| **Mejora en Tiempo de Identificación** | < 20% | 20-24% | **≥ 25%** |
| **Tasa de Error de Lectura (alto contraste)** | > 10% | 5-10% | **≤ 5%** |
 
**Decisión:**
 
- **Ideal:** El rediseño de alto contraste se valida completamente; se aprueba como diseño por defecto de los reportes.
- **Aceptable:** Hay mejora real pero modesta; se mantiene como opción de accesibilidad (toggle) en lugar de reemplazar el diseño estándar.
- **Desfavorable:** El esfuerzo de rediseño no se justifica frente a otras mejoras de usabilidad; se descarta o se prioriza más abajo en el backlog.
---
 
#### Resumen de Criterios de Decisión Global
 
Para determinar si el **conjunto completo de experimentos** justifica avanzar de prototipo/MVP a producto comercial, aplicamos la siguiente regla:
 
- **Avance a Desarrollo Completo Aprobado:** Si **al menos 4 de 5 hipótesis** obtienen resultados "Ideales" o "Aceptables" (con refinamiento menor), el conjunto de experimentos se considera exitoso.
- **Avance Condicional (Requiere Refinamiento):** Si **3 de 5 hipótesis** obtienen "Ideal/Aceptable", pero 2 obtienen "Desfavorable", las funcionalidades que fracasaron deben ser rediseñadas o eliminadas del alcance del MVP inicial.
- **Rechazo / Pivote del Producto:** Si **3 o más hipótesis** obtienen resultados "Desfavorables", el conjunto de experimentos fracasa. Se requiere investigación adicional (entrevistas, análisis de causas raíz) antes de continuar invirtiendo en desarrollo.
**Justificación:**
 
Esta escala de decisión permite un enfoque pragmático: no todas las funcionalidades deben ser perfectas para validar el valor del producto, pero sí debe haber una mayoría clara de validaciones exitosas. Esto es especialmente relevante para H1 (viabilidad del modelo de negocio) y H2 (eficacia del módulo de lotes), que son las hipótesis de mayor riesgo según el scoring de 8.1.4 (Total Score 17 cada una).

### 8.2.6. Methods Selection.
 
Para recolectar los datos de las métricas definidas en la sección 8.2.3 y evaluar los resultados según la escala de decisión de 8.2.5, se seleccionaron los siguientes métodos de experimentación y recolección de datos.
 
---
 
#### Hipótesis 1: Viabilidad del Modelo de Suscripción
 
**Método: Entrevista Guiada con Prototipo (Concierge)**
 
- **Propósito:** medir la disposición a pagar y la percepción de valor del precio.
- **Ejecución:** se entrevista a cada uno de los 10 dueños de bodega mientras interactúan con el prototipo Figma de la calculadora de ROI, registrando si hacen clic en "Adquirir Plan" y su calificación verbal del precio.
- **Herramientas:** Figma, guion de entrevista semiestructurado, planilla de registro de respuestas.
---
 
#### Hipótesis 2: Eficacia del Historial de Lotes
 
**Método: Piloto de Campo sobre Producción Real (Field Trial)**
 
- **Propósito:** medir el impacto real del módulo de lotes sobre las mermas, usando la aplicación ya desplegada en producción en lugar de un entorno aislado.
- **Ejecución:** los 5 "Early Adopters" usan el módulo de lotes directamente en el frontend desplegado ([front-inventiapp.vercel.app](https://front-inventiapp.vercel.app/auth/login)), conectado al backend real en Railway, con cuentas de prueba dedicadas (ver nota de 8.2.4); durante un ciclo completo de inventario (15 días) se compara el conteo de productos vencidos no vendidos contra su registro manual del mes anterior. Adicionalmente, se registrará si cada alerta de "7 días para vencer" deriva en una acción (venta de liquidación o devolución) dentro de las 48 horas siguientes, usando los eventos `batch_alert_triggered` y `batch_alert_action` (ver 8.2.8), para calcular la Tasa de Acción sobre Alertas.
- **Herramientas:** módulo de lotes en producción (Spring Boot/Angular sobre Railway + Vercel), planilla de comparación pre/post.
---
 
#### Hipótesis 3: Adopción por Localización
 
**Método: Prueba de Puerta Falsa (Fake Door / Smoke Test)**
 
- **Propósito:** medir el interés real (no solo declarado) en la versión localizada.
- **Ejecución:** se publica una landing page y una pantalla de inventario traducidas; se mide cuántos de los visitantes de 10 negocios en zonas bilingües completan el registro en la versión localizada vs. la estándar. Al finalizar el registro, se aplicará una encuesta corta (Google Forms) con la pregunta de confianza percibida en escala Likert 1-5 ("siento que esta aplicación fue hecha para mi negocio"), comparando el promedio entre ambas versiones.
- **Herramientas:** landing page bilingüe, formulario de registro, herramienta de analítica web (ej. Google Analytics).
---
 
#### Hipótesis 4: Tolerancia a la Latencia de Búsqueda
 
**Método: Medición de Latencia Real + Network Throttling (Chrome DevTools)**
 
- **Propósito:** identificar el umbral de tiempo de respuesta a partir del cual el usuario se frustra o abandona la tarea, partiendo de la latencia real del sistema desplegado.
- **Ejecución:** primero se mide la latencia base real del endpoint de búsqueda sobre la app desplegada usando la pestaña **Network** de Chrome DevTools (sin throttling). Luego, 8 usuarios realizan búsquedas sobre la misma app real bajo tres escalones de latencia simulados con **Network Throttling** de DevTools (0.5s/1.5s/3s) en un escenario de "atención bajo presión"; se registra tiempo, abandono y frustración reportada.
- **Herramientas:** Chrome DevTools (pestaña Network + Throttling), app real (Vercel + Railway), encuesta Likert post-tarea.
---
 
#### Hipótesis 5: Impacto del Alto Contraste
 
**Método: Test A/B Controlado en Laboratorio**
 
- **Propósito:** cuantificar la mejora real en velocidad de lectura bajo condiciones de baja iluminación.
- **Ejecución:** 6 usuarios resuelven la misma tarea de lectura (encontrar fecha de vencimiento) en ambas versiones del dashboard, en una sala con <100 lux. Además del tiempo, se registrará si la fecha identificada por el usuario fue correcta o incorrecta frente al dato real del reporte, para calcular la Tasa de Error de Lectura en cada versión.
- **Herramientas:** dos versiones del dashboard, cronómetro, luxómetro.
---
 
#### Resumen de Métodos Seleccionados
 
| Método | Hipótesis que Valida | Tipo de Datos | Herramientas Principales |
| --- | --- | --- | --- |
| Entrevista guiada (Concierge) | H1 | Cualitativo/Cuantitativo | Figma, guion de entrevista |
| Piloto de campo sobre producción real | H2 | Cuantitativo | App real (Railway + Vercel), planilla pre/post |
| Fake Door / Smoke Test | H3 | Cuantitativo | Landing page, analítica web |
| Medición de latencia real + Throttling (DevTools) | H4 | Cuantitativo | Chrome DevTools, app real, encuesta Likert |
| Test A/B de laboratorio | H5 | Cuantitativo | Dos versiones del dashboard, luxómetro |
 
**Justificación de la Selección:**
 
- **Entrevista guiada y Fake Door** (H1, H3) usan prototipos/landing pages aisladas porque buscan validar interés antes de comprometer el flujo real de cobro o de registro.
- **Piloto de campo y Medición de Latencia Real** (H2, H4) se ejecutan directamente sobre la aplicación en producción ([backend-stocktrack-production.up.railway.app](https://backend-stocktrack-production.up.railway.app/swagger-ui/index.html) + [front-inventiapp.vercel.app](https://front-inventiapp.vercel.app/auth/login)), ya que ambas dependen de medir comportamiento y rendimiento real del sistema que efectivamente se va a lanzar, no de un sustituto.
- **Test A/B** (H5) se mantiene en prototipo porque la versión de alto contraste todavía no existe como feature desplegada en producción.
- Todos los métodos incluyen una componente de encuesta o entrevista que captura percepción de valor y satisfacción, complementando las métricas cuantitativas de comportamiento.
---
 
#### Comparativa de Herramientas de Medición
 
Adicionalmente, se evaluaron las siguientes herramientas para ejecutar los métodos anteriores, comparando precio, capacidad de análisis, sencillez y ventajas:
 
| Herramienta | Chrome DevTools | Google Forms | Google Analytics | Lighthouse |
| --- | --- | --- | --- | --- |
| **Precio** | Gratuito, integrado en el navegador | Gratuito | Gratuito / créditos gratis | Gratuito, ejecución local o en CI |
| **Capacidad de Análisis** | Medición precisa de latencia de red real y simulación de throttling | Captura de respuestas cualitativas (Likert, abiertas) | Tráfico, conversión y comportamiento de usuarios en landing pages | Performance, Accessibility, Best Practices y SEO de una pantalla específica |
| **Sencillez** | Requiere conocimiento técnico básico (pestaña Network) | Muy sencillo, sin curva de aprendizaje | Aprendizaje sencillo de las métricas principales | Información resumida en puntajes (0-100) por categoría |
| **Ventajas** | Mide la app real sin necesidad de infraestructura adicional; clave para H4 | Recolección rápida de percepción de usuario para H1, H3 y H5 | Mide conversión real (registro) sin instrumentación manual; clave para H3 | Detecta si un mal rendimiento técnico podría contaminar los resultados de H4 y H5 |
 
**Justificación de la selección de herramientas:** se priorizaron herramientas gratuitas y de bajo esfuerzo de configuración, dado que el objetivo de esta fase es validar hipótesis rápidamente sobre la app ya desplegada, sin necesidad de instrumentar todavía un sistema de analítica completo — esa decisión se retoma con mayor profundidad en 8.2.7 y 8.2.8.

### 8.2.7. Data Analytics: Goals, KPIs and Metrics Selection.

Previo al despliegue con usuarios, validamos la estabilidad y eficiencia técnica de nuestra aplicación experimental. Mediante Google Lighthouse, examinamos el rendimiento, la accesibilidad y el cumplimiento de estándares en las secciones más críticas.

**Pantalla: Dashboard**

![Resumen Lighthouse del Dashboard](../assets/img/chapter-VIII/lighthouse-dashboard-overview.png)
 
![Detalle de Performance del Dashboard](../assets/img/chapter-VIII/lighthouse-dashboard-performance.png)
 
**Performance (62):** Puntaje "naranja" (mejorable). El First Contentful Paint y el Largest Contentful Paint se ubican en 3.4s y el Speed Index en 7.6s, valores por encima del umbral de tolerancia de 1.5-2s definido como Condición Experimental para H4 (8.2.4). Esto confirma cuantitativamente el problema de rendimiento señalado en el As-Is (8.1.1).
 
![Detalle de Accessibility del Dashboard](../assets/img/chapter-VIII/lighthouse-dashboard-accessibility.png)
 
**Accessibility (94):** Puntaje alto, pero Lighthouse detecta automáticamente que el contraste entre el fondo y el primer plano no es suficiente, además de la ausencia de un landmark principal en el documento. Este hallazgo es **evidencia técnica directa del problema de bajo contraste** descrito en el As-Is (8.1.1) y valida objetivamente la necesidad del experimento de Hipótesis 5, antes incluso de ejecutar el Test A/B con usuarios.
 
![Detalle de Best Practices del Dashboard](../assets/img/chapter-VIII/lighthouse-dashboard-best-practices.png)
 
**Best Practices (100):** Puntaje perfecto. La aplicación mitiga ataques XSS, aplica aislamiento de origen (COOP) y protección contra clickjacking, sin vulnerabilidades de seguridad evidentes.
 
![Detalle de SEO del Dashboard](../assets/img/chapter-VIII/lighthouse-dashboard-seo.png)
 
**SEO (75):** Aceptable pero poco relevante: el dashboard es una pantalla interna que requiere autenticación, por lo que no necesita ser indexada por motores de búsqueda (de ahí las alertas de `robots.txt` inválido y enlaces no rastreables).

---

**Pantalla: Inventario**
 
![Resumen Lighthouse de Inventario](../assets/img/chapter-VIII/lighthouse-inventario-overview.png)
 
![Detalle de Performance de Inventario](../assets/img/chapter-VIII/lighthouse-inventario-performance.png)
 
**Performance (54):** Es el puntaje más bajo de las dos pantallas auditadas. El FCP y el LCP suben a 6.7s y el Speed Index a 9.6s, casi el doble que en el Dashboard. Dado que esta es precisamente la pantalla donde ocurre la **búsqueda de productos por nombre** (el problema de rendimiento ya identificado en 8.1.1 y el foco de Hipótesis 4), este resultado funciona como **línea base real previa al experimento**: confirma que, incluso sin throttling artificial, la latencia base del sistema ya se acerca al umbral de frustración (>1.5s) definido en la Escala de Decisión de H4 (8.2.5).
 
![Detalle de Accessibility de Inventario](../assets/img/chapter-VIII/lighthouse-inventario-accessibility.png)
 
**Accessibility (95):** Igual que en el Dashboard, se repite la alerta de contraste insuficiente entre fondo y primer plano. Que el mismo issue aparezca en ambas pantallas refuerza que el bajo contraste **no es un caso aislado sino un patrón de diseño transversal** en la aplicación, consistente con la Tarjeta de Experimento 04 e Hipótesis 5.
 
![Detalle de Best Practices de Inventario](../assets/img/chapter-VIII/lighthouse-inventario-best-practices.png)
 
**Best Practices (100):** Puntaje perfecto, con detección correcta de las librerías de JavaScript utilizadas; se señala como mejora menor la ausencia de source maps para JavaScript de primera parte (no crítico para el experimento).
 
![Detalle de SEO de Inventario](../assets/img/chapter-VIII/lighthouse-inventario-seo.png)
 
**SEO (75):** Mismos hallazgos que en el Dashboard (meta descripción ausente, `robots.txt` inválido); poco relevante dado que es una pantalla protegida por login.
 
---

### 8.2.8. Web and Mobile Tracking Plan.

Para recolectar de forma automática los datos cuantitativos definidos en las Métricas (8.2.3) y complementar la auditoría técnica de 8.2.7, se implementará un plan de Event Tracking sobre la aplicación web desplegada, registrando los eventos en una tabla `experiment_events` en el entorno de staging del backend (Spring Boot + Railway).

**No todas las hipótesis generan eventos automatizados.** Siguiendo la misma lógica de los Métodos de 8.2.6, solo se instrumentan las hipótesis que corren sobre **software real y desplegado**:

| Hipótesis | Método (8.2.6) | ¿Corre sobre app real? | ¿Genera eventos en `experiment_events`? |
| :--- | :--- | :---: | :---: |
| H1 — Suscripción | Entrevista guiada sobre **prototipo Figma** | No | No (registro manual) |
| H2 — Historial de Lotes | Piloto de campo sobre **MVP funcional en producción** | Sí | Sí |
| H3 — Localización | **Fake Door** (landing + formulario reales) | Sí | Sí |
| H4 — Latencia de Búsqueda | DevTools Throttling sobre **app real** | Sí | Sí |
| H5 — Alto Contraste | Test A/B en **laboratorio** (cronómetro + luxómetro) | No | No (registro manual) |

---

#### Eventos a Rastrear (Tracking Events)

Se creará una tabla `experiment_events` en la base de datos de staging para registrar las siguientes acciones:

**1. Hipótesis 2: Eficacia del Historial de Lotes**

**Evento: `batch_alert_triggered`**

- **Disparador:** el sistema genera una alerta de "7 días para vencer" durante la verificación diaria.
- **Datos a capturar:**
  - `event_name`: "batch_alert_triggered"
  - `alert_id`: [ID de la alerta generada]
  - `batch_id`: [ID del lote]
  - `user_id`: [ID del dueño de bodega]
  - `timestamp`: Fecha y hora del evento

**Evento: `batch_alert_action`**

- **Disparador:** el usuario registra la acción de mitigación (liquidación o devolución) sobre una alerta. El cruce entre este evento y `batch_alert_triggered` (dentro de la ventana de 48h) calcula la **Alert Action Rate** (8.2.3).
- **Datos a capturar:**
  - `event_name`: "batch_alert_action"
  - `alert_id`: [ID de la alerta atendida]
  - `batch_id`: [ID del lote]
  - `user_id`: [ID del dueño de bodega]
  - `action_type`: ["liquidacion" o "devolucion"]
  - `timestamp`: Fecha y hora del evento

**Evento: `batch_history_viewed`**

- **Disparador:** el usuario consulta el historial de entradas/salidas de un lote.
- **Datos a capturar:**
  - `event_name`: "batch_history_viewed"
  - `batch_id`: [ID del lote consultado]
  - `user_id`: [ID del dueño de bodega]
  - `timestamp`: Fecha y hora del evento

---

**2. Hipótesis 3: Adopción por Localización (Fake Door)**

**Evento: `localized_signup_completed`**

- **Disparador:** un visitante completa el registro en la landing page o pantalla de inventario traducida (Fake Door, 8.2.6).
- **Datos a capturar:**
  - `event_name`: "localized_signup_completed"
  - `session_id`: [identificador de sesión del visitante]
  - `variant`: ["localizada" o "estandar"]
  - `timestamp`: Fecha y hora del evento

---

**3. Hipótesis 4: Tolerancia a la Latencia de Búsqueda**

**Evento: `product_search_performed`**

- **Disparador:** cada búsqueda de producto por nombre común ejecutada en la pantalla de Inventario, ya sea en condiciones normales o durante las sesiones con Network Throttling.
- **Datos a capturar:**
  - `event_name`: "product_search_performed"
  - `user_id`: [ID del dueño de bodega]
  - `response_time_ms`: [tiempo medido entre el ingreso del término y la respuesta]
  - `result_count`: [cantidad de coincidencias devueltas]
  - `timestamp`: Fecha y hora del evento

**Evento: `search_task_abandoned`**

- **Disparador:** el usuario abandona la búsqueda antes de recibir resultados.
- **Datos a capturar:**
  - `event_name`: "search_task_abandoned"
  - `user_id`: [ID del dueño de bodega]
  - `elapsed_time_ms`: [tiempo transcurrido antes del abandono]
  - `timestamp`: Fecha y hora del evento

---

#### Captura de Datos para Hipótesis 1 y 5 (sin eventos automatizados)

Como se explicó, H1 y H5 se validan sobre un prototipo Figma y un test de laboratorio, por lo que sus datos **no** pasan por `experiment_events`: se registran manualmente en una planilla (Google Sheets).

| Hipótesis | Dónde se registra | Campos capturados |
| :--- | :--- | :--- |
| H1 | Planilla de entrevista guiada | `usuario_id`, `clic_adquirir_plan` (sí/no), `calificacion_precio`, `perdida_estimada_usd` |
| H5 | Planilla de laboratorio | `usuario_id`, `version` (estándar/alto contraste), `tiempo_identificacion_seg`, `respuesta_correcta` (sí/no) |

---

#### Estructura de la Tabla `experiment_events`

```sql
CREATE TABLE experiment_events (
    event_id BIGINT AUTO_INCREMENT PRIMARY KEY,
    event_name VARCHAR(50) NOT NULL,
    user_id BIGINT,
    session_id VARCHAR(100),
    payload JSON,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    INDEX idx_event_name (event_name),
    INDEX idx_user_id (user_id),
    INDEX idx_created_at (created_at)
);
```

#### Herramienta de Análisis

Los datos se almacenarán en `experiment_events` y se consultarán mediante SQL para alimentar los reportes de las hipótesis que sí corren sobre software real.

**Ejemplo de Queries SQL:**

- **Alert Action Rate (H2) — % de alertas atendidas dentro de 48h:**

```sql
SELECT
    COUNT(DISTINCT t.payload->>'$.alert_id') AS alertas_generadas,
    COUNT(DISTINCT a.payload->>'$.alert_id') AS alertas_atendidas_48h,
    ROUND(
        COUNT(DISTINCT a.payload->>'$.alert_id') * 100.0
        / COUNT(DISTINCT t.payload->>'$.alert_id'), 1
    ) AS alert_action_rate_pct
FROM experiment_events t
LEFT JOIN experiment_events a
    ON a.event_name = 'batch_alert_action'
    AND a.payload->>'$.alert_id' = t.payload->>'$.alert_id'
    AND a.created_at <= t.created_at + INTERVAL 48 HOUR
WHERE t.event_name = 'batch_alert_triggered';
```

#### Herramienta de Análisis

Los datos se almacenarán en `experiment_events` y se consultarán mediante SQL para alimentar los reportes de las hipótesis que sí corren sobre software real.

**Ejemplo de Queries SQL:**

- **Search Response Time promedio (H4):**

```sql
SELECT AVG(CAST(payload->>'$.response_time_ms' AS UNSIGNED)) AS avg_response_time_ms
FROM experiment_events
WHERE event_name = 'product_search_performed'
  AND created_at BETWEEN '2026-01-01' AND '2026-01-31';
```

#### Herramienta de Análisis

Los datos se almacenarán en `experiment_events` y se consultarán mediante SQL para alimentar los reportes de las hipótesis que sí corren sobre software real.

**Ejemplo de Queries SQL:**

- **Search Response Time promedio (H4):**

```sql
SELECT AVG(CAST(payload->>'$.response_time_ms' AS UNSIGNED)) AS avg_response_time_ms
FROM experiment_events
WHERE event_name = 'product_search_performed'
  AND created_at BETWEEN '2026-01-01' AND '2026-01-31';
```

- **Search Response Time promedio (H4):**

```sql
SELECT
    payload->>'$.variant' AS variante,
    COUNT(*) AS registros_completados
FROM experiment_events
WHERE event_name = 'localized_signup_completed'
GROUP BY payload->>'$.variant';
```

Estos datos cuantitativos se complementarán con los datos cualitativos obtenidos de las entrevistas y encuestas para generar el análisis completo de resultados.

## 8.3. Experimentation
La fase de experimentación traduce los aprendizajes en validación (definidos como hipótesis en 8.2) en requerimientos concretos para el siguiente ciclo. A diferencia de las User Stories del estado **As-Is** (sección 3.2), las **To-Be User Stories** representan únicamente los *incrementos* que el equipo decidió construir como resultado del proceso de Experiment-Driven Development. Por ello no reescriben funcionalidad ya existente (ej. el registro de lotes de US14, la búsqueda de US08 o las notificaciones de US05), sino que la extienden con las mejoras que cada experimento busca validar. Cada historia es trazable a una de las cinco hipótesis de 8.2.1 y a su Tarjeta de Experimento (8.1.5).

#### Épicas incorporadas (extensión de la sección 3.2)

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
  <thead>
    <tr>
      <th style="width:10%;">Epic ID</th>
      <th style="width:20%;">Título</th>
      <th style="width:55%;">Descripción</th>
      <th style="width:15%;">HUs asociadas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>EP-11</td>
      <td>Monetización y Suscripción</td>
      <td>Como dueño de bodega, quiero evaluar el ahorro por mermas frente al costo del plan y contratar una suscripción, para acceder a las funcionalidades premium con una decisión de valor informada.</td>
      <td>US20, US21, TS15</td>
    </tr>
    <tr>
      <td>EP-12</td>
      <td>Internacionalización y Localización</td>
      <td>Como usuario de una zona con diversidad lingüística, quiero usar la plataforma con terminología localizada o en un idioma originario, para reducir la barrera de "tecnología ajena" y adoptarla con confianza. Se alinea con el requisito de i18n del enunciado.</td>
      <td>US23, TS18</td>
    </tr>
  </tbody>
</table>

### 8.3.1. To-Be User Stories.
<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">US15</td>
        <td align="center">Dueño de bodega</td>
        <td align="center">Alta</td>
        <td align="center">EP-01</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Optimizar la búsqueda de productos por nombre común</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> dueño de bodega <br>
            <strong> Quiero </strong> que la búsqueda de productos por nombre común responda casi de inmediato <br>
            <strong> Para </strong> atender al cliente sin interrumpir la venta ni volver al registro manual.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Respuesta dentro del umbral de tolerancia</strong> <br><br>
            <strong> Dado que </strong> existen productos registrados en el inventario <br>
            <strong> Cuando </strong> el usuario busca un producto por su nombre común <br>
            <strong> Entonces </strong> el sistema devuelve los resultados coincidentes en menos de 1.5 segundos.
            <br><br>
            <strong> Escenario 2: Coincidencia parcial o aproximada</strong> <br><br>
            <strong> Dado que </strong> el usuario ingresa un nombre incompleto o con un error de tipeo menor <br>
            <strong> Cuando </strong> se procesa la búsqueda <br>
            <strong> Entonces </strong> el sistema muestra los productos cuyo nombre coincide de forma parcial o aproximada.
            <br><br>
            <strong> Escenario 3: Búsqueda sin resultados</strong> <br><br>
            <strong> Dado que </strong> el término buscado no corresponde a ningún producto <br>
            <strong> Cuando </strong> se procesa la búsqueda <br>
            <strong> Entonces </strong> el sistema informa la ausencia de coincidencias dentro del mismo umbral de tiempo.
        </td>
    </tr>
</table>

<p><em>Trazabilidad: Hipótesis 4 (Tolerancia a la Latencia de Búsqueda) — QD2.</em></p>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">US16</td>
        <td align="center">Dueño de bodega</td>
        <td align="center">Media</td>
        <td align="center">EP-07</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Visualizar reportes en modo de alto contraste</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> dueño de bodega <br>
            <strong> Quiero </strong> activar un modo de alto contraste en los reportes <br>
            <strong> Para </strong> leer los datos críticos sin errores en almacenes con poca iluminación o con fatiga visual.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Activación del modo de alto contraste</strong> <br><br>
            <strong> Dado que </strong> el usuario visualiza un reporte de inventario <br>
            <strong> Cuando </strong> activa el modo de alto contraste <br>
            <strong> Entonces </strong> el sistema presenta el reporte con la paleta de alto contraste.
            <br><br>
            <strong> Escenario 2: Persistencia de la preferencia</strong> <br><br>
            <strong> Dado que </strong> el usuario activó previamente el modo de alto contraste <br>
            <strong> Cuando </strong> vuelve a ingresar al sistema <br>
            <strong> Entonces </strong> el sistema conserva el modo de alto contraste como preferencia del usuario.
        </td>
    </tr>
</table>

<p><em>Trazabilidad: Hipótesis 5 (Impacto del Alto Contraste) — QD3. Según la decisión "Aceptable" de 8.2.5, se implementa como opción de accesibilidad y no como reemplazo del diseño estándar.</em></p>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">US17</td>
        <td align="center">Dueño de bodega</td>
        <td align="center">Alta</td>
        <td align="center">EP-06</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Registrar acción de mitigación sobre alertas de vencimiento próximo</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> dueño de bodega <br>
            <strong> Quiero </strong> recibir una alerta anticipada cuando un lote está próximo a vencer y registrar la acción que tomo <br>
            <strong> Para </strong> actuar a tiempo y dar seguimiento a la efectividad de las alertas.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Generación de alerta anticipada (7 días)</strong> <br><br>
            <strong> Dado que </strong> existe un lote cuya fecha de vencimiento ocurre dentro de 7 días <br>
            <strong> Cuando </strong> el sistema ejecuta la verificación diaria de vencimientos <br>
            <strong> Entonces </strong> el sistema genera una alerta de vencimiento próximo para ese lote.
            <br><br>
            <strong> Escenario 2: Registro de la acción de mitigación</strong> <br><br>
            <strong> Dado que </strong> el usuario atiende una alerta de vencimiento próximo <br>
            <strong> Cuando </strong> registra la acción tomada (liquidación o devolución al proveedor) <br>
            <strong> Entonces </strong> el sistema asocia la acción y su fecha a la alerta y la marca como atendida.
            <br><br>
            <strong> Escenario 3: Alerta sin atención</strong> <br><br>
            <strong> Dado que </strong> una alerta de vencimiento próximo no recibe ninguna acción dentro de 48 horas <br>
            <strong> Cuando </strong> transcurre dicho plazo <br>
            <strong> Entonces </strong> el sistema mantiene la alerta como pendiente para su seguimiento.
        </td>
    </tr>
</table>

<p><em>Trazabilidad: Hipótesis 2 (Eficacia del Historial de Lotes) — QD1. Sustenta la métrica Alert Action Rate (8.2.3) y los eventos batch_alert_triggered / batch_alert_action (8.2.6).</em></p>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">US18</td>
        <td align="center">Dueño de bodega</td>
        <td align="center">Alta</td>
        <td align="center">EP-02</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Consultar el historial de movimientos por lote</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> dueño de bodega <br>
            <strong> Quiero </strong> consultar el historial de entradas y salidas de cada lote <br>
            <strong> Para </strong> hacer trazabilidad detallada y entender por qué un producto llegó a vencerse.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Consulta del historial de un lote</strong> <br><br>
            <strong> Dado que </strong> un lote registra movimientos de entrada y salida <br>
            <strong> Cuando </strong> el usuario consulta el detalle de ese lote <br>
            <strong> Entonces </strong> el sistema muestra los movimientos en orden cronológico con su fecha y cantidad.
            <br><br>
            <strong> Escenario 2: Lote sin movimientos de salida</strong> <br><br>
            <strong> Dado que </strong> un lote solo registra su ingreso inicial <br>
            <strong> Cuando </strong> el usuario consulta su historial <br>
            <strong> Entonces </strong> el sistema muestra únicamente el movimiento de entrada.
        </td>
    </tr>
</table>

<p><em>Trazabilidad: Hipótesis 2 (Eficacia del Historial de Lotes) — QD1.</em></p>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">US19</td>
        <td align="center">Dueño de bodega</td>
        <td align="center">Media</td>
        <td align="center">EP-06</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Recibir alertas de vencimiento por WhatsApp</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> dueño de bodega <br>
            <strong> Quiero </strong> recibir las alertas de vencimiento próximo en WhatsApp <br>
            <strong> Para </strong> enterarme durante la jornada sin depender de revisar la aplicación.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Habilitación del canal de WhatsApp</strong> <br><br>
            <strong> Dado que </strong> el usuario registra y verifica un número de WhatsApp <br>
            <strong> Cuando </strong> guarda su preferencia de notificación <br>
            <strong> Entonces </strong> el sistema habilita el envío de alertas por ese canal.
            <br><br>
            <strong> Escenario 2: Envío de alerta por WhatsApp</strong> <br><br>
            <strong> Dado que </strong> el usuario tiene el canal de WhatsApp habilitado <br>
            <strong> Cuando </strong> se genera una alerta de vencimiento próximo <br>
            <strong> Entonces </strong> el sistema envía un mensaje con el producto afectado y los días restantes.
        </td>
    </tr>
</table>

<p><em>Trazabilidad: Hipótesis 2 (Eficacia del Historial de Lotes) — QD1. Canal de refuerzo previsto en el escenario "Aceptable" de la decisión de 8.2.5; coherente con EP-06, que ya contempla canales externos de notificación.</em></p>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">US20</td>
        <td align="center">Dueño de bodega</td>
        <td align="center">Alta</td>
        <td align="center">EP-11</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Estimar el ahorro por mermas frente al costo de la suscripción</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> dueño de bodega <br>
            <strong> Quiero </strong> comparar mis pérdidas estimadas por mermas con el costo del plan <br>
            <strong> Para </strong> decidir de forma informada si la suscripción representa un ahorro.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Cálculo del ahorro proyectado</strong> <br><br>
            <strong> Dado que </strong> el usuario ingresa una estimación de sus mermas mensuales <br>
            <strong> Cuando </strong> el sistema procesa el dato <br>
            <strong> Entonces </strong> el sistema muestra la pérdida estimada contrastada con el costo mensual del plan.
            <br><br>
            <strong> Escenario 2: Resultado favorable a la suscripción</strong> <br><br>
            <strong> Dado que </strong> la merma estimada supera el costo del plan <br>
            <strong> Cuando </strong> el sistema presenta la comparativa <br>
            <strong> Entonces </strong> el sistema destaca el ahorro neto proyectado y habilita la contratación del plan.
        </td>
    </tr>
</table>

<p><em>Trazabilidad: Hipótesis 1 (Viabilidad del Modelo de Suscripción) — QB1. Sustenta la métrica Perceived Conversion Rate (8.2.3).</em></p>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">US21</td>
        <td align="center">Dueño de bodega</td>
        <td align="center">Alta</td>
        <td align="center">EP-11</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Contratar y gestionar el plan de suscripción</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> dueño de bodega <br>
            <strong> Quiero </strong> contratar y administrar mi plan de suscripción <br>
            <strong> Para </strong> acceder a las funcionalidades premium de la plataforma.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Contratación del plan</strong> <br><br>
            <strong> Dado que </strong> el usuario decide suscribirse <br>
            <strong> Cuando </strong> completa el proceso de pago con datos válidos <br>
            <strong> Entonces </strong> el sistema activa la suscripción y habilita las funcionalidades premium.
            <br><br>
            <strong> Escenario 2: Consulta del estado de la suscripción</strong> <br><br>
            <strong> Dado que </strong> el usuario tiene una suscripción activa <br>
            <strong> Cuando </strong> consulta su plan <br>
            <strong> Entonces </strong> el sistema muestra el plan vigente y la fecha de próxima renovación.
            <br><br>
            <strong> Escenario 3: Cancelación de la renovación</strong> <br><br>
            <strong> Dado que </strong> el usuario tiene una suscripción activa <br>
            <strong> Cuando </strong> solicita cancelar la renovación <br>
            <strong> Entonces </strong> el sistema conserva el acceso hasta el término del ciclo ya pagado.
        </td>
    </tr>
</table>

<p><em>Trazabilidad: Hipótesis 1 (Viabilidad del Modelo de Suscripción) — QB1.</em></p>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">US22</td>
        <td align="center">Dueño de bodega</td>
        <td align="center">Media</td>
        <td align="center">EP-07</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Visualizar el ahorro real por mermas evitadas</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> dueño de bodega <br>
            <strong> Quiero </strong> ver el ahorro generado por las alertas de vencimiento que atendí <br>
            <strong> Para </strong> confirmar el valor que aporta la plataforma frente a su costo.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Ahorro acumulado del periodo</strong> <br><br>
            <strong> Dado que </strong> el usuario atendió alertas de vencimiento durante un ciclo de inventario <br>
            <strong> Cuando </strong> consulta el reporte de ahorro por mermas <br>
            <strong> Entonces </strong> el sistema muestra el valor de los productos liquidados o devueltos a tiempo gracias a las alertas.
            <br><br>
            <strong> Escenario 2: Comparativa con periodo anterior</strong> <br><br>
            <strong> Dado que </strong> existe un registro de mermas de un periodo previo <br>
            <strong> Cuando </strong> el usuario consulta el reporte <br>
            <strong> Entonces </strong> el sistema muestra la variación porcentual de mermas respecto a dicho periodo.
        </td>
    </tr>
</table>

<p><em>Trazabilidad: Hipótesis 1 (QB1) e Hipótesis 2 (QD1). Conecta la reducción de mermas con la percepción de valor del precio; se apoya en los read models de reportes (TS04).</em></p>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">US23</td>
        <td align="center">Dueño de bodega</td>
        <td align="center">Baja</td>
        <td align="center">EP-12</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Seleccionar el idioma de la interfaz</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> dueño de bodega de una zona con diversidad lingüística <br>
            <strong> Quiero </strong> usar la plataforma con terminología localizada o en un idioma originario <br>
            <strong> Para </strong> adoptar la herramienta con confianza y reducir la barrera de "tecnología ajena".
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Selección de idioma</strong> <br><br>
            <strong> Dado que </strong> el sistema ofrece más de un idioma disponible <br>
            <strong> Cuando </strong> el usuario selecciona un idioma <br>
            <strong> Entonces </strong> el sistema presenta la interfaz con la terminología del idioma elegido.
            <br><br>
            <strong> Escenario 2: Persistencia del idioma</strong> <br><br>
            <strong> Dado que </strong> el usuario seleccionó un idioma distinto al predeterminado <br>
            <strong> Cuando </strong> vuelve a ingresar a la plataforma <br>
            <strong> Entonces </strong> el sistema conserva el idioma seleccionado.
        </td>
    </tr>
</table>

<p><em>Trazabilidad: Hipótesis 3 (Adopción por Localización) — QB2. Sustenta las métricas Localized Sign-up Rate y Trust Perception Score (8.2.3) y el requisito de i18n del enunciado.</em></p>

### To-Be Technical Stories

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">TS15</td>
        <td align="center">Desarrollador</td>
        <td align="center">Alta</td>
        <td align="center">EP-11</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Endpoints de gestión de suscripción y pago</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> desarrollador <br>
            <strong> Quiero </strong> implementar servicios de suscripción y pago <br>
            <strong> Para </strong> habilitar la contratación de planes y el control del estado de la suscripción.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Activación de suscripción</strong> <br><br>
            <strong> Dado que </strong> se confirma un pago válido <br>
            <strong> Cuando </strong> se procesa la transacción de suscripción <br>
            <strong> Entonces </strong> el sistema registra el plan activo del usuario y su fecha de renovación.
            <br><br>
            <strong> Escenario 2: Consulta de estado</strong> <br><br>
            <strong> Dado que </strong> un usuario tiene una suscripción registrada <br>
            <strong> Cuando </strong> se solicita su estado <br>
            <strong> Entonces </strong> el sistema devuelve el plan vigente y su vigencia.
        </td>
    </tr>
</table>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">TS16</td>
        <td align="center">Desarrollador</td>
        <td align="center">Media</td>
        <td align="center">EP-06</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Servicio de notificaciones por WhatsApp</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> desarrollador <br>
            <strong> Quiero </strong> integrar un servicio de envío de mensajes por WhatsApp <br>
            <strong> Para </strong> entregar las alertas de vencimiento por un canal externo.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Envío de alerta</strong> <br><br>
            <strong> Dado que </strong> se genera una alerta de vencimiento próximo y el usuario tiene el canal habilitado <br>
            <strong> Cuando </strong> el sistema procesa la notificación <br>
            <strong> Entonces </strong> el servicio envía el mensaje al número verificado y registra el resultado del envío.
        </td>
    </tr>
</table>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">TS17</td>
        <td align="center">Desarrollador</td>
        <td align="center">Alta</td>
        <td align="center">EP-01</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Optimización del índice de búsqueda de productos</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> desarrollador <br>
            <strong> Quiero </strong> optimizar el índice de búsqueda por nombre <br>
            <strong> Para </strong> que las consultas respondan por debajo del umbral de latencia definido.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Consulta bajo umbral</strong> <br><br>
            <strong> Dado que </strong> existe un volumen de productos representativo <br>
            <strong> Cuando </strong> se ejecuta una búsqueda por nombre <br>
            <strong> Entonces </strong> el servicio devuelve los resultados en menos de 1.5 segundos.
            <br><br>
            <strong> Escenario 2: Coincidencia parcial</strong> <br><br>
            <strong> Dado que </strong> el término ingresado es parcial o aproximado <br>
            <strong> Cuando </strong> se procesa la consulta <br>
            <strong> Entonces </strong> el servicio aplica coincidencia parcial sin degradar el tiempo de respuesta.
        </td>
    </tr>
</table>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">TS18</td>
        <td align="center">Desarrollador</td>
        <td align="center">Baja</td>
        <td align="center">EP-12</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Servicio de internacionalización (i18n)</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> desarrollador <br>
            <strong> Quiero </strong> implementar el soporte de internacionalización (i18n) <br>
            <strong> Para </strong> servir los textos de la interfaz según el idioma seleccionado.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Entrega de recursos por idioma</strong> <br><br>
            <strong> Dado que </strong> el usuario selecciona un idioma soportado <br>
            <strong> Cuando </strong> solicita una vista de la aplicación <br>
            <strong> Entonces </strong> el sistema entrega los textos en el idioma correspondiente.
        </td>
    </tr>
</table>

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>Story ID</th>
        <th>User</th>
        <th>Priority</th>
        <th>Epic</th>
    </tr>
    <tr>
        <td align="center">TS19</td>
        <td align="center">Desarrollador</td>
        <td align="center">Alta</td>
        <td align="center">EP-06</td>
    </tr>
    <tr>
        <th>Title</th>
        <td colspan="3">Endpoints de acción y telemetría de alertas de lote</td>
    </tr>
    <tr>
        <th colspan="4">Description</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Como </strong> desarrollador <br>
            <strong> Quiero </strong> exponer servicios para registrar la acción sobre las alertas de vencimiento y emitir sus eventos de telemetría <br>
            <strong> Para </strong> habilitar el cálculo del Alert Action Rate y el plan de tracking del experimento.
        </td>
    </tr>
    <tr>
        <th colspan="4">Acceptance Criteria</th>
    </tr>
    <tr>
        <td colspan="4">
            <strong> Escenario 1: Registro de acción</strong> <br><br>
            <strong> Dado que </strong> existe una alerta de vencimiento próximo <br>
            <strong> Cuando </strong> el usuario registra una acción de mitigación <br>
            <strong> Entonces </strong> el sistema asocia la acción y emite el evento batch_alert_action.
            <br><br>
            <strong> Escenario 2: Emisión del disparo de alerta</strong> <br><br>
            <strong> Dado que </strong> el sistema genera una alerta a 7 días del vencimiento <br>
            <strong> Cuando </strong> se crea la alerta <br>
            <strong> Entonces </strong> el sistema emite el evento batch_alert_triggered con su marca de tiempo.
        </td>
    </tr>
</table>

### 8.3.2. To-Be Product Backlog
El backlog prioriza según el scoring del Question Backlog (8.1.4): primero los incrementos de las hipótesis de mayor riesgo (QD1 y QB1, 17 pts), luego rendimiento (QD2, 15), accesibilidad (QD3, 12) y localización (QB2, 10).

| # Orden | User Story Id | Título | Descripción | Story Points |
| :------ | :------------ | :----- | :---------- | :----------- |
| **01** | US17 | Registrar acción de mitigación sobre alertas de vencimiento próximo | Como dueño de bodega, quiero recibir una alerta anticipada de 7 días cuando un lote está próximo a vencer y registrar la acción que tomo, para actuar a tiempo y medir la efectividad de las alertas. | 5 |
| **02** | US18 | Consultar el historial de movimientos por lote | Como dueño de bodega, quiero consultar el historial de entradas y salidas de cada lote, para hacer trazabilidad detallada y entender por qué un producto llegó a vencerse. | 3 |
| **03** | US20 | Estimar el ahorro por mermas frente al costo de la suscripción | Como dueño de bodega, quiero comparar mis pérdidas estimadas por mermas con el costo del plan, para decidir de forma informada si la suscripción representa un ahorro. | 3 |
| **04** | US21 | Contratar y gestionar el plan de suscripción | Como dueño de bodega, quiero contratar y administrar mi plan de suscripción, para acceder a las funcionalidades premium de la plataforma. | 8 |
| **05** | US15 | Optimizar la búsqueda de productos por nombre común | Como dueño de bodega, quiero que la búsqueda por nombre común responda en menos de 1.5 segundos, para atender al cliente sin interrumpir la venta ni volver al registro manual. | 5 |
| **06** | US22 | Visualizar el ahorro real por mermas evitadas | Como dueño de bodega, quiero ver el ahorro generado por las alertas de vencimiento que atendí, para confirmar el valor que aporta la plataforma frente a su costo. | 3 |
| **07** | US16 | Visualizar reportes en modo de alto contraste | Como dueño de bodega, quiero activar un modo de alto contraste en los reportes, para leer los datos críticos sin errores en almacenes con poca iluminación o con fatiga visual. | 3 |
| **08** | US19 | Recibir alertas de vencimiento por WhatsApp | Como dueño de bodega, quiero recibir las alertas de vencimiento próximo en WhatsApp, para enterarme durante la jornada sin depender de revisar la aplicación. | 8 |
| **09** | US23 | Seleccionar el idioma de la interfaz | Como dueño de bodega de una zona con diversidad lingüística, quiero usar la plataforma con terminología localizada o en un idioma originario, para adoptar la herramienta con confianza. | 5 |
