# Capítulo III: Requirements Specification

## 3.1. To-Be Scenario Mapping.


## 3.2. User Stories

### User Stories
<!-- User Stories – Salida de producto / Venta (inventario + ganancia) -->
<!-- User Stories – Salida de productos (inventario + ganancia, con kits) -->

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
  <thead>
    <tr>
      <th style="width:8%;">Story ID</th>
      <th style="width:18%;">Título</th>
      <th style="width:24%;">Descripción técnica</th>
      <th style="width:40%;">Criterios de Aceptación</th>
      <th style="width:10%;">Relacionado con (Epic ID)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>US01</td>
      <td>Iniciar borrador de salida</td>
      <td>Como cajero, quiero iniciar un borrador de salida para agrupar ítems de una venta antes de confirmarla.</td>
      <td>
        <strong>Escenario 01: Borrador creado</strong><br>
        <strong>Dado</strong> que el usuario está en “Nueva venta”,<br>
        <strong>Cuando</strong> selecciona “Iniciar borrador”,<br>
        <strong>Entonces</strong> el sistema crea un borrador con ID único, estado <em>Draft</em> y fecha de inicio.<br><br>
        <strong>Escenario 02: Reanudación</strong><br>
        <strong>Dado</strong> un borrador en estado <em>Draft</em>,<br>
        <strong>Cuando</strong> el usuario lo reanuda,<br>
        <strong>Entonces</strong> el sistema muestra ítems, cantidades y totales parciales guardados.
      </td>
      <td>EP-04</td>
    </tr>
    <tr>
      <td>US02</td>
      <td>Gestionar ítems del borrador</td>
      <td>Como cajero, quiero buscar productos y agregar/editar/retirar ítems con cantidades válidas sin impactar el stock aún.</td>
      <td>
        <strong>Escenario 01: Agregar ítem</strong><br>
        <strong>Dado</strong> un borrador activo,<br>
        <strong>Cuando</strong> agrego un producto con cantidad &gt; 0,<br>
        <strong>Entonces</strong> el ítem se añade/actualiza (agrupado por producto/lote) y se recalculan subtotales.<br><br>
        <strong>Escenario 02: Editar cantidad</strong><br>
        <strong>Dado</strong> un ítem en el borrador,<br>
        <strong>Cuando</strong> cambio la cantidad a un valor válido (&gt; 0),<br>
        <strong>Entonces</strong> el sistema actualiza el ítem y muestra el nuevo subtotal.<br><br>
        <strong>Escenario 03: Retirar ítem</strong><br>
        <strong>Dado</strong> un ítem en el borrador,<br>
        <strong>Cuando</strong> lo retiro,<br>
        <strong>Entonces</strong> el ítem desaparece del borrador y se recalculan totales.
      </td>
      <td>EP-04</td>
    </tr>
    <tr>
      <td>US03</td>
      <td>Calcular total y utilidad de la salida</td>
      <td>Como dueño, quiero que el sistema calcule en tiempo real el total y la utilidad por ítem/kit y global, usando el costo vigente.</td>
      <td>
        <strong>Escenario 01: Utilidad por ítem</strong><br>
        <strong>Dado</strong> un ítem con precio y costo vigente,<br>
        <strong>Cuando</strong> se recalcula el total,<br>
        <strong>Entonces</strong> se registra <em>utilidad_item = (precio - costo) × cantidad</em> y margen %.<br><br>
        <strong>Escenario 02: Utilidad de la salida</strong><br>
        <strong>Dado</strong> varios ítems (y/o kits),<br>
        <strong>Cuando</strong> se recalcula el total,<br>
        <strong>Entonces</strong> el sistema calcula <em>utilidad_total = Σ utilidad_item</em> y la muestra en el encabezado.<br><br>
        <strong>Escenario 03: Política de costo</strong><br>
        <strong>Dado</strong> una política de costo (p. ej., promedio ponderado o por lote),<br>
        <strong>Cuando</strong> se obtiene el costo,<br>
        <strong>Entonces</strong> el cálculo usa la política activa y deja traza de cuál costo se aplicó.
      </td>
      <td>EP-04</td>
    </tr>
    <tr>
      <td>US04</td>
      <td>Confirmar salida y descontar inventario</td>
      <td>Como cajero, quiero confirmar la salida para registrar los movimientos de inventario (productos y componentes de kits) y actualizar el on-hand.</td>
      <td>
        <strong>Escenario 01: Confirmación exitosa</strong><br>
        <strong>Dado</strong> un borrador válido,<br>
        <strong>Cuando</strong> confirmo la salida,<br>
        <strong>Entonces</strong> el sistema crea movimientos por ítem (y por componente de kit), decrementa <em>on-hand</em>, guarda <em>saldo_post</em> y cambia el estado a <em>Confirmed</em>.<br><br>
        <strong>Escenario 02: Bloqueo por stock insuficiente</strong><br>
        <strong>Dado</strong> que hay ítems/componentes sin stock suficiente y el stock negativo está desactivado,<br>
        <strong>Cuando</strong> intento confirmar,<br>
        <strong>Entonces</strong> el sistema bloquea la acción y lista los faltantes.<br><br>
        <strong>Escenario 03: Disparo de alertas</strong><br>
        <strong>Dado</strong> que se confirma la salida,<br>
        <strong>Cuando</strong> algún producto queda por debajo del umbral,<br>
        <strong>Entonces</strong> el sistema genera la alerta de bajo stock (y la deja disponible para notificación externa).
      </td>
      <td>EP-04</td>
   </tr> 
   <tr>
      <td>US05</td>
      <td>Reporte de stock a fecha (valorizado)</td>
      <td>
        Como gerente, quiero emitir un reporte de stock a una fecha de corte, con cantidades on-hand, costo vigente y valorizado por producto/lote.
      </td>
      <td>
        <strong>Escenario 01: Corte por fecha</strong><br>
        <strong>Dado</strong> una fecha de corte seleccionada,<br>
        <strong>Cuando</strong> genero el reporte,<br>
        <strong>Entonces</strong> se muestran columnas: producto, lote (si aplica), UM, on_hand, costo_vigente, <em>valorizado = on_hand × costo_vigente</em>.<br><br>
        <strong>Escenario 02: Filtros</strong><br>
        <strong>Dado</strong> filtros por categoría, producto y con/sin lotes,<br>
        <strong>Cuando</strong> aplico los filtros,<br>
        <strong>Entonces</strong> el reporte refleja solo los ítems coincidentes.<br><br>
        <strong>Escenario 03: Export</strong><br>
        <strong>Dado</strong> un reporte en pantalla,<br>
        <strong>Cuando</strong> elijo “Exportar”,<br>
        <strong>Entonces</strong> puedo descargar CSV y PDF con el mismo contenido y metadatos (fecha de corte, filtros).
      </td>
      <td>EP-07</td>
    </tr>
    <tr>
      <td>US06</td>
      <td>Reporte de rotación y ventas (utilidad)</td>
      <td>
        Como gerente, quiero un reporte por periodo con unidades vendidas, ingreso, costo y utilidad por producto/categoría, para identificar top/slow movers.
      </td>
      <td>
        <strong>Escenario 01: Cálculo por periodo</strong><br>
        <strong>Dado</strong> un rango de fechas,<br>
        <strong>Cuando</strong> genero el reporte,<br>
        <strong>Entonces</strong> se calculan por producto: unidades_vendidas, <em>ingreso = Σ (precio × cantidad)</em>, <em>costo = Σ (costo_aplicado × cantidad)</em>, <em>utilidad = ingreso − costo</em>, margen% = utilidad/ingreso.<br><br>
        <strong>Escenario 02: Orden y agrupación</strong><br>
        <strong>Dado</strong> opciones de ordenar por unidades/ingreso/utilidad,<br>
        <strong>Cuando</strong> selecciono el criterio,<br>
        <strong>Entonces</strong> el listado se ordena y permite agrupar por categoría.<br><br>
        <strong>Escenario 03: Kits</strong><br>
        <strong>Dado</strong> ventas con kits,<br>
        <strong>Cuando</strong> genero el reporte,<br>
        <strong>Entonces</strong> puedo ver el kit como línea y (opcional) desglosar a componentes; la utilidad considera la suma de costos de componentes.<br><br>
        <strong>Escenario 04: Export</strong><br>
        <strong>Dado</strong> el reporte en pantalla,<br>
        <strong>Cuando</strong> exporto,<br>
        <strong>Entonces</strong> obtengo CSV/PDF con encabezado de parámetros (rango, agrupación).
      </td>
      <td>EP-07</td>
    </tr>
    <tr>
      <td>US07</td>
      <td>Reporte de mermas y ajustes</td>
      <td>
        Como dueño, quiero un reporte de ajustes (±) y mermas por periodo, con motivo, usuario y valorizado, para auditar pérdidas.
      </td>
      <td>
        <strong>Escenario 01: Detalle de movimientos</strong><br>
        <strong>Dado</strong> un rango de fechas,<br>
        <strong>Cuando</strong> genero el reporte,<br>
        <strong>Entonces</strong> se listan: fecha, producto/lote, cantidad (±), motivo, usuario, <em>valor = |cantidad| × costo_aplicado</em>.<br><br>
        <strong>Escenario 02: Totales</strong><br>
        <strong>Dado</strong> el reporte en pantalla,<br>
        <strong>Cuando</strong> visualizo el resumen,<br>
        <strong>Entonces</strong> veo totales por motivo (merma, corrección, conteo) y total general valorizado.<br><br>
        <strong>Escenario 03: Evidencia</strong><br>
        <strong>Dado</strong> ajustes con evidencia (nota/foto),<br>
        <strong>Cuando</strong> consulto el detalle,<br>
        <strong>Entonces</strong> puedo abrir el enlace/adjunto de la evidencia.<br><br>
        <strong>Escenario 04: Export</strong><br>
        <strong>Dado</strong> el reporte,<br>
        <strong>Cuando</strong> exporto,<br>
        <strong>Entonces</strong> descargo CSV/PDF con detalle y totales.
      </td>
      <td>EP-07</td>
    </tr>
    <tr>
      <td>US08</td>
      <td>Reporte de bajo stock y próximos a vencer</td>
      <td>
        Como jefe de compras, quiero un listado de productos bajo umbral y lotes próximos a vencer, con días de cobertura y acciones sugeridas.
      </td>
      <td>
        <strong>Escenario 01: Bajo stock</strong><br>
        <strong>Dado</strong> los umbrales por producto,<br>
        <strong>Cuando</strong> genero el reporte,<br>
        <strong>Entonces</strong> se listan productos con on_hand &lt; umbral y se calcula <em>días_cobertura = on_hand / consumo_promedio_diario</em> (si hay historial).<br><br>
        <strong>Escenario 02: Próximos a vencer</strong><br>
        <strong>Dado</strong> una ventana de X días,<br>
        <strong>Cuando</strong> genero el reporte,<br>
        <strong>Entonces</strong> se listan lotes con vencimiento dentro de la ventana con cantidad y fecha.<br><br>
        <strong>Escenario 03: Acciones</strong><br>
        <strong>Dado</strong> el reporte en pantalla,<br>
        <strong>Cuando</strong> selecciono un ítem,<br>
        <strong>Entonces</strong> puedo abrir atajos a “Registrar ingreso”, “Iniciar salida” o “Ajuste/merma” (según corresponda).<br><br>
        <strong>Escenario 04: Export</strong><br>
        <strong>Dado</strong> el reporte,<br>
        <strong>Cuando</strong> exporto,<br>
        <strong>Entonces</strong> descargo CSV/PDF (y opcional envío a Google Sheets).
      </td>
      <td>EP-07</td>
    </tr>
    <tr>
      <td>US09</td>
      <td>Filtrado de métricas</td>
      <td>Como usuario, quiero filtrar las métricas del dashboard por rango de fechas y categorías de productos, para analizar información más específica y relevante.</td>
      <td>
        <strong>Escenario 01: Filtrar por rango de fechas</strong><br>
        <strong>Dado</strong> que el usuario está en el dashboard,<br>
        <strong>Cuando</strong> selecciona un rango de fechas específico,<br>
        <strong>Entonces</strong> las métricas y gráficos se actualizan mostrando solo la información de ese periodo.<br><br>
        <strong>Escenario 02: Filtrar por categoría de producto</strong><br>
        <strong>Dado</strong> que el usuario está en el dashboard,<em>Draft</em>,<br>
        <strong>Cuando</strong> selecciona una categoría de productos,<br>
        <strong>Entonces</strong> el dashboard muestra únicamente métricas relacionadas con esa categoría.
      </td>
      <td>EP-03</td>
    </tr>
    <tr>
      <td>US10</td>
      <td>Exportación de métricas</td>
      <td>Como usuario, quiero exportar los datos del dashboard, para compartirlos fácilmente con mi equipo o realizar reportes externos.</td>
      <td>
        <strong>Escenario 01: Exportar en formato PDF</strong><br>
        <strong>Dado</strong> que el usuario está en el dashboard,<br>
        <strong>Cuando</strong> hace clic en el botón de exportar y selecciona PDF,<br>
        <strong>Entonces</strong> el sistema genera y descarga un archivo PDF con las métricas actuales aplicando los filtros seleccionados.<br><br>
        <strong>Escenario 02: Exportar en formato Excel</strong><br>
        <strong>Dado</strong> que el usuario está en el dashboard,<em>Draft</em>,<br>
        <strong>Cuando</strong> hace clic en el botón de exportar y selecciona Excel,<br>
        <strong>Entonces</strong> el sistema genera y descarga un archivo Excel con los datos de métricas actuales aplicando los filtros seleccionados.
      </td>
      <td>EP-03</td>
    </tr>
    <tr>
      <td>US11</td>
      <td>Notificaciones en el dashboard</td>
      <td>Como usuario, quiero visualizar en el dashboard notificaciones destacadas de bajo stock y próximos vencimientos, para priorizar las acciones más urgentes.</td>
      <td>
        <strong>Escenario 01: Mostrar notificaciones de bajo stock</strong><br>
        <strong>Dado</strong> que el usuario accede al dashboard, <br>
        <strong>Cuando</strong> hay productos con stock menor al umbral definido,<br>
        <strong>Entonces</strong> el sistema muestra una notificación resaltada en la sección de alertas del dashboard.<br><br>
        <strong>Escenario 02: Mostrar notificaciones de próximos vencimientos</strong><br>
        <strong>Dado</strong> que el usuario accede al dashboard, <em>Draft</em>,<br>
        <strong>Cuando</strong> existen productos que vencen en los próximos 30 días,<br>
        <strong>Entonces</strong> el sistema muestra una notificación resaltada indicando los productos en riesgo de vencimiento.
      </td>
      <td>EP-01</td>
    </tr>
 <tr>
      <td>US12</td>
      <td>Crear producto en catálogo</td>
      <td>Como jefe de compras quiero registrar un nuevo producto para asegurar una gestion productos consistente</td>
      <td>
        <strong>Escenario 01: Registro exitoso</strong><br>
        <strong>Dado</strong> que ingreso un producto con todos los campos obligatorios,<br>
        <strong>Cuando</strong> confirmo el registro,<br>
        <strong>Entonces</strong> el sistema guarda el producto y lo hace disponible en el catálogo.<br><br>
        <strong>Escenario 02: Producto duplicado</strong><br>
        <strong>Dado</strong>que ya existe un producto con el mismo nombre y categoría, <em>Draft</em>,<br>
        <strong>Cuando</strong> intento registrarlo,<br>
        <strong>Entonces</strong> el sistema bloquea el registro y muestra un mensaje de duplicado.
      </td>
      <td>EP-03</td>
    </tr>
    <tr>
      <td>US13</td>
      <td>Edición de producto</td>
      <td>Como jefe de compras quiero editar los datos de un producto existente para mantener actualizada la información en el catálogo</td>
      <td>
        <strong>Escenario 01: Edición exitosa</strong><br>
        <strong>Dado</strong> que selecciono un producto existente,<br>
        <strong>Cuando</strong> edito sus datos válidos,<br>
        <strong>Entonces</strong> el sistema actualiza la información inmediatamente.<br><br>
        <strong>Escenario 02: Campo bloqueado</strong><br>
        <strong>Dado</strong> que intento modificar el identificador único,<br>
        <strong>Cuando</strong> guardo los cambios,<br>
        <strong>Entonces</strong> el sistema rechaza la acción y mantiene el valor original.<br><br>
      </td>
      <td>EP-01</td>
    </tr>
    <tr>
      <td>US14</td>
      <td>Eliminación e inhabilitacion de productos</td>
      <td>Como jefe de compras quiero poder desactivar o eliminar un producto para mantener un control y no saturar el sistema</td>
      <td>
        <strong>Escenario 01: Desactivación exitosa</strong><br>
        <strong>Dado</strong> que selecciono un producto activo,<br>
        <strong>Cuando</strong> ejecuto la acción de desactivar,<br>
        <strong>Entonces</strong> el sistema cambia el estado a inactivo y lo oculta de búsquedas activas.<br><br>
        <strong>Escenario 02: Consulta histórica</strong><br>
        <strong>Dado</strong> que un producto está inactivo,<br>
        <strong>Cuando</strong> consulto un historial o reporte,<br>
        <strong>Entonces</strong> el producto sigue apareciendo con sus registros asociados.<br><br>
      <td>EP-01</td>
    </tr>
    <tr>
      <td>US15</td>
      <td>Clasificación de productos por categoría</td>
      <td>Como jefe de compras quiero asignar categorías a los productos para organizar el catálogo y facilitar búsquedas</td>
      <td>
        <strong>Escenario 01: Clasificación válida</strong><br>
        <strong>Dado</strong> que existe un catálogo de categorías,<br>
        <strong>Cuando</strong> asigno una categoría a un producto,<br>
        <strong>Entonces</strong> el producto queda organizado bajo esa categoría.<br><br>
        <strong>Escenario 02: Filtrado por categoría</strong><br>
        <strong>Dado</strong> que existen varios productos en distintas categorías,<br>
        <strong>Cuando</strong> aplico un filtro por categoría,<br>
        <strong>Entonces</strong> el sistema muestra solo los productos correspondientes.<br><br>
      </td>
      <td>EP-01</td>
    </tr>
    <tr>
      <td>US16</td>
      <td>Búsqueda y filtrado de productos</td>
      <td>Como jefe de compras quiero buscar y filtrar productos por nombre, categoría o estado para acceder rápidamente a la información</td>
      <td>
        <strong>Escenario 01: Búsqueda parcial</strong><br>
        <strong>Dado</strong> que existen productos registrados,<br>
        <strong>Cuando</strong> busco por coincidencias parciales de nombre,<br>
        <strong>Entonces</strong> el sistema lista los resultados correctos.<br><br>
        <strong>Escenario 02: Búsqueda combinada</strong><br>
        <strong>Dado</strong> que aplico filtros por categoría y estado,<br>
        <strong>Cuando</strong> ejecuto la búsqueda,<br>
        <strong>Entonces</strong> el sistema muestra los productos que cumplen todas las condiciones.<br><br>
      </td>
      <td>EP-01</td>
    </tr>
    <tr>
      <td>US17</td>
      <td>Historial de cambios de producto</td>
      <td>Como jefe de compras quiero consultar el historial de cambios de cada producto para corroborar precios y poder planificar estrategicamente</td>
      <td>
        <strong>Escenario 01: Registro de cambios</strong><br>
        <strong>Dado</strong> que un usuario edita un producto,<br>
        <strong>Cuando</strong> se confirma el cambio,<br>
        <strong>Entonces</strong> el sistema genera un registro con usuario, fecha y detalle.<br><br>
        <strong>Escenario 02: Consulta de historial</strong><br>
        <strong>Dado</strong> que accedo al detalle de un producto,<br>
        <strong>Cuando</strong> selecciono la opción de historial,<br>
        <strong>Entonces</strong> el sistema muestra la lista completa de modificaciones.<br><br>
      </td>
      <td>EP-01</td>
    </tr>
    <tr>
      <td>US18</td>
      <td>Sección de funcionalidades</td>
      <td>Como visitante quiero visualizar las principales funcionalidades de stocktrack en la landing para conocer qué ofrece la plataforma</td>
      <td>
        <strong>Escenario 01: Visualización clara</strong><br>
        <strong>Dado</strong> que navego en la landing,<br>
        <strong>Cuando</strong> hago scroll hasta la sección de funcionalidades,<br>
        <strong>Entonces</strong> se muestran al menos 4 funcionalidades clave con iconos y descripciones.<br><br>
        <strong>Escenario 02: Enlace de más información</strong><br>
        <strong>Dado</strong> que visualizo una funcionalidad,<em>Draft</em>,<br>
        <strong>Cuando</strong> hago clic en “ver más”,<br>
        <strong>Entonces</strong> el sistema me dirige a una página con detalles ampliados.<br><br>
      </td>
      <td>EP-09 </td>
    </tr>
    <tr>
      <td>US19</td>
      <td>Formulario de registro</td>
      <td>Como visitante quiero acceder a un formulario de registro en la landing para crear una cuenta rápidamente</td>
      <td>
        <strong>Escenario 01: Registro básico</strong><br>
        <strong>Dado</strong> que accedo al formulario de registro,<br>
        <strong>Cuando</strong> completo los campos obligatorios y envío,<br>
        <strong>Entonces</strong> el sistema crea mi cuenta y me redirige al panel de bienvenida.<br><br>
        <strong>Escenario 02: Validación de datos</strong><br>
        <strong>Dado</strong> que ingreso datos incompletos o inválidos,<br>
        <strong>Cuando</strong> intento registrar,<br>
        <strong>Entonces</strong> el sistema muestra mensajes de error específicos por campo.<br><br>
      </td>
      <td>EP-09</td>
    </tr>
    <tr>
      <td>US20</td>
      <td>Formulario de contacto</td>
      <td>Como visitante quiero llenar un formulario de contacto en la landing para solicitar información adicional sobre stocktrack</td>
      <td>
        <strong>Escenario 01: Envío exitoso</strong><br>
        <strong>Dado</strong> que ingreso mis datos y consulta en el formulario,<br>
        <strong>Cuando</strong> hago clic en enviar,<br>
        <strong>Entonces</strong> el sistema guarda la solicitud y muestra un mensaje de confirmación.<br><br>
        <strong>Escenario 02: Validación de campos</strong><br>
        <strong>Dado</strong> que ingreso un email no válido,<br>
        <strong>Cuando</strong> intento enviar,<br>
        <strong>Entonces</strong> el sistema bloquea la acción y muestra el error.<br><br>
      <td>EP-09</td>
    </tr>
    <tr>
      <td>US21</td>
      <td>Diseño responsive</td>
      <td>Como visitante quiero que la landing sea responsive para navegar de manera cómoda desde cualquier dispositivo</td>
      <td>
        <strong>Escenario 01: Adaptación en móvil</strong><br>
        <strong>Dado</strong> que accedo desde un celular,<br>
        <strong>Cuando</strong> cargo la landing,<br>
        <strong>Entonces</strong> todos los elementos se adaptan al ancho de pantalla.<br><br>
        <strong>Escenario 02: Adaptación en tablet</strong><br>
        <strong>Dado</strong> que accedo desde una tablet,<br>
        <strong>Cuando</strong> cargo la landing,<br>
        <strong>Entonces</strong> las secciones mantienen legibilidad y proporciones correctas.<br><br>
      </td>
      <td>EP-09</td>
    </tr>  
    <tr>
      <td>US22</td>
      <td>Sección de testimonios</td>
      <td>Como visitante quiero ver testimonios de otros usuarios en la landing para confiar más en la plataforma</td>
      <td>
        <strong>Escenario 01: Visualización de testimonios</strong><br>
        <strong>Dado</strong> que llego a la sección de testimonios,<br>
        <strong>Cuando</strong> la página carga,<br>
        <strong>Entonces</strong> se muestran al menos 3 testimonios con nombre, foto y comentario.<br><br>
        <strong>Escenario 02: Rotación automática</strong><br>
        <strong>Dado</strong> que estoy en la sección de testimonios,<br>
        <strong>Cuando</strong> pasan 5 segundos,<br>
        <strong>Entonces</strong> el sistema muestra automáticamente el siguiente testimonio.<br><br>
      </td>
      <td>EP-09</td>
    </tr>
    <tr>
      <td>US23</td>
      <td>Botones claros</td>
      <td>Como visitante quiero ver botones claros y visibles para que sea intuitivo durante la navegación</td>
      <td>
        <strong>Escenario 01: Botnes visibles</strong><br>
        <strong>Dado</strong> que navego en la landing,<br>
        <strong>Cuando</strong> la página carga,<br>
        <strong>Entonces</strong> encontrar botones visibles sin necesidad de buscar.<br><br>
        <strong>Escenario 02: Redirección correcta</strong><br>
        <strong>Dado</strong> que hago clic en el boton,<br>
        <strong>Cuando</strong> lo presiono,<br>
        <strong>Entonces</strong> el sistema me lleva directamente al formulario correcto.<br><br>
      </td>
      <td>EP-09</td>
    </tr>
    <tr>
      <td>US24</td>
      <td>Crear proveedor</td>
      <td>Como jefe de compras, quiero registrar nuevos proveedores con su información clave (nombre, contacto, RUC) para centralizar los datos de mis abastecedores.</td>
      <td>
        <strong>Escenario 01: Creación exitosa</strong><br>
        <strong>Dado</strong> que ingreso los datos obligatorios de un nuevo proveedor,<br>
        <strong>Cuando</strong> guardo el formulario,<br>
        <strong>Entonces</strong> el proveedor se crea y aparece en el listado general.<br><br>
        <strong>Escenario 02: Validación de duplicados</strong><br>
        <strong>Dado</strong> que ya existe un proveedor con el mismo RUC,<br>
        <strong>Cuando</strong> intento guardar el nuevo proveedor,<br>
        <strong>Entonces</strong> el sistema muestra un error de duplicidad y no permite el registro.
      </td>
      <td>EP-10</td>
    </tr>
    <tr>
      <td>US25</td>
      <td>Consultar y editar proveedores</td>
      <td>Como encargado, quiero poder ver la lista de proveedores, buscar uno específico y editar su información para mantener los datos actualizados.</td>
      <td>
        <strong>Escenario 01: Edición exitosa</strong><br>
        <strong>Dado</strong> que abro la ficha de un proveedor existente,<br>
        <strong>Cuando</strong> modifico su número de teléfono y guardo,<br>
        <strong>Entonces</strong> la información se actualiza correctamente.<br><br>
        <strong>Escenario 02: Búsqueda por nombre</strong><br>
        <strong>Dado</strong> que estoy en la lista de proveedores,<br>
        <strong>Cuando</strong> escribo parte del nombre en la barra de búsqueda,<br>
        <strong>Entonces</strong> la lista se filtra en tiempo real mostrando solo las coincidencias.
      </td>
      <td>EP-10</td>
    </tr>
    <tr>
      <td>US26</td>
      <td>Asociar productos a proveedor</td>
      <td>Como jefe de compras, quiero asociar productos a un proveedor para saber a quién comprar cada artículo y facilitar los reportes.</td>
      <td>
        <strong>Escenario 01: Asociar producto</strong><br>
        <strong>Dado</strong> que estoy en la ficha de un proveedor,<br>
        <strong>Cuando</strong> selecciono la opción "Asociar producto" y elijo un ítem del catálogo,<br>
        <strong>Entonces</strong> el producto queda vinculado al proveedor.<br><br>
        <strong>Escenario 02: Visualizar productos del proveedor</strong><br>
        <strong>Dado</strong> un proveedor con productos asociados,<br>
        <strong>Cuando</strong> consulto su ficha,<br>
        <strong>Entonces</strong> puedo ver una lista de todos los productos que este me suministra.
      </td>
      <td>EP-10</td>
    </tr>
    <tr>
      <td>US27</td>
      <td>Visualizar KPIs principales</td>
      <td>Como dueño, quiero ver en el dashboard tarjetas con KPIs clave (valor de inventario, productos con stock bajo) para un resumen rápido del negocio.</td>
      <td>
        <strong>Escenario 01: KPI de Valor de Inventario</strong><br>
        <strong>Dado</strong> que he iniciado sesión,<br>
        <strong>Cuando</strong> cargo el dashboard,<br>
        <strong>Entonces</strong> veo una tarjeta que muestra el valor total de mi inventario (stock x costo).<br><br>
        <strong>Escenario 02: KPI de Stock Bajo</strong><br>
        <strong>Dado</strong> que he iniciado sesión,<br>
        <strong>Cuando</strong> cargo el dashboard,<br>
        <strong>Entonces</strong> veo una tarjeta que muestra el número total de productos cuyo stock está por debajo del umbral mínimo.
      </td>
      <td>EP-03</td>
    </tr>
    <tr>
    <td>US28</td>
    <td>Ver alertas críticas</td>
    <td>Como encargado, quiero que el dashboard me muestre una lista de alertas urgentes (lotes próximos a vencer) para tomar acciones preventivas.</td>
    <td>
      <strong>Escenario 01: Mostrar lotes por vencer</strong><br>
      <strong>Dado</strong> que existen lotes cuya fecha de vencimiento es en los próximos 7 días,<br>
      <strong>Cuando</strong> cargo el dashboard,<br>
      <strong>Entonces</strong> veo una sección de alertas con la lista de dichos lotes.<br><br>
      <strong>Escenario 02: Navegación desde alerta</strong><br>
      <strong>Dado</strong> que veo una alerta de un lote por vencer,<br>
      <strong>Cuando</strong> hago clic en la alerta,<br>
      <strong>Entonces</strong> el sistema me redirige a la ficha del producto correspondiente para gestionarlo.
    </td>
    <td>EP-03</td>
    </tr>
    <tr>
      <td>US29</td>
      <td>Definir composición de un kit</td>
      <td>Como encargado, quiero crear la "receta" de un kit, asociando productos existentes y sus cantidades, para estandarizar el contenido de los paquetes.</td>
      <td>
        <strong>Escenario 01: Creación de la definición</strong><br>
        <strong>Dado</strong> que estoy en la sección de Kits,<br>
        <strong>Cuando</strong> creo un nuevo kit, le asigno un nombre y agrego 3 productos componentes con sus respectivas cantidades,<br>
        <strong>Entonces</strong> el sistema guarda la definición (receta) del kit.<br><br>
        <strong>Escenario 02: Edición de componentes</strong><br>
        <strong>Dado</strong> que un kit ya está definido,<br>
        <strong>Cuando</strong> edito el kit para cambiar la cantidad de un componente,<br>
        <strong>Entonces</strong> la receta del kit se actualiza para futuros ensamblajes.
      </td>
    <td>EP-05</td>
    </tr>
    <tr>
    <td>US30</td>
    <td>Ensamblar kits y ajustar stock</td>
    <td>Como encargado de bodega, quiero registrar el "ensamblaje" de kits para que el sistema descuente el stock de los componentes y aumente el stock del kit como producto final.</td>
    <td>
      <strong>Escenario 01: Ensamblaje exitoso</strong><br>
      <strong>Dado</strong> que tengo stock suficiente de todos los componentes de un kit,<br>
      <strong>Cuando</strong> registro el ensamblaje de 5 kits,<br>
      <strong>Entonces</strong> el sistema reduce el stock de los componentes y aumenta en 5 el stock del producto kit.<br><br>
      <strong>Escenario 02: Bloqueo por falta de stock</strong><br>
      <strong>Dado</strong> que no tengo stock suficiente de uno de los componentes,<br>
      <strong>Cuando</strong> intento registrar el ensamblaje de un kit,<br>
      <strong>Entonces</strong> el sistema bloquea la acción y me informa qué componente falta.
    </td>
    <td>EP-05</td>
    </tr>
    <tr>
      <td>US31</td>
      <td>Configurar umbrales de stock</td>
      <td>Como jefe de compras, quiero definir umbrales mínimos de stock por producto para que el sistema pueda generar alertas automáticas.</td>
      <td>
        <strong>Escenario 01: Registro de umbral</strong><br>
        <strong>Dado</strong> un producto sin umbral,<br>
        <strong>Cuando</strong> registro un valor mínimo,&nbsp;<br>
        <strong>Entonces</strong> el sistema guarda la configuración asociada al producto.<br><br> <strong>Escenario 02: Edición</strong><br>
        <strong>Dado</strong> un umbral ya configurado,<br>
        <strong>Cuando</strong> lo edito y guardo,<br>
        <strong>Entonces</strong> el sistema actualiza el valor y registra la fecha de modificación.
      </td>
        <td>EP-06</td> 
    </tr>
    <tr>
      <td>US32</td>
      <td>Generar alerta de bajo stock</td>
      <td>Como sistema, quiero generar una alerta cuando el stock de un producto caiga por debajo del umbral configurado.</td>
      <td>
        <strong>Escenario 01: Umbral superado</strong><br>
        <strong>Dado</strong> que un producto tiene stock menor al umbral,<br>
        <strong>Cuando</strong> se registra un movimiento de salida,<br>
        <strong>Entonces</strong> el sistema crea una alerta de tipo “Bajo stock” con fecha y cantidad disponible <br><br>
        <strong>Escenario 02: No aplica</strong><br>
        <strong>Dado</strong> un producto sin umbral definido,<br>
        <strong>Cuando</strong> se procesa la salida,<br>
        <strong>Entonces</strong> no se genera alerta.
      </td>
      <td>EP-06</td>
    </tr>
    <tr>
      <td>US33</td>
      <td>Generar alerta de vencimiento</td>
      <td>Como sistema, quiero generar una alerta cuando un lote esté próximo a vencer dentro de la ventana configurada.</td>
      <td>
        <strong>Escenario 01: Próximo vencimiento</strong><br>
        <strong>Dado</strong> un lote con fecha de vencimiento a menos de X días,<br>
        <strong>Cuando</strong> se actualiza el inventario,<br>
        <strong>Entonces</strong> el sistema crea una alerta “Próximo a vencer” con lote, cantidad y fecha.<br><br>
        <strong>Escenario 02: Fuera de ventana</strong><br>
        <strong>Dado</strong> un lote con vencimiento mayor al rango configurado,<br>
        <strong>Cuando</strong> se valida el inventario,<br>
        <strong>Entonces</strong> no se genera alerta. 
      </td>
      <td>EP-06</td> 
    </tr>
    <tr>
      <td>US34</td>
      <td>Listar alertas pendientes</td>
      <td>Como usuario, quiero ver un listado de todas las alertas activas (bajo stock, próximos a vencer, vencidos) para tomar decisiones.</td>
      <td> 
        <strong>Escenario 01: Listado</strong><br>
        <strong>Dado</strong> que existen alertas activas,<br>
        <strong>Cuando</strong> ingreso al módulo de alertas,<br>
        <strong>Entonces</strong> el sistema muestra tabla con tipo, producto/lote, fecha y estado.<br><br>
        <strong>Escenario 02: Sin alertas</strong><br>
        <strong>Dado</strong> que no existen alertas activas,<br>
        <strong>Cuando</strong> consulto el listado,<br>
        <strong>Entonces</strong> el sistema muestra mensaje “No hay alertas pendientes”.
      </td>
      <td>EP-06</td> 
    </tr> 
    <tr>
      <td>US35</td>
      <td>Notificación externa de alertas</td>
      <td>Como usuario, quiero recibir notificaciones por correo o push cuando se generen alertas críticas.</td> <td>
        <strong>Escenario 01: Envío de correo</strong><br>
        <strong>Dado</strong> una alerta de tipo “Bajo stock crítico”,<br>
        <strong>Cuando</strong> se genera,<br>
        <strong>Entonces</strong> el sistema envía correo al jefe de compras con detalle.<br><br>
        <strong>Escenario 02: Notificación push</strong><br>
        <strong>Dado</strong> que el usuario tiene app móvil habilitada,<br>
        <strong>Cuando</strong> ocurre la alerta,<br>
        <strong>Entonces</strong> recibe notificación push con resumen y enlace al sistema.
      </td>
      <td>EP-06</td>
    </tr>
    <tr>
      <td>US36</td>
      <td>Gestionar estado de alertas</td>
      <td>Como jefe de compras, quiero marcar las alertas como atendidas o descartadas para mantener control del seguimiento.</td>
      <td>
        <strong>Escenario 01: Marcar como atendida</strong><br>
        <strong>Dado</strong> una alerta activa,<br>
        <strong>Cuando</strong> la marco como atendida,<br>
        <strong>Entonces</strong> el sistema cambia el estado y registra usuario/fecha.<br><br>
        <strong>Escenario 02: Descartar</strong><br>
        <strong>Dado</strong> una alerta no aplicable,<br>
        <strong>Cuando</strong> la descarto,<br>
        <strong>Entonces</strong> el sistema la archiva sin afectar inventario.
      </td>
      <td>EP-06</td> 
    </tr>
    <tr>
      <td>US37</td>
      <td>Iniciar borrador de ingreso</td>
      <td>Como asistente de almacén, quiero iniciar un borrador de ingreso para registrar productos recibidos antes de confirmarlos.</td>
      <td>
        <strong>Escenario 01: Borrador creado</strong><br>
        <strong>Dado</strong> que estoy en “Nuevo ingreso”,<br>
        <strong>Cuando</strong> selecciono “Iniciar borrador”,<br>
        <strong>Entonces</strong> el sistema crea un borrador con ID único, estado <em>Draft</em> y fecha de inicio.<br><br>
        <strong>Escenario 02: Reanudación</strong><br>
        <strong>Dado</strong> un borrador en estado <em>Draft</em>,<br>
        <strong>Cuando</strong> lo reanudo,<br>
        <strong>Entonces</strong> se muestran ítems y cantidades guardadas.
      </td>
      <td>EP-04</td>
    </tr>
    <tr>
      <td>US38</td>
      <td>Registrar ítems del ingreso</td>
      <td>Como asistente de almacén, quiero agregar productos, lotes y cantidades recibidas al borrador sin impactar aún el stock.</td>
      <td>
        <strong>Escenario 01: Agregar ítem</strong><br>
        <strong>Dado</strong> un borrador activo,<br>
        <strong>Cuando</strong> agrego un producto con lote y cantidad válida,&nbsp;<br>
        <strong>Entonces</strong> el sistema registra el ítem en el borrador.<br><br>
        <strong>Escenario 02: Editar cantidad</strong><br>
        <strong>Dado</strong> un ítem en el borrador,<br>
        <strong>Cuando</strong> cambio la cantidad,<br>
        <strong>Entonces</strong> se actualiza el subtotal.<br><br>
        <strong>Escenario 03: Retirar ítem</strong><br>
        <strong>Dado</strong> un ítem en el borrador,<br>
        <strong>Cuando</strong> lo elimino,<br>
        <strong>Entonces</strong> desaparece y se recalculan totales.
      </td>
      <td>EP-04</td>
    </tr>
    <tr>
      <td>US39</td>
      <td>Registrar costo y proveedor</td>
      <td>Como asistente de almacén, quiero asociar cada ingreso a un costo unitario y proveedor para trazabilidad de compras.</td>
      <td>
        <strong>Escenario 01: Costo y proveedor válidos</strong><br>
        <strong>Dado</strong> un borrador de ingreso,<br>
        <strong>Cuando</strong> ingreso costo y proveedor,<br>
        <strong>Entonces</strong> se guarda la información por producto/lote.<br><br>
        <strong>Escenario 02: Datos incompletos</strong><br>
        <strong>Dado</strong> un ítem sin costo o proveedor,<br>
        <strong>Cuando</strong> intento confirmar,<br>
        <strong>Entonces</strong> el sistema muestra error indicando campos obligatorios.
      </td>
      <td>EP-04</td>
    </tr>
    <tr>
      <td>US40</td>
      <td>Confirmar ingreso y actualizar stock</td>
      <td>Como asistente de almacén, quiero confirmar el ingreso para registrar movimientos positivos y actualizar el on-hand.</td>
      <td>
        <strong>Escenario 01: Confirmación exitosa</strong><br>
        <strong>Dado</strong> un borrador válido,<br>
        <strong>Cuando</strong> confirmo,<br>
        <strong>Entonces</strong> el sistema crea movimientos por ítem, incrementa on-hand y cambia estado a <em>Confirmed</em>.<br><br>
        <strong>Escenario 02: Duplicidad de lote</strong><br>
        <strong>Dado</strong> que ya existe el lote,<br>
        <strong>Cuando</strong> confirmo ingreso,<br>
        <strong>Entonces</strong> el sistema suma cantidades y deja traza de consolidación.
      </td>
      <td>EP-04</td>
    </tr>
    <tr>
      <td>US41</td>
      <td>Adjuntar documento de respaldo</td>
      <td>Como asistente de almacén, quiero adjuntar la factura o guía de remisión al ingreso para evidencia documental.</td>
      <td>
        <strong>Escenario 01: Adjuntar archivo</strong><br>
        <strong>Dado</strong> un borrador,<br>
        <strong>Cuando</strong> subo un PDF o imagen,<br>
        <strong>Entonces</strong> queda vinculado al ingreso y visible en el detalle.<br><br>
        <strong>Escenario 02: Formato inválido</strong><br>
        <strong>Dado</strong> un archivo distinto a PDF/imagen,<br>
        <strong>Cuando</strong> lo subo,<br>
        <strong>Entonces</strong> el sistema rechaza el archivo y muestra mensaje de error.
      </td>
      <td>EP-04</td> 
    </tr>
    <tr>
      <td>US42</td>
      <td>Disparar alertas por ingreso</td>
      <td>Como sistema, quiero recalcular coberturas y eliminar alertas de bajo stock cuando se confirme un ingreso.</td>
      <td>
        <strong>Escenario 01: Recalculo de coberturas</strong><br>
        <strong>Dado</strong> que confirmo un ingreso,<br>
        <strong>Cuando</strong> incrementa el stock de un producto,<br>
        <strong>Entonces</strong> se recalculan días de cobertura y se actualiza estado de alertas previas.<br><br>
        <strong>Escenario 02: Eliminación de alerta</strong><br>
        <strong>Dado</strong> una alerta activa de bajo stock,<br>
        <strong>Cuando</strong> el ingreso hace que on-hand supere el umbral,<br>
        <strong>Entonces</strong> el sistema marca la alerta como resuelta automáticamente.
      </td>
      <td>EP-04</td>
    </tr>
    <tr>
      <td>US43</td>
      <td>Verificar compra de lotes</td>
      <td>Como dueño de bodega, quiero gestionar y verificar la cantidad de los lotes recibidos para tener un mejor control del inventario.</td>
      <td>
        <strong>Escenario 01: Añadir nuevo lote sin registrar</strong><br>
        <strong>Dado</strong> que el dueño de bodega entra a la aplicación<br>
        <strong>Cuando</strong> recibe un nuevo lote de productos no registrados previamente,<br>
        <strong>Entonces</strong> registra el lote recibido con los datos respectivos dentro de la aplicación <br><br>
        <strong>Escenario 02: Añadir lote registrado</strong><br>
        <strong>Dado</strong> que el dueño de bodega entra a la aplicación,<br>
        <strong>Cuando</strong> recibe un nuevo lote de productos registrados previamente,<br>
        <strong>Entonces</strong> añade la cantidad de lotes recibidos registrados previamente.
      </td>
      <td>EP-02</td>
    </tr>
    <tr>
      <td>US44</td>
      <td>Ver fecha de vencimiento de los lotes</td>
      <td>Como asistente de almacén, quiero verificar la fecha de vencimiento de mis productos para estar pendiente de cuando reponerlos.</td>
      <td>
        <strong>Escenario 01: Verificar fecha de vencimiento de los lotes</strong><br>
        <strong>Dado</strong> que el dueño de bodega está dentro de la aplicación y tengo lotes registrados,<br>
        <strong>Cuando</strong> quiere ver la fecha de vencimiento de sus productos <br>
        <strong>Entonces</strong> el sistema muestra la información del lote junto con fecha de vencimiento de los mismos .<br><br>
        <strong>Escenario 02: No hay lotes registrados</strong><br>
        <strong>Dado</strong> que el dueño de bodega está dentro de la aplicación y no tiene lotes registrados,<br>
        <strong>Cuando</strong> quiere ver la fecha de vencimiento de sus productos,<br>
        <strong>Entonces</strong> no se muestra información de los productos y el sistema muestra que se deben registrar lotes primero.<br><br>
      </td>
      <td>EP-02</td>
    </tr>
    <tr>
      <td>US45</td>
      <td>Registrar costo y proveedor</td>
      <td>Como asistente de almacén, quiero asociar cada ingreso a un costo unitario y proveedor para trazabilidad de compras.</td>
      <td>
        <strong>Escenario 01: Costo y proveedor válidos</strong><br>
        <strong>Dado</strong> un borrador de ingreso,<br>
        <strong>Cuando</strong> ingreso costo y proveedor,<br>
        <strong>Entonces</strong> se guarda la información por producto/lote.<br><br>
        <strong>Escenario 02: Datos incompletos</strong><br>
        <strong>Dado</strong> un ítem sin costo o proveedor,<br>
        <strong>Cuando</strong> intento confirmar,<br>
        <strong>Entonces</strong> el sistema muestra error indicando campos obligatorios.
      </td>
      <td>EP-02</td>
    </tr>
    <tr>
      <td>US46</td>
      <td>Alertar vencimiento próximo</td>
      <td>Como dueño de bodega, quiero recibir una alerta cuando un lote esté próximo a vencer para poder tomar decisiones a tiempo.</td>
      <td>
        <strong>Escenario 01: Confirmación exitosa</strong><br>
        <strong>Dado</strong> que hay un lote registrado con fecha de vencimiento en menos de 15 días<br>
        <strong>Cuando</strong> confirmo,<br>
        <strong>Entonces</strong> el sistema muestra una alerta visual indicando producto, lote y fecha próxima a vencer.<br><br>
        <strong>Escenario 02: Sin lotes próximos a vencer</strong><br>
        <strong>Dado</strong> que todos los lotes registrados vencen en más de 15 días,<br>
        <strong>Cuando</strong> ingreso a la aplicación,<br>
        <strong>Entonces</strong> no se muestra ninguna alerta
      </td>
      <td>EP-02</td>
    </tr>
    <tr>
      <td>US47</td>
      <td>Buscar lotes por proveedor</td>
      <td>Como dueño de bodega, quiero filtrar los lotes por proveedor para identificar rápidamente qué productos corresponden a cada socio comercial.</td>
      <td>
        <strong>Escenario 01: Proveedor con lotes registrados</strong><br>
        <strong>Dado</strong> que existen lotes con proveedor “Distribuidora XYZ”,<br>
        <strong>Cuando</strong> filtro por ese proveedor,<br>
        <strong>Entonces</strong> el sistema lista los lotes asociados a él con sus fechas de vencimiento.<br><br>
        <strong>Escenario 02: Proveedor sin lotes registrados</strong><br>
        <strong>Dado</strong> que “Proveedor ABC” no tiene lotes en el sistema,<br>
        <strong>Cuando</strong> aplico el filtro,<br>
        <strong>Entonces</strong> el sistema muestra “No hay lotes asociados a este proveedor”.
      </td>
      <td>EP-02</td>
    </tr>
    <tr>
      <td>US48</td>
      <td>Editar información de un lote</td>
      <td>Como asistente de almacén, quiero poder editar la información de un lote (fecha de vencimiento, cantidad o proveedor) para corregir errores en el registro.</td>
      <td>
        <strong>Escenario 01: Edición exitosa</strong><br>
        <strong>Dado</strong> que un lote está registrado,<br>
        <strong>Cuando</strong> modifico su fecha de vencimiento o cantidad,<br>
        <strong>Entonces</strong> el sistema guarda los cambios y muestra un mensaje de confirmación.<br><br>
        <strong>Escenario 02: Intento de edición con datos inválidos</strong><br>
        <strong>Dado</strong> que ingreso una fecha de vencimiento en el pasado,<br>
        <strong>Cuando</strong> intento guardar,<br>
        <strong>Entonces</strong> el sistema rechaza el cambio y muestra un error.
      </td>
      <td>EP-02</td>
    </tr>
    <tr>
      <td>US49</td>
      <td>Ver historial de movimientos de un lote</td>
      <td>Como dueño de bodega, quiero consultar el historial de movimientos de cada lote para tener trazabilidad de ingresos y salidas.</td>
      <td>
        <strong>Escenario 01: Historial disponible</strong><br>
        <strong>Dado</strong> que un lote tiene registros de ingreso y salida,<br>
        <strong>Cuando</strong> consulto su historial,<br>
        <strong>Entonces</strong> el sistema muestra una lista con fecha, tipo de movimiento, cantidad y usuario que lo realizó.<br><br>
        <strong>Escenario 02: Sin historial</strong><br>
        <strong>Dado</strong> que un lote recién se registró y no tiene movimientos,<br>
        <strong>Cuando</strong> consulto el historial,<br>
        <strong>Entonces</strong> el sistema indica “Este lote no tiene movimientos registrados”.
      </td>
      <td>EP-02</td>
    </tr>
    <tr>
      <td>US50</td>
      <td>Crear usuarios nuevos</td>
      <td>Como dueño de un startup, quiero crear cuentas de usuario para que cada miembro del equipo tenga acceso individual a la plataforma.</td>
      <td>
        <strong>Escenario 01: Creación exitosa</strong><br>
        Dado que estoy en el módulo de usuarios,<br>
        Cuando ingreso nombre, correo y rol,<br>
        Entonces el sistema guarda el nuevo usuario y envía invitación.<br><br>
        <strong>Escenario 02: Datos incompletos</strong><br>
        Dado que no ingresé correo electrónico,<br>
        Cuando intento crear el usuario,<br>
        Entonces el sistema muestra error de campo obligatorio.
      </td>
      <td>EP-08</td>
    </tr>
    <tr>
      <td>US51</td>
      <td>Asignar roles</td>
      <td>Como administrador, quiero asignar un rol a cada usuario para definir qué puede y qué no puede hacer dentro de la aplicación.</td>
      <td>
        <strong>Escenario 01: Rol asignado correctamente</strong><br>
        Dado que un usuario existe,<br>
        Cuando le asigno el rol “Asistente”,<br>
        Entonces el sistema actualiza sus permisos.<br><br>
        <strong>Escenario 02: Usuario sin rol</strong><br>
        Dado que un usuario no tiene rol,<br>
        Cuando intenta ingresar,<br>
        Entonces el sistema muestra “Acceso restringido”.
      </td>
      <td>EP-08</td>
    </tr>
    <tr>
      <td>US52</td>
      <td>Editar permisos personalizados</td>
      <td>Como administrador, quiero ajustar permisos específicos en un usuario para dar accesos excepcionales.</td>
      <td>
        <strong>Escenario 01: Permiso extra</strong><br>
        Dado que un usuario tiene rol “Asistente”,<br>
        Cuando le habilito permiso extra de “Ver reportes”,<br>
        Entonces el usuario puede acceder al módulo.<br><br>
        <strong>Escenario 02: Quitar permisos</strong><br>
        Dado que un usuario tenía acceso a “Crear lotes”,<br>
        Cuando desactivo ese permiso,<br>
        Entonces el sistema bloquea su acceso.
      </td>
      <td>EP-08</td>
    </tr>
    <tr>
      <td>US53</td>
      <td>Bloquear usuarios</td>
      <td>Como administrador, quiero poder desactivar usuarios para evitar accesos no autorizados.</td>
      <td>
        <strong>Escenario 01: Usuario bloqueado</strong><br>
        Dado que un usuario está activo,<br>
        Cuando lo marco como bloqueado,<br>
        Entonces ya no puede iniciar sesión.<br><br>
        <strong>Escenario 02: Intento de ingreso bloqueado</strong><br>
        Dado que un usuario está bloqueado,<br>
        Cuando intenta iniciar sesión,<br>
        Entonces el sistema muestra “Cuenta deshabilitada”.
      </td>
      <td>EP-08</td>
    </tr>
    <tr>
      <td>US54</td>
      <td>Ver lista de usuarios</td>
      <td>Como administrador, quiero ver un listado con todos los usuarios, roles y estado de cuenta para gestionar mejor el equipo.</td>
      <td>
        <strong>Escenario 01: Lista con usuarios</strong><br>
        Dado que hay usuarios registrados,<br>
        Cuando entro al módulo,<br>
        Entonces veo listado con nombre, correo, rol y estado.<br><br>
        <strong>Escenario 02: Sin usuarios</strong><br>
        Dado que no hay usuarios en el sistema,<br>
        Cuando consulto el listado,<br>
        Entonces se muestra “No existen usuarios registrados”.
      </td>
      <td>EP-08</td>
    </tr>
    <tr>
      <td>US55</td>
      <td>Cambiar rol de un usuario</td>
      <td>Como administrador, quiero poder cambiar el rol de un usuario para ajustar sus responsabilidades dentro de la bodega/startup.</td>
      <td>
        <strong>Escenario 01: Cambio exitoso</strong><br>
        Dado que un usuario tiene rol “Asistente”,<br>
        Cuando lo cambio a “Supervisor”,<br>
        Entonces el sistema actualiza sus permisos.<br><br>
        <strong>Escenario 02: Restricción</strong><br>
        Dado que intento degradar al único “Administrador”,<br>
        Cuando confirmo,<br>
        Entonces el sistema impide la acción.
      </td>
      <td>EP-08</td>
    </tr>
    <tr>
      <td>US56</td>
      <td>Auditoría de accesos</td>
      <td>Como administrador, quiero consultar un historial de accesos de los usuarios para detectar intentos fallidos o acciones sospechosas.</td>
      <td>
        <strong>Escenario 01: Accesos exitosos</strong><br>
        Dado que los usuarios ingresaron,<br>
        Cuando consulto el historial,<br>
        Entonces veo fecha, hora, usuario y estado.<br><br>
        <strong>Escenario 02: Intentos fallidos</strong><br>
        Dado que un usuario ingresó mal contraseña 3 veces,<br>
        Cuando reviso,<br>
        Entonces aparece “intento fallido”.
      </td>
      <td>EP-08</td>
    </tr>
    <tr>
      <td>US57</td>
      <td>Roles predefinidos</td>
      <td>Como administrador, quiero contar con roles predefinidos (Administrador, Supervisor, Asistente) para acelerar la configuración inicial.</td>
      <td>
        <strong>Escenario 01: Crear usuario con rol predefinido</strong><br>
        Dado que selecciono “Supervisor”,<br>
        Cuando creo al usuario,<br>
        Entonces el sistema aplica permisos estándar.<br><br>
        <strong>Escenario 02: Personalizar rol</strong><br>
        Dado que un usuario tiene rol “Asistente”,<br>
        Cuando ajusto permisos,<br>
        Entonces el sistema conserva la base del rol y aplica cambios.
      </td>
      <td>EP-08</td>
    </tr>
  </tbody>
