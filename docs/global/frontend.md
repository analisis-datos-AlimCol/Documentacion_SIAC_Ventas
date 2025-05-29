# Ficha Técnica Frontend - SIAC 2.0 Ventas
## 1. Estructura General

### 1.1 Componentes Principales


- **Formularios (`*.forms.php`)**
    - Validaciones  
    - Eventos  
    - Integración con backend  
    - Manejo de estados  

- **Widgets (`*.widgets.php`)**
    - Componentes reutilizables  
    - Visualización de datos  
    - KPIs y estadísticas  

- **Tablas (`*.tablas.php`)**
    - Paginación  
    - Filtros  
    - Ordenamiento  
    - Exportación  

- **Selects (`*.select.php`)**
    - Búsqueda  
    - Autocompletado  
    - Carga dinámica  

- **Select2 (`*.select2.php`)**
    - Búsqueda avanzada  
    - Autocompletado  
    - Multi-selección  

- **Modales (`*.modals.php`)**
    - Formularios emergentes  
    - Mensajes  
    - Confirmaciones  

- **AJAX (`*.ajax.js`)**
    - Comunicación asincrónica  
    - Manejo de eventos  
    - Validaciones  
    - Actualización dinámica 

### 1.2 Estructura de Archivos y Rutas

```plaintext
/frontend/
├── ajax/                         # Archivos AJAX
│   ├── ajax_send_txt_info.js    # AJAX para envío de texto
│   ├── cds_ajax.js              # AJAX para control de CEDIS
│   ├── cds_ajax_1.js            # AJAX auxiliar CEDIS
│   ├── conf_ajax.js             # AJAX para configuración
│   ├── cont_ajax.js             # AJAX para contabilidad
│   ├── mtz_ajax.js              # AJAX para matriz reportes de presupuesto
│   ├── pv_ajax.js               # AJAX para punto de venta
│   ├── pv_ajax_vm.js            # AJAX para vista móvil
│   ├── rh_ajax.js               # AJAX para recursos humanos
│   ├── rp_ajax.js               # AJAX para reportes
│   └── wk_ajax.js               # AJAX para workspace
│
├── forms/                        # Formularios
│   ├── cat_forms.php            # Formularios de catálogos
│   ├── cds_forms.php            # Formularios de CEDIS
│   ├── cds_forms_1.php          # Formularios CEDIS
│   ├── conf_forms.php           # Formularios de configuración
│   ├── cont_forms.php           # Formularios de contabilidad
│   ├── crm_forms.php            # Formularios de CRM
│   ├── mtz_forms.php            # Formularios de matriz reportes
│   ├── pv_forms.php             # Formularios de punto de venta
│   ├── rh_forms.php             # Formularios de recursos humanos
│   ├── rp_forms.php             # Formularios de reportes
│   └── vta_forms.php            # Formularios de ventas
│
├── js/                           # Archivos JavaScript
│   ├── cds_validations.js       # Validaciones
│   ├── jquery_jeditable.js      # jQuery editable
│   └── js_send.js               # Envío de datos
│
├── modals/                       # Modales
│   ├── cat_modals.php           # Modales de catálogos
│   ├── cds_modals.php           # Modales de CEDIS
│   ├── conf_modals.php          # Modales de configuración
│   ├── cont_modals.php          # Modales de contabilidad
│   ├── crm_modals.php           # Modales de CRM
│   ├── mtz_modals.php           # Modales de matriz reportes
│   ├── pv_modals.php            # Modales de punto de venta
│   ├── pv_modals_vm.php         # Modales de vista móvil
│   ├── rh_modals.php            # Modales de recursos humanos
│   └── wk_modals.php            # Modales de workspace
│
├── select/                       # Selects
│   ├── cat_select.php           # Selects de catálogos
│   ├── cds_select.php           # Selects de CEDIS
│   ├── conf_select.php          # Selects de configuración
│   ├── cont_select.php          # Selects de contabilidad
│   ├── pv_select.php            # Selects de punto de venta
│   └── vta_select.php           # Selects de ventas
│
├── select2/                      # Select2 mejorados
│   ├── cat_select2.php          # Select2 de catálogos
│   ├── cds_select2.php          # Select2 de CEDIS
│   ├── conf_select2.php         # Select2 de configuración
│   ├── cont_select2.php         # Select2 de contabilidad
│   ├── crm_select2.php          # Select2 de CRM
│   ├── mtz_select2.php          # Select2 de matriz reportes
│   ├── pv_select2.php           # Select2 de punto de venta
│   └── vta_select2.php          # Select2 de ventas
│
├── tablas/                       # Tablas dinámicas
│   ├── cds_tablas.php           # Tablas de CEDIS
│   ├── cds_tablas_1.php         # Tablas auxiliares CEDIS
│   ├── conf_tablas.php          # Tablas de configuración
│   ├── cont_tablas.php          # Tablas de contabilidad
│   ├── crm_tablas.php           # Tablas de CRM
│   ├── mtz_tablas.php           # Tablas de matriz reportes
│   ├── pv_tablas.php            # Tablas de punto de venta
│   ├── pv_tablas_vm.php         # Tablas de vista móvil
│   └── vta_tablas.php           # Tablas de ventas
│
├── widgets/                      # Widgets y componentes
│   ├── cat_widgets.php          # Widgets de catálogos
│   ├── cds_widgets.php          # Widgets de CEDIS
│   ├── conf_widgets.php         # Widgets de configuración
│   ├── cont_widgets.php         # Widgets de contabilidad
│   ├── crm_widgets.php          # Widgets de CRM
│   ├── mtz_widgets.php          # Widgets de matriz reportes
│   ├── pv_widgets.php           # Widgets de punto de venta
│   ├── pv_widget_vm.php         # Widgets de vista móvil
│   └── vta_widgets.php          # Widgets de ventas
│
├── wspace/                       # Espacios de trabajo
│   ├── cat_wspace.php           # Espacio de catálogos
│   ├── cds_wspace.php           # Espacio de CEDIS
│   ├── cds_wspace_1.php         # Espacio auxiliar CEDIS
│   ├── conf_wspace.php          # Espacio de configuración
│   ├── cont_wspace.php          # Espacio de contabilidad
│   ├── crm_wspace.php           # Espacio de CRM
│   ├── mtz_wspace.php           # Espacio de matriz reportes
│   ├── pv_wspace.php            # Espacio de punto de venta
│   └── wk_workspace.php         # Workspace principal
│
├── clases/                       # Clases PHP
│   ├── class_pv.php             # Clase punto de venta
│   ├── class_cat.php            # Clase catálogos
│   ├── class_conf.php           # Clase configuración
│   ├── class_cont.php           # Clase contabilidad
│   ├── class_crm.php            # Clase CRM
│   ├── class_mtz.php            # Clase matriz reportes
│   ├── class_rh.php             # Clase recursos humanos
│   └── class_rp.php             # Clase reportes
│
├── assets/                       # Recursos estáticos
│   ├── css/                     # Estilos CSS
│   │   └── custom.css          # Estilos personalizados
│   ├── js/                      # JavaScript
│   │   └── validations.js      # Validaciones
│   └── images/                  # Imágenes
│       ├── icons/              # Iconos
│       └── logos/              # Logos
│
└── vendors/                      # Librerías externas
    ├── bootstrap/               # Bootstrap 4
    ├── jquery/                  # jQuery 3.x
    ├── select2/                # Select2 4.x
    ├── datatables/             # DataTables 1.10.x
    ├── sweetalert2/            # SweetAlert2 11.x
    ├── icheck/                 # iCheck
    ├── datepicker/            # Datepicker
    └── chart.js/              # Chart.js 2.x
```


