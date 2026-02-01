# 📊 Análisis de Compras Públicas - Senado de la República

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-107C10?style=for-the-badge&logo=microsoft&logoColor=white)
![Estado](https://img.shields.io/badge/Estado-Proyecto%20Académico-blue?style=for-the-badge)

> **Solución completa de Business Intelligence para análisis de compras públicas de productos de aseo del Senado de la República de Chile**

## 📖 Descripción

Este proyecto presenta una solución integral de **Business Intelligence** desarrollada en **Microsoft Power BI** para el análisis de aproximadamente **38,000 registros** de compras públicas de productos de aseo realizadas por el Senado de la República de Chile. 

La solución implementa un **modelo de datos en esquema estrella** optimizado, con múltiples tablas dimensión y una tabla de hechos, permitiendo análisis multidimensionales eficientes. Incluye más de **30 medidas DAX profesionales** para cálculo de KPIs, análisis temporal, de proveedores, productos y geográfico.

Este trabajo fue desarrollado como **proyecto de título universitario**, demostrando competencias técnicas en análisis de datos, modelado dimensional, programación DAX, visualización de información y generación de reportes ejecutivos para la toma de decisiones.

## 📑 Tabla de Contenidos

- [Acerca del Proyecto](#-acerca-del-proyecto)
- [Características Principales](#-características-principales)
- [Dashboards Disponibles](#-dashboards-disponibles)
- [KPIs Principales](#-kpis-principales)
- [Requisitos Previos](#-requisitos-previos)
- [Inicio Rápido](#-inicio-rápido)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [Documentación](#-documentación)
- [Datos de Ejemplo](#-datos-de-ejemplo)
- [Autor](#-autor)
- [Licencia](#-licencia)

## 🎯 Acerca del Proyecto

### Contexto Académico

Este proyecto de título tiene como objetivo demostrar la capacidad de:

✅ **Diseñar** un modelo de datos robusto en esquema estrella  
✅ **Implementar** transformaciones ETL complejas con Power Query (M)  
✅ **Desarrollar** medidas DAX profesionales para análisis avanzado  
✅ **Crear** dashboards interactivos y visualizaciones efectivas  
✅ **Documentar** soluciones técnicas de forma profesional  
✅ **Generar** reportes ejecutivos para la toma de decisiones

### Objetivo del Análisis

Proveer herramientas de análisis para:

- 📊 Monitorear el gasto en productos de aseo
- 🏢 Evaluar el desempeño de proveedores
- 📦 Analizar el comportamiento de compra de productos
- 🗺️ Identificar patrones geográficos de consumo
- 📈 Detectar tendencias temporales y estacionalidad
- 💰 Optimizar decisiones de compra y negociación con proveedores

## ⭐ Características Principales

### Modelo de Datos Optimizado
- ✨ **Esquema Estrella** clásico con 6 tablas dimensión y 1 tabla de hechos
- 🔗 Relaciones **1:N** correctamente configuradas
- 🚀 Optimizado para **38,000+ registros** con rendimiento rápido
- 🎯 Tabla de calendario completa con jerarquías temporales

### Scripts Listos para Usar
- 📝 **Power Query (M)** completo para transformación de datos
- 🧮 **32+ Medidas DAX** profesionales organizadas por categoría
- 📅 Tablas calculadas incluyendo calendario dinámico
- 💡 Código comentado en español y listo para copiar/pegar

### Análisis Multidimensional
- 🔍 Análisis por **Proveedor**, **Producto**, **Región** y **Tiempo**
- 📊 Clasificación **ABC** de productos
- 🏆 Rankings y **Top N** dinámicos
- 📈 Análisis **Year-over-Year** (YoY)
- 💹 Análisis de **tendencias** y estacionalidad

### Documentación Completa
- 📚 Guías paso a paso en español
- 🎓 Nivel profesional para presentación académica
- 💻 Ejemplos prácticos y casos de uso
- 🛠️ Solución de problemas comunes

## 📊 Dashboards Disponibles

Este proyecto incluye la documentación detallada para implementar **5 dashboards especializados**:

### 1. 📈 Dashboard Resumen Ejecutivo
Vista general del negocio con los KPIs más importantes, tendencias temporales y top performers.

**Componentes:**
- 6-8 tarjetas de KPIs principales
- Gráfico de tendencia temporal de montos
- Top 5 Proveedores por monto
- Top 5 Productos más comprados
- Distribución geográfica
- Slicers de Fecha, Región y Tipo de Producto

### 2. 🏢 Dashboard Análisis de Proveedores
Evaluación detallada de proveedores para optimizar relaciones comerciales.

**Componentes:**
- Ranking completo de proveedores
- Análisis de concentración (Pareto)
- Comparación de precios entre proveedores
- Timeline de compras por proveedor
- Matriz proveedores vs productos
- Tabla detallada con drill-down

### 3. 🎯 Dashboard Análisis de Productos
Gestión del portafolio de productos y análisis de comportamiento.

**Componentes:**
- Clasificación ABC interactiva
- Matriz productos por tipo y marca
- Análisis de variación de precios
- Top 10 productos por cantidad y monto
- Análisis de valor de stock
- Tabla dinámica con drill-through

### 4. 🗺️ Dashboard Análisis Geográfico
Distribución territorial de compras y análisis regional.

**Componentes:**
- Mapa de Chile con compras por región
- Gráficos de distribución regional
- Comparativo de precios por región
- Análisis por comuna
- KPIs regionales
- Distribución porcentual

### 5. 📅 Dashboard Análisis Temporal
Patrones temporales, estacionalidad y análisis de órdenes de compra.

**Componentes:**
- Timeline de compras
- Análisis de estacionalidad mensual/trimestral
- Número de OC por período
- Monto promedio por OC
- Comparativa año actual vs anterior
- Tendencias y proyecciones

## 📊 KPIs Principales

### Métricas Fundamentales
| KPI | Descripción |
|-----|-------------|
| 💰 **Total Monto Transado** | Suma total de todas las compras realizadas |
| 📦 **Total Cantidad Productos** | Número total de unidades compradas |
| 💵 **Precio Promedio General** | Precio promedio ponderado de productos |
| 🏢 **Número Proveedores Únicos** | Cantidad de proveedores distintos |
| 🎯 **Número Productos Únicos** | Cantidad de productos diferentes |
| 📋 **Número Órdenes Compra** | Total de OC procesadas |
| 🎫 **Ticket Promedio por OC** | Monto promedio por orden de compra |

### Análisis Avanzados
- 📈 **Variación % YoY** - Crecimiento año sobre año
- 🎯 **Concentración Top 10** - % de compras en top proveedores
- 📊 **Clasificación ABC** - Categorización de productos
- 💹 **Índice de Rotación** - Frecuencia de compra de productos
- 🗺️ **Distribución Regional** - % por región geográfica

## 🔧 Requisitos Previos

### Software Necesario

- **Microsoft Power BI Desktop** (Versión más reciente)
  - [Descargar gratis desde Microsoft](https://powerbi.microsoft.com/desktop/)
  - Compatible con Windows 10/11
  - Requiere .NET Framework 4.7 o superior

### Datos Requeridos

- Archivo Excel con datos de compras públicas
- Formato especificado en `/data/estructura-ejemplo.csv`
- Aproximadamente 38,000 registros (puede variar)

### Conocimientos Recomendados

- ✅ Conocimientos básicos de Power BI Desktop
- ✅ Familiaridad con conceptos de BI (opcional)
- ✅ Capacidad para seguir instrucciones paso a paso

## 🚀 Inicio Rápido

### Opción 1: Usando Scripts Completos (Recomendado)

```bash
# 1. Clonar el repositorio
git clone https://github.com/Ekzegit/powerbi-informe-titulo.git

# 2. Abrir Power BI Desktop

# 3. Importar datos desde Excel
- Archivo > Obtener datos > Excel
- Seleccionar tu archivo de datos
- Clic en "Transformar datos"

# 4. Aplicar transformaciones de Power Query
- Copiar el script de /powerbi/scripts/power-query-transformaciones.m
- Pegar en el Editor Avanzado de Power Query
- Ajustar la ruta del archivo Excel

# 5. Crear modelo de datos
- Crear tablas dimensión según las instrucciones del script
- Configurar relaciones en la vista de modelo

# 6. Agregar medidas DAX
- Copiar medidas de /powerbi/scripts/medidas-dax.dax
- Pegar en Power BI como nuevas medidas

# 7. Crear tablas calculadas
- Copiar scripts de /powerbi/scripts/tablas-calculadas.dax
- Crear tabla DimCalendario (prioritario)

# 8. Construir dashboards
- Seguir guía en /docs/03-guia-uso-dashboards.md
```

### Opción 2: Usando Datos de Ejemplo

```bash
# 1. Usar el archivo de ejemplo proporcionado
- Ubicado en /data/estructura-ejemplo.csv
- 30 registros de muestra para probar

# 2. Seguir la guía de importación
- Ver /docs/02-guia-importacion-datos.md
```

### Opción 3: Paso a Paso Manual

Seguir las guías completas en orden:
1. 📘 [Guía de Instalación](/docs/01-guia-instalacion.md)
2. 📗 [Guía de Importación de Datos](/docs/02-guia-importacion-datos.md)
3. 📙 [Guía de Uso de Dashboards](/docs/03-guia-uso-dashboards.md)

## 📁 Estructura del Proyecto

```
powerbi-informe-titulo/
│
├── 📄 README.md                          # Este archivo
│
├── 📂 docs/                              # Documentación completa
│   ├── 01-guia-instalacion.md           # Instalación de Power BI Desktop
│   ├── 02-guia-importacion-datos.md     # Importación y configuración de datos
│   ├── 03-guia-uso-dashboards.md        # Descripción de los 5 dashboards
│   ├── 04-diccionario-datos.md          # Descripción de campos y estructura
│   └── 05-medidas-kpis.md               # Documentación de medidas DAX
│
├── 📂 powerbi/                           # Scripts y recursos de Power BI
│   ├── 📂 scripts/                      # Scripts listos para usar
│   │   ├── power-query-transformaciones.m   # Transformaciones ETL completas
│   │   ├── medidas-dax.dax                  # 32+ medidas DAX
│   │   └── tablas-calculadas.dax            # Tabla calendario y auxiliares
│   └── 📂 templates/                    # Información sobre templates
│       └── README.md                     # Guía de templates .pbit
│
├── 📂 data/                              # Datos de ejemplo
│   ├── estructura-ejemplo.csv            # 30 registros de ejemplo
│   └── README.md                         # Descripción del formato de datos
│
└── 📂 images/                            # Imágenes y capturas
    └── README.md                         # Guía para agregar capturas
```

### Descripción de Carpetas

| Carpeta | Contenido | Propósito |
|---------|-----------|-----------|
| `/docs` | Documentación técnica | Guías paso a paso para implementación |
| `/powerbi/scripts` | Código M y DAX | Scripts listos para copiar/pegar |
| `/powerbi/templates` | Info de templates | Explicación de archivos .pbit |
| `/data` | Datos de ejemplo | Ejemplos para pruebas y validación |
| `/images` | Imágenes | Capturas de pantalla de dashboards |

## 🛠️ Tecnologías Utilizadas

### Herramientas de Microsoft

- **Power BI Desktop** - Plataforma principal de desarrollo
  - Versión: Última disponible (2024-2026)
  - Licencia: Gratuita

### Lenguajes y Frameworks

- **Power Query (M)** - ETL y transformación de datos
  - Limpieza de datos
  - Creación de modelo dimensional
  - Optimización de rendimiento

- **DAX (Data Analysis Expressions)** - Cálculos y medidas
  - Más de 30 medidas profesionales
  - Funciones de tiempo intelligence
  - Análisis estadísticos avanzados

### Conceptos Aplicados

- 📊 **Modelado Dimensional** - Esquema Estrella
- 🔄 **ETL** (Extract, Transform, Load)
- 📈 **Business Intelligence**
- 📉 **Data Visualization**
- 🎯 **KPI Management**

## 📚 Documentación

La documentación completa está organizada en 5 guías especializadas:

### 📘 [01 - Guía de Instalación](/docs/01-guia-instalacion.md)
Instalación y configuración de Power BI Desktop
- Requisitos del sistema
- Descarga e instalación paso a paso
- Configuración inicial
- Verificación y troubleshooting

### 📗 [02 - Guía de Importación de Datos](/docs/02-guia-importacion-datos.md)
Importación del archivo Excel y creación del modelo
- Preparación del archivo de datos
- Aplicación de transformaciones Power Query
- Creación de tablas dimensión
- Configuración de relaciones
- Validación del modelo

### 📙 [03 - Guía de Uso de Dashboards](/docs/03-guia-uso-dashboards.md)
Descripción detallada de los 5 dashboards
- Resumen Ejecutivo
- Análisis de Proveedores
- Análisis de Productos
- Análisis Geográfico
- Análisis Temporal
- Mejores prácticas de uso

### 📕 [04 - Diccionario de Datos](/docs/04-diccionario-datos.md)
Descripción completa de cada campo del dataset
- Estructura de datos original
- Tipos de datos y formatos
- Reglas de negocio
- Ejemplos y validaciones

### 📓 [05 - Medidas y KPIs](/docs/05-medidas-kpis.md)
Documentación de todas las medidas DAX
- Fórmulas completas con explicación
- Organización por categoría
- Lógica de negocio
- Casos de uso y ejemplos

## 📊 Datos de Ejemplo

### Archivo de Ejemplo

El repositorio incluye un archivo CSV de ejemplo con **30 registros** que representan compras reales:

- **Ubicación:** `/data/estructura-ejemplo.csv`
- **Formato:** CSV delimitado por comas
- **Codificación:** UTF-8
- **Propósito:** Pruebas y validación del modelo

### Estructura de Datos

```
Convenio, Rut Proveedor, Nombre Proveedor, Rut Organismo, Institución,
Unidad de compra, Región Unidad, Comuna Unidad, Id, Producto,
TipoProducto, Modelo, Marca, Región Medida, Region, Monto Transado,
Numero OC, Precio Promedio, Cantidad, Fecha Ultima Venta
```

### Proveedores de Ejemplo

- **PRISA S.A.** - Proveedor de papel y productos básicos
- **DIMERC S.A.** - Productos de limpieza y químicos
- **MG PUBLICIDAD Y SERVICIOS GENERALES LIMITADA** - Productos diversos

### Regiones Incluidas

- Región Metropolitana (RM)
- Región de Valparaíso (VAL)
- Región del Biobío (BIO)
- Región de la Araucanía (ARA)

📖 **Más información:** Ver `/data/README.md`

## 👨‍💻 Autor

**Ekzegit**

- 🎓 Proyecto de Título Universitario
- 📧 Contacto: [GitHub](https://github.com/Ekzegit)
- 📅 Fecha: Febrero 2026

### Agradecimientos

- Senado de la República de Chile (fuente de datos)
- Microsoft Power BI Community
- Evaluadores del proyecto de título

## 📄 Licencia

Este proyecto es un **trabajo académico** desarrollado como proyecto de título universitario.

**Uso Educativo:**
- ✅ Permitido para fines educativos
- ✅ Permitido para referencia y aprendizaje
- ✅ Permitido citar con atribución

**Restricciones:**
- ⚠️ Los datos son de ejemplo y pueden no reflejar información real
- ⚠️ Proyecto con fines académicos, no comerciales
- ⚠️ Citar apropiadamente si se utiliza como referencia

---

## 🚀 Comenzar Ahora

¿Listo para empezar? Sigue estos pasos:

1. ⬇️ **Clonar** el repositorio
2. 📖 **Leer** la [Guía de Instalación](/docs/01-guia-instalacion.md)
3. 📊 **Importar** datos siguiendo la [Guía de Importación](/docs/02-guia-importacion-datos.md)
4. 🎨 **Crear** dashboards con la [Guía de Dashboards](/docs/03-guia-uso-dashboards.md)
5. 📈 **Analizar** y generar reportes

## 💡 Soporte

Para preguntas o problemas:

1. 📚 Revisar la [documentación completa](/docs/)
2. 🔍 Consultar la sección de troubleshooting en cada guía
3. 💬 Abrir un Issue en GitHub (si aplica)

---

<div align="center">

**⭐ Si este proyecto te fue útil, dale una estrella en GitHub ⭐**

Desarrollado con 💙 para análisis de compras públicas

**Power BI** | **DAX** | **Power Query** | **Business Intelligence**

</div>
