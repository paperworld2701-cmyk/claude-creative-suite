---
name: music-production
description: Diseña música original y crea un estudio musical interactivo en un único archivo HTML usando exclusivamente Web Audio API. Actívala cuando el usuario pida música, bandas sonoras, loops, ambientes o el comando /music-production.
---

# Music Production

## Objetivo

Crear música **original** y un archivo `studio_audio.html` autocontenido. El audio se sintetiza en el navegador mediante Web Audio API: no uses MP3 externos, muestras descargadas, APIs musicales, CDN, paquetes, fuentes externas ni librerías pesadas. No imites exactamente canciones, melodías o artistas existentes; describe y utiliza rasgos musicales generales.

## Flujo de trabajo

1. Interpreta la descripción y selecciona un preset:
   - `[DOCUMENTAL TENSO]`: menor, pedal grave, ostinato lento, percusión discreta, tensión gradual.
   - `[HEROICO/CÓMIC]`: mayor o mixolidio, acordes amplios, bajo firme, pulso marcado y metales sintéticos suaves.
   - `[SUSPENSO/MISTERIO]`: menor/dórico, notas espaciadas, intervalos ambiguos, pulsos suaves y silencios.
   - `[LO-FI/FONDO]`: acordes séptimos, progresión cálida, bajo redondo, ritmo relajado y percusión filtrada.
2. Crea una composición nueva: define tonalidad, progresión de acordes, patrón de bajo, ritmo, melodía/ostinato y variaciones. Evita copiar melodías reconocibles.
3. Genera un único `studio_audio.html` que incluya HTML, CSS y JavaScript en el mismo archivo.
4. No afirmes que un archivo fue creado si no has podido escribirlo. Si trabajas en un entorno con herramientas de archivos, crea el archivo; si no, entrega el HTML completo en un único bloque.
5. Explica cómo abrirlo localmente y cómo iniciar el audio. La reproducción debe comenzar solo después de una interacción del usuario.

## Requisitos obligatorios del estudio

### Motor nativo
- Usa `AudioContext`, osciladores, ganancias, filtros y nodos nativos de Web Audio API.
- Cero dependencias externas y cero archivos de audio externos.
- Implementa un secuenciador con reloj basado en `AudioContext.currentTime` y programación anticipada de eventos (look-ahead), evitando depender de `setInterval` para temporizar cada nota.
- Incluye botón Play/Pause y botón Stop/Reset.
- Evita clicks: aplica envolventes cortas de ataque/caída y cambios de ganancia con `setTargetAtTime` o rampas.
- Maneja `AudioContext` suspendido/reanudado y muestra errores legibles.

### Presets musicales
- Reconoce los cuatro tags escritos arriba, aunque aparezcan en una descripción más larga.
- Cambiar de preset debe actualizar armonía, bajo, ritmo, instrumentación sintetizada y tempo sugerido.
- Permite que el usuario edite BPM después de seleccionar el preset.
- La composición debe sonar musical: no uses una secuencia aleatoria sin estructura. Usa escalas y notas compatibles con los acordes.

### Consola en pantalla
Incluye controles funcionales:
- Deslizador BPM/velocidad (por ejemplo 50–180).
- Filtro Grave/Agudo: controla un `BiquadFilterNode` (low-pass o equivalente) y muestra la frecuencia en Hz.
- Volumen maestro con deslizador.
- Botón de Loop infinito que activa/desactiva la repetición sin reiniciar bruscamente.
- Selector de preset y controles Play, Pause, Stop.
- Diseño adaptable a móvil y escritorio, con etiquetas legibles y valores actuales visibles.

### Exportación
Incluye un campo para duración exacta en segundos y botones de exportación:
- **WAV**: renderiza la duración solicitada con `OfflineAudioContext`, incluye la composición completa y codifica PCM WAV de 16 bits en JavaScript. El archivo debe durar exactamente los segundos indicados (según número de frames y sample rate).
- **WEBM/OGG**: usa `MediaRecorder` y `MediaStreamAudioDestinationNode`; selecciona el primer MIME type soportado entre `audio/webm;codecs=opus`, `audio/ogg;codecs=opus` y los formatos de audio que el navegador informe como soportados. Graba exactamente el tiempo indicado con un temporizador y detiene limpiamente los tracks.
- Si el navegador no admite MediaRecorder o un formato, informa la limitación y deja disponible WAV.
- Usa nombres de descarga claros, por ejemplo `music-production-<preset>-<duracion>s.wav`.
- No prometas soporte OGG/WEBM universal: depende del navegador. WAV debe ser la opción de compatibilidad.

### Calidad y robustez
- Debe funcionar al guardar el archivo y abrirlo en un navegador moderno, sin servidor ni conexión.
- No uses `eval`, `new Function`, ni permisos innecesarios.
- Valida duración (por ejemplo 1–600 s) y BPM.
- Deshabilita controles incompatibles durante la exportación y restaura el estado al terminar o fallar.
- Muestra estado de reproducción/exportación y errores.
- La exportación WAV debe ser independiente del estado Play/Pause en vivo y renderizar el patrón desde el inicio.
- Si Loop está activado, repite la estructura; si está desactivado, el patrón puede repetirse solo para completar la duración solicitada de exportación.
- Evita prometer “cero errores” en todos los dispositivos; implementa detección de capacidades y mensajes de fallback.

## Diseño sonoro inicial

Usa estas guías como punto de partida, no como reglas rígidas:

| Preset | BPM sugerido | Carácter armónico | Bajo / ritmo |
|---|---:|---|---|
| DOCUMENTAL TENSO | 82 | menor, pedal y acordes suspendidos | subgrave espaciado, pulso contenido |
| HEROICO/CÓMIC | 118 | mayor, progresión ascendente | bajo firme, bombo y caja suaves |
| SUSPENSO/MISTERIO | 76 | menor/dórico, tensión sin resolver | pulsos escasos, percusión tenue |
| LO-FI/FONDO | 86 | maj7/m7, cálido | bajo redondo, beat relajado |

## Entrega

- Prioriza crear el archivo real `studio_audio.html`.
- Si no puedes crear archivos, devuelve un único bloque de código HTML completo, no pseudocódigo.
- Resume el preset, tonalidad, BPM y progresión utilizada.
- Indica cómo abrir el HTML y usar los controles.
- No uses música protegida, samples externos ni fragmentos de canciones existentes.
