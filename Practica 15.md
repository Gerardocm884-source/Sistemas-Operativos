# 🏆 Semana 15 — Proyecto Integrador: Administración completa de Ubuntu desde terminal

## 👤 Datos del alumno
- **Nombre:** José Gerardo Cabrera Miranda
- **Fecha:** 6 de noviembre de 2026
- **Grupo / Curso:** Sistemas Operativos
- **Entorno:** Ubuntu instalado en equipo físico (Lenovo ThinkPad L490)

## 🎯 Objetivo del proyecto
Demostrar la capacidad de administrar, diagnosticar e inspeccionar un entorno completo de Ubuntu a través de la interfaz de línea de comandos (CLI), integrando los conceptos fundamentales trabajados durante el semestre: reconocimiento del sistema, dispositivos de almacenamiento, gestión de usuarios y permisos, monitoreo de procesos, administración de paquetes y servicios, diagnóstico de red, seguridad de firewall y auditoría de registros de eventos (*logs*).

---

## 🧭 FReconocimiento del sistema

### Comandos ejecutados
```bash
cat /etc/os-release
uname -a
hostnamectl
uptime
date
uname -m
```

### Respuestas 
1. **¿Qué distribución y versión de Ubuntu utilizas?**  
   Ubuntu 26.04.1 LTS (Resolute Raccoon).
2. **¿Qué información aporta `uname -a`?**  
   Proporciona la arquitectura del sistema (`x86_64`), el nombre del host (`Gerardothinkpad`), la versión exacta del kernel de Linux (`7.0.0-42-generic`), la fecha de compilación del núcleo y el tipo de sistema operativo GNU/Linux.
3. **¿Cuál es el nombre del equipo?**  
   `Gerardothinkpad`.
4. **¿Qué significa el tiempo de actividad mostrado por `uptime`?**  
   Indica el tiempo continuo que lleva el sistema operativo encendido desde el último reinicio, el número de usuarios con sesión activa y la carga promedio del procesador (*load average*) en los últimos 1, 5 y 15 minutos.
5. **¿Por qué es importante registrar el entorno antes de diagnosticarlo?**  
   Porque la versión del kernel, la distribución de Linux y las características de la arquitectura determinan la disponibilidad de ciertos comandos, la compatibilidad de módulos y la ubicación de los archivos de configuración antes de aplicar cualquier acción correctiva.

---

## 💽 Almacenamiento y sistema de archivos

### Comandos ejecutados
```bash
lsblk
df -hT
df -i
findmnt
du -sh ~
```

### Respuestas 
1. **¿Qué dispositivos y particiones aparecen?**  
   Muestra la unidad de disco principal (SSD/HDD) identificada con sus correspondientes particiones de arranque EFI y la partición raíz de Linux.
2. **¿Cuál es el punto de montaje de la raíz (`/`)?**  
   El punto de montaje `/` corresponde al sistema de archivos principal donde reside toda la jerarquía de directorios de Ubuntu.
3. **¿Cuánto espacio libre tiene el sistema de archivos que contiene `/`?**  
   Muestra el espacio disponible en gigabytes mediante la columna *Avail* (Disponible) del comando `df -hT` sobre la fila del punto de montaje `/`.
4. **¿Qué diferencia hay entre el tamaño de un dispositivo en `lsblk` y el espacio disponible en `df -hT`?**  
   `lsblk` reporta la capacidad física o lógica total asignada al bloque/partición, mientras que `df -hT` reporta el espacio útil dentro del sistema de archivos formateado, descontando los bloques reservados para el sistema operativo y metadatos.
5. **¿Por qué revisarías el espacio antes de instalar paquetes o diagnosticar una falla?**  
   Para evitar fallos catastróficos por saturación de disco (100% de uso), lo que impediría la creación de archivos temporales, la escritura de registros en `/var/log` o el desempaquetado de nuevas aplicaciones.

---

## 👤 Usuarios, grupos y permisos

