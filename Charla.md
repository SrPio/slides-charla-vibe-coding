**Título de la Charla: Vibe Coding con Google: De la idea al MVP en tiempo récord**

*Nota de sincronización (recorte a 30 min): el deck (`slides/vibe-coding-charla.html`) se redujo de 34 a 27 slides para caber en el tiempo real de la charla. Se fusionaron o recortaron varias secciones (stats de adopción, NotebookLM, integración MCP→Linear/Jira, caso de uso de n8n, pipeline de diseño a 4 pasos) y se eliminó por completo la sección de selección de modelos (Opus/Sonnet/Haiku). Se añadió una nueva sección de cierre, "Caja de Herramientas de la Charla", con Chrome DevTools MCP y las CLIs de deploy (Vercel/Render) como recomendaciones nuevas. El texto de abajo ya refleja estos cambios.*

*Nota de reorganización (28 slides): dentro del Bloque 3 se reordenaron las slides para que el flujo narrativo coincida con el orden real de un proyecto -contexto/skills primero, luego prototipado (diseño), luego implementación con TDD, luego despliegue- y ese mismo orden es el que resume la slide de pipeline "Del plan a un MVP funcional". Se añadió una slide nueva de Despliegue (skills de deploy + CLIs de Vercel/Render/Supabase) y se sumaron menciones a Cursor, Antigravity y Devin en la slide de TDD como ejemplos de quién ejecuta esa implementación. El texto de abajo ya refleja el nuevo orden.*

Descripción: Descubre un flujo de trabajo práctico para transformar una idea en un MVP funcional en tiempo récord utilizando herramientas de Google y otras soluciones potenciadas por IA. Conocerás técnicas, trucos y buenas prácticas para validar, diseñar, desarrollar y acelerar la creación de productos de forma más eficiente.

¡Muy buenas noches para todos! Antes de entrar de lleno en materia, quiero contarles algo. Aunque el título de la charla menciona herramientas de Google, en realidad vamos a recorrer un panorama bastante más amplio: hoy son muchas las empresas -no solo Google- las que le están metiendo la ficha a la inteligencia artificial, así que también hablaremos de herramientas y soluciones de otros jugadores importantes en este espacio.

También quiero ser honesto con ustedes: esta es la primera vez que me paro frente a un público como ponente, así que sí, tengo un poquito de nervios jeje. Pero no importa, porque lo que más me emociona es compartir con ustedes todo lo que he aprendido sobre este tema que me apasiona. Así que si me ven algo nervioso, ya saben por qué... ¡y no está de más que me deseen algo de suerte!

Bueno, dicho todo esto, creo que es un buen momento para que nos conozcamos un poco mejor antes de arrancar. Déjenme contarles brevemente quién les está hablando hoy.

**Presentación del Ponente**

Mi nombre es Andrés Jaramillo, soy ingeniero de sistemas y desarrollador Frontend, con más de 5 años de experiencia diseñando y construyendo interfaces y experiencias digitales. Soy un apasionado del apartado visual en todas sus formas: el diseño gráfico, el arte digital y el diseño UX/UI son terrenos donde disfruto tanto crear como aprender. Fuera del código, soy un fanático confeso de la cultura pop, así que si en algún momento se me escapa una referencia de una película, videojuego o cómic, ya saben de dónde viene.

**Conceptos Clave:  
**

