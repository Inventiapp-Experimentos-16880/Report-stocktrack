# Capítulo V: Product Implementation

## 5.1 Software Configuration Management

### 5.1.1 Software Development Environment Configuration

**Project Management:**

Para la gestión de nuestro proyecto, hemos utilizado como principal medio de comunicación WhatsApp, a través de un grupo en el cual planificamos reuniones y compartimos nuestras ideas sobre cada parte del trabajo. También utilizamos la aplicación de Discord, para realizar reuniones y conversar en modalidad virtual. Asimismo se utilizó Github el cual elaboramos un repositorio con todos los integrantes del grupo. En esta, hicimos la creación del documento para trabajar de manera colaborativa y también la documentación de las aplicaciones. 

**Requirements Management:**

Para el registro de las historias de usuario, utilizamos la herramienta de Jira, en la cual se registró cada una de ellas y se ordenaron por prioridad en el Product Backlog.

**Product UX/UI Design:**

Se realizaron los productos de UX con la herramienta de UXPressia, así como las User Persona, Impact Mapping, entre otras. Por ello se pudo modelar de manera efectiva el diseño de la experiencia de usuario. Por otro lado, se realizaron los prototipos de la aplicación web utilizando la herramienta Figma, lo cual nos permitió realizae los Wireframes y Mock-ups para tener una mejor perspectiva de la aplicación.

**Software Development:**

Para el desarrollo del proyecto, se ha definido un stack tecnológico especializado que permite una separación clara entre las capas de la aplicación:

- Entornos de Desarrollo (IDEs): El flujo de trabajo se centraliza en herramientas de JetBrains para maximizar la productividad. Se utiliza WebStorm como entorno principal para el desarrollo del frontend e IntelliJ IDEA para la gestión y construcción del backend.
- Tecnologías Frontend: La aplicación web se desarrolla bajo el framework Angular, utilizando HTML, CSS y JavaScript para la creación de interfaces dinámicas y responsivas.
- Tecnologías Backend: Se utiliza Spring Boot para el desarrollo del lado del servidor, aprovechando su robustez para la implementación de la lógica de negocio.
- Control de Versiones y Gestión: Se utiliza GitHub como plataforma central para el alojamiento de repositorios, permitiendo un control detallado del historial de cambios y una colaboración eficiente mediante Git.

### 5.1.2 Source Code Management

Para la gestión de versiones, el proyecto adoptará el modelo GitFlow, utilizando GitHub como repositorio y plataforma principal. En las siguientes secciones se detallará la aplicación de este flujo de trabajo, además de proporcionar los enlace correspondiente de cada repositorio.

Repositorio de GitHub:
- Enlace para acceder a la organización en GitHub: https://github.com/Inventiapp-Experimentos-16880

- Enlace para acceder al repositorio de la landing Page: https://github.com/Inventiapp-Experimentos-16880/Landing-page-stocktrack

- Enlace para acceder al repositorio del reporte: https://github.com/Inventiapp-Experimentos-16880/Report-stocktrack

- Enlace para acceder al repositorio de la App Web: https://github.com/Inventiapp-Experimentos-16880/Front-Inventiapp

- Enlace para acceder al repositorio del back end: https://github.com/Inventiapp-Experimentos-16880/Backend-stocktrack

**Flujo de trabajo GitFlow**

El ciclo de desarrollo se gestionará implementando el modelo de ramas diseñado por Vincent Driessen en 'A successful Git branching model'.

[FALTA PONER IMAGEN DEL NETWORK DEL REPOSITORIO]

Estructura de branches (Ramas):

1. Main (Rama Principal): Constituye el eje central del repositorio, reservada exclusivamente para versiones estables y productivas del software. El código alojado aquí debe haber superado rigurosos procesos de validación y pruebas previas en las ramas de funcionalidad y desarrollo.

2. Develop (Rama de Desarrollo): Actúa como el entorno de integración continua para el equipo. Su función principal es centralizar el progreso diario del proyecto, sirviendo de base para la consolidación de nuevas características antes de su despliegue final.

3. Features (Ramas de Funcionalidad): Se empleará una rama independiente para cada módulo o tarea específica. Una vez concluida y verificada la funcionalidad, esta se integrará a la rama Develop. Para mantener el orden, se aplicará una nomenclatura estandarizada bajo el patrón "feature/chapter-#".

