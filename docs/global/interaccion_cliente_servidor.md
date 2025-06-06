# Interacción Cliente-Servidor en SIAC 2.0

Este documento detalla cómo se comunican las capas frontend y backend del sistema SIAC 2.0, centrándose en el flujo de información, validaciones, uso de AJAX y el manejo de tokens como controladores de lógica de negocio.

---

## 1. Modelo de Comunicación Asíncrona

El sistema SIAC 2.0 está diseñado para operar de forma altamente interactiva mediante **AJAX**. Esto permite que la interfaz de usuario se actualice sin recargar toda la página, proporcionando una experiencia fluida y eficiente.

### 1.1 Flujo General

<div class="mermaid">
sequenceDiagram
    participant Usuario
    participant Navegador
    participant JSFrontend as JavaScript Frontend
    participant AJAXPHP as AJAX PHP Controller
    participant Backend as Clase PHP
    participant DB as Base de Datos

    Usuario->>Navegador: Interacción (clic, cambio, submit)
    Navegador->>JSFrontend: Captura evento
    JSFrontend->>AJAXPHP: Envío vía POST con token
    AJAXPHP->>Backend: Validación de token y lógica
    Backend->>DB: Acceso a datos
    DB-->>Backend: Resultado de la consulta
    Backend-->>AJAXPHP: Resultado procesado
    AJAXPHP-->>JSFrontend: Respuesta JSON o HTML
    JSFrontend-->>Navegador: Actualización de UI
</div>

## 2. Componentes Clave

### 2.1 JavaScript Frontend (`*.ajax.js`)
- Capta eventos (por ejemplo, `onClick`, `onSubmit`).
- Realiza peticiones `$.ajax()` con `type: "POST"`, `dataType: "json"` o `"html"`.
- Usa **token** como selector lógico que determina la acción que ejecutará el backend.
- Maneja `success`, `error` y `complete` para:
  - Actualizar la UI.
  - Mostrar mensajes (Toastr, SweetAlert2).
  - Redirigir.

### 2.2 Controlador AJAX PHP (`*.ajax.php`)
- Cada archivo contiene una estructura `switch ($_POST['token']) { ... }`.
- Se validan los datos de entrada y la sesión de usuario.
- Se llaman métodos de clases específicas según el módulo (por ejemplo, `class_crm`, `class_cds`).
- Retornan arrays codificados en JSON o bloques HTML directamente para insertar en el DOM.

### 2.3 Clases de Negocio (`class_*.php`)
- Contienen métodos públicos para manejar operaciones de negocio:
  - Inserciones.
  - Consultas.
  - Actualizaciones.
  - Validaciones.
- Utilizan conexiones MySQL mediante **PDO** o **mysqli**, con protección contra inyecciones SQL.
- Algunos métodos incluyen lógica de auditoría, control de errores y logs.

## 3. Token-Based Routing

Cada acción se identifica mediante un número entero llamado **token**, enviado desde el frontend.

### 3.1 Ejemplo

```javascript
$.ajax({
    type: "POST",
    url: "crm_ajax.php",
    data: {
        token: 14,
        idcliente: 1283,
        email: 'nuevo@cliente.com'
    },
    success: function(response) {
        // procesar respuesta
    }
});
```
```php
// En crm_ajax.php
switch ($_POST['token']) {
    case 14:
        $crm = new class_crm();
        echo json_encode($crm->actualizarEmail($_POST['idcliente'], $_POST['email']));
        break;
}
```

### 3.2 Convenciones

- Los **tokens** se documentan en cada módulo.
- Deben ser **únicos por archivo AJAX**.
- Cada token debe tener su **documentación funcional**.

## 4. Validaciones en el Ciclo de Comunicación

### 4.1 En el Cliente
- Validación de formularios con **HTML5** (`required`, `pattern`).
- Validación dinámica con **JavaScript** (`onblur`, `keyup`).
- Confirmaciones antes de envío (SweetAlert2, modals).

### 4.2 En el Servidor
- Verificación de **sesión activa**.
- Validación de **estructura y tipo de datos** (`is_numeric`, `filter_var`).
- **Sanitización y escape** para proteger contra **XSS** y **SQLi**.
- Verificación de **permisos por usuario/sucursal**.

## 5. Manejo de Respuestas

Las respuestas desde PHP pueden ser de dos tipos:

- **JSON**: Estructura con `status`, `message`, `data`, usada para actualizar dinámicamente la interfaz.
- **HTML**: Fragmentos renderizados que se insertan directamente en el DOM.

### Ejemplo JSON
```json
{
    "status": "success",
    "message": "Correo actualizado correctamente",
    "data": {
        "idcliente": 1283,
        "email": "nuevo@cliente.com"
    }
}
```

## 6. Seguridad en la Interacción

- Todos los controladores AJAX inician con **validación de sesión** (`$_SESSION`).
- Se verifica que el **token sea válido** para el usuario y el módulo correspondiente.
- Se utilizan **funciones de acceso a base de datos con parámetros preparados** (PDO, `mysqli_stmt`) para evitar **SQL Injection**.
- Se pueden emplear **tokens CSRF adicionales** para acciones críticas.