| **Concepto**                                              | **Definición corta**                                                                                                                |
| --------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **LLM (Large Language Model)**                            | **Modelo de IA entrenado con grandes cantidades de texto para entender y generar lenguaje, responder preguntas y escribir código.** |
| **MCP (Model Context Protocol)**                          | **Protocolo que permite a una IA conectarse de forma estandarizada con herramientas, APIs y bases de datos.**                       |
| **Skills**                                                | **Instrucciones reutilizables que enseñan a la IA cómo realizar una tarea específica de manera consistente.**                       |
| **CLI (Command Line Interface)**                          | **Interfaz que permite interactuar con un programa mediante comandos escritos en la terminal.**                                     |
| **Plugins (IA)**                                          | **Extensiones que agregan nuevas funciones o integraciones a una herramienta de IA.**                                               |
| **SRS (Software Requirements Specification)**             | **Documento que define los requisitos funcionales y no funcionales que debe cumplir el software.**                                  |
| **PRD (Product Requirements Document)**                   | **Documento que describe qué producto se va a construir, para quién y qué problema resuelve.**                                      |
| **Documento de Arquitectura / Especificaciones Técnicas** | **Documento que explica cómo se implementará el sistema: tecnologías, componentes, estructura y decisiones técnicas.**              |

**  
<br/>**

**Introducción: La Nueva Realidad del Desarrollo**

Estamos viviendo una revolución. Ya no hablamos de una promesa futurista, sino de una realidad que está transformando la forma en que desarrollamos software. Hoy, alrededor del **90% de los profesionales del desarrollo utilizan herramientas de inteligencia artificial** como parte de su flujo de trabajo diario, y cada vez es más común que los agentes de IA sean capaces de implementar funcionalidades completas, generar pruebas, refactorizar código e incluso proponer cambios que llegan a producción bajo la supervisión de un desarrollador.

Esta transformación también ha cambiado profundamente la forma en que trabajamos. Hace apenas unos años, la IA se limitaba a sugerir líneas de código o completar funciones. Después llegaron los asistentes conversacionales dentro de los editores, que nos ayudaban a resolver errores o implementar pequeñas funcionalidades. Hoy, con herramientas como Cursor, Claude Code o Gemini CLI, el paradigma es completamente diferente: ya no les pedimos que escriban una función, sino que implementen una característica completa, ejecuten pruebas, corrijan errores y propongan una solución integral. En muchos casos, nuestro teclado ha dejado de ser la principal herramienta de producción; ahora nuestro trabajo consiste en definir objetivos, proporcionar contexto y validar los resultados que generan los agentes.

Pero el verdadero cambio no está únicamente en desarrollar más rápido. Los estudios muestran que herramientas como GitHub Copilot pueden acelerar determinadas tareas de programación hasta en un **55%**, permitiendo que los desarrolladores dediquen más tiempo al diseño de arquitectura, la resolución de problemas complejos y la colaboración con sus equipos. Además, el **90% de los desarrolladores** que utilizan estas herramientas reportan una mayor satisfacción laboral. La IA no viene a reemplazar nuestro criterio; viene a potenciar nuestra capacidad para construir mejores soluciones y permitirnos concentrarnos en las decisiones que realmente generan valor.

En este contexto ha surgido un término muy popular: **Vibe Coding**. Hoy no quiero hablarles del Vibe Coding como una simple tendencia, sino de lo que yo llamo **Vibe Coding Responsable**. Es decir, aprovechar la velocidad, la creatividad y la capacidad de ejecución que nos ofrecen los agentes de IA, sin renunciar al pensamiento crítico ni a la responsabilidad de la ingeniería. No se trata de escribir más código manualmente, sino de tomar mejores decisiones: definir una buena arquitectura, establecer restricciones claras, validar los resultados y garantizar la seguridad, el rendimiento y la mantenibilidad de nuestras aplicaciones.

Para mí, la mejor analogía es la de **un arquitecto dirigiendo a un equipo constructor**. Hoy la IA puede comportarse como un equipo extraordinariamente rápido, capaz de construir gran parte de la solución en cuestión de minutos. Sin embargo, ese equipo necesita a alguien que comprenda el problema, defina el diseño, establezca las reglas, supervise la ejecución y determine cuándo el trabajo realmente cumple con los objetivos del proyecto. Ese rol sigue siendo nuestro.

En otras palabras, el valor del desarrollador ya no reside únicamente en escribir código, sino en aportar criterio, contexto y visión de ingeniería. La IA puede acelerar enormemente la construcción del software, pero la responsabilidad sobre lo que construimos -y por qué lo construimos- continúa siendo completamente humana.

