# **Laboratorio de Sistemas Operativos — Reporte de Instalación**

**Práctica:** Instalación y Configuración de Metasploitable 2 en VirtualBox

## **31\. Tabla de Registro de Evidencia**

| Dato | Resultado del Laboratorio   |
| :---- | :---- |
| **Alumno** | José Gerardo Cabrera Miranda |
| **Fecha** | 15 de septiembre de 2026 |
| **Ubuntu** | Ubuntu 24.04 LTS |
| **VirtualBox** | 7.x |
| **Metasploitable** | Metasploitable2-Linux |
| **RAM** | 512 MB |
| **CPU** | 1 |
| **Disco** | Metasploitable.vmdk |
| **Red** | Host-Only |
| **Interfaz** | vboxnet0 |
| **IP Host** | 192.168.56.1 |
| **IP Metasploitable** | 192.168.56.101 |
| **Ping** | ☑ Exitoso ☐ Fallido |
| **Nmap** | ☑ Exitoso ☐ Fallido |



Evidencia1-VirtualBox
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/18e11e0cf210b0a842cf2858dec5ab3995dbfe6d/Evidencia%201.png)


> **¿Qué demuestra esta imagen?**  
> Muestra que la máquina virtual **Metasploitable 2** ya fue creada correctamente en VirtualBox con los recursos asignados (512 MB de RAM y 1 procesador CPU).


Evidencia 2-Configuración de red

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/9d490c05103df8ddbebbf8b4c2e790bd7fcfbbd6/Evidencia%202.png)

> **¿Qué demuestra esta imagen?**  
> Confirma que la tarjeta de red está configurada en modo **"Adaptador solo-anfitrión"** conectada a **vboxnet0**. Esto aísla a Metasploitable de Internet por seguridad.


Evidencia 3-VMDK

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/9d490c05103df8ddbebbf8b4c2e790bd7fcfbbd6/Evidencia3.png)

> **¿Qué demuestra esta imagen?**  
> Demuestra que la máquina virtual está conectada directamente al archivo de disco **Metasploitable.vmdk** original (sin haber creado un disco vacío por error).


Evidencia 4-IP

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/9d490c05103df8ddbebbf8b4c2e790bd7fcfbbd6/Evidencia%204.png)

> **¿Qué demuestra esta imagen?**  
> Muestra la ejecución del comando `ifconfig` dentro de Metasploitable para consultar su dirección IP privada (otorgada por el servidor DHCP de VirtualBox).


Evidencia 5-Comunicacion

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/9d490c05103df8ddbebbf8b4c2e790bd7fcfbbd6/Evidencia%205.png)

> **¿Qué demuestra esta imagen?**  
> Comprueba la conectividad enviando paquetes `ping` desde Ubuntu hacia la IP de Metasploitable. Si responde con 0% de pérdida, la red virtual está funcionando correctamente.


Evidencia 6-Nmap

![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/9d490c05103df8ddbebbf8b4c2e790bd7fcfbbd6/Evidencia%206.png)

> **¿Qué demuestra esta imagen?**  
> Muestra el escaneo con `nmap` realizado desde Ubuntu. Sirve para identificar qué puertos y servicios vulnerables (como FTP, SSH o HTTP) están abiertos en Metasploitable.



¿Qué diferencia existe entre una máquina virtual y el sistema anfitrión?

 El sistema anfitrión (Host) es el sistema operativo real de la PC (Ubuntu). La máquina virtual (VM) es un entorno de software simulado que funciona como una computadora independiente dentro del anfitrión (Metasploitable). 


 ¿Qué función cumple VirtualBox?

Se encarga de simular el hardware (RAM, CPU, discos) para ejecutar varios sistemas operativos al mismo tiempo. 


¿Qué es un archivo .vmdk?

Es el formato del disco duro virtual. Guarda todos los archivos, datos y el sistema operativo de la máquina virtual.

¿Por qué no necesitamos instalar Metasploitable desde una ISO?

Porque Metasploitable ya viene preinstalado dentro de su disco virtual .vmdk

¿Qué función cumple vboxnet0?

Es la interfaz de red virtual "Solo-Anfitrión" (Host-Only) creada por VirtualBox.

¿Qué significa 192.168.56.0/24?

Es la subred privada del laboratorio.

¿Qué función cumple DHCP?

Asigna direcciones IP de forma automática a los equipos de la red, evitando tener que configurarlas manualmente

¿Por qué Metasploitable no debe utilizar NAT?

 Para aislarla de internet y evitar riesgos de seguridad. 

 ¿Por qué no debemos utilizar Adaptador puente (Bridged)?

 Para evitar conectarla a la red física o Wi-Fi real, lo que pondría en riesgo a otros dispositivos de la red escolar o del hogar.

 ¿Qué información proporciona ifconfig?

 Muestra la configuración de las interfaces de red, como la dirección IP, la máscara de red y la dirección MAC

 ¿Qué función tiene ping?

