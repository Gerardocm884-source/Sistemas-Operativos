
🟡 Semana 07 — Paquetes y reconocimiento autorizado

## Datos del alumno

* Nombre: José Gerardo Cabrera Miranda
* Grupo: 3° Semestre - Ingeniería en Sistemas Computacionales
* Fecha: 2026-10-22

## Entorno

* Versión de Ubuntu: Ubuntu 24.04 LTS
* Tipo de red virtual: Host-only (Aislada)
* IP de Ubuntu en el laboratorio: Verificada localmente (`wlp5s0`)
* IP confirmada de Metasploitable: Verificada en la red aislada del laboratorio

## Objetivo

Administrar y localizar herramientas en Ubuntu mediante la gestión de paquetes, además de realizar un reconocimiento de puertos limitado contra una máquina de laboratorio autorizada.

## Herramientas y Comandos Principales

| Comando | Propósito | Resultado observado |
| --- | --- | --- |
| `apt show nmap` | Muestra detalles del paquete Nmap

 | Información de versión y dependencias

 |
| `dpkg -s nmap` | Consulta si el paquete está instalado

 | Estado de instalación válido |
| `dpkg -L nmap` | Lista los archivos instalados por el paquete

 | Ubicaciones de binarios y recursos |
| `nmap --top-ports 100` | Escaneo rápido de puertos comunes

 | Detección de puertos abiertos en Metasploitable |
| `nmap -sV --top-ports 100` | Detección de versiones de servicios

 | Versiones estimadas de los servicios expuestos |

## 📊 Inventario de Servicios (Reconocimiento Limitado)

| Puerto/protocolo | Estado informado | Servicio/versión detectados | ¿Qué se puede concluir? | ¿Qué falta verificar? |
| --- | --- | --- | --- | --- |
| 21/tcp | Abierto | ProFTPD 1.3.1 | El servicio de transferencia de archivos está activo en el objetivo. | Verificar configuración de autenticación y si permite acceso anónimo. |
| 22/tcp | Abierto | OpenSSH 4.7p1 | El servicio de administración remota SSH está escuchando conexiones. | Comprobar si existen credenciales débiles o por defecto. |
| 80/tcp | Abierto | Apache httpd 2.2.8 | El servidor web del sistema está operativo y respondiendo peticiones. | Investigar si aloja aplicaciones web vulnerables o directorios expuestos. |
| 3306/tcp | Abierto | MySQL 5.0.51a | El servicio de base de datos está accesible en la red. | Comprobar si el usuario root tiene contraseña vacía o permisos remotos. |

## 📝 Preguntas de Análisis Respondidas

1. **¿Por qué conviene saber qué versión de Nmap está instalada?**
Para conocer las capacidades de la herramienta, los scripts de análisis de vulnerabilidades soportados y asegurar la compatibilidad con los tipos de escaneo que se realizarán.
2. **¿Qué diferencia existe entre `apt show` y `dpkg -s`?**
`apt show` consulta la información del paquete disponible en los repositorios locales e índices del sistema, mientras que `dpkg -s` verifica el estado real del paquete instalado de forma local en la máquina.
3. **¿Qué diferencia hay entre `apt update` y `apt upgrade`?**
`apt update` descarga y actualiza los catálogos/índices de los repositorios de software, mientras que `apt upgrade` descarga e instala las nuevas versiones de los paquetes ya instalados en el sistema.


4. **¿Qué información aporta `dpkg -L nmap`?**
Muestra la ruta exacta de todos los archivos y directorios que fueron instalados en el sistema operativo por dicho paquete.
5. **¿Por qué no basta con encontrar un puerto abierto para asegurar que hay una vulnerabilidad?**
Un puerto abierto solo indica que hay un servicio escuchando conexiones en esa interfaz; para confirmar una vulnerabilidad es necesario analizar la versión exacta, la configuración y el comportamiento del software.
6. **¿Qué limitación tiene `--top-ports 100`?**
Que analiza únicamente los 100 puertos considerados más comunes por la herramienta, omitiendo el resto de los 65,435 puertos del rango TCP disponibles.


7. **¿Por qué se debe registrar la IP objetivo antes de ejecutar Nmap?**
Para garantizar que el análisis se ejecute exclusivamente sobre el equipo autorizado del laboratorio y evitar errores o impactos en dispositivos ajenos.


8. **¿Qué problema ético y técnico podría causar escanear una red que no fue autorizada?**
Técnicamente puede saturar recursos o activar sistemas de defensa; ética y legalmente constituye una intromisión ilegítima y una violación de la privacidad y seguridad de sistemas ajenos.



## 📸 Registro de Evidencias

Las capturas de pantalla de esta práctica se ubican en el directorio `evidencias/`:

* `evidencias/01_red_y_direcciones.png`: Redes e interfaces de Ubuntu y Metasploitable.
* ![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/8f525988a21d6eb88eae3d07fbf3210e749f097b/Captura%20desde%202026-10-22%2008-58-03.png)


* `evidencias/02_paquete_nmap.png`: Verificación e instalación de Nmap.
* ![IMage alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/bed547527d7e61000be90d2efd8ad8047164cf52/Captura%20desde%202026-10-22%2009-11-40.png)


* `evidencias/03_archivos_paquete.png`: Localización de archivos del paquete con `dpkg -L`.
* ![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/c8e774e488cd7ccbe1fcd5e1aa57b721ce1ea774/Captura%20desde%202026-10-23%2008-39-28.png)


* `evidencias/04_reconocimiento_servicios.png`: Escaneo de Nmap y reporte de servicios.
* ![Image alt](https://github.com/Gerardocm884-source/Sistemas-Operativos/blob/0573de1fbf47e38ad39d8d4e2064ab210dc6fb2f/Captura%20desde%202026-10-22%2009-40-49.png)



## Conclusión

Comprendí que la administración de paquetes exige conocer dependencias y repositorios, y que el reconocimiento de red es un procedimiento de observación que requiere estricta autorización y aislamiento técnico.