</table>

### Epics

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
  <thead>
    <tr>
      <th style="width:10%;">Epic ID</th>
      <th style="width:20%;">Título</th>
      <th style="width:55%;">Descripción</th>
      <th style="width:15%;">HUs asociadas</th>
    </tr>
  </thead>
  <tbody>   
    <tr>
      <td>EP-01</td>
      <td>Catálogo de Productos</td>
      <td>Como jefe de compras, quiero crear y mantener el maestro de productos (nombre, UM, categoría, estado) y configurar umbrales de bajo stock, para asegurar datos consistentes y habilitar alertas útiles.</td>
      <td>US018, US19, US20, US21, US22, US23</td>
    </tr>
    <tr>
      <td>EP-02</td>
      <td>Lotes y Vencimientos</td>
      <td>Como encargado de bodega, quiero gestionar lotes y asignar fechas de vencimiento aplicando políticas como FEFO, para garantizar trazabilidad y reducir mermas por caducidad.</td>
      <td>US43, US44, US45, US46, US47, US48</td>
    </tr>
    <tr>
      <td>EP-03</td>
      <td>Dashboard</td>
      <td>Como usuario, quiero acceder a un panel de control con métricas clave (productos próximos a vencer, stock bajo, rotación, alertas recientes), para tener una visión general y tomar decisiones rápidas..</td>
      <td>US24, US25</td>
    </tr>
    <tr>
      <td>EP-04</td>
      <td>Movimientos de Inventario</td>
      <td>Como cajero, quiero registrar de forma precisa todas las entradas (compras, ajustes) y salidas de productos, para mantener la exactitud del stock en tiempo real y tener una trazabilidad completa de cada movimiento.</td>
      <td>US01, US02, US03, US04, US05, US06, US36, US37, US38, US39, US40, US41</td>
    </tr>
    <tr>
      <td>EP-05</td>
      <td>Kits</td>
      <td>Como usuario del negocio, quiero definir kits (combos) y agregarlos a la venta con desglose automático de componentes, para impactar correctamente el stock y el costo real.</td>
      <td>US26, US27</td>
    </tr>
    <tr>
      <td>EP-06</td>
      <td>Alertas y Notificaciones</td>
      <td>Como dueño o jefe de compras, quiero recibir alertas de bajo stock y próximos a vencer por canales externos simples (email, Telegram/Slack, push), para reponer a tiempo y evitar pérdidas.</td>
      <td>US28, US29, US30, US31, US32, US33</td>
    </tr>
    <tr>
      <td>EP-07</td>
      <td>Reportes Operativos</td>
      <td>Como gerente, quiero emitir reportes de stock a fecha (valorizado), rotación/ventas con utilidad, mermas/ajustes, con exportación a CSV/PDF/Sheets, para tomar decisiones y auditar.</td>
      <td>US05, US06, US07, US08</td>
    </tr>
    <tr>
      <td>EP-08</td>
      <td>Usuarios, Roles y Permisos</td>
      <td>Como dueño, quiero crear usuarios y asignar roles y permisos mínimos (dueño, encargado, cajero/supervisor), para controlar el acceso y resguardar operaciones clave.</td>
      <td>US47, US48, US49, US50, US51, US52, US53, US54</td>
    </tr>
    <tr>
      <td>EP-09</td>
      <td>Landing</td>
      <td>Como visitante, quiero visualizar una landing con propuesta de valor, funcionalidades y registro/contacto, para conocer StockTrack y convertirme en usuario.</td>
      <td>US012, US13, US14, US15, US16, US17</td>
    </tr>
    <tr>
      <td>EP-10</td>
      <td>Proveedores</td>
      <td>Como encargado de compras, quiero registrar, consultar, editar y eliminar proveedores, asociarlos a productos y gestionar datos de contacto, para asegurar un abastecimiento confiable y trazable.</td>
      <td>US21, US22, US23</td>
    </tr>
  </tbody>
