# Arquitectura del Sistema SIAC 2.0

Este documento describe la arquitectura del sistema SIAC 2.0, una solución empresarial modular desarrollada principalmente en PHP. Está diseñada bajo principios de escalabilidad, separación de responsabilidades y facilidad de mantenimiento.

---

## 1. Visión General


El desarrollo del backend se realizó sin el uso de frameworks PHP, utilizando PHP nativo con una arquitectura personalizada basada en el patrón MVC.

---

## 2. Arquitectura en Capas
<div class="mermaid">
graph TB
  subgraph CapaPresentacion["Capa de Presentación"]
    UI[Interfaz de Usuario]
    UI -->|Formularios| F[Forms]
    UI -->|Widgets| W[Widgets]
    UI -->|Tablas| T[Tablas]
    UI -->|Modales| M[Modals]
    UI -->|Workspaces| WS[Workspaces]
    UI -->|Scripts AJAX| S[Scripts]
  end

  subgraph TB CapaNegocio["Capa de Especificaciones del Negocio"]
    subgraph ModulosPrincipales["Módulos Principales"]
      CEDIS[CEDIS - Inventario]
      CRM[CRM - Clientes]
      VENTAS[Ventas]
      FACT[Facturación]
      LIQ[Liquidación]
      CAJA[Caja]
      REP[Reportes]
      CONF[Configuración]
    end
    
    subgraph Clases["Clases"]
      CLASSES[Clases PHP]
      CLASSES -->|Controladores| CTRL[Controladores]
      CLASSES -->|Modelos| MDL[Modelos]
      CLASSES -->|Vistas| VIEWS_CLASES[Views]
    end
  end

  subgraph TB CapaBD["Capa de Base de Datos"]
    DB[MySQL]
    DB -->|Tablas Principales| TABLAS[Tablas]
    DB -->|Procedimientos| SP[Procedimientos]
    DB -->|Vistas| VIEWS_DB[Vistas]
    DB -->|Indices| IDX[Indices]
  end

  %% Conexiones entre capas
  UI -->|Interactúa con| ModulosPrincipales
  ModulosPrincipales -->|Utiliza| Clases
  Clases -->|Accede a| DB
  DB -->|Almacena| ModulosPrincipales

  %% Conexiones entre componentes
  CEDIS -->|Integra con| VENTAS
  CRM -->|Integra con| VENTAS
  VENTAS -->|Integra con| FACT
  CAJA -->|Integra con| LIQ
  REP -->|Depende de| ModulosPrincipales
  CONF -->|Configura| ModulosPrincipales

  %% Estilos
  classDef capa fill:#f9f,stroke:#333,stroke-width:2px;
  classDef modulo fill:#bbf,stroke:#333,stroke-width:2px;
  classDef componente fill:#dfd,stroke:#333,stroke-width:2px;
  class UI,CEDIS,CRM,VENTAS,FACT,LIQ,CAJA,REP,CONF modulo;
  class F,W,T,M,WS,S,CTRL,MDL,VIEWS_CLASES,TABLAS,SP,VIEWS_DB,IDX componente;

</div>

El sistema sigue una arquitectura en capas tradicional:

### 2.1 Capa de Presentación (Frontend)

Implementada en PHP con HTML5, utilizando tecnologías modernas para interacción dinámica:

- **Bootstrap 4.x**: diseño responsivo, componentes de UI
- **jQuery 3.x**: manipulación del DOM, validaciones, llamadas AJAX
- **Select2, iCheck, Datepicker, SweetAlert2**: para formularios enriquecidos
- **DataTables**: tablas dinámicas con ordenamiento, búsqueda y exportación
- **Chart.js**: visualización de datos con gráficos

La estructura del frontend se divide en componentes reutilizables:
- Formularios (`*.forms.php`)
- Widgets (`*.widgets.php`)
- Tablas (`*.tablas.php`)
- Modales (`*.modals.php`)
- Scripts AJAX (`*.ajax.js`)

Cada módulo tiene su espacio de trabajo en `*.wspace.php`, donde se integran las vistas y funcionalidades.

### 2.2 Capa de Lógica de Negocio (Backend)

El backend está desarrollado en **PHP nativo**, sin frameworks externos, y sigue el patrón **MVC**:

- **Modelos**: clases PHP en `/clases/` que manejan reglas de negocio, acceso a datos y validaciones.
- **Controladores**: scripts AJAX (`*.ajax.php`) que actúan como intermediarios entre frontend y backend.
- **Vistas**: archivos `.php` en `forms`, `widgets`, `tablas` que contienen el HTML renderizado.

Se emplean los siguientes patrones de diseño:

- **Singleton**: para conexiones persistentes a la base de datos.
- **Factory**: para instanciar dinámicamente vistas o procesos según el módulo.
- **Token-Based Routing**: los controladores AJAX interpretan tokens en las solicitudes para ejecutar acciones específicas.

### 2.3 Capa de Datos

La capa de datos utiliza **MySQL** como sistema gestor de base de datos. Características clave:

- Diseño relacional optimizado para consultas de alto rendimiento.
- Amplio uso de **procedimientos almacenados** (`sp_*`) para encapsular lógica compleja del negocio.
- Exportación y respaldo de datos en formatos **JSON** y **PDF**.
- Generación de reportes en **Excel**.
- Integración con archivos TXT y XML para procesos de facturación electrónica y PAC.

---

## 3. Convenciones Generales

- **Naming**: prefijos por módulo (`cds_`, `crm_`, `vta_`, etc.), y sufijos por tipo de archivo (`_forms`, `_tablas`, `_ajax`, `_modals`, `_wspace`).
- **Modularidad**: cada módulo mantiene independencia funcional con puntos de integración bien definidos.
- **Seguridad**: cada llamada AJAX incluye validación de sesión, tokens y control de permisos por rol y sucursal.
- **Reusabilidad**: widgets, modales, validaciones y scripts están diseñados para ser reutilizados.

---

## 4. Interacción General Cliente-Servidor

<div class="mermaid">
sequenceDiagram
    participant Usuario
    participant Navegador
    participant JSFrontend
    participant AJAXPHP
    participant ClasesPHP
    participant BaseDatos

    Usuario->>Navegador: Interacción UI
    Navegador->>JSFrontend: Captura evento
    JSFrontend->>AJAXPHP: Envío de datos (token)
    AJAXPHP->>ClasesPHP: Instanciación y lógica
    ClasesPHP->>BaseDatos: Consulta / actualización
    BaseDatos-->>ClasesPHP: Resultados
    ClasesPHP-->>AJAXPHP: Datos procesados
    AJAXPHP-->>JSFrontend: Respuesta JSON/XML
    JSFrontend-->>Navegador: Renderiza resultados
</div>

