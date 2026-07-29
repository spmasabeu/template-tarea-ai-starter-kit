# 00 - Setup

Objetivo: dejar el repositorio y al menos una herramienta de IA en terminal lista para una primera tarea asistida.

Estado de referencia: verificado el 28 de julio de 2026 contra documentación pública de GitHub, OpenCode, OpenAI, Anthropic y NVIDIA.

## 1. Preparar cuentas

Mínimo recomendado:

- GitHub Student: <https://github.com/settings/education/benefits>
- GitHub Copilot: <https://github.com/settings/copilot>

Opcional para más créditos/modelos:

- NVIDIA Build: crea una cuenta en <https://build.nvidia.com/> y genera un `NVIDIA_API_KEY`.

No subas tokens ni claves al repositorio. Usa variables de entorno locales.

## 2. Clonar el repositorio

Usa tu fork personal del template.

```bash
git clone <URL_DE_TU_REPO>
cd <NOMBRE_DEL_REPO>
git status
```

Resultado esperado: `git status` muestra una rama limpia antes de empezar.

## 3. Preparar entorno

Linux, macOS y WSL pueden seguir los mismos comandos base. En Windows, instala WSL primero y trabaja dentro de Ubuntu:

```powershell
wsl --install
```

Luego abre Ubuntu y continúa con los pasos de Linux.

## 4. Instalar herramientas

Instala solo las que vayas a probar.

OpenCode:

```bash
curl -fsSL https://opencode.ai/install | bash
```

Alternativas:

```bash
npm i -g opencode-ai
brew install anomalyco/tap/opencode
```

Verifica:

```bash
opencode --version
```

GitHub Copilot CLI:

```bash
npm install -g @github/copilot
gh auth login --web
gh copilot
```

Codex:

```bash
npm install -g @openai/codex
codex
```

Claude Code:

```bash
npm install -g @anthropic-ai/claude-code
claude
```

## 5. Configuración compartida

Cada agente tiene su propia configuración, pero todos pueden compartir instrucciones de proyecto:

- `AGENTS.md`: instrucciones portables del repo. Codex, OpenCode y Copilot CLI pueden leerlo directo.
- `CLAUDE.md`: archivo de Claude Code. En este repo solo importa `@AGENTS.md` para no duplicar reglas.
- `opencode.json` o `.opencode/agents/`: configuración específica de OpenCode, modelos, permisos y agentes.
- `~/.codex/config.toml`, `~/.claude/` y `~/.copilot/`: configuración personal. No se commitea.

Usa `AGENTS.md` para reglas comunes: comandos, estilo, seguridad y flujo de trabajo. Usa configs específicas solo cuando una herramienta necesite permisos, modelos o proveedores propios.

Regla práctica: si todos los estudiantes necesitan la misma instrucción, va en el repo. Si depende de tu cuenta, tu máquina o tus preferencias, va en `~/...`.

Ejemplos:

- Repo: comandos para levantar la app, checklist de entrega, convenciones de commits, instrucciones para no subir claves.
- Local: tokens, modelo por defecto, permisos personales, MCPs privados, rutas de tu máquina.

## 6. Conectar proveedores

OpenCode no depende de GitHub Student. Conéctalo con el proveedor que tengas disponible:

```bash
opencode
```

Dentro de OpenCode usa:

```text
/connect
```

Opciones útiles:

- `NVIDIA`: usa el `NVIDIA_API_KEY` de Build para probar modelos gratuitos.
- `Anthropic`, `OpenAI` u otro proveedor: usa una clave personal si tienes créditos.

También puedes dejar NVIDIA como variable local:

```bash
export NVIDIA_API_KEY="nvapi-..."
```

## 7. Probar el agente

Desde la raíz del repositorio:

```bash
opencode
```

Prompt de prueba:

```text
Lee el README y dime qué comandos mínimos necesito para levantar este proyecto. No edites archivos.
```

Resultado esperado:

- La herramienta responde usando contexto del repositorio.
- No aparecen errores de autenticación.
- No se crean cambios en Git.

Comprueba:

```bash
git status
```

## 8. Checklist de entrega

- [ ] Fork creado.
- [ ] Repositorio clonado.
- [ ] Entorno Linux, macOS o WSL listo.
- [ ] GitHub Education activo.
- [ ] Copilot CLI, OpenCode, Codex o Claude instalado.
- [ ] Al menos una herramienta autenticada.
- [ ] `AGENTS.md` leído por la herramienta elegida.
- [ ] Prompt de prueba ejecutado sin editar archivos.

## Fuentes

- GitHub Docs: <https://docs.github.com/en/copilot/how-tos/copilot-on-github/set-up-copilot/enable-copilot/set-up-for-students>
- GitHub Copilot CLI: <https://docs.github.com/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli>
- OpenCode providers: <https://opencode.ai/docs/providers>
- OpenCode agents: <https://opencode.ai/docs/agents/>
- Codex CLI: <https://www.npmjs.com/package/@openai/codex>
- Codex AGENTS.md: <https://learn.chatgpt.com/docs/agent-configuration/agents-md.md>
- Claude Code: <https://docs.anthropic.com/en/docs/claude-code/getting-started>
- Claude memory: <https://code.claude.com/docs/en/memory>
- NVIDIA Build: <https://build.nvidia.com/>
