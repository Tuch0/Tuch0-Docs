---
cover: ../.gitbook/assets/Imagen de WhatsApp 2025-06-05 a las 09.31.30_b7fa0034.jpg
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

# Cómo montar un ciberdeck profesional

_tuch0 — 19 años_

Montar un **ciberdeck** va más allá de conectar cables. En esta guía cuento, de forma directa y sin adornos, cómo pasé de un vídeo en YouTube a tener un laboratorio espacial en una maleta.

***

### Índice

1. Origen de la idea (2025)
2. Qué es un ciberdeck
3. Hardware y coste
4. Diseño y montaje
5. Problemas y soluciones
6. Misiones de prueba
7. Conecta y comparte

***

### 1. Origen de la idea (2025)

Desde pequeño el espacio me ha llamado la atención, como a muchos. Pero era algo lejano y terminaba quedando en segundo plano. Hace unos meses, mientras navegaba por Internet, YouTube me sugirió el vídeo de la NASA **“Cómo es la Estación Espacial Internacional”**. Un astronauta la recorría cámara en mano y salí de ese vídeo totalmente fascinado.

Ese instante unió mis dos aficiones: el espacio y la ciberseguridad. Me vinieron varias preguntas:

* _¿Existe la ciberseguridad de los satélites?_
* _¿Alguien tiene que protegerlos?_
* _¿Son vulnerables?_
* _¿Cómo puedo aprender?_

Investigando encontré la charla de **R0r0x** sobre _satellite hacking_. Confirmé que era posible, pero también que necesitaba hardware específico. Después de ver el vídeo de un inglés que se había construido un equipo para “satellite hacking”, decidí invertir y montar mi propio **ciberdeck** para empezar a aprender.

***

### 2. Qué es un ciberdeck

Una maleta robusta que reúne todo lo necesario para captar y analizar señales de satélite, radio y Wi‑Fi. Debe ser autónoma varias horas y lo bastante compacta para que nada se mueva al transportarla.

***

### 3. Hardware y coste (2025)

| Componente                                    | Detalle                        | Precio €    |
| --------------------------------------------- | ------------------------------ | ----------- |
| Maleta IP67                                   | Tipo Pelican 1150              | 45          |
| Raspberry Pi 4                                | 4 GB + carcasa                 | 95          |
| MicroSD 128 GB                                | Clase A2                       | 8           |
| [RTL‑SDR v3 (kit)](https://amzn.eu/d/60LToUB) | Dongle + antenas               | 100         |
| Alfa AWUS036ACH                               | Adaptador Wi‑Fi                | 25          |
| Monitor 11″ 1080p                             | USB‑C + Mini‑HDMI              | 80          |
| Teclado mecánico 65 %                         | Switch lineal                  | 80          |
| Powerbank 27 000 mAh PD                       | 20 V / 3 A                     | 25          |
| Amplificador LNA                              | 20 dB, 50–1200 MHz             | 15          |
| Hub USB 3.0 compacto                          | Oculto bajo teclado            | 10          |
| Cables y adaptadores                          | USB‑C y (Mini/Micro)‑HDMI en L | 30          |
| **Total aproximado**                          |                                | **≈ 515 €** |

***

### 4. Diseño y montaje paso a paso

1. **Medir antes de comprar**\
   – Teclado 65 % y Raspberry marcan la altura del fondo.\
   – La tapa limita el tamaño del monitor.
2. **Recortar la espuma**\
   – Siluetas exactas; todo queda a ras.
3. **Cableado**\
   – Conectores rectos no cabían → cables en L.\
   – El primer cable de 50 cm fue corto; cambié a 1 m y abrí un canal trasero.\
   – Adaptador HDMI → Micro‑HDMI para la Pi.
4. **Fijación**\
   – Velcro y un punto de silicona para monitor, Pi y Alfa.\
   – Hub USB, RTL‑SDR y LNA bajo el teclado.
5. **Antenas**\
   – Trípode del RTL‑SDR sujeto con velcro en la esquina frontal.\
   – Hueco para las antenas extensibles.
6. **Detalle final**\
   – Pegatinas NASA para dejar clara la temática.

***

### 5. Problemas y soluciones

| Problema            | Causa                | Solución                           |
| ------------------- | -------------------- | ---------------------------------- |
| Cables no entran    | Monitor muy ajustado | Conectores en L.                   |
| Cable corto         | 50 cm a powerbank    | Cable en L de 1 m + canal trasero. |
| Componentes sueltos | Golpes en transporte | Velcro + espuma a medida.          |
| Calor en la Pi      | Maleta cerrada       | Ventilar 5 min cada 2 h.           |

***

### 6. Misiones de prueba

1. **NOAA APT** (137 MHz) → imágenes meteorológicas.
2. **Iridium pager** (1626 MHz) → mensajes de sat‑phones.
3. **AIS** (162 MHz) → tráfico marítimo.

***

### 7. Conecta y comparte

¿Te interesa la **ciberseguridad aeroespacial**? Sígueme y comparte tu progreso:

* YouTube -> [Tuch0\_](https://www.youtube.com/@tuch0_)
* Instagram → [@tuch0\_](https://www.instagram.com/tuch0_/)
* LinkedIn → [tuch0](https://www.linkedin.com/in/tuch0/)
* GitHub → [tuch0](https://github.com/Tuch0)

Construye tu ciberdeck, publícalo con `#SpaceCyberdeck` y aprendamos juntos.