---

## 2. Librerías Principales

### 2.1 jQuery
- **Versión:** 3.x  
- **Documentación:** [https://api.jquery.com/](https://api.jquery.com/)  
- **Uso Principal:** Manipulación del DOM, eventos, AJAX, animaciones, validaciones  

### 2.2 Bootstrap
- **Versión:** 4.x  
- **Documentación:** [https://getbootstrap.com/docs/4.6/](https://getbootstrap.com/docs/4.6/)  
- **Uso Principal:** Grid system, componentes UI, formularios, modal, alertas, cards  

### 2.3 Select2
- **Versión:** 4.x  
- **Documentación:** [https://select2.org/](https://select2.org/)  
- **Uso Principal:** Selects mejorados, búsqueda, autocompletado, multi-selección  

### 2.4 DataTables
- **Versión:** 1.10.x  
- **Documentación:** [https://datatables.net/](https://datatables.net/)  
- **Uso Principal:** Tablas dinámicas, paginación, filtros, ordenamiento, exportación  

### 2.5 SweetAlert
- **Versión:** 1.x  
- **Documentación:** [https://lipis.github.io/bootstrap-sweetalert/](https://lipis.github.io/bootstrap-sweetalert/)  
- **Uso Principal:** Alertas y mensajes de confirmación personalizados  

### 2.6 SweetAlert2
- **Versión:** 11.x  
- **Documentación:** [https://sweetalert2.github.io/](https://sweetalert2.github.io/)  
- **Uso Principal:** Notificaciones modernas, alertas interactivas  

### 2.7 iCheck
- **Versión:** 1.x  
- **Documentación:** [https://fronteed.com/iCheck/](https://fronteed.com/iCheck/)  
- **Uso Principal:** Checkboxes y radios personalizados, estilos personalizados  

### 2.8 jQuery UI Datepicker
- **Versión:** 1.x  
- **Documentación:** [https://jqueryui.com/datepicker/](https://jqueryui.com/datepicker/)  
- **Uso Principal:** Selección de fechas, formatos personalizados, validaciones  

### 2.9 Chart.js
- **Versión:** 2.x  
- **Documentación:** [https://www.chartjs.org/](https://www.chartjs.org/)  
- **Uso Principal:** Visualización de datos, KPIs, gráficos estadísticos  

### 2.10 Prism.js
- **Versión:** 1.x  
- **Documentación:** [https://prismjs.com/](https://prismjs.com/)  
- **Uso Principal:** Resaltado de sintaxis en bloques de código  

### 2.11 jQuery Vector Map
- **Versión:** 2.0.3  
- **Documentación:** [https://jvectormap.com/](https://jvectormap.com/)  
- **Uso Principal:** Mapas interactivos, visualización geográfica de datos  

### 2.12 Unslider
- **Versión:** 2.x  
- **Documentación:** [https://unslider.com/](https://unslider.com/)  
- **Uso Principal:** Sliders simples, carruseles de contenido  

### 2.13 CLNDR.js
- **Versión:** 1.x  
- **Documentación:** [https://kylestetz.github.io/CLNDR/](https://kylestetz.github.io/CLNDR/)  
- **Uso Principal:** Calendarios interactivos, manejo de eventos  

### 2.14 Climacons
- **Versión:** -  
- **Documentación:** [https://adamwhitcroft.com/climacons/](https://adamwhitcroft.com/climacons/)  
- **Uso Principal:** Íconos meteorológicos para interfaces  

### 2.15 Morris.js
- **Versión:** 0.5.x  
- **Documentación:** [https://morrisjs.github.io/morris.js/](https://morrisjs.github.io/morris.js/)  
- **Uso Principal:** Gráficos de líneas, barras y áreas  

### 2.16 DataTables Bootstrap Integration
- **Versión:** 1.10+  
- **Documentación:** [https://datatables.net/manual/styling/bootstrap4](https://datatables.net/manual/styling/bootstrap4)  
- **Uso Principal:** Estilización y compatibilidad con Bootstrap  

### 2.17 Bootstrap Datepicker
- **Versión:** 1.x  
- **Documentación:** [https://bootstrap-datepicker.readthedocs.io/en/latest/](https://bootstrap-datepicker.readthedocs.io/en/latest/)  
- **Uso Principal:** Selección de fechas con soporte Bootstrap  

### 2.18 Meteocons
- **Versión:** -  
- **Documentación:** [https://www.alessioatzeni.com/meteocons/](https://www.alessioatzeni.com/meteocons/)  
- **Uso Principal:** Íconos meteorológicos estilo flat  


## 3. Consideraciones de Frontend Comunes

### 3.1 Diferencias entre Versión Desktop y Móvil

#### 3.1.1 Estructura de Componentes
- **Formularios**
    - Desktop: Layout en columnas con campos agrupados
    - Móvil: Layout vertical con campos en una sola columna
    - Uso de `form-group` de Bootstrap para ambos casos

- **Tablas**
    - Desktop: Tablas completas con todas las columnas visibles
    - Móvil: Tablas responsivas con columnas ocultas y botón de detalles
    - Implementación de `dataTables` con configuración específica para móvil

- **Selects y Select2**
    - Desktop: Select2 con búsqueda y multi-selección
    - Móvil: Select2 con menú desplegable optimizado
    - Uso de `select2-container--mobile` para estilos específicos

- **Modales**
    - Desktop: Modales con tamaño fijo y scroll interno
    - Móvil: Modales full-screen con scroll de la página
    - Implementación de `modal-dialog-scrollable` para móvil

#### 3.1.2 Optimizaciones de Rendimiento
- Carga diferida de imágenes en móvil
- Reducción de elementos DOM en móvil
- Optimización de AJAX para móvil (menos datos)
- Implementación de `lazy-loading` en tablas

#### 3.1.3 Interacciones
- Desktop: Uso de hover y tooltips
- Móvil: Uso de touch y gestos
- Adaptación de eventos (click vs touch)
- Implementación de `touch-action` para mejor rendimiento

### 3.2 Componentes Comunes

#### 3.2.1 Validaciones
- Validaciones en tiempo real
- Mensajes de error consistentes
- Uso de `jQuery.validate()`
- Implementación de `data-validation` para personalización

#### 3.2.2 Manejo de Estados
- Estado de carga (loading)
- Estado de error
- Estado de éxito
- Implementación de `state-manager.js`

#### 3.2.3 Eventos Globales
- Eventos personalizados
- Sistema de notificaciones
- Manejo de sesiones
- Implementación de `event-bus.js`

#### 3.2.4 Estilos Comunes
- Variables CSS compartidas
- Mixins y componentes reutilizables
- Sistema de colores consistente
- Implementación de `custom.scss`

### 3.3 Consideraciones de Seguridad
- Validación de entrada
- Protección contra XSS
- Manejo seguro de datos sensibles
- Implementación de `security.js`

### 3.4 Accesibilidad
- Etiquetas ARIA
- Soporte para lectores de pantalla
- Contraste adecuado
- Implementación de `accessibility.js`
    - Gráficos estadísticos  
    - Visualización de datos  
    - KPIs  

---

## 3. Patrones de Diseño

### 3.1 Templates

- Estructura común para formularios  
- Componentes reutilizables  
- Sistema de eventos  
- Manejo de estados  

### 3.2 Componentes Reutilizables

- Formularios base  
- Tablas dinámicas  
- Selects con búsqueda  
- Modales  
- Widgets estadísticos  

### 3.3 Sistema de Eventos

- AJAX requests  
- Validaciones  
- Manejo de errores  
- Actualización dinámica  

---

## 4. Integración con Backend




### 4.1 Manejo de Datos

- Formateo  
- Validación  
- Exportación  
- Importación  


### 4.2 Comunicación AJAX

- Tokens  
- Validación de sesión  
- Manejo de errores  
- Carga asíncrona  
- **Método:** POST  
- **Formato:** JSON  

**Ejemplo de petición:**

```javascript
$.ajax({
    url: 'pv_ajax.php',
    type: 'POST',
    data: JSON.stringify({
        anf: año,
        eidf: id_empresa,
        sidf: id_sucursal,
        // ... otros parámetros
    }),
    contentType: 'application/json',
    success: function(response) {
        // Manejo de respuesta
    },
    error: function(xhr, status, error) {
        // Manejo de errores
    }
});
```

### 4.3 Manejo de Errores

**Status HTTP:**

- `200`: Éxito  
- `400`: Error de validación  
- `401`: Sesión expirada  
- `500`: Error del servidor  

**Estructura de errores:**

```json
{
  "status": "error",
  "code": "400",
  "message": "Error de validación",
  "errors": {
    "campo1": "Error en campo 1",
    "campo2": "Error en campo 2"
  }
}
```


### 4.4 Estructura de Payloads
**Petición:**

```javascript
CopyInsert
{
    "action": "pv_gv_av_os_doc_unlock_send_x_ids",
    "params": {
        "anf": año,
        "eidf": id_empresa,
        "sidf": id_sucursal,
        // ... otros parámetros
    }
}
```
**Respuesta:**

```javascript
CopyInsert
{
    "status": "success/error",
    "data": {
        // datos de respuesta
    },
    "message": "Mensaje de éxito/error"
}
```

### 4.5 Flujo de Validación

- Validación de sesión
- Validación de permisos
- Validación de datos
- Procesamiento del negocio
- Respuesta al cliente

## 5. Componentes Personalizados

### 5.1 Convenciones de Nombres

**Prefijos:**

- f_: Formularios
- sl_: Selects
- txt_: Textos
- btn_: Botones
- ck_: Checkboxes
- rd_: Radios

**Clases:**

- form-control: Campos de entrada
- slmun: Select múltiple
- minimal: Estilo minimalista
- icheckbox_minimal-blue: Checkbox
- iradio_minimal-blue: Radio

### 5.2 Estados de Componentes

- Activo: iCheck('enable')
- Deshabilitado: iCheck('disable')
- Validado: class="has-success"
- Error: class="has-error"
### 5.3 Inicialización

```javascript
CopyInsert
$(function () {
    // Inicialización de iCheck
    $('input[type="checkbox"].minimal, input[type="radio"].minimal').iCheck({
        checkboxClass: 'icheckbox_minimal-blue',
        radioClass: 'iradio_minimal-blue'
    });

    // Inicialización de Select2
    $('.select2').select2({
        placeholder: 'Selecciona',
        allowClear: true
    });
});
```

## 6. Responsividad y Adaptabilidad

### 6.1 Breakpoints Bootstrap 4:
- xs: <576px
- sm: ≥576px
- md: ≥768px
- lg: ≥992px
- xl: ≥1200px


### 6.2 Reglas Personalizadas
**Grid personalizado:**

```css
CopyInsert
.col-xl-10 {
    flex: 0 0 83.333333%;
    max-width: 83.333333%;
}
```
### 6.3 Consideraciones Móviles
- Formularios adaptativos
- Menús responsivos
- Tablas scrollables
- Botones grandes para touch
## 7. Accesibilidad (a11y)
### 7.1 Etiquetado de Formularios
```html
CopyInsert
<div class="form-group">
    <label for="txtconm" class="text-bold-700">CONTACTO</label>
    <div class="input-group">
        <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon3">
                <i class="fa fa-asterisk"></i>
            </span>
        </div>
        <input type="text" id="txtconm" name="txtconm" class="form-control">
    </div>
</div>
```

### 7.2 ARIA

- aria-label: Etiquetas descriptivas
- aria-describedby: Descripciones adicionales
- aria-expanded: Estados de elementos
- aria-hidden: Elementos ocultos

### 7.3 Navegación por Teclado
- Focus visible
- Tab index
- Role attributes

## 8. Control de Versiones y Entorno
### 8.1 Gestión de Dependencias
- jQuery: Versión 3.x
- Bootstrap: Versión 4.x
- Select2: Versión 4.x
- DataTables: Versión 1.10.x
- SweetAlert2: Versión 11.x
### 8.2 Entorno
Navegadores soportados:

- Chrome (última versión)
- Firefox (última versión)
- Edge (última versión)
