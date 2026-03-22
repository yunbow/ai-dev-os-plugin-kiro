# AI Dev OS Plugin — Kiro — Guía de operación

## Tabla de contenidos

1. [Requisitos previos](#1-requisitos-previos)
2. [Instalación](#2-instalación)
3. [Configuración inicial](#3-configuración-inicial)
4. [Flujo de trabajo diario](#4-flujo-de-trabajo-diario)
5. [Mantenimiento periódico](#5-mantenimiento-periódico)
6. [Incorporación del equipo](#6-incorporación-del-equipo)
7. [Política de idioma](#7-política-de-idioma)
8. [Solución de problemas](#8-solución-de-problemas)

---

## 1. Requisitos previos

- [Kiro](https://kiro.dev/) >= 1.0.0
- Archivos de capas de AI Dev OS (L1-L3) configurados en tu proyecto (plantillas: [TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python))

---

## 2. Instalación

### Opción A: Copiar reglas de dirección (Recomendado)

```bash
git clone https://github.com/yunbow/ai-dev-os-plugin-kiro.git
cp -r ai-dev-os-plugin-kiro/steering/ .kiro/steering/
cp -r ai-dev-os-plugin-kiro/hooks/ .kiro/hooks/
cp -r ai-dev-os-plugin-kiro/checklist-templates/ .kiro/checklist-templates/
```

### Opción B: Git Submodule

```bash
git submodule add https://github.com/yunbow/ai-dev-os-plugin-kiro.git .kiro/plugins/ai-dev-os
cp -r .kiro/plugins/ai-dev-os/steering/* .kiro/steering/
cp -r .kiro/plugins/ai-dev-os/hooks/* .kiro/hooks/
```

### Configuración de hooks

Los hooks de Kiro también se pueden configurar via Hook UI:

1. Abrir Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Escribir "Kiro: Open Kiro Hook UI"
3. Crear hooks según las configuraciones en `hooks/hooks.json`

---

## 3. Configuración inicial

En el chat de Kiro:

```text
#ai-dev-os-init [tech-stack]
```

Ejemplo:

```text
#ai-dev-os-init nextjs
```

---

## 4. Flujo de trabajo diario

### 4.1 Planificación antes de implementar

```text
#ai-dev-os-plan Añadir autenticación de usuario con JWT
```

### 4.2 Crear tickets en lugar de implementar

```text
#ai-dev-os-ticket Añadir autenticación de usuario con JWT
```

### 4.3 Escribir código

Escribe código como de costumbre. Las reglas de dirección y hooks te guiarán automáticamente.

### 4.4 Antes del commit

```text
#ai-dev-os-check
```

### 4.5 Después de revisión de código

```text
#ai-dev-os-extract [file-path]
```

### 4.6 Entender reglas

```text
#ai-dev-os-why "¿por qué está prohibido el tipo any?"
```

---

## 5. Mantenimiento periódico

### Mensual: Auditoría de salud

```text
#ai-dev-os-audit
```

### Trimestral: Evolución espiral SECI

```text
#ai-dev-os-evolve
```

### Semanal/Mensual: Informe de cumplimiento

```text
#ai-dev-os-report 1w
#ai-dev-os-report 1m
```

---

## 6. Incorporación del equipo

### Para nuevos miembros

1. Leer `ai-dev-os/01_philosophy/core-values.md` (5 min)
2. Revisar `ai-dev-os/02_decision-criteria/` (10 min)
3. Invocar `#ai-dev-os-why` para reglas poco claras
4. Comenzar a codificar — las reglas y hooks guiarán automáticamente

### Para equipos que adoptan AI Dev OS

1. Invocar `#ai-dev-os-init` en el proyecto
2. Comenzar con la plantilla **starter** (solo L3)
3. Usar `#ai-dev-os-extract` después de cada revisión de código
4. Después de 2-4 semanas, invocar `#ai-dev-os-audit` para identificar brechas
5. Construir gradualmente L1-L2 a través de `#ai-dev-os-evolve`

---

## 7. Política de idioma

Todos los archivos fuente (steering rules, hooks, templates) se mantienen en **inglés**. La documentación traducida se proporciona bajo `docs/i18n/` como referencia.

---

## 8. Solución de problemas

### Las reglas de dirección no se activan

- Verificar que los archivos estén en `.kiro/steering/`
- Comprobar que el YAML frontmatter sea válido
- Para dirección manual, invocar con `#name` en el chat
- Para dirección automática, verificar que `description` coincida con el contexto

### Los hooks no se activan

- Verificar que los hooks estén en `.kiro/hooks/`
- Configurar via Kiro Hook UI (`Ctrl+Shift+P` → "Kiro: Open Kiro Hook UI")
- Comprobar que `jq` esté instalado

### Usar Kiro Specs con AI Dev OS

El desarrollo basado en specs de Kiro (requisitos → diseño → tareas) complementa AI Dev OS:

- Usar Kiro Specs para planificación de features y descomposición de tareas
- Las directrices de AI Dev OS actúan como puertas de calidad durante la ejecución de tareas de specs

---

Languages: [English](../../operation-guide.md) | [日本語](../ja/operation-guide.md) | [简体中文](../zh-CN/operation-guide.md) | [한국어](../ko/operation-guide.md) | Español
