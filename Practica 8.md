Aquí tienes el contenido completo para el archivo `README.md` de la **Práctica 08**, actualizado con la tabla de inventario de almacenamiento, las preguntas de análisis respondidas y la nota técnica sobre el parámetro SSH utilizado para solventar la compatibilidad con Metasploitable 2:

---

# 🔵 Semana 08 — Sistemas de archivos y laboratorio

## Datos del alumno

* Nombre: José Gerardo Cabrera Miranda
* Grupo: 3° Semestre - Ingeniería en Sistemas Computacionales
* Fecha: 2026-10-23

## Entorno

* Distribución y versión de Ubuntu: Ubuntu 24.04 LTS
* Tipo de máquina: Equipo Físico / Máquina Virtual de análisis


* Tipo de red virtual: Host-only (Aislada)


* IP confirmada de Metasploitable: `192.168.56.101` (Verificada en laboratorio)



## Objetivo

Identificar dispositivos, sistemas de archivos, espacio ocupado y puntos de montaje en Ubuntu, relacionándolo con una inspección informativa no destructiva y de solo lectura en el entorno de Metasploitable.

## 📊 Inventario de Almacenamiento

| Comando | Qué consulta | Hallazgo real |
| --- | --- | --- |
| `lsblk -f` | Dispositivos de bloques y UUID

 | Muestra la estructura de particiones, tipos de formatos y identificadores únicos. |
| `df -h` | Espacio disponible en sistemas montados

 | Detalla el espacio total, usado, disponible y porcentaje de ocupación de las particiones. |
| `du -sh` | Tamaño de directorios específicos

 | Cuantifica de forma exacta el peso y almacenamiento consumido por una ruta concreta. |
| `findmnt` | Sistemas de archivos montados activamente

 | Lista los puntos de montaje actuales y su relación jerárquica con el árbol de directorios. |
| `cat /etc/fstab` | Configuración de montajes estáticos

 | Expone las reglas del sistema para montar particiones automáticamente al iniciar. |

## 📝 Preguntas de Análisis e Interpretación

1. **¿Qué diferencia existe entre un disco y una partición?**
El disco es el medio físico o virtual completo de almacenamiento, mientras que la partición es una sección lógica delimitada dentro de ese mismo disco.
2. **¿Qué es un sistema de archivos y un punto de montaje?**
El sistema de archivos es la estructura lógica que organiza cómo se guardan y leen los datos; el punto de montaje es el directorio del sistema desde el cual se accede a ese contenido estructurado.


3. **¿Por qué `df` y `du` pueden mostrar cantidades distintas?**
Porque `df` mide el espacio global ocupado a nivel de bloques del sistema de archivos montado, mientras que `du` calcula de manera recursiva el tamaño de los archivos individuales dentro de una ruta específica.


4. **¿Para qué sirve el archivo `/etc/fstab`?**
Para configurar de forma persistente qué particiones o dispositivos deben montarse automáticamente y bajo qué parámetros al arrancar el sistema operativo.


5. **¿Qué diferencia hay entre un puerto expuesto y un acceso autenticado en Metasploitable?**
Un puerto expuesto solo indica que hay un servicio escuchando en la red (observado mediante Nmap), pero no otorga ningún privilegio; el acceso autenticado requiere credenciales válidas para interactuar legítimamente con el sistema.



## 🔐 Nota Técnica sobre la Conexión SSH a Metasploitable 2

Debido a que Ubuntu 24.04 cuenta con políticas de seguridad y algoritmos criptográficos modernos, al intentar conectarse de forma predeterminada a Metasploitable 2 (un entorno obsoleto que ofrece llaves de tipo `ssh-rsa` o `ssh-dss`), el sistema rechazaba la negociación. Para permitir el acceso informativo de solo lectura requerido en la práctica, se implementó el siguiente comando explícito para forzar la compatibilidad de llaves:

```bash
ssh -o HostKeyAlgorithms=+ssh-rsa -o PubkeyAcceptedKeyTypes=+ssh-rsa msfadmin@192.168.56.101

```

## 📸 Registro de Evidencias

Las capturas de pantalla de esta práctica se ubican en el directorio `evidencias/`:

* `evidencias/01_lsblk_df.png`: Dispositivos, particiones y espacio disponible (`lsblk`, `df -h`).
* ![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3d2a5a3324fe1448bfd022211a9471757be01924/Captura%208-1png)
* ![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3d2a5a3324fe1448bfd022211a9471757be01924/Captura%208-1..png)


* `evidencias/02_du_findmnt.png`: Uso de directorios y sistemas montados (`du`, `findmnt`).
* ![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3e3b0fee8f128fd5eb767493bd011d851a9cc48b/Captura%208-2.png)
* ![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/3e3b0fee8f128fd5eb767493bd011d851a9cc48b/Captura%208-2..png)


* `evidencias/03_fstab_lectura.png`: Lectura de la configuración de montajes (`cat /etc/fstab`).
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/1460eafdf7b3990bb8500a5526ac0d8629c5156e/Captura%208-3.png)

* `evidencias/04_consultas_objetivo_o_analisis.png`: Consultas informativas de solo lectura en Metasploitable (`df -h`, `mount`, `whoami`).
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/f54b3ae27e9013e22b187e7aad5315291c19a5cd/Captura%20desde%202026-10-23%2009-05-57.png)
![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/f54b3ae27e9013e22b187e7aad5315291c19a5cd/Captura%20desde%202026-10-23%2009-06-46.png)

## Conclusión

Aprendí a diferenciar con claridad los conceptos de disco, partición, sistema de archivos y punto de montaje, comprendiendo que la exploración de un equipo objetivo debe limitarse estrictamente a consultas informativas y de solo lectura para preservar la integridad y seguridad del entorno.
