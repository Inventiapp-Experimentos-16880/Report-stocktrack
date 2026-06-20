# Capítulo VII: DevOps Practices

## 7.1. Continuous Integration

### 7.1.1. Tools and Practices

Para la Integración Continua (CI) de StockTrack/Inventiapp, el equipo se apoya en el modelo de control de versiones **GitFlow** y en **GitHub** como plataforma central para alojar los repositorios. La práctica principal consiste en automatizar la verificación del código cada vez que un desarrollador integra una nueva funcionalidad (desde una rama `feature/chapter-#`) hacia la rama `develop`.

Las herramientas utilizadas incluyen **Railway** (backend) y **Vercel** (frontend) como plataformas de despliegue continuo, las cuales detectan automáticamente cada push al repositorio y ejecutan el proceso de build sin necesidad de un workflow adicional. **GitHub Actions** está disponible en el repositorio para la configuración de pipelines de testing automatizado.
<div align="center">

| Herramienta | Tipo | Descripción | Propósito |
|:---:|---|---|---|
| <img src="https://junit.org/junit5/assets/img/junit5-logo.png" height="32"/><br>**JUnit** | Testing (TDD) | Framework de pruebas unitarias para Java. | Validar que las entidades del dominio (Inventario, Producto, Alerta) funcionen correctamente de forma aislada. |
| <img src="https://github.com/user-attachments/assets/7204ddbe-cc40-44a8-9221-d7a2e7400f16" height="50"/><br>**Mockito** | Simulación (TDD) | Librería para crear mocks y stubs de dependencias externas. | Aislar la lógica de negocio del backend durante las pruebas sin acceder a la base de datos real. |
| <img src="https://www.selenium.dev/images/selenium_logo_square_green.png" height="32"/><br>**Selenium** | Pruebas E2E | Herramienta de automatización de navegadores web. | Validar flujos completos de usuario sobre la interfaz de StockTrack (registro, inventario, alertas). |
| <img src="https://avatars.githubusercontent.com/u/44036562" height="32"/><br>**GitHub Actions** | Orquestación CI | Plataforma de automatización integrada en GitHub. |Disponible para configurar pipelines de testing automatizado (unitarias, integración, BDD) ante cada push o Pull Request. |

</div>

### 7.1.2. Build & Test Suite Pipeline Components

El pipeline de integración consta de los siguientes componentes según la capa del proyecto:

**Frontend (Web App en Angular y Landing en Astro)**

1. Instalación de dependencias (`npm install`)
2. Construcción del proyecto (`npm run build`)
3. Ejecución de pruebas de interfaz y responsividad con Selenium

**Backend (API en Spring Boot)**

1. Compilación del proyecto Java con Maven
2. Validación de la Clean Architecture
3. Ejecución de pruebas unitarias (JUnit, Mockito) y de integración
4. Ejecución de escenarios BDD con Cucumber

<div align="center">
  <table>
    <tr>
      <td align="center">
        <img width="720" alt="Railway — Build y despliegue automático del backend" src="https://github.com/user-attachments/assets/1c8f386a-3e15-4548-af3a-73da5cf0c916" />
        <br><em>Railway — Build y despliegue automático del backend ante cada commit en main</em>
      </td>
    </tr>
  </table>
</div>

---

## 7.2. Continuous Delivery

### 7.2.1. Tools and Practices

La Entrega Continua asegura que cualquier código validado en la fase de CI esté listo para ser desplegado en entornos de staging. La práctica central es mantener la rama `develop` siempre en un **estado desplegable**.

<div align="center">

| Herramienta | Rol | Función en StockTrack |
|:---:|---|---|
| <img src="https://avatars.githubusercontent.com/u/44036562" height="32"/><br>**GitHub Actions** | Orquestación del pipeline | Disponible para configurar pipelines de testing automatizado (unitarias, integración, BDD) ante cada push o Pull Request. |
| <img src="https://assets.vercel.com/image/upload/v1607554385/repositories/vercel/logo.png" height="32"/><br>**Vercel** | Hosting Frontend (Staging) | Genera URLs de preview automáticas para el frontend Angular y el Landing Astro. |
| <img src="https://railway.com/brand/logo-light.png" height="32"/><br>**Railway** | Backend + BD (Staging) | Actualiza el servicio Spring Boot en staging sin afectar producción. Gestiona MySQL con backups automáticos. |
| <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" height="32"/><br>**Docker** | Contenerización | Empaqueta el backend garantizando consistencia entre entornos de desarrollo, staging y producción. |

