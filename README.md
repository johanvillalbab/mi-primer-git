# mi primer git

Una app web que enseña a usar Git y GitHub en 4 pasos, con prompts listos para tu agente (Cursor o Claude Code). Es el punto de partida del taller «GitHub para diseñadores» de Interface School.

## Cómo empezar

1. En GitHub, entra a este repositorio y descárgalo con **Code > Download ZIP**.
2. Descomprime el ZIP y abre la carpeta con tu agente (Cursor o Claude Code).
3. Abre `index.html` con doble clic. Si prefieres un servidor local, corre `npx serve` en la carpeta.
4. Sigue los 4 pasos de la app. Copia cada prompt y pégalo en tu agente.

Descargar el ZIP en lugar de clonar es a propósito. La carpeta llega sin historial y así el paso 1 (`git init`) tiene sentido.

## El ejercicio

Haz un cambio pequeño de esta misma interfaz (un texto, un color) siguiendo los 4 pasos:

1. Crea tu proyecto y ponle Git.
2. Conéctalo a GitHub con GitHub CLI.
3. Haz tu primer commit en una rama nueva.
4. Abre tu primera pull request, revísala y llévala a main.

Pide a tu agente que te explique qué cambió y revisa el resultado antes de integrarlo.

## Después del taller

Sigue la [guía de siguientes pasos](GUIA.md). Te muestra cómo revisar el PR de otra persona, publicar con GitHub Pages o Vercel, hacer tu primer cambio en el repositorio de tu equipo y resolver un conflicto.

## Skill para tu agente

En `skills/git-para-disenadores/` hay una skill que le enseña a tu agente a trabajar con Git y GitHub como se vio en el taller. Crea una rama por cambio, escribe commits claros, abre PRs enfocadas, no integra sin tu aprobación y te explica cada paso en lenguaje llano.

Para instalarla, copia la carpeta `git-para-disenadores` en la carpeta de skills de tu agente:

- Claude Code: `~/.claude/skills/`
- Cursor: `~/.cursor/skills/`
- Codex: `~/.agents/skills/`

Por ejemplo, desde la carpeta de este repo:

```bash
cp -R skills/git-para-disenadores ~/.claude/skills/
```

Abre una sesión nueva del agente para que la cargue.

## Qué hay adentro

HTML, CSS y JavaScript sin build ni dependencias (`index.html`, `styles.css`, `app.js`). Iconos de Phosphor y fuente Geist por CDN. Tu progreso se guarda en el navegador.
