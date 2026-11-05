# 🔵 Semana 10 — Servicios y arranque con systemd en Ubuntu

## 👤 Datos del alumno
- **Nombre:** José Gerardo Cabrera Miranda
- **Fecha:** Noviembre de 2026

## 🖥️ Entorno de Trabajo
- **Distribución y versión:** Ubuntu 26.04.1 LTS (Resolute Raccoon)
- **Kernel:** Linux 7.0.0-42-generic (x86_64)
- **Equipo:** Físico (Lenovo ThinkPad L490)[cite: 4, 8]

## 🎯 Objetivo de la práctica
Comprender cómo Ubuntu administra los servicios y el proceso de arranque mediante `systemd`, consultando estados, registros del sistema y operando de forma controlada sobre unidades de servicio no críticas[cite: 4].

---

## 📋 Inventario y Resultados de la Administración de Servicios

| Componente / Concepto | Comando utilizado | Descripción del resultado obtenido en el equipo |
|---|---|---|
| **Estado General del Sistema** | `systemctl is-system-running` / `uptime` | Se verificó el tiempo activo de la laptop, la hora de inicio con `who-b` y que el administrador de servicios opera de manera estable[cite: 4]. |
| **Unidades Fallidas** | `systemctl --failed` | Se realizó la consulta de unidades con errores en el arranque, confirmando que no existen servicios caídos o fallidos en la sesión actual[cite: 4]. |
| **Estado de un Servicio Específico** | `systemctl status systemd-timesyncd` | Se consultó la unidad de sincronización de tiempo, evaluando sus propiedades mediante `is-active` e `is-enabled`[cite: 4]. |
| **Registros del Servicio** | `journalctl -u systemd-timesyncd -n 40` | Se examinaron los eventos recientes registrados exclusivamente para la unidad en el *journal* del sistema[cite: 4]. |
| **Dependencias y Arranque** | `systemctl get-default` / `list-dependencies` | Se identificó el objetivo predeterminado del sistema operativo y las dependencias asociadas a la unidad investigada[cite: 4]. |

---

## 📸 Registro de Evidencias (Capturas)

Las siguientes capturas se encuentran almacenadas en la carpeta `evidencias/` y respaldan la ejecución de los comandos:

1. **`01_estado_general_y_unidades_fallidas.png`**  
   Verificación del estado general de systemd, tiempo activo y control de unidades fallidas (`uptime`, `who -b`, `systemctl is-system-running`, `systemctl --failed`)[cite: 4].
2. **`02_estado_servicio.png`**  
   Consulta detallada del estado, actividad y habilitación del servicio seleccionado (`systemctl status`, `is-active`, `is-enabled`)[cite: 4].
3. **`03_registros_servicio.png`**  
   Revisión de los mensajes y eventos recientes del servicio filtrados mediante el registro del sistema (`journalctl -u`)[cite: 4].
4. **`05_dependencias_y_arranque.png`**  
   Visualización del objetivo predeterminado de arranque y el árbol de dependencias de la unidad (`systemctl get-default`, `list-dependencies`)[cite: 4].

---

## 🧠 Preguntas de Análisis y Repaso

1. **¿Qué es un servicio?**  
   *Es un programa o componente que se ejecuta en segundo plano para ofrecer funciones continuas al sistema operativo o a otras aplicaciones, sin necesidad de una ventana gráfica interactiva.*

2. **¿Qué función general cumple `systemd`?**  
   *Actúa como el sistema de inicio (*init*) y administrador central de procesos, unidades y servicios en las distribuciones modernas de Linux.*

3. **¿Para qué sirve `systemctl`?**  
   *Es la herramienta de la línea de comandos empleada para consultar, controlar y administrar el estado de las unidades gestionadas por `systemd`[cite: 4].*

4. **¿Qué diferencia hay entre `active` e `inactive`?**  
   *Indica si la unidad se encuentra ejecutándose en la memoria en ese preciso instante (`active`) o si está detenida (`inactive`).*

5. **¿Qué significa que un servicio esté en estado `failed`?**  
   *Significa que `systemd` detectó un error o que la unidad no pudo completarse de manera correcta durante su intento de inicio.*

6. **¿Qué diferencia existe entre `is-active` e `is-enabled`?**  
   *`is-active` evalúa si el servicio está corriendo ahora mismo, mientras que `is-enabled` indica si está configurado para arrancar de forma automática cada vez que se enciende el equipo.*

7. **¿Qué diferencia hay entre iniciar un servicio y habilitarlo?**  
   *Iniciar (`start`) lo pone en marcha de manera inmediata en la sesión actual, mientras que habilitar (`enable`) crea los vínculos necesarios para que inicie solo en futuros reinicios del sistema.*

8. **¿Qué información consulta `journalctl -u`?**  
   *Permite extraer y filtrar los mensajes y registros generados por el núcleo y el sistema exclusivamente para una unidad o servicio determinado[cite: 4].*

9. **¿Por qué una búsqueda sin coincidencias de errores no demuestra que todo esté correcto?**  
   *Porque la ausencia de palabras clave como "error" no garantiza que la aplicación esté cumpliendo correctamente con su lógica de negocio o tareas asignadas.*

10. **¿Por qué no debes detener un servicio crítico del sistema?**  
    *Porque podría interrumpir funciones esenciales de la red, el almacenamiento o la sesión de trabajo, comprometiendo la estabilidad de la computadora.*

---

## 🏁 Conclusión
La práctica permitió comprender el funcionamiento de `systemd` y la utilidad de `systemctl` para auditar y administrar servicios en Ubuntu. El análisis riguroso de estados, dependencias y registros evita la necesidad de recurrir a soluciones drásticas como reiniciar el equipo completo ante una falla operativa[cite: 4].
