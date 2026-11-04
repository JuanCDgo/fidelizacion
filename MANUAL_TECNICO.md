# 🛠️ Manual Técnico · Fidelización (Tarjetas de Sellos Digitales)

**Stack:** HTML5, Tailwind CSS (CDN), Vanilla JavaScript (ES6+), LocalStorage, QRCode.js, Canvas Confetti.  
**Despliegue:** GitHub Pages (`https://juancdgo.github.io/fidelizacion/`).  
**Copia de Seguridad:** Google Drive / LocalStorage JSON.

---

## 1. Arquitectura de la Solución

Aplicación **Single-Page Application (SPA) dual**:
* **Modo Administrador (Comercio):** Gestión de clientes, acreditación de sellos protegida por PIN, canje de recompensas y personalización de marca.
* **Modo Cliente (Pase Público):** Vista aislada activada por URL (`?pass={CLIENT_ID}`). El contenedor de administración se remueve/oculta completamente y el cliente solo interactúa con su tarjeta digital.

### Estructura de Archivos:
```text
Mini Apps/fidelizacion/
├── index.html            # Código fuente unificado (Admin + Pase Público de Cliente)
├── MANUAL_USUARIO.md     # Guía operativa para el comerciante
└── MANUAL_TECNICO.md     # Documentación técnica, esquema de datos y seguridad
```

---

## 2. Esquema de Persistencia (LocalStorage)

### 1. `fidelizacion_settings_v1`
```typescript
{
  bizName: string;          // "Club Fidelidad"
  bizSub: string;           // "Tarjetas de Sellos & Beneficios"
  bizLogo: string;          // Imagen Base64 comprimida
  stampEmoji: string;       // "⭐", "☕", "🍔", etc.
  totalStamps: number;      // Cantidad de sellos para recompensa (default: 8)
  welcomeStamps: number;    // Sellos iniciales de regalo (Estrategia de Progreso Concedido)
  rewardTitle: string;      // "1 Consumición o Premio Especial Gratis"
  pin: string;              // PIN numérico de administración (ej: "1234")
  alias: string;            // Alias de cobro Mercado Pago / CBU
  cbu: string;              // CBU/CVU bancario
  titular: string;          // Titular de la cuenta
  phone: string;            // WhatsApp oficial del negocio
  driveWebhookUrl: string;  // Webhook para sync automático con Google Drive
  autoSyncDrive: boolean;   // Booleano de sincronización
}
```

### 2. `fidelizacion_clients_v1`
```typescript
Array<{
  id: string;               // "c_1730000000000"
  name: string;             // Nombre del cliente
  phone: string;            // Número telefónico para WhatsApp
  stamps: number;           // Sellos activos actuales en la tarjeta
  completedCards: number;   // Tarjetas llenadas históricamente
  rewardsClaimed: number;   // Premios canjeados
  lastStampDate: string;    // "YYYY-MM-DDTHH:mm:ss.sssZ"
  createdAt: string;        // "YYYY-MM-DDTHH:mm:ss.sssZ"
}>
```

---

## 3. Seguridad y Aislamiento del Pase Público

1. **Detección de Parámetro URL:**
   * Al cargar la app, el script evalúa `const urlParams = new URLSearchParams(window.location.search); const passId = urlParams.get('pass');`.
2. **Modo Pase Exclusivo:**
   * Si existe `passId`, se localiza al cliente y se activa `fidelizacion_mode = 'customer'`.
   * El contenedor `#mainAppContainer` se oculta de forma irrevocable.
   * La vista pública solo renderiza la tarjeta del cliente identificado, sin exponer el panel de clientes ni la base de datos de otros usuarios.
3. **Control de Acreditación de Sellos:**
   * La acción `addStampToClient()` solicita validación de PIN para prevenir que un cliente sume sellos si accede indebidamente al dispositivo del comercio.

---

## 4. Cobro QR y Compatibilidad

* **Doble Motor:** Generación local con `QRCode.js` y fallback redundante inmediato a la API de `QuickChart.io`.
* **Copia de Seguridad:** Exportación e importación segura con sanitización de JSON y captura de excepciones.