</div>

**Prácticas aplicadas:**

- **Feature Branching y Merge Requests:** el código se fusiona a `develop` solo tras pasar el CI y recibir aprobación vía Pull Request.
- **Pipeline de Validación en Staging:** los cambios se validan en un entorno que replica producción antes del despliegue definitivo.
- **Despliegue Semiautomático:** Vercel y Railway preparan el entorno, pero la promoción a producción requiere aprobación del equipo.
- **Aprobación Manual:** el responsable del proyecto revisa los resultados del staging antes de autorizar el despliegue.
- **Rollback Manual Controlado:** ante errores en staging, el equipo revierte desde los dashboards de Vercel y Railway.

### 7.2.2. Stages Deployment Pipeline Components

<div align="center">

| Etapa | Descripción |
|:---:|---|
| **1. Trigger de Integración** | Tras el éxito del Build & Test Suite en `develop`, el pipeline de CD se activa automáticamente. |
| **2. Despliegue en Staging** | Vercel genera una URL de preview para el frontend. Railway actualiza el backend en el entorno de pruebas. |
| **3. Validación del Sistema** | Ejecución de pruebas E2E con Selenium sobre las URLs de preview generadas. |
| **4. Aprobación del Despliegue** | El pipeline queda en espera hasta que el responsable apruebe la promoción a producción. |
| **5. Monitoreo y Feedback** | Se recopilan métricas del staging (tiempos de respuesta, errores) como insumo para la decisión de despliegue. |

</div>

<div align="center">
  <table>
    <tr>
      <td align="center">
        <img width="540" alt="Vercel — Preview Deployments - URLs de Preview por PR" src="https://github.com/user-attachments/assets/ec9b44ae-9894-4340-a392-7b726114ab8e" />
        <br><em>Vercel — URLs de Preview generadas automáticamente por PR</em>
      </td>
      <td align="center">
        <img width="540" alt="Railway — Staging - Entorno del backend" src="https://github.com/user-attachments/assets/51ce24b0-a66f-4c98-a557-ff2e1864f32b" />
        <br><em>Railway — Entorno de staging del backend</em>
      </td>
    </tr>
  </table>
</div>

---

## 7.3. Continuous Deployment

### 7.3.1. Tools and Practices

El Despliegue Continuo garantiza que el código fusionado en la rama `main` —reservada exclusivamente para versiones estables— se despliegue **automáticamente** a los usuarios finales. Las integraciones directas entre **GitHub, Vercel y Railway** detectan cambios en la rama principal y aplican los cambios a producción de forma transparente.

<div align="center">

| Herramienta | Rol | Función en StockTrack |
|:---:|---|---|
| <img src="https://avatars.githubusercontent.com/u/44036562" height="32"/><br>**GitHub Actions** | Orquestación del Pipeline | Disponible para configurar pipelines de testing automatizado (unitarias, integración, BDD) ante cada push o Pull Request. |
| <img src="https://assets.vercel.com/image/upload/v1607554385/repositories/vercel/logo.png" height="32"/><br>**Vercel** | Despliegue Frontend | Despliega automáticamente Angular y Astro en los dominios productivos. |
| <img src="https://railway.com/brand/logo-light.png" height="32"/><br>**Railway** | Backend + BD Producción | Despliega el Spring Boot API y aplica migraciones MySQL en producción. |
| <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" height="32"/><br>**Docker** | Contenerización | Empaqueta el backend y facilita el rollback automático a imágenes anteriores. |
| <img src="https://upload.wikimedia.org/wikipedia/commons/5/52/Apache_Maven_logo.svg" height="32"/><br>**Maven** | Build Backend | Compila el proyecto Java y genera el artefacto JAR para la imagen Docker. |

</div>

**Prácticas aplicadas:**

- **Commit-based Deployment:** cada merge a `main` activa el pipeline completo de build, test y despliegue automático.
- **Rollback Automático:** ante fallos post-despliegue, el pipeline revierte a la imagen Docker anterior en Railway y a la versión previa en Vercel.
- **Preview Deployments:** Vercel genera URLs de preview por cada Pull Request antes del merge a `main`.

