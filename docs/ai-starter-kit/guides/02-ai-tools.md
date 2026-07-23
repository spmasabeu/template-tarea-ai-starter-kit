# 02 - AI Tools

Objetivo: usar IA con contexto suficiente, permisos minimos y cambios revisables.

## Contexto durable

`AGENTS.md` sirve para instrucciones permanentes del repositorio: stack, comandos, estilo, restricciones y flujo de trabajo.

No pongas secretos, tokens ni datos personales.

## Prompts temporales

Usa prompts largos solo para la tarea actual. Cuando una instruccion se repite en varias tareas, considera moverla a `AGENTS.md`.

## Skills y workflows

Una skill es una receta reutilizable para una familia de tareas. Agregala solo si el equipo la usara varias veces.

Ejemplos razonables:

- Revisar un PR.
- Preparar una entrega.
- Diagnosticar un test fallido.

Ejemplos que no conviene guardar:

- Una pregunta puntual.
- Un bug unico.
- Una preferencia personal no compartida.

## MCP y permisos

Conecta herramientas externas solo cuando aportan al trabajo.

Regla minima:

- Leer antes que escribir.
- Pedir permiso antes de acciones destructivas.
- No entregar acceso amplio si basta acceso al repositorio.
- Desconectar integraciones que no se usaran en la tarea.

## Modelo y costo

Empieza con el modelo recomendado por la herramienta. Sube a un modelo mas capaz solo cuando:

- El agente no entiende el codigo.
- La tarea cruza varios archivos.
- Hay decisiones de arquitectura.
- La primera respuesta falla de forma clara.

## Prompt de uso responsable

```text
Trabaja con cambios pequenos. Antes de modificar archivos, dime que leiste y que tocaras. Despues de editar, muestra el resumen del diff y los checks ejecutados.
```
