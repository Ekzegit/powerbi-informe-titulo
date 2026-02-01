# 📐 Templates de Power BI

## 📋 Acerca de las Plantillas (.pbit)

Esta carpeta está destinada a almacenar **plantillas de Power BI** (archivos `.pbit`) que permiten reutilizar la estructura del informe sin incluir los datos.

---

## 🎯 ¿Qué es un Archivo .pbit?

### Definición

Un archivo **.pbit** (Power BI Template) es una **plantilla de Power BI** que contiene:

✅ **Incluye:**
- Estructura del modelo de datos (tablas y relaciones)
- Todas las medidas DAX
- Tablas calculadas
- Visualizaciones y diseño de páginas
- Formatos y temas personalizados
- Configuración de parámetros

❌ **NO incluye:**
- Los datos en sí (las tablas están vacías)
- Credenciales de conexión
- Configuración específica de rutas de archivos

### Ventajas de Usar Plantillas

| Ventaja | Descripción |
|---------|-------------|
| 🔄 **Reutilizable** | Usar la misma estructura con diferentes datos |
| 📦 **Tamaño pequeño** | Sin datos, el archivo es muy liviano (<1 MB) |
| 🚀 **Implementación rápida** | Crear nuevos informes en minutos |
| 🔒 **Sin datos sensibles** | Compartir sin exponer información real |
| 📊 **Estandarización** | Todos los informes siguen el mismo formato |
| 🎨 **Diseño consistente** | Mantener identidad visual corporativa |

---

## 🏗️ Cómo Crear una Plantilla

### Método 1: Desde Power BI Desktop

1. **Abrir tu archivo .pbix completo**
   - Asegurarte de que todo esté funcionando correctamente
   - Verificar que las medidas DAX estén bien
   - Revisar que los dashboards se vean bien

2. **Guardar como Plantilla**
   ```
   Archivo > Exportar > Plantilla de Power BI
   ```

3. **Configurar Información de la Plantilla**
   - **Nombre:** Análisis de Compras Públicas - Senado
   - **Descripción:** 
     ```
     Plantilla para análisis de compras públicas de productos de aseo.
     Incluye 5 dashboards especializados y más de 30 medidas DAX.
     Diseñado para dataset con 20 columnas específicas.
     ```
   - **Vista previa:** Se generará automáticamente

4. **Guardar**
   - Nombre de archivo: `ComprasSenado_Template.pbit`
   - Ubicación: Esta carpeta (`/powerbi/templates/`)

### Método 2: Guardar Como

```
Archivo > Guardar como
Tipo de archivo: Power BI Template Files (*.pbit)
Ubicación: /powerbi/templates/
Nombre: ComprasSenado_Template.pbit
```

---

## 📖 Cómo Usar una Plantilla

### Paso 1: Abrir la Plantilla

1. **Doble clic en el archivo .pbit**
   - Se abrirá Power BI Desktop
   - Aparecerá un diálogo solicitando parámetros

2. **Ingresar Parámetros** (si los hay)
   - Ruta del archivo Excel con los datos
   - Otros parámetros configurados
   - O hacer clic en "Cargar" para configurar después

### Paso 2: Conectar los Datos

**Opción A: Configurar en el Diálogo Inicial**
```
1. Ingresar ruta del archivo Excel
2. Hacer clic en "Cargar"
3. Esperar a que se carguen los datos
```

**Opción B: Configurar Después**
```
1. Cerrar el diálogo inicial
2. Inicio > Transformar datos
3. Editor de Power Query > Configuración de origen
4. Cambiar la ruta del archivo
5. Cerrar y aplicar
```

### Paso 3: Verificar

1. Los datos se cargan automáticamente
2. Los dashboards se populan con información
3. Las medidas calculan correctamente
4. Guardar como nuevo archivo .pbix

---

## 🔧 Crear Plantilla para este Proyecto

### Plantilla Sugerida: "ComprasSenado_Template.pbit"

#### Contenido Recomendado

La plantilla debería incluir:

**1. Modelo de Datos**
- ✅ Todas las tablas (vacías)
  - FactCompras
  - DimProveedores
  - DimProductos
  - DimRegiones
  - DimInstituciones
  - DimConvenios
  - DimCalendario
- ✅ Relaciones configuradas
- ✅ Tipos de datos correctos