### 7.3.2. Production Deployment Pipeline Components

**Pipeline del Frontend (Vercel — Angular + Astro)**

1. Vercel detecta el merge a `main` y compila Angular en modo producción.
2. Se ejecutan las pruebas E2E con Selenium sobre el entorno de staging previo.
3. Vercel despliega la nueva versión en los dominios productivos:
   - **Landing Page:** `landing-stocktrack.vercel.app`
   - **Web App:** `front-inventiapp.vercel.app`
4. La CDN global de Vercel distribuye los assets e invalida automáticamente la caché.

<div align="center">
  <table>
    <tr>
      <td align="center">
        <img width="540" alt="Vercel — Production Active (Landing)" src="https://github.com/user-attachments/assets/6e5240b9-2d74-42ba-9b26-ed2318eb3498" />
        <br><em>Vercel — Landing Page en estado Production Active</em>
      </td>
      <td align="center">
        <img width="540" alt="Vercel — Production Active (Web App)" src="https://github.com/user-attachments/assets/aba5cab7-32d9-4aaa-87a2-ae96bc9ecd08" />
        <br><em>Vercel — Web App en estado Production Active</em>
      </td>
    </tr>
  </table>
</div>

**Pipeline del Backend (Railway — Spring Boot + MySQL)**

1. Railway detecta el merge a `main` en el repositorio `Backend-stocktrack`.
2. Maven compila el proyecto y genera el artefacto JAR.
3. Railway construye la imagen Docker y despliega en producción:
   - **URL productiva:** `backend-stocktrack-production.up.railway.app`
4. Spring Boot aplica automáticamente las migraciones de base de datos MySQL pendientes.
5. Railway monitorea el servicio y genera alertas ante anomalías.
6. Swagger UI publica automáticamente la documentación actualizada de la API REST.

<div align="center">
  <table>
    <tr>
      <td align="center">
        <img width="540" alt="Railway — Backend Production" src="https://github.com/user-attachments/assets/e2df0a3a-f88e-4dc7-b991-639109911009" />
        <br><em>Railway — Backend en estado Active con URL productiva</em>
      </td>
      <td align="center">
        <img width="540" alt="Railway — MySQL Production" src="https://github.com/user-attachments/assets/73a640a2-87c3-483b-b078-fb4be91ac7a4" />
        <br><em>Railway — Base de datos MySQL en producción</em>
      </td>
    </tr>
  </table>
</div>

<div align="center">
  <table>
    <tr>
      <td align="center">
        <img width="720" alt="image" src="https://github.com/user-attachments/assets/d45ca3c2-6280-42da-99f4-d8cd0e6e9728" />
        <br><em>Flujo completo del pipeline: desde el commit en main hasta los usuarios finales</em>
      </td>
    </tr>
  </table>
</div>

## 7.4. Continuous Monitoring

El monitoreo continuo en **StockTrack** tiene como objetivo revisar de manera constante el estado del sistema después de su despliegue. Esto permite detectar errores, problemas de rendimiento, caídas del servicio, fallos en la API o comportamientos inesperados en la aplicación web.

Esta práctica es importante porque StockTrack maneja información relacionada con usuarios, inventario, productos, proveedores, ventas y reportes. Por ello, el sistema debe mantenerse disponible, estable y con tiempos de respuesta adecuados para los usuarios.

En el proyecto, el monitoreo se enfoca principalmente en el **backend desarrollado con Spring Boot**, el **frontend desarrollado con Angular**, la **base de datos MySQL** y los servicios de despliegue utilizados. Para ello, se consideran herramientas como **RedLine13 sobre AWS**, **WebPageTest by Catchpoint**, **Google Lighthouse**, **Railway**, **Vercel**, **Postman** y **Swagger/OpenAPI**.

Estas herramientas permiten revisar el rendimiento de la aplicación, validar la disponibilidad de los servicios, comprobar el funcionamiento de los endpoints y detectar posibles problemas antes de que afecten al usuario final.

---

### 7.4.1. Tools and Practices

Para llevar a cabo el monitoreo continuo en StockTrack, se utilizaron herramientas y prácticas orientadas a evaluar el rendimiento, disponibilidad y correcto funcionamiento de los principales componentes del sistema. Estas herramientas ayudan a revisar tanto la experiencia del usuario en el frontend como el comportamiento del backend y su comunicación con la base de datos.