</table>

### Technical stories
<!-- Technical Stories – Formato "Como... quiero... para..." + Criterios (Dado/Cuando/Entonces) -->

<table border="1" cellspacing="0" cellpadding="8" style="border-collapse:collapse; width:100%;">
  <thead>
    <tr>
      <th style="width:8%;">Story ID</th>
      <th style="width:18%;">Título</th>
      <th style="width:24%;">Descripción</th>
      <th style="width:40%;">Criterios de Aceptación</th>
      <th style="width:10%;">Relacionado con (Epic ID)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>TS01</td>
      <td>Bloqueo optimista en stock</td>
      <td>Como administrador del sistema, quiero usar control de versión en inventario para evitar sobreventas cuando dos usuarios confirman salidas a la vez.</td>
      <td>
        <strong>Escenario 01: Actualización con versión válida</strong><br>
        <strong>Dado</strong> un registro con versión <em>v</em>,<br>
        <strong>Cuando</strong> confirmo la salida enviando <em>v</em>,<br>
        <strong>Entonces</strong> se descuenta el stock y la versión cambia a <em>v+1</em>.<br><br>
        <strong>Escenario 02: Conflicto de concurrencia</strong><br>
        <strong>Dado</strong> dos confirmaciones sobre el mismo producto/lote,<br>
        <strong>Cuando</strong> la segunda llega con versión desactualizada,<br>
        <strong>Entonces</strong> el sistema responde <em>409 Conflict</em> y pide recargar.<br><br>
        <strong>Escenario 03: Transacción de un solo agregado</strong><br>
        <strong>Dado</strong> una confirmación de salida,<br>
        <strong>Cuando</strong> se persiste,<br>
        <strong>Entonces</strong> todo ocurre en una única transacción del agregado de inventario.
      </td>
      <td>EP-04</td>
    </tr>
    <tr>
      <td>TS02</td>
      <td>Outbox + eventos de dominio</td>
      <td>Como desarrollador, quiero registrar eventos en una Outbox para enviarlos de forma segura a los consumidores y mantener consistencia.</td>
      <td>
        <strong>Escenario 01: Escritura transaccional</strong><br>
        <strong>Dado</strong> una salida/ingreso confirmado,<br>
        <strong>Cuando</strong> se guarda el movimiento,<br>
        <strong>Entonces</strong> se guarda también un evento en Outbox con <em>status=Pending</em>.<br><br>
        <strong>Escenario 02: Despacho resiliente</strong><br>
        <strong>Dado</strong> eventos pendientes,<br>
        <strong>Cuando</strong> corre el despachador,<br>
        <strong>Entonces</strong> publica con reintentos y marca <em>Processed</em>.<br><br>
        <strong>Escenario 03: Idempotencia</strong><br>
        <strong>Dado</strong> que un evento llega duplicado al consumidor,<br>
        <strong>Cuando</strong> intenta procesarlo,<br>
        <strong>Entonces</strong> no duplica efectos (se deduplica por <em>event_id</em>).
      </td>
      <td>EP-04, EP-06, EP-07</td>
    </tr>
    <tr>
      <td>TS03</td>
      <td>Motor de kits (receta y costo)</td>
      <td>Como encargado, quiero que el sistema desglose los kits en componentes al vender o ensamblar para descontar stock y calcular costo correcto.</td>
      <td>
        <strong>Escenario 01: Desglose al confirmar</strong><br>
        <strong>Dado</strong> una salida con kits,<br>
        <strong>Cuando</strong> confirmo,<br>
        <strong>Entonces</strong> se crean movimientos por cada componente y se descuenta su stock.<br><br>
        <strong>Escenario 02: Cálculo de costo del kit</strong><br>
        <strong>Dado</strong> una receta válida,<br>
        <strong>Cuando</strong> se calcula la utilidad,<br>
        <strong>Entonces</strong> el costo del kit = Σ(costos × cantidades) de componentes.<br><br>
        <strong>Escenario 03: Validaciones</strong><br>
        <strong>Dado</strong> falta de stock o receta con errores (ciclos/componente inexistente),<br>
        <strong>Cuando</strong> intento confirmar,<br>
        <strong>Entonces</strong> el sistema bloquea y muestra el error.
      </td>
      <td>EP-05, EP-04</td>
    </tr>
    <tr>
      <td>TS04</td>
      <td>Read models para KPIs/Reportes</td>
      <td>Como analista, quiero modelos de lectura actualizados por eventos para consultar KPIs y reportes rápidos sin afectar la base transaccional.</td>
      <td>
        <strong>Escenario 01: Proyección consistente</strong><br>
        <strong>Dado</strong> eventos de ingreso/salida/ajuste,<br>
        <strong>Cuando</strong> se procesan,<br>
        <strong>Entonces</strong> los modelos de lectura reflejan saldos y KPIs correctos.<br><br>
        <strong>Escenario 02: Desempeño</strong><br>
        <strong>Dado</strong> volúmenes altos,<br>
        <strong>Cuando</strong> consulto KPIs,<br>
        <strong>Entonces</strong> la API responde &lt; 200&nbsp;ms en consultas comunes.<br><br>
        <strong>Escenario 03: Consistencia eventual</strong><br>
        <strong>Dado</strong> carga elevada,<br>
        <strong>Cuando</strong> ocurre la proyección,<br>
        <strong>Entonces</strong> la latencia es &le; 5&nbsp;s y se muestra “actualizado hace X s”.
      </td>
      <td>EP-03, EP-07</td>
    </tr>
  </tbody>
