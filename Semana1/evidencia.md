![](Pictures/10000001000002D6000001D2152F71E0.png){width="18.572cm"
height="11.92cm"}

# Semana 01 --- Diagnóstico del Almacenamiento en Ubuntu

## 🎯 Objetivo

Aprender a realizar un diagnóstico del almacenamiento de un sistema
operativo Linux (Ubuntu) utilizando la terminal de comandos. El
propósito principal no es memorizar la sintaxis de los comandos, sino
interpretar los datos presentados por el kernel, comprender cómo se
organizan los dispositivos de bloques, sus particiones y sistemas de
archivos, y documentar los hallazgos de forma clara.

# 🧠 Investigación --- Diagnóstico del Almacenamiento

## 1. Conceptos de Almacenamiento y Hardware

### ¿Qué es un HDD?

Un **HDD (Hard Disk Drive)** o disco duro mecánico es un dispositivo de
almacenamiento magnético no volátil. Utiliza platos metálicos o de
cristal que giran a altas velocidades (por ejemplo, 5400 o 7200 RPM) y
cabezales magnéticos para leer y escribir datos. Su funcionamiento
mecánico lo hace más propenso a desgaste físico, sensibilidad a golpes y
ofrece velocidades de lectura/escritura considerablemente más lentas que
los medios de estado sólido.

### ¿Qué es un SSD?

Un **SSD (Solid State Drive)** o unidad de estado sólido es un
dispositivo de almacenamiento de datos que utiliza memoria flash (NAND)
sin partes móviles mecánicas. Al eliminar componentes en movimiento,
ofrece tiempos de acceso casi instantáneos, mayor resistencia a impactos
físicos, menor consumo de energía y velocidades de transferencia
significativamente superiores a las de un HDD.

### ¿Qué es un NVMe?

**NVMe (Non-Volatile Memory Express)** es un protocolo de transporte e
interfaz de comunicaciones diseñado específicamente para acceder a
medios de almacenamiento no volátiles de alta velocidad conectados a
través del bus **PCI Express (PCIe)**. A diferencia de las SSDs
tradicionales que operan sobre la interfaz SATA (limitada a protocolos
antiguos como AHCI), NVMe permite un procesamiento en paralelo masivo y
reduce drásticamente la latencia.

### ¿Qué diferencia existe entre un disco y una partición?

- **Disco:** Es la unidad física de almacenamiento (hardware)
  identificada por el sistema operativo como un único bloque físico (por
  ejemplo, */dev/nvme0n1* o */dev/sda*).
- **Partición:** Es una división lógica dentro de un disco físico. Cada
  partición se delimita en la tabla de particiones del disco y el
  sistema operativo la gestiona como si fuera una unidad independiente.

## 2. Sistemas de Archivos y Esquemas de Particionado

### ¿Qué es un sistema de archivos?

Un **sistema de archivos** es la estructura subyacente que utiliza un
sistema operativo para organizar, nombrar, almacenar, recuperar y
administrar archivos en un dispositivo de almacenamiento o partición.
Define cómo se escriben los datos en el medio físico y cómo se gestionan
sus metadatos (fechas de creación, permisos, nombres, ubicaciones).

### ¿Qué es NTFS?

**NTFS (New Technology File System)** es un sistema de archivos
propietario desarrollado por Microsoft, utilizado por defecto en
sistemas operativos Windows. Admite características avanzadas como
listas de control de acceso (ACL) para permisos, registro de
transacciones (journaling), cifrado nativo, compresión e identificadores
de archivos grandes.

### ¿Qué es ext4?

**ext4 (Fourth Extended Filesystem)** es el sistema de archivos por
defecto en la mayoría de las distribuciones de GNU/Linux. Es un sistema
transaccional (*journaling*) muy estable y eficiente, diseñado para
soportar volúmenes y archivos de gran tamaño, reduciendo la
fragmentación de archivos de manera nativa mediante técnicas como
asignación diferida (*delayed allocation*) y *extents*.

### ¿Qué es UEFI?

**UEFI (Unified Extensible Firmware Interface)** es la especificación de
firmware moderna que reemplazó a la antigua BIOS (*Basic Input/Output
System*). Actúa como la interfaz primaria entre el firmware de la placa
base y el sistema operativo. Proporciona ventajas como tiempos de
arranque más rápidos, soporte para discos de gran capacidad, un entorno
gráfico previo al arranque y soporte para características de seguridad
como *Secure Boot*.

