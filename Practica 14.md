# 🔵 Semana 14 — Administración de un servidor Ubuntu

## 👤 Datos del alumno
- **Nombre:** José Gerardo Cabrera Miranda
- **Fecha:** Noviembre de 2026
- **Grupo / Curso:** Sistemas Operativos

## 🖥️ Entorno
- **Distribución y versión:** Ubuntu 26.04.1 LTS (Resolute Raccoon)
- **Kernel:** Linux 7.0.0-42-generic (x86_64)
- **Equipo:** Físico / Laboratorio local (Lenovo ThinkPad L490)
- **Tipo de red:** Conexión Ethernet local (Red Cabrera)
- **Servicio seleccionado:** `cron.service` y servicios base del sistema

---

## 📋 Inventario y Verificación del Servidor

| Componente | Comando de verificación | Resultado real obtenido en el equipo |
|---|---|---|
| **Sistema y kernel** | `uname -a` | Linux Gerardothinkpad 7.0.0-42-generic x86_64 GNU/Linux |
| **Almacenamiento** | `df -h` y `lsblk -f` | Particiones montadas correctamente; espacio suficiente en almacenamiento principal. |
| **Identidad** | `id` y `groups` | Usuario `gerardocm` con privilegios de sudo y pertenencia a grupos estándar. |
| **Paquete** | `dpkg -s cron` | Paquete instalado, configurado y validado de forma local. |
| **Servicio** | `systemctl status cron` | Servicio operando de forma activa y estable (`active (running)`). |
| **Red y rutas** | `ip -br address` / `ip route` | Interfaz de red y rutas predeterminadas configuradas correctamente vía Ethernet. |
| **Sockets** | `ss -lnt` | Puertos y sockets locales monitoreados sin exposición pública innecesaria. |
| **Firewall** | `sudo ufw status verbose` | Estado y reglas del cortafuegos auditadas para control de tráfico local. |
| **Logs** | `journalctl -u cron` | Bitácoras consultadas sin errores críticos de ejecución. |

---

## ⚙️ Cambios Autorizados y Bitácora
- **Cambio:** Auditoría integral de servicios y permisos sin alteración de parámetros críticos del sistema.
- **Motivo:** Cumplimiento de la práctica de administración segura de servidores de laboratorio bajo el principio de mínimos privilegios.
- **Verificación:** Validación mediante `systemctl`, `ss` y `journalctl` para confirmar la estabilidad operativa.
- **Reversión o estado final:** El servidor y sus servicios quedan en su estado óptimo de funcionamiento, documentados y listos para la revisión.

---

## 📸 Registro de Evidencias (Carpeta `semana14/evidencias/`)

1. **`01_inventario_inicial.png`** — Inventario del sistema, kernel y almacenamiento (`uname -a`, `lsblk -f`, `df -h`).
      ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/cc0b0b7d94abdb4119ad1c96860367d836547d90/Ev!dencia%201.png)
3. **`02_usuarios_permisos.png`** — Identidad de usuario, grupos y permisos del directorio de trabajo.
      ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/e68509e86166671366a396e357ac29ae35a83088/Ev!dencia%202.png)
5. **`03_paquetes.png`** — Consulta de paquetes instalados y estado con `dpkg`.
      ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/b401447771f2a0910fc2b777b35edb20d65d74b8/Ev!dencia%203.png)
7. **`04_estado_servicio.png`** — Estado, activación y arranque del servicio auditado (`systemctl`).
      ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/e1d0ac0135e05318b85e8df46c6a583c395ccc58/Ev!dencai%204.png)
9. **`05_red_sockets_firewall.png`** — Interfaces de red, rutas, sockets en escucha y estado de UFW.
       ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/5e02ecad1e8ead08de955563ab2907160da58daa/Ev!dencia%205.png)
11. **`06_logs_y_verificacion.png`** — Consulta de registros en el journal y tabla final de comprobación.
       ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/0b03ea4b5bd04b857c039beae440fc8650582789/Ev!dencia%206.png)

---

## 🏁 Conclusión
La administración eficiente de un servidor en Ubuntu exige un conocimiento profundo del estado inicial, control riguroso de permisos, auditoría de servicios y revisión constante de logs, garantizando un entorno robusto, seguro y completamente documentado.