Comprobar la conectividad de red entre dos equipos. Sirve para verificar si Ubuntu y Metasploitable pueden comunicarse.

¿Qué información básica proporciona nmap?

Escanea la red para mostrar los puertos abiertos, servicios activos y vulnerabilidades del equipo objetivo.

¿Por qué las pruebas realizadas en esta práctica están autorizadas?

Porque se realizan dentro de un entorno virtual controlado, aislado y privado con fines puramente académicos.

Qué riesgo existiría si Metasploitable se conectara a una red institucional?

Podría comprometer la seguridad de toda la red, ya que un atacante podría hackear Metasploitable fácilmente y usarla como puente para infectar otros equipos.


-----------------------------------------------------------------------------Parte2------------------------------------------------------------------------------------------


# 🕵️ Semana 04 — Investigación de seguridad: Usuarios, Grupos y Permisos

## 👤 Alumno
José Gerardo Cabrera Miranda

## 📅 Fecha
29 de septiembre de 2026

## 🖥 Sistema anfitrión
Ubuntu (Lenovo ThinkPad)[cite: 1, 17]

## 🧪 Máquina objetivo
Metasploitable 2[cite: 1, 17]

## 🌐 Red
Host-Only (vboxnet0)[cite: 1, 17]

## 📡 IP Ubuntu
192.168.56.1[cite: 1, 17]

## 🎯 IP Metasploitable
192.168.56.101[cite: 1, 2, 17]

---

## 🔎 Servicios encontrados (`nmap`)
Durante el escaneo de puertos se identificaron múltiples servicios expuestos en el objetivo, destacando:
* **21/tcp (ftp):** Protocolo de transferencia de archivos[cite: 1, 3, 17].
* **22/tcp (ssh):** Servicio de administración remota cifrada[cite: 1, 3, 17].
* **23/tcp (telnet):** Protocolo de administración remota en texto plano (inseguro)[cite: 1, 3, 17].
* **80/tcp (http):** Servidor web Apache[cite: 1, 3, 17].
* **3306/tcp (mysql):** Base de datos MySQL[cite: 1, 3, 17].

---

## 🔐 Usuario utilizado
* **Usuario:** `msfadmin`[cite: 1, 17]
* **Contraseña:** `msfadmin`[cite: 1, 17]
* **UID:** `1000` | **GID:** `1000`[cite: 1, 12, 17]

---

## 👥 Grupos identificados
1. `msfadmin` (GID 1000): Grupo primario del usuario de laboratorio[cite: 1, 12, 17].
2. `adm` (GID 4): Grupo con permisos para consultar archivos de registros (*logs*) del sistema[cite: 1, 12, 17].
3. `sudo` / `admin`: Permite la ejecución de comandos con privilegios elevados (`root`)[cite: 1, 12, 17].

---

## 🔒 Análisis de permisos
* **`/etc/passwd` (`-rw-r--r--`):** Legible por todos los usuarios para resolución de nombres e IDs, pero solo modificable por `root`[cite: 1, 9, 11, 17].
* **`/etc/shadow` (`-rw-r-----`):** Altamente restringido; contiene los hashes cifrados de las contraseñas del sistema y solo es accesible por `root` o el grupo `shadow`[cite: 1, 8, 17].
* **Archivos SUID:** Se identificaron ejecutables con el bit de permiso `4000`, lo que les permite ejecutarse con privilegios del propietario (`root`)[cite: 1, 7, 17].

---

## 🚨 Hallazgos de seguridad
1. **Servicios inseguros activos:** Presencia de Telnet (puerto 23) transmitiendo datos en texto claro[cite: 1, 3, 17].
2. **Credenciales débiles y por defecto:** Uso del par `msfadmin:msfadmin` con privilegios sudo[cite: 1, 17].
3. **Algoritmos SSH obsoletos:** El servicio SSH requiere negociación explícita de llaves antiguas (`ssh-rsa`, `diffie-hellman-group1-sha1`)[cite: 1, 3, 13, 17].
4. **Superficie de ataque amplia:** Múltiples puertos innecesarios expuestos hacia la red interna[cite: 1, 3, 17].

---

## 🛡️ Medidas de protección recomendadas
1. **Deshabilitar Telnet:** Reemplazar totalmente su uso por SSH[cite: 1, 17].
2. **Endurecimiento de SSH:** Actualizar la versión de SSH y deshabilitar algoritmos de cifrado obsoletos y débiles[cite: 1, 3, 13, 17].
3. **Gestión de contraseñas:** Cambiar contraseñas por defecto y aplicar políticas de complejidad[cite: 1, 17].
4. **Principio de Mínimo Privilegio:** Ajustar permisos de archivos sensibles y auditar ejecutables SUID innecesarios[cite: 1, 7, 17].
5. **Segmentación y Firewall:** Filtrar puertos no requeridos mediante `ufw` o `iptables`[cite: 1, 17].

