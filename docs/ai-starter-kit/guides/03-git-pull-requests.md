# 03 - Git y Pull Requests

Objetivo: entregar cambios pequenos, trazables y faciles de revisar.

## Gitflow minimo

Ramas:

- `main`: version estable.
- `feature/<tema>`: nueva funcionalidad.
- `fix/<tema>`: correccion.
- `docs/<tema>`: documentacion.

Ejemplos:

```bash
git switch -c docs/setup-opencode
git switch -c feature/login
git switch -c fix/navbar-mobile
```

## Commits

Un commit debe explicar una unidad de cambio.

Formato sugerido:

```text
tipo: resumen corto
```

Tipos utiles:

- `feat`: funcionalidad.
- `fix`: correccion.
- `docs`: documentacion.
- `test`: pruebas.
- `refactor`: cambio interno sin comportamiento nuevo.

Ejemplo:

```text
docs: add opencode setup guide
```

## Antes de abrir PR

```bash
git status
git diff
```

Ejecuta los checks que correspondan al proyecto.

## Pull Request

Usa `.github/pull_request_template.md`.

Un buen PR responde:

- Que cambia.
- Por que cambia.
- Como se valido.
- Que queda fuera.

## Revision con IA

Prompt recomendado:

```text
Revisa este diff como code review. Prioriza bugs, riesgos, cambios no pedidos y tests faltantes. No propongas refactors grandes si no bloquean la entrega.
```
