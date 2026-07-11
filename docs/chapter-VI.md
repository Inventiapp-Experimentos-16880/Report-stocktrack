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

Las siguientes preguntas están diseñadas para aplicarse a ambos segmentos, ya que buscan validar si la propuesta de StockTrack responde a sus necesidades reales de gestión de inventario, control de stock, alertas, reportes y organización logística.

1. Después de conocer la propuesta de **StockTrack**, ¿consideras que esta solución podría ayudarte a mejorar la gestión de tu inventario? ¿Por qué?

2. ¿Qué tan útil te parece contar con una plataforma que registre las entradas y salidas de productos de forma ordenada?

3. ¿La función de alertas por bajo stock o productos próximos a vencer resolvería algún problema actual en tu negocio?

4. ¿Qué tan importante sería para ti visualizar el stock disponible en tiempo real?

5. ¿Consideras que los reportes de inventario, ventas o movimientos de productos te ayudarían a tomar mejores decisiones?

6. ¿Qué funcionalidad te parece más importante dentro de **StockTrack**: control de stock, alertas, reportes, gestión de proveedores o historial de movimientos? ¿Por qué?

7. ¿Qué dificultad crees que podrías tener al empezar a usar una herramienta digital para gestionar tu inventario?

8. ¿Preferirías utilizar esta solución desde una computadora, celular o ambos? ¿Por qué?

9. ¿Estarías dispuesto a probar una versión inicial de **StockTrack** en tu negocio? ¿Qué tendría que cumplir para que sigas usándola?

10. En una escala del 1 al 5, donde 1 es “nada útil” y 5 es “muy útil”, ¿qué tan útil consideras **StockTrack** para tu negocio? ¿Por qué?



### 6.3.2 Registro de Entrevistas

Link de entrevistas:<a href="https://tinyurl.com/66etkfv8">https://tinyurl.com/66etkfv8</a> <br>

**Segmento #1: Bodegas especializadas por rubro**

#### Datos del entrevistado:
 **Nombre:** Lucarelly Sanchez Heredia <br> 
  **Edad:** 21 años 
  ![Entrevista 1 - Segmento Dueños de Bodegas](../assets/img/chapter-II/lucas-interview.png) <br> 
**Duración:** 2:53 min 

#### Resumen de entrevista:

Lucarelly administra una bodega junto a su abuelo. Actualmente registra parte de su inventario en Excel, aunque menciona que no siempre se encuentra actualizado. También utiliza una libreta para anotar algunos productos que ingresan o salen durante el día. Uno de sus principales problemas es la falta de control sobre los lotes y fechas de vencimiento, ya que en algunas ocasiones se mezclan productos antiguos con productos nuevos. Esto le ha generado pérdidas por productos vencidos o por no saber exactamente qué productos están por agotarse.

Luego de explicarle la propuesta de StockTrack, consideró que la plataforma podría ayudarle a ordenar mejor su inventario, principalmente si cuenta con alertas de bajo stock y productos próximos a vencer. También indicó que le sería útil poder revisar el stock desde su celular, porque no siempre está usando la laptop. Aunque no ha usado antes una plataforma especializada de inventario, señaló que estaría dispuesto a probar una versión sencilla si no es complicada de usar.

#### Principales hallazgos del segmento:

- El entrevistado sí presenta problemas reales relacionados con control de inventario.
- Existe una necesidad clara de alertas por vencimiento y bajo stock.
- El usuario valora que la plataforma sea simple y fácil de usar.
- El uso desde celular es importante para negocios pequeños como bodegas.
- La propuesta de StockTrack resulta útil, pero debe evitar ser complicada.


**Segmento #2: Startups y emprendedores en expansión con necesidades logísticas**

#### Datos del entrevistado:
**Nombre:** Alexander Miranda Vivanco <br>
**Edad:** 27 años 

 ![Entrevista 1 - Startups y emprendedores en expansión con necesidades logísticas](../assets/img/chapter-II/Entrevista-Alexander-Miranda.png) <br> **Duración:** 3:30 min 

#### Resumen de entrevista:

Alexander tiene un emprendimiento dedicado a la venta de productos para mascotas. Actualmente revisa su inventario de manera presencial en su almacén y lo registra en Excel, apoyándose también en boletas y comprobantes de venta. Indicó que esta forma de trabajo le toma tiempo, especialmente cuando necesita saber qué productos se están vendiendo más o qué productos debe reponer.

