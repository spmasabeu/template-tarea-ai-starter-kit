# 04 - CI/CD y Render

Objetivo: automatizar checks minimos y desplegar de forma repetible.

## Checks minimos

Antes de depender de CI, el proyecto debe tener comandos locales claros.

Ejemplos:

```bash
bin/rails test
bin/rubocop
bin/brakeman
```

Usa los comandos reales del repositorio. No agregues herramientas nuevas si el template ya trae checks suficientes.

## GitHub Actions

El workflow debe hacer lo mismo que un estudiante puede ejecutar localmente:

1. Instalar dependencias.
2. Preparar base de datos si aplica.
3. Ejecutar tests.
4. Ejecutar lint o analisis estatico.

## Leer fallos

Orden recomendado:

1. Primer error real.
2. Archivo y linea.
3. Comando que fallo.
4. Diferencia entre local y CI.

Prompt util:

```text
Analiza este fallo de CI. Dime la causa probable, el archivo a revisar y el cambio minimo. No edites todavia.
```

## Render

Configuracion esperada:

- Servicio conectado al repositorio.
- Rama de deploy acordada.
- Comando de build documentado.
- Comando de start documentado.
- Variables de entorno definidas en Render, no en Git.

## Checklist

- [ ] Tests locales pasan.
- [ ] Workflow de GitHub Actions pasa.
- [ ] Render despliega desde la rama acordada.
- [ ] Variables de entorno estan fuera del repositorio.
- [ ] URL de despliegue verificada.
