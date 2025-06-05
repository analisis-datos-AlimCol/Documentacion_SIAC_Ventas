# Ficha Técnica del Módulo de Caja

## 1. Propósito General

El módulo de Caja es un componente fundamental del sistema de ventas que gestiona todas las operaciones relacionadas con el manejo de efectivo y movimientos financieros en las sucursales. Proporciona una interfaz completa para la administración de recibos, cobranzas y liquidaciones.

## 2. Arquitectura Técnica

Este módulo implementa la arquitectura estándar del sistema SIAC 2.0 definida en [Arquitectura del Sistema](../global/arquitectura.md), incluyendo:

- Separación por capas (presentación, lógica de negocio, datos)
- Uso de AJAX con tokens para interacción dinámica
- Validaciones integradas de sesión, permisos y datos


## 3. Estructura de Archivos Clave

| Archivo                | Funcionalidad                    |
|------------------------|----------------------------------|
| [cont_g_caja.php](cci:7://file:///c:/Users/USER/Documents/Alinsa/DocumentacionTecnica/SIAC_Ventas_2.0_13_05_2025/ventas/cont_g_caja.php:0:0-0:0)      | Gestor principal de caja         |
| [cont_wspace.php](cci:7://file:///c:/Users/USER/Documents/Alinsa/DocumentacionTecnica/SIAC_Ventas_2.0_13_05_2025/ventas/cont_wspace.php:0:0-0:0)      | Espacio de trabajo               |
| `cont_forms.php`       | Formularios de caja             |
| `cont_ajax.js`         | AJAX para caja                  |
| `cont_graficas.php`    | Gráficos y reportes             |

## 4. Funcionalidades Principales



Recibo de ingresos adicionales:
    Implementado en el flujo de "Recibo de Ingresos"
    Incluye validación de datos y generación de movimientos
    Actualiza el estado y notifica automáticamente
Recibos de liquidación de venta:
    Maneja liquidaciones de ventas
    Integra con el módulo de ventas
    Genera movimientos financieros
    Actualiza estados y notifica
Recibos de cobranza:
    Gestiona cobranzas
    Integra con el módulo de clientes y crédito
    Genera movimientos y actualiza estados
    Incluye notificaciones automáticas
Recibo de establecimientos:
    Maneja ingresos de establecimientos
    Integra con el módulo de sucursales
    Genera movimientos y actualiza estados
Corte de caja:
    Permite realizar cortes de caja
    Genera reportes financieros
    Actualiza estados y notifica

generar recibos de liquidacion. 

se selecciona el mes y el agente de venta. luego se selecciona la orden a la cual se le generará su recibo. se agregan movimientos (pagos o tickets) hasta que el importe de la suma de los movimientos sea igual al importe de la orden en liquidacion. una vez agregados todos los movimientos es necesario relacionar los tickets generados con los documentos de venta o remisiones. Hasta que todos los documentos de venta tengan al menos un ticket de pago (movimiento) relacionado.

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

### 4.2 Recibos de Liquidación de Venta

Permite gestionar el proceso de liquidación de ventas a través de ordenes de salida, vinculando múltiples documentos de venta (remisiones) con un solo recibo.

**Características:**

- Gestión de ordenes de salida por vendedor
- Generación de movimientos (tickets)
- Validación de importes totales
- Relacionamiento de tickets con documentos de venta
- Notificaciones automáticas
- Gestión de estados y confirmaciones

Referencias técnicas:

- Lógica principal: `cont_ajax.js`
- Clase principal: `class_vtas.php`, 
- métodos:
    - `cont_rmv_liq_av_os_edo_gen_os_x_scrip`
    - `cont_up_liquidacion_edo_x_ids_scrip`
    - `cont_gcj_rbo_liquidacion`


Vistas: `cont_g_caja.php`, `cont_forms.php`
**Diagrama**
<div class="mermaid">

graph TD
    %% Nodos principales
    A[Inicio] --> B[Selección de Parámetros]

    B --> E[Generación de Movimientos o Tickets de pago]
    E --> E1{¿Monto de Movimientos = Monto Orden?}
    E1 --> |No|E
    E1 --> |Sí|F[Relación de Documentos y Movimientos]
    F --> G{¿Cada Documento Tiene Ticket Asociado?}
    G --> |Sí|H[Validación]
    G --> |No|F
    H --> I[Generar Notificación]
   
%% Estilos personalizados
    classDef process fill:#e1f5fe,stroke:#01579b,color:#000;
    classDef decision fill:#fff3e0,stroke:#e65100,color:#000;
    classDef startend fill:#c8e6c9,stroke:#2e7d32,color:#000;

    class A startend;
    class B,E,F,H,I process;
    class E1,G decision;


</div>

### 4.1 Gestión de Recibos

Permite el control completo de los diferentes tipos de recibos en el sistema de caja.

**Características:**
- Manejo de recibos de ingresos, liquidación y cobranza.
- Validación de datos y estados.
- Generación de movimientos.
- Notificaciones automáticas.

**Referencias técnicas:**
- **Lógica principal:** `cont_ajax.php`
- **Clase:** `class_cont.php`, métodos `cont_gcj_rbo_*`
- **Vistas:** `cont_g_caja.php`, `cont_forms.php`

---

### 4.2 Movimientos Financieros

Controla todos los movimientos de efectivo y otros medios de pago.

**Características:**
- Tipos de movimientos (efectivo, crédito, descuentos).
- Validación de montos.
- Actualización de estados.
- Historial de movimientos.

**Referencias técnicas:**
- **Lógica:** `cont_ajax.php`
- **Clase:** `class_cont.php`, métodos `cont_up_*`
- **Formularios:** `cont_forms.php`

---

### 4.3 Sistema de Notificaciones

Gestiona todas las notificaciones relacionadas con la caja.

**Características:**
- Notificaciones de tickets de venta.
- Complementos de pago.


**Referencias técnicas:**
- **Lógica:** `cont_ajax.php`
- **Clase:** `class_mails.php`
- **Vistas:** `cont_widgets1.php`

---

### 4.4 Reportes y Análisis

Generación de reportes y análisis financieros.

**Características:**
- Reportes de ingresos.
- Estado de caja.


**Referencias técnicas:**
- **Lógica:** `cont_ajax.php`
- **Clase:** `class_cont.php`, métodos `cont_view_*`
- **Vistas:** `cont_graficas.php`

---


## 5. Integraciones

### 5.1 Módulos Internos

#### Módulo de Ventas
Integración con el módulo de ventas para liquidaciones y cobranzas.

- **Características:** Validación de ventas, sincronización de estados.
- **Referencia:** `cont_ajax.php`, líneas relacionadas con liquidaciones.

#### Módulo de CFDI
Integración con el módulo de facturación electrónica.

- **Características:** Generación de CFDI, complementos de pago.
- **Referencia:** `cont_ajax.php`, líneas relacionadas con CFDI.

#### Módulo de Auditoría
Integración con el sistema de auditoría.

- **Características:** Registro de operaciones, seguimiento.
- **Referencia:** `cont_ajax.php`, líneas relacionadas con auditoría.

#### Módulo de Usuarios
Integración con el sistema de usuarios y permisos.

- **Características:** Control de acceso, permisos por sucursal.
- **Referencia:** `cont_ajax.php`, líneas relacionadas con validación.

## 6. Cliente - Servidor


Para detalles sobre el patrón de comunicación cliente-servidor utilizado en este proceso, consulta la sección [Interacción Cliente-Servidor](../global/interaccion_cliente_servidor.md).

## 7. Base de datos
### Tablas de Recibos
- **add_no_recibo_print**: Manejo de recibos.
- **lista_recibos_x_cancelar**: Recibos pendientes de cancelación.
- **add_pagos_noor_rem**: Pagos no relacionados con remisiones.

### Tablas de Liquidación
- **liquidacion**: Información de liquidaciones.
- **add_remision**: Remisiones relacionadas con caja.
- **add_remision_venta_neta**: Ventas netas.


### Tablas de Stock
- **add_stock_ajuste**: Ajustes de stock.
- **add_ct_productos**: Categorías de productos.

### Tablas de Clientes y Crédito
- **add_clientes**: Información de clientes.
- **add_credito_clientes**: Crédito de clientes.


### Tablas de Sucursales
- **add_sucursal**: Información de sucursales.
- **add_rutas**: Rutas de distribución.

### Tablas de CFDI
- **add_cfdi_cpago**: Complementos de pago.
- **add_cfdi_cpago_info**: Información de CFDI.
- **add_cfdi_cpago_cancel**: Cancelaciones de CFDI.

Tablas clave:

add_orden_status_liquidacion: Controla estados de ordenes



## 8. Diagrama de flujo del módulo
<div class="mermaid">
graph TD
    %% Nodos principales
    A[Inicio] --> B[Verificación de Sesión]
    B --> C[Validación de Permisos]
    C --> D[Gestor de Caja]
    
    %% Gestor de Caja
    D --> E[Menú Principal]
    E --> F[Recibo de Ingresos]
    E --> G[Recibo de Liquidación]
    E --> H[Recibo de Cobranza]
    E --> I[Recibo de Establecimientos]
    E --> J[Corte de Caja]
    
    %% Flujo de Recibo de Ingresos
    F --> K[Crear Recibo]
    K --> L[Validar Datos]
    L --> M[Guardar Recibo]
    M --> N[Generar Movimientos]
    N --> O[Actualizar Estado]
    O --> P[Notificar]
    
    %% Flujo de Recibo de Liquidación
    G --> Q[Crear Recibo]
    Q --> R[Validar Datos]
    R --> S[Guardar Recibo]
    S --> T[Generar Movimientos]
    T --> U[Actualizar Estado]
    U --> V[Notificar]
    
    %% Flujo de Recibo de Cobranza
    H --> W[Crear Recibo]
    W --> X[Validar Datos]
    X --> Y[Guardar Recibo]
    Y --> Z[Generar Movimientos]
    Z --> AA[Actualizar Estado]
    AA --> AB[Notificar]
    
    %% Flujo de Recibo de Establecimientos
    I --> AC[Crear Recibo]
    AC --> AD[Validar Datos]
    AD --> AE[Guardar Recibo]
    AE --> AF[Generar Movimientos]
    AF --> AG[Actualizar Estado]
    AG --> AH[Notificar]
    
    %% Flujo de Corte de Caja
    J --> AI[Generar Reporte]
    AI --> AJ[Validar Datos]
    AJ --> AK[Guardar Corte]
    AK --> AL[Actualizar Estado]
    AL --> AM[Notificar]
    
    %% Subprocesos comunes
    subgraph "Proceso de Validación"
    L --> L1[Validar Usuario]
    L --> L2[Validar Datos]
    L --> L3[Validar Estado]
    end
    
    subgraph "Proceso de Notificación"
    P --> P1[Enviar Email]
    P --> P2[Actualizar Estado]
    P --> P3[Generar Reporte]
    end

    %% Estilos homogéneos
    classDef startend fill:#c8e6c9,stroke:#2e7d32,color:#000;
    classDef process fill:#e1f5fe,stroke:#01579b,color:#000;
    classDef decision fill:#fff3e0,stroke:#e65100,color:#000;
    classDef subprocess fill:#d1c4e9,stroke:#512da8,color:#000;

    %% Asignación de estilos
    class A startend;
    class B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z,AA,AB,AC,AD,AE,AF,AG,AH,AI,AJ,AK,AL,AM process;
    class L1,L2,L3,P1,P2,P3 subprocess;
</div>

