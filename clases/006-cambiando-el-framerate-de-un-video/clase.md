# Cambiando el framerate de un video

La idea de esta clase es cambiar el framerate de un video. Adicionalmente vamos a aprender como podemos convertir videos en una secuencia de images
*Separa un video en una secuencia de imagenes nos va a ayudar en un futuro a "debuggear" o analizar los videos que estemos trabajando en busca de posibles fallas*
Para llevar a cabo los ejercicios de esta clase requerimos de un video local que cumpla con las características expuestas en el archivo **README.md**


## Contenidos

### 1. Conceptos 

- **Framerate (Cuadros por Segundo - FPS)**

    El framerate, también conocido como cuadros por segundo (FPS), se refiere a la frecuencia con la que aparecen imágenes fijas consecutivas (llamadas "cuadros" o "frames") en una pantalla durante un segundo de video. Se mide en cuadros por segundo (fps). El estandar de TV o plataformas de streaming 
    El framerate afecta directamente la suavidad del movimiento que percibimos en un video.


- **Secuencia de Imágenes**

    Una secuencia de imágenes es una serie de fotografías o imágenes fijas dispuestas en un orden específico para crear la ilusión de movimiento cuando se visualizan rápidamente una tras otra.


### 2. Cambio de framerate

A continuación realizaremos el cambio de framerate de un video.
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

`video.mp4` *corresponde al nombre del archivo. (Se puede colocar cualquier nombre, lo importante es que el programa lo pueda encontrar, para eso recomendamos usar el path absoluto)*

`mp4` *Corresponde al contenedor del video, que en este caso es mp4 (Si se desea utilizar otro es probable que los comandos de gstreamer cambien dependiendo de las características del video seleccionado)*

`h264 (High)` *Corresponde al codec que se esta usando en este video (Al igual que el contenedor en caso de cambiar el comando de gsteramer tambien se vera afectado)*

*Los demás datos no son de importancia en este momento pero es en un futuro si los usaremos*

Para convertir el video es necesario abrir una terminal en la caperta donde se encuentra y utilizar los siguientes comandos

#### FFMpeg

``` bash
    ffmpeg -i <path/al/video/nombre-del-archivo-mp4> -r <FRAMERATE> <path/al/video/nombre-del-archivo-mp4>
```

Con este comando lo que estamos haciendo es:

1. `ffmpeg`: Llamamos a FFMpeg para poder usar sus funciones
2. `-i`: Este flag indica que a continuación vamos a recibir un **Input**
3. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde se encuentra el archivo que estamos marcando como input
4. `-r`: Este flag le indica a FFMpeg que estamos a punto de declarar el framerate esperado para el output (Se mide en fps y espera un nunero entero, por ejemplo, 30)
5. `<framerate>`: Corresponde a la cantidad de cuadros por segundo que va a contener nuestro video, se declara con un numero entero, por ejemplo 30
5. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde vamos a guardar el archivo que estamos generando *Esto tambien se puede denominar como output*

Asi empezamos el proceso de cambio de framerate, seguido, veremos un proceso en nuestra terminal parecido al siguiente *(Este proceso puede demorar un poco, dependiendo de la resolución del video, la duración del mismo, entre otros muchos factores)*

