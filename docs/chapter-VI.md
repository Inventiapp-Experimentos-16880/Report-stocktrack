# Capítulo VI: Product Verification & Validation
## 6.1. Testing Suites & Validation

Para garantizar la calidad, estabilidad y escalabilidad de la plataforma StockTrack, se ha implementado una estrategia de pruebas multinivel. Todas las pruebas definidas en este capítulo se han derivado directamente de las User Stories (US) establecidas en el Backlog del proyecto. Cada test case ha sido diseñado para validar los Criterios de Aceptación, asegurando que el producto final cumpla con las necesidades funcionales y de negocio.

### 6.1.1. Core Entities Unit Tests.

En esta fase, se realizaron pruebas unitarias sobre la lógica de negocio central en el Backend. Dado que el proyecto utiliza una arquitectura basada en Domain-Driven Design (DDD) implementada con Java y Spring Boot, las pruebas se enfocaron en el aislamiento y validación de las entidades dentro de cada Bounded Context.

Product service test: 

![Product Service Test](../assets/img/chapter-VI/productService.png)

Provider service test:

![Provider Service Test](../assets/img/chapter-VI/providerService.png)

Sale service test:

![Sale Service Test](../assets/img/chapter-VI/saleService.png)


### 6.1.2. Core Integration Tests.

Las pruebas de integración validan la interacción entre los módulos de la capa de presentación (Frontend en Angular) y los servicios del API REST. El objetivo es confirmar que la comunicación bidireccional y el procesamiento de respuestas JSON sean consistentes.

Pruebas de integración para Batch controller:

![Batch Controller Test](../assets/img/chapter-VI/batchControllerTest.png)

Pruebas de integración para Product controller:

![Product Controller Test](../assets/img/chapter-VI/productControllerTest.png)

Pruebas de integración para Provider controller:

![Provider Controller Test](../assets/img/chapter-VI/providerControllerTest.png)

Pruebas de integración para Sale controller:

![Sale Controller Test](../assets/img/chapter-VI/salesControllerTest.png)

Pruebas de integración para category controller:

![Category Controller Test](../assets/img/chapter-VI/categoryControllerTest.png)

Pruebas de integración para kit controller:

![Kit Controller Test](../assets/img/chapter-VI/kitControllerTest.png)

Pruebas de integración para product batch controller:

![Product Batch Controller Test](../assets/img/chapter-VI/productBatchesControllerTest.png)

#### **Pruebas de Integracion Frontend**
Se validó la integración del Frontend en Angular con la API del Backend utilizando la herramienta nativa Jasmine/Karma y HttpClientTestingModule. Estas pruebas garantizan que el flujo de datos entre la capa de infraestructura y el servidor simulado sea fluido, validando los verbos HTTP y la estructura de las peticiones sin depender del entorno de producción.

A continuación, se detalla la validación de los servicios de integración clave:


  Pruebas de Integración - US10: Persistencia de proveedores

  **Módulo:** ProvidersApi

  **Objetivo:** Verificar la correcta ejecución del método HTTP POST y el envío de datos mediante el Assembler.

  **Validación:** Se interceptó la petición hacia /api/v1/providers, confirmando el verbo POST y que la respuesta simulada se procese correctamente en el frontend.


![Test Persistencia de Proveedores](../assets/img/chapter-VI/Test1Fr.png)

Resultado Karma: <br>

![Confirmacion de Test Persistencia de Proveedores](../assets/img/chapter-VI/Test1Fro.PNG)


  Pruebas de Integración - US03: Actualización de stock en tiempo real

  **Módulo:** ProductsApi

  **Objetivo:** Validar la capacidad de solicitar asíncronamente el stock actualizado de un producto.

  **Validación:** Se interceptó la petición GET hacia /api/v1/products/{id}, simulando la respuesta del servidor y confirmando que el frontend recibe los datos para el Store.


![Test de Actualización de stock en tiempo real](../assets/img/chapter-VI/Test2Fr.PNG)


Resultado Karma: <br>

![Confirmacion de Test de Actualización de stock en tiempo real](../assets/img/chapter-VI/Test2Fro.PNG)


  Pruebas de Integración - US04: Visualización dinámica de reportes

  **Módulo:** ReportsApi

  **Objetivo:** Verificar la disponibilidad de la infraestructura base para la agregación de reportes.

  **Validación:** Debido al diseño DDD (los reportes se combinan en el Store), se validó la correcta instanciación e inyección del servicio API base sin errores.

![Test de Visualización dinámica de reportes](../assets/img/chapter-VI/Test3Fr.PNG)


Resultado Karma: <br>

![Confirmacion de Test de Visualización dinámica de reportes](../assets/img/chapter-VI/Test3Fro.PNG)

### 6.1.3. Core Behavior-Driven Development

Las pruebas de BDD se diseñaron para validar los flujos de usuario y las funcionalidades clave desde la perspectiva del usuario final. Utilizando Cucumber, se definieron escenarios basados en las User Stories, asegurando que cada funcionalidad cumpla con los criterios de aceptación establecidos.

![BDD Test](../assets/img/chapter-VI/testBDD.png)

Inventory Outflow Feature:

![Inventory Outflow Feature](../assets/img/chapter-VI/inventoryOutflowFeature.png)

Inventory Reports Feature:
![Inventory Reports Feature](../assets/img/chapter-VI/inventoryReportsFeature.png)

Product Catalog Feature:

![Product Catalog Feature](../assets/img/chapter-VI/productCatalogFeature.png)

Product Kits Feature:

![Product Kits Feature](../assets/img/chapter-VI/productKitsFeature.png)

Stock Tresholds Feature:

![Stock Tresholds Feature](../assets/img/chapter-VI/stockTresholdsFeature.png)

Supplier and Batches Feature:

![Supplier and Batches Feature](../assets/img/chapter-VI/supplierAndBatchesFeature.png)

User Management Feature:

![User Management Feature](../assets/img/chapter-VI/userManagementFeature.png)

### 6.1.4. Core System Tests.

Para la validación final del sistema, se utilizó **Selenium IDE**, enfocándose en el cumplimiento de la **US09 (Diseño Responsive)** de la Landing Page (desarrollada en Astro). Se ejecutó una **Suite de Pruebas de Responsividad** simulando interacciones reales para asegurar que la experiencia de usuario y los flujos de conversión (como el cambio de idioma) sean óptimos en cualquier resolución de pantalla.



<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
    <tr>
        <th>US 09</th>
        <th>Diseño responsive</td></th>
        <th>
        <strong> Como </strong> visitante <br>
        <strong> Quiero </strong> que la landing sea responsive <br>
        <strong> Para </strong> navegar cómodamente desde cualquier dispositivo móvil, tablet o escritorio.
        </td>
        </th> 
    
</table>

<br>


#### **Test 1: Prueba en Dispositivo Movil**

<p align="center">
  <img src="../assets/img/chapter-VI/Pmovil.PNG" alt="Prueba Movil" width="700">
</p>


#### **Test 2: Prueba en Dispositivo Tableta**

<p align="center">
  <img src="../assets/img/chapter-VI/Ptableta.PNG" alt="Pruebas Tableta" width="700">
</p>


#### **Test 3: Prueba en Dispositivo Escritorio**

<p align="center">
  <img src="../assets/img/chapter-VI/Pescr.PNG" alt="Pruebas Escritorio" width="700">
</p>

