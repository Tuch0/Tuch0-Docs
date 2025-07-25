# TCP 111 - UDP 2049 (NFS)

## NFS

> **NOTE** **Network File System (NFS)** es un sistema de archivos de red desarrollado por Sun Microsystems, con un propósito similar al de SMB: permitir el acceso a sistemas de archivos a través de la red como si fueran locales. Utiliza un protocolo distinto y se emplea principalmente entre sistemas Linux y Unix. NFS es un estándar de Internet para sistemas de archivos distribuidos.

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-05-29 a las 12.49.53.png" alt=""><figcaption></figcaption></figure>

***

### Configuración predeterminada

> **NOTE** La configuración de NFS es relativamente sencilla, ya que tiene menos opciones que otros servicios como FTP o SMB. El archivo principal de configuración es `/etc/exports`, donde se define qué sistemas de archivos se comparten y con qué permisos.

#### Archivo de exportaciones

```bash
cat /etc/exports
```

> **INFO** Primero se especifica la carpeta que se desea compartir, y luego se definen los permisos que tendrán los clientes sobre ese recurso, así como las IPs o subredes autorizadas.

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-05-29 a las 13.02.59.png" alt=""><figcaption></figcaption></figure>

***

#### ExportFS

```bash
root@nfs:~# echo '/mnt/nfs  10.129.14.0/24(sync,no_subtree_check)' >> /etc/exports
root@nfs:~# systemctl restart nfs-kernel-server
root@nfs:~# exportfs

/mnt/nfs      	10.129.14.0/24
```

> **INFO** Con esta configuración, la carpeta `/mnt/nfs` se comparte con toda la subred `10.129.14.0/24`. Todos los hosts dentro de esta red podrán montar el recurso y acceder a su contenido.

***

#### Configuraciones peligrosas

<figure><img src="../../.gitbook/assets/Captura de pantalla 2025-05-29 a las 13.07.03.png" alt=""><figcaption></figcaption></figure>

> **WARNING** La opción `insecure` es peligrosa, ya que permite conexiones desde puertos mayores a 1024. Los puertos por debajo de 1024 están reservados para procesos con privilegios de root. Permitir puertos altos debilita la seguridad del servicio NFS.

***

#### Huella del servicio

> **TIP** Para identificar NFS en una red, los puertos más relevantes son el TCP 111 y el 2049.

```bash
# Scripts nmap
sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049
```

> **NOTE** Si se detecta un servicio NFS activo, podemos montarlo en nuestra máquina local. Para ello, creamos una carpeta vacía y montamos el recurso compartido en ella. Esto permite navegar por su contenido como si fuera parte del sistema local.

```bash
# Mostrar acciones disponibles
dhowmount -e 10.129.14.128

# Montaje de recursos compartidos
mkdir target-NFS
sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock
cd target-NFS
tree .

# Listar contenidos con nombre de usuario y grupos
ls -l /mnt/nfs/

# Listar contenidos con UID y GID
ls -n /mnt/nfs/

# Desmontar el recurso compartido
sudo umount ./target-NFS
```

***

### Redes sociales

* LinkedIn: [https://www.linkedin.com/in/tuch0/](https://www.linkedin.com/in/tuch0/)
* Instagram: [https://www.instagram.com/tuch0\_/](https://www.instagram.com/tuch0_/)
* YouTube: [https://www.youtube.com/@tuch0](https://www.youtube.com/@tuch0)\_
* GitHub: [https://github.com/Tuch0](https://github.com/Tuch0)
* Web personal: [https://tuch0.com/](https://tuch0.com/)

> 📄 Apuntes personales de HTB Academy. Para uso educativo.
