## Conclusiones

El proyecto logró implementar una arquitectura frontend–backend desacoplada, con un backend RESTful en Java y un frontend en Angular desplegados en entornos separados. Esta decisión facilita la escalabilidad, la integración futura con otros servicios y la adopción de prácticas de despliegue continuo, mientras que la documentación mediante Swagger mejoró la trazabilidad entre endpoints y funcionalidades, asegurando coherencia entre la capa de presentación y la lógica de negocio.

La base de datos se diseñó bajo un enfoque relacional normalizado, lo que permitió mantener la integridad referencial y reducir la redundancia en el manejo de productos, lotes y proveedores. No obstante, se identifican oportunidades de optimización a nivel de índices y consultas, especialmente en operaciones de lectura intensiva asociadas a reportes de inventario e historiales, que serán clave para sostener el rendimiento a medida que crezca el volumen de datos.

De forma complementaria, la incorporación sistemática de las opiniones de los usuarios durante el desarrollo fue determinante para ajustar tanto los requerimientos funcionales como los detalles de interacción de la página. La retroalimentación sobre pantallas confusas, prioridades de información y acciones más frecuentes permitió priorizar funcionalidades, simplificar flujos y corregir problemas de usabilidad que no eran evidentes desde una perspectiva exclusivamente técnica, alineando mejor la solución con las necesidades reales de quienes la utilizarán.

Como resultado de este ciclo iterativo, se logró construir una interfaz funcional que cumple con el objetivo principal del proyecto: permitir a los usuarios gestionar su información y completar sus tareas de manera clara y eficiente. La organización de la navegación, la disposición de los elementos en pantalla y el comportamiento del sistema frente a las acciones del usuario (mensajes, validaciones y estados de carga) hacen posible completar de inicio a fin los flujos críticos definidos, lo que demuestra que el prototipo alcanzó un nivel de usabilidad suficiente para ser utilizado en un contexto real o servir como base sólida para futuras mejoras.

## Recomendaciones

A partir de lo logrado, se recomienda institucionalizar la recolección de feedback de usuarios como parte del ciclo de desarrollo (por ejemplo, pruebas de usabilidad periódicas o encuestas dentro de la propia página). Esto permitiría seguir refinando la experiencia, detectar tempranamente nuevos problemas de uso y orientar las próximas mejoras en función de evidencia y no solo de supuestos del equipo.

También se recomienda evolucionar la interfaz hacia un diseño más consistente y escalable, adoptando un sistema de diseño (design system) o biblioteca de componentes reutilizables. Con ello se facilitaría mantener coherencia visual entre módulos, acelerar el desarrollo de nuevas pantallas y asegurar que, a medida que la página crezca en funcionalidades, se conserve la misma lógica de interacción que los usuarios ya aprendieron durante esta primera versión.

<div style="page-break-after: always;"></div>