### Comandos ejecutados
```bash
id
groups
getent passwd "$(whoami)"
mkdir -p ~/SistemasOperativos/semana15/laboratorio_permisos
cd ~/SistemasOperativos/semana15/laboratorio_permisos
touch archivo_prueba.txt
chmod 640 archivo_prueba.txt
ls -l archivo_prueba.txt
stat archivo_prueba.txt
```

### Respuestas 
1. **¿Cuál es tu UID y GID?**  
   El UID (User ID) es `1000` (`gerardocm`) y el GID (Group ID) principal es `1000` (`gerardocm`).
2. **¿A qué grupos perteneces?**  
   Pertenece a `gerardocm`, `sudo`, `adm`, `cdrom`, `dip`, `plugdev`, `lpadmin`, entre otros grupos de administración local.
3. **¿Qué representan los permisos `rw-r-----` (`640`)?**  
   - **6 (Propietario):** Lectura y escritura (`rw-`).
   - **4 (Grupo):** Solo lectura (`r--`).
   - **0 (Otros):** Sin ningún tipo de acceso (`---`).
4. **¿Qué riesgo existe si se conceden permisos de escritura a todos los usuarios (`777` o `o+w`)?**  
   Cualquier usuario o proceso local sin privilegios podría modificar, corromper o vaciar el contenido de archivos críticos o ejecutables del sistema.
5. **¿Qué diferencia hay entre propietario, grupo y otros?**  
   El **propietario** es el usuario creador/dueño del archivo; el **grupo** define los privilegios para los integrantes del grupo secundario asignado; y **otros** aplica a cualquier cuenta del sistema que no sea ni el dueño ni pertenezca al grupo.

---

## ⚙️ Procesos y recursos del sistema

### Comandos ejecutados
```bash
ps aux
ps -eo pid,ppid,comm,%cpu,%mem --sort=-%cpu | head
free -h
uptime
top
```

### Respuestas
1. **¿Qué información identifica un PID?**  
   El PID (*Process ID*) es el identificador numérico único asignado por el kernel de Linux a cada proceso en ejecución dentro del sistema.
2. **¿Qué proceso aparece usando más CPU en la consulta realizada?**  
   Corresponde al proceso situado en la parte superior del listado ordenado por porcentaje de uso de CPU (`%cpu`).
3. **¿Cuánta memoria está disponible según `free -h`?**  
   Se observa bajo la columna *available* (disponible), la cual considera la RAM libre y la memoria en caché que se puede liberar de inmediato para nuevas aplicaciones.
4. **¿Qué diferencia hay entre memoria total, usada y disponible?**  
   - **Total:** La cantidad física instalada en el equipo.
   - **Usada:** RAM reservada activamente por procesos y kernel.
   - **Disponible:** Estimación real de cuánta RAM se puede asignar inmediatamente sin forzar intercambio en SWAP.
5. **¿Por qué no se debe terminar un proceso únicamente porque su consumo parezca alto?**  
   Porque podría tratarse de un proceso crítico del núcleo o un daemon esencial del sistema (como `systemd` o servicios de red), y forzar su finalización causaría inestabilidad o el colapso del sistema operativo.

---

## 📦 Paquetes y software instalado

### Comandos ejecutados
```bash
dpkg -l
dpkg -s bash
apt show bash
apt list --upgradable
```

### Respuestas 
1. **¿Qué diferencia existe entre `apt` y `dpkg`?**  
   `dpkg` es la herramienta de bajo nivel que gestiona la instalación/remoción directa de archivos `.deb` individuales sin resolver dependencias; mientras que `apt` es el gestor de alto nivel que descarga paquetes desde repositorios remotos y resuelve dependencias de forma automática.
2. **¿Qué información encontraste sobre el paquete `bash`?**  
   Muestra que se encuentra instalado en estado `install ok installed`, su versión exacta, arquitectura, desarrollador/mantenedor y una breve descripción como el interprete de comandos estándar de GNU.
3. **¿Por qué conviene revisar la información de un paquete antes de instalarlo?**  
   Para verificar su procedencia, espacio requerido en disco, versión exacta y el listado de dependencias que añadirá al sistema.
