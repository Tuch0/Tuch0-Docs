---
description: >-
  Catálogo vivo de utilidades, cheatsheets y lecturas recomendadas para cada
  fase del pentesting corporativo.
cover: https://i.imgur.com/bEG08k9.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Active Directory Descripción

### **¿Por qué Active Directory (AD) importa en el mundo corporativo?**

La mayoría de las redes empresariales basadas en Windows dependen de Active Directory como la columna vertebral de la autenticación, autorización y gestión de usuarios, grupos y políticas. Un fallo o mala configuración en AD puede dejar expuestos todos los recursos críticos de la organización: desde archivos compartidos hasta controladores de dominio.

***

### ¿Qué encontrarás en este capítulo?

1. **Arquitectura y Componentes Clave**
   * Estructura de Bosques, Dominios y Unidades Organizativas (OUs).
   * Controladores de Dominio (DCs), Catálogos Globales y Roles FSMO.
   * Objetos de usuario, grupos, políticas de grupo (GPOs) y relaciones de confianza.
2. **Enumeración y Reconocimiento en AD**
   * Técnicas para descubrir información de dominio sin credenciales (“anonymous binds”).
   * Uso de herramientas como `ldapsearch`, `BloodHound` y `nltest`.
   * Extracción de esquemas LDAP, usuarios, grupos y mapeo de relaciones jerárquicas.
3. **Ataques Típicos y Vectores de Explotación**
   * **Kerberoasting**: Cracking de tickets de servicio para extraer contraseñas de cuentas de servicio.
   * **AS-REP Roasting**: Ataque a cuentas sin preautenticación.
   * **DCSync / DCSHADOW**: Impersonación de un controlador de dominio para replicar hashes.
   * **SIDHistory Abuse**: Aprovechar atributos heredados para elevar privilegios.
   * Lateralidad en AD: técnicas de “Silver Ticket” y “Golden Ticket”.
4. **Hardening y Buenas Prácticas**
   * Configuración de políticas de contraseñas y bloqueo de cuentas.
   * Aplicación de “Least Privilege” en grupos sensibles (`Domain Admins`, `Enterprise Admins`).
   * Monitorización y alerta de eventos críticos: registros de Kerberos, cambios en GPOs y replicación de DC.
   * Segmentación de controladores de dominio y despliegue de DC Lite/Read-Only (RODC).
5. **Laboratorios y Ejercicios Prácticos**
   * Montaje de un entorno AD con **Windows Server** (vd. laboratorio con máquinas virtuales).
   * Escenario guiado: pasar de un usuario normal a comprometer el DC usando Kerberoasting y DCSync.
   * Despliegue de **BloodHound** para gráficamente mapear relaciones y detectar cuentas con privilegios excesivos.
   * Creación de políticas de grupo seguras y prueba de mitigaciones en tiempo real.

***

> **Publicación escalonada**\
> El material se irá completando en varias entregas. Marca esta sección como favorita y recibe notificaciones en GitBook cuando publiquemos nuevos laboratorios o casos prácticos.

***

### ¿A quién está dirigido?

* **Red Teams & Pentesters** que necesiten auditar entornos AD reales y automatizar playbooks de ataque.
* **Blue Teams & SOC** que busquen entender los puntos débiles más comunes y configurar alertas en SIEM.
* **Administradores de Sistemas Windows** que quieran reforzar su dominio y mantener un estado seguro.
* **Equipos de Formación/Certificación** que busquen laboratorios auto-contenidos para talleres y pruebas técnicas.

***

### Mantente conectado

Para ver demos en vídeo, cheatsheets y noticias sobre nuevos ejemplos de AD, sígueme en mis redes:

* 🌐 **Web personal** → [https://tuch0.com](https://tuch0.com/)
* 📷 **Instagram** → [https://www.instagram.com/tuch0\_/](https://www.instagram.com/tuch0_/)
* 💼 **LinkedIn** → [https://www.linkedin.com/in/tuch0](https://www.linkedin.com/in/tuch0)
* ▶️ **YouTube** → [https://www.youtube.com/@tuch0\_](https://www.youtube.com/@tuch0_)