### ¿Qué es GPT?

**GPT (GUID Partition Table)** es el estándar moderno para definir
esquemas de tablas de particiones en discos duros, asociado al estándar
UEFI. GPT utiliza identificadores únicos universales (GUID) para
referenciar particiones y permite un límite teórico de hasta 128
particiones primarias por defecto, además de direccionar discos con
capacidad superior a 2 TB (hasta 9.4 ZB). Cuenta con copias de respaldo
de la tabla de particiones al final del disco para redundancia.

### ¿Qué es MBR?

**MBR (Master Boot Record)** es el esquema de particionado tradicional
utilizado históricamente con BIOS. Se almacena en el primer sector de un
disco (sector 0) e incluye el código de arranque inicial del sistema.
Sus limitaciones principales son el soporte de un máximo de 4
particiones primarias (o 3 primarias y 1 extendida) y un límite máximo
de tamaño direccionable de 2 TB por disco.

## 3. Entorno de Terminal y Shell en Linux

### ¿Qué es una terminal?

Una **terminal** (o emulador de terminal) es un programa de interfaz
gráfica o de texto que proporciona una línea de comandos (CLI) para
interactuar directamente con la capa del sistema operativo mediante el
ingreso de instrucciones escritas.

### ¿Qué es Bash?

**Bash (Bourne Again SHell)** es el intérprete de comandos y lenguaje de
scripting predeterminado en Ubuntu y la mayoría de las distribuciones
Linux. Es el programa encargado de leer, interpretar y ejecutar los
comandos ingresados por el usuario en la terminal.

### ¿Qué significa ejecutar un comando?

Ejecutar un comando significa indicarle a la consola o shell (Bash) que
busque una utilidad del sistema, binario ejecutable o función interna,
cargue el programa en la memoria RAM y procese las instrucciones
indicadas junto con sus argumentos o banderas opcionales.

### ¿Qué es la salida estándar?

La **salida estándar (*****stdout*****)** es el flujo de datos
predeterminado hacia donde un programa o comando envía su texto o
información procesada de resultado. Por omisión en un sistema Linux, el
destino de la salida estándar es la pantalla del emulador de terminal.

### ¿Qué significa utilizar *sudo*?

El comando ***sudo*** **(Superuser Do)** es una utilidad que permite a
usuarios autorizados ejecutar programas con privilegios de seguridad
elevados, generalmente con los permisos del usuario administrador
supremo del sistema (***root***). Se requiere para consultar detalles de
hardware de bajo nivel o realizar cambios administrativos en el sistema.

# 

# 💽 Diagnóstico del Almacenamiento

## 🐧 Identificación del Sistema

Para consultar la información básica del entorno antes de iniciar el
diagnóstico, se ejecutaron los siguientes comandos:

  ------------------------ ---------------- ------------------ ------------------------------------------------------------------------------------------------------------
  Distribución / Versión   lsb_release -a   Ubuntu 24.04 LTS   Permite saber la rama de paquetes, el periodo de soporte del sistema y la compatibilidad con repositorios.
  Arquitectura             uname -m         x86_64             Identifica que el procesador es de 64 bits para la correcta elección de software y controladores.
  Usuario actual           whoami           gerardocm          Confirma qué nivel de contexto y privilegios se tienen antes de intentar modificar el sistema.
  ------------------------ ---------------- ------------------ ------------------------------------------------------------------------------------------------------------

![](Pictures/1000000100000229000000C3EC784B4D.png){width="14.631cm"
height="5.159cm"}

Esto demuestra la distribución de Ubuntu (24.04 LTS), la arquitectura
(*x86_64*) y tu usuario (*gerardocm*).

## 

##  💽 Estructura Física y Lógica (*lsblk*)

Al ejecutar el comando *lsblk* en la terminal, el kernel reportó la
siguiente estructura jerárquica de dispositivos en bloque:

NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS\
nvme0n1 259:0 0 476,9G 0 disk\
├─nvme0n1p1 259:1 0 391,2G 0 part\
├─nvme0n1p2 259:2 0 521M 0 part\
├─nvme0n1p3 259:3 0 84,1G 0 part /\
└─nvme0n1p4 259:4 0 1G 0 part /boot/efi

Aquí tienes el contenido completo estructurado para tu archivo
**diagnostico.md**.

