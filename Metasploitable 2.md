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
