# 🧠 Control Center – Changelog

## 📅 2026-02-02 — Infraestructura base funcional

### ✅ Logros principales
- Raspberry Pi configurada como nodo central (TuringBerry)
- Red privada creada con Tailscale
- Acceso remoto estable desde:
  - PC (WSL / Linux)
  - iPhone
  - Tablet Android
- Conexión SSH funcionando por hostname (`turingberry`)
- Edición remota de código con VS Code (Remote-SSH)
- Página estática privada servida desde la Raspberry
- Página pública temporal publicada con Cloudflare Tunnel (trycloudflare)

---

## 🧱 Arquitectura actual

- **Tailscale**
  - Red privada cifrada
  - SSH, control y administración
  - Sin abrir puertos ni usar IP pública

- **Cloudflare Tunnel (quick tunnel)**
  - Publicación temporal al Internet
  - HTTPS automático
  - Link dinámico (no persistente)

- **Raspberry Pi**
  - Servidor central
  - Aloja:
    - páginas web
    - apps futuras (FastAPI)
    - túneles Cloudflare
    - scripts de control

---

## 🔐 Seguridad aplicada
- SSH accesible solo por Tailscale
- Página privada no expuesta a Internet
- Cloudflare solo apunta a servicios explícitos
- No hay ejecución remota de comandos vía web (todavía)

---

## 🌐 Estado de publicación
- Página privada:
  - Acceso solo por Tailscale
- Página pública:
  - Usando `trycloudflare.com`
  - Link cambia al reiniciar
  - Uso solo para pruebas y demos

---

## 🚀 Próximos hitos planeados
- Panel privado (FastAPI + HTML)
- Acciones controladas desde UI:
  - levantar apps
  - lanzar Cloudflare Tunnel
  - capturar URL pública
- Autostart con systemd
- Separación total:
  - Control privado (Tailscale)
  - Web pública (Cloudflare)
- Dominio propio + túnel nombrado (opcional)

---

## 🏁 Estado general
🟢 Infraestructura estable  
🟡 Publicación temporal  
🔵 Lista para evolucionar a Control Center completo
