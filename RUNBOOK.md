# 🛠️ Control Center – Runbook de Comandos

Este documento describe **todos los comandos utilizados hasta ahora**,  
**para qué sirven**, y **en qué contexto deben usarse** dentro del proyecto.

Pensado como guía operativa (runbook).

---

## 🔐 TAILSCALE – RED PRIVADA

### Ver dispositivos conectados a la red
```bash
tailscale status
Descripción:
Muestra todos los dispositivos conectados a tu red privada (tailnet), junto con
sus IPs internas 100.x.x.x.

Conectarse por SSH a la Raspberry (recomendado)
bash
Copiar código
ssh turing@turingberry
Descripción:
Acceso remoto seguro vía Tailscale usando el hostname del dispositivo.

Conectarse por SSH usando IP Tailscale (alternativa)
bash
Copiar código
ssh turing@100.71.85.114
Descripción:
Acceso directo usando la IP privada de Tailscale.

⏱️ SESIONES SSH
Cerrar sesión SSH
bash
Copiar código
exit
Sesiones persistentes (recomendado para túneles y servidores)
bash
Copiar código
tmux
Reanudar sesión:

bash
Copiar código
tmux attach
Descripción:
Permite mantener procesos activos aunque se caiga la conexión SSH.

🧑‍💻 EDICIÓN REMOTA DE CÓDIGO (VS CODE)
Método recomendado
Editor: VS Code (en la PC)

Extensión: Remote – SSH

Conexión configurada como:

text
Copiar código
ssh turing@turingberry
Descripción:
El código vive en la Raspberry, el editor corre localmente en la PC.

📁 ESTRUCTURA DE TRABAJO
Ir al home del usuario
bash
Copiar código
cd ~
Crear carpeta de proyectos
bash
Copiar código
mkdir -p ~/Server
Descripción:
Directorio principal para apps, panel, scripts y servicios.

🌐 PÁGINA ESTÁTICA PRIVADA (SOLO TAILSCALE)
Crear carpeta web
bash
Copiar código
mkdir -p ~/web
Crear archivo HTML
bash
Copiar código
nano ~/web/index.html
Servir la página estática
bash
Copiar código
cd ~/web
python3 -m http.server 8000 --bind 0.0.0.0
Descripción:
Levanta un servidor HTTP simple en el puerto 8000.

Acceso (solo dentro de Tailscale):

arduino
Copiar código
http://turingberry:8000
🌍 CLOUDFLARE TUNNEL – PUBLICACIÓN TEMPORAL
Uso para pruebas y demos.
El enlace NO es permanente.

Descargar cloudflared (ARM64)
bash
Copiar código
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-arm64
Dar permisos de ejecución
bash
Copiar código
chmod +x cloudflared-linux-arm64
Mover binario a PATH del sistema
bash
Copiar código
sudo mv cloudflared-linux-arm64 /usr/local/bin/cloudflared
Verificar instalación
bash
Copiar código
cloudflared --version
Crear túnel público rápido (trycloudflare)
bash
Copiar código
cloudflared tunnel --url http://localhost:8000
Descripción:
Publica el servicio local localhost:8000 al Internet usando Cloudflare.

Salida típica:

arduino
Copiar código
https://xxxxxx.trycloudflare.com
Características:

HTTPS automático

No requiere dominio

No requiere abrir puertos

El link cambia al reiniciar

Se cae si el proceso termina

🔐 BUENAS PRÁCTICAS DE SEGURIDAD
✔ Usar Tailscale para:

SSH

control

administración

panel privado

✔ Usar Cloudflare solo para:

contenido público

demos

páginas estáticas

APIs read-only

❌ No exponer al Internet:

panel de control

ejecución de comandos

scripts

SSH

endpoints administrativos

🧠 MODELO MENTAL CORRECTO
Tailscale → red privada y control total

Cloudflare Tunnel → vitrina pública segura

Raspberry Pi → orquestador central

Nada sensible se expone directamente

🏁 FIN DEL RUNBOOK
yaml
Copiar código

---

Si quieres, el siguiente paso puede ser:

- 📦 unir **CHANGELOG + RUNBOOK** en un solo `README.md`
- 🧠 crear **diagramas de arquitectura**
- 🚀 empezar el **MVP del panel privado (FastAPI + UI)**

Tú dime cómo lo quieres estructurar y lo dejamos limpio y profesional 👌