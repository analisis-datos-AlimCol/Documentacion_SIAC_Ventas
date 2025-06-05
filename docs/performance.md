# Ficha Técnica de Optimización y Performance - SIAC 2.0 Ventas


Esta ficha técnica proporciona una visión completa de la optimización y rendimiento en el SIAC 2.0 Ventas, cubriendo desde la base de datos hasta la interfaz de usuario, incluyendo seguridad y mejores prácticas.

## 1. Optimización de Base de Datos



### 1.1 Índices

- Índices compuestos para consultas frecuentes
- Índices en campos de búsqueda
- Índices en campos de ordenamiento
- Índices en campos de relación

Ejemplo:


```sql
-- Índices compuestos para consultas frecuentes
CREATE INDEX idx_ticket ON add_ticket_detalle (ide, ids, idav, idos, iddoc, idc);

-- Índices para búsqueda de productos
CREATE INDEX idx_productos ON add_comision_suc_av_prods_prom (ide, ids, idav, ano, idct);

-- Índices para búsqueda de sucursales
CREATE INDEX idx_sucursales ON add_sucursal (ide, ids, t_suc, adescuento, edo);
```
### 1.2 Consultas Optimizadas

- Uso de JOINs selectivos
- Limitación de resultados con LIMIT
- Uso de índices en WHERE
- Evitar SELECT *
- Uso de índices en GROUP BY

Ejemplo: 
```sql
-- Consulta con JOIN selectivo
SELECT tk.nmc, tk.fvta, tk.tpvta, tk.fcdoc, 
       (SELECT av.nmav FROM add_cc_myr AS av 
        WHERE av.ide = tk.ide 
          AND av.ids = tk.ids 
          AND av.rel = tk.idav) 
FROM add_ticket_titulo AS tk 
WHERE tk.ide = ? 
  AND tk.ids = ? 
  AND tk.idav = ? 
  AND tk.idos = ? 
  AND tk.idc = ? 
  AND tk.iddoc = ?;

-- Consulta con GROUP BY optimizada
SELECT razon_social, codsuc, nomsuc 
FROM add_sucursal 
WHERE ide = ? 
  AND (t_suc = 'S' OR t_suc = 'P') 
  AND adescuento = 'S' 
  AND edo = 'A' 
ORDER BY nomsuc ASC;
```

### 1.3 Cache de Consultas

```php

// Uso de cache en AJAX
$.ajax({
    url: 'vta_forms.php',
    cache: true,
    ...
});
```

## 2. Optimización de Memoria

### 2.1 Manejo de Recursos

```php
// Liberación de memoria en procesamiento de imágenes
imagedestroy($image_res); //freeup memory

// Manejo eficiente de resultados
while ($rwprod = mysqli_fetch_array($rsprod)) {
    // Procesamiento de datos
}
```
### 2.2 Sesiones

- Uso eficiente de sesiones
- Timeout de sesiones
- Limite de tamaño de sesión
- Sesiones basadas en cookies

### 2.3 Carga Lazy

- Carga diferida de imágenes
- Carga diferida de scripts
- Carga diferida de contenido

Ejemplo:

```javascript
// Carga diferida de scripts
$(document).ready(function(){
    $("#slsuc").change(function(event){
        var eidv = <?php echo $eidf;?>;
        var comv = 'S';
        var edov = 'A';
        var tokenv = 1;
        $("#view_prods_list").html('');
        var sidv = $("#slsuc").find(':selected').val();
        $('#slan').empty();
        $("#slav").load('vta_select.php?eids='+eidv+'&sids='+sidv+'&coms='+comv+'&edos='+edov+'&token='+tokenv);
    });
});
```

## 3. Optimización Frontend

### 3.1 AJAX

- Cache de peticiones AJAX
- Batch de peticiones
- Timeout de peticiones
- Manejo de errores asíncronos

### 3.2 UI/UX

- Loading states
- Feedback visual
- Optimización de renderizado
- Minimización de recursos

Ejemplo:

```html
<!-- Tabla optimizada con scroll -->
<div class='table-responsive scrollme' id='ckprods'>
    <table class='table table-xs'>
        <!-- Optimización de columnas -->
        <thead class='bg-blue-grey white'>
            <tr>
                <th style='width: 14%' class='text-center font-small-3'>CANTIDAD</th>
                <!-- ... -->
            </tr>
        </thead>
    </table>
</div>
``` 

### 3.3 Scripts

- Minificación de archivos
- Concatenación de archivos
- Carga diferida
- Cache de scripts

## 4. Optimización de Rendimiento

### 4.1 Paginación

- Paginación en listados
- Carga diferida de datos
- Optimización de scroll
- Cache de resultados

Ejemplo:

```javascript
// Paginación en AJAX
$('.slclie').select2({
    placeholder: 'Selecciona un Cliente',
    minimumInputLength: 3,
    ajax: {
        url: 'vta_select2.php?eidv=<?php echo $eidf; ?>&sidv=<?php echo $sidf; ?>&token=9',
        cache: true,
        data: function (params) {
            var query = {
                search: params.term,
                page: params.page || 1
            }
            return query;
        }
    }
});
```

### 4.2 Timeouts

```javascript
toastr.options = { 
    "closeButton": true,
    "debug": true,
    "newestOnTop": false,
    "progressBar": true,
    "positionClass": "toast-top-right",
    "preventDuplicates": false,
    "showDuration": "300",
    "hideDuration": "1000000",
    "timeOut": "3000",
    "extendedTimeOut": "1000"
};
```

### 4.3 Optimización de Red

- Comprimición de datos
- Minimización de peticiones
- Cache de recursos estáticos
- Optimización de transferencias

Ejemplo:

```php
// Optimización de transferencias
header('Content-Encoding: gzip');
ob_start('ob_gzhandler');
```

## 5. Optimización de Seguridad

### 5.1 Sesiones

- Timeout de sesiones
- Validación de tokens
- Protección contra sesiones
- Límite de intentos

### 5.2 Cookies

```php
if ($_COOKIE['siacventas'] == '') { 
    header('location: index.php'); 
}
// Timeout de sesiones
session_start();
session_destroy();
```

### 5.3 Validación

- Validación de entrada
- Validación de permisos
- Validación de estados
- Validación de datos

## 6. Mejores Prácticas

### 6.1 Código

- Reutilización de código
- Modularización
- Separación de responsabilidades
- Documentación

### 6.2 Rendimiento

- Optimización continua
- Monitoreo de rendimiento
- Testing de carga
- Análisis de rendimiento

### 6.3 Seguridad

- Validación de datos
- Protección contra inyecciones
- Manejo de sesiones
- Protección de recursos

## 7. Herramientas de Optimización

### 7.1 Monitoreo

- Tiempo de respuesta
- Uso de memoria
- Uso de CPU
- Tiempo de carga

### 7.2 Testing

- Testing de carga
- Testing de rendimiento
- Testing de seguridad
- Testing de funcionalidad

### 7.3 Optimización

- Optimización de consultas
- Optimización de código
- Optimización de UI
- Optimización de red

## 8. Consideraciones de Seguridad

- Protección contra inyecciones
- Validación de datos
- Protección de sesiones
- Manejo de errores