# Vibe Coding con Google — De la idea al MVP en tiempo récord

Slides para la charla sobre cómo usar IA (Google y otras herramientas) para acelerar el desarrollo de software de forma responsable. Es un deck HTML de un solo archivo, sin dependencias, animado y con soporte para tema claro/oscuro — con un contador de reacciones (👍/❤️) en tiempo real para el público, desplegado en Vercel.

## Ver el deck

- **En vivo**: [slides-five-amber.vercel.app](https://slides-five-amber.vercel.app)
- **Local**: abre [`slides/vibe-coding-charla.html`](slides/vibe-coding-charla.html) directamente en el navegador (doble clic o `file://...`). No requiere build, servidor ni instalación de dependencias — el widget de reacciones simplemente no aparece sin conexión (ver [Reacciones en vivo](#reacciones-en-vivo)).

## Características

- **Stage fijo 16:9** (1920×1080) que escala a cualquier pantalla sin reflow de contenido.
- **Tema claro / oscuro** con acento violeta, con toggle persistente (`localStorage`).
- **Control de tamaño de texto** (`A−` / `A+` o teclas `-`/`+`/`0`) para ajustar la letra en vivo sin romper el diseño.
- **Animaciones de entrada** (fade + stagger), **parallax** de fondo y transiciones suaves entre slides.
- **Gráficas** (dona y barras) con datos de adopción de IA en desarrollo.
- **Retrato del ponente** integrado con efecto Ken Burns.
- **Reacciones en vivo** (👍/❤️): cualquiera que abra el deck puede reaccionar y todos ven el contador subir en tiempo real, con animaciones de emojis — ver detalle abajo.
- **QR de portada** al deck en vivo, con zoom al hacer hover/focus para escanearlo más fácil. **Slide final de contacto** con QR reales (generados con `qrcode` vía `pnpm`) para LinkedIn, GitHub, portafolio e Instagram.
- **Exportar a PDF** con un botón (usa `window.print()`).
- **Edición inline**: hover en la esquina superior izquierda o tecla `E` para editar cualquier texto directamente en el navegador.

## Navegación

- Flechas `←`/`→`, `Space`, rueda del mouse o swipe (táctil).
- `Home` / `End` para ir al inicio/final.
- `T` cambia el tema, `E` activa el modo edición, `H` oculta/muestra los controles de la esquina.
- `R` reinicia el contador de reacciones a 0 (pide una passphrase — ver abajo).

## Reacciones en vivo

El botón 👍/❤️ (esquina inferior izquierda) usa **Supabase** como backend: un proyecto gratuito (`vibe-coding-reacciones`) con Realtime Broadcast para repartir cada tap al instante a todos los que tengan el deck abierto, y una tabla de una sola fila como total autoritativo (para sembrar el contador a quien entra tarde y para el reset).

- El widget se muestra solo si logra conectar con Supabase; abierto por `file://` o sin red, el deck sigue funcionando normal, simplemente sin el widget.
- Los taps propios se agrupan y se escriben a la base de datos cada ~1.5s (no una escritura por click); las reacciones de otras personas llegan por Broadcast y disparan una animación más pequeña/discreta (limitada a ~1 cada 220ms para no saturar la pantalla si reacciona mucha gente a la vez).
- Seguridad: el cliente solo puede **leer** el total y llamar dos funciones RPC (`bump_reaction`, `reset_reactions`) — no hay política de escritura directa a la tabla (verificado: un `UPDATE` directo desde el cliente no modifica ninguna fila).
- **Reiniciar el contador** (recomendado antes de cada charla): tecla `R` en el deck y escribe la passphrase (definida dentro de la función `reset_reactions` en Supabase, no está en el código del cliente ni en este repo).
- El SQL de la migración (tabla `reactions`, RPCs, políticas RLS) vive en el proyecto de Supabase, no en este repo, para no versionar la passphrase de reset.

## Desplegar

El sitio se despliega desde `slides/` (así las rutas relativas a `imgs/` funcionan tal cual). Con el [Vercel CLI](https://vercel.com/docs/cli) ya autenticado:

```
cd slides
vercel --prod
```

`slides/vercel.json` reescribe `/` hacia `vibe-coding-charla.html` para que la URL raíz sirva el deck directamente. `slides/.vercel/` (link local al proyecto de Vercel) y `slides/.gitignore` los genera el propio CLI en el primer deploy.

Si se necesita reconfigurar el backend de reacciones (nuevo proyecto de Supabase, nueva URL/key), hay que actualizar `SUPABASE_URL` y `SUPABASE_KEY` dentro de `setupReactions()` en `vibe-coding-charla.html` y volver a desplegar.

## Estructura

```
Charla.docx / Charla.md   # guion original de la charla (fuente de verdad del contenido)
slides/
  vibe-coding-charla.html # el deck completo (HTML + CSS + JS en un solo archivo)
  imgs/yo.png             # retrato del ponente
  vercel.json             # rewrite de "/" al HTML del deck
CLAUDE.md                 # guía de arquitectura y convenciones para trabajar en el repo con Claude Code
```

## Créditos

Deck construido con la skill [`frontend-slides`](https://github.com/zarazhangrui/frontend-slides) (template Neo-Grid Bold, adaptado a paleta violeta).
