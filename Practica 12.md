# 🔵 Semana 12 — Seguridad, permisos y firewall UFW en Ubuntu

## 👤 Datos del alumno
- **Nombre:** José Gerardo Cabrera Miranda
- **Fecha:** Noviembre de 2026

## 🖥️ Entorno de Trabajo
- **Distribución y versión:** Ubuntu 26.04.1 LTS (Resolute Raccoon)
- **Kernel:** Linux 7.0.0-42-generic (x86_64)
- **Equipo:** Físico (Lenovo ThinkPad L490)

## 🎯 Objetivo de la práctica
Comprender las medidas básicas de seguridad en Ubuntu, aplicar el principio de mínimo privilegio, identificar los servicios y puertos en escucha mediante sockets, consultar de forma controlada el estado y las reglas del firewall UFW, y analizar la relación entre los permisos de archivos y el filtrado de red.

---

## 📋 Inventario y Resultados de Seguridad y Firewall

| Componente / Concepto | Comando utilizado | Descripción del resultado obtenido en el equipo |
|---|---|---|
| **Identidad y Privilegios** | `whoami` / `id` | Se verificaron los permisos, identificadores de usuario y grupos asociados a la sesión actual dentro del sistema operativo. |
| **Permisos de Archivos** | `ls -l ~/SistemasOperativos` | Se examinaron los permisos de acceso, propietario y grupo sobre las carpetas de trabajo del curso. |
| **Sockets en Escucha** | `sudo ss -lntup` | Se consultaron los puertos TCP/UDP abiertos y los procesos del sistema asociados a ellos para detectar servicios activos. |
| **Estado y Políticas de UFW** | `sudo ufw status verbose` | Se comprobó el estado operativo del cortafuegos y las políticas predeterminadas de entrada (*incoming*) y salida (*outgoing*). |
| **Enumeración de Reglas** | `sudo ufw status numbered` | Se listaron las reglas de filtrado existentes de manera numerada para su correcta identificación y control. |

---

## 📸 Registro de Evidencias (Capturas)

Las siguientes capturas se encuentran almacenadas en la carpeta `semana12/evidencias/`:

1. **`01_usuario_permisos_y_sockets.png`**  
   Verificación de identidad (`id`), permisos de directorios de trabajo y sockets en escucha (`sudo ss -lntup`).
   ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/05d4e9d482a484c9d59ec18e4f746f5a4414c645/EVI%201.png)
3. **`02_estado_ufw.png`**  
   Consulta detallada del estado operativo del cortafuegos, políticas predeterminadas y reglas configuradas (`sudo ufw status verbose`, `sudo ufw status numbered`).
   ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/1ff4084f2294c1fd6a2605c56607003021e88c56/EVI%202.png)
5. **`03_diseno_politica_minima.png`**
   Diseño y planeación de una política de mínimos privilegios y servicios necesarios para el entorno.
   ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3551eb2e26f1411b5ce75a037147f3feba723e2f/EVI%203.png)
   ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/036284a16dc60c2cbbef5e6eb360b912814a46ff/EVI3.png)
7. **`04_verificacion_reglas.png`**  
   Verificación del estado del firewall tras la revisión de reglas y políticas de seguridad.
   ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/2d75bbbe94db8d576cfe73ff6afaa5f62cbdd158/EVI%204.png)
9. **`05_revision_final.png`**  
   Comprobación de la integridad, revisión de permisos y cierre de la auditoría de seguridad en el sistema operativo.
   ![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/845dd2df1bd17b6bc552bee41a2a786b6b5bc81f/EVI%205.png)

---

## 🧠 Preguntas de Análisis y Repaso

1. **¿Qué es el principio de mínimo privilegio?**  
   *Es una directriz de seguridad que establece que un usuario, proceso o programa debe contar únicamente con los permisos estrictamente necesarios para cumplir su función.*

2. **¿Qué diferencia hay entre un puerto y un servicio?**  
   *El puerto es el identificador numérico lógico dentro de la capa de transporte, mientras que el servicio es el programa o aplicación que utiliza dicho puerto para escuchar y atender conexiones.*

3. **¿Qué significa que un socket esté en escucha?**  
   *Indica que hay un proceso preparado y a la espera de recibir solicitudes de conexión o datagramas entrantes en una dirección y puerto específicos.*

4. **¿Qué es un firewall?**  
   *Es un sistema de defensa que controla el tráfico de red permitiendo o bloqueando paquetes basándose en un conjunto de reglas preestablecidas.*

5. **¿Para qué sirve UFW?**  
   *Es una interfaz simplificada en Ubuntu diseñada para administrar y configurar las reglas del cortafuegos del kernel de manera más intuitiva.*

6. **¿Qué información muestra `ufw status verbose`?**  
   *Muestra si el cortafuegos está activo, las políticas predeterminadas para el tráfico entrante y saliente, y el estado de registro.*

7. **¿Para qué sirve `ufw status numbered`?**  
   *Muestra las reglas activas precedidas por un número índice, lo cual facilita modificarlas o eliminarlas de forma precisa.*

8. **¿Qué diferencia existe entre tráfico de entrada y salida?**  
   *El tráfico de entrada es el que proviene de redes externas hacia el equipo, y el de salida es el que se origina en el equipo hacia otros destinos.*

9. **¿Por qué se deben revisar las reglas existentes antes de modificarlas?**  
   *Para evitar bloquear accesos críticos de administración remota (como SSH) que corten la conexión con el equipo.*

10. **¿Por qué un puerto en escucha no demuestra automáticamente que sea vulnerable?**  
    *Porque el hecho de que un puerto esté abierto solo indica que un servicio está esperando conexiones; la vulnerabilidad depende de la seguridad, versión y configuración de dicho servicio.*

11. **¿Qué diferencia hay entre los permisos de archivos y el filtrado de red?**  
    *Los permisos de archivos controlan quién puede leer, escribir o ejecutar recursos locales en el sistema de archivos, mientras que el firewall controla qué paquetes de red pueden ingresar o salir del equipo.*

12. **¿Por qué no debe ejecutarse `ufw reset` como parte de una práctica rutinaria?**  
    *Porque borra todas las reglas configuradas y puede dejar el sistema desprotegido o interrumpir servicios de red esenciales.*

---

## 🏁 Conclusión
La práctica permitió entender la relevancia de auditar de manera constante los servicios activos, los permisos locales y las reglas del cortafuegos. La aplicación del principio de mínimo privilegio y el uso responsable de UFW garantizan que el sistema mantenga una postura defensiva sólida sin comprometer su operatividad ni el acceso legítimo.
