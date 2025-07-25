# 161,162 UDP (SNMP)

## SNMP

> **NOTE** **Simple Network Management Protocol (SNMP)** se creó para supervisar dispositivos de red. Además, permite gestionar tareas de configuración y modificar ajustes de forma remota. El hardware compatible con SNMP incluye routers, switches, servidores, dispositivos IoT, entre otros. Es un protocolo esencial para la supervisión y la gestión de dispositivos en redes.

***

### MIB

> **NOTE** Para garantizar compatibilidad entre distintos fabricantes y combinaciones cliente-servidor, se creó el formato **MIB (Management Information Base)**. Es un archivo de texto que contiene identificadores de objetos (_OID_) que definen la información de los dispositivos.

> **TIP** Un **OID** representa un nodo en un espacio de nombres jerárquico. Una secuencia de números identifica únicamente cada nodo. Cuanto más larga sea la cadena, más específica será la información.

***

### Versiones de SNMP

> **WARNING**
>
> * **SNMPv1**: Protocolo básico sin autenticación ni cifrado. Toda la información circula en texto plano.
> * **SNMPv2c**: Mejora en funcionalidades pero misma debilidad en seguridad. Las "community strings" viajan en texto plano.
> * **SNMPv3**: Incorpora autenticación (usuario y contraseña) y cifrado. Más complejo de configurar, pero mucho más seguro.

***

### Community Strings

> **IMPORTANT** Las cadenas de comunidad actúan como contraseñas para determinar el acceso a la información SNMP. Aunque SNMPv3 es más seguro, muchas organizaciones siguen usando SNMPv2 por su simplicidad, dejando activos servicios vulnerables.

***

### Configuración predeterminada

> **IMPORTANT** La configuración por defecto del demonio SNMP define IPs, puertos, MIBs, OIDs, autenticación y cadenas de comunidad.

> Manual oficial: [https://www.net-snmp.org/docs/man/snmpd.conf.html](https://www.net-snmp.org/docs/man/snmpd.conf.html)

```bash
# Configuración
cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'

sysLocation    Sitting on the Dock of the Bay
sysContact     Me <me@example.org>
sysServices    72
master  agentx
agentaddress  127.0.0.1,[::1]
view   systemonly  included   .1.3.6.1.2.1.1
view   systemonly  included   .1.3.6.1.2.1.25.1
rocommunity  public default -V systemonly
rocommunity6 public default -V systemonly
rouser authPrivUser authpriv -V systemonly
```

***

### Configuraciones peligrosas

| Ajustes                                            | Descripción                                     |
| -------------------------------------------------- | ----------------------------------------------- |
| rwuser noauth                                      | Acceso completo al árbol OID sin autenticación. |
| rwcommunity `<community string>` `<IPv4 address>`  | Acceso total sin restricción de origen.         |
| rwcommunity6 `<community string>` `<IPv6 address>` | Igual que el anterior pero usando IPv6.         |

***

## SNMP Enumeration Checklist

Checklist y comandos útiles para recolectar información por el puerto **UDP/161**.

### 1. Descubrir / Bruteforce Community Strings

```bash
# Fuerza bruta con onesixtyone
onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt <IP>

# Detección con Nmap
nmap -sU -p161 --script snmp-brute <IP>
```

### 2. SNMPwalk (v1 / v2c)

```bash
# Volcado completo
snmpwalk -v2c -c <community> <IP>

# Info de sistema
snmpwalk -v2c -c <community> <IP> 1.3.6.1.2.1.1

# Contacto y ubicación
snmpget -v2c -c <community> <IP> 1.3.6.1.2.1.1.4.0  # sysContact
snmpget -v2c -c <community> <IP> 1.3.6.1.2.1.1.6.0  # sysLocation

# Versión del agente
snmpget -v2c -c <community> <IP> 1.3.6.1.4.1.2021.100.2.0
```

### 3. Tablas interesantes

| Tabla         | OID                 | Uso                   |
| ------------- | ------------------- | --------------------- |
| hrSWRunTable  | 1.3.6.1.2.1.25.4.2  | Procesos en ejecución |
| hrSWInstalled | 1.3.6.1.2.1.25.6.3  | Software instalado    |
| hrDevice      | 1.3.6.1.2.1.25.3    | Información hardware  |
| tcpConnTable  | 1.3.6.1.2.1.6.13    | Conexiones TCP        |
| ifDescr       | 1.3.6.1.2.1.2.2.1.2 | Interfaces de red     |

```bash
snmpwalk -v2c -c <community> <IP> 1.3.6.1.2.1.25.4.2
```

### 4. Braa (paralelo y silencioso)

```bash
# Uso básico
braa <community>@<IP>:.1.3.6.*

# Múltiples OIDs
grep -f oids.txt | braa public@<IP>
```

### 5. Scripts NSE de Nmap

```bash
nmap -sU -p 161 --script "snmp-*" <IP>
```

> **NOTE**
>
> Ejemplos de scripts útiles:
>
> * `snmp-ios-config`: descarga la running-config de routers Cisco.
> * `snmp-sysdescr`: muestra banner / versión del sistema.

### 6. Herramientas extra

* `snmp-check`: salida legible con info relevante.
* `snmpenum` (Metasploit): módulo auxiliar para tablas host/hr.
* `snmpscan.py`: escaneo masivo de rangos y cadenas.

### 7. Tips & Trucos

* Aumentar timeout:

```bash
snmpwalk -v2c -c <community> -t 10 <IP>
```

* Filtrar cadenas visibles:

```bash
snmpwalk -v2c -c <community> <IP> | grep -E "STRING|Timeticks"
```

* Si faltan archivos MIB:

```bash
export MIBS=+ALL
```

y/o instalar `snmp-mibs-downloader`.

***

### Checklist Rápido

1. Verifica puerto **161/udp** abierto.
2. Bruteforce de community strings.
3. Usa `snmpwalk` para volcado completo.
4. Extrae `sysDescr`, `sysName`, `sysContact`.
5. Revisa `hrSWRunTable` para procesos sensibles.
6. Consulta versión Net-SNMP (`2021.100.x`).
7. Lanza scripts SNMP con Nmap.

***

### Redes sociales

* LinkedIn: [https://www.linkedin.com/in/tuch0/](https://www.linkedin.com/in/tuch0/)
* Instagram: [https://www.instagram.com/tuch0\_/](https://www.instagram.com/tuch0_/)
* YouTube: [https://www.youtube.com/@tuch0](https://www.youtube.com/@tuch0)\_
* GitHub: [https://github.com/Tuch0](https://github.com/Tuch0)
* Web personal: [https://tuch0.com/](https://tuch0.com/)

> 📄 Apuntes personales de HTB Academy. Para uso educativo.