```bash
ffmpeg version n7.1 Copyright (c) 2000-2024 the FFmpeg developers
built with gcc 14.2.1 (GCC) 20250207
configuration: --prefix=/usr --disable-debug --disable-static --disable-stripping --enable-amf --enable-avisynth --enable-cuda-llvm --enable-lto --enable-fontconfig --enable-frei0r --enable-gmp --enable-gnutls --enable-gpl --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libdav1d --enable-libdrm --enable-libdvdnav --enable-libdvdread --enable-libfreetype --enable-libfribidi --enable-libglslang --enable-libgsm --enable-libharfbuzz --enable-libiec61883 --enable-libjack --enable-libjxl --enable-libmodplug --enable-libmp3lame --enable-libopencore_amrnb --enable-libopencore_amrwb --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libplacebo --enable-libpulse --enable-librav1e --enable-librsvg --enable-librubberband --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libsrt --enable-libssh --enable-libsvtav1 --enable-libtheora --enable-libv4l2 --enable-libvidstab --enable-libvmaf --enable-libvorbis --enable-libvpl --enable-libvpx --enable-libwebp --enable-libx264 --enable-libx265 --enable-libxcb --enable-libxml2 --enable-libxvid --enable-libzimg --enable-libzmq --enable-nvdec --enable-nvenc --enable-opencl --enable-opengl --enable-shared --enable-vapoursynth --enable-version3 --enable-vulkan
    libavutil      59. 39.100 / 59. 39.100
    libavcodec     61. 19.100 / 61. 19.100
    libavformat    61.  7.100 / 61.  7.100
    libavdevice    61.  3.100 / 61.  3.100
    libavfilter    10.  4.100 / 10.  4.100
    libswscale      8.  3.100 /  8.  3.100
    libswresample   5.  3.100 /  5.  3.100
    libpostproc    58.  3.100 / 58.  3.100
    Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'video.mp4':
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
        File 'output.mp4' already exists. Overwrite? [y/N] Y
        Stream mapping:
        Stream #0:0 -> #0:0 (h264 (native) -> h264 (libx264))
        Stream #0:1 -> #0:1 (aac (native) -> aac (native))
        Press [q] to stop, [?] for help
        [libx264 @ 0x60cd50fc4280] using SAR=1/1
        [libx264 @ 0x60cd50fc4280] using cpu capabilities: MMX2 SSE2Fast SSSE3 SSE4.2 AVX FMA3 BMI2 AVX2
        [libx264 @ 0x60cd50fc4280] profile High, level 3.1, 4:2:0, 8-bit
        [libx264 @ 0x60cd50fc4280] 264 - core 164 r3108 31e19f9 - H.264/MPEG-4 AVC codec - Copyleft 2003-2023 - http://www.videolan.org/x264.html - options: cabac=1 ref=3 deblock=1:0:0 analyse=0x3:0x113 me=hex subme=7 psy=1 psy_rd=1.00:0.00 mixed_ref=1 me_range=16 chroma_me=1 trellis=1 8x8dct=1 cqm=0 deadzone=21,11 fast_pskip=1 chroma_qp_offset=-2 threads=12 lookahead_threads=2 sliced_threads=0 nr=0 decimate=1 interlaced=0 bluray_compat=0 constrained_intra=0 bframes=3 b_pyramid=2 b_adapt=1 b_bias=0 direct=1 weightb=1 open_gop=0 weightp=2 keyint=250 keyint_min=10 scenecut=40 intra_refresh=0 rc_lookahead=40 rc=crf mbtree=1 crf=23.0 qcomp=0.60 qpmin=0 qpmax=69 qpstep=4 ip_ratio=1.40 aq=1:1.00
        Output #0, mp4, to 'output.mp4':
        Metadata:
    major_brand     : isom
    minor_version   : 512
    compatible_brands: isomiso2avc1mp41
    title           : kudasaibeats - the girl i haven't met
    artist          : Ikigai
    encoder         : Lavf61.7.100
    Stream #0:0(und): Video: h264 (avc1 / 0x31637661), yuv420p(tv, bt709, progressive), 1280x720 [SAR 1:1 DAR 16:9], q=2-31, 10 fps, 10240 tbn (default)
Metadata:
    handler_name    : ISO Media file produced by Google Inc.
    vendor_id       : [0][0][0][0]
    encoder         : Lavc61.19.100 libx264
    Side data:
    cpb: bitrate max/min/avg: 0/0/0 buffer size: 0 vbv_delay: N/A
Stream #0:1(eng): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 128 kb/s (default)
    Metadata:
    handler_name    : ISO Media file produced by Google Inc.
    vendor_id       : [0][0][0][0]
    encoder         : Lavc61.19.100 aac
    [out#0/mp4 @ 0x60cd510552c0] video:19459KiB audio:3092KiB subtitle:0KiB other streams:0KiB global headers:0KiB muxing overhead: 0.327576%
    frame= 1953 fps= 41 q=-1.0 Lsize=   22625KiB time=00:03:15.10 bitrate= 950.0kbits/s dup=0 drop=3893 speed=4.14x
    [libx264 @ 0x60cd50fc4280] frame I:10    Avg QP:13.17  size: 16558
    [libx264 @ 0x60cd50fc4280] frame P:1820  Avg QP:19.27  size: 10313
    [libx264 @ 0x60cd50fc4280] frame B:123   Avg QP:18.61  size:  8046
    [libx264 @ 0x60cd50fc4280] consecutive B-frames: 88.1% 10.1%  0.9%  0.8%
    [libx264 @ 0x60cd50fc4280] mb I  I16..4: 43.3% 50.1%  6.6%
    [libx264 @ 0x60cd50fc4280] mb P  I16..4: 14.7% 35.9%  1.4%  P16..4: 13.1%  3.4%  0.8%  0.0%  0.0%    skip:30.7%
    [libx264 @ 0x60cd50fc4280] mb B  I16..4:  7.6% 13.7%  0.3%  B16..8: 19.3%  4.8%  0.6%  direct: 6.7%  skip:47.1%  L0:60.8% L1:33.0% BI: 6.3%
    [libx264 @ 0x60cd50fc4280] 8x8 transform intra:68.7% inter:84.9%
    [libx264 @ 0x60cd50fc4280] coded y,uvDC,uvAC intra: 27.8% 45.1% 3.0% inter: 9.5% 14.3% 0.1%
    [libx264 @ 0x60cd50fc4280] i16 v,h,dc,p: 19% 32%  8% 42%
    [libx264 @ 0x60cd50fc4280] i8 v,h,dc,ddl,ddr,vr,hd,vl,hu: 30% 28% 21%  2%  4%  4%  6%  3%  3%
    [libx264 @ 0x60cd50fc4280] i4 v,h,dc,ddl,ddr,vr,hd,vl,hu: 28% 26% 17%  3%  8%  6%  7%  3%  2%
    [libx264 @ 0x60cd50fc4280] i8c dc,h,v,p: 52% 27% 14%  7%
    [libx264 @ 0x60cd50fc4280] Weighted P-Frames: Y:1.4% UV:0.8%
    [libx264 @ 0x60cd50fc4280] ref P L0: 59.8%  8.8% 19.0% 12.4%  0.1%
    [libx264 @ 0x60cd50fc4280] ref B L0: 81.0% 18.5%  0.5%
    [libx264 @ 0x60cd50fc4280] ref B L1: 99.9%  0.1%
    [libx264 @ 0x60cd50fc4280] kb/s:816.21
    [aac @ 0x60cd510cbd80] Qavg: 583.800
```
    
