# 🔥 Comida Anita - Sistema de Ventas PRO

Sistema web de punto de venta (POS) para negocio de comida casera. Gestión completa de menú diario, pedidos, cobros, deudores y comunicación con clientes vía WhatsApp.

## 📱 Demo

- **PROD (Firebase):** [alvahector59-ship-it.github.io/comida-anita](https://alvahector59-ship-it.github.io/comida-anita/)
- **QA (Local):** Abrir `ventas-comida-local/index.html` en navegador

## 🏗️ Arquitectura

```
┌─────────────────────────────────────────────┐
│                 FRONTEND                     │
│          HTML + CSS + JavaScript             │
│              (Single File)                   │
├─────────────────────────────────────────────┤
│                                             │
│  ┌─────────┐  ┌──────────┐  ┌───────────┐  │
│  │ Pedidos │  │Dashboard │  │ Reportes  │  │
│  │  del Día│  │ Gráficas │  │ Día/Rango │  │
│  └─────────┘  └──────────┘  └───────────┘  │
│                                             │
│  ┌─────────┐  ┌──────────┐  ┌───────────┐  │
│  │Deudores │  │Calendario│  │  Config   │  │
│  │ + Cobro │  │ Mensual  │  │ Clientes  │  │
│  └─────────┘  └──────────┘  └───────────┘  │
│                                             │
├─────────────────────────────────────────────┤
│              WhatsApp API                    │
│     api.whatsapp.com/send (mensajes)        │
├─────────────────────────────────────────────┤
│              BASE DE DATOS                   │
│                                             │
│  PROD: Firebase Firestore (nube)            │
│  QA:   IndexedDB (navegador local)          │
└─────────────────────────────────────────────┘
```

## 📁 Estructura de Archivos

```
ventas-comida/          # PROD (Firebase)
├── index.html          # App completa (HTML + CSS + JS)
├── manifest.json       # PWA manifest
└── sw.js               # Service Worker (offline)

ventas-comida-local/    # QA (IndexedDB)
├── index.html          # App con BD local
├── manifest.json       # PWA manifest
└── sw.js               # Service Worker
```

## 🗄️ Modelo de Datos

| Colección | Campos | Descripción |
|-----------|--------|-------------|
| `clients` | name, days[], phone | Clientes con días de pedido y WhatsApp |
| `guisos` | name, price, cat | Catálogo (fijo/guiso/desayuno) |
| `aguas` | name, price | Catálogo de bebidas |
| `orders` | date, clientId, items[], aguas[], extras[], notes, total, paid | Pedidos |
| `dayMenus` | date, guisoIds[] | Menú seleccionado por día |
| `config` | key, value | Meta, sonido, mensajes WhatsApp |

## ✨ Funcionalidades

### 📋 Pedidos del Día
- Selección de menú del día (2 guisos + fijos)
- Viernes: Chilaquiles, Pambazos, Sopes + Huevos/Bistec
- Cantidad por platillo con botones +/−
- Múltiples aguas por pedido
- Extras y notas personalizadas
- Estado clickeable (Pagado/Pendiente)
- Editar y eliminar pedidos
- Meta de ventas con slider y mensajes motivacionales
- Resumen a cocina vía WhatsApp

### 📢 Envío de Menú
- Plantilla personalizable en Config
- Selección de contactos con checkbox
- Envío individual por WhatsApp
- Botón copiar mensaje
- Variables: {dia}, {fecha}, {menu}, {aguas}

### 📊 Dashboard
- Filtro por rango (Semana/Mes/Todo/Personalizado)
- Resumen: Pedidos, Ventas, Cobrado, Pendiente, Deudores
- Platillo estrella
- Top platillos y clientes con gráficas de barras

### 📈 Reportes
- Reporte del Día (fecha específica)
- Reporte por Rango (personalizado)
- Estatus por cliente (Pagado/Pendiente)
- Export CSV y PDF
- WhatsApp de cobro directo

### 💳 Deudores
- Filtro por nombre y rango de fechas
- Estatus por pedido: ✅ Pagado / 🔴 Adeudo
- Marcar pagado individual o total
- WhatsApp de cobro con mensaje personalizado de Config
- Resumen: Venta Total, Cobrado, Pendiente, # Deudores

### 🗓️ Calendario
- Vista mensual con ventas por día
- Detalle al click: pedidos, estado, editar, eliminar

### ⚙️ Configuración
- **Clientes:** CRUD + teléfono WhatsApp + días de pedido
- **Guisos:** Catálogo con precio y categoría (fijo/guiso/desayuno)
- **Aguas:** Catálogo de bebidas
- **General:**
  - Meta de ventas diaria
  - Mensaje de cobro WhatsApp (personalizable con {nombre}, {monto}, {detalle})
  - Plantilla de menú del día
  - Backup/Restore (JSON)
  - Sonido al marcar pagado

## 🔐 Autenticación

Login con usuario y contraseña (sessionStorage):
- `halvarez` / `Mexico123`
- `dpena` / `Mexico123`

## 🎨 UI/UX

- Diseño POS profesional (estilo Square/Toast)
- Modo oscuro con toggle
- Splash screen con logo
- PWA instalable en celular
- Responsive (móvil, tablet, desktop)
- Animaciones suaves (fadeIn, pop)
- Sonido al marcar pagado
- Ventas del día en header
- Badge de deudores en pestaña

## 🛠️ Tecnologías

| Componente | Tecnología |
|------------|------------|
| Frontend | HTML5 + CSS3 + JavaScript vanilla |
| BD PROD | Firebase Firestore |
| BD QA | IndexedDB |
| Hosting | GitHub Pages |
| PWA | Service Worker + Manifest |
| Mensajería | WhatsApp Web API |
| Imágenes | Unsplash (login background) |

## 🚀 Despliegue

### GitHub Pages (PROD)
1. Push a branch `main` o `Release`
2. Settings → Pages → Deploy from branch
3. URL: `https://alvahector59-ship-it.github.io/comida-anita/`

### Local (QA)
```bash
open ventas-comida-local/index.html
```

## 📦 Datos Default

**17 Clientes:** Hector, Diana, Bryan, Anel, Eduardo Fernandez, Lupita, Liz Becker, Alicia, Machuca, Dani Basto, Eduardo Macropay, Alfredo Coba, Alfredo Macropay, Angelica, Tehuitzil, Oscar, Larry

**17 Guisos:**
- *Fijos:* Pechuga Asada, Pechuga Empanizada
- *Guisos:* Tacos Dorados, Enchiladas Verdes, Enchiladas de Mole, Bistec en Pasilla, Milanesas Empanizadas, Albóndigas, Filete de Pescado, Tinga, Chiles Rellenos, Picadillo, Pechuga Parmesana, Bistec a la Mexicana
- *Desayunos:* Chilaquiles, Pambazos, Sopes

**6 Aguas:** Jamaica, Limón, Guayaba, Tamarindo, Naranja, Piña

## 📄 Licencia

Proyecto privado - © 2026 Comida Anita