<div>

He incluido los datos reales extraídos de tus capturas de pantalla de la
terminal (gerardocm@Gerardothinkpad, disco NVMe de 476,9 GB, particiones
p1 a p4, etc.) para que tu reporte sea exacto y personalizado.

Markdown

### 🛑 Análisis de la salida de lsblk

- **Dispositivo principal:** nvme0n1 es un disco de estado sólido con
  protocolo **NVMe** de **476,9 GB** de capacidad total.

- **Partición 1 (****nvme0n1p1****):** Tiene un tamaño de **391,2 GB**.
  No presenta punto de montaje explícito en Linux, correspondiendo a la
  partición principal de Windows en configuración *Dual Boot*.

- **Partición 2 (****nvme0n1p2****):** Tiene un tamaño de **521 MB**. Es
  una partición reservada o de recuperación del sistema.

- **Partición 3 (****nvme0n1p3****):** Tiene un tamaño de **84,1 GB** y
  está montada en la raíz (/). Es el contenedor principal del sistema
  operativo Ubuntu y archivos del usuario.

- **Partición 4 (****nvme0n1p4****):** Tiene un tamaño de **1 GB** y
  está montada en /boot/efi. Corresponde a la partición de sistema EFI
  (ESP).

- **Dispositivos** **loop0** **a** **loop26****:** Son unidades
  virtuales de solo lectura creadas por el demonio de paquetes **Snap**
  para aislar aplicaciones ejecutables (squashfs).

- ![](Pictures/100000010000030D000002A3814A875B.png){width="14cm"
  height="11.464cm"}***lsblk***: Muestra una vista todos los
  dispositivos de discos y particiones, sus tamaños y sus puntos de
  montaje.

## 

## 

## 3. 🗂️ Sistemas de Archivos y Uso (lsblk -f)

Al agregar la bandera -f (lsblk -f), se obtuvieron los detalles de los
sistemas de archivos, identificadores UUID y espacio disponible:

  ----------- ------ ------- -- -------------------------------------- ------- ----- -------------------------
  nvme0n1p1   ntfs              01DAEF65290ACD00                       \-      \-    (Sin montar / Windows)
  nvme0n1p2   ntfs              01DAEF6534694320                       \-      \-    (Sin montar / Recovery)
  nvme0n1p3   ext4   1.0        9dab5a92-234c-4281-8662-58fca6742839   35,8G   51%   /
  nvme0n1p4   vfat   FAT32      51E0-3534                              1G      1%    /boot/efi
  ----------- ------ ------- -- -------------------------------------- ------- ----- -------------------------

### Explicación de las columnas de lsblk -f para el administrador:

- **FSTYPE****:** Indica cómo están formateados los datos. Permite saber
  si el sistema puede escribir directamente (ext4), si requiere
  controladores NTFS o si es para arranque UEFI (vfat).

- **UUID****:** Universally Unique Identifier. Es el identificador único
  de 128 bits que garantiza montar el dispositivo correcto en /etc/fstab
  independientemente de si el nombre del dispositivo cambia en el
  arranque.

- **FSAVAIL** **y** **FSUSE%****:** Muestra el espacio libre exacto y el
  porcentaje ocupado. Sirve para prevención de fallos por almacenamiento
  lleno.

- **MOUNTPOINT****:** Es el directorio en el árbol raíz donde los
  archivos de esa partición se vuelven accesibles para el usuario y las
  aplicaciones.

![](Pictures/1000000100000513000002E047C0A2C7.png){width="17cm"
height="9.631cm"}

En esta captura de pantalla, la salida de ***lsblk -f*** podemos
observar el detalle de los sistemas de archivos, identificadores y uso
del espacio:

**Sistemas de Archivos en las Particiones (*****nvme0n1*****)**

- ***nvme0n1p1*****:** Formato ***ntfs*** (UUID: *01DAEF65290ACD00*). Es
  la partición principal de Windows. No está montada actualmente en
  Linux.
- ***nvme0n1p2*****:** Formato ***ntfs*** (UUID: *01DAEF6534694320*).
  Partición secundaria/recuperación de Windows.
