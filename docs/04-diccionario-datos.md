# 📖 Diccionario de Datos

## 📑 Tabla de Contenidos

1. [Introducción](#introducción)
2. [Estructura del Dataset](#estructura-del-dataset)
3. [Campos de Identificación](#campos-de-identificación)
4. [Campos de Proveedores](#campos-de-proveedores)
5. [Campos Institucionales](#campos-institucionales)
6. [Campos de Productos](#campos-de-productos)
7. [Campos Geográficos](#campos-geográficos)
8. [Campos Transaccionales](#campos-transaccionales)
9. [Relaciones Entre Campos](#relaciones-entre-campos)
10. [Reglas de Validación](#reglas-de-validación)
11. [Problemas Comunes y Soluciones](#problemas-comunes-y-soluciones)

---

## 📌 Introducción

Este diccionario de datos proporciona una **descripción completa y detallada** de todos los campos presentes en el dataset de compras públicas del Senado de la República de Chile. Está diseñado para:

- ✅ Facilitar la comprensión de cada campo
- ✅ Establecer reglas de negocio claras
- ✅ Documentar validaciones y restricciones
- ✅ Servir como referencia para análisis de datos
- ✅ Apoyar el desarrollo de medidas DAX

### Convenciones Utilizadas

| Símbolo | Significado |
|---------|-------------|
| 🔑 | Campo clave (identificador único) |
| 📊 | Campo usado en análisis/métricas |
| 🔗 | Campo de relación con otras tablas |
| ⚠️ | Campo con validaciones especiales |
| 💡 | Campo calculado o derivado |
| 📝 | Campo descriptivo/texto libre |

---

## 📋 Estructura del Dataset

### Información General

| Propiedad | Valor |
|-----------|-------|
| **Nombre del Dataset** | ComprasPublicasSenado.xlsx |
| **Origen** | Portal de Compras Públicas de Chile (ChileCompra) |
| **Período Cubierto** | Enero 2022 - Diciembre 2025 |
| **Número de Registros** | ~38,000 transacciones |
| **Número de Campos** | 20 campos |
| **Tamaño Aproximado** | ~15 MB (Excel) / ~8 MB (Power BI) |
| **Actualización** | Mensual |
| **Formato Fuente** | Excel (.xlsx) |

### Categorías de Campos

Los 20 campos se organizan en las siguientes categorías:

```
📂 CAMPOS DE IDENTIFICACIÓN (2)
   ├── Id
   └── Numero OC

📂 CAMPOS DE PROVEEDORES (3)
   ├── Rut Proveedor
   ├── Nombre Proveedor
   └── [Región Proveedor - derivado]

📂 CAMPOS INSTITUCIONALES (4)
   ├── Convenio
   ├── Rut Organismo
   ├── Institución
   └── Unidad de compra

📂 CAMPOS DE PRODUCTOS (5)
   ├── Producto
   ├── TipoProducto
   ├── Modelo
   ├── Marca
   └── Precio Promedio

📂 CAMPOS GEOGRÁFICOS (4)
   ├── Región Unidad
   ├── Comuna Unidad
   ├── Región Medida
   └── Region

📂 CAMPOS TRANSACCIONALES (4)
   ├── Monto Transado
   ├── Cantidad
   ├── Fecha Ultima Venta
   └── [Fecha - derivado]
```

---

## 🔑 Campos de Identificación

### 1. **Id** 🔑

**Nombre técnico:** `Id`  
**Tipo de dato:** Texto  
**Longitud:** Variable (8-12 caracteres)  
**Categoría:** Identificación  
**Obligatorio:** ✅ Sí  
**Único:** ✅ Sí (identificador único de producto)

#### Descripción
Identificador único del producto o ítem comprado en el catálogo de ChileCompra. Este campo permite identificar de manera unívoca cada producto específico.

#### Formato
```
Patrón: Alfanumérico sin formato estándar
Ejemplos:
- "PROD-12345"
- "8562417"
- "IT-LAP-001"
- "ESC-4589"
```

#### Valores Posibles
- Cualquier cadena alfanumérica
- Puede contener guiones, puntos o barras
- Sin espacios al inicio o final

#### Reglas de Negocio
- ✅ Debe ser único en el dataset
- ✅ No puede ser nulo o vacío
- ✅ Se usa como clave primaria en tabla de productos
- ✅ Relaciona transacciones con catálogo de productos

#### Uso en Análisis
- Identificar productos específicos
- Contar productos únicos: `DISTINCTCOUNT(Id)`
- Filtrar transacciones de un producto
- Crear clasificaciones ABC por producto

#### Validaciones
```DAX
// Verificar valores nulos
Productos Sin ID = 
COUNTROWS(
    FILTER(FactCompras, ISBLANK(FactCompras[Id]))
)
// Debe ser 0

// Verificar duplicados (en combinación con fecha/OC)
Verificar Duplicados = 
COUNTROWS(FactCompras) = 
DISTINCTCOUNT(FactCompras[Id] & FactCompras[Numero OC])
// Debe ser TRUE
```

#### Problemas Comunes
| Problema | Causa | Solución |
|----------|-------|----------|
| IDs duplicados | Mismo producto en diferentes OCs | Normal, no es error |
| IDs vacíos | Importación incorrecta | Revisar archivo origen |
| IDs con espacios | Inconsistencia de datos | Aplicar TRIM en Power Query |

---

### 2. **Numero OC** 🔑📊

**Nombre técnico:** `Numero OC`  
**Tipo de dato:** Texto (numérico)  
**Longitud:** Variable (6-10 dígitos)  
**Categoría:** Identificación / Transaccional  
**Obligatorio:** ✅ Sí  
**Único:** ❌ No (una OC puede tener múltiples líneas)

#### Descripción
Número de la Orden de Compra (OC) emitida por el Senado. Una OC puede contener múltiples productos (líneas), por lo que este campo se repite para diferentes productos de la misma orden.

#### Formato
```
Patrón: Numérico de 6-10 dígitos
Ejemplos:
- "4600012345"
- "3500067890"
- "1234567"
```

#### Valores Posibles
- Números enteros positivos
- Generalmente comienzan con dígitos que identifican el organismo
- Sin guiones, puntos o separadores

#### Reglas de Negocio
- ✅ Identifica una transacción de compra específica
- ✅ Puede repetirse en múltiples filas (diferentes productos)
- ✅ Relaciona con sistemas de gestión de compras
- ✅ Único por proveedor y fecha en sistemas origen
- ⚠️ Puede haber OCs con múltiples entregas/fechas

#### Uso en Análisis
- Contar órdenes de compra: `DISTINCTCOUNT(Numero OC)`
- Calcular ticket promedio por OC
- Analizar frecuencia de compra a proveedores
- Rastrear transacciones específicas

#### Medidas DAX Relacionadas
```DAX
// Número total de órdenes de compra
Número Órdenes Compra = 
DISTINCTCOUNT(FactCompras[Numero OC])

// Ticket promedio por OC
Ticket Promedio por OC = 
DIVIDE(
    SUM(FactCompras[Monto Transado]),
    DISTINCTCOUNT(FactCompras[Numero OC]),
    0
)

// Productos promedio por OC
Productos por OC = 
DIVIDE(
    COUNTROWS(FactCompras),
    DISTINCTCOUNT(FactCompras[Numero OC]),
    0
)
```

#### Validaciones
- No puede ser nulo
- Debe ser numérico (aunque almacenado como texto)
- Longitud mínima: 6 caracteres
- Debe existir al menos un registro por OC

#### Problemas Comunes
| Problema | Solución |
|----------|----------|
| OCs con un solo producto | Normal, compras específicas |
| OCs con >50 productos | Verificar si es consolidación, normal en compras masivas |
| Formatos inconsistentes | Estandarizar a texto en Power Query |

---

## 🏢 Campos de Proveedores

### 3. **Rut Proveedor** 🔗📊

**Nombre técnico:** `Rut Proveedor`  
**Tipo de dato:** Texto  
**Longitud:** 10-12 caracteres (incluyendo guion y dígito verificador)  
**Categoría:** Proveedor - Identificación  
**Obligatorio:** ✅ Sí  
**Único:** ❌ No (un proveedor puede tener múltiples transacciones)

#### Descripción
Rol Único Tributario (RUT) del proveedor, identificador fiscal único en Chile. Identifica de manera unívoca a la empresa o persona que provee bienes o servicios.

#### Formato Estándar
```
Patrón: 99.999.999-D
Componentes:
- Número: 7-8 dígitos
- Guion separador: -
- Dígito verificador: 0-9 o K

Ejemplos válidos:
- "76.123.456-7"
- "12.345.678-K"
- "8.765.432-1"
```

#### Formato en Dataset
⚠️ **Importante:** El dataset puede contener RUTs en diferentes formatos:
- Con puntos y guion: "76.123.456-7"
- Sin puntos, con guion: "76123456-7"
- Solo números: "761234567"

#### Reglas de Negocio
- ✅ Identifica únicamente al proveedor
- ✅ Se usa como clave foránea a tabla DimProveedores
- ✅ Mismo RUT = Mismo proveedor (aunque nombre pueda variar ligeramente)
- ✅ Permite agrupar todas las compras de un proveedor
- ⚠️ Validación de dígito verificador según algoritmo chileno

#### Algoritmo de Validación RUT
```
Pasos:
1. Extraer número sin puntos ni guion (ej: 76123456)
2. Invertir el orden de dígitos
3. Multiplicar cada dígito por secuencia 2,3,4,5,6,7 (repetir)
4. Sumar todos los productos
5. Dividir suma por 11 y obtener residuo
6. Dígito verificador = 11 - residuo
   - Si resultado es 11 → DV = 0
   - Si resultado es 10 → DV = K
   - Otro caso → DV = resultado
```

#### Uso en Análisis
- Identificar proveedores únicos
- Agrupar compras por proveedor
- Análisis de concentración de proveedores
- Verificar duplicados de proveedores

#### Medidas DAX Relacionadas
```DAX
// Contar proveedores únicos
Número Proveedores Únicos = 
DISTINCTCOUNT(FactCompras[Rut Proveedor])

// Monto por proveedor
Monto por Proveedor = 
CALCULATE(
    SUM(FactCompras[Monto Transado])
)
```

#### Transformaciones en Power Query
```M
// Estandarizar formato (eliminar puntos, mantener guion)
= Table.TransformColumns(
    Source,
    {"Rut Proveedor", each Text.Replace(Text.Replace(_, ".", ""), " ", ""), type text}
)

// Validar formato básico
= Table.AddColumn(
    #"Paso Anterior",
    "RUT Válido",
    each Text.Length([Rut Proveedor]) >= 9 and Text.Length([Rut Proveedor]) <= 12,
    type logical
)
```

#### Problemas Comunes
| Problema | Causa | Solución |
|----------|-------|----------|
| RUTs sin guion | Importación como número | Convertir a texto, agregar guion |
| Dígito verificador incorrecto | Error de digitación | Validar contra algoritmo |
| Espacios en blanco | Copia desde PDF | Aplicar TRIM() |
| Múltiples formatos | Fuentes de datos diferentes | Estandarizar en Power Query |

---

### 4. **Nombre Proveedor** 📝📊

**Nombre técnico:** `Nombre Proveedor`  
**Tipo de dato:** Texto  
**Longitud:** Variable (5-100 caracteres)  
**Categoría:** Proveedor - Descriptivo  
**Obligatorio:** ✅ Sí  
**Único:** ❌ No (pueden existir ligeras variaciones)

#### Descripción
Razón social o nombre comercial del proveedor. Descripción textual de la empresa o persona que realiza la venta.

#### Formato
```
Tipo: Texto libre
Ejemplos:
- "COMERCIAL DELTA LTDA."
- "EMPRESA NACIONAL S.A."
- "Juan Pérez González EIRL"
- "TECNOLOGÍA AVANZADA SpA"
```

#### Características
- Mayúsculas o capitalización variable
- Puede incluir tipo societario (LTDA, S.A., SpA, EIRL)
- Puede contener caracteres especiales (., &, -)
- Longitud variable según razón social

#### Reglas de Negocio
- ✅ Debe coincidir con el registro oficial del RUT
- ⚠️ Puede tener ligeras variaciones para el mismo RUT
- ✅ Usado para visualizaciones (más legible que RUT)
- ✅ Permite búsqueda y filtrado textual

#### Variaciones Comunes del Mismo Proveedor
```
Ejemplos de variaciones del mismo proveedor:
RUT: 76.123.456-7

Variación 1: "COMERCIAL DELTA LIMITADA"
Variación 2: "COMERCIAL DELTA LTDA"
Variación 3: "COMERCIAL DELTA LTDA."
Variación 4: "Comercial Delta Ltda."

Solución: Usar RUT como identificador único
```

#### Uso en Análisis
- Etiquetas en gráficos y tablas
- Filtros de búsqueda por nombre
- Reportes para usuarios finales
- Ordenamiento alfabético

#### Transformaciones Recomendadas
```M
// Estandarizar a mayúsculas
= Table.TransformColumns(
    Source,
    {"Nombre Proveedor", Text.Upper, type text}
)

// Eliminar espacios extra
= Table.TransformColumns(
    #"Paso Anterior",
    {"Nombre Proveedor", Text.Clean, type text}
)

// Eliminar puntos finales inconsistentes
= Table.TransformColumns(
    #"Paso Anterior",
    {"Nombre Proveedor", each Text.TrimEnd(_, "."), type text}
)
```

#### Medidas DAX Relacionadas
```DAX
// Top 10 proveedores por nombre
Top 10 Proveedores = 
CONCATENATEX(
    TOPN(
        10,
        VALUES(DimProveedores[Nombre Proveedor]),
        [Monto por Proveedor],
        DESC
    ),
    DimProveedores[Nombre Proveedor],
    ", ",
    DimProveedores[Nombre Proveedor],
    ASC
)
```

#### Validaciones
- No puede ser nulo o vacío
- Longitud mínima razonable (> 3 caracteres)
- Debe existir correspondencia con RUT

#### Problemas Comunes
| Problema | Solución |
|----------|----------|
| Nombres con tildes/eñes mal codificadas | Corregir encoding en importación (UTF-8) |
| Abreviaturas inconsistentes | Estandarizar LTDA, LIMITADA, etc. |
| Espacios dobles | Aplicar Text.Clean en Power Query |
| Nombres excesivamente largos | Truncar para visualización, mantener completo en datos |

---

### 5. **[Región Proveedor]** 💡

**Nota:** Este campo NO está presente en el dataset original, pero puede ser derivado o agregado mediante datos externos.

#### Descripción
Región geográfica donde el proveedor tiene su domicilio fiscal registrado.

#### Fuente de Datos
- Servicios web de SII (Servicio de Impuestos Internos)
- Bases de datos complementarias de empresas
- Cruce con registro de proveedores

#### Utilidad
- Análisis de origen de proveedores
- Identificar proveedores locales vs nacionales
- Políticas de fomento a proveedores regionales

---

## 🏛️ Campos Institucionales

### 6. **Convenio** 📊

**Nombre técnico:** `Convenio`  
**Tipo de dato:** Texto  
**Longitud:** Variable (0-50 caracteres)  
**Categoría:** Institucional - Modalidad  
**Obligatorio:** ❌ No  
**Valores Nulos:** ✅ Permitidos (indica compra sin convenio marco)

#### Descripción
Identifica si la compra se realizó mediante un **Convenio Marco** de ChileCompra. Los Convenios Marco son acuerdos de compra pre-negociados con condiciones favorables.

#### Valores Posibles
```
Opciones:
1. [Vacío/Nulo] → Compra directa, sin convenio marco
2. "CM-XXX-YYYY" → Código del convenio marco específico
3. Nombre descriptivo del convenio

Ejemplos:
- "" (vacío)
- "CM-1234-2024"
- "Convenio Marco Tecnología"
- "CM Insumos de Oficina"
```

#### Reglas de Negocio
- ✅ Compras por convenio marco suelen tener mejores precios
- ✅ Proceso más rápido (condiciones pre-negociadas)
- ✅ Proveedores adjudicados en licitación previa
- ❌ No todas las categorías tienen convenio marco disponible

#### Uso en Análisis
- Comparar eficiencia: Convenio Marco vs Compra Directa
- % de compras bajo convenio
- Análisis de ahorros por uso de convenios
- Identificar categorías sin convenio disponible

#### Medidas DAX
```DAX
// Porcentaje de compras con convenio marco
% Compras con Convenio = 
VAR ComprasConvenio = 
    CALCULATE(
        COUNTROWS(FactCompras),
        NOT(ISBLANK(FactCompras[Convenio]))
    )
VAR ComprasTotal = COUNTROWS(FactCompras)
RETURN
    DIVIDE(ComprasConvenio, ComprasTotal, 0)

// Monto ahorrado estimado (hipótesis: 15% ahorro)
Ahorro Estimado Convenio = 
VAR MontoConvenio = 
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        NOT(ISBLANK(FactCompras[Convenio]))
    )
RETURN
    MontoConvenio * 0.15
```

#### Transformaciones Recomendadas
```M
// Categorizar compras
= Table.AddColumn(
    Source,
    "Tipo Compra",
    each if [Convenio] = null or [Convenio] = "" 
         then "Compra Directa" 
         else "Convenio Marco",
    type text
)
```

---

### 7. **Rut Organismo** 🔗

**Nombre técnico:** `Rut Organismo`  
**Tipo de dato:** Texto  
**Longitud:** 10-12 caracteres  
**Categoría:** Institucional - Identificación  
**Obligatorio:** ✅ Sí  
**Único:** ❌ No (típicamente un solo organismo: Senado)

#### Descripción
RUT de la institución compradora (organismo del Estado). En este dataset específico, generalmente corresponde al Senado de la República.

#### Formato
```
Patrón: Similar a RUT Proveedor
Ejemplo:
- "60.910.000-1" (Senado de la República)
```

#### Reglas de Negocio
- ✅ Identifica al organismo comprador
- ✅ En datasets consolidados multi-institucionales, permite filtrar por organismo
- ✅ En este proyecto, usualmente un solo valor (Senado)

#### Uso en Análisis
- Filtrar datos de organismo específico
- Análisis comparativo entre organismos (datasets ampliados)
- Validación de consistencia de datos

---

### 8. **Institución** 📝📊

**Nombre técnico:** `Institución`  
**Tipo de dato:** Texto  
**Longitud:** Variable (10-50 caracteres)  
**Categoría:** Institucional - Descriptivo  
**Obligatorio:** ✅ Sí  
**Valores Típicos:** Senado, Cámara de Diputados, Ministerios, etc.

#### Descripción
Nombre oficial de la institución compradora. Versión textual legible del organismo.

#### Valores Posibles
```
En este dataset:
- "SENADO DE LA REPÚBLICA"
- "Senado"
- "SENADO"

En datasets ampliados:
- "CÁMARA DE DIPUTADOS"
- "MINISTERIO DE HACIENDA"
- "CONTRALORÍA GENERAL DE LA REPÚBLICA"
```

#### Uso en Análisis
- Etiquetas y títulos de reportes
- Filtrado por institución
- Segmentación de análisis

#### Validaciones
- Debe corresponder con Rut Organismo
- Capitalización consistente

---

### 9. **Unidad de compra** 📝📊

**Nombre técnico:** `Unidad de compra`  
**Tipo de dato:** Texto  
**Longitud:** Variable (10-100 caracteres)  
**Categoría:** Institucional - Organizacional  
**Obligatorio:** ✅ Sí  

#### Descripción
Unidad administrativa específica dentro de la institución que realiza la compra. Permite desagregar análisis a nivel departamental.

#### Ejemplos de Valores
```
Unidades típicas del Senado:
- "DEPARTAMENTO DE ADMINISTRACIÓN"
- "OFICINA DE INFORMÁTICA"
- "UNIDAD DE RECURSOS HUMANOS"
- "BIBLIOTECA DEL CONGRESO NACIONAL"
- "COMISIÓN DE HACIENDA"
- "PRESIDENCIA DEL SENADO"
```

#### Características
- Puede haber múltiples unidades por institución
- Nombres pueden variar en formato (mayúsculas, tildes)
- Refleja estructura organizacional

#### Reglas de Negocio
- ✅ Cada unidad tiene autonomía de compra dentro de su presupuesto
- ✅ Permite análisis de gasto por departamento
- ✅ Útil para asignación presupuestaria
- ⚠️ Unidades pueden reorganizarse (nombres cambian en el tiempo)

#### Uso en Análisis
- Ranking de unidades por gasto
- Identificar unidades con mayor actividad de compra
- Análisis de eficiencia por departamento
- Distribución presupuestaria

#### Medidas DAX
```DAX
// Número de unidades de compra activas
Número Unidades Compra = 
DISTINCTCOUNT(FactCompras[Unidad de compra])

// Monto promedio por unidad
Monto Promedio por Unidad = 
DIVIDE(
    SUM(FactCompras[Monto Transado]),
    DISTINCTCOUNT(FactCompras[Unidad de compra]),
    0
)

// Top 5 unidades
Top 5 Unidades = 
CONCATENATEX(
    TOPN(
        5,
        VALUES(FactCompras[Unidad de compra]),
        [Monto por Unidad],
        DESC
    ),
    FactCompras[Unidad de compra],
    ", "
)
```

#### Transformaciones Recomendadas
```M
// Estandarizar nombres
= Table.TransformColumns(
    Source,
    {"Unidad de compra", Text.Upper, type text}
)

// Eliminar prefijos inconsistentes
= Table.TransformColumns(
    #"Paso Anterior",
    {"Unidad de compra", 
     each Text.Replace(Text.Replace(_, "DEPTO.", "DEPARTAMENTO"), "DPTO.", "DEPARTAMENTO"),
     type text}
)
```

#### Problemas Comunes
| Problema | Solución |
|----------|----------|
| Abreviaturas inconsistentes | Estandarizar: DEPTO → DEPARTAMENTO |
| Cambios de nombre por reorganización | Tabla de mapeo histórico |
| Valores muy largos en visualizaciones | Crear campo abreviado para gráficos |

---

## 📦 Campos de Productos

### 10. **Producto** 📝📊

**Nombre técnico:** `Producto`  
**Tipo de dato:** Texto  
**Longitud:** Variable (10-200 caracteres)  
**Categoría:** Producto - Descriptivo  
**Obligatorio:** ✅ Sí  

#### Descripción
Nombre descriptivo completo del producto o servicio adquirido. Descripción textual que identifica el ítem comprado.

#### Formato
```
Tipo: Texto libre descriptivo
Ejemplos:
- "NOTEBOOK LENOVO THINKPAD E14 14 INTEL CORE I5"
- "PAPEL BOND CARTA 75 GR CAJA 10 RESMAS"
- "SERVICIO DE MANTENCIÓN EQUIPOS COMPUTACIONALES"
- "TONER HP CF410A NEGRO LASERJET"
```

#### Características
- Descripción detallada con especificaciones
- Puede incluir marca, modelo, especificaciones técnicas
- Longitud variable según complejidad del producto
- Mayúsculas o capitalización variable

#### Reglas de Negocio
- ✅ Debe ser suficientemente descriptivo para identificar el producto
- ✅ Idealmente incluye características principales
- ⚠️ Puede tener redundancia con campos Marca y Modelo
- ✅ Usado en catálogos y visualizaciones

#### Uso en Análisis
- Búsqueda de productos específicos
- Análisis de texto (palabras clave)
- Etiquetas en tablas detalladas
- Verificación de especificaciones

#### Transformaciones Recomendadas
```M
// Limpiar y estandarizar
= Table.TransformColumns(
    Source,
    {"Producto", each Text.Upper(Text.Clean(_)), type text}
)

// Extraer palabras clave (ejemplo: detectar "NOTEBOOK")
= Table.AddColumn(
    #"Paso Anterior",
    "Categoría Auto",
    each if Text.Contains(Text.Upper([Producto]), "NOTEBOOK") then "NOTEBOOK"
         else if Text.Contains(Text.Upper([Producto]), "PAPEL") then "PAPELERÍA"
         else if Text.Contains(Text.Upper([Producto]), "TONER") then "CONSUMIBLES"
         else "OTRO",
    type text
)
```

---

### 11. **TipoProducto** 📊🔗

**Nombre técnico:** `TipoProducto`  
**Tipo de dato:** Texto  
**Longitud:** Variable (10-50 caracteres)  
**Categoría:** Producto - Clasificación  
**Obligatorio:** ✅ Sí  
**Jerárquico:** ✅ Usado en jerarquías de producto  

#### Descripción
Categoría o clasificación del producto. Agrupa productos similares para análisis consolidado.

#### Valores Posibles
```
Categorías comunes:
- "EQUIPOS COMPUTACIONALES"
- "INSUMOS DE OFICINA"
- "MOBILIARIO"
- "SERVICIOS GENERALES"
- "CONSUMIBLES TECNOLÓGICOS"
- "SOFTWARE Y LICENCIAS"
- "ARTÍCULOS DE ASEO"
- "SERVICIOS PROFESIONALES"
```

#### Reglas de Negocio
- ✅ Define agrupación principal de productos
- ✅ Usado para segmentación de análisis
- ✅ Base para presupuestación por categoría
- ✅ Puede estar estandarizado según catálogo ChileCompra

#### Uso en Análisis
- Análisis de gasto por categoría
- Gráficos de distribución (pie, donut)
- Filtros principales en dashboards
- Comparación entre categorías

#### Medidas DAX
```DAX
// Número de categorías
Número Categorías = 
DISTINCTCOUNT(FactCompras[TipoProducto])

// Categoría principal
Categoría Principal = 
TOPN(
    1,
    VALUES(FactCompras[TipoProducto]),
    [Monto por Producto],
    DESC
)

// % por categoría
% por Categoría = 
VAR MontoCategoria = SUM(FactCompras[Monto Transado])
VAR MontoTotal = 
    CALCULATE(
        SUM(FactCompras[Monto Transado]),
        ALL(FactCompras[TipoProducto])
    )
RETURN
    DIVIDE(MontoCategoria, MontoTotal, 0)
```

#### Problemas Comunes
| Problema | Solución |
|----------|----------|
| Categorías muy específicas (muchas categorías) | Consolidar en macro-categorías |
| Nombres inconsistentes | Estandarizar nomenclatura |
| Productos en múltiples categorías | Definir regla de clasificación principal |

---

### 12. **Modelo** 📝

**Nombre técnico:** `Modelo`  
**Tipo de dato:** Texto  
**Longitud:** Variable (0-50 caracteres)  
**Categoría:** Producto - Especificación  
**Obligatorio:** ❌ No  
**Valores Nulos:** ✅ Permitidos (no todos los productos tienen modelo)

#### Descripción
Modelo específico del producto cuando aplica. Principalmente relevante para equipos tecnológicos, vehículos, maquinaria.

#### Ejemplos
```
Productos con modelo:
- Notebook → "ThinkPad E14"
- Impresora → "LaserJet Pro M404dn"
- Monitor → "S24F350"
- Teléfono → "Galaxy S23"

Productos sin modelo (vacío):
- Papel bond
- Lápices
- Servicios
- Artículos de aseo
```

#### Uso en Análisis
- Comparación de modelos específicos
- Análisis de precios por modelo
- Estándar tecnológico de la institución
- Lifecycle management de equipos

---

### 13. **Marca** 📝📊

**Nombre técnico:** `Marca`  
**Tipo de dato:** Texto  
**Longitud:** Variable (0-30 caracteres)  
**Categoría:** Producto - Especificación  
**Obligatorio:** ❌ No  
**Valores Nulos:** ✅ Permitidos

#### Descripción
Marca o fabricante del producto cuando aplica.

#### Valores Posibles
```
Marcas tecnológicas:
- "HP"
- "LENOVO"
- "DELL"
- "SAMSUNG"
- "MICROSOFT"

Marcas de insumos:
- "XEROX"
- "PILOT"
- "STAEDTLER"
- "GENÉRICA" (productos sin marca)
```

#### Reglas de Negocio
- ⚠️ Puede ser nulo para productos genéricos
- ✅ Importante para productos tecnológicos y estratégicos
- ✅ Usado en políticas de estandarización
- ✅ Análisis de preferencia de marca

#### Uso en Análisis
- Top marcas por gasto
- Análisis de concentración de marca
- Comparación de precios entre marcas
- Políticas de estandarización

#### Medidas DAX
```DAX
// Top 5 marcas
Top 5 Marcas = 
CONCATENATEX(
    TOPN(
        5,
        VALUES(DimProductos[Marca]),
        [Monto por Marca],
        DESC
    ),
    DimProductos[Marca],
    ", "
)
```

---

### 14. **Precio Promedio** 💰📊

**Nombre técnico:** `Precio Promedio`  
**Tipo de dato:** Número decimal  
**Formato:** Moneda (Pesos Chilenos)  
**Categoría:** Producto - Transaccional  
**Obligatorio:** ✅ Sí  
**Rango:** > 0

#### Descripción
Precio unitario promedio del producto en la transacción específica. Representa el costo por unidad.

#### Formato
```
Tipo: Decimal (2 decimales)
Rango típico: $100 - $5.000.000
Ejemplos:
- $500 (lápices)
- $2.500 (resma de papel)
- $550.000 (notebook)
- $1.200.000 (monitor profesional)
```

#### Cálculo
```
Precio Promedio = Monto Transado / Cantidad

Ejemplo:
Monto Transado: $1.500.000
Cantidad: 3 unidades
Precio Promedio: $500.000 por unidad
```

#### Reglas de Negocio
- ✅ Debe ser > 0
- ✅ Debe ser coherente con Monto Transado y Cantidad
- ✅ Usado para comparación de precios
- ⚠️ Puede variar entre transacciones del mismo producto (diferentes proveedores, fechas)

#### Uso en Análisis
- Benchmarking de precios
- Identificación de outliers de precio
- Análisis de tendencia de precios en el tiempo
- Comparación entre proveedores

#### Medidas DAX
```DAX
// Precio promedio general
Precio Promedio General = 
AVERAGE(FactCompras[Precio Promedio])

// Precio mínimo y máximo
Precio Mínimo = MIN(FactCompras[Precio Promedio])
Precio Máximo = MAX(FactCompras[Precio Promedio])

// Variabilidad de precio
Desviación Precio = 
STDEV.P(FactCompras[Precio Promedio])
```

#### Validaciones
```DAX
// Verificar coherencia
Verificar Precio = 
SUMX(
    FactCompras,
    IF(
        ABS([Monto Transado] - ([Precio Promedio] * [Cantidad])) > 10,
        1,
        0
    )
)
// Debe ser 0 (tolerancia de $10 por redondeos)
```

---

## 🗺️ Campos Geográficos

### 15. **Región Unidad** 🗺️📊

**Nombre técnico:** `Región Unidad`  
**Tipo de dato:** Texto  
**Longitud:** Variable (10-40 caracteres)  
**Categoría:** Geográfico  
**Obligatorio:** ✅ Sí  

#### Descripción
Región de Chile donde se ubica la unidad de compra que realiza la adquisición.

#### Valores Posibles (Regiones de Chile)
```
Regiones válidas (16 regiones):
- "REGIÓN DE ARICA Y PARINACOTA"
- "REGIÓN DE TARAPACÁ"
- "REGIÓN DE ANTOFAGASTA"
- "REGIÓN DE ATACAMA"
- "REGIÓN DE COQUIMBO"
- "REGIÓN DE VALPARAÍSO"
- "REGIÓN METROPOLITANA DE SANTIAGO"
- "REGIÓN DEL LIBERTADOR GENERAL BERNARDO O'HIGGINS"
- "REGIÓN DEL MAULE"
- "REGIÓN DE ÑUBLE"
- "REGIÓN DEL BIOBÍO"
- "REGIÓN DE LA ARAUCANÍA"
- "REGIÓN DE LOS RÍOS"
- "REGIÓN DE LOS LAGOS"
- "REGIÓN DE AYSÉN DEL GENERAL CARLOS IBÁÑEZ DEL CAMPO"
- "REGIÓN DE MAGALLANES Y DE LA ANTÁRTICA CHILENA"
```

#### Formatos Alternativos
```
Formato completo:
- "REGIÓN METROPOLITANA DE SANTIAGO"

Formato abreviado:
- "METROPOLITANA"
- "RM"

Formato con número:
- "XIII REGIÓN METROPOLITANA"
```

#### Reglas de Negocio
- ✅ Debe ser una región válida de Chile
- ✅ Usado para análisis geográfico
- ✅ Permite mapas coropléticos
- ⚠️ Formato debe ser consistente para visualizaciones

#### Uso en Análisis
- Distribución geográfica de compras
- Mapas de Chile por región
- Análisis regional de gasto
- Comparación entre regiones

#### Transformaciones Recomendadas
```M
// Estandarizar nombres de regiones
= Table.TransformColumns(
    Source,
    {"Región Unidad", each 
        if Text.Contains(_, "METROPOLITANA") then "REGIÓN METROPOLITANA"
        else if Text.Contains(_, "VALPARAÍSO") then "REGIÓN DE VALPARAÍSO"
        // ... más transformaciones
        else _,
    type text}
)

// Tabla de mapeo (recomendado)
MapeoRegiones = Table.FromRecords({
    [Original = "RM", Estandar = "REGIÓN METROPOLITANA"],
    [Original = "METROPOLITANA", Estandar = "REGIÓN METROPOLITANA"],
    [Original = "REGIÓN METROPOLITANA DE SANTIAGO", Estandar = "REGIÓN METROPOLITANA"]
    // ... más mapeos
})
```

---

### 16. **Comuna Unidad** 🗺️

**Nombre técnico:** `Comuna Unidad`  
**Tipo de dato:** Texto  
**Longitud:** Variable (5-30 caracteres)  
**Categoría:** Geográfico  
**Obligatorio:** ✅ Sí  

#### Descripción
Comuna específica donde se ubica la unidad de compra dentro de la región.

#### Ejemplos
```
Región Metropolitana:
- "SANTIAGO"
- "PROVIDENCIA"
- "LAS CONDES"
- "MAIPÚ"
- "VALPARAÍSO" → Error, pertenece a otra región

Región de Valparaíso:
- "VALPARAÍSO"
- "VIÑA DEL MAR"
- "CONCÓN"
```

#### Reglas de Negocio
- ✅ Debe pertenecer a la Región Unidad correspondiente
- ✅ Total de 346 comunas en Chile
- ✅ Permite análisis granular geográfico

#### Validaciones
- Comuna debe ser válida
- Comuna debe pertenecer a la región indicada
- No puede ser nula

---

### 17. **Región Medida** 🗺️

**Nombre técnico:** `Región Medida`  
**Tipo de dato:** Texto  
**Longitud:** Variable (5-40 caracteres)  
**Categoría:** Geográfico  
**Obligatorio:** ❓ Depende del contexto  

#### Descripción
Campo que puede referirse a la región donde se mide o entrega el producto. En algunos contextos, puede ser redundante con "Región Unidad".

#### Uso
- Puede indicar región de entrega si difiere de región de compra
- En análisis logísticos
- Puede ser igual a Región Unidad en muchos casos

---

### 18. **Region** 🗺️📊

**Nombre técnico:** `Region`  
**Tipo de dato:** Texto  
**Categoría:** Geográfico  
**Obligatorio:** ✅ Sí  

#### Descripción
Campo de región estandarizado usado en visualizaciones. Puede ser versión normalizada de "Región Unidad" o "Región Medida".

#### Diferencia con otros campos de región
```
Región Unidad → Puede tener formatos variables
Region → Versión estandarizada para análisis

Ejemplo:
Región Unidad: "REGIÓN METROPOLITANA DE SANTIAGO"
Region: "METROPOLITANA"
```

#### Uso en Análisis
- Campo principal para mapas y visualizaciones geográficas
- Filtros de región
- Agrupación geográfica

---

## 💰 Campos Transaccionales

### 19. **Monto Transado** 💰📊🔑

**Nombre técnico:** `Monto Transado`  
**Tipo de dato:** Número decimal  
**Formato:** Moneda (Pesos Chilenos)  
**Categoría:** Transaccional - Financiero  
**Obligatorio:** ✅ Sí  
**Rango:** > 0

#### Descripción
Valor total en pesos chilenos de la línea de compra. Representa el costo total de la transacción (Precio Unitario × Cantidad).

#### Formato
```
Tipo: Decimal (0-2 decimales)
Rango típico: $1.000 - $50.000.000
Ejemplos:
- $15.000 (compra menor)
- $850.000 (compra mediana)
- $12.500.000 (compra mayor)
```

#### Cálculo
```
Monto Transado = Precio Promedio × Cantidad

Ejemplo:
Precio Promedio: $500.000
Cantidad: 10 unidades
Monto Transado: $5.000.000
```

#### Reglas de Negocio
- ✅ Campo más importante para análisis financiero
- ✅ Base de todos los KPIs monetarios
- ✅ Debe ser coherente con Precio Promedio × Cantidad
- ✅ Incluye IVA (19% en Chile)
- ⚠️ Puede haber descuentos aplicados

#### Uso en Análisis
- **KPI Principal:** Suma total de compras
- Ranking de proveedores/productos
- Análisis de tendencias
- Presupuesto vs ejecutado
- Prácticamente todas las medidas financieras

#### Medidas DAX Principales
```DAX
// Total general
Total Monto Transado = 
SUM(FactCompras[Monto Transado])

// Promedio por transacción
Monto Promedio Transacción = 
AVERAGE(FactCompras[Monto Transado])

// Máximo y mínimo
Monto Máximo = MAX(FactCompras[Monto Transado])
Monto Mínimo = MIN(FactCompras[Monto Transado])
```

#### Validaciones
```DAX
// Verificar valores negativos
Montos Negativos = 
COUNTROWS(
    FILTER(FactCompras, FactCompras[Monto Transado] <= 0)
)
// Debe ser 0

// Verificar coherencia con precio y cantidad
Incoherencias Monto = 
COUNTROWS(
    FILTER(
        FactCompras,
        ABS([Monto Transado] - ([Precio Promedio] * [Cantidad])) > 100
    )
)
```

---

### 20. **Cantidad** 📦📊

**Nombre técnico:** `Cantidad`  
**Tipo de dato:** Número entero  
**Categoría:** Transaccional - Volumen  
**Obligatorio:** ✅ Sí  
**Rango:** ≥ 1

#### Descripción
Número de unidades compradas del producto en la transacción específica.

#### Formato
```
Tipo: Número entero positivo
Rango típico: 1 - 10,000
Ejemplos:
- 1 (equipo único)
- 50 (resmas de papel)
- 500 (lápices)
- 5,000 (folletos impresos)
```

#### Reglas de Negocio
- ✅ Debe ser ≥ 1
- ✅ Números enteros (no decimales típicamente)
- ✅ Unidad depende del producto (unidades, cajas, kilos, etc.)
- ⚠️ Puede variar la unidad de medida según producto

#### Uso en Análisis
- Volumen de compras
- Análisis de cantidades vs montos
- Inventario y stock
- Frecuencia de compra

#### Medidas DAX
```DAX
// Total cantidad productos
Total Cantidad Productos = 
SUM(FactCompras[Cantidad])

// Cantidad promedio por transacción
Cantidad Promedio = 
AVERAGE(FactCompras[Cantidad])
```

---

### 21. **Fecha Ultima Venta** 📅📊

**Nombre técnico:** `Fecha Ultima Venta`  
**Tipo de dato:** Fecha  
**Formato:** DD/MM/YYYY o DD-MM-YYYY  
**Categoría:** Transaccional - Temporal  
**Obligatorio:** ✅ Sí  

#### Descripción
Fecha en que se realizó la transacción de compra.

#### Formato
```
Patrón: DD/MM/YYYY
Ejemplos:
- 15/03/2024
- 01/01/2023
- 31/12/2025
```

#### Rango de Fechas
```
Mínimo: 01/01/2022 (aprox.)
Máximo: 31/12/2025 (aprox.)
Período: ~4 años de datos
```

#### Reglas de Negocio
- ✅ Debe estar dentro del rango de datos
- ✅ No puede ser fecha futura (más allá de hoy)
- ✅ Usado para análisis temporal
- ✅ Base para tabla DimCalendario

#### Uso en Análisis
- Series de tiempo
- Análisis de tendencias
- Estacionalidad
- Comparaciones YoY, MoM
- Filtros de período

#### Transformaciones en Power Query
```M
// Convertir a tipo fecha
= Table.TransformColumnTypes(
    Source,
    {{"Fecha Ultima Venta", type date}}
)

// Extraer componentes
= Table.AddColumn(Source, "Año", each Date.Year([Fecha Ultima Venta]), Int64.Type)
= Table.AddColumn(#"Paso Anterior", "Mes", each Date.Month([Fecha Ultima Venta]), Int64.Type)
= Table.AddColumn(#"Paso Anterior", "Trimestre", each Date.QuarterOfYear([Fecha Ultima Venta]), Int64.Type)
```

---

## 🔗 Relaciones Entre Campos

### Modelo de Datos Recomendado

```
DimCalendario (Tabla Calendario)
    ├── Fecha (clave primaria)
    ├── Año
    ├── Trimestre
    ├── Mes
    ├── Día
    └── ... más campos

FactCompras (Tabla de Hechos) ← TABLA PRINCIPAL
    ├── Id (FK a DimProductos)
    ├── Numero OC
    ├── Rut Proveedor (FK a DimProveedores)
    ├── Rut Organismo (FK a DimOrganismos)
    ├── Fecha Ultima Venta (FK a DimCalendario)
    ├── Monto Transado (medida)
    ├── Cantidad (medida)
    ├── Precio Promedio (medida)
    └── ... campos descriptivos

DimProveedores
    ├── Rut Proveedor (clave primaria)
    ├── Nombre Proveedor
    └── [otros atributos del proveedor]

DimProductos
    ├── Id (clave primaria)
    ├── Producto
    ├── TipoProducto
    ├── Marca
    ├── Modelo
    └── [otros atributos del producto]

DimRegiones
    ├── Region (clave primaria)
    ├── Comuna
    └── [otros atributos geográficos]

DimOrganismos
    ├── Rut Organismo (clave primaria)
    ├── Institución
    ├── Unidad de compra
    └── [otros atributos]
```

### Relaciones Clave

| Tabla Origen | Campo | Tabla Destino | Campo | Cardinalidad | Dirección Filtro |
|--------------|-------|---------------|-------|--------------|------------------|
| FactCompras | Fecha Ultima Venta | DimCalendario | Fecha | Muchos a Uno | Ambas |
| FactCompras | Rut Proveedor | DimProveedores | Rut Proveedor | Muchos a Uno | Ambas |
| FactCompras | Id | DimProductos | Id | Muchos a Uno | Ambas |
| FactCompras | Region | DimRegiones | Region | Muchos a Uno | Ambas |

---

## ✅ Reglas de Validación

### Validaciones de Integridad

```DAX
// 1. Verificar registros sin ID
Registros Sin ID = 
COUNTROWS(FILTER(FactCompras, ISBLANK([Id])))
// Esperado: 0

// 2. Verificar montos negativos o cero
Montos Inválidos = 
COUNTROWS(FILTER(FactCompras, [Monto Transado] <= 0))
// Esperado: 0

// 3. Verificar cantidades inválidas
Cantidades Inválidas = 
COUNTROWS(FILTER(FactCompras, [Cantidad] < 1))
// Esperado: 0

// 4. Verificar coherencia Monto = Precio × Cantidad
Incoherencias = 
COUNTROWS(
    FILTER(
        FactCompras,
        ABS([Monto Transado] - ([Precio Promedio] * [Cantidad])) > 100
    )
)
// Esperado: 0 (o muy bajo, por redondeos)

// 5. Verificar fechas futuras
Fechas Futuras = 
COUNTROWS(FILTER(FactCompras, [Fecha Ultima Venta] > TODAY()))
// Esperado: 0

// 6. Verificar RUT Proveedor con formato
RUT Inválidos = 
COUNTROWS(
    FILTER(
        FactCompras,
        LEN([Rut Proveedor]) < 9 || NOT(CONTAINS([Rut Proveedor], "-"))
    )
)
```

---

## ⚠️ Problemas Comunes y Soluciones

### Problemas de Calidad de Datos

| Problema | Síntoma | Causa Probable | Solución |
|----------|---------|----------------|----------|
| **Valores nulos** | Campos vacíos en tabla | Importación incompleta | Filtrar filas con valores nulos en Power Query |
| **Duplicados** | Misma transacción varias veces | Error en fuente | Eliminar duplicados por clave compuesta (OC + Id) |
| **Formatos inconsistentes** | RUTs con/sin puntos, fechas mal formateadas | Múltiples fuentes | Estandarizar en Power Query |
| **Montos descuadrados** | Monto ≠ Precio × Cantidad | Descuentos, redondeos | Recalcular o aceptar tolerancia |
| **Regiones mal escritas** | Visualizaciones geográficas fallan | Errores de tipeo | Tabla de mapeo estandarizada |
| **Outliers de precio** | Precios extremadamente altos/bajos | Error de digitación o producto especial | Investigar manualmente, corregir o documentar |

### Scripts de Limpieza Power Query

```M
// Script completo de limpieza
let
    // 1. Cargar datos
    Fuente = Excel.Workbook(File.Contents("ruta/datos.xlsx"), null, true),
    Hoja = Fuente{[Item="Compras",Kind="Sheet"]}[Data],
    
    // 2. Promover encabezados
    Encabezados = Table.PromoteHeaders(Hoja, [PromoteAllScalars=true]),
    
    // 3. Eliminar filas vacías
    SinVacios = Table.SelectRows(Encabezados, each [Id] <> null and [Id] <> ""),
    
    // 4. Cambiar tipos de datos
    TiposDatos = Table.TransformColumnTypes(SinVacios,{
        {"Id", type text},
        {"Numero OC", type text},
        {"Monto Transado", type number},
        {"Cantidad", Int64.Type},
        {"Precio Promedio", type number},
        {"Fecha Ultima Venta", type date}
    }),
    
    // 5. Estandarizar RUT
    EstandarizarRUT = Table.TransformColumns(TiposDatos,{
        {"Rut Proveedor", each Text.Replace(Text.Replace(_, ".", ""), " ", ""), type text}
    }),
    
    // 6. Limpiar textos (trim, upper)
    LimpiarTextos = Table.TransformColumns(EstandarizarRUT,{
        {"Nombre Proveedor", each Text.Upper(Text.Trim(_)), type text},
        {"Producto", each Text.Upper(Text.Trim(_)), type text}
    }),
    
    // 7. Validar montos positivos
    FiltrarMontos = Table.SelectRows(LimpiarTextos, each [Monto Transado] > 0 and [Cantidad] >= 1)
    
in
    FiltrarMontos
```

---

<div align="center">

✅ **Diccionario de Datos Completo**

Referencia integral de todos los campos del dataset de compras públicas

[⬅️ Guía de Dashboards](03-guia-uso-dashboards.md) | [➡️ Medidas y KPIs](05-medidas-kpis.md)

---

**📖 Análisis de Compras Públicas - Senado de la República de Chile**

*Documentación v1.0 - Febrero 2026*

</div>