- **RedLine13 sobre AWS:**  
  RedLine13 se utiliza para realizar pruebas de carga en la nube utilizando infraestructura de AWS. En StockTrack, esta herramienta permite simular múltiples usuarios realizando acciones dentro del sistema, como iniciar sesión, consultar productos, registrar movimientos de inventario, generar ventas o revisar reportes.

  Su uso ayuda a evaluar si el sistema mantiene tiempos de respuesta adecuados cuando aumenta la cantidad de solicitudes concurrentes. Además, permite identificar posibles cuellos de botella en el backend, problemas de rendimiento en la API REST o limitaciones en la comunicación con la base de datos.

<!-- Imagen recomendada: logo o captura general de RedLine13 mostrando una prueba de carga -->
![RedLine13 sobre AWS](/assets/img/chapter-VII/RedLine13%20sobre%20AWS.png)

- **WebPageTest by Catchpoint:**  
  WebPageTest by Catchpoint se utiliza para analizar el rendimiento web de StockTrack desde el navegador. Esta herramienta permite evaluar métricas como tiempo de carga, Speed Index, First Contentful Paint, Largest Contentful Paint y waterfall de recursos.

  En el proyecto, WebPageTest ayuda a identificar si existen recursos pesados, demoras en la carga inicial, problemas de renderizado o elementos que afecten la experiencia del usuario en la aplicación web.

<!-- Imagen recomendada: captura de WebPageTest con resultados de performance o waterfall -->
![WebPageTest by Catchpoint](/assets/img/chapter-VII/WebPageTest%20by%20Catchpoint.png)

- **Google Lighthouse:**  
  Google Lighthouse se utiliza como herramienta de auditoría para evaluar la calidad del frontend web. Esta herramienta permite revisar aspectos como rendimiento, accesibilidad, buenas prácticas y SEO.

  En StockTrack, Lighthouse ayuda a identificar oportunidades de mejora relacionadas con tiempos de carga, optimización de recursos, accesibilidad de la interfaz y buenas prácticas de desarrollo web.

<!-- Imagen recomendada: captura de resultados de Lighthouse con puntajes de Performance, Accessibility, Best Practices y SEO -->
![Google Lighthouse](/assets/img/chapter-VII/Google%20Lighthouse.png)

- **Railway:**  
  Railway se utiliza para revisar el estado del despliegue del backend y la base de datos. Desde esta plataforma es posible observar logs, errores de ejecución, reinicios del servicio, variables de entorno y posibles fallos de conexión con MySQL.

  En StockTrack, Railway ayuda a detectar problemas relacionados con la disponibilidad del backend, errores internos del servidor, fallos durante el despliegue o problemas al conectarse con la base de datos en producción.

<!-- Imagen recomendada: captura del dashboard de Railway mostrando el servicio backend o base de datos -->
![Railway](/assets/img/chapter-VII/Railway.png)

- **Vercel:**  
  Vercel se utiliza para el despliegue del frontend web o landing page del proyecto. Esta plataforma permite revisar el estado de los despliegues, errores de build y disponibilidad de la aplicación.

  En el caso de StockTrack, Vercel permite comprobar si los cambios realizados en el frontend se publican correctamente y si la aplicación se encuentra accesible para los usuarios.

<!-- Imagen recomendada: captura del deployment de Vercel o dashboard del proyecto desplegado -->
![Vercel](/assets/img/chapter-VII/Vercel.png)

- **Postman y Swagger/OpenAPI:**  
  Postman y Swagger/OpenAPI se utilizan para validar el correcto funcionamiento de la API REST del backend. Swagger permite visualizar la documentación de los endpoints disponibles, mientras que Postman permite probar solicitudes hacia rutas importantes como autenticación, productos, inventario, ventas, proveedores y reportes.

  Estas herramientas permiten verificar que los endpoints respondan correctamente, que la autenticación con JWT funcione y que las operaciones principales del sistema no presenten errores.

<!-- Imagen recomendada: captura de Swagger con endpoints del backend o captura de Postman probando una ruta de la API -->
![Postman y Swagger](/assets/img/chapter-VII/Postman%20y%20Swagger.png)

---

### 7.4.2. Monitoring Pipeline Components

