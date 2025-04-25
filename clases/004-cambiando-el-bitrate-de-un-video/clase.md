# Cambiando el codec de un video

La idea de esta clase es cambiar el bitrate de un video. Con el objetivo de evidenciar la importancia del bitrate en la calidad percibida del video final
Para llevar a cabo los ejercicios de esta clase requerimos de un video local que cumpla con las características expuestas en el archivo **README.md**


## Contenidos

### 1. Conceptos 

- **Bitrate**
    El bitrate es la cantidad de información digital que se transmite por unidad de tiempo. Normalmente se mide en bits por segundo (bps) o megabits por segundo (Mbps)
    El bitrate es un factor clave para determinar la calidad de la imagen y el sonido. Un bitrate más alto suele ofrecer una mejor calidad, pero el archivo será más grande
    El bitrate se ve afectado por el tamanho de los frames, la densidad del color, la cantidad de frames por segundo, el codec, entre otros


### 2. Cambio de bitrate

A continuacion estaremos haciendo cambio de bitrate de un video. Con el objetivo de evidenciar la importancia del bitrate en la calidad percibida del video final
Para esto estaremos usando un video con las siguientes características

``` bash
    Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'video.mp4':=    0B f=0/0   
      Metadata:
        major_brand     : isom
        minor_version   : 512
        compatible_brands: isomiso2avc1mp41
        encoder         : Lavf58.19.102
      Duration: 00:02:00.14, start: 0.000000, bitrate: 1614 kb/s
      Stream #0:0[0x1](und): Video: h264 (High) (avc1 / 0x31637661), yuv420p(tv, bt709, progressive), 1920x800 [SAR 1:1 DAR 12:5], 1480 kb/s, 24 fps, 24 tbr, 12288 tbn (default)
        Metadata:
          handler_name    : ISO Media file produced by Google Inc.
          vendor_id       : [0][0][0][0]
      Stream #0:1[0x2](eng): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 127 kb/s (default)
        Metadata:
          handler_name    : ISO Media file produced by Google Inc.
          vendor_id       : [0][0][0][0]
```

`video.mp4` *corresponde al nombre del archivo. (Se puede colocar cualquier nombre, lo importante es que el programa lo pueda encontrar, para eso recomendamos usar el path absoluto)*

`mp4` *Corresponde al contenedor del video, que en este caso es mp4 (Si se desea utilizar otro es probable que los comandos de gstreamer cambien dependiendo de las características del video seleccionado)*

`h264 (High)` *Corresponde al codec que se esta usando en este video (Al igual que el contenedor en caso de cambiar el comando de gsteramer tambien se vera afectado)*

*Los demás datos no son de importancia en este momento pero es en un futuro si los usaremos*

Para convertir el video es necesario abrir una terminal en la caperta donde se encuentra y utilizar los siguientes comandos

#### FFMpeg

``` bash
    ffmpeg -i <path/al/video/nombre-del-archivo-mp4> -b:v <cantidad-de-birate><unidad-de-medida> <path/al/video/nombre-del-archivo-mp4>
```

Con este comando lo que estamos haciendo es:

1. `ffmpeg`: Llamamos a FFMpeg para poder usar sus funciones
2. `-i`: Este flag indica que a continuacion vamos a recibir un **Input**
3. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde se encuentra el archivo que estamos marcando como input
4. `-b:v`: Este flag esta segmentado en dos secciones importantes, la primera es el `-b` que nos indica que vamos a alterar el bitrate de un flujo multimedia, la siguiente `:v` nos indica que este va a afectar unicamente al video
5. `<cantidad-de-birate>`: Debemos especificar la cantidad que querramos colocar se especifica con numeros enteros positivos, ejemplo, 10
6. `<unidad-de-medida>`: Debemos especificar la unidad de medida que querramos utilizar lo más comun es usar megabits o kilobits, ejemplo, M o K
5. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde vamos a guardar el archivo que estamos generando *Esto tambien se puede denominar como output*

