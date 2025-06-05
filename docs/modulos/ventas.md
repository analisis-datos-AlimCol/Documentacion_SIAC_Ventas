# Ficha Técnica del Módulo Ventas

## 1. Propósito General

El módulo **Ventas** es el componente central del sistema **SIAC Ventas 2.0**, diseñado para gestionar todas las operaciones relacionadas con la venta de productos, desde la toma de pedidos hasta la facturación y el seguimiento de ventas. Proporciona herramientas para la gestión de clientes, productos, pedidos, precios, facturación y análisis de ventas.

**Referencias:**

- `ventas_ajax.php` (Línea 1): Sistema de ventas integrado  
- Archivos principales: `ventas_forms.php`, `ventas_tablas.php`, `ventas_widgets.php`

---

## 2. Arquitectura General

Este módulo implementa la arquitectura estándar del sistema SIAC 2.0 definida en [Arquitectura del Sistema](../global/arquitectura.md), incluyendo:

- Separación por capas (presentación, lógica de negocio, datos)
- Uso de AJAX con tokens para interacción dinámica
- Validaciones integradas de sesión, permisos y datos

## 3. Estructura de Archivos Clave

### 3.1 Archivos PHP

| Archivo              | Funcionalidad                        |
|----------------------|--------------------------------------|
| `vta_ajax.php`       | Controlador principal de operaciones |
| `vta_forms.php`      | Formularios de ventas                |
| `vta_tablas.php`     | Tablas de datos                      |
| `vta_widgets.php`    | Componentes visuales                 |
| `vta_modals.php`     | Ventanas modales                     |
| `class_vtas.php`     | Lógica de negocio                    |
| `vta_select2.php`    | Selectores mejorados                 |
| `vta_graficas.php`   | Gráficos y estadísticas              |
| `class_precio.php`   | Gestión de precios                   |
| `class_factura.php`  | Facturación electrónica              |
| `vta_dtos_promos.php`| Sistema de descuentos y promociones  |
| `vta_g_comisiones.php`| Gestión de comisiones               |
| `vta_g_liquidacion.php`| Liquidación de ventas              |
| `vta_g_precios.php`  | Gestión de precios local/foráneo     |
| `vta_g_osalida.php`  | Gestión de órdenes de salida         |

### 3.2 Archivos JavaScript

| Archivo              | Funcionalidad                        |
|----------------------|--------------------------------------|
| `vta_ajax.js`        | Eventos y validaciones               |
| `vta_dtos_promos.js` | Gestión de descuentos                |
| `vta_graficas.js`    | Generación de gráficos              |
| `vta_precios.js`     | Gestión de precios dinámicos         |
| `vta_liquidacion.js` | Cálculos de liquidación             |
| `vta_comisiones.js`  | Cálculos de comisiones              |
| `vta_validaciones.js`| Validaciones de formularios         |
| `vta_select2.js`     | Configuración de select2            |
| `vta_tablas.js`      | Configuración de tablas             |
| `vta_modal.js`       | Manejo de ventanas modales          |
| `vta_forms.js`       | Eventos de formularios              |
| `vta_utils.js`       | Funciones utilitarias               |


**Clases Principales**

- [c_View_pv (Vista Punto de Venta)](../phpdoc/classc___view__pv.html)
- [c_Add_pv (Añadir Punto de Venta)](../phpdoc/classc___add__pv.html)
- [c_Up_pv (Actualizar Punto de Venta)](../phpdoc/classc___up__pv.html)
- [c_Rmv_pv (Eliminar Punto de Venta)](../phpdoc/classc___rmv__pv.html)
- [c_Fun_pv (Funciones Punto de Venta)](../phpdoc/classc___funs__pv.html)
- [c_Msj_pv (Mensajes Punto de Venta)](../phpdoc/classc___msj__pv.html)
- [c_View_vm (Vista Venta de Mostrador)](../phpdoc/classc___view__vm.html)
- [c_Add_vm (Añadir Venta de Mostrador)](../phpdoc/classc___add__vm.html)
- [c_Up_vm (Actualizar Venta de Mostrador)](../phpdoc/classc___up__vm.html)
- [c_Rmv_vm (Eliminar Venta de Mostrador)](../phpdoc/classc___rmv__vm.html)
- [c_Fun_vm (Funciones Venta de Mostrador)](../phpdoc/classc___fun__vm.html)



---

## 4. Funcionalidades Principales

