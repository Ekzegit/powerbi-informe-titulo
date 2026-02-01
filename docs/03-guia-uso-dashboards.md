# 📊 Guía de Uso de Dashboards

## 📑 Tabla de Contenidos

1. [Introducción](#introducción)
2. [Dashboard 1: Resumen Ejecutivo](#dashboard-1-resumen-ejecutivo)
3. [Dashboard 2: Análisis de Proveedores](#dashboard-2-análisis-de-proveedores)
4. [Dashboard 3: Análisis de Productos](#dashboard-3-análisis-de-productos)
5. [Dashboard 4: Análisis Geográfico](#dashboard-4-análisis-geográfico)
6. [Dashboard 5: Análisis Temporal](#dashboard-5-análisis-temporal)
7. [Navegación Entre Dashboards](#navegación-entre-dashboards)
8. [Exportación y Compartir](#exportación-y-compartir)
9. [Tips y Mejores Prácticas](#tips-y-mejores-prácticas)

---

## 📌 Introducción

Este documento describe en detalle los **5 dashboards principales** del informe de análisis de compras públicas del Senado de la República de Chile. Cada dashboard está diseñado para responder preguntas específicas de negocio y facilitar la toma de decisiones basada en datos.

### Estructura General de los Dashboards

Todos los dashboards comparten una estructura consistente:

```
┌─────────────────────────────────────────────────────┐
│  🏛️ TÍTULO DEL DASHBOARD                           │
├─────────────────────────────────────────────────────┤
│  🔍 FILTROS Y SEGMENTADORES (Top)                  │
├──────────────────┬──────────────────┬───────────────┤
│  📊 KPI 1        │  📊 KPI 2        │  📊 KPI 3     │
├──────────────────┴──────────────────┴───────────────┤
│  📈 VISUALIZACIÓN PRINCIPAL                         │
├──────────────────┬──────────────────────────────────┤
│  📉 VIZ DETALLE 1│  📉 VIZ DETALLE 2               │
└──────────────────┴──────────────────────────────────┘
```

### Paleta de Colores

Los dashboards utilizan una paleta institucional consistente:

| Color | Uso | Código Hex |
|-------|-----|------------|
| 🔵 Azul Principal | KPIs positivos, barras principales | #004B87 |
| 🟢 Verde | Crecimiento, indicadores positivos | #28A745 |
| 🔴 Rojo | Decrementos, alertas | #DC3545 |
| 🟡 Amarillo | Advertencias, valores medios | #FFC107 |
| ⚫ Gris | Valores secundarios, comparaciones | #6C757D |

---

## 📊 Dashboard 1: Resumen Ejecutivo

### 🎯 Objetivo

Proporcionar una **visión de alto nivel** de las compras públicas con los indicadores más relevantes para la toma de decisiones estratégicas.

### 📦 Componentes

#### 1. **Panel de KPIs Principales** (Tarjetas)

| KPI | Medida DAX | Descripción | Formato |
|-----|------------|-------------|---------|
| 💰 **Monto Total** | `Total Monto Transado` | Suma total de todas las compras | $999.999.999 |
| 🏢 **Proveedores** | `Número Proveedores Únicos` | Cantidad de proveedores distintos | 9.999 |
| 📦 **Productos** | `Número Productos Únicos` | Cantidad de productos únicos | 9.999 |
| 📋 **Órdenes de Compra** | `Número Órdenes Compra` | Total de OCs generadas | 99.999 |
| 🎫 **Ticket Promedio** | `Ticket Promedio por OC` | Monto promedio por OC | $999.999 |
| 📈 **Variación Anual** | `Variación % YoY` | Crecimiento año sobre año | +15,5% |

**Interpretación:**
- ✅ **Verde** si Variación YoY > 0% (crecimiento)
- 🔴 **Rojo** si Variación YoY < 0% (decrecimiento)
- Los KPIs se actualizan según los filtros aplicados

#### 2. **Gráfico de Evolución Temporal** (Gráfico de Líneas)

**Configuración:**
- **Eje X:** `Fecha` (DimCalendario)
- **Eje Y:** `Monto Acumulado Año`
- **Leyenda:** `Año` (para comparar múltiples años)
- **Tooltip:** Fecha, Monto, Variación %

**Cómo interpretar:**
- Tendencia ascendente = Mayor actividad de compras
- Picos en meses específicos = Períodos de alta demanda
- Comparación entre años para identificar patrones estacionales

#### 3. **Top 10 Proveedores** (Gráfico de Barras Horizontales)

**Configuración:**
- **Eje Y:** `Nombre Proveedor` (Top 10)
- **Eje X:** `Monto por Proveedor`
- **Etiquetas de datos:** Activadas (mostrar monto y %)

**Uso:**
- Identificar proveedores estratégicos
- Evaluar concentración de compras
- Detectar dependencia de proveedores específicos

#### 4. **Distribución por Tipo de Producto** (Gráfico de Dona)

**Configuración:**
- **Leyenda:** `TipoProducto`
- **Valores:** `Monto por Producto`
- **Etiquetas de detalle:** Porcentaje y monto

**Análisis:**
- Qué categorías representan mayor inversión
- Diversificación de la cartera de compras
- Prioridades de adquisición

#### 5. **Mapa de Compras por Región** (Mapa Coroplético)

**Configuración:**
- **Ubicación:** `Region` (DimRegiones)
- **Saturación de color:** `Monto por Región`
- **Tooltip:** Región, Monto, % del total

### 🔍 Filtros y Segmentadores Disponibles

| Filtro | Tipo | Valores |
|--------|------|---------|
| **📅 Año** | Segmentador de lista | 2022, 2023, 2024, 2025 |
| **📆 Mes** | Segmentador de lista | Enero - Diciembre |
| **🏛️ Institución** | Segmentador desplegable | Lista de instituciones |
| **🗺️ Región** | Segmentador de lista | Regiones de Chile |
| **📦 Tipo Producto** | Segmentador desplegable | Categorías de productos |

**Cómo usar los filtros:**

1. **Selección simple:** Clic en un valor
2. **Selección múltiple:** Ctrl + Clic en varios valores
3. **Limpiar filtro:** Icono de borrador en el segmentador
4. **Sincronización:** Los filtros afectan todos los visuales del dashboard

### 💼 Casos de Uso

**Caso 1: Revisión Mensual de Compras**
```
1. Filtrar por Año actual
2. Seleccionar mes a revisar
3. Analizar KPIs vs mes anterior
4. Revisar top proveedores del mes
5. Identificar categorías de mayor gasto
```

**Caso 2: Comparación Anual**
```
1. No aplicar filtros de año (ver todos)
2. Revisar gráfico de evolución temporal
3. Analizar Variación % YoY
4. Comparar distribución por tipo de producto
5. Evaluar cambios en proveedores principales
```

**Caso 3: Análisis por Institución**
```
1. Seleccionar institución específica
2. Revisar Monto Total y Ticket Promedio
3. Identificar proveedores principales de esa institución
4. Analizar distribución geográfica de compras
```

### 📤 Opciones de Exportación

- **Excel:** Clic derecho en cualquier visual > "Exportar datos" > .xlsx
- **PowerPoint:** Archivo > Exportar > PowerPoint (mantiene interactividad limitada)
- **PDF:** Archivo > Exportar a PDF (estático)
- **Imagen:** Clic derecho en visual > "Exportar datos" > Imagen (.png)

---

## 🏢 Dashboard 2: Análisis de Proveedores

### 🎯 Objetivo

Analizar en profundidad el desempeño, concentración y comportamiento de los proveedores del Senado.

### 📦 Componentes

#### 1. **KPIs de Proveedores**

| KPI | Medida | Interpretación |
|-----|--------|----------------|
| 🏢 **Proveedores Activos** | `Número Proveedores Únicos` | Total de proveedores con transacciones |
| 💰 **Monto Promedio/Proveedor** | `Monto por Proveedor` (promedio) | Ticket promedio por proveedor |
| 🎯 **Concentración Top 10** | `Concentración Top 10 Proveedores` | % del gasto en top 10 |
| 📋 **Promedio OCs/Proveedor** | `Órdenes por Proveedor` (promedio) | Frecuencia de compra promedio |

**Alertas:**
- ⚠️ Si Concentración Top 10 > 70% = Alta dependencia
- ⚠️ Si Proveedores con 1 sola OC > 50% = Atomización excesiva

#### 2. **Ranking de Proveedores** (Tabla Dinámica)

**Columnas:**
1. **#** - Ranking
2. **RUT** - Identificador fiscal
3. **Nombre Proveedor** - Razón social
4. **Monto Total** - Suma de compras
5. **% Participación** - Porcentaje del total
6. **Cantidad Vendida** - Unidades totales
7. **Precio Promedio** - Precio ponderado
8. **# Órdenes** - Cantidad de OCs
9. **Última Venta** - Fecha última transacción

**Formato condicional:**
- 🟢 % Participación > 5% (proveedores principales)
- 🟡 % Participación 1-5% (proveedores medios)
- ⚪ % Participación < 1% (proveedores menores)

**Ordenamiento dinámico:**
- Clic en encabezados para ordenar ascendente/descendente
- Por defecto: ordenado por Monto Total DESC

#### 3. **Análisis de Concentración** (Gráfico de Pareto)

**Configuración:**
- **Eje X:** `Nombre Proveedor` (todos, ordenados por monto)
- **Eje Y Principal (Barras):** `Monto por Proveedor`
- **Eje Y Secundario (Línea):** `% Acumulado`
- **Línea de referencia:** 80% (Principio de Pareto)

**Interpretación:**
- Visualizar cumplimiento del principio 80/20
- Identificar cuántos proveedores representan el 80% del gasto
- Evaluar riesgo de concentración

#### 4. **Distribución de Precios por Proveedor** (Gráfico de Caja y Bigotes)

**Configuración:**
- **Categoría:** `Nombre Proveedor` (Top 20)
- **Valores:** `Precio Promedio Proveedor`
- **Mostrar:** Mediana, cuartiles, outliers

**Análisis:**
- Variabilidad de precios entre proveedores
- Identificar outliers (precios atípicos)
- Comparar rangos de precio para productos similares

#### 5. **Matriz de Proveedor x Producto** (Matriz)

**Configuración:**
- **Filas:** `Nombre Proveedor`
- **Columnas:** `TipoProducto`
- **Valores:** `Monto Transado`
- **Formato condicional:** Escala de colores (blanco → azul oscuro)

**Uso:**
- Identificar especialización de proveedores
- Detectar proveedores multi-categoría
- Evaluar diversificación de cartera

#### 6. **Tendencia de Compras por Proveedor** (Gráfico de Líneas Pequeños Múltiples)

**Configuración:**
- **Eje X:** `Fecha` (mensual)
- **Eje Y:** `Monto por Proveedor`
- **Pequeños múltiples:** Top 10 proveedores (grid 2x5)

**Análisis:**
- Estacionalidad en compras por proveedor
- Identificar proveedores con compras regulares vs esporádicas
- Detectar cambios en patrones de compra

### 🔍 Filtros Específicos del Dashboard

| Filtro | Función |
|--------|---------|
| **🏷️ RUT Proveedor** | Buscar proveedor específico |
| **📊 Rango de Monto** | Filtrar por volumen de compras |
| **📅 Período** | Rango de fechas personalizado |
| **🎯 % Participación** | Umbral mínimo de participación |
| **🗺️ Región Proveedor** | Ubicación geográfica (si disponible) |

### 💼 Casos de Uso

**Caso 1: Evaluación de Proveedor Específico**
```
1. Usar filtro de RUT o buscar en tabla
2. Revisar métricas: monto, participación, frecuencia
3. Analizar evolución temporal en gráfico de tendencia
4. Comparar precio promedio vs competencia
5. Verificar especialización en matriz producto
```

**Caso 2: Análisis de Riesgo de Concentración**
```
1. Revisar KPI "Concentración Top 10"
2. Analizar gráfico de Pareto
3. Identificar proveedores críticos (>10% participación)
4. Evaluar número de proveedores alternativos por categoría
5. Generar recomendaciones de diversificación
```

**Caso 3: Benchmarking de Precios**
```
1. Filtrar por Tipo de Producto específico
2. Revisar gráfico de caja y bigotes
3. Identificar proveedores con precios outliers
4. Comparar precio promedio entre proveedores
5. Detectar oportunidades de negociación
```

### 📊 Métricas de Desempeño

**Indicadores Clave:**
- ✅ **Proveedor Excelente:** >20 OCs/año, precio competitivo, variedad de productos
- 🟡 **Proveedor Regular:** 5-20 OCs/año, precio promedio
- 🔴 **Proveedor Ocasional:** <5 OCs/año, verificar continuidad

---

## 🎯 Dashboard 3: Análisis de Productos

### 🎯 Objetivo

Comprender el comportamiento de compra por producto, identificar productos estratégicos y optimizar inventario.

### 📦 Componentes

#### 1. **KPIs de Productos**

| KPI | Medida | Descripción |
|-----|--------|-------------|
| 📦 **Productos Únicos** | `Número Productos Únicos` | Total de productos diferentes |
| 💰 **Valor Total Stock** | `Valor Stock` | Valor total del inventario |
| 💵 **Precio Prom. General** | `Precio Promedio General` | Precio promedio ponderado |
| 📊 **Productos Clase A** | Cuenta con filtro ABC="A" | Productos que representan 80% ventas |
| 🔄 **Índice de Rotación** | `Índice Rotación` | Frecuencia de compra promedio |

#### 2. **Clasificación ABC de Productos** (Tabla)

**Columnas:**
- **Ranking** - Posición por monto
- **ID Producto** - Identificador único
- **Producto** - Nombre descriptivo
- **Tipo** - Categoría
- **Marca** - Fabricante
- **Monto Total** - Suma de compras
- **% del Total** - Participación
- **% Acumulado** - Acumulado para ABC
- **Clase ABC** - Clasificación A/B/C
- **Cantidad** - Unidades compradas

**Clasificación ABC:**
- 🏆 **Clase A:** Productos que acumulan hasta el 80% del valor (alta rotación)
- 🥈 **Clase B:** Productos entre 80% y 95% acumulado (rotación media)
- 🥉 **Clase C:** Productos que completan el 95-100% (baja rotación)

**Formato condicional:**
```
Clase A → Verde oscuro
Clase B → Amarillo
Clase C → Gris
```

#### 3. **Evolución de Compras por Categoría** (Gráfico de Área Apilada)

**Configuración:**
- **Eje X:** `Fecha` (mensual)
- **Eje Y:** `Monto por Producto`
- **Leyenda:** `TipoProducto`
- **Colores:** Asignados por categoría consistentemente

**Análisis:**
- Estacionalidad por tipo de producto
- Crecimiento/decrecimiento de categorías
- Cambios en composición de compras

#### 4. **Análisis de Precios** (Gráfico de Dispersión)

**Configuración:**
- **Eje X:** `Cantidad por Producto`
- **Eje Y:** `Precio Promedio Producto`
- **Tamaño de burbuja:** `Monto por Producto`
- **Leyenda:** `TipoProducto`
- **Etiquetas:** Mostrar para productos principales

**Interpretación:**
- **Cuadrante superior derecho:** Alta cantidad + Alto precio = Productos estratégicos
- **Cuadrante inferior derecho:** Alta cantidad + Bajo precio = Commodities
- **Cuadrante superior izquierdo:** Baja cantidad + Alto precio = Productos especializados
- **Cuadrante inferior izquierdo:** Baja cantidad + Bajo precio = Productos ocasionales

#### 5. **Top 20 Productos por Monto** (Gráfico de Barras)

**Configuración:**
- **Eje Y:** `Producto` (Top 20)
- **Eje X:** `Monto por Producto`
- **Color:** Por `Clase ABC`
- **Etiquetas de datos:** Monto y %

#### 6. **Variabilidad de Precios** (Gráfico de Barras de Error)

**Configuración:**
- **Eje X:** `Producto` (Top 15 por variabilidad)
- **Valor central:** `Precio Promedio Producto`
- **Barras de error:** ±1 Desviación estándar
- **Uso:** Identificar productos con precios volátiles

#### 7. **Matriz de Productos por Marca** (Matriz)

**Configuración:**
- **Filas:** `Marca`
- **Columnas:** `TipoProducto`
- **Valores:** 
  - `Monto por Producto`
  - `Cantidad por Producto`
  - `Precio Promedio Producto`

### 🔍 Filtros Específicos

| Filtro | Tipo | Uso |
|--------|------|-----|
| **🏷️ Marca** | Desplegable múltiple | Filtrar por fabricante |
| **📦 Tipo Producto** | Lista | Categoría de producto |
| **💰 Rango de Precio** | Deslizador | Filtro por precio promedio |
| **📊 Clase ABC** | Botones | A / B / C |
| **🔍 Búsqueda Producto** | Texto | Buscar por nombre o ID |

### 💼 Casos de Uso

**Caso 1: Identificar Productos Estratégicos**
```
1. Revisar tabla de Clasificación ABC
2. Filtrar solo productos Clase A
3. Analizar en gráfico de dispersión
4. Verificar proveedores en matriz producto-proveedor
5. Evaluar estabilidad de precios
```

**Caso 2: Optimización de Inventario**
```
1. Usar Clasificación ABC para priorizar
2. Clase A → Inventario de seguridad alto
3. Clase B → Inventario moderado
4. Clase C → Compra bajo demanda
5. Revisar índice de rotación
```

**Caso 3: Análisis de Categoría Específica**
```
1. Filtrar por Tipo de Producto
2. Revisar evolución temporal
3. Identificar top productos de la categoría
4. Analizar variabilidad de precios
5. Comparar marcas disponibles
```

**Caso 4: Detección de Anomalías de Precio**
```
1. Revisar gráfico de variabilidad de precios
2. Identificar productos con alta desviación estándar
3. Analizar en tabla detallada las compras
4. Verificar si cambios se deben a:
   - Diferentes proveedores
   - Diferentes modelos/especificaciones
   - Cambios temporales en mercado
5. Generar alerta si necesario
```

### 📈 Métricas de Gestión

**Criterios de evaluación:**
- ✅ **Producto Estratégico (A):** >5% del gasto, alta frecuencia
- 🟡 **Producto Táctico (B):** 1-5% del gasto
- ⚪ **Producto Ocasional (C):** <1% del gasto

---

## 🗺️ Dashboard 4: Análisis Geográfico

### 🎯 Objetivo

Visualizar la distribución geográfica de las compras, identificar patrones regionales y optimizar logística.

### 📦 Componentes

#### 1. **KPIs Geográficos**

| KPI | Medida | Descripción |
|-----|--------|-------------|
| 🗺️ **Regiones Activas** | `COUNT(DISTINCT Region)` | Número de regiones con compras |
| 🏛️ **Comunas Activas** | `COUNT(DISTINCT Comuna Unidad)` | Comunas donde se compra |
| 💰 **Región con Mayor Gasto** | Top 1 por `Monto por Región` | Región líder |
| 📊 **Concentración Regional** | % de top 3 regiones | Concentración geográfica |

#### 2. **Mapa de Chile - Compras por Región** (Mapa Coroplético)

**Configuración:**
- **Ubicación:** `Region` (DimRegiones)
- **Saturación de color:** `Monto por Región`
- **Escala de colores:** Blanco → Azul oscuro
- **Tooltip personalizado:**
  ```
  Región: [Region]
  Monto Total: $[Monto por Región]
  % del Total: [% Distribución por Región]
  Productos: [Número Productos Únicos]
  Proveedores: [Número Proveedores Únicos]
  Precio Promedio: $[Precio Promedio por Región]
  ```

**Interactividad:**
- Clic en región para filtrar otros visuales
- Zoom con scroll del mouse
- Arrastre para desplazar mapa

#### 3. **Ranking de Regiones** (Gráfico de Barras)

**Configuración:**
- **Eje Y:** `Region` (ordenado por monto DESC)
- **Eje X:** `Monto por Región`
- **Etiquetas:** Monto y %
- **Formato condicional:** Degradado de color

#### 4. **Comparación Regional - Métricas Clave** (Tabla)

**Columnas:**
| Columna | Medida | Formato |
|---------|--------|---------|
| **Región** | `Region` | Texto |
| **Monto Total** | `Monto por Región` | $999.999.999 |
| **% del Total** | `% Distribución por Región` | 15,5% |
| **Cantidad** | `Cantidad por Región` | 99.999 |
| **Precio Prom.** | `Precio Promedio por Región` | $9.999 |
| **# Proveedores** | `COUNT(DISTINCT Rut Proveedor)` | 999 |
| **# Productos** | `COUNT(DISTINCT Id)` | 999 |
| **Ticket Prom.** | Monto / # OC | $99.999 |

**Ordenamiento:**
- Por defecto: Monto Total DESC
- Clic en cualquier columna para reordenar

#### 5. **Distribución por Comuna (Top 20)** (Treemap)

**Configuración:**
- **Grupo:** `Comuna Unidad`
- **Valores:** `Monto por Comuna`
- **Saturación:** Cantidad de proveedores
- **Etiqueta:** Comuna y monto

**Interpretación:**
- Tamaño del rectángulo = Monto de compras
- Color más oscuro = Mayor concentración de proveedores

#### 6. **Evolución Temporal por Región** (Gráfico de Líneas)

**Configuración:**
- **Eje X:** `Fecha` (mensual)
- **Eje Y:** `Monto por Región`
- **Leyenda:** `Region` (top 5 regiones)
- **Comparación:** Múltiples líneas

#### 7. **Mapa de Burbujas - Unidades de Compra** (Mapa de Burbujas)

**Configuración:**
- **Ubicación:** `Comuna Unidad` + `Región Unidad`
- **Tamaño:** `Monto Transado`
- **Color:** `TipoProducto` (categoría principal)

### 🔍 Filtros Específicos

| Filtro | Configuración |
|--------|---------------|
| **🗺️ Región** | Segmentador de lista con búsqueda |
| **🏘️ Comuna** | Desplegable dependiente de región |
| **🏛️ Unidad de Compra** | Lista de unidades administrativas |
| **📍 Zona Geográfica** | Norte / Centro / Sur / Extremos |

### 💼 Casos de Uso

**Caso 1: Análisis Regional Completo**
```
1. Revisar mapa coroplético para visión general
2. Identificar regiones con mayor gasto
3. Comparar métricas en tabla regional
4. Analizar evolución temporal de regiones principales
5. Verificar distribución por comuna en treemap
```

**Caso 2: Optimización Logística**
```
1. Identificar regiones con compras frecuentes
2. Analizar mapa de burbujas para ubicación de unidades
3. Evaluar concentración de proveedores por región
4. Considerar centralización de compras en regiones con bajo volumen
5. Proponer contratos marco regionales
```

**Caso 3: Análisis de Precios Regionales**
```
1. Filtrar por producto específico
2. Comparar "Precio Promedio" entre regiones
3. Identificar discrepancias significativas
4. Investigar causas (costos logísticos, proveedores locales)
5. Evaluar oportunidades de estandarización
```

**Caso 4: Expansión de Proveedores**
```
1. Seleccionar región objetivo
2. Revisar # de proveedores activos
3. Identificar categorías con pocos proveedores
4. Comparar con otras regiones similares
5. Generar plan de incorporación de proveedores
```

### 📊 Indicadores de Distribución

**Benchmarks:**
- 🟢 **Distribución balanceada:** No más del 40% en una región
- 🟡 **Concentración moderada:** 40-60% en top 3 regiones
- 🔴 **Alta concentración:** >60% en top 3 regiones

---

## 📅 Dashboard 5: Análisis Temporal

### 🎯 Objetivo

Analizar tendencias históricas, estacionalidad y proyecciones de compras a lo largo del tiempo.

### 📦 Componentes

#### 1. **KPIs Temporales**

| KPI | Medida | Descripción | Formato |
|-----|--------|-------------|---------|
| 📊 **Año Actual** | `Monto Año Actual` | Total del año en curso | $999.999.999 |
| 📉 **Año Anterior** | `Monto Año Anterior` | Total del año previo | $999.999.999 |
| 📈 **Variación YoY** | `Variación % YoY` | Crecimiento anual | +15,5% 🟢 |
| 💰 **Acumulado Año** | `Monto Acumulado Año` | YTD (Year to Date) | $999.999.999 |
| 📅 **Mes Actual** | `Monto Mes Actual` | Total del mes | $99.999.999 |
| 🔄 **Variación MoM** | `Crecimiento Mes a Mes` | Variación mensual | +5,2% 🟢 |

**Indicadores visuales:**
- 🟢 Flecha arriba + verde = Crecimiento positivo
- 🔴 Flecha abajo + rojo = Decrecimiento
- Comparación con período anterior

#### 2. **Línea de Tendencia General** (Gráfico de Líneas con Tendencia)

**Configuración:**
- **Eje X:** `Fecha` (diaria/semanal/mensual según zoom)
- **Eje Y:** `Monto Transado`
- **Línea de tendencia:** Polinómica de grado 2
- **Banda de confianza:** 95%
- **Marcadores:** En puntos de datos

**Análisis de tendencia:**
- Tendencia ascendente sostenida = Crecimiento orgánico
- Tendencia plana = Estabilidad
- Tendencia descendente = Requiere investigación

#### 3. **Comparación Año sobre Año** (Gráfico de Columnas Agrupadas)

**Configuración:**
- **Eje X:** `Mes` (Enero a Diciembre)
- **Eje Y:** `Monto Transado`
- **Leyenda:** `Año` (2022, 2023, 2024, 2025)
- **Colores:** Degradado de azules por año
- **Etiquetas:** Activadas para resaltar diferencias

**Uso:**
- Identificar patrones estacionales repetitivos
- Comparar desempeño entre años
- Detectar meses atípicos

#### 4. **Descomposición Temporal** (Gráfico de Líneas Apiladas)

**Componentes visualizados:**
- **Tendencia:** Línea suavizada (media móvil 3 meses)
- **Estacionalidad:** Patrón repetitivo anual
- **Residual:** Variaciones no explicadas

**Configuración:**
- Usar función de análisis de serie temporal de Power BI
- **Período de estacionalidad:** 12 meses
- **Método:** Descomposición aditiva

#### 5. **Heatmap de Compras** (Matriz con Formato Condicional)

**Configuración:**
- **Filas:** `Año`
- **Columnas:** `Mes`
- **Valores:** `Monto Transado`
- **Formato condicional:** Escala de colores
  - Verde claro = Valores bajos
  - Verde oscuro = Valores altos

**Interpretación rápida:**
- Identificar períodos pico visualmente
- Comparar intensidad entre años
- Detectar anomalías (celdas muy oscuras o muy claras)

#### 6. **Análisis por Trimestre** (Gráfico de Cascada)

**Configuración:**
- **Categoría:** `Trimestre` (Q1, Q2, Q3, Q4)
- **Valores:** 
  - Barra inicial: Trimestre anterior
  - Incremento/Decremento por mes
  - Barra final: Total trimestre
- **Colores:**
  - Verde = Incrementos
  - Rojo = Decrementos
  - Azul = Totales

#### 7. **Proyección de Tendencia** (Gráfico de Líneas con Previsión)

**Configuración:**
- **Datos históricos:** Últimos 24 meses
- **Proyección:** Próximos 6 meses
- **Método:** Suavización exponencial
- **Intervalo de confianza:** 80% y 95%
- **Línea discontinua:** Para valores proyectados

**Disclaimer:** 
⚠️ *Proyecciones basadas en datos históricos. Sujeto a cambios por factores externos.*

#### 8. **Distribución de Compras por Día de la Semana** (Gráfico de Barras)

**Configuración:**
- **Eje X:** `Día de la Semana` (Lun-Dom)
- **Eje Y:** `Número Órdenes Compra`
- **Promedio:** Línea de referencia

**Insights operativos:**
- Días con mayor actividad de compras
- Planificación de carga laboral
- Optimización de procesos

#### 9. **Top 10 Días con Mayor Gasto** (Tabla)

**Columnas:**
- Fecha
- Día de la semana
- Monto Total
- # Órdenes
- Ticket Promedio
- Principal Categoría
- Observaciones

### 🔍 Filtros Específicos

| Filtro | Tipo | Granularidad |
|--------|------|--------------|
| **📅 Año** | Segmentador lista | Anual |
| **📆 Trimestre** | Botones | Q1, Q2, Q3, Q4 |
| **🗓️ Mes** | Timeline slider | Mensual |
| **📊 Rango de Fechas** | Selector rango | Personalizado |
| **🔄 Período Comparación** | Desplegable | Mes anterior, Año anterior, Personalizado |

### 💼 Casos de Uso

**Caso 1: Revisión de Desempeño Anual**
```
1. Seleccionar año a analizar
2. Revisar KPI de Variación YoY
3. Analizar gráfico de comparación año sobre año
4. Identificar meses con mejor/peor desempeño
5. Revisar heatmap para patrones visuales
6. Generar conclusiones y recomendaciones
```

**Caso 2: Planificación Presupuestaria**
```
1. Analizar tendencia histórica (últimos 3 años)
2. Identificar estacionalidad en descomposición temporal
3. Revisar proyección de tendencia
4. Calcular presupuesto mensual considerando:
   - Tendencia de crecimiento
   - Factores estacionales
   - Inflación esperada
5. Distribuir presupuesto anual por trimestre/mes
```

**Caso 3: Análisis de Estacionalidad**
```
1. Usar gráfico de comparación año sobre año
2. Identificar meses consistentemente altos/bajos
3. Revisar heatmap para confirmar patrones
4. Analizar causas (ej: inicio año escolar, fin año fiscal)
5. Ajustar procesos de compra a estacionalidad
```

**Caso 4: Investigación de Anomalías**
```
1. Identificar picos inusuales en gráfico de tendencia
2. Usar Top 10 Días para detallar fechas específicas
3. Filtrar por fecha específica
4. Revisar qué se compró, a qué proveedor, por qué unidad
5. Documentar si es evento único o recurrente
```

**Caso 5: Optimización de Procesos**
```
1. Analizar distribución por día de la semana
2. Identificar días pico de compras
3. Revisar tiempos de procesamiento por día
4. Redistribuir carga laboral
5. Implementar estrategias de compras programadas
```

### 📊 Patrones Temporales Comunes

**Estacionalidad típica en compras públicas chilenas:**

| Período | Patrón Esperado | Causa |
|---------|----------------|-------|
| **Enero-Febrero** | 🔻 Bajo | Período estival, vacaciones |
| **Marzo-Abril** | 🔺 Alto | Inicio año escolar/administrativo |
| **Mayo-Julio** | ➡️ Medio | Actividad normal |
| **Agosto** | 🔺 Alto | Planificación segundo semestre |
| **Septiembre** | ➡️ Medio | Fiestas Patrias |
| **Octubre-Noviembre** | 🔺 Alto | Cierre proyectos anuales |
| **Diciembre** | 🔻 Bajo | Cierre administrativo, vacaciones |

### 📈 Métricas de Evaluación Temporal

**Indicadores de salud:**
- ✅ **Tendencia saludable:** Crecimiento 3-10% anual
- ✅ **Estabilidad:** Variación mensual < ±15%
- ⚠️ **Alerta:** Cambios bruscos >30% sin justificación
- 🔴 **Crítico:** Decrecimiento sostenido >2 trimestres

---

## 🔄 Navegación Entre Dashboards

### Sistema de Navegación

Todos los dashboards incluyen un **panel de navegación** superior con botones:

```
┌────────────────────────────────────────────────────────────┐
│  [🏠 Inicio] [🏢 Proveedores] [🎯 Productos]              │
│  [🗺️ Geográfico] [📅 Temporal]                             │
└────────────────────────────────────────────────────────────┘
```

### Cómo Navegar

**Método 1: Botones de Navegación**
1. Clic en botón del dashboard destino
2. Se carga el dashboard correspondiente
3. Los filtros globales se mantienen (si están sincronizados)

**Método 2: Hipervínculos en Visuales**
- Clic derecho en elemento de gráfico
- "Profundizar" → Lleva a dashboard relacionado
- Ejemplo: Clic en proveedor → Dashboard de Proveedores filtrado

**Método 3: Bookmarks (Marcadores)**
- Panel de vista lateral izquierdo
- Lista de marcadores predefinidos:
  - 📊 Vista Ejecutiva
  - 🏆 Top Performers
  - ⚠️ Alertas y Anomalías
  - 📈 Análisis Mensual
  - 🔍 Drill-down Detallado

### Sincronización de Filtros

**Filtros Globales** (afectan todos los dashboards):
- 📅 Año
- 📆 Rango de Fechas
- 🏛️ Institución

**Filtros Locales** (solo el dashboard actual):
- Filtros específicos de cada análisis
- Se resetean al cambiar de dashboard

**Configuración:**
- Vista > Sincronizar segmentadores
- Seleccionar qué filtros se sincronizan

---

## 📤 Exportación y Compartir

### Opciones de Exportación

#### 1. **Exportar a Excel**

**Desde tabla o visual:**
```
1. Clic derecho en el visual
2. "Exportar datos"
3. Elegir:
   - Datos resumidos (con formato)
   - Datos subyacentes (detalle completo)
4. Guardar archivo .xlsx
```

**Qué se exporta:**
- Datos visibles en el contexto de filtro actual
- Formato de números preservado
- Máximo 150,000 filas (datos subyacentes)

#### 2. **Exportar a PowerPoint**

```
Archivo > Exportar > PowerPoint
```

**Características:**
- Una diapositiva por página del informe
- Visuales como imágenes (no interactivos)
- Incluye filtros aplicados en título
- Útil para presentaciones ejecutivas

**Personalización:**
- Seleccionar páginas específicas
- Incluir/excluir páginas ocultas
- Tamaño de diapositiva: 16:9 o 4:3

#### 3. **Exportar a PDF**

```
Archivo > Exportar a PDF
```

**Opciones:**
- Páginas actuales solamente
- Todas las páginas
- Páginas específicas (1, 3, 5)
- Incluir valores de filtro actuales

**Configuración de página:**
- Tamaño: A4, Carta, Personalizado
- Orientación: Horizontal (recomendado)
- Márgenes: Estrechos

#### 4. **Exportar Visual como Imagen**

```
Clic derecho en visual > Exportar datos > Imagen
```

**Formatos disponibles:**
- PNG (recomendado, alta calidad)
- SVG (vectorial, para edición)
- JPG (menor tamaño archivo)

**Resolución:**
- 1080p (1920x1080) por defecto
- 4K disponible para imágenes de alta calidad

#### 5. **Analizar en Excel (Live Connection)**

```
Desde visual > ... > Analizar en Excel
```

**Requisitos:**
- Excel 2016 o superior
- Conexión al servicio Power BI
- Análisis dinámico en Excel con datos de Power BI

### Publicar en Power BI Service

#### Publicación Inicial

```
1. Archivo > Publicar > Publicar en Power BI
2. Seleccionar área de trabajo
3. Esperar confirmación de carga
4. Clic en "Abrir [nombre] en Power BI"
```

#### Configuración de Actualización

```
En Power BI Service:
1. Ir a Configuración del conjunto de datos
2. Programar actualización:
   - Frecuencia: Diaria
   - Hora: 06:00 AM
   - Zona horaria: (UTC-03:00) Santiago
3. Credenciales de origen de datos
4. Guardar
```

#### Compartir Dashboard

**Método 1: Compartir directo**
```
1. Clic en "Compartir" (icono compartir)
2. Ingresar correos electrónicos
3. Permisos:
   ☑️ Permitir ver
   ☐ Permitir compartir (solo ejecutivos)
   ☐ Permitir crear contenido
4. Agregar mensaje opcional
5. Enviar
```

**Método 2: Enlace de compartir**
```
1. Obtener enlace de compartir
2. Configurar:
   - Solo personas específicas
   - Personas en la organización
   - Cualquiera con el enlace
3. Copiar enlace
4. Distribuir por correo/chat
```

**Método 3: Incrustar en SharePoint/Teams**
```
1. En SharePoint/Teams, agregar web part de Power BI
2. Seleccionar informe
3. Configurar permisos
4. El informe se actualiza automáticamente
```

### Control de Acceso

**Roles recomendados:**

| Rol | Permisos | Usuarios |
|-----|----------|----------|
| **👨‍💼 Administrador** | Editar, compartir, configurar | Jefe de Compras, Analista Senior |
| **📊 Colaborador** | Ver, exportar, comentar | Equipo de Compras |
| **👁️ Lector** | Solo visualizar | Ejecutivos, Auditores |

---

## 💡 Tips y Mejores Prácticas

### Uso Eficiente de los Dashboards

#### 1. **Navegación Rápida**

**Atajos de teclado:**
- `Ctrl + →` / `Ctrl + ←` : Navegar entre páginas
- `Ctrl + F` : Buscar en filtros
- `F11` : Modo pantalla completa
- `Ctrl + Clic` : Selección múltiple en filtros
- `Alt + V` : Limpiar todos los filtros

#### 2. **Filtrado Efectivo**

**Estrategia Top-Down:**
```
1. Empezar con filtros amplios (Año)
2. Agregar filtros específicos (Región, Producto)
3. Analizar resultados
4. Limpiar filtros al cambiar de análisis
```

**Evitar:**
- ❌ Aplicar demasiados filtros simultáneamente
- ❌ Filtros contradictorios (sin resultados)
- ❌ Olvidar filtros activos al interpretar datos

#### 3. **Interpretación de Visuales**

**Gráficos de barras:**
- Leer de arriba abajo (mayor a menor)
- Comparar longitudes, no colores
- Revisar escala del eje

**Gráficos de líneas:**
- Tendencia general > valores individuales
- Identificar patrones y ciclos
- Buscar outliers (picos/valles)

**Mapas:**
- Usar zoom para áreas pequeñas
- Comparar intensidades de color
- Tooltip para valores exactos

**Tablas:**
- Ordenar por columna relevante
- Usar búsqueda para registros específicos
- Exportar para análisis detallado en Excel

#### 4. **Performance y Velocidad**

**Optimizar rendimiento:**
- ✅ Aplicar filtros antes de crear visuales
- ✅ Cerrar dashboards no utilizados
- ✅ Limpiar caché: Archivo > Opciones > Borrar caché
- ✅ Actualizar datos en horarios de baja demanda

**Si el dashboard es lento:**
1. Reducir número de visuales visibles
2. Limitar datos a período relevante (ej: último año)
3. Usar agregaciones predefinidas
4. Consultar con administrador para optimización del modelo

#### 5. **Análisis Combinado**

**Ejemplo de workflow completo:**

```
OBJETIVO: Reducir costos en categoría "Insumos de Oficina"

1. Dashboard Resumen Ejecutivo
   → Identificar que "Insumos Oficina" es 15% del gasto

2. Dashboard Productos
   → Filtrar por categoría
   → Identificar top 10 productos (clasificación ABC)
   → Detectar 3 productos con alta variabilidad de precio

3. Dashboard Proveedores  
   → Analizar quién vende esos productos
   → Comparar precios entre proveedores
   → Identificar proveedor óptimo

4. Dashboard Temporal
   → Revisar patrón de compra mensual
   → Identificar oportunidad de consolidar compras

5. Dashboard Geográfico
   → Verificar si descentralización afecta precios
   → Evaluar centralizar compras en Santiago

RESULTADO: Plan de acción con ahorros proyectados
```

### Mantenimiento y Actualización

#### Frecuencia de Revisión Recomendada

| Dashboard | Frecuencia | Responsable |
|-----------|------------|-------------|
| 📊 Resumen Ejecutivo | Semanal | Jefe de Compras |
| 🏢 Proveedores | Mensual | Analista de Compras |
| 🎯 Productos | Mensual | Analista de Inventario |
| 🗺️ Geográfico | Trimestral | Coordinador Regional |
| 📅 Temporal | Mensual (cierre) | Analista Financiero |

#### Checklist de Calidad de Datos

Antes de análisis críticos, verificar:

- [ ] Datos actualizados (revisar fecha última actualización)
- [ ] No hay valores nulos en campos críticos
- [ ] Totales cuadran con sistemas fuente
- [ ] Relaciones entre tablas funcionan correctamente
- [ ] Medidas DAX devuelven valores coherentes
- [ ] Filtros en estado conocido (limpiar si es necesario)

### Soporte y Ayuda

**Recursos disponibles:**

📚 **Documentación:**
- [01 - Guía de Instalación](01-guia-instalacion.md)
- [02 - Guía de Importación de Datos](02-guia-importacion-datos.md)
- [04 - Diccionario de Datos](04-diccionario-datos.md)
- [05 - Medidas y KPIs](05-medidas-kpis.md)

🆘 **Contacto:**
- Email soporte: [email de soporte técnico]
- Ticket interno: Sistema de tickets interno
- Consultas urgentes: Extensión [número]

---

## ❓ Preguntas Frecuentes

**P: ¿Puedo crear mis propios visuales?**  
R: Sí, si tienes permisos de edición. Archivo > Guardar como > crear tu copia personal.

**P: ¿Los filtros afectan los datos exportados?**  
R: Sí, solo se exportan datos visibles según filtros activos.

**P: ¿Puedo programar envío automático de reportes?**  
R: Sí, desde Power BI Service: Suscribirse > Configurar frecuencia y destinatarios.

**P: ¿Cómo restauro un dashboard a su estado original?**  
R: Clic en "Restablecer" en esquina superior. O eliminar todos los filtros (icono de borrador).

**P: ¿Qué hago si veo datos incorrectos?**  
R: Verificar filtros activos. Si persiste, contactar a administrador con captura de pantalla.

**P: ¿Puedo acceder desde el celular?**  
R: Sí, descargar app "Power BI Mobile" (iOS/Android). Funcionalidad limitada vs escritorio.

**P: ¿Los dashboards se actualizan en tiempo real?**  
R: Depende de configuración. Usualmente actualización diaria programada, no tiempo real.

---

<div align="center">

✅ **Guía de Dashboards Completada**

Ahora tienes el conocimiento para usar efectivamente todos los dashboards del sistema

[⬅️ Guía de Importación](02-guia-importacion-datos.md) | [➡️ Diccionario de Datos](04-diccionario-datos.md)

---

**📊 Análisis de Compras Públicas - Senado de la República de Chile**

*Documentación v1.0 - Febrero 2026*

</div>