---

## 🧾 Registro de Comandos

| Comando | ¿Qué hace? | ¿Qué observé? |
|---|---|---|
| `ip addr` | Muestra las interfaces de red y sus direcciones IP[cite: 1, 17]. | Se localizó la interfaz interna `vboxnet0` con la IP `192.168.56.1`[cite: 1, 17]. |
| `nmap -sn` | Realiza un descubrimiento rápido de equipos encendidos en la red sin escanear puertos[cite: 1, 17]. | Se identificó que la máquina virtual Metasploitable respondía en la IP `192.168.56.101`[cite: 1, 2, 17]. |
| `ping` | Envía paquetes de prueba (*ICMP*) para verificar comunicación con otro host[cite: 1, 17]. | El servidor respondió de forma continua y sin pérdida de datos, confirmando conectividad[cite: 1, 17]. |
| `nmap` | Escanea los puertos y servicios activos de una dirección IP[cite: 1, 3, 17]. | Se descubrieron múltiples puertos abiertos como SSH (22), FTP (21), Telnet (23), HTTP (80) y MySQL (3306)[cite: 1, 3, 17]. |
| `ssh` | Establece una sesión de terminal remota cifrada de forma segura[cite: 1, 13, 17]. | Se logró entrar al servidor utilizando parámetros de compatibilidad para claves antiguas[cite: 1, 13, 17]. |
| `whoami` | Muestra el nombre de usuario de la sesión actual[cite: 1, 12, 17]. | Confirmó que estábamos conectados bajo el usuario predeterminado `msfadmin`[cite: 1, 12, 17]. |
| `id` | Muestra los identificadores numéricos de usuario (UID) y de grupo (GID)[cite: 1, 12, 17]. | Arrojó `uid=1000` y `gid=1000`, indicando un usuario sin privilegios de administración directos[cite: 1, 12, 17]. |
| `groups` | Lista todos los grupos a los que pertenece el usuario activo[cite: 1, 12, 17]. | Muestra los grupos secundarios asignados (ej. `adm`, `sudo`, `audio`)[cite: 1, 12, 17]. |
| `ls -l` | Lista los archivos detallando sus permisos, propietario y tamaño[cite: 1, 9, 17]. | Permitió visualizar los permisos en formato de letras (ej. `-rw-r--r--`)[cite: 1, 9, 17]. |
| `chmod` | Modifica los permisos de lectura, escritura y ejecución de un archivo o carpeta[cite: 1, 5, 17]. | Se aplicó `600` para restringir el acceso exclusivo al archivo de laboratorio[cite: 1, 5, 17]. |
| `chgrp` | Cambia el grupo propietario de un archivo o directorio[cite: 1, 17]. | Se utilizó para asociar recursos de prueba a grupos específicos de trabajo[cite: 1, 17]. |
| `find -perm -4000` | Busca archivos del sistema que tengan el permiso especial SUID activado[cite: 1, 7, 17]. | Desplegó los binarios que pueden ejecutarse temporalmente con privilegios de `root`[cite: 1, 7, 17]. |

---