### 4.1 Portal de Agente de Ventas

- Registro de pedidos de clientes  
- Pedidos a CEDIS (integración con módulo CEDIS)  
- Seguimiento de ventas  
- Generación de CFDI (factura electrónica)  
- Gestión de comisiones y liquidaciones
- Sistema de descuentos y promociones

**Referencias:**  

- `vta_forms.php`, tokens 100–107  
- `class_cds.php`, tokens 200–205  
- `class_vtas.php`, tokens 300–305  
- `class_factura.php`, tokens 400–405


### 4.3 Gestor de Precios

- Precios locales, foráneos y especiales  
- Precios globales  
- Actualización masiva de precios  

**Referencias:**  
- `class_precio.php`, tokens 600–620  
- `ventas_ajax.php`, tokens 621–625

---

### 4.4 Gestión de Pedidos

- Creación y edición de pedidos  
- Asignación de productos  
- Cálculo automático de totales  

**Referencia:** `ventas_forms.php`, tokens 100–107

---

### 4.5 Facturación

- Generación de facturas  
- Integración con CFDI  
- Impresión de documentos  

**Referencia:** `class_cfdi.php`, tokens 200–205

---

### 4.6 Análisis de Ventas

- Reportes de ventas  
- Gráficos de tendencias  
- Análisis por producto o cliente  

**Referencia:** `ventas_graficas.php`, tokens 300–305

---

## 5. Integraciones

### 5.1 Módulos Internos

- **CRM:** Integración para gestión de clientes  
  *Referencia:* `class_crm.php`, token 400

- **Contabilidad:** Registro fiscal de ventas  
  *Referencia:* `class_cont.php`, token 500

- **CEDIS:** Manejo de pedidos y salidas  
  *Referencia:* `class_cds.php`, tokens 200–205

### 5.2 Servicios Externos

- **API de Facturación:** Generación y timbrado de CFDI  
  *Referencia:* `class_cfdi.php`, líneas 100–150

- **Servicios de Correo:** Envío automático de facturas  
  *Referencia:* `class_mails.php`, líneas 200–250

---

### 5.2 Proceso de Creación de Documentos

#### 5.2.1 Selección de Cliente y Ruta
El proceso inicia con la selección del cliente y ruta en CRM:
- **Características**
  - Selección de ruta y cliente
  - Validación de información del cliente
  - Consulta de historial de ventas
  - Generación de reportes de clientes

- **Referencias técnicas**
  - Tablas: `add_clientes`, `add_cc_myr`
  - Clase: `class_crm.php`, métodos `crm_add_clientes()`, `crm_add_cc_myr()`
  - Funciones: `crm_add_clientes_tipos()`, `crm_add_clientes_status()`

#### 5.2.2 Validación de Stock
El sistema verifica la disponibilidad de productos en CEDIS:
- **Características**
  - Validación de stock disponible
  - Consulta de ubicaciones
  - Reserva de productos
  - Generación de reportes de inventario

- **Referencias técnicas**
  - Tablas: `inicia_ruta_stock_vendedor`, `add_mini_stock_vendedor`
  - Clase: `class_cds.php`, métodos `cds_add_gos_cedis_osalida()`, `cds_add_gos_cedis_os_depa()`
  - Funciones: `cds_add_gos_cedis_av_os_prod_dev()`, `cds_add_gos_cedis_os_tit_reg()`

#### 5.2.3 Gestión de Pagos y Facturación
El proceso finaliza con la gestión de pagos y facturación:
- **Características**
  - Validación de condiciones de pago
  - Gestión de descuentos
  - Generación de facturas CFDI
  - Emisión de remisiones

- **Referencias técnicas**
  - Tablas: `add_remision`, `add_remision_productos_orden`
  - Clase: `class_factura.php`, métodos `fact_add_remision()`, `fact_add_remision_productos()`
  - Funciones: `fact_add_remision_venta_neta()`, `fact_add_remision_status()`

