# Music Production

Plugin de Claude Code que añade el comando `/music-production`.

## Instalación
1. Descomprime el ZIP.
2. Instala la carpeta `music-production` como plugin local de Claude Code, o empaquétala según el método de instalación de plugins de tu versión.
3. En Claude Code, ejecuta `/music-production [DOCUMENTAL TENSO]` (o uno de los otros presets).

El comando instruye a Claude a crear un `studio_audio.html` autocontenido. La plantilla incluida en `templates/studio_audio.html` es un estudio funcional de referencia.

## Compatibilidad
- WAV: renderizado offline PCM 16-bit.
- WEBM/OGG: depende de MediaRecorder y del navegador.
- Todo el sonido se genera localmente con Web Audio API.
