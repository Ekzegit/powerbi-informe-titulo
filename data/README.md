# 📊 Datos de Ejemplo

## 📁 Contenido de esta Carpeta

Esta carpeta contiene archivos de datos de ejemplo para probar y validar la solución de Power BI.

### Archivos Disponibles

| Archivo | Descripción | Registros | Tamaño |
|---------|-------------|-----------|--------|
| `estructura-ejemplo.csv` | Datos de muestra de compras públicas | 30 | ~7.5 KB |

---

## 📄 estructura-ejemplo.csv

### Descripción

Archivo CSV con **30 registros de ejemplo** que representan compras públicas de productos de aseo realizadas por el Senado de la República de Chile.

### Características

- ✅ **Formato:** CSV (delimitado por comas)
- ✅ **Codificación:** UTF-8
- ✅ **Encabezados:** Primera fila contiene nombres de columnas
- ✅ **Separador:** Coma (,)
- ✅ **Datos:** Basados en estructura real de compras públicas

### Estructura de Columnas

El archivo contiene **20 columnas**:

```
1.  Convenio              - Tipo de convenio (ASEO)
2.  Rut Proveedor         - RUT del proveedor (formato con guiones)
3.  Nombre Proveedor      - Razón social del proveedor
4.  Rut Organismo         - RUT de la institución
5.  Institución           - SENADO DE LA REPUBLICA
6.  Unidad de compra      - Departamento que compra
7.  Región Unidad         - Región de la unidad compradora
8.  Comuna Unidad         - Comuna de la unidad
9.  Id                    - ID único del producto (PROD001, PROD002, etc.)
10. Producto              - Descripción completa del producto
11. TipoProducto          - Categoría del producto
12. Modelo                - Características/especificaciones
13. Marca                 - Marca comercial
14. Región Medida         - Región asociada al producto
15. Region                - Código de región (RM, VAL, BIO, etc.)
16. Monto Transado        - Monto total de la transacción
17. Numero OC             - Número de orden de compra (OC-2024-XXX)
18. Precio Promedio       - Precio unitario promedio
19. Cantidad              - Cantidad de unidades compradas
20. Fecha Ultima Venta    - Fecha en formato DD-MM-YYYY
```

### Proveedores Incluidos

El archivo de ejemplo incluye 3 proveedores diferentes:

1. **PRISA S.A.** (RUT: 76123456-7)
   - Productos de papel (higiénico, toallas, servilletas)
   - Implementos de aseo
   - Dispensadores

2. **DIMERC S.A.** (RUT: 87654321-8)
   - Productos de limpieza (jabón, cloro, detergente)
   - Químicos de aseo
   - Productos desinfectantes

3. **MG PUBLICIDAD Y SERVICIOS GENERALES LIMITADA** (RUT: 98765432-1)
   - Bolsas de basura
   - Guantes y protección
   - Productos varios de aseo

### Regiones Representadas

- 🗺️ **Región Metropolitana (RM)** - Mayoría de las compras
- 🗺️ **Región de Valparaíso (VAL)** - 2 registros
- 🗺️ **Región del Biobío (BIO)** - 2 registros
- 🗺️ **Región de la Araucanía (ARA)** - 1 registro

### Tipos de Productos Incluidos

- 📄 Papel Higiénico
- 🧻 Toallas de Papel
- 🧴 Jabones y Detergentes
- 🧽 Implementos de Limpieza
- 🗑️ Bolsas de Basura
- 🧤 Guantes
- 🧼 Desinfectantes y Químicos
- 🪣 Accesorios de Aseo

### Rango de Fechas

- **Fecha más antigua:** 15-03-2024
- **Fecha más reciente:** 18-05-2024
- **Período:** Marzo - Mayo 2024 (3 meses)

### Rango de Montos

- **Monto mínimo:** $4,500
- **Monto máximo:** $50,000
- **Total aproximado:** $567,000

---

## 🚀 Cómo Usar el Archivo de Ejemplo

### Opción 1: Importar Directamente el CSV

```
1. Abrir Power BI Desktop
2. Inicio > Obtener datos > Texto/CSV
3. Seleccionar "estructura-ejemplo.csv"
4. Clic en "Transformar datos"
5. Aplicar las transformaciones del script Power Query
```

### Opción 2: Convertir a Excel

```
1. Abrir "estructura-ejemplo.csv" en Excel
2. Archivo > Guardar como
3. Tipo: "Libro de Excel (.xlsx)"
4. Importar a Power BI usando "Obtener datos > Excel"
```

### Opción 3: Usar como Plantilla

```
1. Abrir el archivo en Excel
2. Reemplazar las filas de datos con tus datos reales
3. Mantener exactamente la misma estructura de columnas
4. Guardar y usar para importar a Power BI
```

---

## 📋 Preparación de tus Datos Reales

### Formato Requerido

Para que tus datos funcionen con los scripts proporcionados:

#### Estructura de Archivo

✅ **Correcto:**
```csv
Convenio,Rut Proveedor,Nombre Proveedor,Rut Organismo,...
ASEO,76123456-7,PRISA S.A.,60123789-0,...
ASEO,87654321-8,DIMERC S.A.,60123789-0,...
```

❌ **Incorrecto:**
- Columnas en diferente orden (Power Query se ajustará, pero mejor mantener el orden)
- Nombres de columnas diferentes
- Separadores diferentes (punto y coma en lugar de coma)

#### Formato de Fechas

✅ **Correcto:**
```
15-03-2024
01-04-2024
28-05-2024
```

❌ **Incorrecto:**
```
03/15/2024  (formato americano)
2024-03-15  (formato ISO)
15/03/2024  (con barras en lugar de guiones)
```