**Bloque 1: Investigación y Aprendizaje de Alto Impacto**

**Venciendo las Alucinaciones con NotebookLM**

Uno de los mayores miedos al usar IA es la "alucinación": que el modelo invente datos obsoletos o incorrectos. Para solucionar esto, utilizamos herramientas como **NotebookLM**, donde nosotros tomamos el control total de las fuentes de información.

- **Fuentes Confiables:** Podemos alimentar a la IA con documentación oficial (MDN, Python.org), videos de YouTube o archivos PDF locales.
- **Resultados Verificables:** Al dialogar con este "cuaderno de conocimiento", la IA nos ofrece citas directas, que nos llevan al segundo exacto de un video o al párrafo de un documento, eliminando la incertidumbre.

**Ingeniería de Prompts y "Deep Research"**

La ingeniería de prompts ha pasado de buscar la "frase mágica" a ser un proceso **iterativo y estratégico**.

- **Investigación Profunda:** Con modelos razonadores, podemos realizar análisis de repositorios complejos en GitHub en cuestión de minutos. Lo que antes tomaba semanas de investigación manual para entender una librería, ahora se puede resumir en un informe técnico detallado que identifica puntos de entrada, dependencias críticas y "hotspots" de complejidad.

**Bloque 2: Transformando el Ciclo de Vida del Desarrollo**

**De la Reunión al Ticket Automático**

La IA puede optimizar la fase de gestión de requisitos, que suele ser un cuello de botella.

- **Notas de Reunión:** Usamos herramientas como Gemini para transcribir y resumir automáticamente lo discutido con negocio.
- **Historias de Usuario y Gherkin:** A partir de esas notas, la IA genera **Historias de Usuario** (Como... quiero... para...) y **Criterios de Aceptación** en formato **Gherkin** (Given-When-Then). Esto define de manera inequívoca cuándo una tarea está "terminada".
- **Integración con MCP:** Usando el **Model Context Protocol (MCP)**, agentes como Claude Code pueden conectarse directamente a herramientas como Linear o Jira para crear los tickets automáticamente, ahorrando días de trabajo administrativo.

**El "Contexto" es el Rey**

Para que la IA no alucine dentro de nuestro proyecto, debemos "enseñarle" nuestras reglas.

- **Carpeta de Contexto:** Incluir esquemas SQL o documentación técnica para que la IA entienda nuestra base de datos.
- **Archivo agents.md:** Este archivo se ha convertido en un estándar de facto para definir reglas de estilo (ej. usar snake_case siempre) y establecer las "fuentes de verdad" del proyecto.

**Extendiendo la IA: Skills, MCP y Plugins en la Práctica**

Ya vimos que el contexto es fundamental, pero no siempre queremos reescribir esas reglas para cada proyecto o herramienta. Ahí es donde entran tres piezas clave que ya mencionamos en la tabla de conceptos: los Skills, el Model Context Protocol (MCP) y los Plugins. Estas nos permiten estandarizar y extender lo que la IA puede hacer, sin depender de un prompt gigante cada vez que abrimos el editor.

**Skill de Frontend Design (anthropics/skills):** Es una skill oficial del repositorio open source de Anthropic, pensada para guiar a la IA en la construcción de interfaces consistentes, accesibles y alineadas con buenas prácticas de diseño, en lugar de dejar que "invente" estilos o componentes cada vez.

**Skill y MCP de Context7:** Context7 ofrece tanto una skill como un servidor MCP que inyectan documentación siempre actualizada de librerías y frameworks directamente en el contexto de la IA. Esto evita uno de los problemas más comunes: que el modelo sugiera código basado en versiones antiguas o en APIs que ya cambiaron.

**MCP/Plugin de Base de Datos (por ejemplo, MongoDB):** En lugar de copiar manualmente esquemas a una carpeta de contexto, podemos conectar un MCP o plugin específico de nuestra base de datos -como el de MongoDB- para que la IA consulte la estructura real de las colecciones, entienda las relaciones entre los datos y proponga queries o migraciones con mayor precisión.