- ***nvme0n1p3*****:** Formato ***ext4*** (versión 1.0, UUID:
  *9dab5a92\...*). Es la partición raíz (*/*) de Ubuntu. Tiene **35,8 GB
  disponibles** (*FSAVAIL*) y un uso del **51%** (*FSUSE%*).
- ***nvme0n1p4*****:** Formato ***vfat*** / **FAT32** (UUID:
  *51E0-3534*). Es la partición de arranque UEFI (*/boot/efi*). Tiene
  **1 GB libre** y un uso del **1%**.

**Dispositivos Loop (*****loop0*** **a** ***loop26*****)**

- Todos utilizan el sistema de archivos de solo lectura ***squashfs***
  (versión 4.0).
- Tienen **0 bytes disponibles** (*FSAVAIL = 0*) y están al **100% de
  uso** (*FSUSE% = 100%*), lo cual es completamente normal porque los
  paquetes Snap son imágenes comprimidas de solo lectura.

## 4. 🗂️ Sistemas de Archivos Identificados en el Equipo

1.  **ext4** **(****nvme0n1p3****):**

    - **Uso:** Partición raíz (/) de Linux.

    - **Función:** Sistema de archivos con transacciones (*journaling*)
      propio de Linux que gestiona permisos POSIX, usuarios e integridad
      de programas.

2.  **ntfs** **(****nvme0n1p1** **y** **p2****):**

    - **Uso:** Partición primaria y de recuperación de Microsoft
      Windows.

    - **Función:** Permite a Windows gestionar permisos de archivos,
      compresión y cifrado BitLocker.

3.  **vfat** **/ FAT32 (****nvme0n1p4****):**

    - **Uso:** Partición de arranque EFI (/boot/efi).

    - **Función:** Es un formato estándar simple requerido por el
      firmware UEFI de la placa base para cargar los ejecutables de
      arranque (.efi) antes de iniciar el kernel de Linux o el gestor de
      Windows.

### ❓ Pregunta de análisis: ¿Por qué un mismo equipo puede tener más de un sistema de archivos?

Porque cada componente del hardware y software tiene requerimientos
técnicos distintos. El firmware UEFI de la computadora exige una
partición simple y universal como FAT32 para leer los cargadores de
arranque; Linux opera de forma óptima y segura con soporte de permisos
POSIX usando ext4; y Windows requiere NTFS para sus propias
características de seguridad y funcionamiento interno.

## 5. 🔎 Herramientas Complementarias de Diagnóstico

- **sudo fdisk -l****:** Muestra la estructura de sectores físicos de
  los discos y confirma si la tabla de particiones es **GPT** o **MBR**,
  además del tipo de ID de partición.

  ![](Pictures/1000000100000368000002A50D316543.png){width="15.161cm"
  height="11.769cm"}

- **sudo parted -l****:** Ofrece un resumen del tipo de particionado y
  banderas (*flags*) especiales asociadas a las particiones (como boot o
  esp).

  ![](Pictures/1000000100000227000000DE2E8F88EB.png){width="14.579cm"
  height="5.874cm"}

- **sudo blkid****:** Imprime en una sola lista los pares DEVNAME, UUID
  y TYPE de todas las unidades de bloque presentes, ideal para consultar
  identidades antes de hacer montajes manuales.

</div>

![](Pictures/10000001000003B50000025DEEE856E5.png){width="17cm"
height="10.837cm"}

## 🐧 Entorno

- **Distribución:** Ubuntu 24.04 LTS
- **Arquitectura:** *x86_64* (64-bit)
- **Usuario actual:** *gerardocm*
- **Nombre del host:** *Gerardothinkpad*

## 

## 💽 Diagnóstico del Almacenamiento

Mediante el uso de herramientas de línea de comandos se identificó un
único dispositivo de almacenamiento físico basado en tecnología NVMe:

- **Dispositivo principal:** */dev/nvme0n1*
- **Capacidad total:** 476,9 GB (equivalente a 512 GB comerciales)
- **Tipo de dispositivo:** Unidad de estado sólido NVMe (Non-Volatile
  Memory Express)

## 

##                           Particiones

El disco principal se encuentra dividido en **4 particiones lógicas**:

1.  ***nvme0n1p1*** **(391,2 GB):** Partición principal con sistema de
    archivos NTFS donde reside la instalación de Microsoft Windows
    (configuración Dual-Boot).
2.  ***nvme0n1p2*** **(521 MB):** Partición reservada / recuperación del
    sistema Windows.
