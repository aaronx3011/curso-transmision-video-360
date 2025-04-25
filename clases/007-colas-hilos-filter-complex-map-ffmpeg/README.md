# Filter_complex y Map (FFMpeg)

La idea de esta clase es cambiar el framerate de un video. Adicionalmente vamos a aprender como podemos convertir videos en una secuencia de images
*Separa un video en una secuencia de imagenes nos va a ayudar en un futuro a "debuggear" o analizar los videos que estemos trabajando en busca de posibles fallas*
Para llevar a cabo los ejercicios de esta clase requerimos de un video local que cumpla con las características expuestas en el archivo **README.md**


### Requisitos
En esta clase estaremos usando un video con las siguientes características.


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