**Bloque 3: Diseño, Implementación y Despliegue**

Con el contexto ya resuelto, toca recorrer el resto del ciclo en el mismo orden en que ocurre en un proyecto real: primero diseñamos y prototipamos, después implementamos, y por último desplegamos.

**Prototipado Ultra-Rápido y n8n**

La IA destruye el "síndrome de la hoja en blanco". Con **Google AI Studio**, podemos pasar de un **boceto hecho a mano** a una aplicación web funcional (Next.js/Tailwind) desplegada con un solo clic.

En esta misma línea de prototipado ultra-rápido está **Google Stitch**, un experimento de Google Labs (nacido de la adquisición de Galileo AI) que usa Gemini para convertir un simple prompt de texto -o incluso un boceto o una captura de pantalla- en pantallas de interfaz completas en segundos. Lo interesante es que no genera una sola pantalla suelta: puede describir un flujo completo de la aplicación y generar hasta **5 pantallas conectadas** de una sola vez, listas para exportar a Figma o directamente a código HTML/CSS. Ya lo vamos a ver de nuevo más adelante como parte del flujo de diseño a desarrollo.

Para flujos de trabajo más complejos, herramientas como **n8n** permiten conectar más de 500 aplicaciones mediante **nodos y triggers**.

- **Caso de uso:** Podemos crear un sistema de **Web Scraping con IA** que monitoree sitios web, filtre información específica (como cursos de Python) y guarde los resultados en una base de datos automáticamente.

**Desarrollo Guiado por TDD con IA**

Con el diseño listo, entramos a la implementación. La IA puede aplicar **Test-Driven Development (TDD)**:

- Crea una rama aislada en el repositorio.
- Escribe primero los **tests vacíos** basados en los criterios de aceptación.
- Implementa el código necesario para que los tests pasen de "rojo" a "verde".

¿Quién ejecuta esto en la práctica? Cualquiera de los editores y agentes de código que ya mencionamos: **Claude Code**, **Cursor**, el más reciente **Antigravity** de Google, o alternativas como **Devin** de Cognition Labs -un agente que llega a plantear el plan, implementar el código, correr las pruebas e incluso desplegar de forma autónoma dentro de su propio entorno-. La idea es la misma en todos: nosotros seguimos definiendo el "qué" y el "por qué"; el agente ejecuta el "cómo" bajo supervisión.

**Despliegue: Skills y CLIs**

Una vez el código pasa sus pruebas, falta el último paso: llevarlo a producción. Aquí conviene apoyarse en dos piezas: una **skill de despliegue**, que le enseña al agente el checklist completo -build, variables de entorno, migraciones, verificación post-deploy- para no repetirlo manualmente en cada proyecto; y las **CLIs oficiales** de las plataformas de hosting, como las de **Vercel**, **Render** o **Supabase**. Usar la CLI en lugar de un dashboard nos permite scriptear el despliegue e integrarlo directamente a CI/CD, en vez de hacer clic manualmente cada vez.

**El Flujo de Diseño a Desarrollo: Stitch, Figma y Antigravity**

Ya hablamos de investigación, gestión de requisitos y prototipado rápido. Ahora quiero mostrarles el flujo concreto que uso para llevar una idea desde el diseño hasta un MVP funcional, encadenando varias herramientas de IA.

**Diseño de Interfaces con Google Stitch:** Stitch es la herramienta de Google que permite generar pantallas y prototipos de UI a partir de un simple prompt de texto, dándonos en segundos un punto de partida visual real para el producto.

**De Stitch a Figma (MCP):** Una vez tenemos el diseño generado en Stitch, lo trasladamos a Figma usando su servidor MCP. Esto nos permite refinar el diseño con herramientas profesionales y, después, usar ese mismo archivo como contexto directo para nuestro editor de código.

