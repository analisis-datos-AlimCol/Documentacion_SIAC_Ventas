# Ficha Técnica del Módulo CEDIS - SIAC 2.0 Ventas

## 1. Propósito General

El módulo **CEDIS** (Centro de Distribución) administra el inventario de producto terminado en almacenes principales. Su funcionalidad abarca el registro, control, ajuste y seguimiento de productos que ingresan y salen del almacén, además de gestionar transferencias internas y respaldos de datos.

Este módulo es fundamental para garantizar la trazabilidad del inventario y su disponibilidad en operaciones de ventas, compras, producción y logística.

---

## 2. Arquitectura Técnica

Este módulo implementa la arquitectura estándar del sistema SIAC 2.0 definida en [Arquitectura del Sistema](../global/arquitectura.md), incluyendo:

- Separación por capas (presentación, lógica de negocio, datos)
- Uso de AJAX con tokens para interacción dinámica
- Validaciones integradas de sesión, permisos y datos

---

## 3. Estructura de Archivos del Módulo


| Archivos                          | Funcionalidad                                               |
|----------------------------------|-------------------------------------------------------------|
| `cds_ajax.php`                   | Puente AJAX entre frontend y backend, validación.           |
| `cds_forms.php`                  | Formularios para entradas, salidas, consultas.              |
| `cds_tablas.php`                 | Renderización de tablas HTML.                               |
| `cds_widgets.php`                | Visualización de KPIs.                                      |
| `cds_modals.php`                 | Ventanas emergentes.                                        |
| `cds_g_orden_salida.php`         | Gestión de órdenes de salida.                               |
| `cds_g_inventarios.php`          | Vista principal de inventario.                              |
| `cds_wspace.php`                 | Espacio de trabajo del usuario.                             |
| `cds_select.php`                 | Carga de datos en selects dinámicos.                        |
| `view_cds_stk_ent_loc_pt.php`    | Respaldo de stock desde JSON.                               |
| `cds_ajax.js`                    | Eventos y validaciones principales.                         |
| `cds_ajax_1.js`                  | Eventos adicionales y funciones auxiliares.                 |
| `cds_g_texturizados.js`          | Gestión de texturizados.                                    |
| `cds_g_stock.js`                 | Control de stock.                                           |
| `cds_g_orden_salida.js`          | Eventos de órdenes de salida.                               |
| `cds_g_inventarios.js`           | Eventos de inventario.                                      |
| `cds_g_tarimas.js`               | Gestión de tarimas.                                         |
| `cds_g_movimientos.js`           | Control de movimientos.                                     |
| `cds_g_reportes.js`              | Generación de reportes.                                     |
| `cds_g_config.js`                | Configuración del módulo.                                   |
| `cds_g_validaciones.js`         | Validaciones específicas.                                   |
| `cds_g_widgets.js`               | Eventos de widgets.                                         |
| `cds_g_graficas.js`              | Generación de gráficas.                                     |
| `cds_g_util.js`                  | Funciones utilitarias.                                      |

---


### 3.1 Clases CEDIS Producto Terminado
- [c_View_cds (Vista)](../phpdoc/classc___view__cds.html)
- [c_Add_cds (Añadir)](../phpdoc/classc___add__cds.html)
- [c_Up_cds (Actualizar)](../phpdoc/classc___up__cds.html)
- [c_Rmv_cds (Eliminar)](../phpdoc/classc___rmv__cds.html)
- [c_Fun_cds (Funciones)](../phpdoc/classc___fun__cds.html)
- [c_Msj_cds (Mensajes)](../phpdoc/classc___msj__cds.html)

## 4. Funcionalidades Principales

### 4.1 Gestor de Órdenes de Salida

Gestión completa del proceso de despacho de productos desde el CEDIS. Permite crear órdenes, asignar productos y generar documentos de salida.

**Características:**

- Creación de órdenes de salida
- Edición de órdenes existentes
- Validación de existencias vs. pedidos
- Cálculo de efectividad (porcentaje de solicitud cubierta)
- Generación de reportes y PDFs
- Impresión de documentos

