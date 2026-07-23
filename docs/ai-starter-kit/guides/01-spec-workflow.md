# 01 - Spec Workflow

Objetivo: transformar una necesidad vaga en un cambio pequeno, revisable y validado.

## Flujo minimo

1. Describe el problema.
2. Define alcance y fuera de alcance.
3. Pide un plan antes de editar.
4. Audita el plan contra el codigo actual.
5. Ejecuta el cambio.
6. Revisa diff, tests y criterios de aceptacion.

## Comandos mentales para el agente

Usa estos nombres como convencion de trabajo, aunque la herramienta no tenga comandos reales con esos nombres.

```text
/plan
```

Pide un plan corto. Debe listar archivos probables, riesgos y checks.

```text
/audit
```

Pide contrastar el plan con el repositorio antes de editar.

```text
/execute
```

Autoriza implementar solo lo necesario.

```text
/review
```

Pide revisar el diff, correr checks y detectar huecos.

## Template rapido de necesidad

Usa `docs/ai-starter-kit/templates/prd-template.md`.

## Prompt base

```text
Necesito implementar: <necesidad>.

Antes de editar:
1. Lee el codigo relevante.
2. Propone un plan corto.
3. Indica archivos que tocaras.
4. Indica como validaras el cambio.

No implementes todavia.
```

## Criterio de salida

Una tarea esta lista para implementar cuando tiene:

- Problema claro.
- Alcance acotado.
- Criterios de aceptacion verificables.
- Plan de validacion.
- Fuera de alcance explicito.
