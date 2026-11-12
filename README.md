# ultimate-web

Skill para agentes de código (Claude Code, Codex, Cursor y los que soporta [`skills`](https://github.com/vercel-labs/skills)) que arma un sitio web desde cero en seis pasos, con un skill dueño por paso y preguntas en cada checkpoint.

```bash
npx skills add francoperez03/ultimate-web -g
```

Después, en el agente: "armá una landing para ..." o "revisá el sitio" para correr un paso suelto.

## El flujo

| Paso | Dueño | Sale |
|---|---|---|
| 0 · Referencia (opcional) | capturas de la URL de referencia | qué se toma de ella |
| 1 · Brief | impeccable (init + shape) | `PRODUCT.md` y brief, aprobados |
| 2 · Dirección | frontend-design, con ui-ux-pro-max como catálogo | `DESIGN.md`, aprobado |
| 3 · Construcción | impeccable (craft) | el sitio, sin animación decorativa |
| 4 · Movimiento (opcional) | Motion o GSAP ScrollTrigger + fixing-motion-performance | animaciones con reduced motion |
| 5 · Revisión | subagente con impeccable (critique + audit) y web-design-guidelines, sobre capturas a 390 y 1440 px | lista por gravedad |
| 6 · Pulido | impeccable (polish) | versión final |

## Dependencias

Este repo solo trae el orquestador. La primera vez que corre, pide permiso e instala lo que falte desde los repos de cada autor:

| Skill | Repo | Licencia |
|---|---|---|
| impeccable | [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | Apache-2.0 |
| frontend-design | [anthropics/skills](https://github.com/anthropics/skills) | Apache-2.0 |
| ui-ux-pro-max | [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | MIT |
| web-design-guidelines | [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills) | ver repo |
| Motion | [`motion-ai`](https://www.npmjs.com/package/motion-ai) | MIT |
| gsap-scrolltrigger | [greensock/gsap-skills](https://github.com/greensock/gsap-skills) | MIT |
| fixing-motion-performance | [ibelick/ui-skills](https://github.com/ibelick/ui-skills) | MIT |

Las de movimiento se instalan solo si el paso 4 se usa.

## Licencia

MIT, solo para el orquestador. Cada dependencia mantiene la suya.