#### GStreamer

A direfencia de FFMpeg en GStreamer es un poco más complicado cambiar el framerate del video. *(Existen unas alternativas más sencillas pero con fines educativos lo haremos con el siguiente comando)*

```bash
    gst-launch-1.0 filesrc location='<path/al/video/nombre-del-archivo-mp4>' ! qtdemux ! h264parse ! nvh264dec ! videorate ! video/x-raw,framerate=<FRAMERATE> ! nvh264enc ! h264parse ! qtmux ! filesink location='<path/al/video/nombre-del-archivo-mp4>'
```

Con este comando lo que estamos haciendo es:

1. `gst-launch-1.0`: Llamamos a GStreamer para poder usar sus funciones
2. `filesrc location='<path/al/video/nombre-del-archivo-mp4>'`: Indicamos que la fuente de este flujo, en este caso es un archivo y se encuentra en la ubicacion "<path/al/video/nombre-del-archivo-mp4>"
3. `qtdemux`: Demuxeamos el video para poder obtener unicamente el flujo multimedia correspondiente al video
4. `h264parse`: Ahora empezamos el proceso de descompresion
5. `nvh264dec`: Aca ya estamos descomprimiendo el video en fragmentos separados
6. `videorate`: Indicamos que vamos a cambiar el framerate del video
7. `video/x-raw,framerate=<FRAMERATE>`: Agregamos el framerate que vamos a utilizar, en manera de fraccion, por ejemplo, 30/1, esto es equivalente a 30 frames por casa segundo.
8. `nvh264enc`: Aca estamos comprimiendo el video para poder almacenarlo en el contenedor deseado
9. `h264parse`: Ahora empezamos el proceso de "parseo" (analisis u ordenamiento)
10. `qtmux`: Muxeamos el video para poder empaquetarlo en el contenedor deseado
11. `filesink location='<path/al/video/nombre-del-archivo-mp4>'`: Indicamos que la salida de este flujo es un archivo y se encuentra en la ubicacion "<path/al/video/nombre-del-archivo-mp4>"

Veremos un proceso en nuestra terminal parecido al siguiente *(Este proceso puede demorar un poco, dependiendo de la resolución  del video, la duracion del mismo, entre otros muchos factores)*


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
1. Framerate superiores al original:
    Cuando agregamos "frames" adicionales, es decir generamos un video con un framerate mas alto que el framerate original, vamos a repetir frames y muchas veces eso afectara nuestro bitrate, pero si estamos agregango frames que no existen, por defecto se van a repertir los frames que ya existen y nos puede generar alertas dentro del proceso de conversion del video

#

**Para generar una secuencia de imagenes  de un video, podemos usar el siguiente comando**

``` bash
    ffmpeg -i <path/al/video/nombre-del-archivo-mp4> <path/al/video/nombre-del-archivo-mp4><%05d><extension>
    # Ejemplo
    ffmpeg -i video.mp4 ./imagen%05d.png
```

#

*Si tu video tiene audio es probable que en el primer comando logres escuchar el video pero en el segundo no, esto tiene que ver con que lo demuxeamos, es decir, separamos el audio, los subtitulos, los frames, entre otros, en flujos multimedia separados, y al nuevo video solo le estamos enviando el flujo multimedia correspondiente a los frames*
