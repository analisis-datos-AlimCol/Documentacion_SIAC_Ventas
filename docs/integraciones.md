# Integraciones del Sistema SIAC 2.0

Este documento describe la las integraciones entre módulos del sistema SIAC 2.0 ventas, una solución empresarial modular desarrollada principalmente en PHP. Está diseñada bajo principios de escalabilidad, separación de responsabilidades y facilidad de mantenimiento.


## 1. Módulos Principales del Sistema

Los módulos están organizados por dominio. Cada uno se documenta por separado con su funcionalidad, estructura de archivos y base de datos específica.

- Caja: manejo de recibos, liquidaciones, cobros.

- CRM: gestión de clientes, visitas, rutas.

- CEDIS: control de inventario y distribución.

- Ventas: pedidos, precios, promociones, facturación.

- Facturación: generación y timbrado de CFDI.

- Liquidación: comisiones, validación de órdenes, cierre mensual.


## 2. Dependencias entre Módulos

### 2.1 Dependencias Funcionales

| Módulo Origen | Módulo Destino | Dependencia | Tipo de Dependencia | Descripción |
|---------------|----------------|-------------|---------------------|-------------|
| CEDIS         | Ventas         | Stock       | Directa             | El módulo de ventas consulta el stock disponible en CEDIS antes de procesar un pedido. |
| CRM           | Ventas         | Clientes    | Directa             | Las ventas dependen de la información de clientes proporcionada por CRM para generar pedidos. |
| Ventas        | Facturación    | Pedidos     | Directa             | La facturación requiere información de pedidos de ventas para generar facturas. |
| Ventas        | Liquidación    | Comisiones  | Directa             | La liquidación utiliza información de ventas para calcular comisiones. |
| Caja          | Liquidación    | Cobros      | Directa             | La liquidación requiere información de cobros de caja para conciliar pagos. |
| Reportes      | Todos          | Datos       | Indirecta           | Los reportes dependen de datos de todos los módulos para generar análisis. |
| Configuración | Todos          | Parámetros  | Indirecta           | Todos los módulos dependen de la configuración para obtener parámetros globales. |
| CEDIS   | CEDIS  |Stock  | Directa             | Controla el movimiento de productos entre sucursales |

### 2.2 Flujo de Datos

1. **Flujo CEDIS - Ventas - Facturación**

<div class="mermaid">
sequenceDiagram
    participant CEDIS
    participant Ventas
    participant Facturación
    participant Cliente
    CEDIS->>Ventas: Stock disponible
    Ventas->>Facturación: Pedido
    Facturación->>Cliente: CFDI
    Cliente->>Facturación: Pago
    Facturación->>Caja: Registro de pago
</div>

2. **Flujo CRM - Ventas - Liquidación**

<div class="mermaid">
sequenceDiagram
    participant CRM
    participant Ventas
    participant Liquidación
    CRM->>Ventas: Perfil Cliente
    Ventas->>Liquidación: Venta Realizada
    Liquidación->>Ventas: Comisión Calculada
</div>

3. **Flujo de Traslado de Productos**

<div class="mermaid">
sequenceDiagram
    participant SucursalA
    participant Traslados
    participant CEDIS
    participant SucursalB
    participant Facturación
    participant Caja
    
    SucursalA->>Traslados: Solicitud de traslado
    Traslados->>CEDIS: Verifica stock en A
    CEDIS->>Traslados: Confirma disponibilidad
    Traslados->>SucursalB: Notifica recepción esperada
    SucursalB->>Traslados: Confirma recepción
    Traslados->>CEDIS: Actualiza inventarios
    CEDIS->>SucursalA: Actualiza stock A
    CEDIS->>SucursalB: Actualiza stock B
    SucursalB->>Facturación: Genera CFDI (si aplica)
    Facturación->>Caja: Registro de movimientos
</div>

### 2.3 Dependencias de Procesos
Proceso de Venta Completo
<div class="mermaid">
graph LR
    A[CRM - Cliente] --> B[Ventas - Pedido]
    B --> C[CEDIS - Stock]
    C --> D[Facturación - CFDI]
    D --> E[Caja - Cobro]
    E --> F[Liquidación - Comisión]
</div>

Proceso de Facturación

<div class="mermaid">
graph LR
    A[Ventas - Pedido] --> B[Facturación - CFDI]
    B --> C[Caja - Pago]
    C --> D[Liquidación - Conciliación]
</div>

Proceso de Orden de Traslado

<div class="mermaid">
graph LR
    A[Pedido en Sucursal B] --> B[Verifica Stock en CEDIS]
    B --> C[Genera Orden de Traslado]
    C --> D[Notifica Sucursal A]
    D --> E[Prepara Traslado]
    E --> F[Confirma Recepción]
    F --> G[Actualiza Inventario]
</div>

### 2.4 Puntos de Integración Críticos

- Integración CEDIS-Ventas

    - Verificación de stock
    - Actualización de inventario
    - Notificaciones de stock bajo

- Integración CRM-Ventas
    - Validación de crédito
    - Historial de compras
    - Segmentación de clientes
- Integración Ventas-Facturación
    - Generación de CFDI
    - Validación fiscal
    - Timbrado
- Integración Caja-Liquidación
    - Conciliación de pagos
    - Distribución de comisiones
    - Reportes financieros