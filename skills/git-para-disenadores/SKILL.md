---
name: git-para-disenadores
description: Buenas prácticas de Git y GitHub para trabajar con diseñadores y personas no técnicas. El agente administra ramas, commits, pull requests, conflictos y limpieza, y explica cada paso en lenguaje llano. Úsala siempre que vayas a usar git o gh para alguien que no es desarrollador, o cuando la persona pida cosas como «guarda esto», «súbelo», «publícalo», «crea una rama», «haz una PR», «integra», «junta los cambios», «arregla el conflicto», «deshaz lo que hice» o «borra todo y empieza de cero», aunque no diga Git. También cuando alguien es dueño de un repo y quiere ordenarlo para su equipo. Use it for any Git or GitHub work with designers or non-technical users ("save this", "push it", "open a PR", "merge it").
---

# Git y GitHub para diseñadores

Trabajas con alguien que construye con un agente y no escribe los comandos, pero necesita entender qué haces con su proyecto. Tú ejecutas. La persona decide. Cada paso que des debe poder contarse en una frase sin jerga.

Habla en español salvo que la persona use otro idioma. En ese caso usa el suyo, también para nombres de ramas y mensajes de commit.

## 1. Al empezar, mira y cuenta

Antes de tocar archivos, revisa el estado:

```bash
git status
git branch --show-current
git remote -v
gh pr list --state open
```

Cuéntalo en 2 o 3 líneas llanas. Por ejemplo, «Estás en la rama main. Hay dos archivos cambiados que todavía no guardaste en el historial. El proyecto está conectado a GitHub y tienes una PR abierta».

Si no hay repositorio, explica qué es («una carpeta a la que Git le lleva el historial de cambios») y propone `git init -b main` con un `.gitignore` básico. Si `gh` no está o no hay sesión, dilo y ofrece `gh auth login`.

## 2. Nunca en main. Una rama por cambio

- Antes de editar, acuerda con la persona tres cosas: el objetivo, qué queda fuera y cómo se comprueba. Una frase cada una basta.
- Crea una rama desde main actualizada, una por cambio coherente. Nombre descriptivo en kebab-case en el idioma de la persona, por ejemplo `ajustar-contraste-alertas` o `corrige-texto-boton-pago`.
- Si ya hay cambios sin guardar en main, llévalos a la rama nueva con `git switch -c <rama>`. No los descartes.
- No mezcles en una rama trabajos independientes. Si aparece otro cambio, propón otra rama.

## 3. Commits pequeños que se entiendan

- Antes de cada commit mira qué entra con `git status` y `git diff`. Agrega archivos por nombre con `git add <archivo>`. No uses `git add -A` ni `git add .` sin haber revisado la lista.
- Nunca entran secretos, `.env`, llaves, archivos pesados (videos, exportaciones, `.fig` grandes) ni capturas privadas. Si ves uno, detente y pregunta. Propón sumarlo a `.gitignore`.
- Mensaje con «qué cambió + para qué», en presente y en el idioma de la persona. Un buen mensaje es «Mejora el contraste del texto de error para que se lea sobre fondo claro». Evita «cambios», «fix» o «final final».
- Muestra el mensaje a la persona antes de confirmar cuando el cambio es suyo y no te dio el texto.

## 4. Explica cada comando la primera vez

La primera vez que uses un comando o un término en la conversación, explícalo en una frase. Después ya no hace falta. Usa estas definiciones, que evitan las confusiones típicas de diseñadores:

- **Repositorio.** La carpeta del proyecto más su historial de cambios.
- **Commit.** Un punto guardado del historial con un mensaje. No es Ctrl+S, porque guardar el archivo no crea un commit.
- **Rama.** Una línea de trabajo aparte que apunta a tus commits. No digas que es una copia ni una carpeta. Al cambiar de rama los archivos cambian en pantalla, y eso es normal.
- **Remoto.** La copia del repositorio que vive en GitHub. Se iguala con push (subir) y pull (traer).
- **Pull request (PR).** La propuesta para llevar tu rama a main, que alguien revisa. No es descargar.
- **Merge.** Integrar una rama en otra, normalmente tu rama en main.
- **Conflicto.** Dos ramas cambiaron las mismas líneas y una persona tiene que elegir. No se pierde nada.

Para otros términos y analogías (Figma, staging, revert, enlace de prueba) mira [references/glosario.md](references/glosario.md).

## 5. Pull request enfocada

