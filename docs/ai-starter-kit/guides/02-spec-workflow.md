# 02 - Spec Workflow

Objetivo: transformar una necesidad vaga en un cambio pequeño, revisable y validado.

## Spec Kit simplificado

Este repo usa Spec Kit, pero con un flujo reducido para no generar demasiados archivos.

## Prompt one-shot o Spec Kit

La diferencia es el alcance.

| Usa | Cuando |
| --- | --- |
| `docs/ai-starter-kit/templates/ai-task-prompt.md` | Cambio chico, claro, validable con un check simple y bajo riesgo de tocar archivos extra. |
| Spec Kit | Alcance ambiguo, varios archivos/flujos, casos borde relevantes o necesidad de acordar criterios antes de editar. |

Puedes usar el template de prompt como input inicial para `$speckit-specify`.

Flujo recomendado:

1. `$speckit-specify`: crea `spec.md`.
2. Revisar y ajustar el spec.
3. `$speckit-plan`: crea `plan.md` con tareas embebidas.
4. `$speckit-implement`: implementa solo lo planificado.
5. `$speckit-review`: revisa diff, checks y criterios de éxito.

Resultado esperado por feature:

```text
specs/001-nombre-feature/
├── spec.md
└── plan.md
```

`tasks.md`, `research.md`, `data-model.md`, `quickstart.md` y `contracts/` quedan como modo avanzado.

Si falta información crítica, el agente debe preguntar antes de cerrar `spec.md` o `plan.md`.

## Ejemplo rápido

```text
$speckit-specify "Agregar filtro por estado a la lista de tareas. Debe permitir ver todas, pendientes y completadas. No cambiar autenticación."

$speckit-plan

$speckit-implement

$speckit-review
```

## Crear spec

```text
$speckit-specify <describe el problema, contexto, restricciones y resultado esperado>
```

El spec debe responder:

- Qué problema se resuelve.
- Qué incluye y qué no incluye.
- Qué usuarios o actores participan.
- Qué requisitos son verificables.
- Qué casos borde importan.
- Cómo se sabrá que quedó bien.

## Crear plan

```text
$speckit-plan
```

El plan debe incluir:

- Archivos leídos y qué se aprendió.
- Archivos que probablemente se tocarán.
- Pasos técnicos pequeños.
- Tareas embebidas.
- Validación.
- Riesgos y fuera de alcance.

## Implementar

```text
$speckit-implement
```

El agente debe leer `spec.md` y `plan.md`, tocar solo los archivos planificados y correr la validación definida.

## Revisar

```text
$speckit-review
```

La review debe verificar:

- Requisitos del spec cubiertos.
- Tareas del plan completas.
- Diff sin cambios fuera de alcance.
- Checks ejecutados o pendientes declarados.
- Sin secretos ni credenciales.

## Templates

Templates relevantes:

- `.specify/templates/overrides/spec-template.md`
- `.specify/templates/overrides/plan-template.md`
- `docs/ai-starter-kit/templates/ai-task-prompt.md`

Para tareas one-shot, usa `docs/ai-starter-kit/templates/ai-task-prompt.md`.

## Criterio de salida del spec

Una tarea está lista para implementar cuando tiene:

- Problema claro.
- Alcance acotado.
- Criterios de aceptación verificables.
- Plan de validación.
- Fuera de alcance explícito.

## Criterio de salida del plan

Un plan está listo cuando tiene:

- Archivos concretos.
- Tareas pequeñas.
- Checks claros.
- Riesgos conocidos.
- Nada fuera de alcance.

## Criterio de salida de la implementación

Una implementación está lista cuando:

- Cumple el spec.
- Sigue el plan o explica desviaciones.
- Tiene checks ejecutados.
- Fue revisada contra el diff.
