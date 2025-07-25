# 25 (SMPT)

## SMTP

> **TIP** El protocolo **SMTP** (Simple Mail Transfer Protocol) permite enviar correos electrónicos en una red IP. Puede usarse entre un cliente de correo y un servidor saliente, o entre dos servidores SMTP. Suele combinarse con **IMAP** o **POP3**, que permiten recibir y gestionar los correos.

> **IMPORTANT** Por defecto, los servidores SMTP aceptan conexiones en el puerto **25**. Sin embargo, también se utilizan puertos como el **587/TCP** para conexiones autenticadas y seguras.

***

### Servidor SMTP: funciones clave y flujo de envío

#### Prevención de spam y autenticación

* Implementación de **ESMTP** con **SMTP-Auth** para asegurar que solo usuarios autorizados puedan enviar correos.
* El **MUA** (Mail User Agent) arma el correo (encabezado + cuerpo) y lo envía al servidor SMTP.

#### Componentes principales

1. **Mail Submission Agent (MSA)**
   * También llamado _relay_ o servidor de envío.
   * Verifica origen y validez del mensaje usando SMTP-Auth.
   * Previene ataques como **Open Relay**.
2. **Mail Transfer Agent (MTA)**
   * Componente central del software de correo.
   * Verifica tamaño, filtra spam y almacena temporalmente el mensaje.
   * Consulta DNS para obtener la IP del servidor destino (registro MX).

#### Flujo de entrega

1. El **MUA** se autentica en el **MSA** con SMTP-Auth.
2. El MSA valida las credenciales.
3. El MSA entrega el mensaje al **MTA**.
4. El MTA verifica contenido, filtra y consulta el MX del dominio destino.
5. El MTA envía el mensaje al MTA del destinatario.

> **WARNING** Un **Open Relay Attack** ocurre cuando el servidor acepta reenviar correos de usuarios no autorizados, permitiendo envío masivo de spam.

> **TIP** Una vez entregado al servidor de destino, el correo es procesado por el **Mail Delivery Agent (MDA)** y transferido al buzón del destinatario. _MUA ➔ MSA ➔ MTA ➔ MDA ➔ POP3/IMAP_

***

### Configuración predeterminada de Postfix

```bash
cat /etc/postfix/main.cf | grep -v "#" | sed -r "/^\s*$/d"
```

```bash
smtpd_banner = ESMTP Server
biff = no
append_dot_mydomain = no
readme_directory = no
compatibility_level = 2
smtp_tls_session_cache_database = btree:${data_directory}/smtp_scache
myhostname = mail1.inlanefreight.htb
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
smtp_generic_maps = hash:/etc/postfix/generic
mydestination = $myhostname, localhost
masquerade_domains = $myhostname
mynetworks = 127.0.0.0/8 10.129.0.0/16
mailbox_size_limit = 0
recipient_delimiter = +
smtp_bind_address = 0.0.0.0
inet_protocols = ipv4
smtpd_helo_restrictions = reject_invalid_hostname
home_mailbox = /home/postfix
```

| Comando        | Descripción                                                     |
| -------------- | --------------------------------------------------------------- |
| **AUTH PLAIN** | Autenticación del cliente usando credenciales.                  |
| **HELO**       | Inicia sesión con el nombre del host cliente.                   |
| **MAIL FROM**  | Define al remitente del mensaje.                                |
| **RCPT TO**    | Define al destinatario.                                         |
| **DATA**       | Inicia la transmisión del contenido del correo.                 |
| **RSET**       | Cancela la transmisión pero mantiene la conexión.               |
| **VRFY**       | Verifica si existe un buzón para el destinatario.               |
| **EXPN**       | Similar a VRFY, comprueba disponibilidad para enviar.           |
| **NOOP**       | Solicita respuesta del servidor sin hacer nada, evita timeouts. |
| **QUIT**       | Finaliza la sesión SMTP.                                        |

#### Conexión SMTP con Telnet

```bash
# Logs SMTP
/var/mail/<usuario>

# Conexión
$ telnet 10.129.14.128 25

# Interacción SMTP
EHLO inlanefreight.htb
MAIL FROM: evilmail@inlanefreight.htb
RCPT TO: admin@inlanefreight.htb
DATA
Asunto: Prueba SMTP
Esto es un mensaje de prueba.
.
QUIT
```

> **NOTE** Lista de códigos de estado SMTP: [https://serversmtp.com/smtp-error/](https://serversmtp.com/smtp-error/)

***

### Configuraciones peligrosas

> **TIP** Para evitar el filtrado como spam, es recomendable usar un servidor de retransmisión de confianza y autenticarse correctamente.

> **WARNING** Una mala gestión de los rangos IP permitidos puede abrir el servidor a ataques. Esto es común en pentests internos y externos.

#### Ejemplo de Open Relay

```bash
mynetwork = 0.0.0.0/0
```

> **IMPORTANT** Esta configuración permite enviar correos falsos y realizar ataques de spoofing y lectura de mensajes.

***

### Enumeración de SMTP

```bash
# Escaneo básico con Nmap
sudo nmap 10.129.14.128 -sC -sV -p25

# Detectar Open Relay
sudo nmap 10.129.14.128 -p25 --script smtp-open-relay -v

# Enumerar usuarios SMTP
nmap -p 25 --script smtp-enum-users 10.129.42.195
```

***

### Redes sociales

* LinkedIn: [https://www.linkedin.com/in/tuch0/](https://www.linkedin.com/in/tuch0/)
* Instagram: [https://www.instagram.com/tuch0\_/](https://www.instagram.com/tuch0_/)
* YouTube: [https://www.youtube.com/@tuch0](https://www.youtube.com/@tuch0)\_
* GitHub: [https://github.com/Tuch0](https://github.com/Tuch0)
* Web personal: [https://tuch0.com/](https://tuch0.com/)

> 📄 Apuntes personales de HTB Academy. Para uso educativo.