**2. Medidas DAX**
- ✅ Las 32+ medidas del proyecto
  - KPIs Principales
  - Análisis Temporal
  - Análisis de Proveedores
  - Análisis de Productos
  - Análisis Geográfico
  - Medidas Auxiliares

**3. Tablas Calculadas**
- ✅ DimCalendario (con fórmula)
- ✅ Parámetros de análisis
- ✅ Clasificación ABC
- ✅ Otras tablas auxiliares

**4. Visualizaciones**
- ✅ Dashboard 1: Resumen Ejecutivo
- ✅ Dashboard 2: Análisis de Proveedores
- ✅ Dashboard 3: Análisis de Productos
- ✅ Dashboard 4: Análisis Geográfico
- ✅ Dashboard 5: Análisis Temporal

**5. Configuración**
- ✅ Tema de colores corporativo
- ✅ Formato de números (español chileno)
- ✅ Formato de fechas (DD-MM-YYYY)
- ✅ Slicers configurados

#### Parámetros Sugeridos

Al crear la plantilla, considerar parametrizar:

```
Parámetro: RutaArchivoExcel
Tipo: Texto
Valor por defecto: "C:\Datos\ComprasPublicas.xlsx"
Descripción: "Ruta completa del archivo Excel con datos de compras"

Parámetro: NombreHoja
Tipo: Texto  
Valor por defecto: "ComprasPublicas"
Descripción: "Nombre de la hoja de Excel que contiene los datos"
```

---

## 🚀 Casos de Uso

### Caso 1: Análisis Mensual

```
Escenario: Generar informe cada mes con nuevos datos
Uso: Abrir plantilla > Conectar archivo del mes > Guardar como "Marzo2024.pbix"
Beneficio: 5 minutos vs. horas recreando desde cero
```

### Caso 2: Diferentes Instituciones

```
Escenario: Aplicar el análisis a otra institución pública
Uso: Abrir plantilla > Conectar datos de la otra institución
Beneficio: Mismo análisis, diferentes datos
```

### Caso 3: Distribución al Equipo

```
Escenario: Equipo de analistas necesita la estructura
Uso: Compartir archivo .pbit (< 1 MB) por email
Beneficio: No compartir datos sensibles, solo estructura
```

### Caso 4: Backup de Diseño

```
Escenario: Proteger el diseño sin los datos
Uso: Guardar .pbit como respaldo del modelo
Beneficio: Recuperar estructura si se corrompe el .pbix
```

---

## 📁 Estructura de Archivos Recomendada

```
/powerbi/templates/
│
├── ComprasSenado_Template.pbit              # Plantilla principal completa
├── ComprasSenado_ModeloSolo.pbit            # Solo modelo sin visuales
├── ComprasSenado_Dashboard1.pbit            # Solo Dashboard Ejecutivo
├── ComprasSenado_Dashboard2.pbit            # Solo Dashboard Proveedores
└── README.md                                # Este archivo
```

### Plantillas Especializadas

**Plantilla Completa:**
- 5 dashboards + modelo completo
- Para implementación completa

**Plantilla Solo Modelo:**
- Modelo de datos y medidas
- Sin visualizaciones
- Para que cada usuario cree sus propios dashboards

**Plantillas por Dashboard:**
- Una plantilla por cada dashboard
- Para uso específico o capacitación

---

## 🔒 Buenas Prácticas

### Al Crear Plantillas

1. ✅ **Limpiar datos de prueba**
   - No incluir datos sensibles
   - Usar datos de ejemplo mínimos o vacíos

2. ✅ **Documentar dentro de la plantilla**
   - Agregar página "Instrucciones"
   - Incluir notas sobre parámetros
   - Describir configuración necesaria

3. ✅ **Probar antes de distribuir**
   - Abrir la plantilla
   - Conectar con datos de prueba
   - Verificar que todo funciona

4. ✅ **Versionado**
   - Incluir versión en el nombre
   - Ejemplo: `ComprasSenado_Template_v1.0.pbit`

5. ✅ **Agregar metadatos**
   - Autor
   - Fecha de creación
   - Descripción detallada
   - Requisitos de datos

### Al Usar Plantillas

1. ✅ **Verificar requisitos de datos**
   - Estructura de columnas debe coincidir
   - Nombres exactos
   - Tipos de datos compatibles