**Referencias técnicas:**

- Tokens: 100-107
- Archivos: `cds_g_orden_salida.php`, `cds_ajax.php`
- Clases: `c_Up_cds`, `c_Rmv_cds`, `c_View_cds`

**Funciones principales:**

- `cds_add_gos_cedis_os_tit_reg`: Creación de órdenes
- `cds_up_gos_cedis_os_tit_reg`: Edición de órdenes
- `cds_view_query_x_scrip`: Validación de existencias
- `cds_add_gos_cedis_os_prod`: Asignación de productos

**Diagrama**

<div class="mermaid">

graph TD
    %% Nodos principales
    OS[Gestor de Órdenes de Salida] --> OS1[Crear Orden]
    OS --> OS2[Editar Orden]
    OS --> OS3[Generar Reporte]

    %% Procesos comunes
    SUB1[Validar Existencias] --> SUB11[Consultar Stock]
    SUB11 --> SUB12[Comparar con Pedido]
    SUB12 --> SUB13[Actualizar Efectividad]

    %% Crear Orden
    OS1 --> OS11[Asociar Pedido]
    OS11 --> SUB1
    SUB1 --> OS14[Guardar Orden]

    %% Editar Orden
    OS2 --> OS21[Seleccionar Orden]
    OS21 --> OS22[Modificar Productos]
    OS22 --> SUB1
    SUB1 --> OS23[Guardar Cambios]

    %% Generar Reporte
    OS3 --> OS31[Seleccionar Tipo]
    OS31 --> OS32[Generar PDF]
    OS32 --> OS33[Mostrar Documento]

    %% Estilos
    classDef proceso fill:#bbf,stroke:#333,stroke-width:1px
    classDef subproceso fill:#fbb,stroke:#333,stroke-width:1px
    classDef documento fill:#bfb,stroke:#333,stroke-width:1px

    class OS1,OS2,OS3 proceso
    class OS11,OS14,OS21,OS22,OS23,OS31,OS32,OS33 proceso
    class SUB1,OS11,OS12,OS13 subproceso
</div>

### 4.2 Existencias de Productos Terminados

Control y visualización de inventario de productos terminados en el CEDIS.

**Características:**

- Consulta de existencias en tiempo real
- Gráficas por categorías
- Respaldo de información
- Historial de movimientos
- Generación de reportes

**Referencias técnicas:**

- Tokens: 95-98
- Archivos: `cds_g_stock.php`, `cds_ajax.php`
- Clases: `c_View_cds`, `c_Add_cds`

**Funciones principales:**

- `cds_view_query_x_scrip`: Consulta de existencias
- `cds_add_ginv_stock_bk_prod`: Respaldo de stock
- `cds_add_gtex_cedis_ent_pt_prod`: Entrada de productos
- `cds_up_gtex_prod_stk_cant_x_ids`: Ajustes de stock

**Diagrama**

<div class="mermaid">

graph TD
    %% Nodos principales
    ST[Existencias de Productos Terminados] --> ST1[Consultar Existencias]
    ST --> ST2[Ver Gráficas]
    ST --> ST3[Realizar Respaldo]
    ST --> ST4[Consultar Movimientos]

    %% Consulta de Existencias
    ST1 --> ST11[Seleccionar Categoría]
    ST11 --> ST12[Buscar Producto]
    ST12 --> ST13[Mostrar Stock]
    ST13 --> ST14[Exportar Datos]

    %% Ver Gráficas
    ST2 --> ST21[Generar Gráfica]
    ST21 --> ST22[Mostrar Visualización]

    %% Realizar Respaldo
    ST3 --> ST31[Generar Backup]
    ST31 --> ST32[Guardar Archivo]

    %% Consultar Movimientos
    ST4 --> ST41[Seleccionar Fecha]
    ST41 --> ST42[Mostrar Historial]
    ST42 --> ST43[Exportar Reporte]

    %% Estilos
    classDef proceso fill:#bbf,stroke:#333,stroke-width:1px
    classDef subproceso fill:#fbb,stroke:#333,stroke-width:1px
    classDef documento fill:#bfb,stroke:#333,stroke-width:1px

    class ST1,ST2,ST3,ST4 proceso
    class ST11,ST12,ST13,ST14,ST21,ST22,ST31,ST32,ST41,ST42,ST43 proceso