4. **¿Por qué no debes ejecutar una actualización completa (`apt upgrade`) sin revisar el impacto?**  
   Porque actualizar librerías del sistema o servicios de producción sin prueba previa puede romper configuraciones existentes o volver incompatibles aplicaciones en uso.

---

## ⚡ Servicios del sistema

### Comandos ejecutados
```bash
systemctl --failed
systemctl list-units --type=service --state=running
systemctl status cron --no-pager
journalctl -u cron -n 30 --no-pager
```

### Respuestas 
1. **¿Qué diferencia hay entre un servicio activo y uno habilitado?**  
   - **Activo (*running*):** El servicio se está ejecutando en la memoria RAM en este momento.
   - **Habilitado (*enabled*):** El servicio está configurado para iniciar automáticamente cada vez que el sistema operativo encienda.
2. **¿Qué informa `systemctl --failed`?**  
   Devuelve las unidades o servicios de `systemd` que entraron en estado de error durante el arranque o la operación actual (`0 loaded units listed` si no hay fallos).
3. **¿Qué datos aparecen en `systemctl status`?**  
   Nombre de la unidad, estado del servicio, estado de autoarranque, Main PID, árbol de procesos hijos (CGroup), uso de memoria/CPU y las últimas líneas de registro emitidas.
4. **¿Cómo relacionarías el estado de un servicio con sus registros?**  
   Si `systemctl status` reporta un fallo (`failed`), `journalctl -u NOMBRE_SERVICIO` permite inspeccionar exactamente la línea de código, error de sintaxis o timestamp que provocó la caída.
5. **¿Qué verificarías antes de reiniciar un servicio?**  
   Verificar si hay usuarios/procesos activos dependiendo de él, revisar la sintaxis de sus archivos de configuración y comprobar los registros previos para evitar reiniciar un servicio con errores estructurales.

---

## 🌐 Red, conexiones y puertos

### Comandos ejecutados
```bash
ip addr
ip route
ping -c 4 127.0.0.1
ping -c 4 1.1.1.1
ss -tuln
```

### Respuestas 
1. **¿Qué interfaces aparecen y cuál tiene una dirección IP asignada?**  
   Aparece `lo` (interfaz de loopback `127.0.0.1`) y la interfaz física Ethernet configurada localmente con la IP asignada por la red.
2. **¿Qué función cumple la ruta predeterminada (*default gateway*)?**  
   Indica la dirección IP del router o módem al que deben enviarse todos los paquetes de red cuya IP de destino no pertenezca a la red local.
3. **¿Qué diferencia existe entre una dirección IP y un nombre de dominio?**  
   La dirección IP es el identificador numérico jerárquico de un nodo en la red, mientras que el nombre de dominio es un alias legible para humanos resuelto mediante el protocolo DNS.
4. **¿Qué significa que un puerto esté en escucha (*LISTEN*)?**  
   Que un servicio o daemon está ejecutándose localmente y permanece a la espera de recibir conexiones o peticiones en ese número de puerto específico.
5. **¿Por qué no se debe exponer un servicio sin conocer su función y sus riesgos?**  
   Porque exponer puertos no auditados abre vectores de ataque para accesos no autorizados, explotación de vulnerabilidades conocidas o denegación de servicio.

---

## 🛡️ Firewall y revisión básica de seguridad

### Comandos ejecutados
```bash
sudo ufw status verbose
ss -tuln
```

### Respuestas
1. **¿Está activo UFW?**  
   Muestra el estado reportado por `sudo ufw status verbose` (`active` o `inactive`).
2. **¿Qué política predeterminada y reglas se muestran?**  
   En un entorno estándar suele configurarse en *deny (incoming)* para denegar todo el tráfico entrante no explícitamente autorizado y *allow (outgoing)* para permitir la salida de tráfico.
3. **¿Qué servicios aparecen escuchando?**  
   Los sockets locales filtrados por `ss -tuln` (comúnmente resolutores DNS locales, servicios RPC o servidores locales).
