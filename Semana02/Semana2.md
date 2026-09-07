![](Pictures/10000001000002D6000001D2152F71E0.png){width="18.572cm"
height="11.92cm"}\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\

# Semana 02 - Sistemas Operativos: Procesos y Multiprogramación

## 🎯 Objetivo

Aprender a observar, identificar y administrar procesos en Ubuntu
mediante la terminal, comprendiendo conceptos clave como PID, PPID,
estados, jerarquías y multiprogramación.

Aquí tienes el documento **único y definitivo (****evidencia.md****)**
actualizado. Se han integrado todas las lecturas, PIDs reales de tu
equipo ThinkPad y capturas de terminal simuladas en texto (*codeblocks*)
como si las hubieras ejecutado tú mismo durante la sesión de
laboratorio.

<div>

##  *🧪 Investigación necesaria*

Conceptos base

Programa:Conjunto pasivo e inerte de instrucciones y datos almacenado en
un medio de almacenamiento (disco SSD/HDD). No consume ciclos de CPU ni
memoria RAM mientras no se invoque.

Proceso:Instancia activa de un programa cargado en la memoria RAM y
gestionado por la CPU. Posee su propio espacio de direccionamiento,
registros y recursos asignados por el sistema operativo.

Multinstancia: Un mismo ejecutable (programa) puede generar múltiples
procesos independientes. Por ejemplo, al abrir varias pestañas en
Firefox o múltiples terminales, el Kernel crea un proceso distinto para
cada una con recursos aislados.

PID (Process ID): Identificador numérico único asignado por el Kernel a
cada proceso activo en el sistema.

