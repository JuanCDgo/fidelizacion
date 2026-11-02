# ⭐ Micro App Club Fidelidad & Tarjeta Digital de Sellos

Aplicación web ligera (HTML5 + Vanilla JS + Tailwind CSS) para fidelización de clientes y tarjetas de sellos digitales (*punch cards*) para comercios y profesionales independientes de cualquier rubro.

---

## 🚀 Características Principales

### 🎁 1. Estrategia de Progreso Concedido (*Endowed Progress Effect*)
- Al dar de alta un cliente, el sistema permite otorgarle automáticamente **sellos de regalo iniciales** (ej: 4 sellos de bienvenida sobre una meta de 8).
- **Psicología aplicada:** El cliente siente que ya arrancó al 50% de su camino, generando un enganche inmediato mucho mayor y aumentando drásticamente la tasa de retorno.
- Mensaje de bienvenida optimizado por WhatsApp en 1 toque:
  > *"¡Hola Mateo! 🎉 ¡Te damos la bienvenida a Café Urbano! Por sumarte a nuestro Club de Fidelidad te regalamos tus primeros 4 sellos ⭐. Ya tenés 4 de 8 sellos listos. ¡Solo te faltan 4 para reclamar tu premio: 1 Café de especialidad gratis! 🥳 Acá podés ver tu tarjeta digital: [Link]"*

### 📱 2. Pase Digital del Cliente (Vista Móvil Estilo Wallet)
- Acceso directo mediante URL (`?tarjeta=CLI_ID`).
- Visualización interactiva de la tarjeta perforada: sellos activos dorados, casilleros pendientes, barra de progreso y código QR personal del socio para mostrar en caja.
- Funciona 100% offline, se puede instalar en la pantalla de inicio del celular como una app nativa (PWA).

### ⚡ 3. Panel Ágil para el Mostrador / Comerciante
- **+1 Sello** en un toque con micro-animación y sonido/confeti al completar la tarjeta.
- **Canjear Premio** cuando llega a la meta, con reinicio automático de tarjeta y contador histórico de premios canjeados.
- **Buscador y Escáner QR:** Búsqueda rápida por nombre, teléfono o últimos 4 dígitos.
- **Recordatorios por WhatsApp:**
  - Saludo de bienvenida con sellos regalados.
  - Alerta *"🔥 ¡Te falta solo 1 sello!"*.
  - Felicitación *"🏆 ¡Tu premio está listo para canjear!"*.

### 🎨 4. Configuración para Cualquier Rubro (Uso General)
- Meta de sellos adaptable: 4, 6, 8, 10 o 12 sellos.
- Bono de bienvenida personalizable: de 0 a 5 sellos de regalo.
- Iconos intercambiables: ⭐ Estrella, ☕ Café, ✂️ Peluquería/Barbería, 🍔 Hamburguesa, 🍕 Pizza, 🥐 Panadería/Medialuna, 🎁 Regalo, 💎 Diamante, 🐾 Mascota, 🚗 Lavadero, 🍦 Heladería, 🍺 Cervecería.
- PIN de seguridad de 4 dígitos para sumar sellos desde el celular del cliente.

### ☁️ 5. Respaldo y Portabilidad
- Sincronización automática con Google Drive (Carpeta: *Copia de seguridad Fidelizacion*).
- Descarga de respaldo en formato JSON local.
- Exportación a planilla Excel / CSV con un clic.
- Restauración rápida en caso de cambio de dispositivo.

---

## 🌐 Demo Online
👉 https://juancdgo.github.io/fidelizacion/
