## Conclusiones

El proyecto logró implementar una arquitectura frontend–backend desacoplada, con un backend RESTful en Java y un frontend en Angular desplegados en entornos separados. Esta decisión facilita la escalabilidad, la integración futura con otros servicios y la adopción de prácticas de despliegue continuo, mientras que la documentación mediante Swagger mejoró la trazabilidad entre endpoints y funcionalidades, asegurando coherencia entre la capa de presentación y la lógica de negocio.

La base de datos se diseñó bajo un enfoque relacional normalizado, lo que permitió mantener la integridad referencial y reducir la redundancia en el manejo de productos, lotes y proveedores. No obstante, se identifican oportunidades de optimización a nivel de índices y consultas, especialmente en operaciones de lectura intensiva asociadas a reportes de inventario e historiales, que serán clave para sostener el rendimiento a medida que crezca el volumen de datos.

De forma complementaria, la incorporación sistemática de las opiniones de los usuarios durante el desarrollo fue determinante para ajustar tanto los requerimientos funcionales como los detalles de interacción de la página. La retroalimentación sobre pantallas confusas, prioridades de información y acciones más frecuentes permitió priorizar funcionalidades, simplificar flujos y corregir problemas de usabilidad que no eran evidentes desde una perspectiva exclusivamente técnica, alineando mejor la solución con las necesidades reales de quienes la utilizarán.

Como resultado de este ciclo iterativo, se logró construir una interfaz funcional que cumple con el objetivo principal del proyecto: permitir a los usuarios gestionar su información y completar sus tareas de manera clara y eficiente. La organización de la navegación, la disposición de los elementos en pantalla y el comportamiento del sistema frente a las acciones del usuario (mensajes, validaciones y estados de carga) hacen posible completar de inicio a fin los flujos críticos definidos, lo que demuestra que el prototipo alcanzó un nivel de usabilidad suficiente para ser utilizado en un contexto real o servir como base sólida para futuras mejoras.

## Recomendaciones

A partir de lo logrado, se recomienda institucionalizar la recolección de feedback de usuarios como parte del ciclo de desarrollo (por ejemplo, pruebas de usabilidad periódicas o encuestas dentro de la propia página). Esto permitiría seguir refinando la experiencia, detectar tempranamente nuevos problemas de uso y orientar las próximas mejoras en función de evidencia y no solo de supuestos del equipo.

También se recomienda evolucionar la interfaz hacia un diseño más consistente y escalable, adoptando un sistema de diseño (design system) o biblioteca de componentes reutilizables. Con ello se facilitaría mantener coherencia visual entre módulos, acelerar el desarrollo de nuevas pantallas y asegurar que, a medida que la página crezca en funcionalidades, se conserve la misma lógica de interacción que los usuarios ya aprendieron durante esta primera versión.

<div style="page-break-after: always;"></div>

# Bibliografía

GS1 Uruguay. (2024). _Estudio de faltantes de mercadería en góndola – Investigación 2024_. <https://fmguy.org/web-2024/indice-faltantes.html> <br>

Valverde, J. L. C., Herrera, A. A. C., & Castro, K. J. T. (2023). _Estrategias comerciales de las bodegas y su futuro dentro del canal tradicional_ (Master's thesis, Pontificia Universidad Catolica del Peru (Peru)). <https://www.proquest.com/openview/b7f446f130b7c938439b83a671eb0fee/1?pq-origsite=gscholar&cbl=2026366&diss=y>
<br>

Arroyo Holguin, G. M., & Cruz Aquino, N. A. Identificación y diseño de mejoras en la logística de distribución y cadena de suministros de una Bodega de Vinos y Piscos Naturales en el Valle de Pisco-Perú. Caso: Bodega Murga. <https://repositorioacademico.upc.edu.pe/handle/10757/672284>
<br>

Hinojosa Wong, H. S., & Perca Rivera, A. G. Nuevas tecnologías y su relación con la competitividad de bodegas tradicionales en la ciudad de Huancayo, 2021. <https://repositorioacademico.upc.edu.pe/handle/10757/660397>
<br>

Cairo Casas, E. D., Lucio Cruz, J. J., Makiya Francia, R. G., Ramos Murazzo, J. P., & Palomino Padilla, I. H. (2021). Plataforma digital para la gestión del negocio de las bodegas" GOODSTOCK". <https://tesis.pucp.edu.pe/items/9d8d69cb-2688-4976-b004-cf9a630dd05e>
<br>

Angular Material. (s.f.). Angular Material. <https://material.angular.dev>
<br>

GitHub. (s.f.). GitHub. <https://github.com>
<br>

Swagger. (s.f.). Swagger. <https://swagger.io>
<br>

Railway. (s.f.). Railway: Deploy your code, instantly. <https://railway.app>
<br>

Vercel. (s.f.). Vercel: Develop. Preview. Ship. <https://vercel.com>
<br>

<div style="page-break-after: always;"></div>