1. Revisa tu propio diff completo (`git diff main...HEAD`) antes de abrirla. Busca cambios que no tocan al objetivo y sácalos.
2. `git push -u origin <rama>` y luego `gh pr create --base main` con la descripción de [references/plantilla-pr.md](references/plantilla-pr.md). Usa `--draft` si falta algo.
3. Incluye capturas antes y después o el enlace de Figma cuando el cambio es visual. Si el repo está en Vercel, espera su enlace de prueba y pásalo.
4. Dale a la persona el enlace de la PR y explícale el diff en lenguaje llano.

Si no hay remoto en GitHub, explica qué es un remoto y ofrece `gh repo create`. Pregunta si debe ser público o privado.

## 6. Merge solo con un sí explícito

No hagas merge sin que la persona lo apruebe en esta conversación con palabras claras, o sin la revisión que el equipo exija. «Súbelo» significa push y PR, no merge. Que GitHub muestre el botón de merge disponible no es aprobación. Si dudas, pregunta.

## 7. Conflictos

Un conflicto pasa cuando dos ramas cambiaron las mismas líneas. No es un error de la persona y no se pierde nada.

- Para. Muestra las dos versiones en lenguaje llano. Di qué dice cada una y de dónde viene.
- La persona decide con cuál quedarse o cómo combinarlas. Nunca elijas «mi versión» ni `--ours`/`--theirs` por tu cuenta.
- Muestra el resultado antes de commitear y prueba de nuevo el cambio.
- Nunca reclones, borres la carpeta ni el repo para salir del paso. Si no entiendes el archivo, dilo y sugiere pedir apoyo técnico.

## 8. Acciones destructivas. Explica, ofrece lo seguro y espera un sí

Estas acciones borran trabajo o reescriben historia. No las ejecutes sin explicar en una frase qué se pierde y recibir un sí explícito a esa acción concreta:

`git push --force`, `git reset --hard`, `git rebase` de ramas compartidas, `git clean -fd`, `git checkout -- .` o `git restore .` sobre cambios sin guardar, `git branch -D` o `git push origin --delete` de ramas con trabajo sin integrar, `rm -rf .git`, borrar o reclonar el repositorio, `gh repo delete`.

Ofrece siempre la alternativa segura primero (rama de respaldo, `git revert`, `git stash`, `--force-with-lease`). Pedidos como «borra todo y empieza de cero» o «deshaz todo» son ambiguos. Pregunta qué quiere conservar y qué quiere lograr antes de proponer nada. La tabla completa está en [references/comandos.md](references/comandos.md).

## 9. Información sensible

Si una contraseña, token o llave llegó a un commit, avisa de inmediato. Explica que borrarla del archivo no la saca del historial y que lo primero es revocarla o cambiarla en el servicio de origen. Limpiar el historial es una acción destructiva de la sección 8.

## 10. Limpieza después del merge

Cuando la PR ya está integrada:

```bash
git switch main
git pull
git branch -d <rama>
git push origin --delete <rama>
```

`-d` minúscula solo borra si la rama ya está integrada. Si Git se niega, no fuerces. Revisa por qué. Borrar la rama remota de una PR ya integrada no necesita permiso extra.

De vez en cuando, o al empezar en un repo con desorden, lista ramas viejas (`git branch -vv`, `git branch -r --merged main`) y PRs abiertas (`gh pr list`) y propón cuáles cerrar. Nunca las borres sin preguntar.

## 11. Si la persona es dueña del repositorio

Compruébalo con `gh repo view --json viewerPermission`. Si es `ADMIN`, ofrece una vez, sin imponer:

- `README` con para qué sirve, cómo usarlo y a quién pedir ayuda.
- `CONTRIBUTING.md` con cómo proponer cambios y nombrar ramas, y una plantilla `.github/pull_request_template.md`.
- Protección de main (PR obligatoria, sin force-push ni borrado) con `gh api`, si su plan lo permite.
- Revisión de permisos, con el mínimo necesario para cada persona.
- `CODEOWNERS` si hay equipo.

Comandos en [references/comandos.md](references/comandos.md) y el texto completo de buenas prácticas en [references/buenas-practicas.md](references/buenas-practicas.md). Las mismas reglas aplican al dueño. Ser dueño no salta la rama ni la PR.

## 12. Al cerrar cada tarea

Termina con un resumen corto:

- **Rama.** En cuál quedó el trabajo.
- **Commits.** Cuántos y qué dicen.
- **PR.** Enlace y estado (borrador, abierta, integrada).
- **Falta.** Lo que queda pendiente y quién lo decide.
