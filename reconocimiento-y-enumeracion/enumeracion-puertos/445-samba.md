---
description: >-
  Una recopilación concisa ―pero exhaustiva― sobre el protocolo Server Message
  Block (SMB) y su implementación libre Samba en sistemas Unix‑like. Aquí
  encontrarás conceptos básicos, configuraciones reco
---

# 445 (Samba)

***

### ¿Qué es SMB?

> **Cita:Server Message Block (SMB)** es un protocolo cliente‑servidor que regula el acceso a archivos, directorios completos y otros recursos de red —como impresoras o interfaces de red— dentro de un entorno compartido. Asimismo, permite el intercambio de información entre procesos del sistema.**Advertencia:** Los derechos de acceso se definen mediante **Access Control Lists (ACLs)** y pueden afinarse al nivel de _execute_, _read_ o _full access_ para usuarios o grupos.

***

### ¿Qué es Samba?

> **Cita:Samba** es la implementación libre del protocolo SMB/CIFS para sistemas **Unix**. Proporciona interoperabilidad con los sistemas Windows recientes y suele referirse a sí misma como **SMB/CIFS**.

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-05-29 a las 10.12.13 (1).png" alt=""><figcaption></figcaption></figure>

***

### Configuraciones predeterminadas

Para inspeccionar la configuración activa de Samba:

```bash
# Mostrar la configuración de smb.conf sin comentarios
grep -vE '^[#;]' /etc/samba/smb.conf
```

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-05-29 a las 10.18.06.png" alt=""><figcaption></figcaption></figure>

***

### Configuraciones peligrosas

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-05-29 a las 10.20.01.png" alt=""><figcaption></figcaption></figure>

> **Advertencia:** El siguiente ejemplo crea un recurso compartido _extremadamente_ permisivo —solo con fines didácticos—. **No lo uses en producción.**

```ini
[notes]
   comment        = CheckIT
   path           = /mnt/notes/
   browseable     = yes
   read only      = no
   writable       = yes
   guest ok       = yes
   enable privileges = yes
   create mask    = 0777
   directory mask = 0777
```

Después de modificar **smb.conf** recuerda recargar el servicio:

```bash
sudo systemctl restart smbd
```

***

### Conexión al recurso compartido

#### crackmapexec

```bash
crackmapexec smb <IP>
crackmapexec smb <IP> --shares
crackmapexec smb 10.10.11.4 -u 'jmontgomery' -p 'Midnight_121' -M spider_plus
```

#### smbmap

```bash
smbmap -H <IP>
smbmap -H <IP> -u 'null'
smbmap -H <IP> -u <user> -p <password> --download <dir>/<file>
smbmap -H <IP> -u <user> -p <password> -r
```

#### smbclient

```bash
smbclient -L //<IP> -N
smbclient //<IP>/<recurso> -N
```

#### rpcclient

```bash
rpcclient -U "" <IP>
```

***

### Seguridad a nivel de dominio

> **Nota:**\
> Con seguridad a nivel de dominio, el servidor Samba actúa como miembro de un dominio Windows. La autenticación la gestiona el **Controlador de Dominio (DC)**.

Comandos útiles dentro de `smbclient`:

```bash
# Descargar un archivo
get <archivo>

# Ejecutar un comando local sin cerrar la sesión SMB
!<cmd>

# Mostrar qué recurso está usando cada usuario (requiere privilegios de admin)
smbstatus
```

***

### Enumeración con rpcclient

> **Info:**`rpcclient` permite interactuar con los servicios **MS‑RPC** expuestos por un servidor SMB, de forma local o remota.

```bash
srvinfo                    # Información del servidor
enumdomains                # Lista de dominios
querydominfo               # Info de dominio, servidor y usuario
netshareenumall            # Lista completa de recursos compartidos
netsharegetinfo <share>    # Detalles de un recurso
enumdomusers               # Enumerar usuarios de dominio
queryuser <RID>            # Info de un usuario
querygroup <RID>           # Info de un grupo
```

> **Importante:**\
> Algunos comandos dependen del RID. Si desconoces qué RID corresponde a cada usuario, puedes _forzar_ la consulta:

```bash
for i in $(seq 500 1100); do
  rpcclient -N -U "" 10.129.14.128 -c "queryuser 0x$(printf '%x\n' $i)" \
  | grep -E 'User Name|user_rid|group_rid' && echo ""
done
```

Salida de ejemplo:

```
User Name   :   sambauser
user_rid    :   0x1f5
group_rid   :   0x201

User Name   :   mrb3n
user_rid    :   0x3e8
group_rid   :   0x201

User Name   :   cry0l1t3
user_rid    :   0x3e9
group_rid   :   0x201
```

Alternativamente puedes usar [`samrdump.py`](https://github.com/SecureAuthCorp/impacket/blob/master/examples/samrdump.py):

```bash
samrdump.py 10.129.14.128
```

***

### Herramientas adicionales

#### Enum4linux‑NG

```bash
git clone https://github.com/cddmp/enum4linux-ng.git
cd enum4linux-ng
pip3 install -r requirements.txt
./enum4linux-ng.py 10.129.14.128
```

***

### Buenas prácticas de seguridad

1. **Principio de privilegio mínimo:** comparte solo los directorios necesarios y con el nivel mínimo de permisos.
2. **Deshabilita cuentas invitadas** salvo que sea estrictamente necesario.
3. **Habilita SMBv3** y desactiva versiones obsoletas (SMBv1).
4. **Aplica firewall interno** y permite el acceso únicamente desde subredes confiables.
5. **Registra y monitoriza** accesos y modificaciones en recursos compartidos.

***

### Créditos y referencias

* [Samba Documentation](https://www.samba.org/samba/docs/)
* [Microsoft SMB Protocol](https://learn.microsoft.com/en-us/windows/win32/fileio/microsoft-smb-protocol-and-ci)

***

> **Licencia:** MIT. Se permite la copia y modificación con atribución.