## 📸 Índice de Evidencias (Capturas)
* `Evidencia 1
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%201p2.png

  
* Evidencia 2
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%202p2.png

* Evidencia 3
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%203p2.png

* Evidencia 4
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%204p2.png

* Evidencia 5
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%205p2.png

* Evidencia 6
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia6p2.png

* Evidencia 7
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%207p2.png

* Evidencia 8
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%208p2.png

* Evidencia 9
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%209p2.png

* Evidencia 10
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%2010p2%20.png

* Evidencia 11
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%2011p2.png

* Evidencia 12
* ![Image alt]https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bc76ffa846e8c495a225237dfef224d9d2bee03c/Evidencia%2012p2%20.png

# 🕵️ Informe de Incidente y Auditoría de Seguridad

## 1️⃣ ¿El servidor estaba expuesto?
**Sí.** Al realizar el escaneo de puertos con `nmap`, encontramos múltiples servicios activos y expuestos en la red, tales como FTP (puerto 21), SSH (puerto 22), Telnet (puerto 23), servidor web HTTP (puerto 80) y bases de datos MySQL (puerto 3306)[cite: 1, 3, 17]. Esto significa que cualquier equipo en la red interna podía intentar comunicarse con ellos[cite: 1, 17].

## 2️⃣ ¿Existía una cuenta conocida?
**Sí.** Se utilizó el usuario por defecto del laboratorio que viene configurado en Metasploitable con credenciales débiles e inseguras (`msfadmin / msfadmin`)[cite: 1, 17].

## 3️⃣ ¿Qué usuario obtuviste?
Al ingresar al sistema y ejecutar los comandos de identidad, obtuvimos:
* `whoami`: `msfadmin`[cite: 1, 12, 17]
* `id`: `uid=1000(msfadmin) gid=1000(msfadmin)...`[cite: 1, 12, 17]
* `groups`: Pertenencia a varios grupos locales del sistema como `adm`, `sudo`, `audio`, etc[cite: 1, 12, 17].

## 4️⃣ ¿Qué grupos existen?
Mencionando tres grupos importantes encontrados:
1. **`root`**: Grupo del súper usuario con control total del sistema[cite: 1, 17].
2. **`sudo`**: Permite ejecutar comandos administrativos utilizando privilegios elevados[cite: 1, 12, 17].
3. **`adm`**: Permite consultar los archivos de registro (*logs*) del sistema operativo[cite: 1, 12, 17].

## 5️⃣ ¿Qué permisos encontraste?
Con el comando `ls -l` observamos la estructura de permisos en formato de letras (ejemplo: `-rwxr-x---`), donde se divide en tres partes: lo que puede hacer el **Propietario**, lo que puede hacer el **Grupo**, y lo que pueden hacer los **Otros** (cualquier otro usuario) usando lectura (`r`), escritura (`w`) y ejecución (`x`)[cite: 1, 17].

## 6️⃣ ¿Qué archivos son especialmente sensibles?
* **`/etc/passwd`**: Contiene la lista de usuarios del sistema[cite: 10, 11, 17]. Es legible por todos (`-rw-r--r--`) porque el sistema operativo necesita que se puedan consultar los nombres y UIDs[cite: 1, 9, 17].
* **`/etc/shadow`**: Contiene las contraseñas cifradas (*hashes*)[cite: 8, 17]. Sus permisos son estrictos (`-rw-r-----`) y solo los puede leer el usuario `root` para evitar que cualquiera intente descifrar las claves[cite: 1, 8, 17].

## 7️⃣ ¿Qué significa SUID?
Es un permiso especial (*Set User ID*) en archivos ejecutables[cite: 7, 17]. Significa que cuando un usuario común ejecuta ese programa, el sistema lo hace temporalmente con los privilegios del **dueño del archivo** (usualmente `root`)[cite: 1, 7, 17]. Debe auditarse porque si un programa con SUID tiene fallas de seguridad, un intruso podría escalar privilegios y volverse administrador[cite: 1, 17].

## 8️⃣ ¿Qué configuración de permisos consideras peligrosa?
Cualquier archivo o carpeta con permisos **`777`** (lectura, escritura y ejecución para todo el mundo)[cite: 1, 17]. Esto es peligroso porque cualquier persona o programa malicioso puede modificar, borrar o inyectar código sin restricciones[cite: 1, 17].

## 9️⃣ ¿Cómo reducirías el riesgo?
1. Deshabilitar servicios inseguros obsoletos (como Telnet)[cite: 1, 3, 17].
2. Cambiar todas las contraseñas por defecto y débiles[cite: 1, 17].
3. Aplicar el principio de mínimo privilegio (quitar permisos y grupos innecesarios a los usuarios)[cite: 1, 17].
4. Restringir el uso masivo de permisos abiertos y auditar archivos SUID[cite: 1, 7, 17].
5. Implementar reglas de firewall (*iptables / ufw*) para bloquear accesos no autorizados[cite: 1, 17].

---

## Tabla de Hallazgos y Acciones (Defensor)

| Hallazgo | Riesgo | Acción recomendada | Prioridad |
|---|---|---|---|
| Puerto 23 abierto (Telnet) | Transmite contraseñas y datos en texto plano por la red | Deshabilitar el servicio Telnet y usar exclusivamente SSH[cite: 1, 3, 17]. | Alta |
| Contraseña débil por defecto (`msfadmin`) | Acceso inmediato no autorizado por fuerza bruta o credenciales conocidas | Cambiar inmediatamente la contraseña por una compleja[cite: 1, 17]. | Alta |
| Permisos demasiado amplios en directorios clave | Modificación o eliminación de archivos de configuración por usuarios no autorizados | Auditar y corregir permisos usando `chmod` y `chown`[cite: 1, 5, 17]. | Media |
| Binarios SUID innecesarios o mal configurados | Escalación de privilegios hacia `root` | Revisar la lista de archivos SUID y remover el bit si no es indispensable[cite: 1, 7, 17]. | Alta |
| Múltiples servicios antiguos activos | Mayor superficie de ataque ante vulnerabilidades conocidas | Apagar todos los servicios que no se utilicen en la aplicación interna[cite: 1, 3, 17]. | Media |
