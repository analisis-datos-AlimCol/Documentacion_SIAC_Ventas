
# Ficha Técnica del Módulo Facturación Electrónica (CFDI)

## 1. Propósito General

El módulo **Facturación Electrónica (CFDI)** es un componente crítico del sistema **SIAC Ventas 2.0**, diseñado para la generación, validación y manejo de facturas electrónicas (CFDI) según las normativas del SAT. Proporciona una interfaz segura y eficiente para la creación, timbrado y almacenamiento de facturas electrónicas.

**Referencia:**

- `clases/class_cfdi.php` (Línea 1): Sistema de facturación electrónica  
- Archivos principales: `cont_g_cfdi.php`, `pv_g_cfdi.php`, `rp_g_suc_cfdi.php`

---

## 2. Arquitectura Técnica

Este módulo implementa la arquitectura estándar del sistema SIAC 2.0 definida en [Arquitectura del Sistema](../global/arquitectura.md), incluyendo:

- Separación por capas (presentación, lógica de negocio, datos)
- Uso de AJAX con tokens para interacción dinámica
- Validaciones integradas de sesión, permisos y datos

---

## 3. Estructura de Archivos Clave

| Archivo                | Funcionalidad                    |
|------------------------|----------------------------------|
| `clases/class_cfdi.php`| Lógica principal de CFDI         |
| `cont_g_cfdi.php`      | Generación de CFDI               |
| `pv_g_cfdi.php`        | Facturación punto de venta       |
| `rp_g_suc_cfdi.php`    | Reportes por sucursal            |
| `view_cfdi_cpago.php`  | Visualización de pagos           |
| `view_cfdi_doc_vta.php`| Documentos de venta              |
| `view_cfdi_fg_doc.php` | Documentos financieros           |
| `view_cfdi_ticket.php` | Tickets electrónicos             |
| `cont_ajax.js`| Generación de facturas |
| `ajax_send_txt_info.js`|  Envío de información TXT | 


**Clases Principales**

- [Facturación Electrónica](../phpdoc/class_facturacion_moderna.html)
- [c_View_cont (Vista Contabilidad)](../phpdoc/classc___view__cont.html)
- [c_Add_cont (Añadir Facturas)](../phpdoc/classc___add__cont.html)
- [c_Up_cont (Actualizar Facturas)](../phpdoc/classc___up__cont.html)
- [c_Rmv_cont (Eliminar Facturas)](../phpdoc/classc___rmv__cont.html)
- [c_Fun_cont (Funciones Contabilidad)](../phpdoc/classc___fun__cont.html)
- [c_Msj_cont (Mensajes Contabilidad)](../phpdoc/classc___msj__cont.html)

## 4. Funcionalidades Principales

### 4.1 Generación de CFDI

- Creación de facturas electrónicas  
- Integración con PAC  
- Generación de UUID  

**Referencia:** `class_cfdi.php`, tokens 100–107

### 4.2 Timbrado

- Validación de datos  
- Generación de XML  
- Creación de CBB  

**Referencia:** `class_cfdi.php`, tokens 200–205

### 4.3 Generación de Documentos

- PDFs de facturas  
- Tickets electrónicos  

**Referencia:** `view_cfdi_*.php`, tokens 300–305

### 4.4 Validación

- Verificación de PAC  
- Validación de UUID  

**Referencia:** `class_cfdi.php`, tokens 400–405

### 4.5 Facturación por ticket:

- Implementada en cfdi_gcfdi_cpago_cli_crea_cfdi
- Genera CFDI para pagos individuales
- Maneja timbrado y generación de documentos

### 4.6 Facturación Multi-Docs:

- Implementada en cfdi_mdocs_vta_docs_crea_factura
- Procesa múltiples documentos en una sola factura
- Actualiza estados individuales por documento


### 4.7 Complementos de pago:

- Implementada en cfdi_cpago_cancela_uuid
- Maneja pagos y su relación con CFDIs
- Actualiza estados de pagos y relaciona con facturas



---

## 5. Integraciones

### 5.1 Módulos Internos

- **Ventas:** `pv_g_cfdi.php`, token 500  
- **Contabilidad:** `cont_g_cfdi.php`, token 505

### 5.2 Servicios Externos

- **Facturación Moderna (PAC):** `class_cfdi.php`, líneas 100–150

---


## 6. Interacción Cliente-Servidor

Para detalles sobre el patrón de comunicación cliente-servidor utilizado en este proceso, consulta la sección [Interacción Cliente-Servidor](../global/interaccion_cliente_servidor.md).




## 7. Base de Datos

### Tablas Clave

| Tabla       | Propósito               |
|-------------|--------------------------|
| `cfdi`      | Registro de CFDI         |
| `cfdi_rel`  | Relaciones de CFDI       |
| `pac`       | Configuración PAC        |
| `docs_cfdi` | Documentos               |

**Relaciones:**

- Llaves primarias: `idcfdi`, `uuid`  
- Llaves foráneas: `idpac`, `iddoc`  
- Relaciones: `cfdi` → `docs_cfdi`

---


## 8. Diagrama de Flujo del Módulo

<div class="mermaid">
graph TD
    A[Inicio Facturación Electrónica] --> B{Validar Sesión}
    B -->|Sí| C[Verificar Archivo TXT]
    C -->|Sí| D{Validar PAC}
    D -->|Sí| E[Crear XML]
    E --> F[Timbrar con PAC]
    F -->|Sí| G[Guardar Documentos]
    G --> H[Actualizar Estados]
    H --> I[Completar]
    
    F -->|No| J[Error: Timbrado]
    J --> K[Notificar Error]
    
    D -->|No| L[Error: Sin PAC]
    C -->|No| M[Error: TXT No Existe]
    
    I --> N{Necesita Cancelación?}
    N -->|Sí| O[Cancelar CFDI]
    O --> P{Motivo}
    P -->|01| Q[Generar Sustitución]
    P -->|02/03| R[Cancelar Directo]
    Q --> S[Actualizar Estado]
    R --> S
    S --> T[Completar Cancelación]

    %% Estilos
    classDef process fill:#e1f5fe,stroke:#01579b,color:#000
    classDef decision fill:#fff3e0,stroke:#e65100,color:#000
    classDef startend fill:#c8e6c9,stroke:#2e7d32,color:#000
    classDef error fill:#ffebee,stroke:#d32f2f,color:#000

    %% Clases
    class A startend
    class B,D,N,P decision
    class C,E,F,G,H,I,O,Q,R,S,T process
    class J,K,L,M error

</div> 


