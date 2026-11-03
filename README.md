# ⭐ Manual Técnico: Micro App Club Fidelidad & Tarjeta Digital de Sellos

Aplicación web progresiva (PWA / SPA) ultra ligera construida en Vanilla JavaScript (ES6+), HTML5 y Tailwind CSS, diseñada para fidelización de clientes y tarjetas de sellos digitales (*punch cards*) para comercios y profesionales independientes de cualquier rubro.

---

## 🏗️ 1. Arquitectura y Seguridad

### 🔒 Blindaje de Privacidad y Modo Tarjeta Directa
- **Separación Estricta de Contextos (Cliente vs. Comercio):**
  - **Modo Cliente (`?c=ID...` y Acceso Directo PWA):** Al abrir el enlace de su tarjeta o iniciar desde el Acceso Directo en la pantalla de su teléfono, la app guarda la tarjeta en el dispositivo (`fidelizacion_saved_pass`) y fija el dispositivo en `fidelizacion_mode = 'customer'`. Renderiza **únicamente** la tarjeta digital (`#customerPassView`) sin pedir claves, sin botones de volver y sin ninguna vía de entrada al panel del comercio.
  - **Portabilidad Total de Pases:** Los enlaces generados por WhatsApp incluyen los parámetros del cliente (`c`, `nom`, `tel`, `s`, `t`, `b`, `e`, `p`). Esto garantiza que **cualquier teléfono móvil** renderice la tarjeta personalizada al instante y su acceso directo lleve siempre derecho a la tarjeta.

---

## 💾 2. Modelo de Datos (LocalStorage)

### Cliente (`clients` en `fidelizacion_clients`)
```typescript
interface Client {
  id: string;                     // Timestamp ID único (ej: 'cli_1730000000')
  name: string;                   // Nombre y Apellido
  phone: string;                  // Celular con código de área (ej: '54911...')
  stamps: number;                 // Sellos acumulados actuales
  totalStampsTarget: number;      // Meta de sellos (ej: 8 o 10)
  rewardsClaimed: number;         // Contador de premios canjeados
  isWelcomeBonus: boolean;        // Si recibió sellos de bienvenida
  welcomeStampsGranted: number;   // Cantidad de sellos iniciales
  notes: string;                  // Preferencias del cliente
  lastVisit: string;              // Fecha ISO última visita
  createdAt: string;              // Fecha ISO alta
}
```

### Configuración (`settings` en `fidelizacion_settings`)
```typescript
interface Settings {
  bizName: string;                // Nombre comercial
  bizSub: string;                 // Subtítulo / rubro
  stampEmoji: string;             // Emoji del sello (ej: 🐉, ⭐, ☕, 💅)
  bizLogo: string;                // Base64 DataURL
  totalStamps: number;            // Meta global por defecto (ej: 8)
  welcomeStamps: number;          // Sellos de regalo de bienvenida (ej: 4)
  rewardTitle: string;            // Premio (ej: '1 Consumición Gratis')
  pin: string;                    // PIN de seguridad (default: '1234')
  phone: string;                  // Celular del comercio
  driveWebhookUrl: string;        // Google Apps Script Webhook
  autoSyncDrive: boolean;         // Sincronización automática
  lastBackupDate: string | null;  // Timestamp de último backup
}
```

---

## 🌐 3. URL de Producción en GitHub Pages
👉 **https://juancdgo.github.io/fidelizacion/**