Después de presentarle StockTrack, consideró que la plataforma podría ayudarle a mejorar la organización del inventario y reducir el tiempo que dedica a revisar productos manualmente. Le llamó la atención la posibilidad de registrar entradas y salidas, generar reportes y consultar el stock actualizado. También mencionó que una herramienta digital podría ser útil si su negocio sigue creciendo, ya que actualmente el control manual todavía funciona, pero empieza a volverse limitado.

#### Principales hallazgos del segmento:

- El entrevistado tiene una necesidad clara de reducir el tiempo de revisión manual del inventario.
- Los reportes son una funcionalidad importante para negocios en crecimiento.
- El historial de movimientos ayuda a controlar mejor las entradas y salidas.
- El usuario considera útil una plataforma digital si es rápida y fácil de implementar.
- Existe disposición para probar una versión inicial de StockTrack. 


### 6.3.3 Evaluaciones Según Heuristicas 

**Aplicación para evaluar:** StockTrack

### Tareas que evaluar:

- Registrar un nuevo producto en el inventario.
- Visualizar el stock disponible de los productos.
- Registrar entradas y salidas de productos.
- Revisar alertas por bajo stock o productos próximos a vencer.
- Consultar reportes de inventario y ventas.

### Tabla de resumen:

| Escala de Severidad | Descripción |
|---|---|
| 1 | No tan grave |
| 2 | Leve |
| 3 | Moderado |
| 4 | Grave |
| 5 | Muy grave |

| #Orden | Problema | Escala de Severidad | Heurística / Principio violado |
|---|---|---:|---|
| #1 | El usuario puede confundirse al registrar un nuevo producto si el formulario solicita muchos datos al mismo tiempo. | 3 | Eficiencia de uso |
| #2 | No se muestra un mensaje suficientemente visible cuando un producto se registra correctamente. | 4 | Visibilidad del estado del sistema |
| #3 | La sección de alertas de bajo stock no se identifica rápidamente desde el panel principal. | 4 | Reconocimiento antes que recuerdo |
| #4 | El usuario no cuenta con una opción rápida para filtrar productos por categoría, proveedor o estado de stock. | 3 | Flexibilidad y eficiencia de uso |
| #5 | Los reportes pueden ser difíciles de interpretar si no se muestran gráficos o indicadores claros. | 3 | Estética y diseño minimalista |

---

## Heurísticas y Recomendaciones

### Problema #1: Formulario de registro de producto con demasiados campos visibles

**Heurística violada:** Eficiencia de uso

**Descripción del problema:**  
Al registrar un nuevo producto, el usuario puede sentirse confundido si el formulario presenta muchos campos al mismo tiempo, como nombre, categoría, proveedor, precio, lote, fecha de vencimiento, stock mínimo y stock inicial. Esto puede ser más complicado para usuarios que vienen de usar Excel o una libreta.

**Recomendación:**  
Organizar el formulario por secciones, separando información básica, datos de inventario y datos adicionales. También se recomienda marcar claramente los campos obligatorios y mostrar textos de ayuda cortos para orientar al usuario.

---

### Problema #2: Falta de confirmación visible al registrar un producto

**Heurística violada:** Visibilidad del estado del sistema

**Descripción del problema:**  
Cuando el usuario registra un producto, si el sistema no muestra una confirmación clara, puede generar dudas sobre si el producto fue guardado correctamente. Esto podría causar que el usuario repita el registro o revise manualmente la lista para confirmar.

**Recomendación:**  
Agregar un mensaje visible de confirmación, como “Producto registrado correctamente”. También se puede usar una notificación tipo alerta o toast en la parte superior o inferior de la pantalla.

---

### Problema #3: Alertas de bajo stock poco visibles

**Heurística violada:** Reconocimiento antes que recuerdo

**Descripción del problema:**  
Las alertas por bajo stock o productos próximos a vencer son una funcionalidad importante para ambos segmentos. Si estas alertas no se muestran claramente desde el dashboard, el usuario podría olvidarse de revisarlas y seguir teniendo problemas de reposición o vencimiento.

**Recomendación:**  
Incluir una sección visible en el dashboard con alertas principales, usando colores o íconos para diferenciar bajo stock, productos por vencer y productos agotados. Esto facilitaría que el usuario detecte problemas apenas ingrese al sistema.

---

### Problema #4: Falta de filtros rápidos en la lista de productos

**Heurística violada:** Flexibilidad y eficiencia de uso

**Descripción del problema:**  
Cuando el inventario crece, buscar productos manualmente puede volverse lento. Esto afecta especialmente a emprendedores en expansión, ya que manejan más productos, proveedores y movimientos de stock.

**Recomendación:**  
Agregar filtros rápidos por categoría, proveedor, estado de stock y fecha de vencimiento. También se recomienda incluir una barra de búsqueda visible para encontrar productos por nombre o código.