</div>

### 4.3 Gestor de Materiales Adicionales

Gestión de productos sin pedidos asociados y seguimiento de inventario.

**Características:**

- Creación de órdenes independientes
- Gestión de productos
- Seguimiento de existencias
- Control de movimientos

**Referencias técnicas:**

- Tokens: 80-84
- Archivos: `cds_g_materiales.php`, `cds_ajax.php`
- Clases: `c_Add_cds`, `c_Rmv_cds`

**Funciones principales:**

- `cds_add_gos_cedis_os_tit_reg`: Creación de órdenes
- `cds_add_gos_cedis_os_prod`: Gestión de productos
- `cds_view_query_x_scrip`: Seguimiento de inventario

**Diagrama**

<div class="mermaid">
graph TD
    %% Nodos principales
    MA[Gestor de Materiales Adicionales] --> MA1[Crear Orden]
    MA --> MA2[Gestionar Productos]
    MA --> MA3[Seguimiento de Existencias]

    %% Crear Orden
    MA1 --> MA11[Generar Título]
    MA11 --> MA12[Asignar Productos]
    MA12 --> MA13[Guardar Orden]

    %% Gestionar Productos
    MA2 --> MA21[Seleccionar Producto]
    MA21 --> MA22[Actualizar Cantidad]
    MA22 --> MA23[Guardar Cambios]

    %% Seguimiento de Existencias
    MA3 --> MA31[Consultar Stock]
    MA31 --> MA32[Mostrar Movimientos]
    MA32 --> MA33[Exportar Reporte]

    %% Estilos
    classDef proceso fill:#bbf,stroke:#333,stroke-width:1px
    classDef subproceso fill:#fbb,stroke:#333,stroke-width:1px
    classDef documento fill:#bfb,stroke:#333,stroke-width:1px

    class MA1,MA2,MA3 proceso
    class MA11,MA12,MA13,MA21,MA22,MA23,MA31,MA32,MA33 proceso
</div>

### 4.4 Gestor de Texturizados

Gestión de productos texturizados desde producción hasta almacenamiento.

**Características:**

- Entrada de productos desde producción
- Confirmación de tarimas
- Actualización manual de productos
- Control de precios
- Consulta de movimientos

**Referencias técnicas:**

- Tokens: 107-110
- Archivos: `cds_g_texturizados.php`, `cds_ajax.php`
- Clases: `c_Ws_Up`, `c_View_cds`, `c_Add_cds`

**Funciones principales:**

- `cds_gtex_prog_fol_tma_edo_up_x_ids`: Confirmación de tarimas
- `cds_add_gtex_cedis_ent_pt_prod`: Entrada de productos
- `cds_add_gtex_cedis_ent_pt_tit`: Creación de títulos
- `cds_up_gtex_prod_stk_cant_x_ids`: Actualización de precios

**Diagrama**

