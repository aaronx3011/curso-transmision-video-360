# Filter_complex y Map (FFMpeg)

La idea de esta clase es introducir dos opciones muy potentes y flexibles de FFmpeg: `-filter_complex` y `-map`.
Estas herramientas nos permiten realizar operaciones complejas que involucran múltiples flujos (streams) de entrada y/o salida, como superponer imágenes, combinar audio, crear efectos de picture-in-picture, y mucho más. Comprender el funcionamiento del comando `-filter_complex` nos va a permitir realizar operaciones muy avanzadas.


## Contenidos

### 1. Conceptos 

- **Stream (Flujo)**

    Como vimos antes, un archivo multimedia (como un MP4) es un contenedor que puede tener varios flujos de datos: normalmente un flujo de video, uno o más flujos de audio, y a veces flujos de subtítulos o metadatos. FFmpeg identifica estos flujos con índices (ej: 0:0 para el primer flujo del primer input, 0:1 para el segundo flujo del primer input, 1:0 para el primer flujo del segundo input, etc.).


- **Filtergraph**

    Es una cadena o red de filtros que procesan los flujos multimedia. Un filtro toma uno o más flujos de entrada, realiza una operación (cambiar tamaño, superponer, ajustar color, etc.) y produce uno o más flujos de salida.

- **Map**
    Esta función especifica exactamente qué flujos deben incluirse en el archivo de salida y en qué orden. Es crucial cuando se usa -filter_complex, ya que los flujos de salida no se incluyen automáticamente en el output final; deben ser "mapeados" explícitamente. 

- **Hilos (Threads)**
    FFmpeg es una herramienta multihilo. Esto significa que puede realizar varias tareas en paralelo para acelerar el procesamiento, siempre que tengas un CPU con múltiples núcleos. Puede usar hilos separados para:

    - Leer y demuxear los archivos de entrada.
    - Decodificar diferentes flujos (video, audio).
    - Ejecutar ciertos filtros (algunos filtros están diseñados para usar múltiples hilos).
    - Codificar los flujos de salida.
    - Escribir el archivo de salida. El uso eficiente de hilos es clave para el rendimiento, especialmente con filter_complex.

### 2. Mapeo de audio y video

A continuación realizaremos el mapeo de un adio con un video, el objetivo es tener dos inputs de video diferentes y que en cada uno se genere el mismo audio asi mantendremos un video con el audio original y otro con el audio nuevo, el cual corresponde al primer video.
Para esto estaremos usando un video con las siguientes características

``` bash
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'video.mp4':=    0B
  Metadata:
    major_brand     : isom
    minor_version   : 512
    compatible_brands: isomiso2avc1mp41
    title           : kudasaibeats - the girl i haven't met
    artist          : Ikigai
    encoder         : Lavf61.7.100
  Duration: 00:03:15.15, start: 0.000000, bitrate: 1027 kb/s
  Stream #0:0[0x1](und): Video: h264 (High) (avc1 / 0x31637661), yuv420p(tv, bt709, progressive), 1280x720 [SAR 1:1 DAR 16:9], 889 kb/s, 29.97 fps, 29.97 tbr, 30k tbn (default)
      Metadata:
        handler_name    : ISO Media file produced by Google Inc.
        vendor_id       : [0][0][0][0]
        encoder         : Lavc61.19.100 libx264
  Stream #0:1[0x2](eng): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 129 kb/s (default)
      Metadata:
        handler_name    : ISO Media file produced by Google Inc.
        vendor_id       : [0][0][0][0]
```

``` bash
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'video.mp4':=    0B
  Metadata:
    major_brand     : isom
    minor_version   : 512
    compatible_brands: isomiso2avc1mp41
    title           : kudasaibeats - Dream of her
    artist          : Ikigai
    encoder         : Lavf61.7.100
  Duration: 00:02:15.00, start: 0.000000, bitrate: 1027 kb/s
  Stream #0:0[0x1](und): Video: h264 (High) (avc1 / 0x31637661), yuv420p(tv, bt709, progressive), 1280x720 [SAR 1:1 DAR 16:9], 889 kb/s, 29.97 fps, 29.97 tbr, 30k tbn (default)
      Metadata:
        handler_name    : ISO Media file produced by Google Inc.
        vendor_id       : [0][0][0][0]
        encoder         : Lavc61.19.100 libx264
  Stream #0:1[0x2](eng): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 129 kb/s (default)
      Metadata:
        handler_name    : ISO Media file produced by Google Inc.
        vendor_id       : [0][0][0][0]
```

`video.mp4` *corresponde al nombre del archivo. (Se puede colocar cualquier nombre, lo importante es que el programa lo pueda encontrar, para eso recomendamos usar el path absoluto)*

`mp4` *Corresponde al contenedor del video, que en este caso es mp4 (Si se desea utilizar otro es probable que los comandos de gstreamer cambien dependiendo de las características del video seleccionado)*

`h264 (High)` *Corresponde al codec que se esta usando en este video (Al igual que el contenedor en caso de cambiar el comando de gsteramer tambien se vera afectado)*

**En este caso son dos videos musicales y vamos a mantener solo la musica de uno en los dos videos**

*Los demás datos no son de importancia en este momento pero es en un futuro si los usaremos*

Para convertir el video es necesario abrir una terminal en la caperta donde se encuentra y utilizar los siguientes comandos

#### FFMpeg

``` bash
    ffmpeg -i <path/al/video1/nombre-del-archivo-mp4> -i <path/al/video1/nombre-del-archivo-mp4> -filter_complex "[0:v]copy[video1];[1:v]copy[video2];" -map "[video1]" <path/al/output1/nombre-del-archivo-mp4> -map "[video2]" -map 0:a <path/al/output2/nombre-del-archivo-mp4>
```

Con este comando lo que estamos haciendo es:

1. `ffmpeg`: Llamamos a FFMpeg para poder usar sus funciones
2. `-i`: Este flag indica que a continuación vamos a recibir un **Input**
3. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde se encuentra el archivo que estamos marcando como input
4. `-i`: Este flag indica que a continuación vamos a recibir un **Input**
5. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde se encuentra el archivo que estamos marcando como input
6. `-filter_complex`: Empezamos a utilizar los filtros en nuestros streams multimedia, en este caso solo usaremos copy 
7. `-map "[video1]"`: Aca estamos mapeando el resultado del filter_complex [video1]
8. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde vamos a guardar el archivo que estamos generando *Esto tambien se puede denominar como output*
9. `-map "[video2]"`: Aca estamos mapeando el resultado del filter_complex [video2]
10. `-map 0:a`: Este paso es importante porque es donde realmente estamos redirigiendo los datos de un stream a otro, es importante aclarar que hay maneras mas faciles de hacerlo pero con fines didacticos los estamos haciendo con de esta manera
11. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde vamos a guardar el archivo que estamos generando *Esto tambien se puede denominar como output*

Asi empezamos el proceso, veremos que es un proceso mas largo que el de costumbre, pero lo mas importante de todo el output que recibimos en consola es lo siguiente

```bash
Stream mapping:
  Stream #0:0 (h264) -> copy:default
  Stream #1:0 (h264) -> copy:default
  copy:default -> Stream #0:0 (libx264)
  copy:default -> Stream #1:0 (libx264)
  Stream #0:1 -> #1:1 (aac (native) -> aac (native))
```

*El stream mapping nos mustra de donde a donde van nuestros streams, si nos damos cuenta en la ultima linea vemos como los audios se estan conectando y se le esta  colocando el audio del estream "0:1" al "1:1"*

