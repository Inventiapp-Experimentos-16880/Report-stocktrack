# Capítulo VI: Product Verification & Validation
## 6.1. Testing Suites & Validation

Para garantizar la calidad, estabilidad y escalabilidad de la plataforma StockTrack, se ha implementado una estrategia de pruebas multinivel. Todas las pruebas definidas en este capítulo se han derivado directamente de las User Stories (US) establecidas en el Backlog del proyecto. Cada test case ha sido diseñado para validar los Criterios de Aceptación, asegurando que el producto final cumpla con las necesidades funcionales y de negocio.

### 6.1.1. Core Entities Unit Tests.

En esta fase, se realizaron pruebas unitarias sobre la lógica de negocio central en el Backend. Dado que el proyecto utiliza una arquitectura basada en Domain-Driven Design (DDD) implementada con Java y Spring Boot, las pruebas se enfocaron en el aislamiento y validación de las entidades dentro de cada Bounded Context.

### 6.1.2. Core Integration Tests.

Las pruebas de integración validan la interacción entre los módulos de la capa de presentación (Frontend en Angular) y los servicios del API REST. El objetivo es confirmar que la comunicación bidireccional y el procesamiento de respuestas JSON sean consistentes.

### 6.1.3. Core Behavior-Driven Development



### 6.1.4. Core System Tests.

Para la validación final del sistema, se utilizó **Selenium IDE**, enfocándose en el cumplimiento de la **US09 (Diseño Responsive)** de la Landing Page (desarrollada en Astro). Se ejecutó una **Suite de Pruebas de Responsividad** simulando interacciones reales para asegurar que la experiencia de usuario y los flujos de conversión (como el cambio de idioma y el acceso al registro) sean óptimos en cualquier resolución de pantalla.

#### Tabla de Pruebas de Sistema (Landing Page)

| Caso de Prueba | Resolución | Objetivo de la Prueba | Resultado Esperado | Estado |
| :--- | :--- | :--- | :--- | :--- |
| **ST-01: Mobile** | 375 x 667 | Validar interacción del menú hamburguesa y anclaje. | Menú desplegable funcional, secciones apiladas y legibilidad mantenida. | **PASSED** |
| **ST-02: Tablet** | 768 x 1024 | Validar adaptabilidad en resoluciones intermedias. | Elementos redimensionados y grillas ajustadas sin desbordamiento (overflow). | **PASSED** |
| **ST-03: Desktop**| 1920 x 1080 | Validar navegación completa y botones de *Call to Action*. | Barra de navegación superior visible y elementos distribuidos en ancho completo. | **PASSED** |


#### **Pruebas:**


<p align="center">
  <img src="../assets/img/chapter-VI/Pmovil.PNG" alt="Prueba Movil" width="700">
</p>
> Reporte de ejecución exitosa en Selenium IDE validando la responsividad y flujos de navegación en versión Móvil (375x667).
<br>
<br>
<br>

<p align="center">
  <img src="../assets/img/chapter-VI/Ptableta.PNG" alt="Pruebas Tableta" width="700">
</p>
> Reporte de ejecución exitosa en Selenium IDE validando la responsividad y flujos de navegación en versión Tableta (768x1024).
<br>
<br>
<br>

<p align="center">
  <img src="../assets/img/chapter-VI/Pescr.PNG" alt="Pruebas Escritorio" width="700">
</p>
> Reporte de ejecución exitosa en Selenium IDE validando la responsividad y flujos de navegación en versión Escritorio (1920x1080).

