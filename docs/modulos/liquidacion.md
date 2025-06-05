# Ficha Técnica del Módulo Liquidación de Ventas - SIAC 2.0 Ventas

## 1. Propósito General

El módulo de Liquidación de Ventas es un componente crítico del sistema SIAC Ventas 2.0, diseñado para gestionar el proceso de liquidación de órdenes de compra, verificando que todos los productos sacados de CEDIS hayan sido vendidos o devueltos. Proporciona un proceso estructurado para la validación, liquidación y control de órdenes de compra.

## 2. Arquitectura Técnica

Este módulo implementa la arquitectura estándar del sistema SIAC 2.0 definida en [Arquitectura del Sistema](../global/arquitectura.md), incluyendo:

- Separación por capas (presentación, lógica de negocio, datos)
- Uso de AJAX con tokens para interacción dinámica
- Validaciones integradas de sesión, permisos y datos

## 3. Estructura de Archivos Clave

| Archivo                | Funcionalidad                    |
|------------------------|----------------------------------|
| [vta_g_liquidacion.php](cci:7://file:///c:/Users/USER/Documents/Alinsa/DocumentacionTecnica/SIAC_Ventas_2.0_13_05_2025/ventas/vta_g_liquidacion.php:0:0-0:0)| Gestor principal de liquidación   |
| [vta_wspace.php](cci:7://file:///c:/Users/USER/Documents/Alinsa/DocumentacionTecnica/SIAC_Ventas_2.0_13_05_2025/ventas/vta_wspace.php:0:0-0:0)       | Espacio de trabajo               |
| [view_os_liquidacion.php](cci:7://file:///c:/Users/USER/Documents/Alinsa/DocumentacionTecnica/SIAC_Ventas_2.0_13_05_2025/ventas/pdf/view_os_liquidacion.php:0:0-0:0)| Visualización de órdenes        |
| [view_vta_os_liquidacion.php](cci:7://file:///c:/Users/USER/Documents/Alinsa/DocumentacionTecnica/SIAC_Ventas_2.0_13_05_2025/ventas/pdf/view_vta_os_liquidacion.php:0:0-0:0)| Liquidación de ventas          |
| `vta_ajax.js`          | AJAX para liquidación           |

## 4. Funcionalidades Principales

### 4.1 Gestión de Liquidación de Órdenes

**Características:**

- Validación de órdenes de compra
- Control de productos vendidos/devueltos
- Gestión de estados de liquidación
- Cancelación de órdenes

**Referencias técnicas:**

- Tokens: 100-110
- Archivos: [vta_g_liquidacion.php](cci:7://file:///c:/Users/USER/Documents/Alinsa/DocumentacionTecnica/SIAC_Ventas_2.0_13_05_2025/ventas/vta_g_liquidacion.php:0:0-0:0), [vta_ajax.php](cci:7://file:///c:/Users/USER/Documents/Alinsa/DocumentacionTecnica/SIAC_Ventas_2.0_13_05_2025/ventas/vta_ajax.php:0:0-0:0)
- Clases: `c_Add_vta`, `c_Up_vta`, `c_Rmv_vta`

**Funciones principales:**

- `vta_gliq_suc_av_os_act_widget_view_x_ids`: Gestión inicial de liquidación
- `vta_gliq_suc_av_os_liq_envia_x_ids`: Envío de liquidación por correo
- `vta_gliq_suc_av_os_liq_imprime_x_ids`: Impresión de liquidación
- `vta_gliq_suc_av_os_act_liquida_ok_x_ids`: Confirmación de liquidación
- `vta_gliq_suc_av_os_act_rmv_x_ids`: Cancelación de liquidación

**Diagrama**

<div class="mermaid">
graph TD
    A[Inicio Proceso de Liquidación] --> B[Seleccionar Orden de Salida]
    B --> C[Establecer Fecha de Liquidación]
    C --> D[Confirmar]
    D --> E[Validar Productos]
    E --> F[Validar Documentos de Venta]
    F --> G[Generar Liquidación]


    G --> H[Confirmar Liquidación]
    H --> I[Enviar notificación]
  
   

   %% Estilos personalizados
    classDef process fill:#e1f5fe,stroke:#01579b,color:#000;
    classDef decision fill:#fff3e0,stroke:#e65100,color:#000;
    classDef startend fill:#c8e6c9,stroke:#2e7d32,color:#000;

    class A startend;
    
    class B,C,D,F,E,+G,H,I,J,K process;
</div>



### 4.2 Control de Cancelaciones

**Características:**

- Validación de remisiones
- Gestión de estados
- Solicitud de auditoría
- Cancelación de liquidación

**Referencias técnicas:**

- Tablas: `liquidacion`, `add_orden_status_liquidacion`
- Clases: `c_Rmv_vta`, `c_Up_vta`
- Funciones: `vta_rmv_query_x_scrip`, `vta_up_docs_tit_val_x_ids`

**Diagrama**

<div class="mermaid">
graph TD
    A[Inicio Proceso Cancelación Orden de Salida] --> B[Seleccionar Orden de Salida]
    B --> C{¿Tiene Documentos de Venta Asociados?}
    C -->|Sí| D[No se Puede Cancelar]
    D --> |Diríjase a| K[Módulo Ventas]
    C -->|No| E[Petición al Auditor]
    E --> F[Acepta]
    E --> G[Rechaza]
    F --> H[Orden Cancelada]

    %% Estilos personalizados
    classDef process fill:#e1f5fe,stroke:#01579b,color:#000;
    classDef decision fill:#fff3e0,stroke:#e65100,color:#000;
    classDef startend fill:#c8e6c9,stroke:#2e7d32,color:#000;
    classDef rejected fill:#ffcdd2,stroke:#b71c1c,color:#000;

    class A,H startend;
    class C,E decision;
    class B,K,F process;
    class D,G rejected;
</div>



### 4.3 Generación de Documentos

**Características:**

- Generación de PDFs
- Exportación de datos
- Envío por correo
- Historial de documentos

**Referencias técnicas:**

- Directorio: `archivos/liquidacion/`
- Archivos: `.json`, `.pdf`
- Funciones: `vta_gliq_suc_av_os_liq_envia_x_ids`




## 5. Integraciones


### 5.1 Proceso de Liquidación de Ordenes de Salida

#### 5.1.1 Validación de Documentos

El proceso de liquidación inicia con la validación de remisiones en el sistema CRM:

**Características**

   - Verificación de remisiones por cliente
  - Validación de estado de documentos
  - Consulta de historial de ventas
  - Generación de reportes de remisiones pendientes

**Referencias técnicas**

   - Tablas: `add_remision`, `add_remision_productos_orden`
  - Clase: `class_crm.php`, métodos `crm_add_remision()`, `crm_add_remision_productos()`
  - Funciones: `crm_add_remision_status()`, `crm_add_remision_venta_neta()`

#### 5.1.2 Validación de Productos

El sistema verifica el estado de los productos en CEDIS:

**Características**

- Validación de productos vendidos
- Verificación de devoluciones
- Control de stock disponible
- Actualización de movimientos

**Referencias técnicas**

   - Tablas: `inicia_ruta_stock_vendedor`, `add_mini_stock_vendedor`
  - Clase: `class_cds.php`, métodos `cds_add_gos_cedis_osalida()`, `cds_add_gos_cedis_os_depa()`
  - Funciones: `cds_add_gos_cedis_av_os_prod_dev()`, `cds_add_gos_cedis_os_tit_reg()`

#### 5.1.3 Gestión de Cobros

El proceso finaliza con la gestión de cobros en Caja:

**Características**

   - Validación de pagos
  - Gestión de cobros
  - Conciliación de ventas
  - Reportes de caja

**Referencias técnicas**

   - Tablas: `add_ticket_titulo`, `add_ticket_detalle`
  - Clase: `class_caja.php`, métodos `caja_add_ticket_titulo()`, `caja_add_ticket_detalle()`
  - Funciones: `caja_add_ticket_status()`, `caja_add_ticket_movimientos()`


<div class="mermaid">
graph TD
  %% Componentes principales
  LIQ["Componente: Módulo Liquidación"]
  CRM["Componente: CRM"]
  CEDIS["Componente: CEDIS"]
  CAJA["Componente: CAJA"]

  %% Relaciones estructurales
  LIQ -->|Consulta remisiones| CRM
  LIQ -->|Valida productos devueltos| CEDIS
  LIQ -->|Genera liquidación y remite a| CAJA

  %% Estilos
  classDef componente fill:#b3cde0,stroke:#333,stroke-width:2px,color:#000;
  class LIQ,CRM,CEDIS,CAJA componente;

</div>




### 5.2 Funciones de Integración


- `vta_gliq_suc_av_os_act_widget_view_x_ids`: Gestión inicial de liquidación
- `vta_gliq_suc_av_os_liq_envia_x_ids`: Envío de liquidación por correo
- `vta_gliq_suc_av_os_liq_imprime_x_ids`: Impresión de liquidación
- `vta_gliq_suc_av_os_act_liquida_ok_x_ids`: Confirmación de liquidación






## 6. Interacción Cliente-Servidor

Ver detalles del patrón de comunicación en [Interacción Cliente-Servidor](../global/interaccion_cliente_servidor.md).

## 7. Base de datos

### Tablas de Liquidación
- **liquidacion**: Almacena información de las liquidaciones.
- **add_orden_status_liquidacion**: Mantiene el estado de las órdenes en proceso de liquidación.

### Tablas de Ventas y Remisiones
- **inicia_ruta_stock_vendedor**: Gestiona las rutas y stock de los vendedores.
- **add_remision**: Almacena información de las remisiones.
- **add_remision_productos_orden**: Detalles de productos en remisiones.
- **add_remision_venta_neta**: Información de ventas netas.

### Tablas de Productos
- **add_productos**: Catálogo de productos.
- **add_ct_productos**: Categorías de productos.
- **add_mini_stock_vendedor**: Stock de productos por vendedor.

### Tablas de Clientes
- **add_clientes**: Información de clientes.
- **add_clientes_tipos**: Tipos de clientes.

### Tablas de Vendedores
- **add_cc_myr**: Información de vendedores.
- **add_comision_suc_meses**: Comisiones por mes.
- **add_comision_suc_av_prods_prom**: Promedios de comisiones por producto.

### Tablas de Tickets y Documentos
- **add_ticket_titulo**: Títulos de tickets.
- **add_ticket_detalle**: Detalles de tickets.

### Tablas de Configuración
- **add_sucursal**: Información de sucursales.
- **add_ano_nuevo**: Años de operación.
- **rel_ano_mes_nuevo**: Relación de años y meses.

### Tablas de Estado
- **add_remision_venta_neta**: Estado de ventas netas.
- **add_comision_producto**: Configuración de comisiones por producto.



## 8. Flujo de Proceso

<div class="mermaid">
graph TD
    A[Inicio] --> B[Seleccionar Sucursal]
    B --> C[Verificar Permisos]
    C -->|Sí| D[Mostrar Espacio de Trabajo]
    D --> E{Órdenes Pendientes?}
    E -->|Sí| F[Seleccionar Orden]
    F --> G[Validar Productos]
    G --> H[Validar Documentos]
    H --> I[Generar Liquidación]
    I --> J[Actualizar Estado]
    E -->|No| K[Mostrar Reportes]

   %% Estilos personalizados
    classDef process fill:#e1f5fe,stroke:#01579b,color:#000;
    classDef decision fill:#fff3e0,stroke:#e65100,color:#000;
    classDef startend fill:#c8e6c9,stroke:#2e7d32,color:#000;

    class A startend;
    class E decision;
    class B,C,D,F,G,H,I,J,K process;
</div>




