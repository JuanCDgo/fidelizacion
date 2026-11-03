# ⭐ Manual Técnico: Micro App Club Fidelidad & Tarjeta Digital de Sellos

Aplicación web progresiva (PWA / SPA) ultra ligera construida en Vanilla JavaScript (ES6+), HTML5 y Tailwind CSS, diseñada para fidelización de clientes y tarjetas de sellos digitales (*punch cards*) para comercios y profesionales independientes de cualquier rubro.

---

## 🏗️ 1. Arquitectura y Seguridad

### 🔒 Control de Acceso y Blindaje de Privacidad
- **Separación de Contextos (Cliente vs. Comercio):**
  - **Modo Cliente (`?c=ID...`):** Al abrir un enlace de pase, la aplicación renderiza exclusivamente la tarjeta digital de socio (`#customerPassView`). **No existe botón de volver** ni acceso a la base de clientes.
  - **Modo Comercio:** Al ingresar a la raíz de la aplicación sin parámetros de cliente, el sistema exige validación de identidad mediante **PIN de 4 dígitos** (`#pinLockView`).
  - **Persistencia de Sesión Segura:** La autenticación administrativa se almacena en `sessionStorage` (`fidelizacion_admin_auth = 'true'`), lo que permite al comerciante operar sin reingresar el PIN en cada recarga durante su jornada de trabajo, pero se cierra automáticamente al cerrar la pestaña o tocar el botón **`🔒`** en la cabecera.
- **Portabilidad Total de Pases:** Los enlaces generados por WhatsApp incluyen los parámetros del cliente (`c`, `nom`, `tel`, `s`, `t`, `b`, `e`, `p`). Esto garantiza que **cualquier teléfono móvil** renderice la tarjeta personalizada al instante, aun sin tener datos previos en su memoria local.

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
