# Validacion de instalacion
En esta clase el objetivo principal es instalar los requerimientos que se encuentran en el archivo **README.md**

## Contenidos
### 1. GStreamer
*GStreamer es un framework multimedia libre y multiplataforma, escrito en el lenguaje de programación C, usando la biblioteca GObject.*
*GStreamer permite crear aplicaciones audiovisuales. La función del núcleo de GStreamer es proveer un framework para complementos, flujo de datos y manejo/negociación de distintos tipos de medios, además provee una API muy útil para escribir aplicaciones para el procesado de datos multimedia.*

Ahora lo que haremos es revisar que se encuentre instalado correctamente.
Para eso utilizaremos el siguiente comando.

```bash
gst-launch-1.0 --gst-version

```

El resultado debe ser algo parecido a esto **(Puede variar dependiendo de la versión utilizada)**

``` bash
GStreamer Core Library version 1.24.2

```

### 2. FFmpeg
*FFmpeg es una colección de software libre que puede grabar, convertir (transcodificar) y hacer streaming de audio y vídeo. Incluye libavcodec, una biblioteca de códecs. FFmpeg está desarrollado en GNU/Linux, pero puede ser compilado en la mayoría de los sistemas operativos, incluyendo Windows*
*Es capaz de elegir el códec con sólo escribir la extensión, esto ayuda bastante a la hora de desarrollar flujos sencillos que no necesiten tanta especifididad*

Igualmente vamos a revisar que se encuentre instalado correctamente.
Para eso utilizaremos el siguiente comando.

```bash
ffmpeg --version

```

El resultado debe ser algo parecido a esto **(Puede variar dependiendo de la versión utilizada)**

``` bash

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


```