</table>

## 3.3. Product Backlog

| # Orden | User Story Id | Título                                    | Descripción                                                                                                                                                                  | Story Points (1/2/3/5/8) |
| :------ | :------------ | :---------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------- |
| 01      | US-01         | Iniciar borrador de salida                | Como cajero, quiero iniciar un borrador de salida para agrupar ítems de una venta antes de confirmarla.                                                                      | 3                        |
| 02      | US-02         | Gestionar ítems del borrador              | Como cajero, quiero buscar productos y agregar/editar/retirar ítems con cantidades válidas sin impactar el stock aún.                                                        | 3                        |
| 03      | US-03         | Calcular total y utilidad de la salida    | Como dueño, quiero que el sistema calcule en tiempo real el total y la utilidad por ítem/kit y global, usando el costo vigente.                                              | 5                        |
| 04      | US-04         | Confirmar salida y descontar inventario   | Como cajero, quiero confirmar la salida para registrar los movimientos de inventario (productos y componentes de kits) y actualizar el on-hand.                              | 2                        |
| 05      | US-05         | Reporte de stock a fecha (valorizado)     | Como gerente, quiero emitir un reporte de stock a una fecha de corte, con cantidades on-hand, costo vigente y valorizado por producto/lote.                                  | 8                        |
| 06      | US-06         | Reporte de rotación y ventas (utilidad)   | Como gerente, quiero un reporte por periodo con unidades vendidas, ingreso, costo y utilidad por producto/categoría, para identificar top/slow movers.                       | 5                        |
| 07      | US-07         | Reporte de mermas y ajustes               | Como dueño, quiero un reporte de ajustes (±) y mermas por periodo, con motivo, usuario y valorizado, para auditar pérdidas.                                                  | 3                        |
| 08      | US-08         | Reporte de bajo stock y próximos a vencer | Como jefe de compras, quiero un listado de productos bajo umbral y lotes próximos a vencer, con días de cobertura y acciones sugeridas.                                      | 5                        |
| 09      | US-09         | Filtrado de métricas                      | Como usuario, quiero filtrar las métricas del dashboard por rango de fechas y categorías de productos, para analizar información más específica y relevante.                 | 3                        |
| 10      | US-10         | Exportación de métricas                   | Como usuario, quiero exportar los datos del dashboard, para compartirlos fácilmente con mi equipo o realizar reportes externos.                                              | 3                        |
| 11      | US-11         | Notificaciones en el dashboard            | Como usuario, quiero visualizar en el dashboard notificaciones destacadas de bajo stock y próximos vencimientos, para priorizar las acciones más urgentes.                   | 3                        |
| 12      | US-12         | Crear producto en catálogo                | Como jefe de compras quiero registrar un nuevo producto para asegurar una gestion productos consistente                                                                      | 3                        |
| 13      | US-13         | Edición de producto                       | Como jefe de compras quiero editar los datos de un producto existente para mantener actualizada la información en el catálogo                                                | 2                        |
| 14      | US-14         | Eliminación e inhabilitacion de productos | Como jefe de compras quiero poder desactivar o eliminar un producto para mantener un control y no saturar el sistema                                                         | 3                        |
| 15      | US-15         | Clasificación de productos por categoría  | Como jefe de compras quiero asignar categorías a los productos para organizar el catálogo y facilitar búsquedas                                                              | 2                        |
| 16      | US-16         | Búsqueda y filtrado de productos          | Como jefe de compras quiero buscar y filtrar productos por nombre, categoría o estado para acceder rápidamente a la información                                              | 3                        |
| 17      | US-17         | Historial de cambios de producto          | Como jefe de compras quiero consultar el historial de cambios de cada producto para corroborar precios y poder planificar estrategicamente                                   | 3                        |
| 18      | US-18         | Sección de funcionalidades                | Como visitante quiero visualizar las principales funcionalidades de stocktrack en la landing para conocer qué ofrece la plataforma                                           | 3                        |
| 19      | US-19         | Formulario de registro                    | Como visitante quiero acceder a un formulario de registro en la landing para crear una cuenta rápidamente                                                                    | 3                        |
| 20      | US-20         | Formulario de contacto                    | Como visitante quiero llenar un formulario de contacto en la landing para solicitar información adicional sobre stocktrack                                                   | 3                        |
| 21      | US-21         | Diseño responsive                         | Como visitante quiero que la landing sea responsive para navegar de manera cómoda desde cualquier dispositivo                                                                | 2                        |
| 22      | US-22         | Sección de testimonios                    | Como visitante quiero ver testimonios de otros usuarios en la landing para confiar más en la plataforma                                                                      | 3                        |
| 23      | US-23         | Botones claros                            | Como visitante quiero ver botones claros y visibles para que sea intuitivo durante la navegación                                                                             | 3                        |
| 24      | US-24         | Crear proveedor                           | Como jefe de compras, quiero registrar nuevos proveedores con su información clave (nombre, contacto, RUC) para centralizar los datos de mis abastecedores.                  | 3                        |
| 25      | US-25         | Consultar y editar proveedores            | Como encargado, quiero poder ver la lista de proveedores, buscar uno específico y editar su información para mantener los datos actualizados.                                | 3                        |
| 26      | US-26         | Asociar productos a proveedor             | Como jefe de compras, quiero asociar productos a un proveedor para saber a quién comprar cada artículo y facilitar los reportes.                                             | 5                        |
| 27      | US-27         | Visualizar KPIs principales               | Como dueño, quiero ver en el dashboard tarjetas con KPIs clave (valor de inventario, productos con stock bajo) para un resumen rápido del negocio.                           | 2                        |
| 28      | US-28         | Ver alertas críticas                      | Como encargado, quiero que el dashboard me muestre una lista de alertas urgentes (lotes próximos a vencer) para tomar acciones preventivas.                                  | 3                        |
| 29      | US-29         | Definir composición de un kit             | Como encargado, quiero crear la "receta" de un kit, asociando productos existentes y sus cantidades, para estandarizar el contenido de los paquetes.                         | 3                        |
| 30      | US-30         | Ensamblar kits y ajustar stock            | Como encargado de bodega, quiero registrar el "ensamblaje" de kits para que el sistema descuente el stock de los componentes y aumente el stock del kit como producto final. | 5                        |
| 31      | US-31         | Configurar umbrales de stock              | Como jefe de compras, quiero definir umbrales mínimos de stock por producto para que el sistema pueda generar alertas automáticas.                                           | 5                        |
| 32      | US-32         | Generar alerta de bajo stock              | Como sistema, quiero generar una alerta cuando el stock de un producto caiga por debajo del umbral configurado.                                                              | 5                        |
| 33      | US-33         | Generar alerta de vencimiento             | Como sistema, quiero generar una alerta cuando un lote esté próximo a vencer dentro de la ventana configurada.                                                               | 3                        |
| 34      | US-34         | Listar alertas pendientes                 | Como usuario, quiero ver un listado de todas las alertas activas (bajo stock, próximos a vencer, vencidos) para tomar decisiones.                                            | 3                        |
| 35      | TS-35         | Notificación externa de alertas           | Como usuario, quiero recibir notificaciones por correo o push cuando se generen alertas críticas.                                                                            | 8                        |
| 36      | TS-36         | Gestionar estado de alertas               | Como jefe de compras, quiero marcar las alertas como atendidas o descartadas para mantener control del seguimiento.                                                          | 3                        |
| 37      | TS-37         | Iniciar borrador de ingreso               | Como asistente de almacén, quiero iniciar un borrador de ingreso para registrar productos recibidos antes de confirmarlos.                                                   | 3                        |
| 38      | TS-38         | Registrar ítems del ingreso               | Como asistente de almacén, quiero agregar productos, lotes y cantidades recibidas al borrador sin impactar aún el stock.                                                     | 3                        |
| 39      | TS-39         | Registrar costo y proveedor               | Como asistente de almacén, quiero asociar cada ingreso a un costo unitario y proveedor para trazabilidad de compras.                                                         | 3                        |
| 40      | TS-40         | Confirmar ingreso y actualizar stock      | Como asistente de almacén, quiero confirmar el ingreso para registrar movimientos positivos y actualizar el on-hand.                                                         | 5                        |
| 41      | TS-41         | Adjuntar documento de respaldo            | Como asistente de almacén, quiero adjuntar la factura o guía de remisión al ingreso para evidencia documental.                                                               | 2                        |
| 42      | TS-42         | Disparar alertas por ingreso              | Como sistema, quiero recalcular coberturas y eliminar alertas de bajo stock cuando se confirme un ingreso.                                                                   | 5                        |
| 43      | TS-43         | Verificar compra de lotes                 | Como dueño de bodega, quiero gestionar y verificar la cantidad de los lotes recibidos para tener un mejor control del inventario.                                            | 3                        |
| 44      | TS-44         | Ver fecha de vencimiento de los lotes     | Como asistente de almacén, quiero verificar la fecha de vencimiento de mis productos para estar pendiente de cuando reponerlos.                                              | 2                        |
| 45      | US-45         | Registrar costo y proveedor               | Como asistente de almacén, quiero asociar cada ingreso a un costo unitario y proveedor para trazabilidad de compras.                                                         | 1                        |
| 46      | US-46         | Alertar vencimiento próximo               | Como dueño de bodega, quiero recibir una alerta cuando un lote esté próximo a vencer para poder tomar decisiones a tiempo.                                                   | 2                        |
| 47      | US-47         | Buscar lotes por proveedor                | Como dueño de bodega, quiero filtrar los lotes por proveedor para identificar rápidamente qué productos corresponden a cada socio comercial.                                 | 2                        |
| 48      | US-48         | Editar información de un lote             | Como asistente de almacén, quiero poder editar la información de un lote (fecha de vencimiento, cantidad o proveedor) para corregir errores en el registro.                  | 2                        |
| 49      | US-49         | Ver historial de movimientos de un lote   | Como dueño de bodega, quiero consultar el historial de movimientos de cada lote para tener trazabilidad de ingresos y salidas.                                               | 3                        |
| 50      | US-50         | Crear usuarios nuevos                     | Como dueño de un startup, quiero crear cuentas de usuario para que cada miembro del equipo tenga acceso individual a la plataforma.                                          | 3                        |
| 51      | US-51         | Asignar roles                             | Como administrador, quiero asignar un rol a cada usuario para definir qué puede y qué no puede hacer dentro de la aplicación.                                                | 3                        |
| 52      | US-52         | Editar permisos personalizados            | Como administrador, quiero ajustar permisos específicos en un usuario para dar accesos excepcionales.                                                                        | 3                        |
| 53      | US-53         | Bloquear usuarios                         | Como administrador, quiero poder desactivar usuarios para evitar accesos no autorizados.                                                                                     | 2                        |
| 54      | US-54         | Ver lista de usuarios                     | Como administrador, quiero ver un listado con todos los usuarios, roles y estado de cuenta para gestionar mejor el equipo.                                                   | 2                        |
| 55      | US-55         | Cambiar rol de un usuario                 | Como administrador, quiero poder cambiar el rol de un usuario para ajustar sus responsabilidades dentro de la bodega/startup.                                                | 3                        |
| 56      | US-56         | Auditoría de accesos                      | Como administrador, quiero consultar un historial de accesos de los usuarios para detectar intentos fallidos o acciones sospechosas.                                         | 2                        |
| 57      | US-57         | Roles predefinidos                        | Como administrador, quiero contar con roles predefinidos (Administrador, Supervisor, Asistente) para acelerar la configuración inicial.                                      | 5                        |

## 3.4. Impact Mapping

A continuación se visualiza el **Impact Map** del proyecto **Inventiapp**, donde se muestra la relación entre el *Business Goal* definido, los **User Personas** identificados, los **Impactos** esperados en su comportamiento, los **Deliverables** que como negocio digital podemos ofrecer y las **User Stories** asociadas que permitirán implementar las funcionalidades necesarias en la aplicación web y la landing page. Este mapa busca asegurar la alineación entre los objetivos estratégicos y el desarrollo de la solución digital.

<p align="center">
  <img src="/assets/img/chapter-III/impactMap.png" alt="Impact Map" width="700">
</p>

