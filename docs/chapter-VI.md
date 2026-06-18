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

Pruebas de Generar reportes de estado de inventario:

![Test Report](../assets/img/chapter-VI/Test1Re.png)

Gestionar catálogo de productos:

![Test Getionar Catalogo](../assets/img/chapter-VI/Test2Gest.png)

Clasificación de productos por categoría:

![Test Clasificar Productos](../assets/img/chapter-VI/Test3Clas.png)

Búsqueda y filtrado de productos:

![Test Búsqueda y filtrado de productos](../assets/img/chapter-VI/Test4Bus.png)

Gestionar ítems del borrador:

![Test Getionar Catalogo](../assets/img/chapter-VI/Test5GestB.png)

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

## 6.2 Static Testing and Verification

### 6.2.1. Static Code Analysis
Esta sección se centra en los métodos de prueba estática y verificación del código aplicados en el proyecto **StockTrack**. El objetivo principal es revisar la calidad interna del software antes de su ejecución, permitiendo identificar problemas de estructura, estilo, mantenibilidad, duplicación de código y posibles riesgos de seguridad en una etapa temprana del desarrollo.

El análisis de código estático permite revisar el código fuente sin necesidad de ejecutar completamente el sistema. En StockTrack, esta revisión se aplica principalmente sobre los dos componentes desarrollados: el **backend** y el **frontend web**. El backend está desarrollado con **Java y Spring Boot**, mientras que el frontend utiliza **Angular y TypeScript**.

Este enfoque ayuda a mantener un proyecto más ordenado, ya que StockTrack contiene distintos módulos relacionados con autenticación, usuarios, permisos, inventario, ventas, reportes, proveedores y administración de personal. Al revisar el código desde etapas tempranas, el equipo puede reducir errores antes de integrar los cambios a las ramas principales del repositorio.


<p align="center">
  <img src="../assets/img/chapter-VI/i1.png" alt="Pruebas Escritorio" width="700">
</p>

#### 6.2.1.1 Coding Standart & Code Conventions

Las normas de codificación y las convenciones de código son lineamientos que permiten mantener un código más claro, coherente y fácil de mantener. En el proyecto StockTrack, estas convenciones se aplican tanto en el backend como en el frontend, con el propósito de facilitar la colaboración entre los integrantes del equipo y reducir errores durante el desarrollo.

En primer lugar, se aplica el principio de **Clean Code**, ya que se busca utilizar nombres descriptivos para clases, métodos, variables, servicios y archivos. Esto permite que el código sea más fácil de leer y comprender. Por ejemplo, en el backend se identifican nombres relacionados con controladores, servicios, repositorios, comandos, consultas y recursos. En el frontend también se utilizan nombres relacionados con cada funcionalidad, como autenticación, dashboard, inventario, ventas, reportes, proveedores y configuración.

En el backend, StockTrack presenta una organización modular. El código se encuentra dividido en módulos como `iam`, `inventory`, `sales`, `reports`, `userpermission` y `shared`. Esta separación permite que cada parte del sistema tenga una responsabilidad más clara. Por ejemplo, el módulo `iam` se relaciona con autenticación y usuarios, mientras que `inventory` contiene la lógica relacionada con productos, categorías, lotes, kits y proveedores.


<p align="center">
  <img src="../assets/img/chapter-VI/i2.png" alt="Pruebas Escritorio" width="700">
</p>

También se observa una estructura cercana a **Domain-Driven Design**, porque los módulos del backend están organizados en capas como `domain`, `application`, `infrastructure` e `interfaces`. Esta separación permite que la lógica de negocio no se mezcle directamente con los controladores o la persistencia de datos. De esta forma, el proyecto mantiene una estructura más ordenada y alineada con los procesos principales del sistema.

Dentro del backend también se identifican algunos patrones importantes. Se utiliza una **arquitectura por capas**, donde la capa de interfaces expone los endpoints REST, la capa de aplicación contiene los servicios, la capa de dominio maneja los modelos y reglas principales, y la capa de infraestructura contiene aspectos técnicos como persistencia y seguridad. Además, se aplica el **Repository Pattern** mediante Spring Data JPA para separar el acceso a datos de la lógica de negocio.

Otro patrón identificado es una separación básica entre comandos y consultas, conocida como **CQRS básico**. Esto se puede observar en carpetas como `commands`, `queries`, `commandservices` y `queryservices`. Los comandos se utilizan para operaciones que modifican información, mientras que las consultas se enfocan en obtener datos. Esta separación ayuda a que el código sea más entendible y mantenible.

