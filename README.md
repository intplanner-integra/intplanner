# INTPLANNER PRO V5 — Sistema de Gestión Empresarial

**Versión actual:** 5.1.0  
**Autor:** Integra Consultores GR  
**Ubicación:** Medellín, Colombia  
**Licencia:** Propietaria — Uso exclusivo del equipo Integra Consultores

---

## 📋 Descripción

INTPLANNER PRO es una **plataforma SaaS multi-módulo** autocontenida en un único archivo HTML, diseñada para la gestión integral de operaciones empresariales con:

- ✅ **Dashboard ejecutivo** con KPIs y análisis en tiempo real
- ✅ **Gestión de tareas y proyectos** con Kanban reactivo
- ✅ **Facturación y cobranzas** con seguimiento de pagos
- ✅ **Control de equipos y recursos** con asignación automática
- ✅ **Visitas a clientes** con generación de PDF y reportes
- ✅ **Respaldos automáticos** en local + Firebase Storage
- ✅ **Sincronización en tiempo real** con Firestore
- ✅ **Autenticación segura** con Firebase Auth
- ✅ **Código QR de sesión** para login entre dispositivos
- ✅ **PWA offline-first** — funciona sin conexión

---

## 🚀 Inicio rápido

### Opción 1 — Desde GitHub Pages (recomendado para el equipo)

Abre directamente en tu navegador:
```
https://intplanner-integra.github.io/intplanner/
```

**Ventajas:**
- Siempre la versión más reciente
- No requiere descargas
- Notificaciones automáticas de updates

### Opción 2 — Descarga local

1. Descarga `INTPLANNER_PRO_V5_Actualizada.html`
2. Abre el archivo con tu navegador (Ctrl+O o Cmd+O)
3. Inicia sesión con tu cuenta Integra Consultores

---

## 📦 Instalación en tu equipo (contribuyentes)

### Requisitos