Asi empezamos el proceso de cambio de codec, seguido, veremos un proceso en nuestra terminal parecido al siguiente *(Este proceso puede demorar un poco, dependiendo de la resolucion del video, la duracion del mismo, entre otros muchos factores)*

```bash
    ffmpeg version 6.1.1-3ubuntu5 Copyright (c) 2000-2023 the FFmpeg developers
      built with gcc 13 (Ubuntu 13.2.0-23ubuntu3)
      configuration: --prefix=/usr --extra-version=3ubuntu5 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --disable-omx --enable-gnutls --enable-libaom --enable-libass --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libdav1d --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libglslang --enable-libgme --enable-libgsm --enable-libharfbuzz --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzimg --enable-openal --enable-opencl --enable-opengl --disable-sndio --enable-libvpl --disable-libmfx --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r --enable-ladspa --enable-libbluray --enable-libjack --enable-libpulse --enable-librabbitmq --enable-librist --enable-libsrt --enable-libssh --enable-libsvtav1 --enable-libx264 --enable-libzmq --enable-libzvbi --enable-lv2 --enable-sdl2 --enable-libplacebo --enable-librav1e --enable-pocketsphinx --enable-librsvg --enable-libjxl --enable-shared
      libavutil      58. 29.100 / 58. 29.100
      libavcodec     60. 31.102 / 60. 31.102
      libavformat    60. 16.100 / 60. 16.100
      libavdevice    60.  3.100 / 60.  3.100
      libavfilter     9. 12.100 /  9. 12.100
      libswscale      7.  5.100 /  7.  5.100
      libswresample   4. 12.100 /  4. 12.100
      libpostproc    57.  3.100 / 57.  3.100
    Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'video.mp4':
      Metadata:
        major_brand     : isom
        minor_version   : 512
        compatible_brands: isomiso2avc1mp41
        encoder         : Lavf58.19.102
      Duration: 00:02:00.14, start: 0.000000, bitrate: 1614 kb/s
      Stream #0:0[0x1](und): Video: h264 (High) (avc1 / 0x31637661), yuv420p(tv, bt709, progressive), 1920x800 [SAR 1:1 DAR 12:5], 1480 kb/s, 24 fps, 24 tbr, 12288 tbn (default)
        Metadata:
          handler_name    : ISO Media file produced by Google Inc.
          vendor_id       : [0][0][0][0]
      Stream #0:1[0x2](eng): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 127 kb/s (default)
        Metadata:
          handler_name    : ISO Media file produced by Google Inc.
          vendor_id       : [0][0][0][0]
    Stream mapping:
      Stream #0:0 -> #0:0 (h264 (native) -> h264 (libx264))
      Stream #0:1 -> #0:1 (aac (native) -> vorbis (libvorbis))
    Press [q] to stop, [?] for help
    [libx264 @ 0x600774a62740] using SAR=1/1
    [libx264 @ 0x600774a62740] using cpu capabilities: MMX2 SSE2Fast SSSE3 SSE4.2 AVX FMA3 BMI2 AVX2
    [libx264 @ 0x600774a62740] profile High, level 4.0, 4:2:0, 8-bit
    [libx264 @ 0x600774a62740] 264 - core 164 r3108 31e19f9 - H.264/MPEG-4 AVC codec - Copyleft 2003-2023 - http://www.videolan.org/x264.html - options: cabac=1 ref=3 deblock=1:0:0 analyse=0x3:0x113 me=hex subme=7 psy=1 psy_rd=1.00:0.00 mixed_ref=1 me_range=16 chroma_me=1 trellis=1 8x8dct=1 cqm=0 deadzone=21,11 fast_pskip=1 chroma_qp_offset=-2 threads=12 lookahead_threads=2 sliced_threads=0 nr=0 decimate=1 interlaced=0 bluray_compat=0 constrained_intra=0 bframes=3 b_pyramid=2 b_adapt=1 b_bias=0 direct=1 weightb=1 open_gop=0 weightp=2 keyint=250 keyint_min=24 scenecut=40 intra_refresh=0 rc_lookahead=40 rc=crf mbtree=1 crf=23.0 qcomp=0.60 qpmin=0 qpmax=69 qpstep=4 ip_ratio=1.40 aq=1:1.00
    Output #0, matroska, to 'video.mkv':
      Metadata:
        major_brand     : isom
        minor_version   : 512
        compatible_brands: isomiso2avc1mp41
        encoder         : Lavf60.16.100
      Stream #0:0(und): Video: h264 (H264 / 0x34363248), yuv420p(tv, bt709, progressive), 1920x800 [SAR 1:1 DAR 12:5], q=2-31, 24 fps, 1k tbn (default)
        Metadata:
          handler_name    : ISO Media file produced by Google Inc.
          vendor_id       : [0][0][0][0]
          encoder         : Lavc60.31.102 libx264
        Side data:
          cpb: bitrate max/min/avg: 0/0/0 buffer size: 0 vbv_delay: N/A
      Stream #0:1(eng): Audio: vorbis (oV[0][0] / 0x566F), 44100 Hz, stereo, fltp (default)
        Metadata:
          handler_name    : ISO Media file produced by Google Inc.
          vendor_id       : [0][0][0][0]
          encoder         : Lavc60.31.102 libvorbis
    [out#0/matroska @ 0x600774a96980] video:27056kB audio:1446kB subtitle:0kB other streams:0kB global headers:4kB muxing overhead: 0.231403%
    frame= 2882 fps= 35 q=-1.0 Lsize=   28568kB time=00:02:00.13 bitrate=1948.0kbits/s speed=1.47x    
    [libx264 @ 0x600774a62740] frame I:86    Avg QP:17.00  size: 26884
    [libx264 @ 0x600774a62740] frame P:1261  Avg QP:20.40  size: 12953
    [libx264 @ 0x600774a62740] frame B:1535  Avg QP:21.00  size:  5902
    [libx264 @ 0x600774a62740] consecutive B-frames: 15.2% 31.4% 29.7% 23.7%
    [libx264 @ 0x600774a62740] mb I  I16..4: 27.5% 68.9%  3.6%
    [libx264 @ 0x600774a62740] mb P  I16..4: 11.5% 27.6%  0.3%  P16..4: 24.1%  5.1%  1.1%  0.0%  0.0%    skip:30.3%
    [libx264 @ 0x600774a62740] mb B  I16..4:  2.5%  4.2%  0.0%  B16..8: 29.7%  3.0%  0.2%  direct: 1.4%  skip:59.0%  L0:44.9% L1:51.9% BI: 3.1%
    [libx264 @ 0x600774a62740] 8x8 transform intra:68.9% inter:90.1%
    [libx264 @ 0x600774a62740] coded y,uvDC,uvAC intra: 20.5% 23.4% 2.6% inter: 5.6% 6.3% 0.2%
    [libx264 @ 0x600774a62740] i16 v,h,dc,p: 18% 45% 10% 27%
    [libx264 @ 0x600774a62740] i8 v,h,dc,ddl,ddr,vr,hd,vl,hu: 29% 32% 26%  2%  2%  2%  4%  1%  3%
    [libx264 @ 0x600774a62740] i4 v,h,dc,ddl,ddr,vr,hd,vl,hu: 21% 41% 13%  3%  5%  4%  6%  3%  4%
    [libx264 @ 0x600774a62740] i8c dc,h,v,p: 61% 27% 10%  2%
    [libx264 @ 0x600774a62740] Weighted P-Frames: Y:8.1% UV:3.4%
    [libx264 @ 0x600774a62740] ref P L0: 68.7% 14.4% 11.3%  5.4%  0.2%
    [libx264 @ 0x600774a62740] ref B L0: 83.5% 14.6%  1.9%
    [libx264 @ 0x600774a62740] ref B L1: 99.0%  1.0%
    [libx264 @ 0x600774a62740] kb/s:1845.70
```
    