En el frontend, el proyecto también se encuentra organizado por módulos funcionales. Se identifican carpetas como `auth`, `dashboard`, `inventory`, `reports`, `sales`, `providers-management`, `personal-administration`, `settings` y `shared`. Esta estructura permite separar las vistas, servicios, modelos y componentes según la funcionalidad a la que pertenecen.


<p align="center">
  <img src="../assets/img/chapter-VI/i3.png" alt="Pruebas Escritorio" width="700">
</p>

En el frontend también se aplican convenciones de formato mediante archivos como `.editorconfig`, `package.json` y `tsconfig.json`. El archivo `.editorconfig` ayuda a mantener reglas de formato como la indentación, codificación UTF-8 y eliminación de espacios innecesarios. Además, el proyecto utiliza Prettier para mantener un estilo uniforme en el código.

También se identifican reglas estrictas de TypeScript, como `strict`, `noImplicitReturns`, `noFallthroughCasesInSwitch` y `strictTemplates`. Estas reglas ayudan a detectar errores durante el desarrollo, principalmente errores de tipado, retornos incompletos o problemas en las plantillas de Angular.

En general, las convenciones utilizadas en StockTrack permiten que el código sea más ordenado y fácil de mantener. Aunque el proyecto todavía podría mejorar con herramientas adicionales de análisis automático, la estructura actual permite trabajar de forma más clara en equipo.


#### 6.2.1.2 Code Quality & Code Security

La calidad del código y la seguridad son aspectos importantes en StockTrack, debido a que el sistema maneja información relacionada con usuarios, inventario, productos, proveedores, ventas y reportes. Por ello, se busca mantener un código entendible, seguro y con una estructura que permita realizar cambios sin afectar todo el sistema.

#### Calidad del Código

La calidad del código en StockTrack se apoya principalmente en la organización modular del backend y frontend, el uso de convenciones de código, las reglas estrictas de TypeScript y la existencia de pruebas automatizadas.

En el backend, se utilizan tecnologías como **Java, Spring Boot, Maven, Spring Web, Spring Data JPA, Spring Validation, Spring Security, MySQL, Lombok, JWT y OpenAPI**. Estas herramientas permiten construir una API REST organizada, con validaciones, persistencia de datos, autenticación y documentación de endpoints.

En el frontend, se utilizan **Angular, TypeScript, Angular Material, Angular Router, RxJS, Angular Signals, Chart.js, ExcelJS y ngx-translate**. Estas tecnologías permiten construir una interfaz web modular, con rutas protegidas, componentes reutilizables, gráficos, exportación de información y soporte para traducciones.

La calidad del código también se refuerza con las pruebas existentes. En el backend se identifican pruebas de servicios y controladores, además de archivos `.feature` que describen escenarios funcionales relacionados con inventario, reportes, catálogo de productos, kits, proveedores, lotes y administración de usuarios. En el frontend se identifican archivos `.spec.ts`, utilizados para pruebas unitarias con Jasmine y Karma.

Entre los criterios de calidad considerados en el proyecto se encuentran:

- Organización modular del código.
- Separación de responsabilidades entre capas.
- Uso de nombres claros y descriptivos.
- Reutilización de componentes y servicios.
- Validaciones en backend.
- Configuración estricta de TypeScript.
- Pruebas unitarias y de integración.
- Documentación de API mediante OpenAPI/Swagger.

#### Seguridad del Código

La seguridad del código es importante porque StockTrack controla usuarios, permisos y datos relacionados con inventario y ventas. En el backend se utiliza **Spring Security** para proteger los endpoints del sistema. La configuración de seguridad permite el acceso público a rutas de autenticación y documentación, pero solicita autenticación para los demás recursos.

Además, el backend utiliza **JWT** para generar y validar tokens de autenticación. Esto permite identificar al usuario que realiza cada solicitud y controlar el acceso a los recursos protegidos. También se utiliza **BCrypt** para codificar contraseñas, evitando almacenarlas directamente en texto plano.

En el frontend, la seguridad se complementa mediante guards e interceptores. El `authGuard` protege rutas que requieren autenticación, mientras que el `permissionGuard` valida si el usuario cuenta con permisos para acceder a ciertos módulos. Además, el `authInterceptor` agrega automáticamente el token JWT en las solicitudes HTTP hacia el backend mediante el encabezado `Authorization: Bearer`.


