# 3306 (MySQL)

## MySQL

> **TIP** **MySQL** es un sistema de gestión de bases de datos relacionales (RDBMS) de código abierto, desarrollado y respaldado por Oracle. Permite organizar, almacenar y recuperar grandes cantidades de datos con alto rendimiento.

***

### Clientes MySQL

> **NOTE** Los clientes MySQL interactúan con el servidor de base de datos mediante consultas SQL. Esto permite insertar, eliminar, modificar y recuperar información de forma eficiente y concurrente.

***

### Bases de datos MySQL

> **NOTE** MySQL es ideal para aplicaciones como sitios web dinámicos, donde la eficiencia y la velocidad de respuesta son clave. Suele formar parte del stack LAMP (Linux, Apache, MySQL, PHP) o LEMP (Linux, Nginx, MySQL, PHP).
>
> Almacena contenido requerido por scripts PHP como:

| Encabezados                       | Textos                  | Metaetiquetas          | Formularios |
| --------------------------------- | ----------------------- | ---------------------- | ----------- |
| Clientes                          | Nombres de usuario      | Administradores        | Moderadores |
| Direcciones de correo electrónico | Información del usuario | Permisos               | Contraseñas |
| Enlaces externos/internos         | Enlaces a archivos      | Contenidos específicos | Valores     |

***

### Comandos de MySQL

> **NOTE** Una base de datos MySQL traduce internamente los comandos SQL a instrucciones ejecutables en el sistema.

***

### Configuración predeterminada

```bash
# Instalamos MySQL
sudo apt install mysql-server -y

# Mostramos configuración activa sin comentarios
cat /etc/mysql/mysql.conf.d/mysqld.cnf | grep -v "#" | sed -r '/^\s*$/d'
```

***

### Configuraciones peligrosas

> **WARNING** Muchas configuraciones por defecto de MySQL pueden representar un riesgo. Es recomendable revisarlas cuidadosamente y ajustarlas para mejorar la seguridad.

| Ajustes            | Descripción                                                                 |
| ------------------ | --------------------------------------------------------------------------- |
| `user`             | Usuario bajo el cual se ejecuta el servicio MySQL.                          |
| `password`         | Contraseña del usuario MySQL.                                               |
| `admin_address`    | Dirección IP donde escucha conexiones TCP/IP el servidor.                   |
| `debug`            | Indica si está activa la depuración.                                        |
| `sql_warnings`     | Controla la generación de advertencias en instrucciones `INSERT`.           |
| `secure_file_priv` | Limita operaciones de importación/exportación de datos a una ruta concreta. |

***

### Reconocimiento

> **IMPORTANT** Aunque no es recomendable, algunos servidores MySQL están accesibles desde el exterior. Esto representa un riesgo si no está debidamente asegurado.

```bash
# Escaneo con Nmap
sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*

# Conexión al servidor MySQL
mysql -u root -h 10.129.14.132

# Conexión autenticada
mysql -u root -pP4SSw0rd -h 10.129.14.128
```

#### Consultas más usadas

| Comando                                              | Descripción                                                               |
| ---------------------------------------------------- | ------------------------------------------------------------------------- |
| `mysql -u <user> -p<password> -h <IP address>`       | Conecta con el servidor MySQL. No hay espacio entre `-p` y la contraseña. |
| `show databases;`                                    | Muestra las bases de datos disponibles.                                   |
| `use <database>;`                                    | Selecciona una base de datos.                                             |
| `show tables;`                                       | Lista las tablas de la base de datos activa.                              |
| `show columns from <table>;`                         | Muestra las columnas de una tabla.                                        |
| `select * from <table>;`                             | Muestra todos los registros de una tabla.                                 |
| `select * from <table> where <column> = "<string>";` | Filtra registros por coincidencia en una columna.                         |

***

### Redes sociales

* LinkedIn: [https://www.linkedin.com/in/tuch0/](https://www.linkedin.com/in/tuch0/)
* Instagram: [https://www.instagram.com/tuch0\_/](https://www.instagram.com/tuch0_/)
* YouTube: [https://www.youtube.com/@tuch0](https://www.youtube.com/@tuch0)\_
* GitHub: [https://github.com/Tuch0](https://github.com/Tuch0)
* Web personal: [https://tuch0.com/](https://tuch0.com/)

> 📄 Apuntes personales de HTB Academy. Para uso educativo.
