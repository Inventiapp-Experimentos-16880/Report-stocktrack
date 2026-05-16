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
