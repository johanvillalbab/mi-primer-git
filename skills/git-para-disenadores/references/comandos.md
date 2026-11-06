# Comandos seguros y peligrosos

## Peligrosos y su alternativa segura

Antes de cualquiera de la columna izquierda, explica en una frase qué se pierde, ofrece la alternativa y espera un sí explícito a esa acción concreta.

| Peligroso | Qué se pierde | Alternativa segura |
|---|---|---|
| `git push --force` | Commits de otras personas en la rama remota. | `git push --force-with-lease`, y solo en ramas tuyas que nadie más usa. Nunca en main. |
| `git reset --hard` | Todo cambio sin commit y los commits que quedan atrás. | `git stash push -m "<motivo>"` para apartar cambios. `git revert <commit>` para deshacer algo ya guardado. Antes de un reset, `git branch respaldo-<fecha>`. |
| `git rebase` en ramas compartidas | Reescribe commits que otras personas ya tienen. | `git merge origin/main` dentro de tu rama. |
| `git clean -fd` | Archivos nuevos que Git todavía no guarda. No van a la papelera. | `git clean -nd` para ver la lista primero. Mover lo que sobra a otra carpeta. |
| `git checkout -- .` o `git restore .` | Cambios sin guardar en todos los archivos. | `git stash push -m "<motivo>"`, o restaurar un archivo puntual que la persona nombró. |
| `git branch -D <rama>` | Commits de esa rama que no están en main. | `git branch -d <rama>`, que se niega si falta integrar. |
| `git push origin --delete <rama>` sin integrar | La rama en GitHub y su PR abierta. | Cerrar la PR con un comentario y dejar la rama, o preguntar. |
| `rm -rf .git`, borrar la carpeta, reclonar | Todo el historial y el trabajo local sin subir. | Crear una rama nueva desde main para «empezar de cero» sin perder nada. |
| `gh repo delete` | El repositorio en GitHub, sus PRs e issues. Irreversible. | `gh repo archive`, que lo deja de solo lectura. |
| `git commit --amend` o `git rebase -i` sobre commits ya subidos | Obliga a hacer force push. | Un commit nuevo que corrige. |

## «Borra todo y empieza de cero»

No ejecutes nada. Pregunta qué quiere decir:

1. ¿Descartar los cambios de hoy que no están guardados?
2. ¿Volver a como estaba main antes de esta rama?
3. ¿Rehacer el diseño desde cero pero conservar el historial?
4. ¿Borrar el repositorio entero?

Para 1 a 3 propone una rama nueva desde main y deja la anterior como respaldo. Solo si la persona elige 4 y confirma después de saber qué se pierde, sigue la tabla de arriba.

## Seguros, que puedes usar sin preguntar

`git status`, `git diff`, `git log --oneline --graph`, `git branch -vv`, `git remote -v`, `git fetch`, `git switch <rama existente>`, `git switch -c <rama nueva>`, `git add <archivo revisado>`, `git commit`, `git push -u origin <tu rama>`, `git pull` en main, `git stash push -m`, `gh pr list`, `gh pr view`, `gh pr diff`, `gh pr create`.

## Configuración para dueños del repo

Comprueba el permiso:

```bash
gh repo view --json nameWithOwner,viewerPermission,visibility
```

Proteger main (necesita repo público o un plan de pago en privados). Exige PR con una aprobación y bloquea force push y borrado:

```bash
gh api -X PUT "repos/{owner}/{repo}/branches/main/protection" --input - <<'JSON'
{
  "required_status_checks": null,
  "enforce_admins": true,
  "required_pull_request_reviews": { "required_approving_review_count": 1 },
  "restrictions": null,
  "allow_force_pushes": false,
  "allow_deletions": false
}
JSON
```

Si la persona trabaja sola, `required_approving_review_count` puede ser `0`. Así sigue exigiendo PR sin bloquearla. `enforce_admins: true` aplica las reglas también al dueño.

Ver y ajustar permisos:

```bash
gh api "repos/{owner}/{repo}/collaborators" --jq '.[] | {login, role_name}'
gh api -X PUT "repos/{owner}/{repo}/collaborators/<usuario>" -f permission=push
gh api -X DELETE "repos/{owner}/{repo}/collaborators/<usuario>"
```

`push` es el rol Write, suficiente para proponer cambios. Quitar a alguien es una acción que se confirma antes.

Borrar ramas automáticamente al integrar una PR:

```bash
gh repo edit --delete-branch-on-merge
```

Archivos que conviene ofrecer:

- `README.md` con para qué sirve, cómo usarlo y a quién pedir ayuda.
- `CONTRIBUTING.md` basado en [buenas-practicas.md](buenas-practicas.md).
- `.github/pull_request_template.md` con la plantilla de [plantilla-pr.md](plantilla-pr.md).
- `.github/CODEOWNERS` si hay equipo, por ejemplo `/estilos/ @usuario-diseno`. Para que su aprobación sea obligatoria, agrega `"require_code_owner_reviews": true` dentro de `required_pull_request_reviews`.