2. ✅ **Guardar como .pbix después de conectar datos**
   - No trabajar directamente sobre la plantilla
   - Guardar con nombre descriptivo

3. ✅ **Actualizar conexiones de datos**
   - Revisar rutas de archivos
   - Configurar credenciales si es necesario

---

## ⚙️ Diferencias: .pbix vs .pbit

| Característica | .pbix (Archivo) | .pbit (Plantilla) |
|----------------|-----------------|-------------------|
| **Datos** | ✅ Incluye datos | ❌ Sin datos |
| **Tamaño** | Grande (MB-GB) | Pequeño (KB-MB) |
| **Editable** | ✅ Sí | ⚠️ Solo al abrir |
| **Compartir** | Cuidado con datos | ✅ Seguro |
| **Conexiones** | Guardadas | Se piden al abrir |
| **Uso principal** | Trabajo diario | Distribución/reutilización |
| **Actualización** | Automática | Manual al abrir |

---

## 💡 Alternativas a Plantillas

### Opción 1: Scripts Separados (Usada en este Proyecto)

```
✅ Ventajas:
- Mayor flexibilidad
- Fácil de versionar en Git
- Educativo (ver el código)
- Modificable sin Power BI

❌ Desventajas:
- Requiere aplicar scripts manualmente
- Más pasos para implementar
```

### Opción 2: Archivo .pbix de Referencia

```
✅ Ventajas:
- Todo en un solo archivo
- Copiar y pegar visuales

❌ Desventajas:
- Incluye datos
- Archivo grande
- Difícil de versionar
```

### Opción 3: Power BI Apps (Requiere Power BI Service)

```
✅ Ventajas:
- Distribución en la nube
- Actualizaciones automáticas
- Control de acceso

❌ Desventajas:
- Requiere licencia Power BI Pro
- Necesita servicio en la nube
```

---

## 🎓 Para este Proyecto Académico

### Recomendación

Para el examen de título y presentación:

**Opción A: Usar Scripts (Actual)**
```
✅ Demuestra conocimiento técnico
✅ Código visible para evaluadores  
✅ Fácil de explicar el proceso
✅ Versionable en GitHub
```

**Opción B: Crear Plantilla Adicional**
```
1. Crear plantilla después de terminar
2. Incluirla como entregable adicional
3. Mostrar capacidad de crear plantillas
4. Útil para demo rápida
```

### Sugerencia de Implementación

```
1. Completar el desarrollo con scripts
2. Probar con datos de ejemplo
3. Crear plantilla final
4. Guardar en esta carpeta
5. Documentar en README (este archivo)
6. Mencionar en presentación como valor agregado
```

---

## 📚 Recursos Adicionales

### Documentación Oficial Microsoft

- [Crear plantillas de informes](https://docs.microsoft.com/power-bi/create-reports/desktop-templates)
- [Usar plantillas de informes](https://docs.microsoft.com/power-bi/create-reports/desktop-templates-use)

### Tutoriales Recomendados

- Búsqueda en YouTube: "Power BI template tutorial"
- Comunidad Power BI: Ejemplos de plantillas

---

## ❓ Preguntas Frecuentes

**P: ¿Cuál es la diferencia entre .pbix y .pbit?**  
R: .pbix incluye datos, .pbit es solo la estructura/diseño.

**P: ¿Puedo distribuir plantillas gratis?**  
R: Sí, las plantillas se pueden compartir libremente.

**P: ¿Las plantillas funcionan en Power BI Service?**  
R: No, solo en Power BI Desktop. Al abrirlas, se convierten en .pbix que sí se pueden publicar.

**P: ¿Necesito licencia especial para crear plantillas?**  
R: No, Power BI Desktop es gratuito y permite crear plantillas.

**P: ¿Qué pasa si mi estructura de datos cambia?**  
R: Debes actualizar la plantilla o modificar Power Query al usarla.

**P: ¿Por qué no hay un archivo .pbit en esta carpeta?**  
R: Este proyecto usa scripts separados por flexibilidad. Puedes crear tu propia plantilla siguiendo las instrucciones.

---

<div align="center">

📐 **Plantillas de Power BI**

Reutiliza la estructura del análisis fácilmente

[🏠 Volver al Inicio](../../README.md) | [📘 Documentación](../../docs/)

</div>