#### GStreamer

A direfencia de FFMpeg en GStreamer es un poco más complicado cambiar el bitrate del video. *(Existen unas alternativas más sencillas pero con fines educativos lo haremos con el siguiente comando)*

```bash
    gst-launch-1.0 filesrc location='<path/al/video/nombre-del-archivo-mp4>' ! qtdemux ! h264parse ! nvh264dec ! nvh264enc bitrate=<cantidad-de-birate> ! h264parse ! qtmux ! filesink location='<path/al/video/nombre-del-archivo-mp4>'
```

Con este comando lo que estamos haciendo es:

1. `gst-launch-1.0`: Llamamos a GStreamer para poder usar sus funciones
2. `filesrc location='<path/al/video/nombre-del-archivo-mp4>'`: Indicamos que la fuente de este flujo, en este caso es un archivo y se encuentra en la ubicacion "<path/al/video/nombre-del-archivo-mp4>"
3. `qtdemux`: Demuxeamos el video para poder obtener unicamente el flujo multimedia correspondiente al video
4. `h264parse`: Ahora empezamos el proceso de descompresion
5. `nvh264dec`: Aca ya estamos descomprimiendo el video en fragmentos separados
5. `nvh264enc`: Aca estamos comprimiendo el video para poder almacenarlo en el contenedor deseado, sin embargo en esta ocasion, le vamos a agregar el bitrate que deseamos al proceso de codificacion, usando el parametro bitrate, el cual recibe numeros enteros positivos, ejemplo, 1000
7. `h264parse`: Ahora empezamos el proceso de "parseo" (analisis u ordenamiento)
8. `qtmux`: Muxeamos el video para poder empaquetarlo en el contenedor deseado
9. `filesink location='<path/al/video/nombre-del-archivo-mp4>'`: Indicamos que la salida de este flujo es un archivo y se encuentra en la ubicacion "<path/al/video/nombre-del-archivo-mp4>"

