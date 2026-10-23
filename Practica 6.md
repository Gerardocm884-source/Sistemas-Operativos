# 🟢 Semana 06 — Memoria y recursos en Ubuntu

## 👤 Datos del alumno
- Nombre: José Gerardo Cabrera Miranda
- Grupo: 5° Semestre - Ingeniería en Sistemas Computacionales
- Fecha: 19 de octubre de 2026

## 💻 Entorno
- Distribución y versión: Ubuntu 24.04 LTS (x86_64)
- Equipo físico o máquina virtual: Equipo Físico (Lenovo ThinkPad)
- CPU lógicas: 8 (Intel Core i5-8265U, 4 núcleos / 8 hilos)

## 🎯 Objetivo
Analizar la gestión de memoria RAM, memoria virtual, swap y carga del sistema en Ubuntu mediante comandos en la terminal y consultas al sistema de archivos `/proc`, realizando comparaciones antes, durante y después de la ejecución de actividades controladas.

## 📏 Medición inicial
| Indicador | Resultado | Interpretación |
|---|---|---|
| RAM total | 15,017,080 kB (~14.3 GiB) | Capacidad física total de memoria RAM reconocida por el sistema. |
| RAM disponible | 11,205,696 kB (~10.6 GiB) | Estimación real de memoria libre y recuperable para nuevas aplicaciones. |
| Swap total | 0 kB / No configurada | No se detectó espacio de intercambio Swap activo en el sistema. |
| Swap usada | 0 kB | Sin uso de memoria Swap. |
| Carga promedio | 0.73, 0.80, 0.89 | Carga promedio a 1, 5 y 15 minutos; muy por debajo de los 8 núcleos lógicos. |

## 🔍 Procesos observados
- Mayor uso de CPU observado: `firefox` (PID: 6491, ~47.5% CPU)
- Mayor uso de memoria observado: `firefox` (PID: 6491, ~5.9% MEM)
- PID analizado: `6491`
- ¿Qué información consulté en `/proc`?: Consulté `/proc/cpuinfo` para obtener los datos del procesador, `/proc/meminfo` para los detalles de la memoria y `/proc/6491/status` para revisar el estado, la memoria residente (`VmRSS`) y los hilos activos del proceso.

## 🧪 Experimento antes/durante/después
- **Antes:** Se registró un estado de reposo con una memoria disponible de ~10.6 GiB y carga baja.
- **Durante:** Se ejecutó el proceso `sleep 120`. Dado que `sleep` únicamente suspende su ejecución sin consumir CPU ni RAM significativa, los valores de memoria y carga se mantuvieron estables.
- **Después:** Tras la finalización del proceso, la memoria y la carga retornaron a sus niveles iniciales sin variaciones apreciables.

## 📸 Evidencias
Basandome en las lecturas obtenidas (`free -h`, `vmstat` y `/proc/meminfo`), el equipo cuenta con suficiente memoria RAM disponible (~10.6 GiB libres) y los promedios de carga (0.73) están muy por debajo de la capacidad de procesamiento de los 8 núcleos lógicos del procesador. No se presentan signos de saturación ni cuellos de botella por falta de RAM.

1. ¿Cuánta memoria está disponible, según free -h?

Según las lecturas obtenidas de /proc/meminfo y free -h, el equipo cuenta con 11,205,696 kB (aproximadamente 10.6 GiB a 11 GiB) de memoria disponible (MemAvailable) de un total de ~14.3 GiB.

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/84cda2d1f59129bd54ba4d2f79fc36798184f2e2/Captura%201.png)


2. ¿Existe swap configurada? ¿Está siendo utilizada?

No existe espacio Swap configurado en el sistema. Las lecturas de SwapTotal y SwapFree muestran 0 kB. Por lo tanto, no se está utilizando memoria de intercambio.

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/b6806742c4b9707cb7ddbfa7d0bb1e310f61141d/Captura%202.png)


3. ¿Qué procesos aparecen con mayor porcentaje de memoria?En el listado ordenado por uso de RAM (ps aux --sort=-%mem), los procesos que encabezan la lista son:Firefox (proceso web / contenido) con ~5.9% de RAM (PID 6491).   Firefox (proceso principal) con ~4.5% de RAM (PID 4912).   Firefox (proceso aislado / pestaña) con ~3.5% de RAM (PID 6196).   GNOME Shell (gnome-shell) con ~1.8% de RAM (PID 2597).

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/b6806742c4b9707cb7ddbfa7d0bb1e310f61141d/Captura%203.png)


