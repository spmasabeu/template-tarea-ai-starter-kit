# Template Tarea AI Starter Kit

Starter kit Rails para trabajar tareas del curso con apoyo de IA, PRs revisables, CI en GitHub Actions y deploy en Render.

## Por donde partir

Lee las guías en orden:

1. [00 - Setup](docs/ai-starter-kit/guides/00-setup.md)
2. [01 - AI Tools](docs/ai-starter-kit/guides/01-ai-tools.md)
3. [02 - Spec Workflow](docs/ai-starter-kit/guides/02-spec-workflow.md)
4. [03 - Git y Pull Requests](docs/ai-starter-kit/guides/03-git-pull-requests.md)
5. [04 - CI/CD y Render](docs/ai-starter-kit/guides/04-ci-cd-render.md)

Índice corto: [docs/ai-starter-kit](docs/ai-starter-kit/README.md).

## Comandos base

```bash
bin/setup
bin/rails server
bin/rails test
bin/ci
```

`bin/ci` corre el mismo chequeo que usa GitHub Actions: setup, tests, RuboCop y Brakeman.

## Flujo esperado

1. Trabaja en una rama corta desde `main`.
2. Usa IA con contexto del repo y cambios pequeños.
3. Abre PR hacia `main`.
4. Espera CI verde y revisión.
5. Mergea a `main`.
6. Render despliega desde `main`.

No guardes tokens, API keys ni credenciales en Git.
