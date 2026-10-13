# 🟣 Semana 05 — Procesos, PID y Señales en Ubuntu

## 👤 Datos del alumno
- **Nombre:** José Gerardo Cabrera Miranda
- **Fecha:** Octubre de 2026

## 🖥️ Entorno
- **Sistema operativo:** Ubuntu (Lenovo ThinkPad)[cite: 1, 5]
- **Entorno de ejecución:** Terminal de Bash local

## 🎯 Objetivo de la práctica
Observar y administrar procesos de prueba en Ubuntu, identificando sus identificadores (PID y PPID), estados, prioridades de planificación y comportamiento mediante el uso de comandos de monitoreo y control de trabajos[cite: 5].

---

## 🧾 Registro de Comandos

| Comando | ¿Qué hace? | Resultado observado |
|---|---|---|
| `whoami`, `tty`, `echo "$SHELL"` | Muestra el usuario activo, la terminal asociada y el intérprete de comandos[cite: 5]. | Permitió identificar los datos básicos de la sesión de trabajo actual[cite: 5]. |
| `uptime` | Muestra el tiempo de actividad del equipo y las cargas promedio recientes[cite: 5]. | Reveló el estado de carga del sistema operativo[cite: 5]. |
| `ps` / `ps aux` | Genera una instantánea de los procesos activos en la sesión o en todo el sistema[cite: 5]. | Desplegó la lista detallada de procesos con columnas de usuario, PID, consumo y estado[cite: 5]. |
| `pgrep -a bash` | Busca procesos activos que coincidan con el patrón indicado (ej. `bash`)[cite: 5]. | Localizó los identificadores y rutas de ejecución coincidentes[cite: 5]. |
| `top` | Muestra de manera dinámica e interactiva los procesos y recursos del sistema en tiempo real[cite: 5]. | Permitió observar cambios fluidos en el uso de CPU y memoria[cite: 5]. |
| `sleep 300 &` | Inicia un proceso inofensivo de espera y lo envía de forma controlada al segundo plano[cite: 5]. | Devolvió un número de trabajo y el PID asignado sin bloquear la terminal[cite: 5]. |
| `jobs -l` | Lista los trabajos controlados por la sesión actual de la terminal, incluyendo sus PID[cite: 5]. | Confirmó la existencia del proceso de prueba en segundo plano[cite: 5]. |
| `ps -o ... -p PID` | Consulta un conjunto específico de columnas para un PID determinado[cite: 5]. | Detalló los campos de PID, PPID, estado y prioridad del proceso analizado[cite: 5]. |
| `kill -TERM PID` | Envía una señal de terminación ordenada a un proceso utilizando su identificador[cite: 5]. | Solicitó el cierre limpio del proceso de prueba de forma controlada[cite: 5]. |

---

## 📸 Índice de Evidencias
* `01_sesion_uptime.png`: Consulta inicial de usuario, terminal y tiempo de actividad (`uptime`)[cite: 5].
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3ba984dde25da9ea8dd0a894299f3335b88b7260/Evidencia%201.png)


* `02_ps.png`: Listado completo de procesos del sistema y búsqueda mediante `pgrep`[cite: 5].
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3ba984dde25da9ea8dd0a894299f3335b88b7260/Evidencia%202.png)

* `03_top.png`: Monitoreo dinámico de recursos en tiempo real[cite: 5].
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3ba984dde25da9ea8dd0a894299f3335b88b7260/Evidencia%203.png)
* 
* `04_proceso_pid_ppid.png`: Creación del proceso `sleep` y consulta de sus identificadores PID y PPID[cite: 5].
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3ba984dde25da9ea8dd0a894299f3335b88b7260/Evidencia%204.png)
* 
* `05_jobs.png`: Verificación de trabajos activos con `jobs -l`[cite: 5].
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3ba984dde25da9ea8dd0a894299f3335b88b7260/Evidencia%205.png)
* 
* `06_prioridad_nice.png`: Consulta del valor de prioridad (`NI`) del proceso de prueba[cite: 5].
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3ba984dde25da9ea8dd0a894299f3335b88b7260/Evidencia%206%20.png)

* `07_terminacion_sigterm.png`: Envío de la señal de terminación `SIGTERM` y confirmación de su cierre[cite: 5].
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3ba984dde25da9ea8dd0a894299f3335b88b7260/Evidencia%207.png)
* 
