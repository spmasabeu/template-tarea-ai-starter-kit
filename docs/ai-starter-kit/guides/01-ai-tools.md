# 01 - AI Tools

Objetivo: usar IA con contexto suficiente, permisos mínimos y cambios revisables.

## AGENTS.md

`AGENTS.md` es el contexto durable del repo. Sirve para que distintos agentes partan con las mismas reglas: stack, comandos, estilo, restricciones y flujo de trabajo.

No pongas secretos, tokens ni datos personales.

Qué conviene poner:

- Cómo levantar, testear y revisar el proyecto.
- Reglas de seguridad: no subir claves, pedir permiso para acciones destructivas.
- Convenciones del curso: cambios pequeños, diffs revisables, criterios de entrega.
- Contexto que un estudiante o agente tendría que leer en cada tarea.

Qué no conviene poner:

- Tokens, API keys o credenciales.
- Preferencias personales de una máquina.
- Instrucciones largas para una tarea única.

Claude Code usa `CLAUDE.md`, por eso este repo tiene un `CLAUDE.md` que importa `@AGENTS.md`. Así evitamos duplicar reglas.

## Prompting de tarea

Usa prompts largos solo para la tarea actual. Cuando una instrucción se repite en varias tareas, considera moverla a `AGENTS.md`.

Template base: `docs/ai-starter-kit/templates/ai-task-prompt.md`.

Estructura mínima de un buen prompt:

- Rol: qué tipo de agente necesitas.
- Conocimiento esperado: qué debe leer o considerar.
- Problema: qué hay que resolver.
- Contexto: dónde ocurre y por qué importa.
- Restricciones: qué no puede tocar, cambiar o asumir.
- Resultado esperado: qué debe entregar.
- Output: formato de respuesta, si importa.
- Criterios de éxito: cómo sabremos que quedó bien.
- Review: qué debe verificar antes de cerrar.

Usa esta estructura para un cambio one-shot o como input inicial para crear un spec.

## Skills y workflows

Una skill es una receta reutilizable para una familia de tareas. Agrégala solo si el equipo la usará varias veces.

Ejemplos razonables:

- Revisar un PR.
- Preparar una entrega.
- Diagnosticar un test fallido.

Ejemplos que no conviene guardar:

- Una pregunta puntual.
- Un bug único.
- Una preferencia personal no compartida.

Dónde pueden vivir:

- Proyecto: `.agents/skills/<nombre>/SKILL.md`, `.claude/skills/<nombre>/SKILL.md` o `.opencode/skills/<nombre>/SKILL.md`.
- Personal: `~/.agents/skills/`, `~/.claude/skills/`, `~/.config/opencode/skills/` o `~/.codex/skills/`.

Repos útiles para explorar:

- `openai/skills`: skills para Codex.
- `anthropics/skills`: skills compatibles con Claude.
- `github/awesome-copilot`: colección comunitaria para Copilot.

Crea una skill propia cuando notes que estás copiando el mismo prompt, checklist o procedimiento en varias tareas.

## MCP y permisos

MCP conecta el agente con herramientas externas: GitHub, Notion, Render, bases de datos, navegadores o APIs internas.

Regla mínima:

- Leer antes que escribir.
- Pedir permiso antes de acciones destructivas.
- No entregar acceso amplio si basta acceso al repositorio.
- Desconectar integraciones que no se usarán en la tarea.

Ejemplo práctico: Render MCP permite listar servicios, revisar logs, disparar deploys o consultar métricas desde el agente.

Codex con OAuth:

```bash
codex mcp add render --url https://mcp.render.com/mcp --oauth-client-id codex
```

Claude Code con OAuth:

```bash
claude mcp add --transport http --client-id claude render https://mcp.render.com/mcp
```

Prompt de prueba:

```text
Lista mis servicios de Render y dime cuál fue el último deploy del servicio web. No modifiques nada.
```

OpenCode con API key local, en `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "servers": {
      "render": {
        "type": "remote",
        "url": "https://mcp.render.com/mcp",
        "oauth": false,
        "headers": {
          "Authorization": "Bearer {env:RENDER_API_KEY}"
        }
      }
    }
  }
}
```

Guarda `RENDER_API_KEY` como variable de entorno, no en el repo.

## Modelo y costo

Empieza con el modelo recomendado por la herramienta. Sube a un modelo más capaz o a mayor esfuerzo solo cuando:

- El agente no entiende el código.
- La tarea cruza varios archivos.
- Hay decisiones de arquitectura.
- La primera respuesta falla de forma clara.

Regla práctica:

| Caso | OpenAI/Codex | Claude | Uso esperado |
| --- | --- | --- | --- |
| Pregunta corta o cambio trivial | modelo económico, esfuerzo bajo | Haiku | Respuestas rápidas, bajo costo |
| Trabajo diario de código | GPT-5.6 Terra o similar, esfuerzo medio | Sonnet | Buen balance costo/calidad |
| Problema difícil o refactor grande | GPT-5.6 Sol, esfuerzo alto | Opus | Más razonamiento, más tokens |
| Mucho contexto | variante con contexto largo si existe | Sonnet/Opus 1M | Leer repos, trazas o docs extensos |

No elijas por nombre solamente. El costo real depende de tokens de entrada, tokens de salida, contexto cargado y esfuerzo de razonamiento. Para una tarea chica, un modelo robusto puede ser desperdicio; para una tarea ambigua o de arquitectura, un modelo barato puede salir caro si falla y hay que repetir.

## Prompt de uso responsable

```text
Trabaja con cambios pequeños. Antes de modificar archivos, dime qué leíste y qué tocarás. Después de editar, muestra el resumen del diff y los checks ejecutados.
```

## Checklist de uso

- [ ] `AGENTS.md` tiene reglas comunes del repo.
- [ ] El prompt usa el template cuando la tarea no es trivial.
- [ ] La herramienta tiene solo los permisos necesarios.
- [ ] Los MCP conectados son relevantes para la tarea.
- [ ] El modelo elegido calza con dificultad, contexto y costo.
- [ ] El agente entrega diff, checks y riesgos antes de cerrar.

## Fuentes

- Codex AGENTS.md: <https://learn.chatgpt.com/docs/agent-configuration/agents-md.md>
- OpenCode skills: <https://opencode.ai/docs/skills/>
- OpenCode agents: <https://opencode.ai/docs/agents/>
- OpenCode MCP: <https://opencode.ai/v2/docs/mcp-servers>
- GitHub agent skills: <https://docs.github.com/en/copilot/concepts/agents/about-agent-skills>
- Claude Code skills: <https://code.claude.com/docs/en/slash-commands>
- Claude models: <https://code.claude.com/docs/en/model-config>
- OpenAI model guidance: <https://developers.openai.com/api/docs/guides/latest-model>
- Render MCP: <https://render.com/docs/mcp-server>
