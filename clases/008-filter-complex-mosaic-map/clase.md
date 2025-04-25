# Filter complex, Vstack y Hstack

La idea de esta clase es profundizar en las opciones `-filter_complex` y `-map`.
Para eso usaremos `vstack` y `hstack` al igual que filtros como `split`

## Contenidos

### 2. Mapeo de audio y video

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
    ffmpeg -i <path/al/video1/nombre-del-archivo-mp4> -filter_complex "[0:v]split=2[split1][split2];[split1][split2]vstack=inputs=2[split1y2]" -map "[split1y2]" -map 0:a output.mp4

```

Con este comando lo que estamos haciendo es:

1. `ffmpeg`: Llamamos a FFMpeg para poder usar sus funciones
2. `-i`: Este flag indica que a continuación vamos a recibir un **Input**
3. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde se encuentra el archivo que estamos marcando como input
6. `-filter_complex`: Empezamos a utilizar los filtros en nuestro streams multimedia
7. `split`: Con este filtro podemos dividir el stream inicial en la cantidad de streams que queramos en este caso estamos usando 2 streams para poder stackerlos de manera vertical usando vstack
8. `vstack`: Este filtro nos permite stackear dos inputs de manera vertical para generar un solo video
9. `-map "[split1y2]"`: Aca estamos mapeando el resultado del filter_complex [video2]
10. `-map 0:a`: Este paso es importante porque es donde realmente estamos redirigiendo los datos del stream de audio al nuevo video staceado
11. `<path/al/video/nombre-del-archivo-mp4>`: Indica donde vamos a guardar el archivo que estamos generando *Esto tambien se puede denominar como output*

Asi empezamos el proceso, veremos que es un proceso mas largo que el de costumbre, pero lo mas importante de todo el output que recibimos en consola es lo siguiente

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
Stream mapping:
  Stream #0:0 (h264) -> split:default
  vstack:default -> Stream #0:0 (libx264)
  Stream #0:1 -> #0:1 (aac (native) -> aac (native))
Press [q] to stop, [?] for help
[libx264 @ 0x58c027f4c1c0] using SAR=1/1
[libx264 @ 0x58c027f4c1c0] using cpu capabilities: MMX2 SSE2Fast SSSE3 SSE4.2 AVX FMA3 BMI2 AVX2
[libx264 @ 0x58c027f4c1c0] profile High, level 4.0, 4:2:0, 8-bit
[libx264 @ 0x58c027f4c1c0] 264 - core 164 r3108 31e19f9 - H.264/MPEG-4 AVC codec - Copyleft 2003-2023 - http://www.videolan.org/x264.html - options: cabac=1 ref=3 deblock=1:0:0 analyse=0x3:0x113 me=hex subme=7 psy=1 psy_rd=1.00:0.00 mixed_ref=1 me_range=16 chroma_me=1 trellis=1 8x8dct=1 cqm=0 deadzone=21,11 fast_pskip=1 chroma_qp_offset=-2 threads=12 lookahead_threads=2 sliced_threads=0 nr=0 decimate=1 interlaced=0 bluray_compat=0 constrained_intra=0 bframes=3 b_pyramid=2 b_adapt=1 b_bias=0 direct=1 weightb=1 open_gop=0 weightp=2 keyint=250 keyint_min=25 scenecut=40 intra_refresh=0 rc_lookahead=40 rc=crf mbtree=1 crf=23.0 qcomp=0.60 qpmin=0 qpmax=69 qpstep=4 ip_ratio=1.40 aq=1:1.00
Output #0, mp4, to 'output.mp4':
  Metadata:
    major_brand     : isom
    minor_version   : 512
    compatible_brands: isomiso2avc1mp41
    title           : kudasaibeats - the girl i haven't met
    artist          : Ikigai
    encoder         : Lavf61.7.100
  Stream #0:0: Video: h264 (avc1 / 0x31637661), yuv420p(tv, bt709/unknown/unknown, progressive), 1280x1440 [SAR 1:1 DAR 8:9], q=2-31, 29.97 fps, 30k tbn
      Metadata:
        encoder         : Lavc61.19.100 libx264
      Side data:
        cpb: bitrate max/min/avg: 0/0/0 buffer size: 0 vbv_delay: N/A
  Stream #0:1(eng): Audio: aac (LC) (mp4a / 0x6134706D), 44100 Hz, stereo, fltp, 128 kb/s (default)
      Metadata:
        handler_name    : ISO Media file produced by Google Inc.
        vendor_id       : [0][0][0][0]
        encoder         : Lavc61.19.100 aac
[out#0/mp4 @ 0x58c0280b2340] video:41885KiB audio:3092KiB subtitle:0KiB other streams:0KiB global headers:0KiB muxing overhead: 0.442977%
frame= 5846 fps= 35 q=-1.0 Lsize=   45176KiB time=00:03:15.02 bitrate=1897.6kbits/s speed=1.18x
[libx264 @ 0x58c027f4c1c0] frame I:24    Avg QP:17.28  size: 31659
[libx264 @ 0x58c027f4c1c0] frame P:2566  Avg QP:21.57  size: 13213
[libx264 @ 0x58c027f4c1c0] frame B:3256  Avg QP:18.71  size:  2526
[libx264 @ 0x58c027f4c1c0] consecutive B-frames: 10.9% 24.6% 59.6%  4.9%
[libx264 @ 0x58c027f4c1c0] mb I  I16..4: 32.0% 62.8%  5.2%
[libx264 @ 0x58c027f4c1c0] mb P  I16..4: 13.2% 28.0%  0.7%  P16..4: 13.3%  2.0%  0.4%  0.0%  0.0%    skip:42.3%
[libx264 @ 0x58c027f4c1c0] mb B  I16..4:  1.4%  1.9%  0.0%  B16..8:  9.8%  0.5%  0.0%  direct: 1.7%  skip:84.7%  L0:47.6% L1:46.7% BI: 5.7%
[libx264 @ 0x58c027f4c1c0] 8x8 transform intra:65.7% inter:92.5%
[libx264 @ 0x58c027f4c1c0] coded y,uvDC,uvAC intra: 19.0% 29.5% 1.3% inter: 1.9% 3.8% 0.0%
[libx264 @ 0x58c027f4c1c0] i16 v,h,dc,p: 18% 32%  9% 42%
[libx264 @ 0x58c027f4c1c0] i8 v,h,dc,ddl,ddr,vr,hd,vl,hu: 35% 27% 22%  2%  3%  3%  4%  2%  2%
[libx264 @ 0x58c027f4c1c0] i4 v,h,dc,ddl,ddr,vr,hd,vl,hu: 27% 25% 22%  3%  7%  5%  7%  3%  2%
[libx264 @ 0x58c027f4c1c0] i8c dc,h,v,p: 58% 24% 13%  5%
[libx264 @ 0x58c027f4c1c0] Weighted P-Frames: Y:1.4% UV:0.7%
[libx264 @ 0x58c027f4c1c0] ref P L0: 66.0% 10.1% 13.2% 10.6%  0.1%
[libx264 @ 0x58c027f4c1c0] ref B L0: 80.1% 17.3%  2.5%
[libx264 @ 0x58c027f4c1c0] ref B L1: 99.5%  0.5%
[libx264 @ 0x58c027f4c1c0] kb/s:1759.03
[aac @ 0x58c027f55e80] Qavg: 583.800
```
