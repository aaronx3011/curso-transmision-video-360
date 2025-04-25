# Cambiando el codec de un video

La idea de esta clase es cambiar el bitrate de un video. Con el objetivo de evidenciar la importancia del bitrate en la calidad percibida del video final
Para llevar a cabo los ejercicios de esta clase requerimos de un video local que cumpla con las características expuestas en el archivo **README.md**


## Contenidos

### 1. Conceptos 

- **Resolución**
    La resolución de un video se refiere a la cantidad de píxeles que tiene en ancho por alto, como 1920x1080 (Full HD) o 3840x2160 (4K), se suele asociar con la nitidez y la calidad de una imagen

### 2. Cambio de resolución

A continuación realizaremos el cambio de resolución de un video. Con el objetivo de apreciar la importancia de la resolución en la calidad percibida del video final, y el peso del mismo
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
    ffmpeg -i <path/al/video/nombre-del-archivo-mp4> -vf "scale=<width>:<height>" <path/al/video/nombre-del-archivo-mp4>
```

Con este comando lo que estamos haciendo es:

1. `ffmpeg`: Llamamos a FFMpeg para poder usar sus funciones
2. `-i`: Este flag indica que a continuación vamos a recibir un **Input**
3. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde se encuentra el archivo que estamos marcando como input
4. `-vf`: Este flag le indica a FFMpeg que estamos a puntod de usar un filtro en el video, en este caso vamos a usar un filtro llamado "scale" para poder rescalar el video
4. `scale`: Este filtro nos permite reescalar el video de manera sencilla.
5. `<width>`: Corresponde a la cantidad de pixeles horizontales que va a tener nuestro video una vez que pase por el filtro.
5. `<width>`: Corresponde a la cantidad de pixeles verticales que va a tener nuestro video una vez que pase por el filtro.
5. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde vamos a guardar el archivo que estamos generando *Esto tambien se puede denominar como output*

Asi empezamos el proceso de cambio de resolución, seguido, veremos un proceso en nuestra terminal parecido al siguiente *(Este proceso puede demorar un poco, dependiendo de la resolución del video, la duración del mismo, entre otros muchos factores)*

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
        minor_version   : 1
        compatible_brands: isomavc1
        creation_time   : 2014-10-21T20:59:15.000000Z
      Duration: 00:22:55.23, start: 0.000000, bitrate: 702 kb/s
      Stream #0:0[0x1](und): Video: h264 (High) (avc1 / 0x31637661), yuv420p(progressive), 1280x720, 651 kb/s, 23.98 fps, 23.98 tbr, 24k tbn (default)
          Metadata:
            creation_time   : 2014-10-21T20:59:15.000000Z
            handler_name    : Video
            vendor_id       : [0][0][0][0]
      Stream #0:1[0x2](eng): Audio: aac (HE-AAC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 48 kb/s (default)
          Metadata:
            creation_time   : 2014-10-21T20:59:18.000000Z
            handler_name    : GPAC ISO Audio Handler
            vendor_id       : [0][0][0][0]
    File 'video2.mp4' already exists. Overwrite? [y/N] Y
    Stream mapping:
      Stream #0:0 -> #0:0 (h264 (native) -> h264 (libx264))
      Stream #0:1 -> #0:1 (aac (native) -> aac (native))
    Press [q] to stop, [?] for help
    [libx264 @ 0x558fc313b0c0] using cpu capabilities: MMX2 SSE2Fast SSSE3 SSE4.2 AVX FMA3 BMI2 AVX2
    [libx264 @ 0x558fc313b0c0] profile High, level 1.2, 4:2:0, 8-bit
    [libx264 @ 0x558fc313b0c0] 264 - core 164 r3108 31e19f9 - H.264/MPEG-4 AVC codec - Copyleft 2003-2023 - http://www.videolan.org/x264.html - options: cabac=1 ref=3 deblock=1:0:0 analyse=0x3:0x113 me=hex subme=7 psy=1 psy_rd=1.00:0.00 mixed_ref=1 me_range=16 chroma_me=1 trellis=1 8x8dct=1 cqm=0 deadzone=21,11 fast_pskip=1 chroma_qp_offset=-2 threads=3 lookahead_threads=1 sliced_threads=0 nr=0 decimate=1 interlaced=0 bluray_compat=0 constrained_intra=0 bframes=3 b_pyramid=2 b_adapt=1 b_bias=0 direct=1 weightb=1 open_gop=0 weightp=2 keyint=250 keyint_min=23 scenecut=40 intra_refresh=0 rc_lookahead=40 rc=crf mbtree=1 crf=23.0 qcomp=0.60 qpmin=0 qpmax=69 qpstep=4 ip_ratio=1.40 aq=1:1.00
    Output #0, mp4, to 'video2.mp4':
      Metadata:
        major_brand     : isom
        minor_version   : 1
        compatible_brands: isomavc1
        encoder         : Lavf61.7.100
      Stream #0:0(und): Video: h264 (avc1 / 0x31637661), yuv420p(tv, progressive), 300x100, q=2-31, 23.98 fps, 24k tbn (default)
          Metadata:
            creation_time   : 2014-10-21T20:59:15.000000Z
            handler_name    : Video
            vendor_id       : [0][0][0][0]
            encoder         : Lavc61.19.100 libx264
          Side data:
            cpb: bitrate max/min/avg: 0/0/0 buffer size: 0 vbv_delay: N/A
      Stream #0:1(eng): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 128 kb/s (default)
          Metadata:
            creation_time   : 2014-10-21T20:59:18.000000Z
            handler_name    : GPAC ISO Audio Handler
            vendor_id       : [0][0][0][0]
            encoder         : Lavc61.19.100 aac
    [out#0/mp4 @ 0x558fc325ce40] video:17037KiB audio:21614KiB subtitle:0KiB other streams:0KiB global headers:0KiB muxing overhead: 2.316335%
    frame=32969 fps=383 q=-1.0 Lsize=   39547KiB time=00:22:54.99 bitrate= 235.6kbits/s speed=  16x
    [libx264 @ 0x558fc313b0c0] frame I:423   Avg QP:19.49  size:  6705
    [libx264 @ 0x558fc313b0c0] frame P:13077 Avg QP:23.13  size:   868
    [libx264 @ 0x558fc313b0c0] frame B:19469 Avg QP:28.13  size:   167
    [libx264 @ 0x558fc313b0c0] consecutive B-frames: 15.9% 13.8%  7.1% 63.2%
    [libx264 @ 0x558fc313b0c0] mb I  I16..4:  7.5% 30.0% 62.5%
    [libx264 @ 0x558fc313b0c0] mb P  I16..4:  0.7%  1.5%  2.4%  P16..4: 25.9% 12.2%  9.1%  0.0%  0.0%    skip:48.2%
    [libx264 @ 0x558fc313b0c0] mb B  I16..4:  0.1%  0.2%  0.4%  B16..8: 18.2%  3.1%  1.3%  direct: 1.1%  skip:75.6%  L0:44.0% L1:48.0% BI: 8.0%
    [libx264 @ 0x558fc313b0c0] 8x8 transform intra:30.6% inter:45.3%
    [libx264 @ 0x558fc313b0c0] coded y,uvDC,uvAC intra: 69.3% 87.0% 68.2% inter: 9.1% 9.6% 4.0%
    [libx264 @ 0x558fc313b0c0] i16 v,h,dc,p: 22% 47%  9% 22%
    [libx264 @ 0x558fc313b0c0] i8 v,h,dc,ddl,ddr,vr,hd,vl,hu: 16% 31% 20%  4%  4%  3%  7%  3% 10%
    [libx264 @ 0x558fc313b0c0] i4 v,h,dc,ddl,ddr,vr,hd,vl,hu: 28% 23% 14%  5%  6%  5%  8%  4%  8%
    [libx264 @ 0x558fc313b0c0] i8c dc,h,v,p: 43% 35% 13%  8%
    [libx264 @ 0x558fc313b0c0] Weighted P-Frames: Y:2.6% UV:1.8%
    [libx264 @ 0x558fc313b0c0] ref P L0: 66.4% 12.1% 11.9%  9.5%  0.2%
    [libx264 @ 0x558fc313b0c0] ref B L0: 82.3% 11.8%  5.9%
    [libx264 @ 0x558fc313b0c0] ref B L1: 94.7%  5.3%
    [libx264 @ 0x558fc313b0c0] kb/s:101.49
    [aac @ 0x558fc3447e40] Qavg: 1286.574
```
    