---

### Problema #5: Reportes poco claros para la toma de decisiones

**Heurística violada:** Estética y diseño minimalista

**Descripción del problema:**  
Los reportes de inventario y ventas pueden no ser tan útiles si se muestran solo como tablas extensas. Los usuarios necesitan identificar rápidamente qué productos se venden más, cuáles tienen baja rotación y qué productos deben reponerse.

**Recomendación:**  
Incluir gráficos simples, indicadores clave y resúmenes visuales. Por ejemplo, productos más vendidos, productos con bajo stock, productos próximos a vencer y movimientos recientes. Esto ayudaría a que los usuarios tomen decisiones más rápidas.

## 6.4. Auditoría de Experiencias de Usuario

## 6.4.1. Auditoría realizada

### 6.4.1.1. Información del grupo auditado

| Elemento | Información identificada |
|---|---|
| Startup / proyecto auditado | LiquoTrack |
| Equipo auditado | Equipo de Desarrollo LiquoTrack |
| Integrantes del equipo auditado | - Coronel Espinoza, Farid Sebastian<br>- Diaz Quispe, Matias Sebastian<br>- Juarez Leon, Nicolas Emilio Walter<br>- Julca Minaya, Sergio Gino |
| Artefactos revisados | - Plan de Auditoría LiquoTrack<br>- Informe del Equipo LiquoTrack |
| Contenido funcional observado | Flujos To-Be relacionados con catálogos de productos, exploración de catálogos, carrito de compras y compras. |
| Criterio de referencia | Final Project Statement, metodología Experiment-Driven Development, plan de auditoría y evidencia documental presentada. |
| Tipo de auditoría | Académica interna |

### 6.4.1.2. Cronograma de auditoría realizada


| Horario / Fecha | Área / Proceso | Equipo auditor | Responsable | Requisito |
|---|---|---|---|---|
| 10:00-10:10 | Reunión de apertura | Auditor líder / Equipo auditado | Auditor líder / Equipo auditado | Explicar objetivo, alcance y criterios de la auditoría. |
| 10:10-10:25 | As-Is Summary | Giovany Smith Torres Apolinario | Equipo de Desarrollo LiquoTrack | Problemas actuales claramente definidos: rendimiento, UX, funcionalidad y usabilidad. |
| 10:25-10:40 | Raw Material | Yaku Mateo Guzmán Cabrejos | Equipo de Desarrollo LiquoTrack | Assumptions, knowledge gaps, ideas y claims deben sustentar las preguntas experimentales. |
| 10:40-10:55 | Experiment-Ready Questions | Antonio Jhair Navarro Chinga | Equipo de Desarrollo LiquoTrack | Preguntas belief-led y exploratorias deben ser medibles y conectadas a problemas reales. |
| 10:55-11:10 | Question Backlog | Dayro Richard Rios Piñan | Equipo de Desarrollo LiquoTrack | Verificar scoring C/R/I/In, prioridad, justificación de puntajes y orden de preguntas por riesgo e impacto. |
| 11:10-11:30 | Experiment Cards | Dayro Richard Rios Piñan | Equipo de Desarrollo LiquoTrack | Cada tarjeta debe incluir pregunta, why, hypothesis, what, medidas, condiciones y escala. |
| 11:30-11:45 | Hypotheses | Antonio Jhair Navarro Chinga | Equipo de Desarrollo LiquoTrack | Cada hipótesis debe tener creencia, hipótesis principal y nula, cuantificable y trazable a una tarjeta. |
| 11:45-12:00 | Methods Selection | Antonio Jhair Navarro Chinga | Equipo de Desarrollo LiquoTrack | Verificar que el método elegido sea adecuado para cada hipótesis y que las herramientas permitan recolectar datos válidos. |
| 12:00-12:15 | To-Be User Stories | Giovany Smith Torres Apolinario | Equipo de Desarrollo LiquoTrack | US15-US23 deben tener usuario, prioridad, épica, descripción, criterios de aceptación y trazabilidad. |
| 12:15-12:30 | To-Be Technical Stories | Giovany Smith Torres Apolinario | Equipo de Desarrollo LiquoTrack | Verificar que TS15-TS19 tengan usuario, prioridad, épica, descripción, criterios de aceptación y trazabilidad. |
| 12:30-12:45 | To-Be Product Backlog | Yaku Mateo Guzmán Cabrejos | Equipo de Desarrollo LiquoTrack | Verificar que el backlog esté priorizado según Question Backlog, riesgo, impacto, story points y dependencias del producto. |
| 12:45-13:00 | Reunión de cierre | Auditor líder | Equipo de Desarrollo LiquoTrack | Registrar cumplimiento, incumplimientos y acciones correctivas. |