<div class="mermaid">
graph TD
    %% Nodos principales
    TX[Gestor de Texturizados] --> TX1[Entrada de Productos]
    TX --> TX2[Entrada Manual]
    TX --> TX3[Actualizar Precios]
    TX --> TX4[Consultar Movimientos]

    %% Entrada de Productos
    TX1 --> TX11[Recibir Datos]
    TX11 --> TX12[Validar Entrada]
    TX12 --> TX13[Confirmar Tarimas]
    TX13 --> TX14[Registrar Productos]
    TX14 --> TX15[Actualizar Stock]

    %% Entrada Manual
    TX2 --> TX21[Seleccionar Producto]
    TX21 --> TX22[Ingresar Datos]
    TX22 --> TX23[Actualizar Stock]
    TX23 --> TX24[Guardar Cambios]

    %% Actualizar Precios
    TX3 --> TX31[Seleccionar Producto]
    TX31 --> TX32[Actualizar Precio]
    TX32 --> TX33[Guardar Cambios]

    %% Consultar Movimientos
    TX4 --> TX41[Seleccionar Fecha]
    TX41 --> TX42[Mostrar Historial]
    TX42 --> TX43[Exportar Reporte]

    %% Estilos
    classDef proceso fill:#bbf,stroke:#333,stroke-width:1px
    classDef subproceso fill:#fbb,stroke:#333,stroke-width:1px
    classDef documento fill:#bfb,stroke:#333,stroke-width:1px

    class TX1,TX2,TX3,TX4 proceso
    class TX11,TX12,TX13,TX14,TX15,TX21,TX22,TX23,TX24,TX31,TX32,TX33,TX41,TX42,TX43 proceso
</div>


## 5. Integraciones

### 5.1 Módulos Internos

#### Módulo de Ventas

Permite validar existencia de productos al momento de realizar ventas y sincronizar los movimientos de inventario.

- **Características:** Validación de stock en tiempo real, sincronización de precios
- **Referencia:** `cds_ajax.php`, líneas 312–349

#### Módulo de Contabilidad

Ajustes contables automáticos según los movimientos de inventario, órdenes de salida y devoluciones.

- **Características:** Facturación automática, comprobantes de egreso, ajuste de inventarios con impacto contable
- **Referencia:** `cds_ajax.php`, líneas 212–247

#### Módulo de Compras

Automatiza la recepción de productos y su ingreso al inventario al cierre del ciclo de compras.

- **Características:** Validación de órdenes, asignación a ubicaciones, control de calidad
- **Referencia:** `cds_ajax.php`, líneas 142–176

---

### 5.2 Servicios Externos

#### Servicios Web

Sincronización con servicios externos para control de tarimas y envío de notificaciones.

- **Características:** Comunicación vía JSON, envío de etiquetas, respuesta a eventos externos
- **Referencia:** `cds_ajax.php`, líneas 1–30

#### Facturación Electrónica

Generación de comprobantes y sincronización con el sistema fiscal externo.

- **Características:** Generación de CFDI, integración con folios, emisión automática
- **Referencia:** Integración general (consultas cruzadas con módulo contable)

---

### 5.3 Sistema de Archivos

Gestión documental para reportes e historiales del sistema, incluyendo exportaciones en formato PDF y respaldos automáticos.

- **Características:** Exportación, almacenamiento estructurado, control de versiones
- **Referencia:** `cds_ajax.php`, líneas 248–277

### 5.4 Flujo de Integraciones

<div class="mermaid">
graph TD
    A[CEDIS] --> B[Ventas]
    B --> C[Contabilidad]
    C --> D[Compras]
    A --> E[Servicios Web]
    A --> F[Facturación]
</div>


## 6. Interacción Cliente-Servidor


Ver detalles del patrón de comunicación en [Interacción Cliente-Servidor](../global/interaccion_cliente_servidor.md).

---

## 7. Seguridad y Validaciones

- Validación de sesión en cada llamada AJAX
- Control de acceso por tipo de usuario, empresa y sucursal
- Validación de datos con HTML5 y JavaScript en frontend
- Validación de existencia, disponibilidad y consistencia de datos en backend

Ver estándares completos en [Seguridad y Validaciones](../global/seguridad_validaciones.md).

---


## 7. Base de Datos

**Procedimientos Almacenados (SPs):** `sp_cds_*`

**Tablas clave:**

- Tablas de Ordenes de Salida:
    - `add_mini_stock_vendedor_temp` (almacena temporalmente productos para órdenes)
    - `add_mini_stock_vendedor` (almacena productos de órdenes)
    - `add_stock_ajuste` (almacena ajustes de stock)
