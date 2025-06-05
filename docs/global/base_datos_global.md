# Base de Datos Global - SIAC 2.0

Este documento presenta la estructura relacional y temática de las principales tablas utilizadas en el sistema SIAC 2.0. Su objetivo es servir como guía general sobre cómo se organiza y relaciona la información a nivel de base de datos, sin documentar exhaustivamente cada campo. Las tablas de uso común se explican aquí. Las tablas específicas se abordan en las fichas técnicas de cada módulo.

---

## 1. Entidades Principales

Estas tablas representan entidades fundamentales y son reutilizadas por varios módulos:


| Tabla              | Descripción                                                                 | Módulos que la usan                        |
|--------------------|------------------------------------------------------------------------------|---------------------------------------------|
| `add_clientes`     | Contiene información general de clientes: identificación, contacto, ubicación y asignación comercial. | CRM, Ventas, Liquidación, Facturación       |
| `add_productos`    | Catálogo central de productos, incluye descripción, precio, estado, y categoría. | Inventario, Ventas, Producción, Facturación |
| `add_remision`     | Encabezado de remisiones de producto: cliente, fecha, estatus y totales.     | Ventas, CEDIS, Liquidación, Facturación     |
| `add_remision_productos_orden` | Detalle de productos asociados a una remisión: cantidades, precios, descuentos. | Ventas, Liquidación, Facturación           |
| `liquidacion`      | Registra operaciones validadas (órdenes cerradas) con resumen de ventas por agente. | Liquidación                                 |
| `add_cfdi_cpago`   | Almacena los complementos de pago emitidos para uno o más CFDIs.              | Facturación, Caja                           |
| `add_stock_ajuste` | Contiene la información actualizada del stock. | CEDIS, Ventas|

---

### Descripción Detallada de Tablas Núcleo

### `add_clientes`

Tabla principal de clientes con datos personales, comerciales y fiscales.

- Campos principales: `idc`, `codigo`, `nombre`, `mail`, `idr`, `ide`, `ids`
- Relaciones:
  - `add_credito_clientes`: condiciones de crédito
  - `add_clientes_maps`, `add_emails_clientes`: contacto y geolocalización
  - `add_remision`, `add_cfdi_cpago`: historial de ventas y pagos
  - `add_clientes_tipos`: clasificación comercial
- Usos: validación de crédito, asignación de rutas, facturación:contentReference[oaicite:0]{index=0}

### `add_productos`

Catálogo maestro de productos disponibles para remisión y facturación.

- Campos comunes: `idprod`, `clave`, `nombre`, `categoria`, `precio`, `activo`
- Relaciones:
  - `add_ct_productos`: categorías
  - `add_stock`: control de inventario
  - `add_remision_productos_orden`, `add_cfdi_venta_productos`: historial de ventas
- Usos: generación de pedidos, control de stock, reporte de productos:contentReference[oaicite:1]{index=1}

### `add_remision`

Encabezado de remisión con información de cliente, monto, fecha y estatus.

- Campos: `idrem`, `idc`, `fecha`, `total`, `estatus`
- Relaciones:
  - `add_remision_productos_orden`: detalle por producto
  - `liquidacion`: relación con cierre de ventas
  - `add_cfdi_venta_clientes`: relación con facturación CFDI
- Usos: confirmación de entregas, base para CFDI, cierre de ventas:contentReference[oaicite:2]{index=2}

### `add_remision_productos_orden`

Detalle de productos por remisión: cantidades, unidad, descuentos, precio unitario.

- Clave compuesta: `idrem`, `idprod`
- Usos: generación de CFDI, cálculo de comisiones, análisis de ventas netas:contentReference[oaicite:3]{index=3}

### `liquidacion`

Tabla resumen de procesos de validación de ventas (por agente, sucursal, producto).

- Campos: `idliq`, `idrem`, `idvendedor`, `total`, `estado`, `fecha`
- Relaciones:
  - `add_remision`: fuente primaria
  - `add_comision_suc_meses`: cálculo de comisiones
