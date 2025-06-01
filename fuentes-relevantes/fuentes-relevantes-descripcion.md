---
description: >-
  Esta sección funciona como tu caja de herramientas central. Iremos
  incorporando fichas rápidas, ejemplos de uso y enlaces oficiales de cada
  recurso conforme los necesitemos en los distintos capítulos.
---

# Fuentes Relevantes Descripción

### Cómo está organizada

* **Reconocimiento & Enumeración** → descubrir hosts, puertos, rutas, usuarios y credenciales expuestos.
* **Explotación** → obtener acceso inicial, elevar privilegios y pivotar dentro de la red.
* **Post-explotación** → recolección de credenciales, mapeo de Active Directory y persistencia.
* **Utilidades misceláneas** → convertidores de hashes, depuradores y herramientas cloud.

Cada herramienta tendrá:

1. **One-liner** mínimo viable.
2. Ejemplo práctico en laboratorio.
3. Indicadores & contramedidas (para Blue Teams).
4. Enlace a documentación oficial.

> **Publicación progresiva**\
> Las fichas se irán activando a medida que los capítulos dependientes se publiquen. Sigue esta página o nuestras redes para enterarte de las nuevas altas.

***

### Reconocimiento & Enumeración

| Herramienta              | Rol principal                       | Estado                   |
| ------------------------ | ----------------------------------- | ------------------------ |
| `arp-scan`               | Descubrimiento de hosts en la LAN   | ✅ Ficha básica           |
| `Nmap`                   | Escaneo de puertos y servicios      | 🔄 Ampliando scripts NSE |
| `GoBuster` / `DirSearch` | Fuerza bruta de rutas web           | ⏳ Próxima                |
| `GitHack`                | Extracción de `.git` expuesto       | ⏳ Próxima                |
| `FUFF`                   | Fuzzing de directorios y parámetros | ⏳ Próxima                |
| `LDAP-Enum`              | Recolección de usuarios AD vía LDAP | ⏳ Próxima                |

***

### Explotación

| Herramienta            | Uso típico                                | Estado               |
| ---------------------- | ----------------------------------------- | -------------------- |
| `Metasploit Framework` | Payloads y módulos CVE                    | ✅ Cheatsheet inicial |
| `Responder`            | Captura de hashes SMB/LLMNR               | ✅ Ficha completa     |
| `Hydra`                | Ataques de diccionario (brute/cred-spray) | ⏳ Próxima            |
| `CrackMapExec`         | Living-off-the-Land en redes Windows      | ⏳ Próxima            |
| `SqlMap`               | Explotación SQLi automática               | ⏳ Próxima            |
| `Chisel`               | Túneles y port-forwarding                 | ⏳ Próxima            |

***

### Post-explotación

| Herramienta  | Función                               | Estado           |
| ------------ | ------------------------------------- | ---------------- |
| `BloodHound` | Mapeo de relaciones en AD             | 🔄 Añadiendo lab |
| `Inveigh`    | Escucha SMB/HTTP para hash-spray      | ✅ Ficha básica   |
| `firepwd`    | Extracción de credenciales de Firefox | ⏳ Próxima        |

***

### Utilidades Misceláneas

* **Conversores de hashes**: `gpg2john`, `zip2john`, `keepass2john`.
* **Debugging & exploitation**: `GDB-Peda`, `Swask`.
* **Transferencia/Pivoting**: `Netcat`, `Mount`, `rpcclient`.
* **Cloud**: scripts para enumeration & hardening de **AWS** _(en preparación)_.

***

### ¿Para quién es?

| Perfil                   | Beneficio inmediato                                                   |
| ------------------------ | --------------------------------------------------------------------- |
| **Red Team / Pentester** | One-liners listos para copiar-pegar en la fase adecuada.              |
| **Blue Team / SOC**      | Indicadores de compromiso y guías de detección asociadas a cada tool. |
| **Formación interna**    | Material de laboratorio reutilizable en workshops y certs.            |

***

### Mantente al día

* 🌐 **Web**: [https://tuch0.com/](https://tuch0.com/)
* 📷 **Instagram**: [https://www.instagram.com/tuch0\_/](https://www.instagram.com/tuch0_/)
* 💼 **LinkedIn**: [https://www.linkedin.com/in/tuch0](https://www.linkedin.com/in/tuch0)
* ▶️ **YouTube**: [https://www.youtube.com/@tuch0\_](https://www.youtube.com/@tuch0_)

