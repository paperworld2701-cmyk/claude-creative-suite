---
name: animation-studio
description: Crea animaciones y videos cortos (HTML/SVG/CSS/Canvas con reproductor, y MP4 o GIF cuando el entorno lo permite). Usar siempre que el mensaje empiece con /animation-studio, o cuando la persona pida una animación, un video animado, motion graphics, un explicador animado, un logo animado o una intro, aunque no use esas palabras exactas.
---

# Animation Studio

Esta skill se activa con `/animation-studio` seguido de la descripción de lo que la persona quiere animar. Ejemplo: `/animation-studio un logo que se dibuja y luego late, 5 segundos, fondo oscuro`.

## Flujo de trabajo

1. **Entender el pedido.** Si falta algo esencial (tema, duración aproximada, estilo, formato de salida), haz como máximo UNA pregunta corta. Si se puede inferir, no preguntes: asume, dilo en una línea y construye.
2. **Planificar en pocas líneas.** Define: duración total, escenas con su tiempo (ej. 0–1 s entrada, 1–4 s acción, 4–5 s salida), paleta de colores, tipografía y proporción (16:9 por defecto; 9:16 si es para móvil/redes).
3. **Construir la animación** como una página HTML autocontenida (un solo archivo) usando:
   - SVG + CSS `@keyframes` para formas, logos, iconos y texto.
   - Canvas + `requestAnimationFrame` para partículas, física o efectos generativos.
   - Librerías solo desde cdnjs, con versión fija, si realmente hacen falta (por ejemplo GSAP).
4. **Incluir controles de reproducción**: botón play/pausa, reiniciar, y barra de progreso. Si la animación debe repetirse, que haga loop.
5. **Entregar.** Publicar la página con la herramienta Artifact si está disponible; si no, guardar el .html en `/mnt/user-data/outputs/` y presentarlo con `present_files`.
6. **Ofrecer iteración**: cambiar velocidad, colores, duración o añadir escenas.

## Reglas de calidad

- Usar easing (ease-in-out, cubic-bezier) en lugar de movimientos lineales; dar ritmo con escalonado (stagger) entre elementos.
- Contraste alto y texto legible; nada de texto más pequeño de 24 px en 16:9.
- Respetar `prefers-reduced-motion` ofreciendo pausa visible.
- Sin imágenes remotas: todo en SVG/CSS/Canvas o como data URI.
- Mantener la animación fluida: animar `transform` y `opacity`, evitar propiedades que fuerzan relayout.
- Comentar brevemente el código por escena para que sea fácil de editar.

## Exportar a video (MP4 / GIF)

Un navegador no genera MP4 directamente desde esta skill, así que sé honesto con la persona:

- Por defecto la entrega es una **animación HTML reproducible** que se puede grabar con la grabación de pantalla.
- Si el entorno tiene `ffmpeg` y un navegador sin interfaz (por ejemplo Playwright/Chromium), verifícalo con bash y, si existen, renderiza los fotogramas (PNG a 30 fps) y únelos en MP4/GIF.
- Si no están disponibles, dilo en una línea y ofrece la versión HTML o una secuencia de fotogramas.
- No prometer audio, voz ni música: no se generan aquí.

## Respuesta final

Breve: qué se hizo (duración, escenas), cómo reproducirlo y una oferta concreta de ajuste. Sin repetir el código en el chat.
