# Contribuir en Bookforce.io

Gracias por contribuir. Estas reglas aplican a **todos** los repositorios de la organización; el
detalle está en el repositorio paraguas `bookforce-workspace` → `pautas/`.

## 1. Identidad

Commitea **siempre** con tu correo `@bookforce.io`. Verifica antes del primer commit:

```bash
git config user.email   # nombre@bookforce.io
```

Los PR con commits de otros correos no pasan el chequeo `autoria-bookforce`. Para corregir el último
commit: `git commit --amend --reset-author --no-edit`.

## 2. Flujo

1. **Issue** con la plantilla que corresponda, etiquetas `tipo:` y `prioridad:` y responsable.
2. Comenta en el issue al empezar (`estado: en curso`) indicando la rama.
3. **Rama** `tipo/<n>-descripcion` (`fix/42-cupos-duplicados`).
4. **Commits** convencionales con el issue: `fix(reservas): evita cupos duplicados (#42)`.
5. **PR** con la plantilla y `Refs #<n>` (no `Closes`). Comenta el enlace en el issue
   (`estado: en revisión`).
6. **Validación** por alguien distinto de quien implementó → `estado: validado`.
7. **Merge a la rama productiva** → el issue se cierra con el comentario de dónde quedó.
8. **Changelog** actualizado en la wiki del repositorio.

## 3. Nunca

- Push directo a la rama productiva.
- Cerrar un issue sin validación o antes de que el cambio esté en la rama productiva.
- Subir secretos (`.env`, llaves, tokens). Usa `.env.example`.
- Agregar `Co-Authored-By` o atribuciones automáticas (de IA o de herramientas) en commits y PR.