---

### 6.4.1.3. Contenido de auditoría realizada

### 6.1. Lista de Verificación

| Resultado | Cantidad |
|---|---:|
| Cumple | 7 |
| Cumple parcialmente | 3 |
| No cumple | 0 |
| Total de ítems auditados | 10 |

| ID | Sección auditada | Resultado de revisión | Evidencia / comentario de auditoría | Clasificación |
|---|---|---|---|---|
| LV01 | As-Is Summary | Cumple | Se identifican problemas actuales relacionados con rendimiento, experiencia de usuario, funcionalidad y usabilidad. También se declaran objetivos de mejora para orientar el estado To-Be. | Fortaleza |
| LV02 | Raw Material | Cumple | Se presentan assumptions, knowledge gaps, ideas y claims que sirven como insumo para formular preguntas experimentales. | Fortaleza |
| LV03 | Experiment-Ready Questions | Cumple | Las preguntas belief-led y exploratorias están conectadas con problemas reales del producto y permiten orientar experimentos medibles. | Fortaleza |
| LV04 | Question Backlog | Cumple | Se observa un backlog de preguntas priorizado mediante criterios C/R/I/In, lo que permite ordenar el riesgo y el impacto de los experimentos. | Fortaleza |
| LV05 | Experiment Cards | Cumple | Las tarjetas contienen pregunta, motivación, hipótesis, experimento, medidas, condiciones y escala de éxito, por lo que funcionan como contrato experimental. | Fortaleza |
| LV06 | Hypotheses | Cumple | Las hipótesis principales y nulas están formuladas de manera cuantificable y se relacionan con las preguntas y experiment cards. | Fortaleza |
| LV07 | Methods Selection | Cumple parcialmente | Se seleccionan métodos adecuados como entrevistas, pruebas de campo, fake door, DevTools y test A/B. Sin embargo, se requiere evidenciar la ejecución real de cada método. | Observación |
| LV08 | To-Be User Stories | Cumple parcialmente | Se identifican User Stories To-Be asociadas a las funcionalidades nuevas del producto. Para fortalecerlas, deben incluir criterios de aceptación completos y trazabilidad explícita con hipótesis y experimentos. | Observación |
| LV09 | To-Be Technical Stories | Cumple parcialmente | Se identifican historias técnicas orientadas a soportar las funcionalidades To-Be. Se recomienda precisar endpoints, servicios, base de datos, responsables y evidencias técnicas. | Observación |
| LV10 | To-Be Product Backlog | Cumple | El backlog To-Be ordena los incrementos derivados de los experimentos y permite visualizar prioridad, alcance y esfuerzo estimado. | Fortaleza |

---

### 6.4.2. Auditoría recibida

La auditoría recibida corresponde a la revisión interna realizada al Capítulo VIII: **Experiment-Driven Development** del proyecto **StockTrack**. Esta auditoría tuvo como finalidad verificar el cumplimiento de las secciones solicitadas en el enunciado del Trabajo Final, así como identificar observaciones, no conformidades y oportunidades de mejora en el informe del proyecto.

#### 6.4.2.1. Información del grupo auditor

| Elemento | Información |
|---|---|
| Proyecto auditado | StockTrack |
| Equipo auditado | Equipo Inventiapp |
| Tipo de auditoría | Interna |
| Modalidad | Remota |
| Fecha de auditoría | 05/07/2026 |
| Objetivo | Verificar los contenidos del informe de reporte del proyecto y el cumplimiento de las secciones y descripciones del enunciado del Trabajo Final. |
| Alcance | Informe del Proyecto StockTrack del Capítulo VIII. |
| Criterios de auditoría | Enunciado proporcionado por la administración del curso sobre los contenidos del Trabajo Final. |

**Equipo auditor**

| Rol | Integrante |
|---|---|
| Auditor líder | Coronel Espinoza, Farid Sebastian |
| Auditor interno 2 | Diaz Quispe, Matias Sebastian |
| Auditor interno 3 | Juarez Leon, Nicolas Emilio Walter |
| Auditor interno 4 | Julca Minaya, Sergio Gino |

---

#### 6.4.2.2. Cronograma de auditoría recibida