4. **¿Todos los puertos en escucha tienen que estar expuestos a otras máquinas? Explica.**  
   No. Los servicios que solo requieran comunicación interna deben vincularse exclusivamente a la interfaz local `127.0.0.1` (*localhost*) para no ser accesibles desde la red externa.
5. **¿Qué significa aplicar el principio de mínimo privilegio?**  
   Conceder únicamente los permisos de acceso, puertos abiertos y privilegios de usuario strictly necesarios para cumplir una función específica, restringiendo todo lo demás por defecto.

---

## 📝 Logs y diagnóstico

### Comandos ejecutados
```bash
journalctl -n 50 --no-pager
journalctl -b -n 50 --no-pager
sudo dmesg | grep -iE 'error|fail|warn' | tail -n 30
```

### Caso de diagnóstico
1. **¿Qué ocurrió?**  
   Se identificó una advertencia en `cron.service` (*"Referenced but unset environment variable evaluates to an empty string: EXTRA_OPTS"*) y avisos informativos del kernel.
2. **¿Cuándo ocurrió?**  
   Durante el proceso de arranque del sistema registrado en la sesión actual.
3. **¿Qué componente o servicio estuvo involucrado?**  
   `cron.service` y el cargador de módulos del kernel de Linux.
4. **¿Dónde se registró?**  
   En el journal de `systemd` (`journalctl -u cron`) y en el buffer del núcleo (`dmesg`).
5. **¿Qué hipótesis razonable planteas?**  
   El servicio intenta leer una variable opcional de entorno en `/etc/default/cron` que no está definida; sin embargo, al ser un aviso secundario, el daemon opera con total normalidad.
6. **¿Qué comprobarías después?**  
   Ejecutar `systemctl status cron` para corroborar el estado `active (running)` y validar que los trabajos programados sigan ejecutándose.
7. **¿Se solucionó?**  
   Se determinó que no requiere intervención destructiva ni reinicios, quedando auditado y operativo.

---

## 📋Evidencias 

|---|---|---|
| `01_reconocimiento.png` | Reconocimiento del sistema | `cat /etc/os-release`, `uname -a`, `uptime` |

![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/97ecb44d07e9f33330aa55dc0f0d8ae7bfe316c4/Evdencia%201.png)
| `02_almacenamiento.png` | Discos y almacenamiento | `lsblk`, `df -hT` |
![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/9fc2af22ed662f71dfe7bd92fc849f4221abb654/Evdencia%202.png)

| `03_usuarios_permisos.png` | Identidad y permisos | `id`, `ls -l archivo_prueba.txt` (`640`) |
![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/c69616e686f0d45fb94c54431f7e950a7819d57a/Evdencia%203.png)

| `04_procesos_recursos.png` | Recursos y procesos | `ps -eo ... --sort=-%cpu`, `free -h` |
![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/711e39cff06a355999447bb648f34fc925d90264/Evdencia%204.png)

| `05_paquetes_servicios.png` | Paquetes y servicios | `dpkg -s bash`, `systemctl status cron` |
![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/6d7e7939e7f8b2be5f92adcf79ddbbbd995af03a/Evdencia%205.png)

| `06_red_firewall.png` |  Red, sockets y UFW | `ip addr`, `ss -tuln`, `sudo ufw status verbose` |
![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/7ea35b966ec4bcea21dec8b815d3283783f0af47/Evdencia%206.png)

| `07_logs_diagnostico.png` | Logs y diagnóstico | `journalctl -u cron`, `dmesg` |
![Image](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/663f1cfe3ce54e5cb01654063b1d157e133128bd/Evdencia%207.png)


---

## 🏁 Conclusiones
El desarrollo del proyecto integrador consolida el uso de la terminal de Linux como la interfaz principal y más potente para la administración de sistemas operativos. Se demostró que la inspección metódica mediante herramientas CLI permite verificar el estado real de un servidor o equipo de escritorio, interpretar mensajes de error y aplicar medidas de seguridad de forma fundamentada y sin riesgos.
