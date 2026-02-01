# 🖼️ Imágenes y Capturas de Pantalla

## 📁 Contenido de esta Carpeta

Esta carpeta está destinada a almacenar **capturas de pantalla** y **recursos visuales** del proyecto de Power BI para documentación y presentación.

---

## 🎯 Propósito

### ¿Para qué se Usa?

Esta carpeta debe contener:

- 📸 **Capturas de pantalla de dashboards** - Para documentación
- 🖼️ **Imágenes del modelo de datos** - Diagrama de relaciones
- 📊 **Gráficos destacados** - Visualizaciones importantes
- 🎨 **Mockups y diseños** - Diseño de interfaz
- 📋 **Diagramas de flujo** - Proceso de ETL
- 🏆 **Resultados y logros** - Para presentación

---

## 📸 Capturas Recomendadas

### Para Documentación del Proyecto

#### 1. Modelo de Datos (Vista de Modelo)

**Archivo sugerido:** `modelo-datos-estrella.png`

**Cómo capturar:**
```
1. En Power BI Desktop, ir a Vista de Modelo
2. Organizar las tablas para mostrar el esquema estrella
3. Asegurarse de que se vean todas las relaciones
4. Windows + Shift + S (captura de pantalla)
5. Guardar en esta carpeta
```

**Qué debe mostrar:**
- ✅ Tabla FactCompras al centro
- ✅ 6 tablas dimensión alrededor
- ✅ Líneas de relación visibles con cardinalidad (1, *)
- ✅ Nombres de tablas legibles

---

#### 2. Dashboard 1 - Resumen Ejecutivo

**Archivo sugerido:** `dashboard-01-resumen-ejecutivo.png`

**Qué capturar:**
- ✅ Vista completa del dashboard
- ✅ Todos los KPIs visibles
- ✅ Gráficos poblados con datos
- ✅ Slicers en estado visible

**Elementos importantes:**
- Tarjetas de KPIs principales
- Gráfico de tendencia temporal
- Top 5 proveedores
- Top 5 productos
- Distribución regional

---

#### 3. Dashboard 2 - Análisis de Proveedores

**Archivo sugerido:** `dashboard-02-proveedores.png`

**Elementos destacados:**
- Ranking de proveedores
- Gráfico de concentración (Pareto)
- Matriz proveedores vs productos
- Comparación de precios

---

#### 4. Dashboard 3 - Análisis de Productos

**Archivo sugerido:** `dashboard-03-productos.png`

**Elementos destacados:**
- Clasificación ABC
- Top productos por monto
- Top productos por cantidad
- Análisis de precios

---

#### 5. Dashboard 4 - Análisis Geográfico

**Archivo sugerido:** `dashboard-04-geografico.png`

**Elementos destacados:**
- Mapa de regiones (si lo hay)
- Distribución por región
- Gráfico de comparación regional
- KPIs por región

---

#### 6. Dashboard 5 - Análisis Temporal

**Archivo sugerido:** `dashboard-05-temporal.png`

**Elementos destacados:**
- Timeline de compras
- Análisis de estacionalidad
- Comparativa YoY
- Tendencias mensuales

---

#### 7. Editor de Power Query

**Archivo sugerido:** `power-query-transformaciones.png`

**Qué mostrar:**
- Vista del Editor de Power Query
- Lista de consultas (izquierda)
- Pasos aplicados (derecha)
- Vista previa de datos (centro)

---

#### 8. Medidas DAX

**Archivo sugerido:** `medidas-dax-organizadas.png`

**Qué capturar:**
- Panel de campos mostrando las medidas
- Organizadas en carpetas de visualización
- Íconos de medidas (Σ o ƒx)

---

### Para Presentación del Examen de Título

#### Capturas Adicionales Sugeridas

| Archivo | Contenido | Uso |
|---------|-----------|-----|
| `portada-proyecto.png` | Título y logo del proyecto | Slide de presentación |
| `comparacion-antes-despues.png` | Sin BI vs Con BI | Mostrar valor agregado |
| `kpis-principales.png` | Solo las tarjetas de KPIs | Destacar métricas |
| `clasificacion-abc.png` | Gráfico ABC de productos | Análisis técnico |
| `mapa-chile.png` | Distribución geográfica | Análisis regional |
| `grafico-pareto.png` | Concentración de proveedores | Análisis de Pareto |
| `tendencia-temporal.png` | Gráfico de línea temporal | Análisis de series de tiempo |

---

## 🎨 Mejores Prácticas para Capturas

### Configuración Antes de Capturar

