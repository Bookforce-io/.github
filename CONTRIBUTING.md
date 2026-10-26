# Contribuir en Bookforce.io

Gracias por contribuir. Estas reglas aplican a **todos** los repositorios de la organización; el
detalle está en el repositorio paraguas `bookforce-workspace` → `pautas/`.

## 1. GitHub CLI (`gh`) primero

Toda interacción con GitHub se hace con **`gh`**, no con `git` ni con la web. Usa `git` **solo cuando
`gh` no cubre la operación**: commitear, hacer push de tu rama, worktrees y submódulos.

| Para… | Usa | En lugar de |
| --- | --- | --- |
| Clonar | `gh repo clone Bookforce-io/<repo>` | `git clone https://…` |
| Crear un issue | `gh issue create` | la web |
| Tomar un issue | `gh issue edit <n> --add-assignee @me --add-label "estado: en curso"` | la web |
| Comentar un issue | `gh issue comment <n> --body "…"` | la web |
| Crear un PR | `gh pr create --fill --body "Refs #<n>"` | la web |
| Revisar un PR / CI | `gh pr view`, `gh pr diff`, `gh pr checks` | `git fetch` + `git diff` |
| Traer un PR a local | `gh pr checkout <n>` | `git fetch origin pull/<n>/head` |
| Mergear | `gh pr merge <n> --squash --delete-branch` | `git merge` + `git push` |
| Cerrar un issue validado | `gh issue close <n> --comment "✅ …"` | la web |
| Consultar la API | `gh api repos/Bookforce-io/<repo>/…` | `curl` con token |

`git` es requerido solo para: `git add` / `git commit`, `git push -u origin <rama>`,
`git worktree …`, `git submodule …` y el estado local (`git status -s`, `git diff --stat`).

## 2. Identidad

Commitea **siempre** con tu correo `@bookforce.io`. Verifica antes del primer commit:

```bash
git config user.email   # nombre@bookforce.io
```

Los PR con commits de otros correos no pasan el chequeo `autoria-bookforce`. Para corregir el último
commit: `git commit --amend --reset-author --no-edit`.

## 3. Flujo

Trabaja cada issue en su propio worktree y elimínalo apenas publiques los cambios.

1. **Issue** con la plantilla que corresponda, etiquetas `tipo:` y `prioridad:` y responsable:
   `gh issue create`.
2. **Tómalo y coméntalo** al empezar, indicando la rama:
   `gh issue edit <n> --add-assignee @me --add-label "estado: en curso"` y
   `gh issue comment <n> --body "Tomo esto en fix/<n>-…"`.
3. **Worktree y rama** `tipo/<n>-descripcion` (`fix/42-cupos-duplicados`).
4. **Commits** convencionales con el issue: `fix(reservas): evita cupos duplicados (#42)`.
5. **PR** con la plantilla y `Refs #<n>` (no `Closes`): `gh pr create`. Comenta el enlace en el issue
   y pon `estado: en revisión`.
6. **Validación** por alguien distinto de quien implementó → `estado: validado`.
7. **Merge a la rama productiva** con `gh pr merge` → el issue se cierra con el comentario de dónde
   quedó.
8. **Changelog** actualizado en la wiki del repositorio.
9. **Elimina el worktree** en cuanto los cambios estén publicados.

## 4. Nunca

- Push directo a la rama productiva.
- Cerrar un issue sin validación o antes de que el cambio esté en la rama productiva.
- Subir secretos (`.env`, llaves, tokens). Usa `.env.example`.
- Agregar `Co-Authored-By` o atribuciones automáticas (de IA o de herramientas) en commits y PR.
