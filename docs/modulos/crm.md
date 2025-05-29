# Ficha Técnica Unificada del Módulo CRM - SIAC 2.0 Ventas

## 1. Propósito General

El módulo CRM (Customer Relationship Management) gestiona la información completa de clientes, incluyendo:

Este módulo permite administrar de manera integral toda la información relacionada con los clientes de la empresa, desde sus datos básicos hasta su historial de ventas y preferencias.

Funciones principales:

- Gestión completa de información de clientes
- Asignación de agentes de ventas
- Gestión de rutas de visita
- Control de visitas y frecuencias
- Gestión de datos fiscales
- Manejo de contactos
- Historial de ventas
- Gestión de crédito
- Sincronización con otros módulos del sistema

**Ubicación:** `ventas/`  
**Parte del sistema:** `SIAC_2_0_Ventas`


## 2. Arquitectura Técnica

Este módulo implementa la arquitectura estándar del sistema SIAC 2.0 definida en [Arquitectura del Sistema](../global/arquitectura.md), incluyendo:

- Separación por capas (presentación, lógica de negocio, datos)
- Uso de AJAX con tokens para interacción dinámica
- Validaciones integradas de sesión, permisos y datos


## 3. Estructura de Archivos Clave

| Archivos                          | Funcionalidad                                               |
|----------------------------------|-------------------------------------------------------------|
| `crm_ajax.php`                   | Puente AJAX entre frontend y backend, validación.           |
| `crm_forms.php`                  | Formularios para alta/editar cliente, datos fiscales, etc.  |
| `crm_tablas.php`                 | Renderización de tablas HTML.                               |
| `crm_widgets.php`                | Visualización de KPIs y estadísticas.                       |
| `crm_modals.php`                 | Ventanas emergentes.                                        |
| `crm_select.php`                 | Carga de datos en selects dinámicos.                        |
| `crm_select2.php`                | Select2 para búsquedas avanzadas.                           |
| `crm_g_clientes.php`             | Vista principal de gestión de clientes.                     |
| `crm_g_mtz_clientes.php`         | Gestión de clientes por sucursal.                           |
| `crm_g_rutas.php`                | Gestión de rutas de visita.                                 |
| `crm_g_r_vtaav.php`              | Reportes de ventas por agente.                              |
| `crm_g_r_vtaclie.php`            | Reportes de ventas por cliente.                             |
| `crm_g_r_vtaprod.php`            | Reportes de ventas por producto.                            |
| `crm_g_r_vtawork.php`            | Reportes de trabajo de visitas.                             |
| `crm_ajax.js`                    | Eventos y validaciones principales.                         |
| `crm_ajax_1.js`                  | Eventos adicionales y funciones auxiliares.                 |
| `crm_av_ajax.js`                 | Funciones de validación avanzada.                           |
| `crm_forms.php`| Formularios y vistas.|
| `crm_tablas.php`| Generación de listados.|
| `crm_widgets.php`| Componentes interactivos.|
| `crm_select.php`, `crm_select2.php`| Selectores dinámicos.|

## 4. Funcionalidades Principales

### 4.1 Gestión de Clientes

Permite el control integral de la información de clientes dentro del sistema. La funcionalidad incluye:

**Características:**

- Alta, edición y baja de clientes
- Asignación de agentes de ventas
- Asignación de rutas de visita
- Clasificación de clientes por tipo
- Gestión de datos fiscales
- Control de visitas y frecuencia
- Historial de ventas
- Gestión de crédito
- Visualización en mapas geográficos
- Sistema de copia de clientes
- Exportación de datos a PDF y Excel
- Gestión de contactos múltiples por cliente
- Sistema de notificaciones y correos electrónicos

**Referencias técnicas:**

- Lógica principal: `crm_ajax.php` (Líneas 177–211)
- Clase: `class_crm.php`, método `get_movimientos()`
- Vista: `crm_g_clientes.php`, `crm_widgets.php`
- Exportación: `export/xls_crm_rutas.php`, `export/xls_crm_suc_clies.php`
- Mapas: `modals/crm_cliente_maps.php`, `modals/crm_ruta_clies_maps.php`

---

### 4.2 Datos Fiscales

Gestión completa de la información fiscal de los clientes, incluyendo:

**Características:**

- RFC y razón social
- Tipo de persona
- Código de uso
- Nombre de uso
- Dirección fiscal completa
- Código postal
- Municipio
- Estado
- País

**Referencias técnicas:**

- Lógica: `crm_ajax.php` (Líneas 100–141)
- Vistas: `crm_g_clientes.php`
- Clase: `class_crm.php`, método `crm_add_gclie_datos_fiscales()`

---

### 4.3 Gestión de Crédito

Control de límites y condiciones crediticias de los clientes.

**Características:**

- Límite de crédito
- Tipo de crédito
- Condiciones de pago
- Estado de crédito
- Historial de aprobaciones

**Referencias técnicas:**

- Lógica: `crm_ajax.php` (Líneas 350–384)
- Formularios: `crm_forms.php`
- Clase: `class_crm.php`, funciones `crm_add_gclie_credito()`

