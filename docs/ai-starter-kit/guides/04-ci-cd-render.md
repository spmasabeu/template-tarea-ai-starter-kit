# 04 - CI/CD y Render

Objetivo: correr checks automáticos en cada PR y desplegar en Render solo desde `main`.

## Flujo esperado

1. Trabaja en una rama `feature/`, `fix/`, `docs/` o `chore/`.
2. Abre un PR hacia `main`.
3. GitHub Actions corre CI.
4. Si CI está verde, revisa y mergea a `main`.
5. Render detecta el cambio en `main`, ejecuta build y despliega.

No despliegues ramas de trabajo por defecto. Para este curso, `main` es la rama estable y la fuente del deploy.

## Checks locales

Antes de abrir PR, corre el mismo chequeo que usará CI:

```bash
bin/ci
```

Ese comando ejecuta:

- `bin/setup --skip-server`
- `bin/rails test`
- `bin/rubocop`
- `bin/brakeman --quiet --no-pager --exit-on-warn --exit-on-error`

Si necesitas aislar un fallo:

```bash
bin/rails test
bin/rubocop
bin/brakeman
```

## GitHub Actions

El workflow vive en `.github/workflows/ci.yml` y corre en:

- cada PR;
- cada push a `main`.

La regla práctica: si falla CI, no se mergea. Primero se arregla el fallo en la misma rama del PR.

## Leer fallos

Orden recomendado:

1. Primer error real.
2. Comando que falló.
3. Archivo y línea.
4. Diferencia entre local y CI.

Prompt útil:

```text
Analiza este fallo de CI. Dime la causa probable, el archivo a revisar y el cambio mínimo. No edites todavía.
```

## Render

Configuración esperada:

- Servicio conectado al repo de GitHub.
- Rama de deploy: `main`.
- Auto deploy activado para `main`.
- Build command: `./bin/render-build.sh`.
- Pre-deploy command: `./bin/rails db:migrate`.
- Start command: `./bin/rails server`.
- Variables de entorno definidas en Render, no en Git.

Render ejecuta build, luego pre-deploy y finalmente start. Si falla una etapa, el deploy falla y sigue viva la última versión correcta.

Nota: `Pre-deploy Command` requiere un servicio pagado. Si usan plan free, mueve `bundle exec rails db:migrate` al final de `bin/render-build.sh`.

El script `bin/render-build.sh` instala gems, compila assets y limpia assets antiguos. No guarda secretos ni configura producción.

Si el proyecto usa Docker, Render debe construir con el `Dockerfile` del repo y el build/start se definen desde la configuración del servicio.

## Variables de entorno

Mantén secretos fuera del repositorio. En Render configura, según corresponda:

- `RAILS_MASTER_KEY`
- `DATABASE_URL`
- claves de proveedores externos

Resend queda fuera de este manual por ahora. Cuando se use correo transaccional, agrega la API key solo en Render y documenta el flujo en una sección específica.

## Checklist

- [ ] `bin/ci` pasa localmente.
- [ ] PR apunta a `main`.
- [ ] GitHub Actions pasa.
- [ ] PR aprobado y mergeado.
- [ ] Render despliega desde `main`.
- [ ] `bin/render-build.sh` está configurado como build command.
- [ ] Variables de entorno están en Render, no en Git.
- [ ] URL de despliegue verificada.

## Fuentes

- Render deploys: <https://render.com/docs/deploys>
- Render Rails 8: <https://render.com/docs/deploy-rails-8>
