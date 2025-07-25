# IMAP / POP3

> **NOTE** Con la ayuda de **IMAP** (Internet Message Access Protocol), es posible acceder a los correos electrónicos desde un servidor de correo. A diferencia de **POP3** (Post Office Protocol), IMAP permite la gestión en línea de correos directamente en el servidor y admite estructuras de carpetas.

> **TIP** IMAP es ideal para funcionalidades como buzones jerárquicos directamente en el servidor, acceso a múltiples buzones durante una sesión y preselección de correos electrónicos.

> **IMPORTANT** IMAP transmite comandos, correos y credenciales en texto plano si no se configura cifrado. Muchos servidores requieren IMAP cifrado mediante **SSL/TLS** para proteger el tráfico. El cifrado puede usarse en el puerto estándar 143 o el alternativo 993.

***

### Configuración predeterminada

#### Comandos IMAP

| Comando                         | Descripción                                                  |
| ------------------------------- | ------------------------------------------------------------ |
| `1 LOGIN username password`     | Inicio de sesión del usuario.                                |
| `1 LIST "" *`                   | Enumera todos los directorios.                               |
| `1 CREATE "INBOX"`              | Crea un buzón con un nombre especificado.                    |
| `1 DELETE "INBOX"`              | Elimina un buzón.                                            |
| `1 RENAME "ToRead" "Important"` | Cambia el nombre de un buzón.                                |
| `1 LSUB "" *`                   | Devuelve un subconjunto de nombres de los buzones suscritos. |
| `1 SELECT INBOX`                | Selecciona un buzón para acceder a sus mensajes.             |
| `1 UNSELECT INBOX`              | Sale del buzón seleccionado.                                 |
| `1 FETCH <ID> all`              | Recupera datos de un mensaje en el buzón.                    |
| `1 CLOSE`                       | Elimina los mensajes con la bandera Deleted.                 |
| `1 LOGOUT`                      | Cierra la conexión con el servidor IMAP.                     |

#### Comandos POP3

| Comando         | Descripción                                       |
| --------------- | ------------------------------------------------- |
| `USER username` | Identifica al usuario.                            |
| `PASS password` | Autenticación del usuario mediante su contraseña. |
| `STAT`          | Solicita la cantidad de correos almacenados.      |
| `LIST`          | Solicita número y tamaño de los correos.          |
| `RETR id`       | Recupera un correo electrónico por ID.            |
| `DELE id`       | Elimina un correo electrónico por ID.             |
| `CAPA`          | Muestra las capacidades del servidor.             |
| `RSET`          | Restablece la información transmitida.            |
| `QUIT`          | Cierra la conexión con el servidor POP3.          |

***

### Configuraciones peligrosas

> **WARNING** Una configuración incorrecta podría permitir acceso anónimo o registro de comandos, como sucede con algunos servicios FTP.

> **BUG** Algunos servidores privados mal configurados podrían permitir leer todos los correos enviados y recibidos, incluyendo datos confidenciales.

| Configuración             | Descripción                                             |
| ------------------------- | ------------------------------------------------------- |
| `auth_debug`              | Habilita el registro de depuración de autenticación.    |
| `auth_debug_passwords`    | Incluye contraseñas y esquemas en los registros.        |
| `auth_verbose`            | Registra intentos fallidos y sus motivos.               |
| `auth_verbose_passwords`  | Muestra contraseñas usadas (pueden aparecer truncadas). |
| `auth_anonymous_username` | Define el nombre de usuario para sesiones SASL ANÓNIMO. |

***

### Reconocimiento

> **TIP** Puertos predeterminados: **110** y **995** para POP3, **143** y **993** para IMAP. Los puertos 995 y 993 cifran con **TLS/SSL**.

```bash
# Enumeración con nmap
nmap 10.129.14.128 -sV -p110,143,993,995 -sC

# Listar correos (con credenciales)
curl -k 'imaps://10.129.14.128' --user user:p4ssw0rd
curl -k 'imaps://10.129.14.128' --user cry0l1t3:1234 -v

# OpenSSL - Interacción cifrada TLS POP3
openssl s_client -connect 10.129.14.128:pop3s

# OpenSSL - Interacción cifrada TLS IMAP
openssl s_client -connect 10.129.14.128:imaps

# Iniciar sesión
A001 LOGIN robin robin
```

```ruby
# Listamos los buzones
A003 LIST "" *
* LIST (\Noselect \HasChildren) "." DEV
* LIST (\Noselect \HasChildren) "." DEV.DEPARTMENT
* LIST (\HasNoChildren) "." DEV.DEPARTMENT.INT
* LIST (\HasNoChildren) "." INBOX

# Seleccionamos uno
A004 SELECT DEV.DEPARTMENT.INT
* OK [CLOSED] Previous mailbox closed.
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 1 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1636414279] UIDs valid
* OK [UIDNEXT 2] Predicted next UID

# Leemos un mensaje
A005 FETCH 1 BODY[TEXT]
* 1 FETCH (BODY[TEXT] {34}
HTB{983uzn8jmfgpd8jmof8c34n7zio}
)
A005 OK Fetch completed (0.008 + 0.000 + 0.007 secs).

# Vemos remitente, destinatario y contenido
* 1 FETCH (BODY[] {167}
Subject: Flag
To: Robin <robin@inlanefreight.htb>
From: CTO <devadmin@inlanefreight.htb>
Date: Wed, 03 Nov 2021 16:13:27 +0200

HTB{983uzn8jmfgpd8jmof8c34n7zio}
)
A005 OK Fetch completed (0.001 + 0.000 secs).
* BAD Error in IMAP command : Unknown command (0.001 + 0.000 secs).
```

***

### Redes sociales

* LinkedIn: [https://www.linkedin.com/in/tuch0/](https://www.linkedin.com/in/tuch0/)
* Instagram: [https://www.instagram.com/tuch0\_/](https://www.instagram.com/tuch0_/)
* YouTube: [https://www.youtube.com/@tuch0](https://www.youtube.com/@tuch0)\_
* GitHub: [https://github.com/Tuch0](https://github.com/Tuch0)
* Web personal: [https://tuch0.com/](https://tuch0.com/)

> 📄 Apuntes personales de HTB Academy. Para uso educativo.
