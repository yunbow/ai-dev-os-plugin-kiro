# AI Dev OS Plugin — Kiro

[![Lint & Link Check](https://github.com/yunbow/ai-dev-os-plugin-kiro/actions/workflows/lint.yml/badge.svg)](https://github.com/yunbow/ai-dev-os-plugin-kiro/actions/workflows/lint.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](../../../LICENSE)

Un plugin de Kiro que integra el modelo de 4 capas de AI Dev OS en el sistema de Steering Rules y Hooks de Kiro.

**Parte de [AI Dev OS](https://github.com/yunbow/ai-dev-os)** — un framework para convertir conocimiento tácito en reglas de codificación AI ejecutables ([Lifespan Layers](https://github.com/yunbow/ai-dev-os#lifespan-layers--the-4-layer-model)).
Requiere [AI Dev OS Rules](https://github.com/yunbow/ai-dev-os-rules-typescript) configurado en tu proyecto.

## ¿Por qué este plugin?

Integra las directrices de AI Dev OS en el **sistema de steering de Kiro**:

- **11 Steering Rules** — `#ai-dev-os-check`, `#ai-dev-os-scan`, `#ai-dev-os-extract` y más
- **3 Auto Steering** — Asesor de filosofía, verificador de principios, auditor de directrices
- **2 File Match Rules** — Verificación automática en archivos de código, advertencias de dependencia L1-L2
- **Configuración con un comando** — `npx ai-dev-os init --rules typescript --plugin kiro`

![AI Dev OS Check & Fix Report](../../../docs/images/ai-dev-os-check.png)

## Inicio rápido

```bash
npx ai-dev-os init --rules typescript --plugin kiro
```

> El CLI agrega submódulos, copia la plantilla AGENTS.md y copia las reglas de steering y hooks a `.kiro/` automáticamente.
> Consulta [AI Dev OS CLI](https://github.com/yunbow/ai-dev-os-cli) para más detalles.

Requisitos: [Kiro](https://kiro.dev/) >= 1.0.0 y archivos de capas AI Dev OS (L1-L3) en tu proyecto ([TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python)).

<details>
<summary>Configuración manual</summary>

**Opción A: Submódulo**

```bash
# 1. Agregar reglas de AI Dev OS como submódulo
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os
# Para proyectos Python:
# git submodule add https://github.com/yunbow/ai-dev-os-rules-python.git docs/ai-dev-os

# 2. Agregar este plugin como submódulo
git submodule add https://github.com/yunbow/ai-dev-os-plugin-kiro.git .kiro/plugins/ai-dev-os
cp -r .kiro/plugins/ai-dev-os/steering/ .kiro/steering/
cp -r .kiro/plugins/ai-dev-os/hooks/ .kiro/hooks/
```

**Opción B: Copia directa**

```bash
# 1. Agregar reglas como submódulo (igual que arriba)
git submodule add https://github.com/yunbow/ai-dev-os-rules-typescript.git docs/ai-dev-os

# 2. Clonar y copiar archivos del plugin
git clone https://github.com/yunbow/ai-dev-os-plugin-kiro.git
cp -r ai-dev-os-plugin-kiro/steering/ .kiro/steering/
cp -r ai-dev-os-plugin-kiro/hooks/ .kiro/hooks/
```

3. Invoca `#ai-dev-os-init` en el chat de Kiro para configurar la estructura de 4 capas
4. Comienza a codificar — las reglas de steering y hooks te guiarán automáticamente

Consulta la [Guía de operación](./operation-guide.md) para instrucciones detalladas.

</details>

## Steering Rules

### Manual Steering (invocar con `#name` en el chat)

| Regla de Steering | Invocación | Descripción |
|-------------------|------------|-------------|
| **Init** | `#ai-dev-os-init` | Asistente de configuración — introduce AI Dev OS en un proyecto en 30 minutos |
| **Check** | `#ai-dev-os-check` | Verifica cambios de código contra directrices (soporta `git diff`, staging, comparación de ramas) |
| **Scan** | `#ai-dev-os-scan` | Escaneo completo de cumplimiento de TODOS los archivos fuente del proyecto |
| **Review** | `#ai-dev-os-review` | Auto-revisión pre-PR combinando cumplimiento L3 + revisión de diseño L2 + alineación L1 |
| **Extract** | `#ai-dev-os-extract` | Extrae nuevas reglas de diffs de revisión de código (Rule Harvesting) |
| **Why** | `#ai-dev-os-why` | Rastrea una regla a través de L3→L2→L1 para explicar su fundamento |
| **Plan** | `#ai-dev-os-plan` | Crea un plan de implementación con checklists de directrices antes de codificar |
| **Ticket** | `#ai-dev-os-ticket` | Genera un ticket (archivo local o GitHub Issue) con resumen de implementación y candidatos de checklist |
| **Audit** | `#ai-dev-os-audit` | Audita la salud de 4 capas: regla de dependencia, frescura, cobertura, consistencia |
| **Evolve** | `#ai-dev-os-evolve` | Analiza commits recientes para proponer actualizaciones L1-L2 (espiral SECI) |
| **Report** | `#ai-dev-os-report` | Genera resumen de cumplimiento para equipos e interesados |

### Auto Steering (activado automáticamente)

| Regla de Steering | Activación | Descripción |
|-------------------|------------|-------------|
| `philosophy-advisor` | Decisiones de arquitectura/diseño | Soporte de juicio basado en L1 |
| `principle-checker` | Discusiones de cambios de código | Verificación de alineación L2 |
| `guideline-auditor` | Discusiones de mantenimiento de directrices | Auditoría de cobertura y consistencia L3 |

### File Match Steering (activado en archivos coincidentes)

| Regla de Steering | Patrón de archivo | Descripción |
|-------------------|------------------|-------------|
| `guideline-compliance` | `**/*.{ts,tsx,py,go,js,jsx}` | Verificación ligera de directrices en archivos de código |
| `layer-dependency` | `**/01_philosophy/**`, `**/02_decision-criteria/**` | Advertencia de violación de regla de dependencia |

## Hooks

| Evento | Disparador | Acción |
|--------|-----------|--------|
| File Save | Archivos de código | Verificación rápida de cumplimiento de directrices |
| Pre Tool Use (terminal: git commit) | Antes del commit | Recordatorio para ejecutar `#ai-dev-os-check` |
| User Prompt Submit | Prompts relacionados con implementación | Sugiere `#ai-dev-os-plan` |

<details>
<summary>Estructura del paquete</summary>

```
ai-dev-os-plugin-kiro/
├── steering/
│   ├── ai-dev-os-init.md              # Asistente de configuración (manual)
│   ├── ai-dev-os-check.md             # Verificación de cumplimiento (manual)
│   ├── ai-dev-os-scan.md              # Escaneo completo de cumplimiento (manual)
│   ├── ai-dev-os-review.md            # Auto-revisión pre-PR (manual)
│   ├── ai-dev-os-extract.md           # Rule Harvesting desde código (manual)
│   ├── ai-dev-os-why.md               # Explicación de fundamento de regla (manual)
│   ├── ai-dev-os-plan.md              # Planificación con directrices (auto)
│   ├── ai-dev-os-ticket.md            # Generación de tickets (manual)
│   ├── ai-dev-os-audit.md             # Auditoría de salud de 4 capas (manual)
│   ├── ai-dev-os-evolve.md            # Retroalimentación espiral SECI (manual)
│   ├── ai-dev-os-report.md            # Generación de informes de cumplimiento (manual)
│   ├── philosophy-advisor.md          # Juicio arquitectónico basado en L1 (auto)
│   ├── principle-checker.md           # Verificación de alineación L2 (auto)
│   ├── guideline-auditor.md           # Auditoría de cobertura y consistencia L3 (auto)
│   ├── guideline-compliance.md        # Verificación automática en archivos de código (fileMatch)
│   └── layer-dependency.md            # Advertencia de regla de dependencia (fileMatch)
├── hooks/
│   └── hooks.json                     # Hooks de eventos del ciclo de vida
├── checklist-templates/
│   ├── python.md                      # Checklist específico de Python
│   ├── go.md                          # Checklist específico de Go
│   └── nextjs.md                      # Checklist específico de Next.js
├── templates/
│   ├── AGENTS.md.template             # Plantilla AGENTS.md con cascada
│   ├── ai-dev-os-starter/             # Plantilla de configuración mínima
│   └── ai-dev-os-full/                # Plantilla completa de 4 capas
└── docs/
    └── operation-guide.md             # Instrucciones detalladas de uso
```

</details>

## Specificity Cascade

Cuando las reglas entran en conflicto: framework-specific > common > project-specific > decision criteria > philosophy. [→ Detalles](https://github.com/yunbow/ai-dev-os/blob/main/spec/priority-cascade.md)

## Relacionados

| Repositorio | Descripción |
|---|---|
| [ai-dev-os](https://github.com/yunbow/ai-dev-os) | Framework specification and theory |
| [rules-typescript](https://github.com/yunbow/ai-dev-os-rules-typescript) | TypeScript / Next.js / Node.js guidelines |
| [rules-python](https://github.com/yunbow/ai-dev-os-rules-python) | Python / FastAPI guidelines |
| [plugin-claude-code](https://github.com/yunbow/ai-dev-os-plugin-claude-code) | Skills, Hooks, and Agents for Claude Code |
| [plugin-cursor](https://github.com/yunbow/ai-dev-os-plugin-cursor) | Cursor Rules (.mdc) |
| [cli](https://github.com/yunbow/ai-dev-os-cli) | `npx ai-dev-os init` |
| [benchmark](https://github.com/yunbow/ai-dev-os-benchmark) | Quantitative benchmark — guideline impact data |

## Licencia

[MIT](../../../LICENSE)

---

Languages: [English](../../../README.md) | [日本語](../ja/README.md) | [简体中文](../zh-CN/README.md) | [한국어](../ko/README.md) | Español
