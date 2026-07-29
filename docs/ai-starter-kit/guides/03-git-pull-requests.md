# 03 - Git y Pull Requests

Objetivo: entregar cambios pequeños, trazables y fáciles de revisar.

## Gitflow mínimo

Para el curso, usa un flujo simple:

1. Actualiza `main`.
2. Crea una rama corta desde `main`.
3. Haz commits pequeños.
4. Abre PR hacia `main`.
5. Corrige feedback.
6. Fusiona cuando esté aprobado y los checks pasen.

No trabajes directo sobre `main`. No usamos rama `stage` por defecto; agrégala solo si el equipo necesita probar integraciones antes de llegar a `main`.

## Ramas

- `main`: versión estable.
- `feature/<tema>`: nueva funcionalidad.
- `fix/<tema>`: corrección.
- `docs/<tema>`: documentación.
- `chore/<tema>`: mantención sin cambio funcional.

Ejemplos:

```bash
git switch main
git pull
git switch -c docs/setup-opencode
git switch -c feature/login
git switch -c fix/navbar-mobile
git switch -c chore/update-deps
git push -u origin <rama>
```

Regla práctica: nombre corto, en minúsculas, separado por guiones, y asociado al cambio.

## Commits

Un commit debe explicar una unidad de cambio.

Formato sugerido:

```text
tipo: resumen corto
```

Tipos útiles:

- `feat`: funcionalidad.
- `fix`: corrección.
- `docs`: documentación.
- `test`: pruebas.
- `refactor`: cambio interno sin comportamiento nuevo.
- `chore`: mantención, dependencias o configuración.

Ejemplo:

```text
docs: add opencode setup guide
```

Buenos commits:

- Tocan una idea.
- Se pueden revertir sin romper cambios no relacionados.
- No mezclan formato, feature y fixes en el mismo commit.

## Antes de abrir PR

```bash
git status
git diff
```

Revisa:

- Que el diff solo contiene lo que querías cambiar.
- Que no hay secretos ni archivos temporales.
- Que corriste los checks que correspondan.
- Que el branch está actualizado contra `main` si hubo cambios recientes.

## Pull Request

Usa `.github/pull_request_template.md`. La copia de referencia vive en `docs/ai-starter-kit/templates/pull-request-template.md`.

Un buen PR responde:

- Contexto del problema: qué se intenta resolver y dónde nace la necesidad. Si usaste Spec Kit, enlaza `spec.md` o `plan.md` desde `specs/YYYYMMDD-HHMMSS-nombre-feature/`.
- Implementación: qué se cambió y qué archivos o flujos toca.
- Validación: comandos, pruebas manuales y criterios cubiertos.
- Impacto y riesgos: qué podría romperse y qué queda fuera.

Tamaño recomendado: chico. Si el PR necesita mucha explicación para ser revisable, probablemente conviene partirlo.

## Revisión con IA

Prompt recomendado:

```text
Revisa este diff como code review. Prioriza bugs, riesgos, cambios no pedidos y tests faltantes. No propongas refactors grandes si no bloquean la entrega.
```

Antes de mergear:

- [ ] PR apunta a `main`.
- [ ] Template completo.
- [ ] Checks pasaron o pendientes explicados.
- [ ] Feedback resuelto.
- [ ] No hay cambios fuera de alcance.

## Fuentes

- GitHub pull requests: <https://docs.github.com/en/pull-requests>
- GitHub protected branches: <https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches>