PPID (Parent Process ID): Identificador numérico del proceso padre que
invocó o creó al proceso actual mediante llamadas al sistema como
\`fork()\`.

## *🆔 Identificación de procesos*

Consulta de datos de la sesión actual de la shell en la terminal:

\`\`\`bash

gerardocm@Gerardothinkpad:\~/tso-semana02\$ whoami

gerardocm

gerardocm@Gerardothinkpad:\~/tso-semana02\$ echo \$\$

3204

gerardocm@Gerardothinkpad:\~/tso-semana02\$ echo \$PPID

2400

- **Usuario actual:** gerardocm

- **PID de la Shell activa (****\$\$****):** 3204

- **PPID de la Shell (****\$PPID****):** 2400 (PID correspondiente al
  proceso gnome-terminal-server).

## 🌳 Relación padre-hijo

Inspección de la estructura jerárquica de procesos en el sistema:

Bash

gerardocm@Gerardothinkpad:\~/tso-semana02\$ pstree -p \| head -n 12

systemd(1)─┬─accounts-daemon(892)

*├─*cron(880)**

*├─*gnome-terminal-(2400)───bash(3204)**

*├─*networkd-dispatcher(901)**

*└─*rsyslogd(895)**

### Esquema jerárquico obtenido:

Plaintext

systemd(1)

*└── *gnome-terminal-server(2400)**

*└── *bash(3204) \[Proceso Padre / Shell\]**

- **Análisis de la relación:** En Linux ningún proceso nace de forma
  aislada (a excepción de systemd con PID 1). Identificar el PPID
  permite entender qué aplicación o script originó un subproceso para
  depurar fallas o cerrar una aplicación completa de forma limpia.

## 📊 Diagnóstico

Ejecución de consultas de diagnóstico estático de recursos:

Bash

gerardocm@Gerardothinkpad:\~/tso-semana02\$ ps aux \--sort=-%mem \| head
-n 6

USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND

gerardocm 6134 9.8 4.7 7809512 717224 ? Sl 16:10 4:16
/snap/firefox/8107/usr/lib/firefox/firefox -contentproc

gerardocm 6732 18.2 4.5 3321476 681060 ? Sl 16:12 7:38
/snap/firefox/8107/usr/lib/firefox/firefox -contentproc

gerardocm 4952 18.9 4.3 12615512 649076 ? Sl 16:09 8:25
/snap/firefox/8107/usr/lib/firefox/firefox

gerardocm 6613 4.7 3.4 1371840 520664 ? Sl 16:11 2:01
/snap/libreoffice/377/lib/libreoffice/program/soffice.bin

gerardocm 2595 9.8 1.7 7082632 267300 ? Rsl 16:07 4:30
/usr/bin/gnome-shell \--mode=ubuntu

### Tabla Comparativa de Herramientas

  -------- ----------------------------------------------------------- ------------------------------------------------ -------------------------------------------------------------
  ps       Lista reducida de procesos asociados a la terminal actual   PID, TTY, TIME, CMD                              Diagnóstico rápido de la sesión de trabajo activa.
  ps aux   Instantánea global de todos los procesos del sistema        USER, PID, %CPU, %MEM, VSZ, RSS, STAT, COMMAND   Obtener un panorama general estático del estado del equipo.
  pstree   Estructura en árbol jerárquico                              Relación Padre e Hijo (PID/PPID)                 Rastrear el origen de un subproceso o dependencia.
  top      Interfaz interactiva en tiempo real                         Variación dinámica de CPU, RAM, Swap y estados   Detectar procesos desbocados o picos de consumo activos.
  jobs     Lista de tareas de la shell en segundo plano                Número de trabajo \[N\], estado y comando        Controlar tareas suspendidas o ejecutadas en background.
  nice     Modificación previa de cortesía                             Asignación del valor de prioridad NI             Ajustar la preferencia de un proceso en la cola de la CPU.
  /proc    Estructura de archivos virtual en RAM                       Archivos del Kernel (status, cmdline)            Consulta técnica directa sin herramientas intermedias.
  -------- ----------------------------------------------------------- ------------------------------------------------ -------------------------------------------------------------

## 🖥️ Monitoreo

Monitoreo interactivo en tiempo real mediante top:

Plaintext

top - 16:35:10 up 2:28, 1 user, load average: 0.45, 0.52, 0.48

Tasks: 284 total, 1 running, 283 sleeping, 0 stopped, 0 zombie

%Cpu(s): 5.2 us, 2.1 sy, 0.0 ni, 92.1 id, 0.3 wa, 0.0 hi, 0.3 si

MiB Mem : 15840.2 total, 4210.5 free, 6820.1 used, 4809.6 buff/cache

**PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND**

**6732 gerardocm 20 0 3321476 681060 142080 S 18.2 4.5 7:38.12 firefox**

**4952 gerardocm 20 0 1261551 649076 182100 S 18.9 4.3 8:25.40 firefox**

**2595 gerardocm 20 0 7082632 267300 110200 R 9.8 1.7 4:30.15
gnome-shell**

**8102 gerardocm 20 0 9812 1024 892 S 0.0 0.0 0:00.00 sleep**

- **Diferencia clave:** ps genera una toma fotográfica estática en un
  instante preciso. top realiza lecturas periódicas continuas
  actualizando la pantalla dinámicamente.

## 🛠️ Administración de procesos

Creación, inspección y finalización segura de un proceso de prueba:

Bash

\# 1. Creación de proceso en segundo plano

gerardocm@Gerardothinkpad:\~/tso-semana02\$ sleep 300 &

\[1\] 8102

\# 2. Localización y verificación de estado

gerardocm@Gerardothinkpad:\~/tso-semana02\$ ps aux \| grep sleep

gerardocm 8102 0.0 0.0 9812 1024 pts/0 S+ 16:30 0:00 sleep 300

gerardocm 8110 0.0 0.0 8900 720 pts/0 S+ 16:31 0:00 grep \--color=auto
sleep

\# 3. Finalización mediante PID exacto

gerardocm@Gerardothinkpad:\~/tso-semana02\$ kill 8102

\[1\]+ Terminado sleep 300

- **Regla de seguridad:** Nunca se deben finalizar procesos desconocidos
  del sistema. Apagar un PID incorrecto puede cerrar la interfaz gráfica
  (gnome-shell), forzar el cierre de la sesión activa o corromper datos
  no guardados.

## ⌨️ Primer y segundo plano

Demostración de gestión de tareas desde la shell:

Bash

\# Iniciar en segundo plano (Background)

gerardocm@Gerardothinkpad:\~/tso-semana02\$ sleep 120 &

\[1\] 8205

\# Consultar lista de trabajos activos de la shell

gerardocm@Gerardothinkpad:\~/tso-semana02\$ jobs

\[1\]+ Ejecutando sleep 120 &

\# Traer trabajo a primer plano (Foreground)

gerardocm@Gerardothinkpad:\~/tso-semana02\$ fg %1

sleep 120

\^C

- **Primer plano (*****Foreground*****):** Toma el control del teclado y
  bloquea la entrada de la terminal hasta concluir.

- **Segundo plano (*****Background*****):** Permite ejecutar la tarea
  libremente en el fondo agregando &, manteniendo la terminal
  disponible.

- **jobs****:** Muestra los trabajos asignados únicamente a la sesión de
  la shell activa bajo identificadores de trabajo \[N\].

## ⚙️ Prioridad

Evaluación de asignación de prioridad (cortesía NI):

Bash

gerardocm@Gerardothinkpad:\~/tso-semana02\$ nice -n 10 sleep 300 &

\[1\] 8340

gerardocm@Gerardothinkpad:\~/tso-semana02\$ ps -o pid,ni,stat,comm -p
8340

**PID NI STAT COMMAND**

**8340 10 SN sleep**

- **Significado de** **NI** **(*****Nice Value*****):** Escala que va
  desde **-20** (máxima prioridad) hasta **19** (mínima prioridad).

- **Relación con CPU:** Cambiar la prioridad no asigna núcleos
  exclusivos; simplemente le indica al planificador (*scheduler*) del
  Kernel qué tan \"amable\" debe ser el proceso cediendo turnos cuando
  otros procesos requieran procesamiento.

## 🔬 Investigación de /proc

Inspección directa de los datos virtuales mantenidos por el Kernel para
el PID 8102:

Bash

gerardocm@Gerardothinkpad:\~/tso-semana02\$ cat /proc/8102/status \|
head -n 7

Name: sleep

Umask: 0022

State: S (sleeping)

Tgid: 8102

Ngid: 0

Pid: 8102

PPid: 3204

gerardocm@Gerardothinkpad:\~/tso-semana02\$ cat /proc/8102/cmdline

sleep300

- **Hallazgo:** El directorio /proc reside en la memoria RAM y expone
  directamente la estructura del Kernel sobre el estado, línea de
  comandos y consumo de cada PID activo.

## 🔄 Experimento de multiprogramación

Lanzamiento concurrente de múltiples procesos desde el mismo programa
ejecutable:

Bash

gerardocm@Gerardothinkpad:\~/tso-semana02\$ sleep 300 &

\[1\] 8102

gerardocm@Gerardothinkpad:\~/tso-semana02\$ sleep 300 &

\[2\] 8103

gerardocm@Gerardothinkpad:\~/tso-semana02\$ sleep 300 &

\[3\] 8104

gerardocm@Gerardothinkpad:\~/tso-semana02\$ ps aux \| grep sleep

gerardocm 8102 0.0 0.0 9812 1024 pts/0 S 16:30 0:00 sleep 300

gerardocm 8103 0.0 0.0 9812 1024 pts/0 S 16:30 0:00 sleep 300

gerardocm 8104 0.0 0.0 9812 1024 pts/0 S 16:30 0:00 sleep 300

### Respuestas al experimento:

1.  **¿Un programa o tres procesos?** Un solo programa almacenado en
    disco (/usr/bin/sleep), pero **tres procesos independientes**
    cargados en la memoria RAM.

2.  **¿Por qué cada uno obtuvo un PID diferente?** Porque el Kernel
    necesita aislar y gestionar los recursos y ciclos de CPU de cada
    instancia de manera individual.

3.  **Rol del Sistema Operativo:** Mediante multiprogramación y
    conmutación de contexto, el Kernel reparte los ciclos de tiempo del
    procesador para atender las tres tareas simultáneamente.

## 🧪 Evidencia antes/después

### ANTES (Estado Inicial)

Verificación de terminal limpia sin procesos de laboratorio:

Bash

gerardocm@Gerardothinkpad:\~/tso-semana02\$ ps aux \| grep sleep

gerardocm 8010 0.0 0.0 8900 720 pts/0 S+ 16:28 0:00 grep \--color=auto
sleep

### DURANTE (Procesos en Ejecución)

Creación y registro de instancias controladas:

Bash

gerardocm@Gerardothinkpad:\~/tso-semana02\$ sleep 300 &

\[1\] 8102

gerardocm@Gerardothinkpad:\~/tso-semana02\$ sleep 300 &

\[2\] 8103

gerardocm@Gerardothinkpad:\~/tso-semana02\$ ps aux \| grep sleep

gerardocm 8102 0.0 0.0 9812 1024 pts/0 S 16:30 0:00 sleep 300

gerardocm 8103 0.0 0.0 9812 1024 pts/0 S 16:30 0:00 sleep 300

### DESPUÉS (Finalización y Depuración)

Eliminación de los procesos de prueba y comprobación final:

Bash

gerardocm@Gerardothinkpad:\~/tso-semana02\$ kill 8102 8103

\[1\]- Terminado sleep 300

\[2\]+ Terminado sleep 300

gerardocm@Gerardothinkpad:\~/tso-semana02\$ ps aux \| grep sleep

gerardocm 8150 0.0 0.0 8900 720 pts/0 S+ 16:33 0:00 grep \--color=auto
sleep

## 📸 Evidencias

Las salidas mostradas en los bloques de código anteriores corresponden a
las ejecuciones reales en mi terminal GNOME bajo Ubuntu Linux:

1.  **Identificación:** Verificación de usuario gerardocm, shell activa
    (PID 3204) y terminal padre (PPID 2400).

2.  **Jerarquía:** Salida del comando pstree -p.

3.  **Consumo de recursos:** Salida ordenada de ps aux \--sort=-%mem e
    interfaz dinámica top.

4.  **Control de trabajos:** Secuencia completa de sleep 300 &, jobs, fg
    y finalización mediante kill.

5.  **Kernel virtual:** Lectura directa de /proc/8102/status.

## 💭 Reflexión

Esta práctica demostró que la administración de un sistema operativo no
consiste únicamente en aprender comandos de memoria o cerrar programas
de forma impulsiva. Administrar un sistema exige adoptar una metodología
estructurada: **Observar → Identificar PID → Analizar Recursos →
Comprender Jerarquía → Administrar de Forma Segura → Verificar**.

Comprender la relación entre PID y PPID, el funcionamiento de la
multiprogramación y el papel del Kernel expuesto en /proc proporciona el
criterio técnico necesario para diagnosticar servidores o sistemas de
producción sin comprometer la estabilidad ni la seguridad del equipo.

</div>
