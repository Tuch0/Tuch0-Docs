# Guía definitiva de satélites de banda S

<figure><img src="../.gitbook/assets/Diseño sin título.jpg" alt=""><figcaption></figcaption></figure>

## Guía personal y completa sobre satélites en banda S

> ¿Qué es la banda S?\
> La banda S es un rango de frecuencias entre los 2 y 4 GHz. Puede sonar técnico, pero es más común de lo que imaginas: muchas misiones espaciales, desde satélites científicos hasta pequeños cubesats universitarios, usan esta banda para comunicarse con la Tierra.

***

### 1. ¿Por qué escribo esta guía?

Porque me apasiona el espacio y la radiofrecuencia, y creo que no hay nada más increíble que poder escuchar desde casa cómo se comunica un satélite en órbita. Lo que estás a punto de leer no es un texto técnico frío: es una guía escrita con entusiasmo, con intención de que tú también puedas sumarte a este fascinante mundo.

***

### 2. ¿Qué tiene de especial la banda S?

Esta banda tiene una magia especial: es resistente a la lluvia y a la niebla (a diferencia de otras), tiene buena penetración atmosférica y lleva décadas funcionando como el canal principal de miles de misiones espaciales.

Por ejemplo, la NASA usó esta banda en el programa Apollo, y aún hoy sigue vigente en satélites de última generación. No es casualidad: es estable, segura y versátil.

> ¿Sabías que Artemis I también empezó transmitiendo datos por banda S?

***

### 3. Usos reales en satélites (y por qué importa)

La banda S no es solo "una frecuencia más". Aquí tienes ejemplos reales de cómo se usa:

* **Telemetría**: datos vitales sobre el estado del satélite (temperaturas, baterías, fallos... todo).
* **Control remoto**: comandos que se envían desde Tierra, como encender sensores o cambiar de órbita.
* **Datos científicos**: cámaras, sensores, espectrómetros… todo eso necesita enviar info.
* **Comunicación entre satélites**: sí, algunos se hablan entre ellos (increíble, ¿no?).

Y todo eso... pasa por la banda S.

***

### 4. Ejemplos concretos de satélites que la usan

Aquí van algunos que me parecen interesantes:

#### Científicos:

* **AQUA (NASA)** – Estudia el agua en la Tierra.
* **SMOS (ESA)** – Mide la humedad del suelo y la salinidad del océano.

#### Comunicaciones:

* **IRIDIUM** – Sus canales de control operan en banda S.
* **GlobalStar** – También usa esta banda para gestionar su red.

#### Universitarios:

* **Delfi-C3** – Un proyecto educativo de la Universidad de Delft.
* **AAUSAT-4** – Satélite danés que ayuda al monitoreo marítimo.

> Cada mes aparecen nuevos cubesats que emiten en banda S. Es un campo vivo, en constante cambio.

***

### 5. Cómo empezar a recibir señales desde casa

No necesitas una estación de la NASA para iniciarte. Con algo de ingenio y pocas herramientas puedes captar señales reales:

#### Qué necesitas (mínimo viable):

* **Un SDR** como el RTL-SDR Blog V4 (barato y muy capaz).
* **Una antena helicoidal** (puedes hacerla tú con alambre y PVC).
* **Un filtro de banda S** para limpiar la señal.
* **Software SDR++** (mi favorito) o GQRX para visualizar.
* **Orbitron o Gpredict** para saber cuándo pasa un satélite.

Con eso ya puedes empezar. Créeme, la primera vez que ves una señal real en pantalla… se siente mágico.

***

### 6. Decodificando señales sin morir en el intento

Vale, ya tienes la señal... ¿y ahora qué? Aquí va el proceso paso a paso:

1. Mira el pase del satélite (puedes usar TLEs).
2. Apunta bien la antena (esto es todo un arte).
3. Sintoniza la frecuencia (ejemplo: 2.2 GHz).
4. Observa la forma de onda en SDR++.
5. Usa GNURadio o SatDump para demodular.
6. Si todo va bien, verás datos reales o incluso imágenes.

> Algunas señales vienen en formato CCSDS, un estándar usado por agencias como ESA y NASA.

***

### 7. Proyectos caseros y cosas curiosas

Esto es lo que puedes hacer una vez que domines lo básico:

* **Recibir imágenes meteorológicas** de satélites en tiempo real.
* **Construir una antena helicoidal casera** y afinarla a 2.2 GHz.
* **Grabar y analizar tramas de cubesats**.

Todo esto suena complejo, pero poco a poco se aprende. Y hay mucha comunidad dispuesta a ayudar.

***

### 8. Aspectos legales y éticos a tener en cuenta

Aunque captar señales es legal en muchos países, hay límites:

* ✅ Puedes escuchar señales libres y educativas.
* ❌ No debes retransmitir señales cifradas o sensibles.
* ✅ Puedes compartir tus análisis técnicos (sin mostrar datos personales).

> &#x20;"Explorar está bien. Cruzar la línea, no."

***

### 9. Comunidad y recursos para seguir aprendiendo

* [SatNOGS](https://network.satnogs.org/): red de estaciones SDR global.
* [Hack-A-Sat](https://hackasat.com/): la competición que lo cambió todo.
* [Reddit /r/RTLSDR](https://reddit.com/r/RTLSDR): un lugar con ideas, tutoriales y respuestas.
* [SatDump](https://github.com/SatDump/SatDump): software para decodificar muchos satélites.

***

### 10. Cierre y próximos pasos

Si llegaste hasta aquí, te animo a que lo pruebes. No necesitas ser ingeniero aeroespacial, solo tener ganas de aprender y trastear un poco.

> &#x20;¿Y después?\
> Pronto publicaré una guía sobre cómo automatizar tu estación, cómo interpretar señales CCSDS, y cómo analizar redes satelitales reales.

Si te ha gustado esta guía, compártela. ¡Y si pruebas algo, escríbeme! Me encantará saber qué has captado 🚀
