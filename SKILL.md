---
name: ultimate-web
description: Arma un sitio web desde cero en seis pasos (brief, dirección, construcción, movimiento, revisión, pulido), con un skill dueño por paso y preguntas en cada checkpoint. Orquesta impeccable, frontend-design, ui-ux-pro-max, web-design-guidelines y skills de motion, y los instala si faltan. Usar cuando se pide "armá un sitio", "landing desde cero", "hacé la web de X", "nuevo sitio", o para correr un paso suelto ("revisá el sitio", "rehacé la dirección", "paso 5").
---

# ultimate-web

Orquestador. No diseña por su cuenta: en cada paso carga el skill dueño y sigue sus instrucciones. Un paso, un dueño; nunca cargar dos skills de estética en el mismo paso porque se pisan.

## Arranque (una vez por sesión)

1. **Dependencias.** Verificar cuáles están disponibles (en la lista de skills de la sesión, o como carpeta en `.agents/skills/`, `~/.agents/skills/` o `~/.claude/skills/`):

   | Skill | Si falta |
   |---|---|
   | `impeccable` | `npx skills add pbakaus/impeccable -s impeccable -g -y` |
   | `frontend-design` (o el plugin `frontend-design:frontend-design`) | `npx skills add anthropics/skills -s frontend-design -g -y` |
   | `ui-ux-pro-max` | `npx skills add nextlevelbuilder/ui-ux-pro-max-skill -s ui-ux-pro-max -g -y` |
   | `web-design-guidelines` | `npx skills add vercel-labs/agent-skills -s web-design-guidelines -g -y` |

   Si falta alguno: listarlos, pedir permiso UNA vez, instalar todos, y avisar que si no aparecen en la sesión hay que reiniciar el agente (mientras tanto, leer su `SKILL.md` directo desde la carpeta instalada). Las de movimiento se instalan recién en el paso 4.

2. **Rutas de impeccable.** Sus instrucciones usan `node .agents/skills/impeccable/scripts/...`. Si esa carpeta no existe en el proyecto, usar la misma ruta bajo `~/.agents/skills/`.

3. **Retomar.** Mirar el proyecto: si ya hay `PRODUCT.md` y/o `DESIGN.md` (raíz, `.agents/context/` o `docs/`) o código, decir en qué paso parece estar y preguntar si sigue desde ahí o salta a otro. Si el usuario pidió un paso puntual, ir directo a ese paso.

## Los pasos

Preguntas: con la herramienta de preguntas del agente si existe, máximo 4 por ronda, cada una con una opción recomendada. No repetir lo que ya responden `PRODUCT.md`, `DESIGN.md` o el pedido. El banco de preguntas está en `reference/preguntas.md`.

### 0 · Referencia (solo si hay un sitio a imitar)
Si el usuario dio una URL de referencia: si está disponible `landing-research`, usarlo; si no, abrir la URL con el navegador o Playwright, sacar capturas a 390 px y 1440 px y anotar en 5 líneas qué se toma (estructura, tipografía, ritmo, movimiento). Se copia la idea, nunca los assets ni los textos.

### 1 · Brief · dueño `impeccable` (init + shape)
- Hacer primero las preguntas de proyecto de `reference/preguntas.md` §1 que impeccable no cubre (stack, dónde se publica, contenido disponible, referencia).
- Después correr `impeccable` init si no hay `PRODUCT.md`, y `impeccable shape` para la entrevista del sitio. Sus preguntas son las suyas: no duplicarlas.
- **Checkpoint:** mostrar `PRODUCT.md` y el brief de shape. Seguir solo con OK.

### 2 · Dirección · dueño `frontend-design`
- Si el brief pide un estilo fijo (minimalista, brutalista, etc.) y hay un skill instalado para ese estilo, ese reemplaza a `frontend-design` en este paso.
- Preguntas de §2.
- Seguir el proceso de `frontend-design`: plan de tokens (4 a 6 colores con hex, tipografías y rol, layout en wireframe ASCII, principios), revisión contra el brief para sacar lo genérico.
- `ui-ux-pro-max` solo como catálogo: consultar paletas o pares de fuentes con su `scripts/search.py` cuando haga falta una opción concreta. No usar su "design system" completo: la dirección la decide `frontend-design`.
- Volcar el plan en `DESIGN.md` con el formato de `impeccable` (`reference/document.md`: frontmatter YAML de tokens + las seis secciones).
- **Checkpoint:** mostrar `DESIGN.md` (paleta, fuentes, wireframe). Es el último punto barato para cambiar de rumbo. No escribir código sin OK.

### 3 · Construcción · dueño `impeccable` (craft)
- Correr `impeccable craft` sobre el brief y el `DESIGN.md` aprobados. Respetar sus gates.
- Stack: el que se eligió en el paso 1. Si hay skills del stack disponibles (por ejemplo shadcn, Next.js, Astro), cargarlos como apoyo técnico, nunca como fuente de estética.
- Construir sin animaciones decorativas: que funcione y se vea bien quieto. Solo transiciones de estado (hover, focus, abrir/cerrar).
- Si un token cambia, se edita `DESIGN.md`, no se hardcodea.

### 4 · Movimiento (opcional) · dueño `motion` o `gsap-scrolltrigger`
- Preguntas de §4. Si la respuesta es "sin movimiento", saltar al paso 5.
- Instalar lo que falte: `npx motion-ai` (Motion, para React/Vue y CSS), `npx skills add greensock/gsap-skills -s gsap-scrolltrigger -g -y` (scroll), y siempre `npx skills add ibelick/ui-skills -s fixing-motion-performance -g -y`.
- Un solo momento orquestado mejor que efectos en cada sección. Siempre con alternativa `prefers-reduced-motion`.
- Cerrar con `fixing-motion-performance` sobre lo animado.

### 5 · Revisión · `impeccable` (critique + audit) + `web-design-guidelines`
- Levantar el sitio y sacar capturas de página completa a **390 px y 1440 px**.
- La revisión la hace un **subagente aparte** que recibe el código, `PRODUCT.md`, `DESIGN.md` y las capturas, sin el razonamiento de quien construyó. Corre `impeccable critique`, `impeccable audit` y `web-design-guidelines` sobre los archivos de la UI.
- Unir los hallazgos en una sola lista ordenada por gravedad (bloquea / importante / detalle), sin duplicados.
- **Checkpoint:** preguntas de §5 (qué se arregla ahora). Arreglar, volver a capturar y comparar.

### 6 · Pulido · dueño `impeccable` (polish)
- Correr `impeccable polish` con la vara elegida en §5 (MVP o terminado).
- Capturas finales a 390 px y 1440 px y resumen al usuario: qué quedó, qué quedó pendiente, cómo se publica.

## Reglas

- Un paso, un dueño. Los demás skills entran solo como consulta (catálogo, stack, guías).
- Los checkpoints de los pasos 1, 2 y 5 son obligatorios aunque el pedido parezca claro.
- Toda decisión visual vive en `DESIGN.md`; toda decisión de producto en `PRODUCT.md`.
- Las capturas son la evidencia de cualquier revisión: se revisa lo que se ve, no solo el código.
- Contenido real del usuario siempre gana a placeholder; si falta, placeholder marcado como tal y anotado en el resumen final.