#### GStreamer

A direfencia de FFMpeg en GStreamer es un poco más complicado cambiar el bitrate del video. *(Existen unas alternativas más sencillas pero con fines educativos lo haremos con el siguiente comando)*

```bash
    gst-launch-1.0 filesrc location='<path/al/video/nombre-del-archivo-mp4>' ! qtdemux ! h264parse ! nvh264dec ! videoscale ! video/x-raw,width=<WIDTH>,height=<HEIGHT> ! nvh264enc ! h264parse ! qtmux ! filesink location='<path/al/video/nombre-del-archivo-mp4>'
```

Con este comando lo que estamos haciendo es:

1. `gst-launch-1.0`: Llamamos a GStreamer para poder usar sus funciones
2. `filesrc location='<path/al/video/nombre-del-archivo-mp4>'`: Indicamos que la fuente de este flujo, en este caso es un archivo y se encuentra en la ubicacion "<path/al/video/nombre-del-archivo-mp4>"
3. `qtdemux`: Demuxeamos el video para poder obtener unicamente el flujo multimedia correspondiente al video
4. `h264parse`: Ahora empezamos el proceso de descompresion
5. `nvh264dec`: Aca ya estamos descomprimiendo el video en fragmentos separados
6. `videoscale`: Indicamos que vamos a cambiar la escala del video
7. `video/x-raw,width=<WIDTH>,height=<HEIGHT>`: Agregamos la escala que queremos utilizar
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
1. Tamaño del archivo:
    Si nos fijamos en el resultado de los comandos que ejecutamos, nos devuelven un video. Este archivo de video tiene un peso diferente al original, y este va a variar dependiendo de la cantidad de bitrate que le coloquemos

#

*Si tu video tiene audio es probable que en el primer comando logres escuchar el video pero en el segundo no, esto tiene que ver con que lo demuxeamos, es decir, separamos el audio, los subtitulos, los frames, entre otros, en flujos multimedia separados, y al nuevo video solo le estamos enviando el flujo multimedia correspondiente a los frames*