| Horario / Fecha | Área / Proceso | Equipo auditor | Responsable | Requisito |
|---|---|---|---|---|
| 11:00 - 11:30<br>05/07/2026 | Reunión de Apertura y Presentación del Plan de Auditoría | Equipo Auditor: Coronel, Diaz, Juarez y Julca | Equipo Inventiapp: Torres, Guzmán, Navarro y Rios | Presentación del alcance, criterios y agenda de la auditoría al Capítulo VIII. |
| 11:30 - 12:00<br>05/07/2026 | 8.1 Experiment Planning<br>As-Is Summary, Raw Material, Questions, Backlog, Experiment Cards | Diaz Quispe, Matias Sebastian | Navarro Chinga, Antonio Jhair | Enunciado TF - Capítulo VIII, secciones 8.1.1 a 8.1.5. |
| 12:00 - 12:30<br>05/07/2026 | 8.2 Experiment Design<br>Hypotheses, Metrics, Measures, Conditions | Juarez Leon, Nicolas Emilio Walter | Navarro Chinga, Antonio Jhair | Enunciado TF - Capítulo VIII, secciones 8.2.1 a 8.2.4. |
| 12:30 - 13:00<br>05/07/2026 | 8.2 Experiment Design<br>Scale, Methods, Tracking Plan | Julca Minaya, Sergio Gino | Navarro Chinga, Antonio Jhair | Enunciado TF - Capítulo VIII, secciones 8.2.5 a 8.2.8. |
| 13:00 - 13:30<br>05/07/2026 | 8.3 Experimentation<br>To-Be User Stories y To-Be Product Backlog | Coronel Espinoza, Farid Sebastian | Guzmán Cabrejos, Yaku Mateo | Enunciado TF - Capítulo VIII, secciones 8.3.1 y 8.3.2. |
| 15:00 - 16:00<br>05/07/2026 | Reunión de Cierre y Consolidación de Hallazgos | Equipo Auditor: Coronel, Diaz, Juarez y Julca | Equipo Inventiapp | Consolidación de hallazgos y próximos pasos. |

---

#### 6.4.2.3. Contenido de auditoría recibida

La auditoría recibida evaluó el cumplimiento de las secciones del Capítulo VIII relacionadas con la planificación, diseño y experimentación basada en hipótesis. La revisión se enfocó en comprobar si el documento presentaba trazabilidad entre problemas, preguntas experimentales, hipótesis, métricas, métodos de validación, historias de usuario To-Be y backlog del producto.

##### Lista de verificación recibida

| N° | Sección / Requisito evaluado | Ítem de verificación | Cumple | Evidencia observada | Observación |
|---|---|---|---|---|---|
| 8.1.1 | As-Is Summary | ¿Describe el estado actual del negocio, problemas y objetivos de mejora? | Sí | Se describen procesos manuales, cuatro problemas y cuatro objetivos de mejora. | Cumple con lo solicitado. |
| 8.1.2 | Raw Material | ¿Incluye las cuatro categorías de materia prima claramente diferenciadas? | Sí | Se presentan Assumptions, Knowledge Gaps, Ideas y Claims. | Sin observación crítica. |
| 8.1.3 | Experiment-Ready Questions | ¿Distingue preguntas Belief-led de Exploratorias y aplica 5W+1H? | Sí | Se presentan preguntas BC1-BC3, EX1-EX3 y tabla 5W1H. | Sin observación crítica. |
| 8.1.4 | Question Backlog | ¿Presenta Broad/Deep Backlog con “Por qué” y scoring? | Sí | Se presenta backlog con criterios de Confianza, Riesgo, Impacto e Interés. | Se recomienda mejorar el criterio de desempate. |
| 8.1.5 | Experiment Cards | ¿Cada tarjeta incluye lado frontal y posterior? | Sí | Se presentan cinco tarjetas con pregunta, motivación, hipótesis, experimento, medidas, condiciones y escala. | Se recomienda uniformizar la plantilla. |
| 8.2.1 | Hypotheses | ¿Cada hipótesis es falsable, medible y tiene hipótesis nula emparejada? | Sí | Se presentan cinco hipótesis con belief, hypothesis y null hypothesis. | Se recomienda explicar antes el concepto de hipótesis alternativa y nula. |
| 8.2.2 | Domain Business Metrics | ¿Define métricas de dominio con fórmula, técnica de recolección y meta? | Sí | Se presentan métricas de negocio. | Se requiere detallar fórmulas de cálculo. |
| 8.2.3 | Measures | ¿Selecciona medidas representativas para cada hipótesis? | Sí | Se presentan medidas asociadas a las hipótesis. | Se requiere mejorar consistencia de umbrales. |
| 8.2.4 | Conditions | ¿Define condición experimental y de control? | Sí | Se presentan condiciones experimentales y de control. | Se requiere precisar mecanismos de asignación de grupos. |
| 8.2.5 | Scale Calculations and Decisions | ¿Sustenta certeza, precisión y reglas de decisión? | Sí | Se presentan escalas de decisión. | Se requiere aclarar límites inclusivos y ponderación de hipótesis. |
| 8.2.6 | Methods Selection | ¿Aplica el principio “Simplest Useful Thing”? | Sí | Se presentan métodos como pruebas, fake door y análisis técnico. | Se requiere ajustar métodos según línea base real. |
| 8.2.7 | Data Analytics: Goals, KPIs and Metrics Selection | ¿Vincula metas, KPIs y métricas de analítica? | Sí | Se presentan objetivos, KPIs y métricas. | Se requiere ampliar evidencia técnica a la pantalla de reportes. |
| 8.2.8 | Web and Mobile Tracking Plan | ¿Define eventos a rastrear y estructura de captura? | Sí | Se presenta tabla de eventos y herramientas de análisis. | Se recomienda mejorar campos técnicos e índices. |
| 8.3.1 | To-Be User Stories | ¿Incluye historias en formato Como/Quiero/Para, Gherkin y trazabilidad? | Sí | Se presentan User Stories, Technical Stories y trazabilidad. | Se identificaron inconsistencias en algunas historias. |
| 8.3.2 | To-Be Product Backlog | ¿Prioriza según scoring e incluye Story Points? | Sí | Se presenta backlog con historias y estimaciones. | Se recomienda ajustar priorización y dependencias técnicas. |