El pipeline de monitoreo de StockTrack está compuesto por diferentes etapas que permiten observar el comportamiento del sistema desde la interfaz web hasta el backend y la base de datos. Este flujo ayuda a detectar errores en distintos puntos del sistema y facilita la toma de decisiones para corregir problemas.

Primero, se monitorea el **frontend web** desplegado. Para esta etapa se utilizan herramientas como **WebPageTest by Catchpoint** y **Google Lighthouse**, las cuales permiten evaluar el rendimiento de la aplicación, tiempos de carga, accesibilidad, buenas prácticas y experiencia general del usuario.

Luego, se revisa la comunicación entre el frontend y la **API REST**. Esta parte se valida mediante **Postman** y **Swagger/OpenAPI**, comprobando que los endpoints principales respondan correctamente. Entre las rutas más importantes se consideran autenticación, consulta de productos, registro de inventario, ventas, proveedores y reportes.

En el **backend Spring Boot**, el monitoreo se realiza mediante la revisión de logs, errores HTTP, tiempos de respuesta y estado del despliegue en Railway. Esta etapa permite identificar errores internos del servidor, problemas de autenticación con JWT, fallos de autorización, errores de validación o fallos de conexión con la base de datos.

También se considera el uso de **RedLine13 sobre AWS** dentro del pipeline, ya que permite ejecutar pruebas de carga para evaluar cómo responde el sistema ante múltiples usuarios o solicitudes concurrentes. Con los resultados de estas pruebas, el equipo puede analizar si el backend mantiene un rendimiento adecuado y si la aplicación soporta una mayor demanda.

Finalmente, se monitorea la **base de datos MySQL**, ya que es un componente importante para la persistencia de usuarios, productos, inventario, proveedores, ventas y reportes. En esta etapa se revisan posibles errores de conexión, lentitud en consultas, fallos al guardar información o problemas de disponibilidad.

El flujo del pipeline de monitoreo puede resumirse de la siguiente manera:

1. El usuario accede al frontend web de StockTrack.
2. WebPageTest y Lighthouse permiten revisar el rendimiento y calidad de la interfaz.
3. El frontend realiza solicitudes hacia la API REST.
4. Postman y Swagger/OpenAPI permiten validar manualmente los endpoints.
5. El backend Spring Boot procesa las solicitudes.
6. RedLine13 permite ejecutar pruebas de carga sobre el sistema.
7. Railway permite revisar logs, errores y estado del despliegue.
8. La base de datos MySQL almacena o devuelve la información solicitada.
9. El equipo revisa los resultados y aplica correcciones cuando sea necesario.

Este pipeline permite tener una visión más completa del funcionamiento de StockTrack y facilita la detección de errores en diferentes partes del sistema.

<!-- Imagen recomendada: diagrama general del pipeline: Usuario -> Frontend -> API REST -> Backend -> MySQL -> Herramientas de monitoreo -->
![Monitoring Pipeline](/assets/img/chapter-VII/pip1.png)

---

### 7.4.3. Alerting Pipeline Components

El componente de alertas permite detectar problemas importantes dentro de StockTrack y notificar al equipo cuando ocurre una situación que requiere atención. Las alertas ayudan a responder de manera más rápida ante errores del backend, caídas del servicio, problemas de base de datos o bajo rendimiento en el frontend.

En una primera etapa, las alertas pueden apoyarse en las herramientas utilizadas durante el monitoreo, como Railway, Vercel, WebPageTest, Lighthouse y RedLine13. Estas herramientas permiten identificar fallos de despliegue, problemas de carga, errores en la API o resultados negativos en pruebas de rendimiento.

En el backend, las alertas pueden enfocarse en los siguientes eventos:

- Caída del servicio desplegado.
- Errores HTTP 500 en endpoints importantes.
- Tiempo de respuesta alto en la API REST.
- Fallos de conexión con la base de datos MySQL.
- Errores durante el inicio de sesión o validación JWT.
- Problemas en operaciones críticas como registrar productos, ventas o reportes.

En el frontend, las alertas pueden relacionarse con:

- Fallos de build o despliegue en Vercel.
- Problemas de carga en la aplicación web.
- Bajo rendimiento detectado por WebPageTest o Lighthouse.
- Recursos demasiado pesados que afecten la experiencia del usuario.
- Errores al consumir la API del backend.