<div class="mermaid">
flowchart TD
  LIQ["Módulo Liquidación"]

  subgraph Proceso_5_2["Proceso 5.2: Creación de Documentos (Remisiones)"]
    LIQ_SEL_CLIENTE[" Selección Cliente y Ruta"]
    LIQ_VALID_STOCK[" Agregar productos"]
    LIQ_GEST_PAGO_FACT[" Gestión de Pago y Facturación"]

    LIQ --> LIQ_SEL_CLIENTE
    LIQ_SEL_CLIENTE --> LIQ_VALID_STOCK
    LIQ_VALID_STOCK --> LIQ_GEST_PAGO_FACT
  end

  %% Módulos relacionados
  CRM["CRM"]
  CEDIS["CEDIS"]
  FACT["Facturación"]

  %% Conexiones de pasos con módulos
  LIQ_SEL_CLIENTE --> |Consulta|CRM
  LIQ_VALID_STOCK --> |Validado por|CEDIS
  LIQ_GEST_PAGO_FACT --> |De acuerdo a|CRM
  LIQ_GEST_PAGO_FACT --> |Gestionado por|FACT

  %% Estilos
  classDef modulo fill:#bbf,stroke:#333,stroke-width:2px;
  classDef paso fill:#dfd,stroke:#333,stroke-width:2px;
  class LIQ,CRM,CEDIS,FACT modulo;
  class LIQ_SEL_CLIENTE,LIQ_VALID_STOCK,LIQ_GEST_PAGO_FACT paso;
</div>

<div class="mermaid">
graph TD
  %% Componentes principales
  LIQ["Componente: Módulo Liquidación"]
  CRM["Componente: CRM"]
  CEDIS["Componente: CEDIS"]
  FACT["Componente: Facturación"]

  %% Interfaces/servicios que utiliza el módulo Liquidación
  LIQ -->|Consulta Cliente y Ruta| CRM
  LIQ -->|Validación de Stock| CEDIS
  LIQ -->|Consulta condiciones de pago| CRM
  LIQ -->|Gestión de Pago y Factura| FACT

  %% Estilos
  classDef componente fill:#b3cde0,stroke:#333,stroke-width:2px,color:#000;
  class LIQ,CRM,CEDIS,FACT componente;
</div>

## 6. Interacción Cliente-Servidor

Para una explicación completa del modelo de comunicación y procesamiento de tokens, consulta la sección [Interacción Cliente-Servidor](../global/interaccion_cliente_servidor.md).

---

## 7. Base de Datos

### Tablas Clave

**Tablas de Productos y Stock:**

- add_productos
- add_ct_productos
- add_stock_ajuste
- add_mini_stock_vendedor
- add_mini_stock_vendedor_temp

**Tablas de Entradas y Salidas:**

- add_tit_entradas_stock
- add_entrada_producto_stock
- add_os_pa_titulo
- add_os_pa_productos
- add_os_pa_producto_dev

**Tablas de Precios y Descuentos:**
- ajuste_precio_pr
- add_descuento_prom_prod_his
- add_comision_producto

**Tablas de Empleados y Usuarios:**

- add_empleados
- add_user
- rel_em_suc_empleado

**Tablas de Sucursales y Departamentos:**
- add_sucursal
- add_depas

**Tablas de Año y Configuración:**

-add_ano_nuevo

**Tablas de Pedidos y Ventas:**

- prodts_pedido_stock_temp
- add_cedis_os_prod_cont

**Tablas de Backup:**

- add_backup_stock_almacen


---

## 8. Diagrama de Flujo del Módulo

<div class="mermaid">
graph TD
    A[Inicio Ventas] --> B[Verificar Sesión]
    B --> C{¿Usuario Autenticado?}
    C --> |Sí| D[Seleccionar Función]

    %% Portal de Agente
    D --> E{¿Portal de Agente?}
    E --> |Sí| F[Registrar Pedido]
    F --> G[Validar Pedido]
    G --> H[Enviar a CEDIS]
    H --> I[Generar Factura]
    I --> J[Integrar CFDI]
    J --> K[Enviar Factura]

    %% Gestión de Precios
    D --> L{¿Gestión de Precios?}
    L --> |Sí| M[Actualizar Precios]
    M --> N[Validar Precios]
    N --> O[Guardar Precios]

    %% Liquidación
    D --> P{¿Liquidación?}
    P --> |Sí| Q[Calcular Comisión]
    Q --> R[Generar Reporte]
    R --> S[Registrar Liquidación]

    %% Estilos personalizados
    classDef process fill:#e1f5fe,stroke:#01579b,color:#000;
    classDef decision fill:#fff3e0,stroke:#e65100,color:#000;
    classDef startend fill:#c8e6c9,stroke:#2e7d32,color:#000;

    class A startend;
    class C,E,L,P decision;
    class B,D,F,G,H,I,J,K,M,N,O,Q,R,S process;
</div>