- Usos: reporte de cierre mensual, generación de comisiones, auditoría de ventas:contentReference[oaicite:4]{index=4}

### `add_cfdi_cpago`

Complemento de pago asociado a múltiples CFDIs, conforme a normativa SAT.

- Campos: `idcpago`, `uuid`, `idcliente`, `monto`, `fecha_pago`
- Relaciones:
  - `add_cfdi_cpago_info`: método y forma de pago
  - `add_cfdi_cpago_rel_cfdis`: relación con CFDIs origen
  - `add_cfdi_cpago_cancel`: cancelaciones
- Usos: gestión de pagos parciales, cumplimiento fiscal, conciliación con remisiones:contentReference[oaicite:5]{index=5}

---

## 2. Agrupación Funcional de Tablas

### 2.1 Clientes y CRM

Incluye información de clientes, clasificación, crédito, y visitas.

- `add_clientes`, `add_clientes_tipos`
- `add_credito_clientes`, `add_datos_facturas_clientes`
- `add_rutas`, `add_frec_visita_clientes`
- `add_emails_clientes`, `add_clientes_maps`
- `add_clientes_cred_check`, `add_clientes_archivos`

### 2.2 Productos y Stock

Catálogo de productos y control de inventario.

- `add_productos`, `add_ct_productos`
- `add_stock`, `add_stock_ajuste`, `add_backup_stock_almacen`
- `add_mini_stock_vendedor`, `prodts_pedido_stock`
- `traslado_stock`, `add_no_salida_stock`

### 2.3 Ventas y Remisiones

Pedidos, remisiones y control de documentos de venta.

- `pedido_clientes`, `producto_pedido_clientes`
- `add_remision`, `add_remision_productos`
- `add_remision_venta_neta`, `add_remision_productos_orden`
- `venta_curso`, `venta_neta_sucursal`, `liquidacion`

### 2.4 Cobranza y Caja

Gestión de pagos, recibos y conciliaciones.

- `add_no_recibo_print`, `lista_recibos_x_cancelar`
- `add_pagos_noor_rem`, `add_cxc_abona`, `add_cxc_docs_cobrar_av`
- `add_cxc_cza_doc_pago`, `add_cxc_cza_rbo_av`

### 2.5 Facturación Electrónica (CFDI)

CFDIs emitidos, complementos de pago y cancelaciones.

- `add_cfdi_info`, `add_cfdi_cpago`, `add_cfdi_cancel`
- `add_cfdi_venta_clientes`, `add_cfdi_venta_productos`
- `add_cfdi_rel_cfdis_cfdi`, `add_cfdi_cpago_rel_cfdis`

### 2.6 Comisiones y Presupuesto

Asignación y cálculo de comisiones y metas.

- `add_comision_suc_meses`, `add_comision_producto`
- `add_comision_pje_suc`, `add_comision_docs_cobranza`
- `add_presupuesto_suc_mes`, `add_presupuesto_av_anual`

### 2.7 Recursos Humanos

Datos de empleados y administración laboral.

- `add_empleados`, `add_rh_docs`, `add_rh_bajas`
- `add_empleado_bien_inmb`, `add_vacas_emplea`

### 2.8 Seguridad y Usuarios

Control de accesos, roles y permisos.

- `add_user`, `add_user_empresa`, `add_user_tipo`
- `roles_usuar`, `roles_usuar_menu`
- `add_permiso_app_siac`, `add_user_menu_hijo`

### 2.9 Geografía y Localización

División territorial y de sucursales.

- `pais`, `pais_estados`, `pais_municipios`
- `add_sucursal`, `add_rel_zonas_suc`

---

## 3. Consideraciones

- Cada módulo define sus propias tablas auxiliares que **no se listan aquí** si su uso es exclusivo.
- Para campos específicos, índices y procedimientos almacenados, consultar el **diccionario técnico de base de datos** o la documentación de cada módulo.
- Se recomienda usar este documento como guía conceptual para comprender la arquitectura de datos y las relaciones transversales del sistema.