Con **RedLine13**, las alertas o resultados importantes se relacionan principalmente con las pruebas de carga. Por ejemplo, si al simular varios usuarios el sistema presenta tiempos de respuesta altos, errores en las solicitudes o caídas del backend, estos resultados deben ser revisados por el equipo para aplicar mejoras.

Como mejora futura, el pipeline de alertas podría complementarse con herramientas como **Prometheus**, **Alertmanager** y **Grafana**. Prometheus permitiría recolectar métricas del backend, Alertmanager gestionaría las reglas de alerta y Grafana permitiría visualizar dashboards con información del sistema.

Algunas reglas de alerta que podrían configurarse son:

- Notificar si la API no responde durante un periodo determinado.
- Notificar si el tiempo promedio de respuesta supera un límite definido.
- Notificar si aumenta la cantidad de errores HTTP 500.
- Notificar si la base de datos presenta fallos de conexión.
- Notificar si el consumo de recursos del servidor es demasiado alto.
- Notificar si las pruebas de carga muestran una tasa elevada de errores.

Este sistema permitiría que el equipo no dependa solamente de revisar manualmente los logs, sino que pueda recibir avisos cuando ocurra un problema importante en el sistema.

<!-- Imagen recomendada: diagrama o imagen representativa de alertas con Prometheus, Grafana o una campana de alerta conectada a backend/frontend -->
![Alerting Pipeline](/assets/img/chapter-VII/pip2.png)

---

### 7.4.4. Notification Pipeline Components

El componente de notificaciones se encarga de informar al equipo cuando una alerta o evento importante ocurre dentro del sistema. En StockTrack, estas notificaciones pueden estar relacionadas con errores de despliegue, fallos en la API, problemas de base de datos, resultados de pruebas de carga o problemas de rendimiento en el frontend.

En una primera versión, las notificaciones pueden realizarse mediante los propios servicios utilizados en el proyecto. Por ejemplo, **GitHub** puede notificar cambios en Pull Requests, commits o problemas relacionados con el repositorio. **Railway** puede mostrar errores del backend o problemas de despliegue, mientras que **Vercel** permite identificar errores de build o fallos durante la publicación del frontend.

Además, los resultados obtenidos en **WebPageTest**, **Lighthouse** y **RedLine13** pueden ser revisados por el equipo para detectar problemas de rendimiento. Si una prueba muestra tiempos de carga altos, mala puntuación de performance o errores bajo carga, el equipo puede registrar el incidente y priorizar una corrección.

El flujo de notificaciones puede organizarse de la siguiente manera:

1. Ocurre un evento en el sistema, como error en la API, caída del backend, fallo de despliegue o bajo rendimiento.
2. La herramienta de monitoreo detecta el problema.
3. Se genera una alerta o resultado que requiere revisión.
4. El equipo recibe o revisa la notificación en la herramienta correspondiente.
5. El integrante responsable analiza el problema.
6. Se aplica una corrección en el backend, frontend o configuración del despliegue.
7. Se vuelve a desplegar o ejecutar la prueba para confirmar que el problema fue solucionado.

Como mejora futura, se puede integrar un pipeline de notificaciones más completo utilizando **GitHub Actions**, **Railway**, **Vercel**, **Prometheus Alertmanager** y un canal de comunicación como **Discord**, **Slack** o correo electrónico. De esta forma, el equipo podría recibir avisos automáticos cuando fallen las pruebas, cuando un despliegue no se complete correctamente o cuando el backend presente errores críticos.

<!-- Imagen recomendada: diagrama de notificaciones: Herramientas de monitoreo -> Alerta -> Discord/Slack/Correo -> Equipo de desarrollo -->
![Notification Pipeline](/assets/img/chapter-VII/pip3.png)

En conclusión, el monitoreo continuo en StockTrack permite mantener un mejor control sobre el estado del sistema después del despliegue. Actualmente, el proyecto puede apoyarse en herramientas como **RedLine13 sobre AWS**, **WebPageTest by Catchpoint**, **Google Lighthouse**, **Railway**, **Vercel**, **Postman** y **Swagger/OpenAPI**. Además, el monitoreo podría fortalecerse en futuras iteraciones con herramientas como **Prometheus**, **Grafana**, **Alertmanager** y **GitHub Actions**, logrando un proceso más automatizado y completo.