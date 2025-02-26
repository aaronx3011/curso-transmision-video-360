# Reproduciendo un video local
En esta clase el objetivo principal es reproducir un video local que cumpla con los requerimientos expuestos en el archivo **README.md**

## Contenidos

### 1. Conceptos importantes

- **Contenerdor**
    *Un contenedor de video es un formato de archivo diseñado para almacenar y organizar múltiples flujos de datos multimedia, como vídeo, audio, subtítulos y metadatos. Como su nombre lo indica contiene estos datos individuales en una única estructura -Que normalmente conocemos como formato de video (AVI, MOV, MP4, etc…)-.*
    *Permitiendo así enviar o recibir lo que el usuario concibe como video, no solo el contenido visual, si no también el audio, los subtítulos, entre otros.*

- **Demuxer**
    *El trabajo de los demuxers es separar los contenedores en los flujos de datos multimedia correspondientes para posteriormente ser procesados en caso de ser necesario.*


- **[Codec](https://www.dacast.com/es/blog-es/que-es-un-codec-de-video/)**

    *El codec es un algoritmo que se utiliza para comprimir y descomprimir archivos de video. Los codecs son esenciales para reducir el tamaño de los archivos de video, lo que facilita su almacenamiento, transmisión y reproducción. La compresión de video implica eliminar información redundante o menos perceptible del video original, lo que reduce su tamaño sin afectar significativamente la calidad visual. Al reproducir un video, el codec realiza el proceso inverso, descomprimiendo el archivo para que pueda ser visualizado. Existen diferentes tipos de codecs, cada uno con sus propias características en cuanto a calidad de imagen, eficiencia de compresión y complejidad computacional. Los codecs mas populares son [h.264](https://www.dacast.com/es/blog-es/que-es-un-codec-de-video/) y [h.265 (HEVC)](https://eems.mit.edu/wp-content/uploads/2014/06/H.265-HEVC-Tutorial-2014-ISCAS.pdf)* 


### 2. Reproducción del video

La idea es reproducir un video que se encuentre descargado localmente en nuestro equipo donde vamos a realizar las pruebas.
En este caso nuestro video tiene estas características.

``` bash
    Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'dives.mp4':=    0B f=0/0   
      Metadata:
        major_brand     : mp42
        minor_version   : 0
        compatible_brands: isommp42
        creation_time   : 2024-07-30T03:00:13.000000Z
        encoder         : Google
      Duration: 00:06:37.57, start: 0.000000, bitrate: 366 kb/s
      Stream #0:0(und): Video: h264 (Main) (avc1 / 0x31637661), yuv420p(tv, bt709), 640x360 [SAR 1:1 DAR 16:9], 235 kb/s, 25 fps, 25 tbr, 12800 tbn, 50 tbc (default)
        Metadata:
          creation_time   : 2024-07-30T03:00:13.000000Z
          handler_name    : ISO Media file produced by Google Inc. Created on: 07/29/2024.
          vendor_id       : [0][0][0][0]
      Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 127 kb/s (default)
        Metadata:
          creation_time   : 2024-07-30T03:00:13.000000Z
          handler_name    : ISO Media file produced by Google Inc. Created on: 07/29/2024.
          vendor_id       : [0][0][0][0]

```
`dives.mp4` *corresponde al nombre del archivo. (Se puede colocar cualquier nombre, lo importante es que el programa lo pueda encontrar, para eso recomendamos usar el path absoluto)*
`mp4` *Corresponde al contenedor del video, que en este caso es mp4 (Si se desea utilizar otro es probable que los comandos de gstreamer cambien dependiendo de las características del video seleccionado)*
`h264 (Main)` *Corresponde al codec que se esta usando en este video (Al igual que el contenerdor en caso de cambiar el comando de gsteramer tambien se vera afectado)*

*Los demas datos no son de importancia en este momento pero es en un futuro si los usaremos*

Para reproducir los videos es necesario abrir una terminal en la caperta donde se encuentra y utilizar los siguientes comandos

#### FFMpeg

``` bash
    ffplay <path/al/video/nombre-del-archivo>
```

Ese comando nos abrira una nueva ventana en la cual se va a estar reproduciendo el video que seleccionamos en el comando.
Ademas veremos un resultado en nuestra terminal parecido al mostrado anteriormente.

```bash
    Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'dives.mp4':=    0B f=0/0   
      Metadata:
        major_brand     : mp42
        minor_version   : 0
        compatible_brands: isommp42
        creation_time   : 2024-07-30T03:00:13.000000Z
        encoder         : Google
      Duration: 00:06:37.57, start: 0.000000, bitrate: 366 kb/s
      Stream #0:0(und): Video: h264 (Main) (avc1 / 0x31637661), yuv420p(tv, bt709), 640x360 [SAR 1:1 DAR 16:9], 235 kb/s, 25 fps, 25 tbr, 12800 tbn, 50 tbc (default)
        Metadata:
          creation_time   : 2024-07-30T03:00:13.000000Z
          handler_name    : ISO Media file produced by Google Inc. Created on: 07/29/2024.
          vendor_id       : [0][0][0][0]
      Stream #0:1(und): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 127 kb/s (default)
        Metadata:
          creation_time   : 2024-07-30T03:00:13.000000Z
          handler_name    : ISO Media file produced by Google Inc. Created on: 07/29/2024.
          vendor_id       : [0][0][0][0]
```
    
#### GStreamer

A direfencia de FFMpeg en gsteramer es un poco mas complicado reproducir el video. *(Existen unas alternativas mas sencillas pero por fines educativos lo haremos con el siguiente comando)*

```bash
    gst-launch-1.0 filesrc location='<path/al/video/nombre-del-archivo>' ! qtdemux ! h264parse ! nvh264dec ! videoconvert ! autovideosink
```

Aca lo que estamos haciendo es:

1. `gst-launch-1.0`: Llamamos a gsteramer para poder usar sus funciones
2. `filesrc location='<path/al/video/nombre-del-archivo>'`: Indicamos que la fuente de este flujo es un archivo y se encuentra en la ubicacion "<path/al/video/nombre-del-archivo>"
3. `qtdemux`: Demuxeamos el video para poder obtener unicamente el video
4. `h264parse`: Ahora empezamos el proceso de descompresion
5. `nvh264dec`: Aca ya estamos descomprimiendo el video en fragmentos separados para poder reproducirlo utilizando autovideosink
6. `videoconvert`: Antes de poder reproducirlo vamos a usar este conversor, para que una vez que tengamos una salida en formato RAW del decoder, podamos transformarlo en lo que el reproductor necesita
7. `autovideosink`: Este es el paso final que nos permite reproducir el video

Ese comando nos abrira una nueva ventana en la cual se va a estar reproduciendo el video que seleccionamos en el comando.
Ademas veremos un resultado en nuestra terminal parecido al siguiente.


```bash
    Setting pipeline to PAUSED ...
    Pipeline is PREROLLING ...
    Got context from element 'nvh264dec0': gst.cuda.context=context, gst.cuda.context=(GstCudaContext)"\(GstCudaContext\)\ cudacontext0", cuda-device-id=(int)0;
    Got context from element 'nvh264dec0': gst.gl.GLDisplay=context, gst.gl.GLDisplay=(GstGLDisplay)"\(GstGLDisplayX11\)\ gldisplayx11-0";
    Redistribute latency...
    Pipeline is PREROLLED ...
    Setting pipeline to PLAYING ...
    Redistribute latency...
    New clock: GstSystemClock
    ERROR: from element /GstPipeline:pipeline0/GstAutoVideoSink:autovideosink0/GstXvImageSink:autovideosink0-actual-sink-xvimage: Output window was closed
    Additional debug info:
    ../sys/xvimage/xvimagesink.c(568): gst_xv_image_sink_handle_xevents (): /GstPipeline:pipeline0/GstAutoVideoSink:autovideosink0/GstXvImageSink:autovideosink0-actual-sink-xvimage
    Execution ended after 0:00:03.136905297
    Setting pipeline to NULL ...
    ERROR: from element /GstPipeline:pipeline0/GstQTDemux:qtdemux0: Internal data stream error.
    Additional debug info:
    ../gst/isomp4/qtdemux.c(6760): gst_qtdemux_loop (): /GstPipeline:pipeline0/GstQTDemux:qtdemux0:
    streaming stopped, reason error (-5)
    Freeing pipeline ...
```

#

*Si tu video tiene audio es probable que en el primer comando logres escuchar el video pero en el segundo no, esto tiene que ver con que lo demuxeamos, es decir, separamos el audio, los subtitulos, los frames, entre otros, en flujos multimedia separados, y al reproductor solo le estamos enviando el flujo multimedia correspondiente a los frames*
