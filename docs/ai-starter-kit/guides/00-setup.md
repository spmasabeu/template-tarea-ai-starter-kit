# 00 - Setup

Objetivo: dejar el repositorio, GitHub Copilot Student y OpenCode listos para una primera tarea asistida por IA.

Estado de referencia: verificado el 22 de julio de 2026 contra documentacion publica de GitHub y OpenCode.

## 1. Preparar GitHub Student

1. Entra a <https://github.com/settings/education/benefits>.
2. Si GitHub aun no reconoce tu cuenta como estudiante, inicia la postulacion.
3. Activa GitHub Copilot Student desde los beneficios educacionales.
4. Revisa tu plan en la configuracion de Copilot.

GitHub indica que estudiantes verificados acceden sin costo a Copilot Student y que la elegibilidad se reevalua mensualmente.

## 2. Clonar el repositorio

Usa tu fork personal del template.

```bash
git clone <URL_DE_TU_FORK>
cd <NOMBRE_DEL_REPO>
git status
```

Resultado esperado: `git status` muestra una rama limpia antes de empezar.

## 3. Instalar OpenCode

Elige una opcion segun tu entorno.

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

## 4. Conectar Copilot con OpenCode

Camino recomendado:

```bash
opencode
```

Dentro de OpenCode:

```text
/connect
```

Selecciona GitHub Copilot, completa el login de dispositivo y vuelve a la terminal.

Si tu version de OpenCode usa comandos de autenticacion directa:

```bash
opencode auth github
```

## 5. Probar el agente

Desde la raiz del repositorio:

```bash
opencode
```

Prompt de prueba:

```text
Lee el README y dime que comandos minimos necesito para levantar este proyecto. No edites archivos.
```

Resultado esperado:

- OpenCode responde usando contexto del repositorio.
- No aparecen errores de autenticacion.
- No se crean cambios en Git.

Comprueba:

```bash
git status
```

## 6. Si Copilot Student no aparece en OpenCode

GitHub documenta Copilot Student como beneficio gratuito para estudiantes verificados, pero el anuncio de soporte oficial de OpenCode menciona explicitamente Copilot Pro, Pro+, Business y Enterprise. Si tu cuenta Student no autentica en OpenCode:

1. Confirma que Copilot funciona en GitHub o en VS Code.
2. Actualiza OpenCode.
3. Repite `/connect`.
4. Si sigue fallando, usa Copilot en el IDE para esta etapa y reporta el caso al equipo docente.

No agregues tokens personales al repositorio. Si usas un proveedor alternativo, guarda claves solo en variables de entorno locales.

## 7. Checklist de entrega

- [ ] Fork creado.
- [ ] Repositorio clonado.
- [ ] GitHub Education activo.
- [ ] Copilot Student activo.
- [ ] OpenCode instalado.
- [ ] OpenCode conectado a GitHub Copilot o alternativa acordada.
- [ ] Prompt de prueba ejecutado sin editar archivos.

## Fuentes

- GitHub Docs: <https://docs.github.com/en/copilot/how-tos/copilot-on-github/set-up-copilot/enable-copilot/set-up-for-students>
- GitHub Copilot licenses: <https://docs.github.com/en/billing/concepts/product-billing/github-copilot-licenses>
- GitHub Changelog OpenCode: <https://github.blog/changelog/2026-01-16-github-copilot-now-supports-opencode/>
- OpenCode docs: <https://opencode-ai.com/en/docs.html>
