# Introducción a LLMNR y NBT-NS desde Linux

> **QUOTE:** [La resolución de nombres de multidifusión local de enlace](https://datatracker.ietf.org/doc/html/rfc4795) (LLMNR) y [el servicio de nombres NetBIOS](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc940063\(v=technet.10\)?redirectedfrom=MSDN) (NBT-NS) son componentes de Microsoft Windows que sirven como métodos alternativos de identificación de host que se pueden utilizar cuando falla el DNS.\
> Si una máquina intenta resolver un host pero la resolución DNS falla, normalmente la máquina intentará preguntar a todas las demás máquinas de la red local la dirección de host correcta a través de LLMNR.

> **NOTE:** LLMNR se basa en el formato del sistema de nombres de dominio (DNS) y permite que los hosts en el mismo enlace local realicen la resolución de nombres para otros hosts. Si LLMNR falla, se utilizará NBT-NS. NBT-NS identifica los sistemas en una red local por su nombre NetBIOS.

### Ejemplo rápido: envenenamiento por LLMNR/NBT-NS

1. Un host intenta conectarse al servidor de impresión en \print01.inlanefreight.local, pero accidentalmente escribe \printer01.inlanefreight.local.
2. El servidor DNS responde indicando que este host es desconocido.
3. Luego, el host transmite a toda la red local preguntando si alguien conoce la ubicación de \printer01.inlanefreight.local.
4. El atacante (nosotros con `Responder` en ejecución) responde al host indicando que lo que está buscando es \printer01.inlanefreight.local.
5. El host cree en esta respuesta y envía una solicitud de autenticación al atacante con un nombre de usuario y un hash de contraseña NTLMv2.
6. Luego, este hash se puede descifrar sin conexión o utilizar en un ataque de retransmisión SMB si se dan las condiciones adecuadas.

> **IMPORTANT:** Realizamos estas acciones para recopilar información de autenticación enviada a través de la red en forma de hashes de contraseñas NTLMv1 y NTLMv2. NTLMv1 y NTLMv2 son protocolos de autenticación que utilizan el hash LM o NT.

| Tool       | Description                                                                                                                              |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Responder  | Responder es una herramienta diseñada específicamente para envenenar LLMNR, NBT-NS y MDNS, con muchas funciones diferentes.              |
| Inveigh    | Inveigh es una plataforma MITM multiplataforma que puede utilizarse para ataques de suplantación de identidad y envenenamiento.          |
| Metasploit | Metasploit tiene varios escáneres integrados y módulos de suplantación de identidad diseñados para lidiar con ataques de envenenamiento. |

> Tanto "Responder" como "Inveigh" pueden atacar a los siguientes protocolos:
>
> * LLMNR
> * Sistema de nombres de dominio
> * MDNS
> * NBNS
> * DHCP
> * Protocolo ICMP
> * HTTP
> * HTTPS
> * SMB
> * LDAP
> * WebDAV
> * Autenticación de proxy

> Responder también tiene soporte para:
>
> * MSSQL
> * DCE-RPC
> * Autenticación FTP, POP3, IMAP y SMTP

```bash
# Primero identificar interfaz de red
ifconfig

# Uso básico
responder -I tun0 -rwf

# Rutas donde se guarda la información automáticamente:
1- /usr/share/responder/logs
2- /usr/share/responder/Responder.conf

# Obtenemos los hashes de cada usuario:
cat /usr/share/responder/logs/SMB-NTLMv2-SSP-172.16.5.130.txt | awk -F'::' '{print $1 "::" $2}' | sort -t ':' -k 1,1 -u

# Ahora los guardamos en un archivo y los rompemos con hashcat o johnTheRipper
```