<p align="center">
  <img src="../assets/img/chapter-VI/i4.png" alt="Pruebas Escritorio" width="700">
</p>

Entre los principales mecanismos de seguridad identificados se encuentran:

- Protección de endpoints mediante Spring Security.
- Autenticación basada en JWT.
- Uso de BCrypt para contraseñas.
- Control de acceso mediante roles y permisos.
- Guards en Angular para proteger rutas.
- Interceptor HTTP para enviar el token al backend.
- Validación de datos recibidos en los controladores.

En comparación con otros ejemplos revisados, en los repositorios de StockTrack no se identificó una configuración directa de SonarQube. Por ello, no se toma como evidencia principal del proyecto. Sin embargo, herramientas como SonarQube o SonarLint podrían incorporarse como mejora futura para detectar duplicación de código, vulnerabilidades, problemas de complejidad y malas prácticas de forma más automática.

### 6.2.2. Reviews

En StockTrack, las revisiones de código son una práctica importante para controlar la calidad del software antes de integrar cambios en las ramas principales. Este proceso permite que los integrantes del equipo revisen el trabajo realizado, detecten errores y verifiquen que las funcionalidades cumplan con lo esperado.

El proyecto utiliza GitHub como plataforma de control de versiones. Cada integrante puede trabajar en una rama específica según la funcionalidad asignada y luego subir sus cambios para revisión. Este proceso permite mantener un mejor control del código y evita que los cambios se integren directamente sin una validación previa.

#### Tipos de Revisiones

**Revisión de código por pares:**  
Consiste en que un integrante del equipo revise el código desarrollado por otro compañero. En esta revisión se comprueba que el código sea entendible, que tenga nombres claros, que respete la estructura del proyecto y que no genere errores en otros módulos.

**Revisión técnica:**  
Al finalizar una actividad o sprint, se revisan las funcionalidades implementadas para confirmar que cumplan con los objetivos definidos. En el caso de StockTrack, se revisan módulos como autenticación, inventario, ventas, reportes, proveedores y administración de usuarios.

**Revisión automática o asistida:**  
El proyecto cuenta con algunas herramientas que ayudan a encontrar errores durante el desarrollo, como TypeScript strict mode, Prettier, EditorConfig, Jasmine, Karma, JUnit, Mockito y archivos feature. Además, SonarLint o SonarQube podrían agregarse más adelante para fortalecer el análisis estático del proyecto.

#### Proceso de Revisión

El proceso inicia cuando un desarrollador trabaja en una rama específica del proyecto. Luego realiza los cambios correspondientes en el backend o frontend y verifica que el proyecto compile correctamente. Después, sube los cambios a GitHub y solicita la revisión antes de integrarlos a la rama principal o de desarrollo.

Durante la revisión se consideran los siguientes aspectos:

- Que el código esté ubicado en el módulo correcto.
- Que los nombres de clases, métodos y archivos sean claros.
- Que se mantenga la separación entre capas y responsabilidades.
- Que no exista duplicación innecesaria.
- Que los endpoints tengan validaciones adecuadas.
- Que las rutas protegidas respeten autenticación y permisos.
- Que el frontend mantenga el uso correcto de componentes, stores, guards e interceptores.
- Que las pruebas existentes no fallen.
- Que los cambios no afecten funcionalidades ya implementadas.

Si se encuentran errores o mejoras, el revisor deja observaciones para que el desarrollador las corrija. Luego de realizar los ajustes, el código se vuelve a revisar. Cuando el cambio cumple con lo solicitado, se aprueba y puede integrarse a la rama correspondiente.


## 6.3 Validation Interviews

### 6.3.1 Diseño de Entrevistas

### 6.3.2 Registro de Entrevistas

### 6.3.3 Evaluaciones Según Heuristicas 

## 6.4. Auditoría de Experiencias de Usuario

### 6.4.1. Auditoría realizada

#### 6.4.1.1. Información del grupo auditado

#### 6.4.1.2. Cronograma de auditoría realizada

#### 6.4.1.3. Contenido de auditoría realizada

### 6.4.2. Auditoría recibida

#### 6.4.2.1. Información del grupo auditor

#### 6.4.2.2. Cronograma de auditoría recibida

#### 6.4.2.3. Contenido de auditoría recibida

#### 6.4.2.4. Resumen de modificaciones para subsanar hallazgos 