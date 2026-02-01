# 📘 Guía de Instalación de Power BI Desktop

## 📑 Tabla de Contenidos

1. [Requisitos Previos](#requisitos-previos)
2. [Descarga de Power BI Desktop](#descarga-de-power-bi-desktop)
3. [Instalación Paso a Paso](#instalación-paso-a-paso)
4. [Configuración Inicial](#configuración-inicial)
5. [Verificación de la Instalación](#verificación-de-la-instalación)
6. [Solución de Problemas Comunes](#solución-de-problemas-comunes)
7. [Tips y Recomendaciones](#tips-y-recomendaciones)

---

## 📋 Requisitos Previos

Antes de instalar Power BI Desktop, asegúrate de cumplir con los siguientes requisitos:

### Requisitos del Sistema

| Componente | Requisito Mínimo | Requisito Recomendado |
|------------|------------------|----------------------|
| **Sistema Operativo** | Windows 10 (64-bit) | Windows 11 (64-bit) |
| **Procesador** | 1 GHz o superior | Intel Core i5 o superior |
| **RAM** | 2 GB | 8 GB o más |
| **Espacio en Disco** | 2.5 GB disponibles | 10 GB disponibles |
| **Resolución** | 1440 x 900 | 1920 x 1080 o superior |
| **.NET Framework** | 4.7 o superior | Última versión |
| **Internet** | Requerido para descarga | Requerido para actualizaciones |

### Compatibilidad

✅ **Compatible con:**
- Windows 10 (versión 1809 o posterior)
- Windows 11
- Windows Server 2016 o posterior

❌ **NO compatible con:**
- macOS (usar Power BI Service en navegador)
- Linux
- Tablets o dispositivos móviles
- Windows 7 o versiones anteriores

### Notas Importantes

⚠️ **Importante:**
- Power BI Desktop es **gratuito**
- Requiere cuenta Microsoft (se puede crear durante la instalación)
- La versión de escritorio es diferente al servicio Power BI en la nube
- Se actualiza mensualmente con nuevas características

---

## 📥 Descarga de Power BI Desktop

### Método 1: Descarga Directa desde Microsoft (Recomendado)

1. **Abrir el navegador web** (Edge, Chrome, Firefox)

2. **Ir al sitio oficial de Microsoft:**
   ```
   https://powerbi.microsoft.com/desktop/
   ```

3. **Hacer clic en el botón "Descargar gratis"**
   - El sitio detectará automáticamente tu sistema operativo
   - Se descargará el instalador (aproximadamente 500 MB)

4. **Ubicación de descarga:**
   - Por defecto: Carpeta "Descargas"
   - Nombre del archivo: `PBIDesktopSetup_x64.exe`

### Método 2: Microsoft Store (Alternativo)

1. **Abrir Microsoft Store** en Windows 10/11

2. **Buscar** "Power BI Desktop"

3. **Hacer clic en "Obtener"** o "Instalar"
   - Ventaja: Actualizaciones automáticas
   - Desventaja: Requiere Windows 10/11 con Store activo

### Método 3: Descarga para Instalación Masiva

Para administradores de TI o instalación en múltiples equipos:

```
https://www.microsoft.com/download/details.aspx?id=58494
```

---

## 🔧 Instalación Paso a Paso

### Paso 1: Ejecutar el Instalador

1. **Localizar** el archivo descargado `PBIDesktopSetup_x64.exe`

2. **Hacer doble clic** en el archivo

3. **Permitir cambios** en el dispositivo (UAC)
   - Hacer clic en "Sí" cuando Windows lo solicite
   - Se requieren privilegios de administrador

### Paso 2: Asistente de Instalación

1. **Pantalla de Bienvenida**
   - Leer el mensaje de bienvenida
   - Hacer clic en **"Siguiente"**

2. **Términos de Licencia**
   - Marcar ☑️ "Acepto los términos del contrato de licencia"
   - Hacer clic en **"Siguiente"**

3. **Carpeta de Destino**
   - **Ruta por defecto recomendada:**
     ```
     C:\Program Files\Microsoft Power BI Desktop\
     ```
   - **Cambiar ruta** (opcional): Hacer clic en "Cambiar"
   - Verificar espacio disponible (mínimo 2.5 GB)
   - Hacer clic en **"Siguiente"**

4. **Accesos Directos**
   - ☑️ Crear acceso directo en el escritorio (recomendado)
   - ☑️ Crear acceso directo en el menú Inicio
   - Hacer clic en **"Instalar"**

### Paso 3: Proceso de Instalación

1. **Esperar** mientras se instalan los archivos
   - Barra de progreso indicará el avance
   - Tiempo estimado: 3-5 minutos
   - No cerrar la ventana durante la instalación

2. **Pantalla de Finalización**
   - Mensaje: "La instalación se completó correctamente"
   - ☑️ Marcar "Iniciar Power BI Desktop" (opcional)
   - Hacer clic en **"Finalizar"**

---

## ⚙️ Configuración Inicial

### Primer Inicio de Power BI Desktop

1. **Abrir Power BI Desktop**
   - Desde el acceso directo del escritorio, o
   - Menú Inicio > Power BI Desktop

2. **Pantalla de Bienvenida**
   - Aparecerá un splash screen con el logo
   - Primera carga puede tardar 30-60 segundos

3. **Iniciar Sesión** (Opcional pero recomendado)
   ```
   Opción 1: Iniciar sesión con cuenta Microsoft
   - Hacer clic en "Iniciar sesión" (esquina superior derecha)
   - Ingresar correo electrónico de cuenta Microsoft
   - Ingresar contraseña
   
   Opción 2: Continuar sin iniciar sesión
   - Hacer clic en "Cerrar" en el diálogo de inicio de sesión
   - Algunas características limitadas
   ```

### Configuración Regional

4. **Configurar idioma y región:**
   - Ir a **Archivo** > **Opciones y configuración** > **Opciones**
   - Sección **Global** > **Configuración regional**
   - Seleccionar:
     - **Idioma de la aplicación:** Español (España) o Español (Chile)
     - **Configuración regional:** Español (Chile)
     - **Formato de fecha:** DD-MM-YYYY
   - Hacer clic en **Aceptar**
   - **Reiniciar** Power BI Desktop

### Configuraciones Recomendadas

5. **Optimizar configuración para el proyecto:**

   ```
   Archivo > Opciones y configuración > Opciones
   
   [ARCHIVO ACTUAL]
   ✅ Carga de datos:
      - Habilitar "Relaciones entre tablas al importar"
      - Habilitar "Autodetectar nuevas relaciones"
   
   [GLOBAL]
   ✅ Vista de datos:
      - Separador de miles: Activado
      - Decimales por defecto: 2
   
   ✅ Power Query Editor:
      - Habilitar "Permitir vista previa de datos"
      - Habilitar "Habilitar diagnósticos de consultas"
   
   ✅ Seguridad:
      - Nivel de privacidad: "Omitir niveles de privacidad" 
        (solo para este proyecto académico)
   ```

---

## ✅ Verificación de la Instalación

### Prueba 1: Interfaz Principal

Al abrir Power BI Desktop, deberías ver:

```
┌─────────────────────────────────────────────┐
│  [Archivo] [Inicio] [Vista] [Modelado]...  │ ← Cinta de opciones
├─────────────────────────────────────────────┤
│                                             │
│  VISUALIZACIONES    │   CAMPOS              │ ← Paneles laterales
│  [Gráficos]         │   [Tablas]            │
│                     │                       │
│         LIENZO PRINCIPAL                    │ ← Área de trabajo
│         (espacio en blanco)                 │
│                                             │
└─────────────────────────────────────────────┘
```

### Prueba 2: Crear un Informe de Prueba

1. **Obtener datos de ejemplo:**
   - Clic en **Obtener datos** > **Excel**
   - O usar datos de muestra integrados
   - Clic en **Cargar**

2. **Crear visualización simple:**
   - Seleccionar un visual (ej: gráfico de barras)
   - Arrastrar campos al lienzo
   - Si aparece el gráfico, ✅ **instalación correcta**

### Prueba 3: Verificar Power Query

1. **Abrir Editor de Power Query:**
   - Cinta **Inicio** > **Transformar datos**
   - Debería abrir una nueva ventana

2. **Verificar que aparecen:**
   - ✅ Lista de consultas a la izquierda
   - ✅ Vista previa de datos al centro
   - ✅ Panel de pasos aplicados a la derecha

### Prueba 4: Comprobar Versión

1. **Verificar versión instalada:**
   ```
   Archivo > Ayuda > Acerca de
   ```

2. **Información que debe aparecer:**
   - Versión de Power BI Desktop (ej: Febrero 2026)
   - Número de compilación
   - Arquitectura: 64 bits
   - Versión de .NET instalada

---

## 🔧 Solución de Problemas Comunes

### Problema 1: Error al Instalar - "No se puede instalar"

**Síntomas:**
- Mensaje de error durante la instalación
- Instalación se detiene al 50%

**Soluciones:**
1. ✅ Verificar que tienes **privilegios de administrador**
2. ✅ Desactivar **antivirus temporalmente** durante instalación
3. ✅ Desinstalar versiones anteriores de Power BI
4. ✅ Actualizar **Windows Update** completamente
5. ✅ Instalar **.NET Framework 4.7 o superior** manualmente

### Problema 2: Power BI no Inicia

**Síntomas:**
- Se cierra inmediatamente al abrir
- Pantalla en blanco al iniciar

**Soluciones:**
1. ✅ Verificar **requisitos del sistema**
2. ✅ Actualizar **controladores de gráficos**
3. ✅ Ejecutar como administrador:
   - Clic derecho en Power BI > "Ejecutar como administrador"
4. ✅ Reparar la instalación:
   - Panel de Control > Programas > Power BI Desktop > Reparar
5. ✅ Reinstalar completamente

### Problema 3: Error de .NET Framework

**Síntomas:**
- Mensaje: "Requiere .NET Framework 4.7 o superior"

**Solución:**
```
1. Descargar .NET Framework desde:
   https://dotnet.microsoft.com/download/dotnet-framework
   
2. Instalar versión 4.8 (más reciente)

3. Reiniciar el equipo

4. Volver a instalar Power BI Desktop
```

### Problema 4: No Puedo Iniciar Sesión

**Síntomas:**
- Error al iniciar sesión con cuenta Microsoft
- "No se pudo conectar al servicio"

**Soluciones:**
1. ✅ Verificar **conexión a internet**
2. ✅ Desactivar **proxy o VPN** temporalmente
3. ✅ Verificar que no esté bloqueado por **firewall corporativo**
4. ✅ Usar modo **"Continuar sin iniciar sesión"** (funcionalidad limitada)

### Problema 5: Interfaz en Inglés

**Solución:**
```
1. Ir a File > Options and settings > Options
2. Regional Settings > Application language
3. Seleccionar "Español"
4. Reiniciar Power BI Desktop
```

### Problema 6: Actualizaciones Automáticas

**Configurar actualizaciones:**
```
Archivo > Opciones y configuración > Opciones > Global > Actualizaciones

Opciones:
☑️ Notificarme cuando haya actualizaciones disponibles
☐ Descargar actualizaciones automáticamente (no recomendado durante proyectos activos)
```

---

## 💡 Tips y Recomendaciones

### Mejores Prácticas

1. **✅ Mantener Actualizado**
   - Microsoft libera actualizaciones mensuales
   - Revisar novedades en: https://powerbi.microsoft.com/blog/
   - Actualizar después de terminar proyectos importantes

2. **✅ Crear Cuenta Microsoft**
   - Permite guardar en la nube
   - Necesaria para compartir reportes
   - Gratis en: https://account.microsoft.com

3. **✅ Guardar Frecuentemente**
   - Archivo > Guardar (Ctrl + S)
   - Power BI tiene auto-guardado pero es mejor prevenir
   - Guardar antes de aplicar cambios grandes

4. **✅ Organizar Archivos**
   ```
   Estructura recomendada:
   C:\PowerBI\
   ├── Proyectos\
   │   └── Compras-Senado\
   │       ├── datos\
   │       ├── reportes\
   │       └── backups\
   ```

### Atajos de Teclado Útiles

| Atajo | Acción |
|-------|--------|
| `Ctrl + S` | Guardar archivo |
| `Ctrl + O` | Abrir archivo |
| `Ctrl + N` | Nuevo archivo |
| `Ctrl + C/V` | Copiar/Pegar visuales |
| `Ctrl + Z` | Deshacer |
| `Ctrl + Y` | Rehacer |
| `F11` | Modo pantalla completa |
| `Alt + F4` | Cerrar Power BI |

### Recursos Adicionales

📚 **Documentación Oficial:**
- https://docs.microsoft.com/power-bi/

🎓 **Aprendizaje Gratuito:**
- Microsoft Learn: https://learn.microsoft.com/training/powerbi/

💬 **Comunidad:**
- Power BI Community: https://community.powerbi.com/

📹 **Videos:**
- Canal oficial YouTube: https://www.youtube.com/user/mspowerbi

---

## 🎯 Siguiente Paso

Una vez verificada la instalación correcta:

➡️ **Continuar con:** [02 - Guía de Importación de Datos](02-guia-importacion-datos.md)

---

## ❓ Preguntas Frecuentes

**P: ¿Necesito pagar por Power BI Desktop?**  
R: No, Power BI Desktop es completamente gratuito. Solo el servicio en la nube Power BI Pro requiere suscripción.

**P: ¿Puedo tener múltiples versiones instaladas?**  
R: No se recomienda. Mejor desinstalar versiones antiguas antes de instalar nuevas.

**P: ¿Funciona sin internet?**  
R: Sí, una vez instalado puedes trabajar offline. Solo necesitas internet para actualizaciones y compartir en la nube.

**P: ¿Cuánto espacio ocupa?**  
R: Aproximadamente 2.5 GB la instalación, pero los archivos .pbix pueden crecer según el volumen de datos.

**P: ¿Se puede usar en MacOS?**  
R: No hay versión nativa para Mac. Alternativas: usar Power BI Service en navegador o virtualización (Parallels, VMware).

---

<div align="center">

✅ **Instalación Completada**

Ahora estás listo para comenzar a trabajar con Power BI Desktop

[⬅️ Volver al README principal](../README.md) | [➡️ Siguiente: Importación de Datos](02-guia-importacion-datos.md)

</div>