#### Formato de RUTs

✅ **Aceptable (se limpiarán automáticamente):**
```
76.123.456-7
76123456-7
761234567
```

Todos se convertirán a: `761234567`

#### Formato de Montos

✅ **Aceptable:**
```
48000
48.000
48000.00
```

Todos se convertirán a número decimal.

---

## 🔍 Validación de Datos

Antes de importar tus datos reales, verificar:

### Checklist de Validación

- [ ] **Encabezados:** Primera fila contiene los 20 nombres de columnas
- [ ] **Formato:** Archivo es .csv o .xlsx
- [ ] **Codificación:** UTF-8 (sin caracteres raros)
- [ ] **Separador:** Comas para CSV
- [ ] **Fechas:** Formato DD-MM-YYYY
- [ ] **Números:** Sin símbolos de moneda ($), solo números
- [ ] **Cantidad de datos:** Aproximadamente 38,000 registros
- [ ] **Sin filas vacías** al inicio o final
- [ ] **Sin columnas extra** no documentadas

### Prueba Rápida

1. Abrir el archivo en Excel
2. Verificar que se ve bien
3. Filtro automático en encabezados
4. Revisar últimas filas (no deben estar vacías)
5. Buscar caracteres extraños (�, ?, etc.)

---

## 📊 Estadísticas del Archivo de Ejemplo

### Resumen de Datos

| Métrica | Valor |
|---------|-------|
| Total de Registros | 30 |
| Proveedores Únicos | 3 |
| Productos Únicos | 23 |
| Regiones Diferentes | 4 |
| Tipos de Producto | 15 |
| Órdenes de Compra | 23 |
| Monto Total Transado | $567,000 |
| Cantidad Total Productos | 465 unidades |
| Precio Promedio | ~$1,220 |

### Distribución por Proveedor

| Proveedor | Registros | Monto Total | % del Total |
|-----------|-----------|-------------|-------------|
| PRISA S.A. | 13 | $293,000 | 51.7% |
| DIMERC S.A. | 11 | $197,500 | 34.8% |
| MG PUBLICIDAD | 6 | $76,500 | 13.5% |

### Distribución por Región

| Región | Registros | Monto Total |
|--------|-----------|-------------|
| Metropolitana (RM) | 25 | $511,000 |
| Valparaíso (VAL) | 2 | $78,000 |
| Biobío (BIO) | 2 | $36,000 |
| Araucanía (ARA) | 1 | $16,000 |

---

## 💡 Casos de Uso

### Caso 1: Aprendizaje y Práctica

```
Objetivo: Aprender Power BI sin datos reales
Uso: Importar estructura-ejemplo.csv
Resultado: Poder probar todas las funcionalidades sin datos sensibles
```

### Caso 2: Validación de Scripts

```
Objetivo: Verificar que los scripts Power Query funcionan
Uso: Aplicar transformaciones al archivo de ejemplo
Resultado: Confirmar que el proceso de ETL está correcto
```

### Caso 3: Demo para Evaluadores

```
Objetivo: Mostrar la solución en examen de título
Uso: Presentar dashboards con datos de ejemplo
Resultado: Demostrar capacidades sin exponer datos reales
```

### Caso 4: Plantilla para Datos Reales

```
Objetivo: Preparar archivo para importación masiva
Uso: Copiar estructura y reemplazar datos
Resultado: Archivo listo para importar 38,000 registros
```

---

## ⚠️ Limitaciones

### Datos de Ejemplo

- 📌 **Solo 30 registros** (vs. 38,000 reales)
- 📌 Datos **ficticios** pero realistas
- 📌 Montos y fechas **ilustrativos**
- 📌 No representa patrones reales completos
- 📌 Para **fines educativos** únicamente

### Análisis Limitado

Con solo 30 registros:
- ❌ Análisis de tendencias limitado (pocas fechas)
- ❌ Clasificación ABC poco representativa
- ❌ Patrones estacionales no visibles
- ✅ Estructura del modelo completa
- ✅ Todas las funcionalidades probables
- ✅ Relaciones funcionan correctamente

---

## 🔗 Recursos Relacionados

### Documentación

- 📘 [Guía de Importación de Datos](../docs/02-guia-importacion-datos.md) - Cómo importar este archivo
- 📕 [Diccionario de Datos](../docs/04-diccionario-datos.md) - Descripción de cada columna
- 📄 [README Principal](../README.md) - Documentación del proyecto

### Scripts

- 🔧 [Transformaciones Power Query](../powerbi/scripts/power-query-transformaciones.m) - Scripts de ETL
- 📊 [Medidas DAX](../powerbi/scripts/medidas-dax.dax) - Fórmulas de análisis

---

## ❓ Preguntas Frecuentes

**P: ¿Puedo modificar el archivo de ejemplo?**  
R: Sí, puedes agregar o modificar registros manteniendo la estructura de columnas.

**P: ¿Los datos son reales?**  
R: No, son datos ficticios basados en la estructura real de compras públicas.

**P: ¿Puedo usarlo en mi presentación?**  
R: Sí, está diseñado para uso educativo y demostraciones.

**P: ¿Dónde consigo los 38,000 registros reales?**  
R: Debes obtenerlos del sistema de compras públicas real o generar un dataset más grande siguiendo esta estructura.

**P: ¿Por qué hay solo 30 registros?**  
R: Para facilitar la revisión manual y pruebas rápidas. Un archivo grande sería difícil de inspeccionar.

---

<div align="center">

📊 **Datos Listos para Usar**

Archivo de ejemplo perfecto para pruebas y validación

[🏠 Volver al Inicio](../README.md) | [📘 Guía de Importación](../docs/02-guia-importacion-datos.md)

</div>
