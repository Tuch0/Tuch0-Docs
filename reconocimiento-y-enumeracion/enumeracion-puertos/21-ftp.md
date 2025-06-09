# 21 (FTP)

### FTP - Puertos y funcionamiento

> El protocolo File Transfer Protocol ( FTP) es uno de los más antiguos de Internet. El FTP se ejecuta en la capa de aplicación de la pila de protocolos TCP/IP. Por lo tanto, se encuentra en la misma capa que HTTPo POP.

#### Puertos

* **Puerto 21 (Control):**
  * Envía comandos: `USER`, `PASS`, `LIST`, `RETR`, `STOR`…
  * Responde con códigos: `200` = OK, `550` = Error, …
* **Puerto 20 (Datos):**
  * Transfiere los bytes del fichero.
  * Detección de errores y reanudación automática si se corta la conexión.

#### Funcionamiento paso a paso

1. **Conexión de control (Puerto 21)**
   * Cliente → Servidor: autenticación (`USER`/`PASS`) y envío de comandos.
2. **Apertura del canal de datos (Puerto 20)**
   * Tras aceptar un comando de transferencia, el servidor abre el canal de datos.
3. **Transferencia de archivos**
   * Flujo de datos por el puerto 20.
   * Comprobación de bloques y códigos de estado.
   * Si hay caída de conexión, al reconectar retoma donde quedó.
4. **Cierre de la conexión**
   * Se cierran ambos canales (21 y 20) al finalizar.

> [Lista Códigos de Estado](https://en.wikipedia.org/wiki/List_of_FTP_server_return_codes)

***

#### TFTP

> \[!quote] Trivial File Transfer Protocol (TFTP) es más simple que FTP y realiza transferencias de archivos entre procesos cliente y servidor. Sin embargo, does notproporciona autenticación de usuarios y otras funciones valiosas compatibles con FTP. Además, mientras que FTP usa TCP, TFTP usa UDP, lo que lo convierte en un protocolo poco fiable y obliga a utilizar la recuperación de la capa de aplicación asistida por UDP.



<figure><img src="../../.gitbook/assets/Pasted image 20250527104930.png" alt=""><figcaption></figcaption></figure>

```bash
# Instalar vsFTPd
sudo apt install vsftpd 

# Archivo de configuración vsFTPd
cat /etc/vsftpd.conf | grep -v "#"
```

<figure><img src="../../.gitbook/assets/Pasted image 20250527105907 (1).png" alt=""><figcaption></figcaption></figure>

```bash
# Usuarios FTP
cat /etc/ftpusers
```

#### Configuraciones peligrosas

<figure><img src="../../.gitbook/assets/Pasted image 20250527110123.png" alt=""><figcaption></figcaption></figure>

```bash
# Inicio con ftp anonymous
ftp 10.129.14.136
user: anonymous
```

```bash
# Enumeración de entorno
status -> Descripción general del sistema
debug  -> Información útil para nuestros fines
trace  -> Información útil para nuestros fines
```

<figure><img src="../../.gitbook/assets/Pasted image 20250527110703.png" alt=""><figcaption></figcaption></figure>

```bash
# Descargar todos los archivos disponibles
wget -m --no-passive ftp://anonymous:anonymous@10.129.14.136

# Subida de archivos
touch testupload.txt
put testupload.txt (dentro del ftp)

# Scripts de nmap
sudo nmap --script-updatedb (ruta sripts: /usr/share/nmap/scripts/)
find / -type f -name ftp* 2>/dev/null | grep scripts
```

#### Interacción de servicio

```bash
# Netcat
nc -nv 10.129.14.136 21

# Telnet
telnet 10.129.14.136 21

# Openssl
openssl s_client -connect 10.129.14.136:21 -starttls ftp
```

***

#### Conexión básica

```bash
# Nos conectamos por FTP
ftp <ip_address> 

# Nos conectamos como anonymous
frp <ip_address>
user: anonymous
password:
```

### Fuerza bruta con Hydra

```bash
# Iniciamos ataque de fuerza bruta
hydra -l <user> -P <wordlists>.txt ftp://<ip_address> -t 15
```

```ad-quote
Los parametros `-l y -p` se escriben en minuscula cuando sabes el dato , si vas a usar un diccionario como el caso de `-P` lo pones en mayuscula para indicar que es un archivo
```
