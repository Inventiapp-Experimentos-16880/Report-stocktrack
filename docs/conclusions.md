## Conclusiones

El proyecto logró implementar una arquitectura frontend–backend desacoplada, con un backend RESTful en Java y un frontend en Angular desplegados en entornos separados. Esta decisión facilita la escalabilidad, la integración futura con otros servicios y la adopción de prácticas de despliegue continuo, mientras que la documentación mediante Swagger mejoró la trazabilidad entre endpoints y funcionalidades, asegurando coherencia entre la capa de presentación y la lógica de negocio.

La base de datos se diseñó bajo un enfoque relacional normalizado, lo que permitió mantener la integridad referencial y reducir la redundancia en el manejo de productos, lotes y proveedores. No obstante, se identifican oportunidades de optimización a nivel de índices y consultas, especialmente en operaciones de lectura intensiva asociadas a reportes de inventario e historiales, que serán clave para sostener el rendimiento a medida que crezca el volumen de datos.

De forma complementaria, la incorporación sistemática de las opiniones de los usuarios durante el desarrollo fue determinante para ajustar tanto los requerimientos funcionales como los detalles de interacción de la página. La retroalimentación sobre pantallas confusas, prioridades de información y acciones más frecuentes permitió priorizar funcionalidades, simplificar flujos y corregir problemas de usabilidad que no eran evidentes desde una perspectiva exclusivamente técnica, alineando mejor la solución con las necesidades reales de quienes la utilizarán.

Como resultado de este ciclo iterativo, se logró construir una interfaz funcional que cumple con el objetivo principal del proyecto: permitir a los usuarios gestionar su información y completar sus tareas de manera clara y eficiente. La organización de la navegación, la disposición de los elementos en pantalla y el comportamiento del sistema frente a las acciones del usuario (mensajes, validaciones y estados de carga) hacen posible completar de inicio a fin los flujos críticos definidos, lo que demuestra que el prototipo alcanzó un nivel de usabilidad suficiente para ser utilizado en un contexto real o servir como base sólida para futuras mejoras.

### Conclusiones de los Experimentos de Validación (Hipótesis)

En base a la fase de experimentación técnica y de usuario descrita en el Capítulo VIII, se exponen las conclusiones específicas para cada una de las hipótesis validadas en el proyecto:

* **Hipótesis 1: Viabilidad del Modelo de Suscripción**
  * **Qué se realizó:** Se llevó a cabo una evaluación de tipo *Concierge* mediante entrevistas guiadas con 10 usuarios potenciales utilizando un prototipo interactivo en Figma. El prototipo incluía una calculadora de ROI diseñada para proyectar el ahorro mensual estimado por mermas en comparación directa con el costo de la suscripción premium.
  * **Conclusión:** La hipótesis fue **validada con éxito**. El 70% de los usuarios piloto hicieron clic en "Adquirir Plan" tras comprender el retorno de inversión y el ahorro neto proyectado, considerando que la tarifa era justa en comparación con sus pérdidas históricas de inventario. Esto aprueba el desarrollo del flujo de pago en el roadmap.

* **Hipótesis 2: Eficacia del Historial de Lotes**
  * **Qué se realizó:** Se desarrolló y desplegó un piloto funcional en producción (entornos Railway y Vercel) durante un ciclo experimental de 15 días. Se comparó el comportamiento de un grupo experimental con acceso al módulo de "Lotes Próximos a Vencer" y alertas automáticas a 7 días, frente a un grupo de control sin alertas que gestionaba su stock de forma convencional.
  * **Conclusión:** Se alcanzó un resultado **ideal (validado)**. La visibilidad activa y las alertas redujeron las mermas reales de inventario en más del 20% y lograron una tasa de acción sobre las alertas superior al 60% dentro de las primeras 48 horas de emisión. Se ratifica que este módulo representa el núcleo principal de la propuesta de valor del producto.

* **Hipótesis 3: Adopción por Localización**
  * **Qué se realizó:** Se implementó una prueba de tipo *Fake Door* a través de una landing page con un formulario de registro que permitía seleccionar una versión de interfaz localizada (idiomas originarios o inglés técnico) versus la versión estándar. El interés inicial y el tráfico de los usuarios fueron monitoreados cuantitativamente con herramientas de analítica web.
  * **Conclusión:** Obtuvo un resultado **aceptable / de validación parcial**. Aunque más del 20% de los nuevos registrados seleccionaron la versión localizada, el incremento neto de la confianza percibida no superó el 15% en comparación con la versión estándar. Por ello, se concluye posponer la inversión de una internacionalización completa inmediata y mantener la localización como una mejora incremental a mediano plazo en el backlog.

* **Hipótesis 4: Tolerancia a la Latencia de Búsqueda**
  * **Qué se realizó:** Se sometió a 8 usuarios reales a tareas repetitivas de búsqueda de inventario bajo tres niveles de latencia simulados mediante *Network Throttling* en Chrome DevTools (0.5s, 1.5s y 3.0s) en un escenario simulado de atención al cliente bajo presión comercial.
  * **Conclusión:** La hipótesis fue **validada**. Se identificó que el umbral de tolerancia máximo aceptable para evitar el abandono de la tarea y mantener el nivel de frustración bajo ($\le 2/5$ en escala Likert) es de 1.5 segundos. Latencias mayores (como la de 3 segundos o el rendimiento de la línea base técnica inicial de 1.7s en LCP medida en Lighthouse) disparan el abandono y empujan al usuario a regresar a los registros físicos. Esto fundamenta la optimización prioritaria de índices y caché en la arquitectura definitiva.

* **Hipótesis 5: Impacto del Alto Contraste**
  * **Qué se realizó:** Se realizó un test A/B controlado en laboratorio con 6 usuarios en una sala con iluminación reducida ($< 100$ lux). Se midió la velocidad de lectura (tiempo de identificación de fechas de vencimiento de lotes) y la tasa de errores cometidos al comparar la versión de pantalla de Reportes estándar frente a la nueva versión mejorada con paleta de alto contraste.
  * **Conclusión:** Se validó con un resultado **ideal**. El rediseño de alto contraste redujo el tiempo de lectura e interpretación de datos críticos en un 25% y mantuvo la tasa de error por debajo del 5% bajo condiciones de poca luz. El modo de alto contraste se confirma como la solución directa para mitigar la fatiga visual y los errores operativos en almacenes oscuros, por lo que se implementará como un toggle de accesibilidad.

## Recomendaciones

A partir de lo logrado, se recomienda institucionalizar la recolección de feedback de usuarios como parte del ciclo de desarrollo (por ejemplo, pruebas de usabilidad periódicas o encuestas dentro de la propia página). Esto permitiría seguir refinando la experiencia, detectar tempranamente nuevos problemas de uso y orientar las próximas mejoras en función de evidencia y no solo de supuestos del equipo.

También se recomienda evolucionar la interfaz hacia un diseño más consistente y escalable, adoptando un sistema de diseño (design system) o biblioteca de componentes reutilizables. Con ello se facilitaría mantener coherencia visual entre módulos, acelerar el desarrollo de nuevas pantallas y asegurar que, a medida que la página crezca en funcionalidades, se conserve la misma lógica de interacción que los usuarios ya aprendieron durante esta primera versión.

<div style="page-break-after: always;"></div>