---

### 4.4 Gestión de Contactos

Administración de contactos asociados a cada cliente.

**Características:**

- Contacto principal
- Contacto de compras
- Contacto de pagos
- Contacto de ventas
- Información de contacto (teléfono, email, WhatsApp)

**Referencias técnicas:**

- Lógica: `crm_ajax.php` (Líneas 470–506)
- Clase: `class_crm.php`, funciones `crm_add_gclie_contactos()`

---

### 4.5 Gestión de Visitas

Control de las visitas a clientes.

**Características:**

- Programación de visitas
- Frecuencia de visita
- Rutas de visita
- Historial de visitas
- Agentes asignados

**Referencias técnicas:**

- Lógica: `crm_ajax.php` (Líneas 528–553)
- Clase: `class_crm.php`, funciones `crm_add_gclie_visitas()`

---

### 4.6 Reportes y Estadísticas

Generación de reportes y estadísticas sobre clientes.

**Referencias técnicas:**

- Métodos: `get_movimientos()`, `get_estadisticas()` en `class_crm.php`
- Visualización: `crm_graficas.php`, `crm_widgets.php`
- Exportación: `crm_export.php`

---

## 5. Integraciones

### 5.1 Módulos Internos

#### Módulo de Ventas

Permite validar existencia de clientes al momento de realizar ventas y sincronizar los movimientos de crédito.

- **Características:** Validación de cliente en tiempo real, sincronización de ventas
- **Referencia:** `crm_ajax.php`, líneas 312–349

#### Módulo de Contabilidad

Ajustes contables automáticos según los movimientos de crédito y ventas.

- **Características:** Actualización automática de estados financieros
- **Referencia:** `crm_ajax.php`, líneas 283–296

#### Módulo de Inventario

Sincronización de información de productos y precios.

- **Características:** Actualización automática de información de productos
- **Referencia:** `crm_ajax.php`, líneas 400–420

### 5.2 Servicios Externos

- Mapas: Integración para mostrar la geolocalización de clientes.
- Correo Electrónico: Envío y administración de emails asociados a contactos.
- Exportación: Generación de archivos Excel y PDF.



## 6. Interacción Cliente-Servidor

Para una descripción completa del flujo de datos y el manejo de tokens, consulta la sección [Interacción Cliente-Servidor](../global/interaccion_cliente_servidor.md).


## 7. Base de Datos

### 7.1 Tablas Principales

1. **add_clientes**


2. **add_clientes_tipos**


3. **add_clientes_cred_check**


4. **add_datos_facturas_clientes**


### 7.2 Tablas de Relación

1. **add_rutas**


2. **add_sucursal**


### 7.3 Tablas de Configuración

1. **add_ano_nuevo**


2. **add_cfdi_reg_fiscal**


### 7.4 Tablas de Contacto

1. **add_emails_clientes**

2. **add_clientes_maps**



## 8. Diagrama de Flujo del Módulo CRM

 <div class="mermaid">
graph TD
    A[Inicio] --> B[Autenticación]
    B --> C{Menú Principal CRM}

    %% Gestión de Clientes
    C --> |Gestión de Clientes| D[Crear/Editar Cliente]
    D --> E[Validar Datos]
    E --> F{¿Datos Válidos?}
    F --> |Sí| G[Guardar Cliente]
    F --> |No| H[Mostrar Errores]
    G --> I[Actualizar Listado]

    %% Gestión de Datos Fiscales
    C --> |Datos Fiscales| J[Crear/Editar Datos]
    J --> K[Validar RFC]
    K --> L{¿RFC Válido?}
    L --> |Sí| M[Guardar Datos]
    L --> |No| N[Mostrar Errores]

    %% Gestión de Crédito
    C --> |Crédito| O[Crear/Editar Crédito]
    O --> P[Validar Límite]
    P --> Q{¿Límite Aprobado?}
    Q --> |Sí| R[Guardar Crédito]
    Q --> |No| S[Enviar a Aprobación]

    %% Gestión de Contactos
    C --> |Contactos| T[Crear/Editar Contacto]
    T --> U[Validar Email]
    U --> V{¿Email Válido?}
    V --> |Sí| W[Guardar Contacto]
    V --> |No| X[Mostrar Errores]

    %% Reportes
    C --> |Reportes| Y[Seleccionar Tipo]
    Y --> Z[Generar Reporte]
    Z --> AA[Exportar/Imprimir]

    %% Estilos personalizados
    classDef process fill:#e1f5fe,stroke:#01579b,color:#000;
    classDef decision fill:#fff3e0,stroke:#e65100,color:#000;
    classDef startend fill:#c8e6c9,stroke:#2e7d32,color:#000;
    classDef error fill:#ffebee,stroke:#c62828,color:#b71c1c;

    class A,AA startend;
    class F,L,Q,V decision;
    class H,N,X error;
    class B,C,D,E,G,I,J,K,M,O,P,R,S,T,U,W,Y,Z process;
</div>