Veremos un proceso en nuestra terminal parecido al siguiente *(Este proceso puede demorar un poco, dependiendo de la resolucion del video, la duracion del mismo, entre otros muchos factores)*


```bash
    Setting pipeline to PAUSED ...
    Pipeline is PREROLLING ...
    Got context from element 'nvh264enc0': gst.cuda.context=context, gst.cuda.context=(GstCudaContext)"\(GstCudaContext\)\ cudacontext1", cuda-device-id=(uint)0;
    Got context from element 'nvh264enc0': gst.gl.GLDisplay=context, gst.gl.GLDisplay=(GstGLDisplay)"\(GstGLDisplayX11\)\ gldisplayx11-0";
    Redistribute latency...
    Redistribute latency...
    Redistribute latency...
    Redistribute latency...
    Redistribute latency...
    Pipeline is PREROLLED ...
    Setting pipeline to PLAYING ...
    Redistribute latency...
    New clock: GstSystemClock
    Redistribute latency...
    Got EOS from element "pipeline0".
    Execution ended after 0:00:03.987873839
    Setting pipeline to NULL ...
    Freeing pipeline ...
```

## Detalles importantes
1. Tamaño del archivo:
    Si nos fijamos en el resultado de los comandos que ejecutamos, nos devuelven un video. Este archivo de video tiene un peso diferente al original, y este va a variar dependiendo de la cantidad de bitrate que le coloquemos

#

*Si tu video tiene audio es probable que en el primer comando logres escuchar el video pero en el segundo no, esto tiene que ver con que lo demuxeamos, es decir, separamos el audio, los subtitulos, los frames, entre otros, en flujos multimedia separados, y al nuevo video solo le estamos enviando el flujo multimedia correspondiente a los frames*
