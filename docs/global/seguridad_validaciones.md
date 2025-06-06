# Seguridad y Validaciones en SIAC 2.0

Este documento detalla los mecanismos de control de acceso, validación de datos y protección contra amenazas comunes que se implementan en el sistema SIAC 2.0. Incluye tanto medidas en el cliente como en el servidor, con enfoque en la integridad, confidencialidad y disponibilidad de los datos.

---

## 1. Control de Acceso

### 1.1 Autenticación

- Basada en sesiones PHP (`$_SESSION`).
- Login requiere usuario, contraseña y empresa/sucursal.
- Contraseñas almacenadas con hash y validadas en el backend.
- Expiración configurable de sesión por inactividad.

### 1.2 Autorización

- Cada usuario tiene un perfil definido por tipo (`add_user_tipo`).
- Los permisos se asignan por rol en `roles_usuar` y se vinculan con menús en `roles_usuar_menu`.
- El acceso a cada módulo se controla en tiempo de ejecución mediante validaciones en scripts AJAX y menús dinámicos.

### 1.3 Control Multisucursal

- Cada acción verifica el contexto de empresa (`ide`) y sucursal (`ids`) activa.
- Se emplean filtros para limitar la visibilidad de datos a usuarios autorizados.

---

## 2. Validación de Sesiones y Tokens

### 2.1 Validación de Sesión

- Todos los controladores AJAX inician con verificación de existencia y validez de `$_SESSION`.
- Si la sesión no está activa, se retorna error y se redirige a login.

### 2.2 Validación por Token

- Cada solicitud AJAX lleva un `token` (`$_POST['token']`), que determina la acción a ejecutar.
- Los scripts como `crm_ajax.php`, `cds_ajax.php` emplean `switch(token)` para controlar el flujo.
- Tokens son únicos por archivo y se documentan en cada módulo.
- Verificaciones adicionales por tipo de usuario y permisos específicos.

---

## 3. Validaciones de Datos

### 3.1 Validaciones en Frontend (JavaScript)

- HTML5: `required`, `pattern`, `maxlength`, `min`, `max`.
- Validaciones dinámicas con jQuery para formularios (`*.forms.php`).
- Plugins: iCheck, Toastr, SweetAlert2 para interacción visual.

### 3.2 Validaciones en Backend (PHP)

- Sanitización de datos de entrada: `htmlspecialchars()`, `filter_var()`.
- Validación de tipos (`is_numeric`, `is_string`, `DateTime::createFromFormat`).
- Prevención de SQL Injection con consultas preparadas (`mysqli`, `PDO`).
- Verificación de integridad lógica: no duplicación, rangos válidos, estado consistente.

---

## 4. Seguridad en Transporte y Almacenamiento

### 4.1 Transporte

- Implementación de HTTPS recomendada.
- Uso de `$.ajax` con método `POST` para evitar exposición en URL.

### 4.2 Almacenamiento

- Contraseñas con hashing (por ejemplo, `bcrypt`).
- Control de acceso a archivos por permisos del sistema operativo.
- Archivos de configuración (conexiones, claves) fuera del directorio público.

---

## 5. Prevención de Amenazas Comunes

| Amenaza                  | Mecanismo de Prevención                           |
|--------------------------|----------------------------------------------------|
| SQL Injection            | Consultas preparadas, validación de entradas      |
| Cross-Site Scripting (XSS)| `htmlspecialchars`, `strip_tags`, validaciones JS |
| Session Hijacking        | Regeneración de session ID, expiración de sesiones|
| CSRF (Cross-Site Request Forgery) | Validación de sesión, tokens únicos AJAX   |
| Fuerza Bruta             | Límite de intentos, captcha (opcional)           |

---

## 6. Buenas Prácticas de Desarrollo

- Validar todos los datos del lado servidor, incluso si ya fueron validados en frontend.
- Documentar y versionar tokens de AJAX.
- Utilizar roles mínimos necesarios para usuarios nuevos.
- Revisar y limpiar sesiones obsoletas periódicamente.
- Nunca confiar en datos del cliente sin validación interna.

---

Este documento sirve como referencia para desarrolladores y auditores de seguridad para garantizar que el sistema SIAC 2.0 cumple con buenas prácticas de protección de datos y control de acceso.

