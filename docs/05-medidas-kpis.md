# 📐 Medidas DAX y KPIs

## 📑 Tabla de Contenidos

1. [Introducción](#introducción)
2. [Categoría 1: KPIs Principales](#categoría-1-kpis-principales)
3. [Categoría 2: Análisis Temporal](#categoría-2-análisis-temporal)
4. [Categoría 3: Análisis de Proveedores](#categoría-3-análisis-de-proveedores)
5. [Categoría 4: Análisis de Productos](#categoría-4-análisis-de-productos)
6. [Categoría 5: Análisis Geográfico](#categoría-5-análisis-geográfico)
7. [Categoría 6: Medidas Auxiliares y Avanzadas](#categoría-6-medidas-auxiliares-y-avanzadas)
8. [Guía de Implementación](#guía-de-implementación)
9. [Optimización y Mejores Prácticas](#optimización-y-mejores-prácticas)
10. [Solución de Problemas](#solución-de-problemas)

---

## 📌 Introducción

Este documento contiene la **documentación completa de las 32 medidas DAX** utilizadas en el proyecto de análisis de compras públicas del Senado de la República. Cada medida está diseñada para proporcionar insights específicos sobre diferentes aspectos del negocio.

### 📊 Resumen de Medidas

| Categoría | Cantidad | Propósito Principal |
|-----------|----------|---------------------|
| **KPIs Principales** | 8 medidas | Indicadores ejecutivos de alto nivel |
| **Análisis Temporal** | 7 medidas | Tendencias, comparaciones año/mes, acumulados |
| **Análisis de Proveedores** | 6 medidas | Desempeño y concentración de proveedores |
| **Análisis de Productos** | 7 medidas | Clasificación, ranking y valor de productos |
| **Análisis Geográfico** | 4 medidas | Distribución territorial de compras |
| **Medidas Auxiliares** | 3 medidas | Soporte y validaciones |
| **TOTAL** | **32 medidas** | Cobertura completa de análisis |

### 🎯 Convenciones

| Símbolo | Significado |
|---------|-------------|
| 📊 | Medida base (agregación simple) |
| 🧮 | Medida calculada (lógica compleja) |
| 📈 | Medida temporal (uso de funciones de tiempo) |
| 🎯 | Medida de contexto (CALCULATE, FILTER) |
| 💡 | Medida avanzada (uso de variables, iteradores) |
| ⚡ | Medida optimizada (alto rendimiento) |

### 🛠️ Requisitos Previos

Para usar estas medidas correctamente:

✅ Modelo de datos configurado con relaciones  
✅ Tabla DimCalendario creada y relacionada  
✅ Campos importados con tipos de datos correctos  
✅ Nombres de campos coinciden exactamente con el modelo  

---

## 📊 Categoría 1: KPIs Principales

Esta categoría contiene las **8 medidas fundamentales** que proporcionan una visión de alto nivel del desempeño global de las compras.

### 1.1 Total Monto Transado 💰📊⚡

**Propósito:** Suma total de todas las compras realizadas en el contexto de filtro actual.

**Fórmula DAX:**
```DAX
Total Monto Transado = 
SUM(FactCompras[Monto Transado])
```

**Lógica de Negocio:**
- Agrega todos los montos de las transacciones
- Respeta el contexto de filtro (fecha, proveedor, producto, etc.)
- Base para prácticamente todos los análisis financieros

**Formato Recomendado:**
- Tipo: Moneda
- Símbolo: $ (Pesos Chilenos)
- Decimales: 0 (para reportes ejecutivos) o 2 (para análisis detallado)
- Separador de miles: Punto (.) o Coma (,) según configuración regional

**Ejemplo de Valores:**
```
Sin filtros:        $1.245.678.900
Filtro Año 2024:    $456.789.000
Filtro Proveedor X: $12.345.000
```

**Casos de Uso:**
1. **Tarjeta KPI principal** en dashboard ejecutivo
2. **Eje Y en gráficos** de barras, líneas, áreas
3. **Base de cálculo** para porcentajes y promedios
4. **Validación** de totales contra sistemas fuente

**Uso en Visualizaciones:**
```
Tarjeta:
┌─────────────────────┐
│ Monto Total Compras │
│   $1.245.678.900    │
│   ▲ +12.5% vs 2023  │
└─────────────────────┘

Gráfico de Barras:
Proveedor A  ████████████ $450M
Proveedor B  ████████ $320M
Proveedor C  █████ $180M
```

**Validaciones:**
```DAX
// Verificar que no hay valores negativos
Validar Monto Positivo = 
IF([Total Monto Transado] < 0, "ERROR: Monto negativo", "OK")
```

---

### 1.2 Total Cantidad Productos 📦📊⚡

**Propósito:** Suma total de unidades de productos comprados.

**Fórmula DAX:**
```DAX
Total Cantidad Productos = 
SUM(FactCompras[Cantidad])
```

**Lógica de Negocio:**
- Agrega todas las cantidades de productos
- Útil para análisis de volumen (no solo valor monetario)
- Permite calcular precio promedio ponderado

**Formato Recomendado:**
- Tipo: Número entero
- Separador de miles: Activado
- Decimales: 0
- Ejemplo: 125.487 unidades

**Casos de Uso:**
1. **Análisis de volumen** vs valor
2. **Cálculo de precio promedio** (Monto / Cantidad)
3. **Gestión de inventario** y stock
4. **Análisis de consumo** por período

**Ejemplo Práctico:**
```
Escenario: Compra de notebooks
- 150 unidades compradas
- Monto: $75.000.000
- Precio promedio: $500.000 c/u

[Total Cantidad Productos] = 150
```

**Visualización Recomendada:**
```
Tarjeta KPI:
┌──────────────────────┐
│ Productos Comprados  │
│      125.487         │
│   unidades           │
└──────────────────────┘
```

---

### 1.3 Precio Promedio General 💵🧮⚡

**Propósito:** Calcular el precio promedio ponderado considerando todas las transacciones.

**Fórmula DAX:**
```DAX
Precio Promedio General = 
DIVIDE(
    SUM(FactCompras[Monto Transado]),
    SUM(FactCompras[Cantidad]),
    0
)
```

**Lógica de Negocio:**
- **No** es simplemente `AVERAGE(Precio Promedio)` ❌
- **Sí** es un promedio ponderado por cantidad ✅
- El tercer parámetro (0) previene errores de división por cero

**¿Por qué no AVERAGE?**
```
Ejemplo demostrativo:

Transacción 1: 1 unidad a $1.000.000 → Precio: $1.000.000
Transacción 2: 100 unidades a $10.000 → Precio: $10.000

AVERAGE(Precio Promedio) = $505.000 ❌ (incorrecto)
Precio ponderado real = $1.000.000 + $1.000.000 / 101 = $19.802 ✅ (correcto)

La medida DIVIDE hace el cálculo correcto:
($1.000.000 + $1.000.000) / 101 = $19.802
```

**Formato Recomendado:**
- Tipo: Moneda
- Decimales: 2 (para precisión)
- Ejemplo: $18.456,75

**Casos de Uso:**
1. **Benchmarking de precios** general
2. **Análisis de inflación** en compras
3. **Comparación temporal** de costos unitarios
4. **Indicador de eficiencia** de compras

---

### 1.4 Número Proveedores Únicos 🏢📊

**Propósito:** Contar cuántos proveedores distintos han vendido en el período.

**Fórmula DAX:**
```DAX
Número Proveedores Únicos = 
DISTINCTCOUNT(FactCompras[Rut Proveedor])
```

**Lógica de Negocio:**
- Usa `DISTINCTCOUNT` para contar valores únicos (no COUNT)
- Basado en RUT Proveedor (identificador único fiscal)
- Útil para medir diversificación de la cartera

**Formato Recomendado:**
- Tipo: Número entero
- Sin decimales
- Ejemplo: 1.247 proveedores

**Interpretación:**
```
Número alto de proveedores:
✅ Mayor competencia
✅ Diversificación de riesgo
⚠️ Posible atomización (dificulta gestión)

Número bajo de proveedores:
⚠️ Riesgo de concentración
⚠️ Menor competencia
✅ Más fácil de gestionar
```

**Análisis Complementario:**
```DAX
// Tasa de concentración
Tasa Concentración Proveedores = 
DIVIDE(
    10, // Top 10
    [Número Proveedores Únicos],
    0
)

// Si resultado > 0.5 (50%) → Alta concentración
```

---

### 1.5 Número Productos Únicos 🎯📊

**Propósito:** Contar cuántos productos diferentes se han comprado.

**Fórmula DAX:**
```DAX
Número Productos Únicos = 
DISTINCTCOUNT(FactCompras[Id])
```

**Lógica de Negocio:**
- Basado en campo `Id` (identificador único de producto)
- Indica diversidad de catálogo de compras
- Útil para análisis de portfolio

**Formato Recomendado:**
- Tipo: Número entero
- Ejemplo: 3.456 productos

**Casos de Uso:**
1. **Gestión de catálogo** de productos
2. **Análisis de complejidad** de compras
3. **Planificación de inventario**
4. **Indicador de estandarización**

**Métricas Derivadas:**
```DAX
// Productos por proveedor (promedio)
Productos por Proveedor = 
DIVIDE(
    [Número Productos Únicos],
    [Número Proveedores Únicos],
    0
)

// Interpretación:
// < 5 → Proveedores especializados
// > 20 → Proveedores multi-categoría
```

---

### 1.6 Número Órdenes Compra 📋📊

**Propósito:** Contar cuántas órdenes de compra distintas se han generado.

**Fórmula DAX:**
```DAX
Número Órdenes Compra = 
DISTINCTCOUNT(FactCompras[Numero OC])
```

**Lógica de Negocio:**
- Cuenta OCs únicas (no líneas de OC)
- Una OC puede tener múltiples productos
- Indicador de frecuencia de compra

**Formato Recomendado:**
- Tipo: Número entero
- Ejemplo: 12.456 OCs

**Análisis Operativo:**
```DAX
// Líneas promedio por OC
Líneas por OC = 
DIVIDE(
    COUNTROWS(FactCompras),
    [Número Órdenes Compra],
    0
)

// Interpretación:
// 1-3 líneas → Compras específicas
// 10-50 líneas → Compras consolidadas
// >100 líneas → Mega compras (eventos especiales)
```

**Casos de Uso:**
1. **Carga administrativa** (cada OC requiere proceso)
2. **Eficiencia de compras** (consolidación)
3. **Planificación de recursos** (equipo de compras)

---

### 1.7 Ticket Promedio por OC 🎫💡⚡

**Propósito:** Calcular el monto promedio de cada orden de compra.

**Fórmula DAX:**
```DAX
Ticket Promedio por OC = 
VAR TotalMonto = SUM(FactCompras[Monto Transado])
VAR NumeroOC = DISTINCTCOUNT(FactCompras[Numero OC])
RETURN
    DIVIDE(TotalMonto, NumeroOC, 0)
```

**Lógica de Negocio:**
- Usa **variables (VAR)** para mejor rendimiento y legibilidad
- Divide monto total entre número de OCs
- Indicador de tamaño promedio de compras

**Formato Recomendado:**
- Tipo: Moneda
- Decimales: 0
- Ejemplo: $1.234.567

**Interpretación:**
```
Ticket Alto (>$5M):
✅ Compras consolidadas
✅ Eficiencia administrativa
⚠️ Posible riesgo por monto

Ticket Bajo (<$500K):
✅ Compras específicas
⚠️ Posible atomización excesiva
⚠️ Mayor carga administrativa
```

**Análisis de Tendencia:**
```DAX
// Evolución del ticket promedio
Variación Ticket YoY = 
VAR TicketActual = [Ticket Promedio por OC]
VAR TicketAnterior = 
    CALCULATE(
        [Ticket Promedio por OC],
        SAMEPERIODLASTYEAR(DimCalendario[Fecha])
    )
RETURN
    DIVIDE(TicketActual - TicketAnterior, TicketAnterior, 0)
```

---

### 1.8 Monto Promedio Transacción 💵📊

**Propósito:** Calcular el monto promedio por línea de compra (no por OC).

**Fórmula DAX:**
```DAX
Monto Promedio Transacción = 
AVERAGE(FactCompras[Monto Transado])
```

**Diferencia con Ticket Promedio por OC:**
```
Monto Promedio Transacción → Por LÍNEA de compra
Ticket Promedio por OC → Por ORDEN completa

Ejemplo:
OC #12345 con 3 líneas:
- Línea 1: $100.000
- Línea 2: $200.000
- Línea 3: $300.000

Monto Promedio Transacción = $200.000 (promedio de líneas)
Ticket Promedio por OC = $600.000 (total de la OC)
```

**Formato Recomendado:**
- Tipo: Moneda
- Decimales: 0
- Ejemplo: $456.789

**Casos de Uso:**
1. **Análisis granular** de compras
2. **Detección de outliers** por línea
3. **Política de compras** (montos mínimos/máximos)

---

## 📅 Categoría 2: Análisis Temporal

Esta categoría contiene **7 medidas** especializadas en análisis de series de tiempo, comparaciones interanuales y tendencias.

### 2.1 Monto Año Actual 📈🎯

**Propósito:** Total de compras del año seleccionado en el contexto actual.

**Fórmula DAX:**
```DAX
Monto Año Actual = 
VAR AnioActual = MAX(DimCalendario[Año])
RETURN
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        DimCalendario[Año] = AnioActual
    )
```

**Lógica de Negocio:**
- Identifica el año máximo en el contexto de filtro
- Usa `CALCULATE` para forzar filtro de ese año
- Útil para comparaciones dinámicas

**Comportamiento por Contexto:**
```
Sin filtro de año:
→ Monto del año más reciente en datos (ej: 2025)

Con filtro de año 2024:
→ Monto de 2024

Con selección de múltiples años:
→ Monto del año mayor seleccionado
```

**Formato Recomendado:**
- Tipo: Moneda
- Decimales: 0
- Ejemplo: $567.890.000

**Visualización:**
```
Tarjeta Comparativa:
┌──────────────────────┐
│   Año Actual (2025)  │
│   $567.890.000       │
│                      │
│   Año Anterior       │
│   $498.765.000       │
│   ▲ +13.9%           │
└──────────────────────┘
```

---

### 2.2 Monto Año Anterior 📉🎯

**Propósito:** Total de compras del año inmediatamente anterior al actual.

**Fórmula DAX:**
```DAX
Monto Año Anterior = 
VAR AnioActual = MAX(DimCalendario[Año])
VAR AnioAnterior = AnioActual - 1
RETURN
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        DimCalendario[Año] = AnioAnterior
    )
```

**Lógica de Negocio:**
- Calcula año anterior (Año actual - 1)
- Filtra datos específicamente de ese año
- Base para cálculo de variación YoY

**Casos de Uso:**
1. **Comparación año sobre año**
2. **Cálculo de variación porcentual**
3. **Análisis de crecimiento**
4. **Benchmarking temporal**

---

### 2.3 Variación % YoY 📊💡

**Propósito:** Calcular variación porcentual Year over Year (año sobre año).

**Fórmula DAX:**
```DAX
Variación % YoY = 
VAR MontoActual = [Monto Año Actual]
VAR MontoAnterior = [Monto Año Anterior]
RETURN
    DIVIDE(
        MontoActual - MontoAnterior,
        MontoAnterior,
        0
    )
```

**Fórmula Matemática:**
```
Variación % = ((Valor Actual - Valor Anterior) / Valor Anterior) × 100%

Ejemplo:
Actual: $600.000.000
Anterior: $500.000.000
Variación = ($600M - $500M) / $500M = 0.20 = 20% ✅ Crecimiento

Actual: $450.000.000
Anterior: $500.000.000
Variación = ($450M - $500M) / $500M = -0.10 = -10% 🔴 Decrecimiento
```

**Formato Recomendado:**
- Tipo: Porcentaje
- Decimales: 1
- Ejemplo: +15,5% o -8,2%

**Formato Condicional:**
```
Positivo (>0%) → Verde 🟢
Neutro (0%)   → Gris ⚪
Negativo (<0%) → Rojo 🔴
```

**Visualización Avanzada:**
```DAX
// Indicador visual con flecha
Indicador YoY = 
VAR Variacion = [Variación % YoY]
VAR Icono = 
    SWITCH(
        TRUE(),
        Variacion > 0, "▲",
        Variacion < 0, "▼",
        "="
    )
VAR Color = 
    SWITCH(
        TRUE(),
        Variacion > 0, "#28A745",  // Verde
        Variacion < 0, "#DC3545",  // Rojo
        "#6C757D"                  // Gris
    )
RETURN
    Icono & " " & FORMAT(Variacion, "0.0%")
```

**Casos de Uso:**
1. **KPI principal** de crecimiento
2. **Dashboards ejecutivos**
3. **Análisis de desempeño** departamental
4. **Alertas automáticas** (si variación fuera de rango)

---

### 2.4 Monto Acumulado Año 📈💡

**Propósito:** Calcular monto acumulado desde inicio de año hasta fecha actual (YTD - Year To Date).

**Fórmula DAX:**
```DAX
Monto Acumulado Año = 
VAR FechaMax = MAX(DimCalendario[Fecha])
VAR AnioActual = YEAR(FechaMax)
RETURN
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        FILTER(
            ALL(DimCalendario),
            DimCalendario[Año] = AnioActual &&
            DimCalendario[Fecha] <= FechaMax
        )
    )
```

**Lógica de Negocio:**
- Acumula desde 01/01 del año hasta la fecha seleccionada
- Usa `FILTER` con `ALL` para ignorar filtros de fecha pero mantener el acumulado
- Esencial para gráficos de evolución temporal

**Ejemplo Práctico:**
```
Fecha actual: 15/06/2025

Enero:    $50.000.000  → Acumulado: $50.000.000
Febrero:  $45.000.000  → Acumulado: $95.000.000
Marzo:    $60.000.000  → Acumulado: $155.000.000
Abril:    $55.000.000  → Acumulado: $210.000.000
Mayo:     $48.000.000  → Acumulado: $258.000.000
Junio:    $30.000.000  → Acumulado: $288.000.000 (hasta el 15)
```

**Visualización:**
```
Gráfico de Líneas (Acumulado):
$300M ┤        ╭────
      │      ╭─╯
$200M ┤    ╭─╯
      │  ╭─╯
$100M ┤╭─╯
      └┴─┴─┴─┴─┴─┴─→
       E F M A M J J
```

**Casos de Uso:**
1. **Seguimiento de presupuesto** anual
2. **Proyecciones** basadas en tendencia
3. **Comparación YTD** entre años
4. **Dashboards de progreso**

---

### 2.5 Días Desde Última Venta 📅🧮

**Propósito:** Calcular días transcurridos desde la transacción más reciente.

**Fórmula DAX:**
```DAX
Días Desde Última Venta = 
VAR UltimaFecha = MAX(FactCompras[Fecha Ultima Venta])
VAR FechaHoy = TODAY()
RETURN
    DATEDIFF(UltimaFecha, FechaHoy, DAY)
```

**Lógica de Negocio:**
- Usa `TODAY()` para obtener fecha actual del sistema
- `DATEDIFF` calcula diferencia en días
- Útil para detectar inactividad

**Interpretación:**
```
0-7 días   → 🟢 Actividad reciente
8-30 días  → 🟡 Actividad normal
31-90 días → 🟠 Inactividad moderada
>90 días   → 🔴 Inactividad prolongada (requiere investigación)
```

**Casos de Uso:**
1. **Monitoreo de actividad** del sistema
2. **Validación de actualización** de datos
3. **Alertas de inactividad**

**Validación de Frescura de Datos:**
```DAX
Estado Datos = 
VAR Dias = [Días Desde Última Venta]
RETURN
    SWITCH(
        TRUE(),
        Dias <= 7, "✅ Datos actualizados",
        Dias <= 30, "⚠️ Datos desactualizados",
        "🔴 Datos obsoletos - Actualizar"
    )
```

---

### 2.6 Monto Mes Actual 📆🎯

**Propósito:** Total de compras del mes seleccionado.

**Fórmula DAX:**
```DAX
Monto Mes Actual = 
VAR MesActual = MAX(DimCalendario[Mes])
VAR AnioActual = MAX(DimCalendario[Año])
RETURN
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        DimCalendario[Mes] = MesActual,
        DimCalendario[Año] = AnioActual
    )
```

**Lógica de Negocio:**
- Filtra por mes Y año (evita ambigüedad entre años)
- Dinámico según selección de filtros

**Formato Recomendado:**
- Tipo: Moneda
- Decimales: 0
- Ejemplo: $45.678.000

---

### 2.7 Monto Trimestre Actual 📊🎯

**Propósito:** Total de compras del trimestre seleccionado.

**Fórmula DAX:**
```DAX
Monto Trimestre Actual = 
VAR TrimestreActual = MAX(DimCalendario[Trimestre])
VAR AnioActual = MAX(DimCalendario[Año])
RETURN
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        DimCalendario[Trimestre] = TrimestreActual,
        DimCalendario[Año] = AnioActual
    )
```

**Definición de Trimestres:**
```
Q1 (Trimestre 1): Enero - Marzo
Q2 (Trimestre 2): Abril - Junio
Q3 (Trimestre 3): Julio - Septiembre
Q4 (Trimestre 4): Octubre - Diciembre
```

**Casos de Uso:**
1. **Reportes trimestrales** ejecutivos
2. **Análisis de estacionalidad**
3. **Planificación trimestral**

---

## 🏢 Categoría 3: Análisis de Proveedores

Esta categoría contiene **6 medidas** enfocadas en analizar el desempeño, concentración y comportamiento de los proveedores.

### 3.1 Monto por Proveedor 💰🎯⚡

**Propósito:** Calcular el monto total de compras por proveedor específico.

**Fórmula DAX:**
```DAX
Monto por Proveedor = 
CALCULATE(
    SUM(FactCompras[Monto Transado])
)
```

**Lógica de Negocio:**
- Usa `CALCULATE` para respetar contexto de filtro de proveedor
- Se utiliza en tablas y gráficos con dimensión de proveedor
- Base para rankings y análisis de participación

**Formato Recomendado:**
- Tipo: Moneda
- Decimales: 0
- Ejemplo: $123.456.789

**Uso en Visualizaciones:**
```
Tabla de Proveedores:
┌─────────────────────────────┬────────────────┐
│ Proveedor                   │ Monto Total    │
├─────────────────────────────┼────────────────┤
│ COMERCIAL DELTA LTDA.       │ $450.000.000   │
│ TECNOLOGÍA AVANZADA SpA     │ $320.000.000   │
│ INSUMOS GENERALES S.A.      │ $180.000.000   │
└─────────────────────────────┴────────────────┘
```

---

### 3.2 % Participación Proveedor 📊💡

**Propósito:** Calcular el porcentaje que representa cada proveedor del total de compras.

**Fórmula DAX:**
```DAX
% Participación Proveedor = 
VAR MontoProveedor = [Monto por Proveedor]
VAR MontoTotal = 
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        ALL(DimProveedores)
    )
RETURN
    DIVIDE(MontoProveedor, MontoTotal, 0)
```

**Lógica de Negocio:**
- `ALL(DimProveedores)` elimina filtro de proveedor para calcular total general
- Divide monto del proveedor entre total global
- Fundamental para análisis de concentración

**Ejemplo de Cálculo:**
```
Proveedor A: $450.000.000
Total General: $1.500.000.000

% Participación = $450M / $1.500M = 0.30 = 30%
```

**Formato Recomendado:**
- Tipo: Porcentaje
- Decimales: 2
- Ejemplo: 15,75%

**Análisis de Concentración:**
```
>20% → 🔴 Alta dependencia (riesgo crítico)
10-20% → 🟡 Proveedor importante (monitorear)
5-10% → 🟢 Proveedor relevante
<5% → ⚪ Proveedor menor
```

**Visualización:**
```
Gráfico de Pareto:
100% ┤                    ╭──────
     │              ╭─────╯
 80% ┤        ╭─────╯ ← 80% en top 10
     │   ╭────╯
 50% ┤╭──╯
     └┴─┴─┴─┴─┴─┴─┴─┴─┴─→
      Proveedores (ordenados por monto)
```

---

### 3.3 Concentración Top 10 Proveedores 🎯💡

**Propósito:** Calcular qué porcentaje del gasto total está concentrado en los 10 principales proveedores.

**Fórmula DAX:**
```DAX
Concentración Top 10 Proveedores = 
VAR Top10 = 
    CALCULATETABLE(
        TOPN(
            10,
            VALUES(DimProveedores[Rut Proveedor]),
            [Monto por Proveedor],
            DESC
        )
    )
VAR MontoTop10 = 
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        Top10
    )
VAR MontoTotal = SUM(FactCompras[Monto Transado])
RETURN
    DIVIDE(MontoTop10, MontoTotal, 0)
```

**Lógica de Negocio:**
1. `TOPN` identifica los 10 proveedores con mayor monto
2. `CALCULATETABLE` materializa esa lista
3. `CALCULATE` suma solo esos 10 proveedores
4. `DIVIDE` calcula el porcentaje

**Interpretación:**
```
<50% → 🟢 Baja concentración (diversificación saludable)
50-70% → 🟡 Concentración moderada (aceptable)
70-85% → 🟠 Alta concentración (riesgo moderado)
>85% → 🔴 Concentración crítica (alto riesgo)
```

**Formato Recomendado:**
- Tipo: Porcentaje
- Decimales: 1
- Ejemplo: 68,5%

**Indicadores de Riesgo:**
```DAX
Nivel Riesgo Concentración = 
VAR Conc = [Concentración Top 10 Proveedores]
RETURN
    SWITCH(
        TRUE(),
        Conc > 0.85, "🔴 RIESGO CRÍTICO",
        Conc > 0.70, "🟠 RIESGO ALTO",
        Conc > 0.50, "🟡 RIESGO MODERADO",
        "🟢 RIESGO BAJO"
    )
```

---

### 3.4 Precio Promedio Proveedor 💵🧮

**Propósito:** Calcular precio promedio ponderado de productos vendidos por un proveedor.

**Fórmula DAX:**
```DAX
Precio Promedio Proveedor = 
VAR MontoTotal = SUM(FactCompras[Monto Transado])
VAR CantidadTotal = SUM(FactCompras[Cantidad])
RETURN
    DIVIDE(MontoTotal, CantidadTotal, 0)
```

**Casos de Uso:**
1. **Benchmarking** de precios entre proveedores
2. **Análisis de competitividad**
3. **Negociación** de contratos
4. **Detección de sobreprecios**

**Ejemplo de Análisis:**
```
Producto: Resma de papel

Proveedor A: $2.500 promedio → ✅ Competitivo
Proveedor B: $2.800 promedio → 🟡 Precio alto
Proveedor C: $3.500 promedio → 🔴 Sobreprecio (40% más caro)
```

---

### 3.5 Cantidad Vendida Proveedor 📦📊

**Propósito:** Total de unidades vendidas por un proveedor.

**Fórmula DAX:**
```DAX
Cantidad Vendida Proveedor = 
SUM(FactCompras[Cantidad])
```

**Formato Recomendado:**
- Tipo: Número entero
- Separador de miles: Activado
- Ejemplo: 125.487 unidades

**Análisis Combinado:**
```DAX
// Ticket unitario promedio del proveedor
Ticket Unitario Proveedor = 
DIVIDE(
    [Monto por Proveedor],
    [Cantidad Vendida Proveedor],
    0
)
```

---

### 3.6 Órdenes por Proveedor 📋📊

**Propósito:** Número de órdenes de compra emitidas a un proveedor.

**Fórmula DAX:**
```DAX
Órdenes por Proveedor = 
DISTINCTCOUNT(FactCompras[Numero OC])
```

**Análisis de Frecuencia:**
```
>50 OCs/año → 🟢 Proveedor recurrente (relación estable)
20-50 OCs/año → 🟡 Proveedor frecuente
5-20 OCs/año → 🟠 Proveedor ocasional
<5 OCs/año → ⚪ Proveedor esporádico
```

**Medida Derivada:**
```DAX
// Ticket promedio por OC del proveedor
Ticket Promedio OC Proveedor = 
DIVIDE(
    [Monto por Proveedor],
    [Órdenes por Proveedor],
    0
)
```

---

## 🎯 Categoría 4: Análisis de Productos

Esta categoría contiene **7 medidas** para analizar productos, clasificarlos y gestionar inventario.

### 4.1 Monto por Producto 💰🎯

**Propósito:** Total de compras por producto específico.

**Fórmula DAX:**
```DAX
Monto por Producto = 
CALCULATE(
    SUM(FactCompras[Monto Transado])
)
```

**Formato Recomendado:**
- Tipo: Moneda
- Decimales: 0

---

### 4.2 Cantidad por Producto 📦📊

**Propósito:** Total de unidades compradas por producto.

**Fórmula DAX:**
```DAX
Cantidad por Producto = 
SUM(FactCompras[Cantidad])
```

---

### 4.3 Valor Stock 💎💡

**Propósito:** Calcular valor total del inventario (Cantidad × Precio Promedio).

**Fórmula DAX:**
```DAX
Valor Stock = 
SUMX(
    FactCompras,
    FactCompras[Cantidad] * FactCompras[Precio Promedio]
)
```

**Lógica de Negocio:**
- Usa `SUMX` (iterador) para multiplicar fila por fila
- Calcula valor por cada línea y luego suma
- Útil para valorización de inventario

**Diferencia con Monto Transado:**
```
Monto Transado → Valor pagado en la compra
Valor Stock → Valorización a precio promedio

Pueden diferir si:
- Hubo descuentos en compra
- Precio promedio incluye múltiples compras
- Diferentes proveedores/fechas
```

---

### 4.4 Clasificación ABC Producto 🏆💡

**Propósito:** Clasificar productos en categorías A, B o C según la regla de Pareto (80/15/5).

**Fórmula DAX:**
```DAX
Clasificación ABC = 
VAR MontoProducto = [Monto por Producto]
VAR MontoTotal = 
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        ALL(DimProductos)
    )
VAR PorcentajeAcumulado = 
    VAR ProductosSuperiores = 
        FILTER(
            ALL(DimProductos),
            [Monto por Producto] >= MontoProducto
        )
    VAR MontoAcumulado = 
        CALCULATE(
            SUM(FactCompras[Monto Transado]),
            ProductosSuperiores
        )
    RETURN
        DIVIDE(MontoAcumulado, MontoTotal, 0)
RETURN
    SWITCH(
        TRUE(),
        PorcentajeAcumulado <= 0.80, "A",
        PorcentajeAcumulado <= 0.95, "B",
        "C"
    )
```

**Regla de Pareto - Clasificación ABC:**
```
Clase A: Productos que acumulan hasta 80% del valor
- ~20% de productos
- Alto valor, alta rotación
- Control estricto, inventario de seguridad

Clase B: Productos entre 80% y 95% acumulado
- ~30% de productos
- Valor medio, rotación moderada
- Control moderado

Clase C: Productos que completan el 95-100%
- ~50% de productos
- Bajo valor individual
- Control simple, compra bajo demanda
```

**Ejemplo Práctico:**
```
Total productos: 1.000
Total monto: $1.000.000.000

Clase A:
- 200 productos (20%)
- $800.000.000 (80%)
- Promedio: $4.000.000 por producto

Clase B:
- 300 productos (30%)
- $150.000.000 (15%)
- Promedio: $500.000 por producto

Clase C:
- 500 productos (50%)
- $50.000.000 (5%)
- Promedio: $100.000 por producto
```

**Políticas de Gestión:**
```DAX
Política Stock = 
SWITCH(
    [Clasificación ABC],
    "A", "Stock de seguridad: 30 días, Revisión: Semanal",
    "B", "Stock de seguridad: 15 días, Revisión: Quincenal",
    "C", "Compra bajo demanda, Revisión: Mensual"
)
```

---

### 4.5 Precio Promedio Producto 💰📊

**Propósito:** Precio promedio de un producto específico.

**Fórmula DAX:**
```DAX
Precio Promedio Producto = 
AVERAGE(FactCompras[Precio Promedio])
```

---

### 4.6 Variación Precio Producto 📈🧮

**Propósito:** Medir variabilidad/volatilidad del precio de un producto.

**Fórmula DAX:**
```DAX
Variación Precio Producto = 
STDEV.P(FactCompras[Precio Promedio])
```

**Interpretación:**
```
Desviación baja (<5% del precio promedio):
✅ Precio estable
✅ Mercado predecible
✅ Fácil presupuestar

Desviación alta (>20% del precio promedio):
⚠️ Precio volátil
⚠️ Investigar causas:
   - Diferentes proveedores
   - Diferentes especificaciones
   - Cambios de mercado
```

**Coeficiente de Variación:**
```DAX
Coeficiente Variación Precio = 
DIVIDE(
    [Variación Precio Producto],
    [Precio Promedio Producto],
    0
)

// Interpretación:
// <0.10 → Baja variabilidad
// 0.10-0.25 → Variabilidad moderada
// >0.25 → Alta variabilidad
```

---

### 4.7 Ranking Producto 🏆💡

**Propósito:** Posición del producto según monto total de compras.

**Fórmula DAX:**
```DAX
Ranking Producto = 
RANKX(
    ALL(DimProductos),
    [Monto por Producto],
    ,
    DESC,
    DENSE
)
```

**Parámetros de RANKX:**
- `ALL(DimProductos)`: Evalúa contra todos los productos
- `[Monto por Producto]`: Criterio de ranking
- (vacío): Sin valor alternativo
- `DESC`: Descendente (mayor valor = ranking 1)
- `DENSE`: Sin saltos en ranking (1, 2, 3, ... sin gaps)

**Formato Recomendado:**
- Tipo: Número entero
- Ejemplo: #1, #2, #3, ...

**Uso en Filtros:**
```DAX
Top 10 Productos = 
FILTER(
    ALL(DimProductos),
    [Ranking Producto] <= 10
)
```

---

## 🗺️ Categoría 5: Análisis Geográfico

Esta categoría contiene **4 medidas** para análisis de distribución territorial.

### 5.1 Monto por Región 🗺️🎯

**Propósito:** Total de compras por región geográfica.

**Fórmula DAX:**
```DAX
Monto por Región = 
CALCULATE(
    SUM(FactCompras[Monto Transado])
)
```

**Casos de Uso:**
1. **Mapas coropléticos** de Chile
2. **Análisis de distribución** geográfica
3. **Identificación de regiones** con mayor/menor actividad

---

### 5.2 % Distribución por Región 📊💡

**Propósito:** Porcentaje que representa cada región del total.

**Fórmula DAX:**
```DAX
% Distribución por Región = 
VAR MontoRegion = [Monto por Región]
VAR MontoTotal = 
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        ALL(DimRegiones)
    )
RETURN
    DIVIDE(MontoRegion, MontoTotal, 0)
```

**Análisis de Centralización:**
```
Región Metropolitana >60% → 🟡 Alta centralización
Región Metropolitana 40-60% → 🟢 Centralización moderada
Región Metropolitana <40% → ✅ Buena distribución regional
```

---

### 5.3 Precio Promedio por Región 💵🧮

**Propósito:** Precio promedio de productos en cada región.

**Fórmula DAX:**
```DAX
Precio Promedio por Región = 
VAR MontoTotal = SUM(FactCompras[Monto Transado])
VAR CantidadTotal = SUM(FactCompras[Cantidad])
RETURN
    DIVIDE(MontoTotal, CantidadTotal, 0)
```

**Análisis de Disparidades:**
- Comparar precios entre regiones
- Identificar sobrecostos logísticos
- Evaluar eficiencia de compras regionales

---

### 5.4 Cantidad por Región 📦📊

**Propósito:** Total de unidades compradas por región.

**Fórmula DAX:**
```DAX
Cantidad por Región = 
SUM(FactCompras[Cantidad])
```

---

## 🛠️ Categoría 6: Medidas Auxiliares y Avanzadas

Medidas de soporte, control y análisis avanzado.

### 6.1 Total Registros 🎯📊

**Propósito:** Contar registros totales en la tabla de hechos.

**Fórmula DAX:**
```DAX
Total Registros = 
COUNTROWS(FactCompras)
```

**Casos de Uso:**
- Validación de importación de datos
- Verificación de filtros
- Control de calidad

---

### 6.2 Crecimiento Mes a Mes 📈💡

**Propósito:** Variación porcentual del mes actual vs mes anterior.

**Fórmula DAX:**
```DAX
Crecimiento Mes a Mes = 
VAR MontoMesActual = [Monto Mes Actual]
VAR MontoMesAnterior = 
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        DATEADD(DimCalendario[Fecha], -1, MONTH)
    )
RETURN
    DIVIDE(
        MontoMesActual - MontoMesAnterior,
        MontoMesAnterior,
        0
    )
```

**Interpretación:**
```
>+10% → 🟢 Crecimiento significativo
0% a +10% → 🟢 Crecimiento moderado
-5% a 0% → 🟡 Estabilidad/leve decrecimiento
<-5% → 🔴 Decrecimiento preocupante
```

---

### 6.3 Índice de Rotación 💹🧮

**Propósito:** Medir frecuencia de compra (transacciones / productos únicos).

**Fórmula DAX:**
```DAX
Índice Rotación = 
VAR NumTransacciones = COUNTROWS(FactCompras)
VAR NumProductos = DISTINCTCOUNT(FactCompras[Id])
RETURN
    DIVIDE(NumTransacciones, NumProductos, 0)
```

**Interpretación:**
```
Índice >10 → Alta rotación (productos recurrentes)
Índice 3-10 → Rotación moderada
Índice <3 → Baja rotación (productos especializados)
```

---

## 🚀 Guía de Implementación

### Paso a Paso para Crear Medidas

**1. Preparar el modelo de datos:**
```
✅ Importar datos
✅ Crear relaciones
✅ Crear tabla DimCalendario
✅ Validar tipos de datos
```

**2. Crear medidas organizadas:**
```
Power BI Desktop:
1. Ir a vista de "Datos" o "Modelo"
2. Clic derecho en tabla FactCompras > "Nueva medida"
3. Copiar y pegar fórmula DAX
4. Nombrar medida exactamente como se indica
5. Presionar Enter
6. Configurar formato
```

**3. Organizar en carpetas de visualización:**
```
Panel de Campos:
📁 FactCompras
   📁 📊 KPIs Principales
      📊 Total Monto Transado
      📊 Número Proveedores Únicos
      ...
   📁 📅 Temporales
      📈 Monto Año Actual
      📈 Variación % YoY
      ...
   📁 🏢 Proveedores
   📁 🎯 Productos
   📁 🗺️ Geográfico
```

**4. Configurar formatos:**
```DAX
// Para medidas de moneda
Formato: $ Español
Decimales: 0 o 2
Separador de miles: Activado

// Para medidas de porcentaje
Formato: Porcentaje
Decimales: 1 o 2

// Para medidas de cantidad
Formato: Número entero
Separador de miles: Activado
```

---

## ⚡ Optimización y Mejores Prácticas

### 1. Uso de Variables (VAR)

**✅ BUENA PRÁCTICA:**
```DAX
Ticket Promedio por OC = 
VAR TotalMonto = SUM(FactCompras[Monto Transado])
VAR NumeroOC = DISTINCTCOUNT(FactCompras[Numero OC])
RETURN
    DIVIDE(TotalMonto, NumeroOC, 0)
```

**❌ MALA PRÁCTICA:**
```DAX
Ticket Promedio por OC = 
DIVIDE(
    SUM(FactCompras[Monto Transado]),
    DISTINCTCOUNT(FactCompras[Numero OC]),
    0
)
// Funciona pero es menos eficiente y menos legible
```

**Beneficios de variables:**
- ✅ Cálculo una sola vez (no se repite)
- ✅ Mejor rendimiento
- ✅ Más fácil de debugear
- ✅ Código más legible

### 2. Usar DIVIDE en lugar de operador /

**✅ CORRECTO:**
```DAX
Promedio = DIVIDE([Suma], [Cantidad], 0)
// Si Cantidad = 0, devuelve 0 (no error)
```

**❌ INCORRECTO:**
```DAX
Promedio = [Suma] / [Cantidad]
// Error si Cantidad = 0
```

### 3. Filtros Eficientes

**✅ EFICIENTE:**
```DAX
Monto 2024 = 
CALCULATE(
    SUM(FactCompras[Monto Transado]),
    DimCalendario[Año] = 2024
)
```

**❌ INEFICIENTE:**
```DAX
Monto 2024 = 
CALCULATE(
    SUM(FactCompras[Monto Transado]),
    FILTER(
        ALL(DimCalendario),
        DimCalendario[Año] = 2024
    )
)
// FILTER es más lento que filtro directo
```

### 4. Iteradores con Precaución

**Iteradores (SUMX, AVERAGEX, etc.):**
- 🟡 Útiles pero más lentos
- ✅ Usar cuando es necesario (cálculos fila por fila)
- ⚠️ Evitar en tablas muy grandes si hay alternativa

**Cuándo usar iteradores:**
```DAX
// ✅ NECESARIO: Multiplicación fila por fila
Valor Stock = 
SUMX(
    FactCompras,
    [Cantidad] * [Precio Promedio]
)

// ❌ INNECESARIO: Agregación simple
Total Monto = SUMX(FactCompras, [Monto Transado])
// Mejor usar: SUM(FactCompras[Monto Transado])
```

---

## 🔧 Solución de Problemas

### Error: "No se puede determinar el valor"

**Causa:** Relaciones mal configuradas o campos inexistentes

**Solución:**
```
1. Verificar relaciones en vista de Modelo
2. Confirmar nombre exacto de campos
3. Validar que tabla existe y está cargada
```

### Error: "Referencia circular"

**Causa:** Medida se usa a sí misma directamente

**Solución:**
```
❌ NO hacer:
Medida A = [Medida A] * 2

✅ SÍ hacer:
Medida A = SUM(Tabla[Campo]) * 2
```

### Medida devuelve valor incorrecto

**Causa:** Contexto de filtro no esperado

**Solución:**
```DAX
// Debugear con variables
Medida Debug = 
VAR Paso1 = SUM(Tabla[Campo])
VAR Paso2 = CALCULATE(Paso1, ALL(Tabla))
RETURN
    "Paso1: " & Paso1 & " | Paso2: " & Paso2
```

### Rendimiento lento

**Causas y soluciones:**
```
1. ❌ Uso excesivo de FILTER
   ✅ Usar filtros directos cuando sea posible

2. ❌ Iteradores en tablas grandes
   ✅ Evaluar si se puede usar agregación directa

3. ❌ Medidas dentro de medidas (profundidad >3)
   ✅ Optimizar jerarquía de medidas

4. ❌ ALL() sobre tablas completas grandes
   ✅ Usar ALLEXCEPT o filtros específicos
```

---

<div align="center">

✅ **Documentación de Medidas DAX Completa**

32 medidas documentadas con explicaciones, fórmulas, casos de uso y mejores prácticas

[⬅️ Diccionario de Datos](04-diccionario-datos.md) | [🏠 Volver al README](../README.md)

---

**📐 Análisis de Compras Públicas - Senado de la República de Chile**

*Documentación v1.0 - Febrero 2026*

</div>
