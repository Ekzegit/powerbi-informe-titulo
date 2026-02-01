# 📗 Guía de Importación de Datos

## 📑 Tabla de Contenidos

1. [Preparación del Archivo Excel](#preparación-del-archivo-excel)
2. [Importación de Datos a Power BI](#importación-de-datos-a-power-bi)
3. [Aplicar Transformaciones Power Query](#aplicar-transformaciones-power-query)
4. [Crear Modelo de Datos Estrella](#crear-modelo-de-datos-estrella)
5. [Establecer Relaciones](#establecer-relaciones)
6. [Validar la Importación](#validar-la-importación)
7. [Troubleshooting](#troubleshooting)

---

## 📁 Preparación del Archivo Excel

### Estructura Requerida del Archivo

Antes de importar, asegúrate de que tu archivo Excel cumple con estos requisitos:

#### Formato del Archivo

- **Extensión:** `.xlsx` o `.xls` (recomendado: `.xlsx`)
- **Hojas:** Una sola hoja con los datos (puede tener otras hojas, pero se usará una)
- **Tamaño:** Aproximadamente 38,000 filas
- **Primera fila:** Debe contener los nombres de las columnas (encabezados)

#### Columnas Requeridas

El archivo debe tener **exactamente** estas 20 columnas en cualquier orden:

```
1.  Convenio
2.  Rut Proveedor
3.  Nombre Proveedor
4.  Rut Organismo
5.  Institución
6.  Unidad de compra
7.  Región Unidad
8.  Comuna Unidad
9.  Id
10. Producto
11. TipoProducto
12. Modelo
13. Marca
14. Región Medida
15. Region
16. Monto Transado
17. Numero OC
18. Precio Promedio
19. Cantidad
20. Fecha Ultima Venta
```

### Verificación Pre-Importación

✅ **Checklist antes de importar:**

- [ ] El archivo Excel se abre correctamente
- [ ] La primera fila contiene los nombres de columnas
- [ ] No hay filas en blanco al principio
- [ ] Los nombres de columnas coinciden exactamente (mayúsculas, tildes, espacios)
- [ ] La columna "Fecha Ultima Venta" tiene formato DD-MM-YYYY (ej: 15-03-2024)
- [ ] Los montos son numéricos (pueden tener separadores de miles)
- [ ] Los RUTs pueden tener puntos y guiones (se limpiarán automáticamente)
- [ ] El archivo pesa menos de 500 MB

### Ejemplo de Datos de Muestra

Si quieres probar primero, usa el archivo de ejemplo:

```
📁 Ubicación: /data/estructura-ejemplo.csv
📊 Registros: 30 filas de muestra
✅ Formato: Listo para importar
```

Para usar el CSV:
1. Abrirlo en Excel
2. Guardar como `.xlsx`
3. Seguir los pasos de importación

---

## 📥 Importación de Datos a Power BI

### Paso 1: Abrir Power BI Desktop

1. Iniciar Power BI Desktop
2. Si aparece la pantalla de inicio, hacer clic en "Cerrar" o usar una de las opciones de inicio rápido

### Paso 2: Obtener Datos desde Excel

**Opción A: Usando la Cinta de Opciones**

```
1. Clic en la pestaña "Inicio"
2. Grupo "Datos" > Clic en "Obtener datos"
3. Seleccionar "Excel" de la lista
4. O usar el botón directo "Excel" si está visible
```

**Opción B: Usando Acceso Directo**

```
Inicio > Excel (botón grande en la cinta)
```

### Paso 3: Seleccionar el Archivo

1. **Navegador de archivos:**
   - Buscar la ubicación de tu archivo Excel
   - Seleccionar el archivo (ej: `ComprasPublicas.xlsx`)
   - Hacer clic en **"Abrir"**

2. **Ventana "Navegador":**
   - Aparecerá una lista de hojas del archivo Excel
   - Seleccionar la hoja que contiene los datos (ej: "Hoja1" o "ComprasPublicas")
   - Verás una **vista previa** de los datos a la derecha

3. **Vista Previa de Datos:**
   ```
   Verificar:
   ✅ Primera fila muestra nombres de columnas
   ✅ Datos aparecen correctamente
   ✅ ~38,000 filas cargadas (ver en la esquina inferior)
   ```

### Paso 4: Transformar Datos

**⚠️ IMPORTANTE:** NO hacer clic en "Cargar" todavía.

1. **Hacer clic en "Transformar datos"** (botón inferior derecho)
   - Esto abrirá el **Editor de Power Query**
   - Necesario para aplicar las transformaciones

2. **Editor de Power Query:**
   ```
   ┌─────────────────────────────────────────────┐
   │ [Inicio] [Transformar] [Agregar columna]... │
   ├─────────┬───────────────────────────────────┤
   │ CONSUL- │   VISTA PREVIA DE DATOS           │
   │ TAS     │   [Tabla con tus datos]           │
   │ • Query1│                                   │
   │         │                                   │
   └─────────┴───────────────────────────────────┘
   ```

---

## 🔄 Aplicar Transformaciones Power Query

### Opción 1: Usar Script Completo (Recomendado)

Esta es la forma más rápida y sin errores:

1. **Abrir el Editor Avanzado:**
   ```
   En Power Query:
   Vista > Editor avanzado
   ```

2. **Copiar el Script:**
   - Abrir el archivo: `/powerbi/scripts/power-query-transformaciones.m`
   - Copiar **TODA** la sección "SECCIÓN 1: IMPORTACIÓN DE DATOS"
   - Desde `let` hasta `TablaFinal`

3. **Reemplazar el Código:**
   - En el Editor Avanzado, seleccionar **todo** el código existente
   - Pegar el código copiado
   - **IMPORTANTE:** Ajustar la línea que dice:
     ```m
     Origen = Excel.Workbook(File.Contents("C:\Datos\ComprasPublicas.xlsx"), null, true),
     ```
   - Reemplazar la ruta con la ubicación real de tu archivo

4. **Verificar Sintaxis:**
   - Si hay errores, aparecerán resaltados en rojo
   - Verificar que las comillas estén correctas
   - Verificar que las comas estén en los lugares correctos

5. **Hacer clic en "Listo"**

6. **Verificar Resultados:**
   - Los datos deberían aparecer transformados
   - Verificar que la columna "Fecha" aparece como tipo Date
   - Verificar que no hay valores "-" en las columnas

### Opción 2: Aplicar Transformaciones Manualmente

Si prefieres hacerlo paso a paso:

#### Transformación 1: Promover Encabezados

Si la primera fila aparece como datos:
```
Inicio > Usar primera fila como encabezados
```

#### Transformación 2: Cambiar Tipos de Datos

```
Seleccionar cada columna y cambiar tipo:

Texto:
- Convenio, Nombre Proveedor, Institución, Producto, etc.

Número entero:
- Cantidad

Número decimal:
- Monto Transado, Precio Promedio

Mantener como texto (por ahora):
- Rut Proveedor, Rut Organismo, Numero OC, Id, Fecha Ultima Venta
```

#### Transformación 3: Reemplazar Valores Nulos

```
1. Seleccionar TODAS las columnas (Ctrl + A)
2. Inicio > Reemplazar valores
3. Valor para buscar: "-"
4. Reemplazar con: (dejar vacío)
5. Clic en "Aceptar"
```

#### Transformación 4: Limpiar RUTs

Para columna "Rut Proveedor":
```
1. Seleccionar columna "Rut Proveedor"
2. Transformar > Formato > Quitar caracteres no alfanuméricos
3. O usar: Transformar > Reemplazar valores > "." por "" (nada)
4. Repetir para quitar "-"
```

Repetir para "Rut Organismo"

#### Transformación 5: Convertir Fechas

```
1. Seleccionar columna "Fecha Ultima Venta"
2. Agregar columna > Columna personalizada
3. Nombre: "Fecha"
4. Fórmula:
   Date.FromText([Fecha Ultima Venta], [Format="dd-MM-yyyy"])
5. Cambiar tipo de columna "Fecha" a "Date"
```

#### Transformación 6: Agregar Columnas Calculadas

```
Agregar Año:
Agregar columna > Fecha > Año

Agregar Mes:
Agregar columna > Fecha > Mes > Mes

Agregar Trimestre:
Agregar columna > Fecha > Trimestre > Trimestre del año

Agregar MontoLinea:
Agregar columna > Columna personalizada
Nombre: MontoLinea
Fórmula: [Cantidad] * [Precio Promedio]
```

#### Transformación 7: Filtrar Nulos

```
1. Columna "Fecha" > Filtro > Quitar vacíos
2. Columna "Monto Transado" > Filtro > Quitar vacíos
```

### Paso 5: Renombrar la Consulta

```
En el panel izquierdo, clic derecho en "Query1" (o nombre actual)
> Cambiar nombre
> Escribir: "DatosCompras" o "TablaFinal"
```

---

## 🌟 Crear Modelo de Datos Estrella

### Concepto de Modelo Estrella

```
       DimProveedores          DimProductos
              ↓                      ↓
       DimInstituciones  →  FactCompras  ←  DimRegiones
              ↑                      ↑
       DimConvenios           DimCalendario
```

### Crear Tablas Dimensión

Para cada tabla dimensión, seguir estos pasos:

#### DimProveedores

```
1. En el panel izquierdo de Power Query
2. Clic derecho en "DatosCompras" > "Referencia"
3. Renombrar la nueva consulta a "DimProveedores"
4. Seleccionar SOLO las columnas:
   - Rut Proveedor
   - Nombre Proveedor
5. Inicio > Quitar otras columnas
6. Inicio > Quitar duplicados
7. Inicio > Ordenar ascendente (por Rut Proveedor)
```

#### DimProductos

```
1. Referencia desde "DatosCompras"
2. Renombrar a "DimProductos"
3. Seleccionar columnas:
   - Id
   - Producto
   - TipoProducto
   - Modelo
   - Marca
4. Quitar otras columnas
5. Quitar duplicados
6. Ordenar por Id
```

#### DimRegiones

```
1. Referencia desde "DatosCompras"
2. Renombrar a "DimRegiones"
3. Seleccionar columnas:
   - Region
   - Región Medida
4. Quitar otras columnas
5. Quitar duplicados
6. Ordenar por Region
```

#### DimInstituciones

```
1. Referencia desde "DatosCompras"
2. Renombrar a "DimInstituciones"
3. Seleccionar columnas:
   - Rut Organismo
   - Institución
   - Unidad de compra
   - Región Unidad
   - Comuna Unidad
4. Quitar otras columnas
5. Quitar duplicados (por Rut Organismo + Unidad de compra)
6. Ordenar por Rut Organismo
```

#### DimConvenios

```
1. Referencia desde "DatosCompras"
2. Renombrar a "DimConvenios"
3. Seleccionar columna:
   - Convenio
4. Quitar otras columnas
5. Quitar duplicados
6. Ordenar alfabéticamente
```

### Crear Tabla de Hechos - FactCompras

```
1. Referencia desde "DatosCompras"
2. Renombrar a "FactCompras"
3. Seleccionar SOLO estas columnas:
   - Id (FK a DimProductos)
   - Rut Proveedor (FK a DimProveedores)
   - Rut Organismo (FK a DimInstituciones)
   - Region (FK a DimRegiones)
   - Convenio (FK a DimConvenios)
   - Fecha (FK a DimCalendario)
   - Numero OC
   - Monto Transado
   - Precio Promedio
   - Cantidad
   - MontoLinea
   - Unidad de compra
4. Quitar otras columnas
5. Filtrar nulos en Fecha
```

### Crear DimCalendario (Tabla Calculada)

⚠️ **Importante:** Esta tabla se crea después de cargar los datos a Power BI.

```
1. Cerrar y aplicar Power Query
2. En Power BI, ir a "Vista de datos"
3. Inicio > Nueva tabla
4. Copiar el código de DimCalendario desde:
   /powerbi/scripts/tablas-calculadas.dax
5. Ajustar fechas FechaMin y FechaMax según tus datos
6. Enter para crear la tabla
```

### Aplicar Cambios

```
Inicio > Cerrar y aplicar
```

Esto:
- Cerrará Power Query
- Cargará todas las tablas a Power BI
- Puede tardar 1-3 minutos con 38,000 registros

---

## 🔗 Establecer Relaciones

### Abrir Vista de Modelo

```
Hacer clic en el icono de "Modelo" en la barra lateral izquierda
(Icono con 3 tablas conectadas)
```

### Crear Relaciones Manualmente

Para cada relación, seguir estos pasos:

#### Relación 1: FactCompras → DimProveedores

```
1. Arrastrar columna "Rut Proveedor" de FactCompras
2. Soltar sobre columna "Rut Proveedor" de DimProveedores
3. En el diálogo de relación:
   - Cardinalidad: Varios a uno (*:1)
   - Dirección de filtro cruzado: Una
   - Hacer activa esta relación: ✅
4. Clic en "Aceptar"
```

#### Relación 2: FactCompras → DimProductos

```
FactCompras[Id] → DimProductos[Id]
Cardinalidad: *:1
Dirección: Una
Activa: Sí
```

#### Relación 3: FactCompras → DimRegiones

```
FactCompras[Region] → DimRegiones[Region]
Cardinalidad: *:1
Dirección: Una
Activa: Sí
```

#### Relación 4: FactCompras → DimInstituciones

```
FactCompras[Rut Organismo] → DimInstituciones[Rut Organismo]
Cardinalidad: *:1
Dirección: Una
Activa: Sí
```

#### Relación 5: FactCompras → DimConvenios

```
FactCompras[Convenio] → DimConvenios[Convenio]
Cardinalidad: *:1
Dirección: Una
Activa: Sí
```

#### Relación 6: FactCompras → DimCalendario

```
FactCompras[Fecha] → DimCalendario[Fecha]
Cardinalidad: *:1
Dirección: Una
Activa: Sí
```

### Verificar Relaciones

El modelo debe verse así:

```
         DimProveedores
               ↓
         FactCompras ← DimProductos
         ↓  ↓  ↓  ↓
         ↓  ↓  ↓  DimRegiones
         ↓  ↓  DimInstituciones
         ↓  DimConvenios
         DimCalendario
```

### Marcar Tabla de Fechas

```
1. Clic derecho en DimCalendario
2. "Marcar como tabla de fechas"
3. Seleccionar columna: "Fecha"
4. Clic en "Aceptar"
```

---

## ✅ Validar la Importación

### Validación 1: Conteo de Registros

```
1. Vista de datos
2. Verificar cada tabla:
   - FactCompras: ~38,000 filas
   - DimProveedores: ~50-100 filas
   - DimProductos: ~500-1000 filas
   - DimRegiones: ~15-20 filas
   - DimInstituciones: ~50-100 filas
   - DimConvenios: ~5-10 filas
   - DimCalendario: ~2000-4000 filas (según rango de fechas)
```

### Validación 2: Tipos de Datos

Verificar en cada tabla que los tipos sean correctos:

```
✅ Fechas: Tipo "Date"
✅ Montos: Tipo "Decimal" o "Número fijo"
✅ Cantidades: Tipo "Número entero"
✅ IDs y RUTs: Tipo "Texto"
✅ Nombres: Tipo "Texto"
```

### Validación 3: Relaciones

```
Vista de modelo:
✅ 6 relaciones activas (líneas sólidas)
✅ Todas son 1:N (símbolo 1 y * en los extremos)
✅ No hay relaciones muchos a muchos (M:N)
✅ No hay líneas punteadas (relaciones inactivas no deseadas)
```

### Validación 4: Crear Visual de Prueba

```
1. Ir a Vista de informe
2. Insertar una tarjeta
3. Arrastrar "Total Monto Transado" (medida a crear)
4. Si aparece un número, ✅ el modelo funciona
```

### Validación 5: Verificar Filtros

```
1. Crear un gráfico simple (barras)
2. Eje: DimProveedores[Nombre Proveedor]
3. Valores: SUM(FactCompras[Monto Transado])
4. Agregar slicer de DimCalendario[Año]
5. Cambiar el año en el slicer
6. ✅ El gráfico debe actualizarse
```

---

## 🔧 Troubleshooting

### Problema 1: Error al Cargar Excel

**Error:** "No se puede abrir el archivo"

**Soluciones:**
- Cerrar el archivo Excel si está abierto
- Verificar que la ruta es correcta
- Verificar permisos de lectura del archivo
- Copiar el archivo a una ubicación sin caracteres especiales

### Problema 2: Columnas No Coinciden

**Error:** "No se encuentra la columna X"

**Soluciones:**
- Verificar nombres exactos (mayúsculas, tildes, espacios)
- Revisar la primera fila del Excel
- Usar "Usar primera fila como encabezados" en Power Query

### Problema 3: Fechas No Se Convierten

**Error:** Columna Fecha muestra "Error"

**Soluciones:**
```
Verificar formato original:
✅ Debe ser DD-MM-YYYY (15-03-2024)
❌ NO MM/DD/YYYY
❌ NO YYYY-MM-DD

Ajustar fórmula:
Date.FromText([Fecha Ultima Venta], [Format="dd-MM-yyyy"])
```

### Problema 4: Relaciones No Se Crean

**Error:** "No se puede crear la relación"

**Causas y soluciones:**
- **Tipos de datos diferentes:** Asegurar que ambas columnas tengan el mismo tipo
- **Valores nulos:** Filtrar nulos antes de crear relación
- **Duplicados en tabla dimensión:** La tabla dimensión debe tener valores únicos en la clave
- **Relación ya existe:** Eliminar relación existente primero

### Problema 5: Rendimiento Lento

**Síntoma:** La carga tarda mucho (>10 minutos)

**Soluciones:**
- Cerrar otros programas
- Aumentar RAM asignada a Power BI
- Reducir datos de prueba si solo estás probando
- Aplicar filtros en Power Query para reducir filas

### Problema 6: Medidas No Funcionan

**Error:** Las medidas DAX muestran error

**Verificar:**
- Que las relaciones estén activas
- Que los nombres de tablas y columnas sean correctos
- Que la sintaxis DAX sea correcta (corchetes, paréntesis)
- Crear medidas después de cargar datos

---

## 📊 Siguiente Paso

Una vez validada la importación correcta y el modelo de datos:

➡️ **Continuar con:** [03 - Guía de Uso de Dashboards](03-guia-uso-dashboards.md)

➡️ **Agregar medidas DAX:** Usar el archivo `/powerbi/scripts/medidas-dax.dax`

---

## 💾 Guardar el Trabajo

No olvides guardar tu archivo:

```
Archivo > Guardar como
Nombre sugerido: "ComprasSenado.pbix"
Ubicación: Carpeta del proyecto
```

---

<div align="center">

✅ **Importación y Modelo Completados**

El modelo de datos estrella está listo para análisis

[⬅️ Anterior: Instalación](01-guia-instalacion.md) | [🏠 Inicio](../README.md) | [➡️ Siguiente: Dashboards](03-guia-uso-dashboards.md)

</div>