1. **Modo de Vista**
   ```
   Vista > Modo de vista > Vista de lectura (F5)
   - Oculta la cinta de opciones
   - Muestra solo el informe
   - Más profesional para presentación
   ```

2. **Tema y Colores**
   ```
   Asegurar que:
   ✅ Tema aplicado consistentemente
   ✅ Colores corporativos si aplican
   ✅ Alto contraste para legibilidad
   ```

3. **Datos Actualizados**
   ```
   ✅ Actualizar datos antes de capturar
   ✅ Verificar que las fechas sean actuales
   ✅ Comprobar que no hay errores visibles
   ```

4. **Resolución**
   ```
   Configurar Power BI a pantalla completa
   Usar monitor de al menos 1920x1080
   Capturar en alta calidad
   ```

### Durante la Captura

**Herramientas Recomendadas:**

1. **Snipping Tool (Windows)**
   ```
   Windows + Shift + S
   - Seleccionar área rectangular
   - Captura directa al portapapeles
   - Pegar en Paint o editor
   ```

2. **PowerPoint (Para capturas con anotaciones)**
   ```
   1. Capturar pantalla
   2. Pegar en PowerPoint
   3. Agregar cuadros de texto, flechas
   4. Exportar como imagen
   ```

3. **Power BI Export**
   ```
   Archivo > Exportar > Exportar como PDF
   - Captura todas las páginas
   - Alta calidad
   - Luego convertir PDF a imágenes
   ```

### Después de Capturar

1. **Nomenclatura de Archivos**
   ```
   Formato: [tipo]-[numero]-[descripcion].png
   
   Ejemplos correctos:
   ✅ dashboard-01-resumen-ejecutivo.png
   ✅ modelo-datos-estrella.png
   ✅ kpi-monto-total.png
   
   Evitar:
   ❌ Captura1.png
   ❌ Screenshot 2024-03-15.png
   ❌ IMG_12345.png
   ```

2. **Formato de Archivo**
   ```
   Recomendado: PNG
   - Mejor calidad para capturas de pantalla
   - Soporta transparencia
   - Sin compresión con pérdida
   
   Alternativa: JPG
   - Para fotos o imágenes grandes
   - Menor tamaño de archivo
   ```

3. **Tamaño de Archivo**
   ```
   Objetivo: < 2 MB por imagen
   
   Si es muy grande:
   - Reducir resolución a 1920x1080 máximo
   - Usar compresión PNG
   - Recortar áreas innecesarias
   ```

---

## 📐 Dimensiones Recomendadas

### Para Documentación

| Tipo de Captura | Ancho | Alto | Ratio |
|-----------------|-------|------|-------|
| Dashboard completo | 1920px | 1080px | 16:9 |
| Modelo de datos | 1600px | 900px | 16:9 |
| Gráfico individual | 800px | 600px | 4:3 |
| KPI/Tarjeta | 400px | 300px | 4:3 |

### Para Presentación (PowerPoint)

```
Tamaño de slide: 16:9 (1920x1080)
Resolución de imagen: Mínimo 1280x720
Calidad: 96 DPI o superior
```

---

## 🎓 Para el Examen de Título

### Set Mínimo Recomendado

Para una presentación profesional, incluir al menos:

1. ✅ **Portada del proyecto** - Imagen con título y logo
2. ✅ **Modelo de datos** - Diagrama del esquema estrella
3. ✅ **5 dashboards** - Uno por cada dashboard implementado
4. ✅ **KPIs principales** - Captura destacando métricas clave
5. ✅ **Gráfico técnico destacado** - Ej: Clasificación ABC
6. ✅ **Editor Power Query** - Mostrar proceso ETL
7. ✅ **Lista de medidas DAX** - Organización de medidas

### Set Completo (Ideal)

Además del mínimo, agregar:

- 📊 Capturas de cada tipo de visual usado
- 🔍 Detalles de funcionalidades específicas
- 📈 Comparaciones antes/después
- 🎯 Casos de uso específicos con datos
- 📋 Drill-down y drill-through en acción
- 🔗 Interacción entre visuales
- 📱 Vista móvil (si aplica)

---

## 🖼️ Plantillas de Diseño

### Portada del Proyecto

Crear una imagen de portada con:

```
┌─────────────────────────────────────────┐
│                                         │
│     📊 ANÁLISIS DE COMPRAS PÚBLICAS     │
│                                         │
│      Senado de la República de Chile   │
│                                         │
│     [Logo Power BI]                     │
│                                         │
│     Business Intelligence Dashboard     │
│     Proyecto de Título Universitario    │
│                                         │
│     [Tu nombre]                         │
│     Febrero 2026                        │
│                                         │
└─────────────────────────────────────────┘
```