- Tablas de Productos:
    - `add_descuento_prom_prod_his` (historial de descuentos y promociones)
    - `add_stock_ajuste` (ajustes de stock)
- Tablas de Agentes de Venta:
    - `add_cc_myr` (agentes de venta y sus permisos)
- Tablas de CEDIS:
    - `add_stock_ajuste` (control de stock)
    - `add_mini_stock_vendedor` (stock por vendedor)
- Tablas de Movimientos de Stock:
    - `add_stock_ajuste` (registra ajustes de stock)
    - `add_mini_stock_vendedor` (movimientos de stock por vendedor)
- Tablas de Historial:
    - `add_descuento_prom_prod_his` (historial de descuentos)
    - `add_stock_ajuste` (historial de ajustes)
- Tablas de Configuración:
    - `add_cc_myr` (configuración de agentes y sucursales)

- Tablas de Stock Principal:
    - add_stock_ajuste - Ajustes de stock
    - add_mini_stock_vendedor - Stock temporal de vendedores
    - prodts_pedido_stock - Productos en pedidos de stock
    - prodts_pedido_stock_temp - Productos en pedidos de stock temporal
- Tablas de Traslados y Movimientos:
    - inicia_ruta_stock_vendedor - Rutas de traslado de stock
    - add_no_salida_stock - Números de salida de stock
- Tablas de Backup:
    - stock_backup_titulo - Títulos de backups
    - stock_backup_productos - Productos en backups
    - add_backup_stock_almacen - Backups de stock por almacén
    - add_backup_stock_almacen_prod - Productos en backups de almacén
- Tablas de Pedidos y Órdenes:
    - pedido_general_stock - Pedidos generales de stock
    - ini_rut_stock_rel_t_loc - Relaciones de rutas de stock
Tablas de Registro de Ajustes:
    - reg_stock_ajuste - Registro de ajustes de stock
    





## 8. Diagrama de Flujo – Módulo CEDIS

<div class="mermaid">
graph TD
    A[Inicio] --> B[Autenticación]
    B --> C{Menú Principal CEDIS}

    %% Entradas de Productos
    C --> |Entradas| E1[Entrada de Productos]
    E1 --> E2{¿Tipo de Entrada?}
    E2 --> |Producción| E3[Entrada por Producción]
    E2 --> |Manual| E4[Entrada Manual]
    E3 --> E5[Validar Producto]
    E4 --> E5
    E5 --> E6[Actualizar Stock]
    E6 --> E7[Registrar Movimiento]
    E7 --> E8[Generar Respaldos]

    %% Salidas de Productos
    C --> |Salidas| S1[Salida de Productos]
    S1 --> S2{¿Tipo de Salida?}
    S2 --> |Órdenes| S3[Órdenes de Salida Ventas, Donaciones, Mermas, etc.]
    S2 --> |Traslados| S4[Traslados a Sucursales]
    S3 --> S5[Validar Existencia]
    S4 --> S5
    S5 --> S6{¿Suficiente Stock?}
    S6 --> |Sí| S7[Actualizar Stock]
    S6 --> |No| S8[Notificar Falta]
    S7 --> S9[Registrar Movimiento]
    S9 --> S10[Generar Documentos]
    S10 --> S11[Generar Respaldos]

    %% Consultas y Reportes
    C --> |Consultas| R1[Consultar Stock]
    R1 --> R2[Generar Reporte]
    R2 --> R3[Exportar/Imprimir]

    %% Estilos personalizados
    classDef process fill:#e1f5fe,stroke:#01579b,color:#000;
    classDef decision fill:#fff3e0,stroke:#e65100,color:#000;
    classDef startend fill:#c8e6c9,stroke:#2e7d32,color:#000;
    classDef database fill:#f5f5f5,stroke:#000000,color:#000;

    class A startend;
    class E2,S2,S6 decision;
    class B,C,E1,E3,E4,E5,E6,E7,E8,S1,S3,S4,S5,S7,S8,S9,S10,S11,R1,R2,R3 process;
</div>

