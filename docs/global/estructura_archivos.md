# Estructura de Archivos del Sistema SIAC 2.0

Este documento describe la convención general para la organización de archivos en el sistema SIAC 2.0. Cada módulo del sistema sigue esta estructura, aunque algunos archivos pueden variar según las necesidades del módulo.

## 1. Organización por Carpeta

Los archivos del sistema se agrupan en el directorio principal `frontend/`, el cual contiene subcarpetas especializadas según su función:

### 1.1 `/frontend/ajax/`
Archivos JavaScript que manejan la comunicación asincrónica (AJAX) con el backend.
- Ejemplos: `cds_ajax.js`, `crm_ajax.js`, `pv_ajax.js`
- Función: Captura eventos de interfaz, realiza peticiones HTTP, y gestiona respuestas JSON/XML.

### 1.2 `/frontend/forms/`
Formularios PHP utilizados para entrada de datos y vistas estructuradas.
- Ejemplos: `crm_forms.php`, `cds_forms.php`, `pv_forms.php`
- Función: Contienen la lógica HTML y elementos de entrada del sistema.

### 1.3 `/frontend/modals/`
Ventanas emergentes reutilizables en el sistema.
- Ejemplos: `crm_modals.php`, `cds_modals.php`
- Función: Interfaz secundaria para edición, confirmación o vistas rápidas.

### 1.4 `/frontend/tablas/`
Tablas dinámicas utilizadas para mostrar datos con opciones de filtrado y exportación.
- Ejemplos: `crm_tablas.php`, `cds_tablas.php`
- Función: Implementadas con DataTables para ordenamiento, búsqueda y paginación.

### 1.5 `/frontend/widgets/`
Componentes visuales reutilizables para KPIs, gráficos y estados.
- Ejemplos: `crm_widgets.php`, `cds_widgets.php`
- Función: Proveen visualizaciones en paneles de control y dashboards.

### 1.6 `/frontend/select/` y `/frontend/select2/`
Selectores simples (`select`) y avanzados (`select2`) para entrada de datos.
- Función: Carga de listas dinámicas, autocompletado y búsqueda avanzada.

### 1.7 `/frontend/wspace/`
Espacios de trabajo integrados del usuario.
- Ejemplos: `cds_wspace.php`, `crm_wspace.php`
- Función: Consolidan vistas y funcionalidades en una sola interfaz.

### 1.8 `/frontend/clases/`
Clases PHP backend que contienen la lógica de negocio de cada módulo.
- Ejemplos: `class_crm.php`, `class_cds.php`, `class_vtas.php`

---

## 2. Uso en Fichas de Módulo

Cada módulo de SIAC 2.0 describe únicamente los archivos relevantes a su funcionamiento específico, omitiendo estructura repetitiva. Se recomienda consultar esta sección global para comprender el patrón general y facilitar el desarrollo de nuevos módulos.

---