4. ¿Qué procesos aparecen con mayor porcentaje de CPU?En el listado ordenado por uso de CPU (ps aux --sort=-%cpu), los procesos con mayor consumo en ese instante son:Firefox (proceso de contenido web) consumiendo 47.5% de CPU (PID 6491).   Firefox (proceso principal) consumiendo 36.0% de CPU (PID 4912).   Firefox (otra pestaña/subproceso) consumiendo 16.6% de CPU (PID 6196).   GNOME Shell (gnome-shell) consumiendo 15.4% de CPU (PID 2597).


![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/b6806742c4b9707cb7ddbfa7d0bb1e310f61141d/Captura%204.png)

5. ¿Qué indican si y so en vmstat?

    si (Swap-In): Representa la cantidad de memoria leída/traída desde la partición Swap hacia la RAM física por segundo (en KB/s).

    so (Swap-Out): Representa la cantidad de memoria escrita/enviada desde la RAM física hacia la Swap por segundo (en KB/s).

    En mi equipo, ambos valores permanecen en 0 porque no hay Swap configurada y hay suficiente RAM libre.

   ![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/af28137fdb6d8ec188bb7c04be17aa1184e58ed2/Captura%205.png)


6. ¿La carga promedio debe interpretarse como un porcentaje?

No, la carga promedio (load average) no es un porcentaje. Es un número que representa la cantidad promedio de procesos o hilos que están en estado ejecutable (usando CPU) o en espera no interrumpible (esperando operaciones de disco/entrada/salida) durante un intervalo de tiempo (1, 5 y 15 minutos).

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/6a27a793b360c1453fbd3f660716a9b32110051f/Captura%20%206.png)


7. ¿Qué relación existe entre la carga y el número de CPU lógicas?La carga se debe interpretar directamente contra el número de núcleos/hilos lógicos (nproc).En tu equipo dispones de 8 CPUs lógicas (Intel Core i5 con 4 núcleos / 8 hilos).   Una carga de 0.73 significa que, en promedio, menos de 1 procesador lógico de los 8 disponibles estuvo ocupado al 100%.   El sistema estaría saturado únicamente si la carga promedio superara de manera sostenida el valor de 8.0.

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/b2ab0587606f847d55125640b4370f148cb02ce2/Captura%207.png)

8. ¿Los datos respaldan la afirmación del usuario ("Mi computadora está lenta porque la RAM está al 90%")? Justifica.

No, los datos desmienten la afirmación del usuario.

  Justificación: La lectura muestra que hay más de 10.6 GiB de RAM disponible de un total de ~14.3 GiB (más del 70% de la RAM física está completamente disponible para uso inmediato). El usuario probablemente confundió la memoria en caché (buff/cache) con memoria ocupada de manera irreversible. Si el equipo presenta alguna lentitud puntual, se debe más al consumo transitorio de CPU por parte del navegador (alrededor del 47.5%) y no a la falta de RAM.

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3c04271df6d395d2b14b9655753436e567848534/Captura%208.png)


9. ¿Qué otra información necesitarías antes de recomendar cerrar procesos o ampliar RAM?

    Monitorear el estado de lectura/escritura del disco duro/SSD (métrica wa en vmstat o mediante iostat).

    Analizar el comportamiento de la RAM de forma prolongada mientras el usuario realiza sus actividades habituales más pesadas.

    Verificar la temperatura del procesador para descartar estrangulamiento térmico (thermal throttling).

   ![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/ef474316c343581103c918ff7daf2a186ea3bb37/Captura%209.png)

10. Propón dos acciones prudentes que no pongan en riesgo el trabajo del usuario.

    Pestañas de Firefox: Identificar y cerrar o suspender únicamente aquellas pestañas pesadas o inactivas dentro de Firefox (usando administradores de pestañas como Auto Tab Discard o el propio administrador de tareas interno de Firefox Shift + Esc) sin cerrar el navegador por completo ni arriesgar perder trabajo en progreso.

    Optimización de memoria en background: Limpiar la caché secundaria del sistema si fuera necesario mediante el Kernel o simplemente dejar que el asignador de memoria de Linux libere buff/cache automáticamente a medida que las aplicaciones lo requieran, sin necesidad de invertir en hardware adicional ni forzar cierres de aplicaciones.

## Conclusión
Comprendí que la memoria reportada como "usada" por Linux a menudo incluye cachés y buffers (`buff/cache`) que el Kernel maneja eficientemente para agilizar el sistema y que pueden ser liberados al instante cuando una aplicación lo requiera. Además, aprendí a verificar la carga relativa del procesador comparándola con la cantidad de CPUs lógicas (`nproc`).