**Herramientas para crear:**
- PowerPoint
- Canva (online)
- Adobe Spark
- GIMP (gratuito)

---

## 📝 Documentar las Imágenes

### Crear un Índice de Imágenes

**Archivo:** `INDICE-IMAGENES.md`

```markdown
# Índice de Imágenes

## Dashboards
- dashboard-01-resumen-ejecutivo.png - Vista general con KPIs
- dashboard-02-proveedores.png - Análisis de proveedores
- dashboard-03-productos.png - Clasificación y análisis de productos
- dashboard-04-geografico.png - Distribución por regiones
- dashboard-05-temporal.png - Tendencias y estacionalidad

## Modelo
- modelo-datos-estrella.png - Esquema estrella completo

## Detalles Técnicos
- power-query-editor.png - Editor de transformaciones
- medidas-dax.png - Organización de medidas
- relaciones-modelo.png - Vista de relaciones
```

---

## 📊 Uso en Documentación

### Insertar en Markdown

```markdown
## Dashboard Resumen Ejecutivo

![Dashboard Resumen Ejecutivo](../images/dashboard-01-resumen-ejecutivo.png)

Este dashboard muestra...
```

### Insertar en PowerPoint

```
1. Insertar > Imágenes > Este dispositivo
2. Seleccionar la imagen de esta carpeta
3. Ajustar tamaño al slide
4. Agregar descripción en notas del orador
```

---

## 🔧 Herramientas Útiles

### Captura de Pantalla

- **Windows Snipping Tool** (Nativo)
- **ShareX** (Gratuito, avanzado)
- **Greenshot** (Gratuito, con anotaciones)
- **Lightshot** (Rápido y fácil)

### Edición de Imágenes

- **Paint** (Básico, nativo Windows)
- **Paint.NET** (Gratuito, más funciones)
- **GIMP** (Gratuito, profesional)
- **Photoshop** (Pago, profesional)

### Optimización

- **TinyPNG** (web) - Comprimir PNG
- **JPEGmini** (web) - Comprimir JPG
- **ImageOptim** (Mac) - Optimización batch

### Anotaciones

- **PowerPoint** - Para agregar textos y flechas
- **Snagit** (Pago) - Capturas con anotaciones
- **Greenshot** (Gratis) - Anotaciones básicas

---

## ⚠️ Consideraciones de Privacidad

### Antes de Capturar

```
⚠️ VERIFICAR:
- No incluir información sensible real
- Usar datos de ejemplo o anonimizados
- Ocultar nombres/RUTs reales si aplica
- No mostrar credenciales o tokens
- Revisar que no haya datos confidenciales visibles
```

### Para Compartir Públicamente

```
Si vas a subir a GitHub o compartir:
✅ Usar solo datos de ejemplo
✅ Verificar que no hay información privada
✅ Revisar dos veces antes de publicar
```

---

## 📋 Checklist Final

Antes del examen de título:

- [ ] Capturas de los 5 dashboards completos
- [ ] Imagen del modelo de datos (esquema estrella)
- [ ] Captura del editor Power Query
- [ ] Vista de medidas DAX organizadas
- [ ] Portada del proyecto creada
- [ ] Todas las imágenes en alta resolución
- [ ] Nombres de archivo descriptivos
- [ ] Sin información sensible visible
- [ ] Tamaño de archivos optimizado
- [ ] Colores y tema consistentes
- [ ] Índice de imágenes creado

---

## ❓ Preguntas Frecuentes

**P: ¿Qué resolución debo usar?**  
R: Mínimo 1280x720, ideal 1920x1080 para presentaciones.

**P: ¿PNG o JPG?**  
R: PNG para capturas de pantalla (mejor calidad), JPG para fotos.

**P: ¿Debo incluir capturas en el README?**  
R: Sí, es muy recomendable para mejorar la documentación.

**P: ¿Cómo ocultar datos sensibles?**  
R: Usar datos de ejemplo o desenfocar áreas sensibles en un editor.

**P: ¿Necesito permisos para las capturas?**  
R: Si son de tu propio trabajo, no. Si incluyes logos corporativos, verificar.

---

## 📚 Recursos

- [Markdown Image Syntax](https://www.markdownguide.org/basic-syntax/#images)
- [Power BI Export Options](https://docs.microsoft.com/power-bi/create-reports/desktop-export)
- [Screenshot Best Practices](https://techsmith.com/blog/screenshot-tips/)

---

<div align="center">

🖼️ **Recursos Visuales del Proyecto**

Capturas profesionales para documentación y presentación

[🏠 Volver al Inicio](../README.md)

</div>