##### Resumen de resultados de la auditoría recibida

| Resultado | Cantidad |
|---|---:|
| Sí | 15 |
| Parcial | 3 |
| No | 7 |
| N/A | 0 |

##### Resumen de hallazgos recibidos

| Clasificación | Cantidad |
|---|---:|
| Observación | 21 |
| No conformidad | 15 |
| No conformidad crítica | 2 |
| Total de hallazgos | 38 |

##### Principales hallazgos identificados

| N° | Hallazgo | Severidad | Criterio evaluado | Clasificación |
|---|---|---:|---|---|
| 1 | La definición de hipótesis alternativa y nula debía presentarse antes de la tabla y explicar para qué sirve cada tipo de hipótesis. | 1 | 8.2.1 Hypotheses | Observación |
| 2 | Para cada métrica de dominio era necesario detallar la fórmula de cálculo. | 3 | 8.2.2 Domain Business Metrics | No conformidad |
| 3 | El umbral de búsqueda cambiaba entre “menos de 2 segundos” y “menos de 1.5 segundos” sin explicación. | 3 | 8.1.1 As-Is Summary | No conformidad |
| 4 | La lista de problemas identificados no incluía evidencia o datos de respaldo. | 2 | 8.1.1 As-Is Summary | Observación |
| 5 | Las assumptions incluían porcentajes específicos como si fueran hechos conocidos, mientras que los knowledge gaps indicaban que esos aspectos aún eran desconocidos. | 3 | 8.1.2 Raw Material | No conformidad |
| 6 | Las claims no indicaban fuente ni fecha, lo que impedía verificar su origen. | 2 | 8.1.2 Raw Material | Observación |
| 7 | La pregunta relacionada con alertas automáticas por WhatsApp no fue incorporada al Question Backlog ni recibió Experiment Card. | 3 | 8.1.3 Experiment-Ready Questions | No conformidad |
| 8 | La regla de desempate del Question Backlog no resolvía correctamente el empate entre QB1 y QD1. | 3 | 8.1.4 Question Backlog | No conformidad |
| 9 | Las Experiment Cards no seguían una plantilla completamente consistente. | 1 | 8.1.5 Experiment Cards | Observación |
| 10 | En H2 no existía una condición de control comparable en el tiempo. | 3 | 8.2.4 Conditions | Observación |
| 11 | Los tamaños de muestra eran pequeños para sustentar umbrales de éxito precisos. | 3 | 8.1.5 Experiment Cards | No conformidad |
| 12 | La métrica “Nivel de Frustración” no definía claramente cómo interpretar todos los escenarios de latencia. | 2 | 8.2.3 Measures | Observación |
| 13 | Las métricas de H2 dependían de registros manuales poco confiables. | 3 | 8.2.3 Measures | No conformidad |
| 14 | No se detalló el mecanismo de asignación de usuarios a grupo experimental y grupo control. | 2 | 8.2.4 Conditions | Observación |
| 15 | La regla global de decisión ponderaba todas las hipótesis por igual, aunque H1 y H2 eran de mayor riesgo estratégico. | 3 | 8.2.5 Scale Calculations and Decisions | No conformidad |
| 16 | Los rangos de las escalas de decisión no indicaban si los límites eran inclusivos o exclusivos. | 2 | 8.2.5 Scale Calculations and Decisions | Observación |
| 17 | El método de H4 no fue ajustado con base en la línea base real obtenida con Lighthouse. | 3 | 8.2.6 Methods Selection | No conformidad |
| 18 | El método Fake Door de H3 no aclaraba cómo se controlarían variables externas ni tamaño mínimo de muestra. | 2 | 8.2.6 Methods Selection | Observación |
| 19 | La auditoría Lighthouse no cubría la pantalla de Reportes, pese a estar relacionada con la Hipótesis 5. | 3 | 8.2.7 Data Analytics | No conformidad |
| 20 | No se definió un mecanismo de re-auditoría después de implementar mejoras de rendimiento o contraste. | 2 | 8.2.7 Data Analytics | Observación |
| 21 | El evento `product_search_performed` no diferenciaba búsqueda normal de búsqueda bajo throttling simulado. | 3 | 8.2.8 Tracking Plan | No conformidad |
| 22 | La query de Alert Action Rate podía generar problemas de rendimiento al consultar un campo JSON sin índice específico. | 2 | 8.2.8 Tracking Plan | Observación |
| 23 | US19 fue construida sin pasar por Question Backlog ni Experiment Card propia. | 4 | 8.3.1 To-Be User Stories | No conformidad crítica |
| 24 | US16 estaba redactada como si el resultado del experimento ya hubiera sido validado antes de ejecutarse. | 4 | 8.3.1 To-Be User Stories | No conformidad crítica |
| 25 | US23 recibió story points pese a ser considerada de baja prioridad. | 2 | 8.3.2 To-Be Product Backlog | Observación |
| 26 | Las historias técnicas TS16, TS17, TS18 y TS19 no aparecían en la tabla de priorización. | 3 | 8.3.2 To-Be Product Backlog | No conformidad |
| 27 | La épica EP-11 tenía un alcance demasiado específico y se asemejaba más a una historia de usuario. | 2 | 8.3 Experimentation | Observación |
| 28 | La épica EP-12 mezclaba necesidad de usuario con referencia técnica de i18n. | 2 | 8.3 Experimentation | Observación |
| 29 | US15 mezclaba optimización de búsqueda con coincidencias aproximadas, ampliando demasiado el alcance. | 2 | 8.3 To-Be User Stories | Observación |
| 30 | US16 incorporaba elementos de diseño UI/UX dentro de criterios de aceptación funcionales. | 3 | 8.3 To-Be User Stories | No conformidad |
| 31 | US17 mezclaba alertas anticipadas con registro de acciones de mitigación. | 2 | 8.3 To-Be User Stories | Observación |
| 32 | US18 no aclaraba correctamente el manejo de entradas y salidas en el historial de lote. | 2 | 8.3 To-Be User Stories | Observación |
| 33 | US20 comparaba directamente pérdidas por mermas con el costo del plan, generando posible interpretación incorrecta. | 3 | 8.3 To-Be User Stories | No conformidad |
| 34 | TS15 presentaba inconsistencia entre rol, título y alcance técnico. | 2 | 8.3 To-Be User Stories | Observación |
| 35 | TS16 debía especificar rol backend y contemplar errores, reintentos y registro de estado de notificación. | 3 | 8.3 To-Be User Stories | No conformidad |
| 36 | TS18 debía especificar rol frontend y aclarar que la internacionalización se aplicaría en la interfaz. | 2 | 8.3 To-Be User Stories | Observación |
| 37 | Algunas historias de 5 y 8 story points resultaban demasiado amplias para un ciclo menor a una semana. | 2 | 8.3 To-Be Product Backlog | Observación |
| 38 | La priorización colocaba monetización y suscripción antes de funcionalidades que demuestran valor principal del producto. | 2 | 8.3 To-Be Product Backlog | Observación |

