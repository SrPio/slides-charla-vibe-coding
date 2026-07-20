# Vibe Coding con Google — De la idea al MVP en tiempo récord

Slides para la charla sobre cómo usar IA (Google y otras herramientas) para acelerar el desarrollo de software de forma responsable. Es un deck HTML de un solo archivo, sin dependencias, animado y con soporte para tema claro/oscuro.

## Ver el deck

Abre [`slides/vibe-coding-charla.html`](slides/vibe-coding-charla.html) directamente en el navegador (doble clic o `file://...`). No requiere build, servidor ni instalación de dependencias.

## Características

- **Stage fijo 16:9** (1920×1080) que escala a cualquier pantalla sin reflow de contenido.
- **Tema claro / oscuro** con acento violeta, con toggle persistente (`localStorage`).
- **Control de tamaño de texto** (`A−` / `A+` o teclas `-`/`+`/`0`) para ajustar la letra en vivo sin romper el diseño.
- **Animaciones de entrada** (fade + stagger), **parallax** de fondo y transiciones suaves entre slides.
- **Gráficas** (dona y barras) con datos de adopción de IA en desarrollo.
- **Retrato del ponente** integrado con efecto Ken Burns.
- **Slide final de contacto** con QR reales (generados con `qrcode` vía `pnpm`) para LinkedIn, GitHub, portafolio e Instagram.
- **Exportar a PDF** con un botón (usa `window.print()`).
- **Edición inline**: hover en la esquina superior izquierda o tecla `E` para editar cualquier texto directamente en el navegador.

## Navegación

- Flechas `←`/`→`, `Space`, rueda del mouse o swipe (táctil).
- `Home` / `End` para ir al inicio/final.
- `T` cambia el tema, `E` activa el modo edición.

## Estructura

```
Charla.docx / Charla.md   # guion original de la charla (fuente de verdad del contenido)
slides/
  vibe-coding-charla.html # el deck completo (HTML + CSS + JS en un solo archivo)
  imgs/yo.png             # retrato del ponente
CLAUDE.md                 # guía de arquitectura y convenciones para trabajar en el repo con Claude Code
```

## Créditos

Deck construido con la skill [`frontend-slides`](https://github.com/zarazhangrui/frontend-slides) (template Neo-Grid Bold, adaptado a paleta violeta).