### 5.1.3 Source Code Style Guide & Conventions

En el desarrollo de este trabajo, se utilizará una gran variedad de lenguajes y frameworks para trabajar en la Landing Page, el Frontend Web Application y los Web Services. Para ello, se utilizará la siguiente guía de estilos y convenciones.

#### HTML
Es el lenguaje utilizado para estructurar el contenido de las interfaces, brindando los elementos necesarios para la interacción del usuario. 
Referencia: [https://www.w3schools.com/html/html5_syntax.asp](https://www.w3schools.com/html/html5_syntax.asp)

*   Declarar siempre el tipo de documento en la primera línea con `<!DOCTYPE html>`.
*   Respetar la estructura básica del HTML: `<html>`, `<head>`, `<body>`.
*   Declarar el título de la página para dar a conocer al usuario en qué página se encuentra usando el elemento `<title>`.
*   Siempre cerrar los elementos que lo requieran, ya sea una división, párrafo o título.
*   Declarar el atributo `alt` para todas las imágenes para asegurar la accesibilidad.
*   Se usará una indentación coherente para lograr una lectura sencilla del código y sus niveles de anidamiento.

#### CSS
Es el lenguaje utilizado para definir el diseño visual, incluyendo los estilos, fuentes, colores y contenedores.
Referencia: [https://google.github.io/styleguide/htmlcssguide.html](https://google.github.io/styleguide/htmlcssguide.html)

*   Usar indentación de forma correcta para mantener el orden.
*   Los nombres para los elementos y clases deben ser cortos y en minúsculas.
*   Declarar los colores en código hexadecimal (Ejemplo: #024A86).
*   Dejar comentarios para conocer el propósito del estilo y su uso dentro de la hoja de estilos.
*   El diseño debe ser responsive para que los usuarios lo visualicen cómodamente desde cualquier dispositivo.

#### TypeScript (Angular)
Es el superconjunto de JavaScript que añade tipado estático y funciones avanzadas para el desarrollo del Frontend.
Referencia: [https://www.typescriptlang.org/docs/handbook/intro.html](https://www.typescriptlang.org/docs/handbook/intro.html)

*   Declarar nombres significativos y consistentes para las variables y funciones.
*   Declarar interfaces y tipos utilizando `PascalCase`.
*   Declarar variables y funciones utilizando `camelCase`.
*   Evitar el uso del tipo `any` para aprovechar las ventajas del tipado fuerte.
*   Usar interfaces para la reutilización de código y contratos de datos claros.
*   Dejar comentarios para explicar la lógica de los servicios y componentes complejos.

#### Angular
Framework utilizado para la creación de la aplicación web principal de forma modular y escalable.
Referencia: [https://angular.io/docs](https://angular.io/docs)

*   Mantener una estructura de carpetas organizada separando components, services, models y modules.
*   Crear componentes reutilizables para evitar la duplicación de código en la interfaz.
*   Separar la lógica de negocio de la vista, delegando el consumo de APIs a los servicios.
*   Utilizar la inyección de dependencias de forma correcta para mantener el código desacoplado.
*   Documentar el propósito de los componentes mediante comentarios internos.

#### Astro
Framework utilizado para el desarrollo de la Landing Page, optimizando el rendimiento y la velocidad de carga.
Referencia: [https://docs.astro.build/](https://docs.astro.build/)

*   Utilizar la arquitectura de "islas" para minimizar el envío de JavaScript innecesario al cliente.
*   Organizar los componentes globales de la landing en la carpeta `src/components`.
*   Aprovechar el sistema de rutas basado en archivos dentro de la carpeta `src/pages`.
*   Optimizar el uso de recursos multimedia mediante los componentes nativos de Astro.

#### Java (Spring Boot)
Lenguaje y framework utilizado para el desarrollo de los Web Services y la lógica del lado del servidor.
Referencia: [https://google.github.io/styleguide/javaguide.html](https://google.github.io/styleguide/javaguide.html)

*   Nombrar las variables, funciones y clases con `camelCase` o `PascalCase` según corresponda, siendo significativos y cortos.
*   Seguir los principios de **Clean Architecture**, separando la lógica de dominio de la infraestructura.
*   Usar indentación correctamente para un código coherente y ordenado.
*   Usar comillas dobles (") para las cadenas de texto.
*   Utilizar las anotaciones de Lombok para reducir el código repetitivo y mejorar la legibilidad.
*   Dejar comentarios en cada bloque de código relevante para explicar su funcionalidad.

### 5.1.4 Software Deployment Configuration

## 5.2 Product Implementation & Deployment

Durante este sprint decisivo, el equipo de desarrollo llevó a cabo la implementación, integración y despliegue de todas las capas del software. Se trabajó en paralelo en el desarrollo de la Landing Page, la Aplicación Web (Frontend en Angular) y la API RESTful (Backend en Spring Boot), culminando con el despliegue del sistema completo en la nube.

### 5.2.1 Sprint Backlogs

Para este sprint de implementación integral, el backlog reunió todas las historias de usuario necesarias para garantizar el funcionamiento *End-to-End* de la aplicación (Landing Page, Frontend y Backend). A continuación, se detalla cada Historia de Usuario desarrollada, las tareas técnicas implicadas y sus responsables:

| **ID** | **Historia de Usuario (Title)** | **Descripción del Trabajo Realizado (Backend & Frontend / Diseño)** | **Asignado a** | **Estado** |
| :--- | :--- | :--- | :--- | :--- |
| **US-18** | Sección de funcionalidades | Definición de estructura e implementación visual de la sección de beneficios en la Landing Page. | Antonio | Done |
| **US-19** | Formulario de registro (Landing) | Implementación de contenido, llamados a la acción (CTAs) y validaciones visuales. | Giovany | Done |
| **US-20** | Formulario de contacto | Diseño, maquetación y aplicación de estilos de las cards y sección de contacto. | Dayro | Done |
| **US-21** | Diseño responsive | Adaptación del layout de todas las secciones de la Landing a distintos breakpoints móviles y tablet. | Giovany | Done |
| **US-22** | Sección de testimonios | Maquetación HTML/CSS e integración de los testimonios de usuarios en la Landing Page. | Dayro | Done |
| **US-23** | Botones claros | Diseño del Hero principal y botones con contraste adecuado para conversión. | Dayro | Done |
| **US-28** | Login de usuarios | **Full-Stack:** Creación de endpoint `/auth/login`, generación de token JWT, vista Angular e implementación de AuthGuard. | Antonio | Done |
| **US-29** | Registro de usuarios | **Full-Stack:** Endpoint `/auth/register` con encriptación, validación de duplicados y conexión al formulario de UI. | Antonio | Done |
| **US-30** | Dashboard principal | **Full-Stack:** Servicio de métricas en API y conexión con widgets interactivos (gráficos y totales) en Angular. | Giovany | Done |
| **US-24** | Módulo de proveedores | **Full-Stack:** Creación de endpoints REST (GET, POST, PUT, DELETE) y formularios UI para la gestión de proveedores. | Dayro | Done |
| **US-25** | Listado de proveedores | **Full-Stack:** Filtros, búsqueda dinámica y tabla paginada en Angular conectada al backend. | Dayro | Done |
| **US-26** | Salida de producto | **Full-Stack:** Endpoint `/inventory/out` para validar stock, y formulario frontend para registrar mercancía saliente. | Giovany | Done |
| **US-27** | Integración de salida con inventario | **Full-Stack:** Servicio backend para descontar cantidades de la base de datos y refrescar la tabla del frontend en tiempo real. | Dayro | Done |
| **US-31** | Administración de personal | **Full-Stack:** Configuración de rutas protegidas en API y vistas base en Angular para la gestión de usuarios del sistema. | Antonio | Done |
| **US-32** | CRUD de personal | **Full-Stack:** Endpoints y formularios UI para crear, editar, listar y eliminar personal interno del sistema. | Yaku | Done |
| **US-33** | Integración con dashboard | **Full-Stack:** Lógica de autorización y roles (backend) para controlar qué módulos se ocultan/muestran en el menú del frontend. | Antonio | Done |
| **US-34** | Módulo de inventario | **Full-Stack:** Endpoints de productos, interfaz con tabla, buscador y filtros en Angular. | Yaku | Done |
| **US-35** | Actualización de stock | **Full-Stack:** Endpoint `/inventory/in` y formularios UI para registrar entradas de mercancía y ajustes manuales. | Yaku | Done |
| **US-36** | Visualización de movimientos | **Full-Stack:** Creación de endpoint e interfaz para listar el historial de transacciones (entradas, salidas, ajustes). | Yaku | Done |
| **US-37** | Integración inventario–proveedores | **Full-Stack:** Consulta relacional en base de datos para devolver el proveedor asociado y visualizarlo en el detalle de producto en UI. | Yaku | Done |

### 5.2.2 Implemented Landing Page Evidence

El equipo completó el diseño interactivo y el despliegue de la página de aterrizaje (Landing Page) promocional para StockTrack, utilizando tecnologías web modernas para asegurar su rapidez y diseño responsive.
* **Plataforma de Despliegue:** Vercel
* **Link de despliegue:** [link](link)
* **Evidencia en Video:** [link](link)
* **Características Implementadas:** Hero interactivo, sección de características y beneficios, planes de suscripción (PricingSection), testimonios de usuarios y formularios de contacto.

### 5.2.3 Implemented Frontend-Web Application Evidence

Se construyó una Single Page Application (SPA) robusta utilizando el framework Angular. Esta aplicación es el núcleo visual del sistema, donde los usuarios interactúan con los módulos de negocio.
* **Plataforma de Despliegue:** Vercel
* **Link de Despliegue:** [https://front-inventiapp.vercel.app/auth/login](https://front-inventiapp.vercel.app/auth/login)
* **Módulos implementados y conectados:**
  * **Seguridad:** Login y Registro protegidos por AuthGuards e interceptores HTTP para enviar el token JWT.
  * **Dashboard:** Panel de control con navegación lateral (Sidebar) y métricas de negocio.
  * **Gestión Operativa:** Vistas dinámicas para Inventario (entradas, salidas, reposición) y Proveedores.
  * **Administración:** Gestión de usuarios del sistema, asignación de roles y permisos.


### 5.2.4 Implemented RESTful API and/or Serverless Backend Evidence

Se implementó el backend del sistema utilizando Java y Spring Boot bajo el enfoque de *Domain-Driven Design* (DDD). La API expone servicios REST seguros para interactuar con una base de datos relacional PostgreSQL/MySQL.
* **Plataforma de Despliegue:** Railway (Backend + Database)
* **Base API URL:** [https://backend-stocktrack-production.up.railway.app/api/v1](https://backend-stocktrack-production.up.railway.app//api/v1)
* **Evidencia de Ejecución:** El funcionamiento completo de la API fue validado a través de colecciones en Postman, comprobando respuestas HTTP correctas (200 OK, 201 Created, 401 Unauthorized, 404 Not Found) para casos de éxito y manejo de excepciones en las operaciones de negocio.

### 5.2.5 RESTful API documentation

Se utilizó la especificación OpenAPI (Swagger) para garantizar una documentación clara, interactiva y estandarizada. Esta herramienta fue fundamental para que el equipo frontend pudiera consumir los endpoints correctamente durante el sprint.
* **Swagger API URL:** [https://backend-stocktrack-production.up.railway.app/swagger-ui/index.html](https://backend-stocktrack-production.up.railway.app/swagger-ui/index.html)
* **Módulos y Endpoints Documentados:**
  * **Autenticación (`/api/v1/authentication`):** Endpoints `sign-in` y `sign-up` para generación de JWT.
  * **Productos (`/api/v1/products`):** GET, POST, PUT, DELETE para la gestión del catálogo.
  * **Lotes (`/api/v1/batches`):** Gestión de lotes, vencimientos e historial.
  * **Ventas (`/api/v1/sales`):** Registro y consulta de transacciones de salida.
  * **Proveedores (`/api/v1/providers`):** Administración de la cadena de suministro.
  * **Seguridad (`/api/v1/users`, `/api/v1/roles`):** CRUD de perfiles y roles del sistema.

### 5.2.6 Team Collaboration Insights

Al ejecutar todas las fases del desarrollo en este sprint, la colaboración del equipo requirió alta sincronización mediante GitHub y Discord:


## 5.3 Video About-the-Product