---

#### 6.4.2.4. Resumen de modificaciones para subsanar hallazgos 

Luego de recibir los hallazgos de auditoría, el equipo realizó ajustes documentales y de trazabilidad en el Capítulo VIII con la finalidad de corregir inconsistencias, fortalecer la evidencia presentada y mejorar la relación entre problemas, preguntas, hipótesis, experimentos, métricas, historias y backlog.

| Hallazgo relacionado | Modificación realizada |
|---|---|
| H1 | Se reorganizó la sección de hipótesis, colocando antes de la tabla una explicación breve sobre la hipótesis alternativa y la hipótesis nula, indicando su propósito dentro del proceso experimental. |
| H2 | Se añadieron fórmulas de cálculo para las métricas de dominio, indicando cómo se obtiene cada valor, qué datos se requieren y cómo serán interpretados. |
| H3 | Se homologó el umbral de búsqueda en el documento para evitar contradicciones. Se definió un único criterio de éxito para el tiempo de búsqueda y se explicó su relación con el objetivo de mejora. |
| H4 | Se agregaron evidencias de respaldo para los problemas identificados, considerando mediciones de rendimiento, observaciones del flujo actual y retroalimentación de usuarios. |
| H5 | Se corrigieron las assumptions para que no presenten porcentajes como hechos confirmados. Los porcentajes fueron tratados como supuestos a validar mediante experimentos. |
| H6 | Se incorporó fuente y fecha a los claims, diferenciando si provienen de usuarios, stakeholders, entrevistas, observaciones internas o supuestos del equipo. |
| H7 y H23 | Se incorporó la pregunta de alertas automáticas por WhatsApp al Question Backlog y se creó su respectiva Experiment Card antes de mantenerla como historia de usuario. |
| H8 | Se mejoró la regla de desempate del Question Backlog, agregando criterios secundarios como impacto, interés y dependencia estratégica. |
| H9 | Se uniformizó la plantilla de las Experiment Cards para que todas incluyan los mismos campos: tipo, pregunta, motivación, hipótesis, experimento, medidas, condiciones y escala de éxito. |
| H10, H13 y H14 | Se fortaleció la definición de condiciones experimentales y de control, evitando comparaciones con registros manuales poco confiables y precisando el mecanismo de asignación de usuarios. |
| H11 y H18 | Se revisaron los tamaños de muestra y se aclaró el alcance exploratorio de los experimentos, evitando presentar resultados pequeños como estadísticamente concluyentes. |
| H12 | Se precisó cómo interpretar la métrica de Nivel de Frustración en cada escenario de latencia probado. |
| H15 y H16 | Se ajustaron las reglas de decisión, aclarando límites inclusivos y exclusivos, además de considerar mayor peso para hipótesis de mayor riesgo estratégico. |
| H17 | Se actualizó el diseño experimental de H4 tomando en cuenta la línea base real de rendimiento obtenida mediante Lighthouse. |
| H19 y H20 | Se amplió la auditoría técnica para incluir la pantalla de Reportes y se definió una re-auditoría posterior a las mejoras de rendimiento y accesibilidad. |
| H21 y H22 | Se mejoró el Tracking Plan agregando campos diferenciadores como `test_scenario` y se propusieron índices para optimizar consultas sobre eventos relevantes. |
| H24 | Se reformuló US16 para evitar asumir resultados experimentales no validados. La historia fue redactada como una necesidad pendiente de validación. |
| H25 y H38 | Se revisó la priorización del backlog, dando mayor prioridad a funcionalidades que demuestran valor principal para el dueño de bodega antes de monetización o expansión. |
| H26 | Se incorporaron las Technical Stories TS16, TS17, TS18 y TS19 dentro de la tabla de priorización del backlog, indicando su relación con las historias funcionales. |
| H27 y H28 | Se reformularon las épicas EP-11 y EP-12 para que representen objetivos amplios de producto y no historias demasiado específicas. |
| H29, H31 y H32 | Se dividieron o precisaron historias de usuario con alcance amplio, separando funcionalidades distintas para facilitar su validación e implementación. |
| H30 | Se separaron los criterios funcionales de US16 de las especificaciones visuales o de diseño, dejando los detalles de paleta y contraste como criterios técnicos de accesibilidad. |
| H33 | Se reformuló US20 para comparar el ahorro estimado por reducción de mermas frente al costo del plan, evitando afirmar que la suscripción elimina completamente las pérdidas. |
| H34, H35 y H36 | Se ajustaron las Technical Stories para especificar correctamente el rol responsable, ya sea frontend o backend, y se agregaron escenarios técnicos como errores, reintentos, validaciones y registro de estados. |
| H37 | Se redujo el alcance de historias con estimaciones altas, dividiéndolas en historias más pequeñas y manejables para un ciclo de desarrollo corto. |

En conclusión, las modificaciones realizadas permitieron mejorar la coherencia del Capítulo VIII, reforzar la trazabilidad entre los artefactos del enfoque Experiment-Driven Development y corregir inconsistencias detectadas durante la auditoría recibida. Asimismo, se fortaleció la justificación de los experimentos, la definición de métricas, la priorización del backlog y la claridad de las historias funcionales y técnicas.