# 🟢 Semana 06 — Memoria y recursos en Ubuntu

## Datos del alumno
- Nombre: José Gerardo Cabrera Miranda
- Grupo: 3° Semestre - Ingeniería en Sistemas Computacionales
- Fecha: 19 de octubre de 2026

## Entorno
- Distribución y versión: Ubuntu 24.04 LTS (x86_64)
- Equipo físico o máquina virtual: Equipo Físico (Lenovo ThinkPad)
- CPU lógicas: 8 (Intel Core i5-8265U, 4 núcleos / 8 hilos)

## Objetivo
Analizar la gestión de memoria RAM, memoria virtual, swap y carga del sistema en Ubuntu mediante comandos en la terminal y consultas al sistema de archivos `/proc`, realizando comparaciones antes, durante y después de la ejecución de actividades controladas.

## Medición inicial
| Indicador | Resultado | Interpretación |
|---|---|---|
| RAM total | 15,017,080 kB (~14.3 GiB) | Capacidad física total de memoria RAM reconocida por el sistema. |
| RAM disponible | 11,205,696 kB (~10.6 GiB) | Estimación real de memoria libre y recuperable para nuevas aplicaciones. |
| Swap total | 0 kB / No configurada | No se detectó espacio de intercambio Swap activo en el sistema. |
| Swap usada | 0 kB | Sin uso de memoria Swap. |
| Carga promedio | 0.73, 0.80, 0.89 | Carga promedio a 1, 5 y 15 minutos; muy por debajo de los 8 núcleos lógicos. |

## Procesos observados
- Mayor uso de CPU observado: `firefox` (PID: 6491, ~47.5% CPU)
- Mayor uso de memoria observado: `firefox` (PID: 6491, ~5.9% MEM)
- PID analizado: `6491`
- ¿Qué información consulté en `/proc`?: Consulté `/proc/cpuinfo` para obtener los datos del procesador, `/proc/meminfo` para los detalles de la memoria y `/proc/6491/status` para revisar el estado, la memoria residente (`VmRSS`) y los hilos activos del proceso.

## Experimento antes/durante/después
- **Antes:** Se registró un estado de reposo con una memoria disponible de ~10.6 GiB y carga baja.
- **Durante:** Se ejecutó el proceso `sleep 120`. Dado que `sleep` únicamente suspende su ejecución sin consumir CPU ni RAM significativa, los valores de memoria y carga se mantuvieron estables.
- **Después:** Tras la finalización del proceso, la memoria y la carga retornaron a sus niveles iniciales sin variaciones apreciables.

## Diagnóstico
Basado en las lecturas obtenidas (`free -h`, `vmstat` y `/proc/meminfo`), el equipo cuenta con suficiente memoria RAM disponible (~10.6 GiB libres) y los promedios de carga (0.73) están muy por debajo de la capacidad de procesamiento de los 8 núcleos lógicos del procesador. No se presentan signos de saturación ni cuellos de botella por falta de RAM.

## Conclusión
Comprendí que la memoria reportada como "usada" por Linux a menudo incluye cachés y buffers (`buff/cache`) que el Kernel maneja eficientemente para agilizar el sistema y que pueden ser liberados al instante cuando una aplicación lo requiera. Además, aprendí a verificar la carga relativa del procesador comparándola con la cantidad de CPUs lógicas (`nproc`).