3.  ***nvme0n1p3*** **(84,1 GB):** Partición principal de Linux montada
    en la raíz del sistema (*/*).
4.  ***nvme0n1p4*** **(1 GB):** Partición de Sistema EFI (ESP) montada
    en */boot/efi*.

## 

**Sudo fdisk -l**: Muestra la tabla de particiones completa a bajo
nivel, incluyendo el sector exacto donde inicia y termina cada
partición, el tipo de tabla (GPT o MBR) y el tipo de partición (Linux
filesystem, EFI System, Microsoft basic data, etc.).

![](Pictures/1000000100000513000002E0AA93DB51.png){width="18.124cm"
height="10.268cm"}

## 

## 

## 

## 🗂️ Sistemas de Archivos

Al ejecutar *lsblk -f* se identificaron los siguientes formatos y su
ocupación de espacio:

- ***ext4*** **(en** ***nvme0n1p3*****):** Sistema de archivos
  transaccional (*journaling*) propio de Linux. Dispone de **35,8 GB
  libres** de sus 84,1 GB totales, representando un **51% de uso**.
- ***vfat*** **/ FAT32 (en** ***nvme0n1p4*****):** Formato universal
  utilizado para la partición EFI. Utiliza **1% de su capacidad** (menos
  de 20 MB usados) y cuenta con **1 GB libre**.
- ***ntfs*** **(en** ***nvme0n1p1*** **y** ***p2*****):** Sistema de
  archivos de Windows. No se encuentra montado activamente en el entorno
  de Linux.

## 🔎 Herramientas Utilizadas

  ---------- ------------------------ ------------------------------------------------------------------------------- ----------------------------------------------------------------------------------
  lsblk      Dispositivos en bloque   Lista en árbol de discos, particiones, tamaños y puntos de montaje              Mapear rápidamente la estructura física del almacenamiento.
  lsblk -f   Sistemas de archivos     Tipos de formato (*FSTYPE*), UUID, espacio libre (*FSAVAIL*) y uso (*FSUSE%*)   Mapear identificadores únicos para montaje en */etc/fstab* y supervisar espacio.
  fdisk -l   Tablas de particionado   Esquema de particiones (GPT), sectores de inicio y fin, tipos de partición      Analizar la estructura de discos a bajo nivel y verificar compatibilidades.
  blkid      Atributos de bloques     Etiquetas, UUIDs y tipos de formatos sin jerarquía de árbol                     Obtener rápidamente el UUID exacto de un volumen sin contexto visual extra.
  ---------- ------------------------ ------------------------------------------------------------------------------- ----------------------------------------------------------------------------------

## 

## 🥾 EFI / UEFI

Se identificó la presencia de la partición */dev/nvme0n1p4* en formato
*FAT32* montada bajo la ruta */boot/efi*. Su función es contener los
ejecutables e imágenes de arranque (*.efi*) que el firmware UEFI de la
placa base consulta al encender el equipo para iniciar el cargador de
arranque (GRUB) o el gestor de Windows.

## 🔄 GPT / MBR

El disco */dev/nvme0n1* utiliza el esquema de particionado **GPT (GUID
Partition Table)**. Esto permite sobrepasar el límite histórico de 4
particiones primarias de MBR, ofrecer redundancia mediante copias de
seguridad de la tabla de particiones al final del disco y operar
nativamente con el firmware UEFI.

## 🔐 BitLocker

Debido a que el equipo cuenta con una partición de Windows
(*nvme0n1p1*), es fundamental tomar precauciones si BitLocker se
encuentra habilitado. Tratar una partición cifrada desde Linux como si
fuera un volumen normal o intentar modificar sus sectores puede provocar
la pérdida irrecoverable de la clave de acceso o la corrupción completa
de los datos.

## 🗺️ Mapa del Almacenamiento

![](Pictures/10000000000005800000030096DF2E96.jpg){width="19.482cm"
height="10.626cm"}

*sudo parted -l:Indica claramente si el disco usa **GPT** o **MBR** (en
la línea *Partition Table*) y muestra las banderas (*flags*) activas en
cada partición (como boot o esp)*

![](Pictures/1000000100000513000002E07CF7F6AD.png){width="17cm"
height="9.631cm"}

*cat /proc/partitions: Muestra el listado crudo de todas las particiones
que el Kernel de Linux ha detectado en el hardware, indicando el número
de bloques y el nombre del dispositivo.*

![](Pictures/10000001000001A0000002B1838406FF.png){width="11.007cm"
height="17.657cm"}
