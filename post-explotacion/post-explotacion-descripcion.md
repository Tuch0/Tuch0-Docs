---
description: >-
  Técnicas para consolidar acceso, escalar privilegios, moverse lateralmente y
  mantener persistencia tras la intrusión inicial.
---

# Post Explotación descripción

***

## Post Explotación

> **Objetivo**\
> Cubrir la fase crítica posterior a la intrusión: **convertir un acceso inicial en control total y sostenido** dentro de la infraestructura.

### Contenido previsto

#### 1. Escalada de privilegios

**Linux**

* Grupos privilegiados (`adm`, `docker`, `lxd`, etc.)
* Abuso de **capabilities** y detección
* Privilegios mediante **sudoers** y **SUID**
* _Path / Library Hijacking_ y servicios internos
* **Kernel exploits** y _Docker breakout_
* Automatización de la enumeración (_linpeas_, _lse_, scripts propios)

**Windows**

* Grupos especiales (DnsAdmins, Server Operators, LAPS Readers…)
* **SeImpersonatePrivilege** & `WriteOwner`
* `AlwaysInstallElevated` y otras políticas inseguros
* **PFX exploitation** y gestión de certificados
* Cheatsheet de _privesc_ + scripts para leer contraseñas LAPS

#### 2. Movimientos laterales

* **Pivoting** con _Metasploit_ (port-forwarding, SOCKS5, SteelCheat)
* Laboratorios paso a paso (incluida simulación de examen eCPTv2)
* Enumeración de saltos de red y bypass de restricciones internas

#### 3. Persistencia

* Activar RDP o servicios remotos de forma sigilosa
* _Dumping_ de hashes y reutilización de credenciales (**Mimikatz**, **LaZagne**)
* Modificación de `LocalAccountTokenFilterPolicy`
* Persistencias "one-liner" y scripts multi-OS

> **Publicación continua**\
> Cada sub-tópico se lanzará cuando los laboratorios y capturas estén listos. Los temas en gris indican que están en cola de QA.

### Quién se beneficia

| Rol                        | Ventaja                                                        |
| -------------------------- | -------------------------------------------------------------- |
| **Red Team**               | Playbooks reproducibles y listos para CI/CD.                   |
| **Blue Team / SOC**        | Visibilidad de TTP reales para afinar detecciones en SIEM.     |
| **Ingeniería de sistemas** | Guías de hardening para bloquear vectores tras la explotación. |

### Mantente al día

* 🌐 **Web:** [https://tuch0.com/](https://tuch0.com/)
* 📸 **Instagram:** [@tuch0\_](https://www.instagram.com/tuch0_/)
* 💼 **LinkedIn:** [https://www.linkedin.com/in/tuch0](https://www.linkedin.com/in/tuch0)
* ▶️ **YouTube:** [https://www.youtube.com/@tuch0\_](https://www.youtube.com/@tuch0_)