**Cursor o Antigravity como Editor:** Para pasar del diseño al código, usamos editores potenciados por IA como Cursor o el más reciente Antigravity de Google, capaces de implementar pantallas completas a partir del diseño en Figma y las instrucciones del proyecto.

**MCP de Backend (Supabase o Firebase):** En lugar de programar manualmente la base de datos, la autenticación o el almacenamiento, conectamos un MCP de Supabase o Firebase para que el agente cree tablas, configure la autenticación y despliegue el backend directamente desde el editor.

**Antigravity para Pruebas (Control del Navegador):** Una de las funciones más interesantes de Antigravity es su capacidad de controlar el navegador de forma autónoma: abre la aplicación, navega entre pantallas, hace clic en los botones y valida que el flujo funcione como se espera, sin que nosotros escribamos una sola línea de test manualmente.

**La Seguridad no es Negociable**

La rapidez no puede comprometer la integridad. La IA a menudo genera patrones inseguros basados en datos de entrenamiento obsoletos.

- **Vulnerabilidades comunes:** Credenciales hardcodeadas (ej. "admin/123456") o controles de acceso rotos que permiten acceder a URLs internas sin loguearse.
- **Nuestro rol:** Debemos aplicar los principios de **Security by Design** y **Security by Default**, auditando cada sugerencia de la IA para implementar hashing de contraseñas y validaciones robustas en el servidor.

**Antes de Cerrar: Caja de Herramientas de la Charla**

Antes de despedirme, quiero dejarles un resumen rápido: un mapa de todas las herramientas, MCPs y skills que mencionamos hoy, organizado por la etapa del flujo de trabajo donde encajan.

- **01 · Investigación & Requisitos:** NotebookLM, Gemini, integración con Linear/Jira vía MCP.
- **02 · Diseño:** Google Stitch, Figma (MCP).
- **03 · Desarrollo & Contexto:** Cursor, Claude Code, Antigravity, Devin, Context7 (MCP).
- **04 · Backend & Datos:** Supabase, Firebase, MongoDB (MCP).
- **05 · QA & Automatización:** Antigravity QA (control de navegador), **MCP Chrome DevTools** -para que el agente inspeccione consola, red y DOM del navegador en tiempo real durante las pruebas, sin salir del editor-, y n8n para automatizaciones más amplias.
- **06 · Deploy (CLI):** además de Google AI Studio con su despliegue de un clic, para proyectos que crecen más allá de eso recomiendo apoyarse en las CLIs oficiales de plataformas como **Vercel** o **Render**: permiten scriptear el despliegue, integrarlo a CI/CD y repetirlo de forma consistente en lugar de hacer clic manualmente en un dashboard cada vez.

**Conclusión: El Desarrollador Orquesta**

El futuro del desarrollo no es menos humano, sino **más estratégico**. El programador exitoso hoy es quien sabe orquestar todas estas piezas -investigación, diseño, desarrollo, backend, QA y despliegue- sin perder de vista el criterio de ingeniería en cada paso.

La IA es la herramienta más avanzada que hemos tenido jamás para construir, pero el ingenio, la arquitectura y la supervisión crítica siguen siendo, y seguirán siendo, nuestra responsabilidad única.

<br/><br/><br/>Fuentes:  
\- <https://blog.google/innovation-and-ai/technology/developers-tools/dora-report-2025/?utm_source=chatgpt.com>  
<br/>\- <https://github.blog/news-insights/research/research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/?utm_source=chatgpt.com>  
<br/>\- <https://developers.googleblog.com/build-with-google-antigravity-our-new-agentic-development-platform/> (Google Antigravity)  
<br/>\- <https://antigravity.google/> (Google Antigravity, sitio oficial)  
<br/>\- <https://cognition.ai/> (Cognition Labs / Devin)  
<br/>\- <https://vercel.com/docs/cli> (Vercel CLI)  
<br/>\- <https://render.com/docs/cli> (Render CLI)  
<br/>\- <https://supabase.com/docs/guides/local-development/cli/getting-started> (Supabase CLI)

\-