- **Git** instalado ([descargar](https://git-scm.com/))
- **Cuenta GitHub** con acceso a este repositorio
- **Node.js** (opcional, solo para validación local)

### Clonar el repositorio

```bash
git clone https://github.com/intplanner-integra/intplanner.git
cd intplanner
```

### Servir localmente (opcional)

Con Python 3.x:
```bash
python -m http.server 8000
# Abre http://localhost:8000 en tu navegador
```

Con Node.js:
```bash
npx http-server
# Abre http://localhost:8080 en tu navegador
```

---

## 🔄 Flujo de actualización

### Para administradores (tú)

1. Actualiza el archivo `INTPLANNER_PRO_V5_Actualizada.html`
2. Actualiza `version.json` con la nueva versión
3. Haz commit y push:
   ```bash
   git add INTPLANNER_PRO_V5_Actualizada.html version.json
   git commit -m "v5.1.0: [descripción de cambios]"
   git push origin main
   ```
4. GitHub Pages se actualiza automáticamente en ~1-3 minutos

### Para usuarios finales

- **Si acceden por GitHub Pages:** Verán un banner notificando la nueva versión
  - Opción: actualizar ahora o después
- **Si acceden por archivo local:** Deben descargar la versión nueva manualmente

---

## 🔐 Configuración inicial

### Firebase

INTPLANNER requiere credenciales Firebase válidas. Están configuradas en:

```javascript
// Dentro del archivo HTML — líneas 480-510
const FIREBASE_CONFIG = {
  apiKey:           "...",
  authDomain:       "intplanner-v12.firebaseapp.com",
  projectId:        "intplanner-v12",
  storageBucket:    "intplanner-v12.appspot.com",
  messagingSenderId: "...",
  appId:            "..."
};
```

**Para cambiar proyecto Firebase:** Edita `FIREBASE_CONFIG` directamente en el archivo HTML.

### Empresa (Logo, NIT, Contacto)

Accede a: **Configuración → Empresa**

- Logo institucional (PNG, JPG, SVG)
- NIT, teléfono, email
- Url de la aplicación (para QR entre dispositivos)

Estos datos se guardan localmente + Firebase Firestore.

---

## 💾 Respaldos automáticos

### Ubicaciones de almacenamiento

| Tipo | Ubicación | Retención |
|---|---|---|
| Local | `localStorage` (navegador) | Permanente |
| Firebase Storage | `backups/{uid}/auto/` | Últimas 10 versiones |
| Manual | Descarga .json | Usuario decide |

### Restaurar un backup

1. Ve a: **Configuración → Respaldo de Datos**
2. Presiona: **Restaurar Backup**
3. Selecciona un archivo .json descargado previamente
4. La app se recargará con los datos restaurados

---

## 📱 Funcionalidades offline

INTPLANNER es una **Progressive Web App (PWA)**:

- Funciona **sin conexión a internet**
- Los cambios se sincronizan automáticamente al reconectar
- Todos los datos se guardan localmente
- Compatible con instalación en home screen (Android/iOS)

### Instalar como app

**Android:**
1. Abre INTPLANNER en Chrome
2. Menú → "Instalar aplicación"

**iPhone/iPad:**
1. Abre INTPLANNER en Safari
2. Compartir → "Añadir a pantalla de inicio"

---

## 🔑 Gestión de usuarios

### Crear usuario (Admin)

1. Ve a: **Configuración → Usuarios**
2. Presiona: **Nuevo Usuario**
3. Completa:
   - Nombre, email, rol
   - Contraseña (mín. 8 caracteres, 1 mayúscula, 1 número)
4. **Guardar**

### Roles disponibles

| Rol | Permisos |
|---|---|
| **administrador** | Acceso total — usuarios, configuración, todas las colecciones |
| **consultor** | Gestión de tareas, clientes, proyectos — sin usuarios ni configuración |
| **analista** | Solo lectura + reportes (Analytics) |
| **ejecutivo** | Dashboard + reportes de ventas/cobros |

### Cambiar contraseña

1. Ve a: **Configuración → Usuarios**
2. Presiona el ícono **🔑** en el usuario
3. Ingresa nueva contraseña
4. **Guardar**

---

## 🛠️ Desarrollo y mantenimiento

### Estructura del archivo

El archivo HTML es **single-file autocontenido**:

```
<!DOCTYPE html>
<html>
  <head>
    <meta ...>
    <style>...</style>  <!-- CSS embebido -->
  </head>
  <body>
    <div id="app"></div>
    <script>
      // React + todo el JavaScript incrustado
      // Sin dependencias externas (excepto CDNs)
    </script>
  </body>
</html>
```

### Dependencias (CDN)

- **React 18** — via unpkg.com
- **Firebaselib** — via googleapis.com
- **jsPDF + html2canvas** — para exportación PDF
- **QRCode.js** — para códigos QR
- **Babel Standalone** — transpilación JSX en el navegador

### Modificaciones seguras

Para agregar features:

1. **Encuentra el módulo** (ej: `const Dashboard = () => { ... }`)
2. **Realiza cambios quirúrgicos** (sin tocar otros módulos)
3. **Prueba en Consola** (F12 → Console) antes de publicar
4. **Valida con `node --check`** si trabajas localmente
5. **Haz commit + push** a GitHub Pages

---

## 🐛 Reportar problemas

Si encuentras errores:

1. **Abre la Consola:** F12 → Console
2. **Copia el error** completo
3. **Crea un issue** en GitHub o contacta al equipo técnico

**Errores comunes:**

| Error | Solución |
|---|---|
| "Firebase no inicializado" | Verifica credenciales en FIREBASE_CONFIG |
| "localStorage lleno" | Restaura un backup antiguo — limpia datos |
| "QR no funciona" | Configura URL de la app en Empresa |
| "Cambios no se sincronizan" | Verifica conexión + reglas Firestore |

---

## 📋 Changelog

### v5.1.0 — Junio 2026

- ✅ **Auto-Backup reactivo** — indicador sincronizado en tiempo real
- ✅ **Verificador de versión** — notificación automática de updates
- ✅ **Exportación PDF en Visita Cliente** — con logo y flujo completo
- ✅ Correcciones en Backup & QR — suscripción a eventos reactivos
- 🔧 Mejoras de rendimiento en sincronización Firebase

### v5.0.0 — Mayo 2026

- ✅ Lanzamiento inicial de INTPLANNER PRO V5
- ✅ Dashboard ejecutivo con KPIs
- ✅ Módulo Visita Cliente con PDF
- ✅ Auto-backup con Firebase Storage
- ✅ Código QR de sesión

---

## 📞 Soporte

**Contacto técnico:** YAC — Technical Director, Integra Consultores GR  
**Email:** [tu email]  
**Teléfono:** [tu teléfono]  
**Ubicación:** Medellín, Colombia

---

**INTPLANNER PRO** © 2026 Integra Consultores GR. Todos los derechos reservados.
