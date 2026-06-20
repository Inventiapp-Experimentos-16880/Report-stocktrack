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

### 8.2.6. Methods Selection.

### 8.2.7. Data Analytics: Goals, KPIs and Metrics Selection.

### 8.2.8. Web and Mobile Tracking Plan.

## 8.3. Experimentation

### 8.3.1. To-Be User Stories.

### 8.3.2. To-Be Product Backlog
