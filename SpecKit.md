<table bgcolor="#ffffff" width="100%" style="width: 100%; border-collapse: collapse; border: 1px solid #d0d0d0; background-color: #ffffff !important; font-family: Arial, sans-serif; opacity: 1 !important;">
  <tr bgcolor="#ffffff" style="background-color: #ffffff !important;">
    <td align="center" bgcolor="#ffffff" style="padding: 25px; vertical-align: middle; background-color: #ffffff !important;">
      <div style="background-color: #ffffff !important; padding: 10px;">
        <img src="https://talentodigitalextremadura.com/wp-content/uploads/2025/05/junta-ext-transforma2.png" height="140" style="height: 140px; width: auto; display: inline-block; background-color: #ffffff !important;">
      </div>
      <hr style="border: 0; border-top: 1px solid #dddddd; width: 85%; margin: 20px auto;">
      <table width="100%" bgcolor="#ffffff" style="width: 100%; border-collapse: collapse; background-color: #ffffff !important;">
        <tr bgcolor="#ffffff" style="background-color: #ffffff !important;">
          <td align="center" width="33.3%" bgcolor="#ffffff" style="padding: 10px; background-color: #ffffff !important; border: none;">
            <img src="https://talentodigitalextremadura.com/wp-content/uploads/2024/10/Grafismo-UEx-Color-3.png" height="110" style="height: 110px; width: auto; background-color: #ffffff !important;">
          </td>
          <td align="center" width="33.3%" bgcolor="#ffffff" style="padding: 10px; background-color: #ffffff !important; border: none;">
            <img src="https://talentodigitalextremadura.com/wp-content/uploads/2026/01/logointia.png" height="110" style="height: 110px; width: auto; background-color: #ffffff !important;">
          </td>
          <td align="center" width="33.3%" bgcolor="#ffffff" style="padding: 10px; background-color: #ffffff !important; border: none;">
            <img src="https://talentodigitalextremadura.com/wp-content/uploads/2024/10/Group-59651.png" height="110" style="height: 110px; width: auto; background-color: #ffffff !important;">
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table>

# GitHub Spec Kit - Plan de Generación de Talento Digital

## Tabla de Contenidos

- [Introducción](#introducción)
- [¿Qué es Spec-Driven Development?](#qué-es-spec-driven-development)
- [Conceptos Principales](#conceptos-principales)
- [Arquitectura y Componentes](#arquitectura-y-componentes)
- [Flujo de Trabajo](#flujo-de-trabajo)
- [Instalación y Configuración](#instalación-y-configuración)
- [Comandos Disponibles](#comandos-disponibles)
- [Ejemplo Práctico: Aplicación Taskify](#ejemplo-práctico-aplicación-taskify)
- [Casos de Uso](#casos-de-uso)
- [Agentes IA Soportados](#agentes-ia-soportados)
- [Mejores Prácticas](#mejores-prácticas)
- [Troubleshooting](#troubleshooting)

---

## Introducción

**GitHub Spec Kit** es un toolkit de código abierto creado por GitHub que revoluciona la forma en que desarrollamos software. En lugar del enfoque tradicional donde el código es el punto de partida, Spec Kit pone las **especificaciones executable como el centro del desarrollo**.

### Objetivo Principal

Permitir que los desarrolladores se enfoquen en **escenarios de producto y resultados predecibles** en lugar de escribir código "por intuición" desde cero.

### Estadísticas

- ⭐ **73.9K** estrellas en GitHub
- 🔀 **6.3K** forks
- 🐍 **72% Python**, 15.5% Shell, 12.5% PowerShell
- 📦 **112+ releases**

---

## ¿Qué es Spec-Driven Development?

### El Cambio de Paradigma

```
ENFOQUE TRADICIONAL:
┌─────────────────────────────────────────┐
│ Requisitos → Especificaciones →         │
│ Código → Pruebas → Documentación        │
│ (Especificaciones = Documentación)      │
└─────────────────────────────────────────┘

SPEC-DRIVEN DEVELOPMENT:
┌─────────────────────────────────────────┐
│ Especificaciones Ejecutables            │
│          ↓                              │
│ Código Generado                         │
│          ↓                              │
│ Aplicación Funcional                    │
│ (Especificaciones = Fuente de Verdad)   │
└─────────────────────────────────────────┘
```

### Principios Fundamentales

1. **Intent-Driven Development**: Define el "¿Qué?" y "¿Por qué?" antes del "¿Cómo?"
2. **Especificaciones Ricas**: Utiliza guardrails y principios organizacionales
3. **Refinamiento Multi-Paso**: Evita la generación de código de "un disparo"
4. **Potencia de IA Avanzada**: Aprovecha capacidades de modelos de IA modernos

### Beneficios

| Aspecto | Beneficio |
|---------|-----------|
| **Velocidad** | Generar aplicaciones funcionales en horas en lugar de semanas |
| **Calidad** | Especificaciones ricas generan código de mayor calidad |
| **Mantenibilidad** | Cambios y evoluciones se rastrean en especificaciones |
| **Reutilización** | Especificaciones pueden adaptarse a múltiples tech stacks |
| **Colaboración** | Especificaciones claras permiten mejor comunicación |

---

## Conceptos Principales

### 1. Constitución del Proyecto

La **Constitución** es el documento foundacional que define:

- Principios de calidad de código
- Estándares de pruebas
- Consistencia de UX
- Requisitos de rendimiento
- Gobernanza técnica

```
┌─ CONSTITUCIÓN ─────────────────┐
│ • Principios de Codificación   │
│ • Estándares de Pruebas        │
│ • UX Consistency               │
│ • Requerimientos de Performance│
│ • Gobernanza                   │
└────────────────────────────────┘
         ↓ Guía ↓
   Toda la Especificación
```

### 2. Especificación (Spec)

Define **qué se va a construir** sin enfoque técnico:

- **Historias de Usuario**: ¿Qué necesita hacer el usuario?
- **Requisitos Funcionales**: ¿Cuál es el comportamiento esperado?
- **Casos de Uso**: ¿Cómo interactúan los usuarios?
- **Criterios de Aceptación**: ¿Cómo verificamos que funciona?

**Ejemplo:**
```
Usuario: Product Manager
Necesidad: Crear proyectos y asignar tareas a miembros del equipo
Resultado: Dashboard de tareas con vista Kanban
```

### 3. Plan Técnico

Responde: **¿Cómo implementamos esto?**

- **Tech Stack**: Tecnologías a usar
- **Arquitectura**: Estructura de la solución
- **Servicios Necesarios**: APIs, Bases de Datos, etc.
- **Detalles de Implementación**: Contratos, modelos de datos

**Ejemplo:**
```
Frontend: Blazor Server
Backend: .NET con ASP.NET Core
Base de Datos: PostgreSQL
Real-time: SignalR
```

### 4. Tareas (Tasks)

Breakdown ejecutable del plan:

- Tareas ordenadas por dependencias
- Marcadas para ejecución paralela `[P]`
- Incluye rutas de archivos específicas
- Estructura TDD (pruebas primero)

---

## Arquitectura y Componentes

### Estructura de Directorios

```
proyecto/
├── .specify/
│   ├── memory/
│   │   └── constitution.md          # Principios del proyecto
│   ├── scripts/
│   │   ├── check-prerequisites.sh
│   │   ├── common.sh
│   │   ├── create-new-feature.sh
│   │   ├── setup-plan.sh
│   │   └── update-claude-md.sh
│   ├── specs/
│   │   └── 001-feature-name/
│   │       ├── spec.md              # Especificación
│   │       ├── plan.md              # Plan técnico
│   │       ├── tasks.md             # Tareas
│   │       ├── data-model.md        # Modelo de datos
│   │       ├── research.md          # Investigación
│   │       ├── quickstart.md        # Guía rápida
│   │       └── contracts/           # Especificaciones API
│   │           ├── api-spec.json
│   │           └── signalr-spec.md
│   └── templates/
│       ├── spec-template.md
│       ├── plan-template.md
│       └── tasks-template.md
├── src/                             # Código fuente generado
├── tests/                           # Suite de pruebas
├── docs/                            # Documentación
└── README.md
```

### Componentes Clave

#### CLI (Specify)

Herramienta de línea de comandos para:
- Inicializar proyectos
- Generar estructura
- Verificar requisitos

#### Templates

Plantillas predefinidas para:
- Especificaciones
- Planes técnicos
- Listas de tareas

#### Scripts

Scripts automatizados para:
- Verificación de prerequisites
- Creación de ramas
- Actualización de metadatos

---

## Flujo de Trabajo

### 📊 Diagrama General del Proceso

```
                          SPEC-DRIVEN DEVELOPMENT WORKFLOW
                          
┌──────────────────────────────────────────────────────────────────┐
│                    INICIO: specify init                          │
│              (Inicializar proyecto con Spec Kit)                 │
└────────────────────────┬─────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────────────┐
│    PASO 1: /speckit.constitution                                │
│  (Establecer principios y gobernanza del proyecto)              │
│                                                                  │
│  Input: "Crear principios de calidad de código,                │
│          estándares de pruebas, UX consistente"                │
│  Output: constitution.md (Documento de referencia)             │
└────────────────────────┬─────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────────────┐
│    PASO 2: /speckit.specify                                     │
│  (Crear especificación funcional - SIN tech stack)             │
│                                                                  │
│  Input: "Construir app de gestión de fotos..."                │
│  Output: spec.md (Requisitos, historias de usuario)           │
│          Rama creada automáticamente                           │
└────────────────────────┬─────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────────────┐
│    PASO 3: /speckit.clarify (OPCIONAL)                          │
│  (Aclarar áreas no especificadas)                              │
│                                                                  │
│  Output: Sección de Aclaraciones añadida a spec.md            │
└────────────────────────┬─────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────────────┐
│    PASO 4: /speckit.plan                                        │
│  (Crear plan técnico - CON tech stack específico)             │
│                                                                  │
│  Input: "Usar .NET Aspire, PostgreSQL, Blazor Server"        │
│  Output: plan.md                                               │
│          data-model.md                                        │
│          contracts/api-spec.json                             │
│          research.md (Investigación de tech stack)           │
└────────────────────────┬─────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────────────┐
│    PASO 5: /speckit.analyze (OPCIONAL)                          │
│  (Validación de consistencia entre artefactos)                │
│                                                                  │
│  Output: Análisis de cobertura y consistencia                 │
└────────────────────────┬─────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────────────┐
│    PASO 6: /speckit.tasks                                       │
│  (Generar lista de tareas ejecutables)                         │
│                                                                  │
│  Input: plan.md                                                │
│  Output: tasks.md (Tareas ordenadas por dependencias)        │
│          Marcas: [P] para ejecución paralela                 │
└────────────────────────┬─────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────────────┐
│    PASO 7: /speckit.implement                                   │
│  (Ejecutar implementación automática)                          │
│                                                                  │
│  Valida: Constitution ✓, Spec ✓, Plan ✓, Tasks ✓            │
│  Ejecuta: Tareas en orden respetando dependencias             │
│  Genera: Código funcional, archivos, estructura               │
│  Output: Aplicación lista para probar                         │
└────────────────────────┬─────────────────────────────────────────┘
                         ↓
┌──────────────────────────────────────────────────────────────────┐
│                      VERIFICACIÓN Y REFINAMIENTO                │
│                  (Pruebas, correcciones, iteración)             │
└──────────────────────────────────────────────────────────────────┘
```

### Ciclo Iterativo

```
           ┌─── CICLO DE MEJORA ───┐
           │                       │
           ↓                       │
    Probar Aplicación              │
           ↓                       │
    Encontrar Problemas            │
           ↓                       │
    Actualizar Spec/Plan           │
           ↓                       │
    Ejecutar /speckit.tasks        │
           ↓                       │
    Ejecutar /speckit.implement    │
           │                       │
           └───────────────────────┘
```

---

## Instalación y Configuración

### Prerrequisitos

```
✓ Linux, macOS o Windows
✓ Python 3.11+
✓ Git instalado
✓ uv (gestor de paquetes) - https://docs.astral.sh/uv/
✓ Agente IA soportado (Claude Code, Copilot, etc.)
```

### Opción 1: Instalación Persistente (Recomendado)

```bash
# Instalar una sola vez
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# Usar directamente
specify init mi-proyecto

# O inicializar en directorio actual
specify init . --ai claude
specify init --here --ai gemini

# Actualizar
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
```

**Ventajas:**
- Herramienta permanece disponible
- Mejor gestión con `uv tool list`, `uv tool upgrade`
- Más limpio que crear aliases

### Opción 2: Uso Único (Sin Instalación)

```bash
# Ejecutar sin instalar
uvx --from git+https://github.com/github/spec-kit.git specify init mi-proyecto
```

### Inicializar Proyecto

```bash
# Crear nuevo proyecto
specify init mi-proyecto --ai claude

# Especificar script (Bash o PowerShell)
specify init mi-proyecto --ai claude --script sh   # Linux/macOS
specify init mi-proyecto --ai claude --script ps   # Windows

# En directorio actual
specify init . --force --ai gemini

# Omitir verificación de herramientas
specify init mi-proyecto --ai claude --ignore-agent-tools

# Habilitar debug
specify init mi-proyecto --ai claude --debug

# Con token de GitHub
specify init mi-proyecto --ai claude --github-token ghp_xxx

# Instalar skills del agente
specify init mi-proyecto --ai claude --ai-skills
```

### Verificar Instalación

```bash
# Verificar herramientas instaladas
specify check
```

---

## Comandos Disponibles

### Comandos Principales

| Comando | Descripción | Entrada | Salida |
|---------|-----------|---------|--------|
| `/speckit.constitution` | Establecer principios del proyecto | Áreas a cubrir (calidad, pruebas, UX) | `constitution.md` |
| `/speckit.specify` | Crear especificación funcional | Requisitos sin tech stack | `spec.md` + Rama git |
| `/speckit.clarify` | Aclarar requisitos ambiguos | Preguntas del agente | Sección de aclaraciones |
| `/speckit.plan` | Plan técnico con tech stack | Tech stack y arquitectura | `plan.md`, `data-model.md`, `contracts/` |
| `/speckit.analyze` | Validar consistencia | (Automático de artefactos) | Reporte de análisis |
| `/speckit.tasks` | Generar tareas ejecutables | `plan.md` | `tasks.md` con dependencias |
| `/speckit.implement` | Ejecutar implementación | `tasks.md` | Código fuente generado |
| `/speckit.checklist` | Validación de calidad | Requisitos | Lista de verificación |

### Ejemplos de Uso

```bash
# En tu agente IA dentro del proyecto:

# 1. Establecer principios
/speckit.constitution Crear principios enfocados en calidad de código, \
                      estándares de pruebas, UX consistente y performance

# 2. Definir qué construir (SIN tecnologías específicas)
/speckit.specify Construir una aplicación que permita organizar fotos \
                 en álbumes agrupados por fecha. Los álbumes se pueden \
                 reorganizar con drag-and-drop. Las fotos usan interfaz \
                 tipo tiles.

# 3. Aclarar requisitos (ANTES de hacer el plan)
/speckit.clarify

# 4. Definir CÓMO implementarlo (CON tecnologías)
/speckit.plan Usar Vite con HTML/CSS/JavaScript vanilla. \
              Almacenar fotos localmente con metadatos en SQLite.

# 5. Generar tareas
/speckit.tasks

# 6. Implementar
/speckit.implement
```

---

## Agentes IA Soportados

```
┌──────────────────────────────────────────────────┐
│         AGENTES IA SOPORTADOS POR SPEC KIT       │
├──────────────────────────────────────────────────┤
│ ✅ Claude Code (Anthropic)                       │
│ ✅ GitHub Copilot                                │
│ ✅ Cursor (cursor-agent)                         │
│ ✅ Windsurf                                      │
│ ✅ Google Gemini CLI (gemini)                    │
│ ✅ Qwen Code (qwen)                              │
│ ✅ OpenCode (opencode)                           │
│ ✅ Codex CLI (codex)                             │
│ ✅ Qoder CLI (qodercli, kiro)                    │
│ ✅ Kiro CLI                                      │
│ ✅ Roo Code (roocode)                            │
│ ✅ CodeBuddy CLI                                 │
│ ✅ Auggie CLI                                    │
│ ✅ Amp (ampcode)                                 │
│ ✅ Jules                                         │
│ ✅ SHAI (OVHcloud)                               │
│ ✅ IBM Bob                                       │
│ ✅ Antigravity (agy)                             │
│ ✅ Kilo Code (kilocode)                          │
│ ✅ Generic (bring your own agent)                │
└──────────────────────────────────────────────────┘
```

### Seleccionar Agente

```bash
# Especificar al inicializar
specify init mi-proyecto --ai claude
specify init mi-proyecto --ai copilot
specify init mi-proyecto --ai cursor-agent
specify init mi-proyecto --ai windsurf
specify init mi-proyecto --ai gemini

# Con agente personalizado
specify init mi-proyecto --ai generic --ai-commands-dir .myagent/commands/
```

---

## Casos de Uso

### 1. 🆕 Desarrollo de Cero (Greenfield)

**Escenario:** Nueva aplicación desde cero

```
Constitution → Specify → Plan → Tasks → Implement

Ejemplo: Crear plataforma de e-learning con cursos, lecciones y usuarios
Tiempo: 4-8 horas para MVP funcional
```

### 2. 🔧 Modernización (Brownfield)

**Escenario:** Mejorar aplicación existente

```
Constitution → Specify (nueva feature) → Plan → Tasks → Implement

Ejemplo: Añadir sistema de notificaciones a aplicación existente
```

### 3. 🎨 Exploración Creativa

**Escenario:** Probar múltiples enfoques

```
Una spec → Plan A (tech stack 1)
         → Plan B (tech stack 2)
         → Plan C (tech stack 3)

Resultado: Comparar implementaciones
```

### 4. 🏢 Restricciones Empresariales

**Escenario:** Aplicación con constraints

```
Constitution (define constraints) → Specify → Plan → Implement

Ejemplo: Debe funcionar offline, usar solo Node.js, 
         cumplir GDPR, máximo 5MB bundle
```

### 5. 🚀 Generación Rápida de Prototipos

**Escenario:** MVP en horas

```
Specify (simple) → Plan → Tasks (simples) → Implement

Resultado: Prototipo funcional para validación
```

---

## Mejores Prácticas

### ✅ Al Usar Constitution

```markdown
# Haz:
- Sé específico sobre estándares de calidad
- Define métricas medibles
- Incluye requisitos de seguridad
- Documenta decisiones arquitectónicas

# Evita:
- Ser demasiado genérico
- Incluir detalles de implementación
- Contradecir en múltiples secciones
```

### ✅ Al Escribir Specifications

```markdown
# Haz:
- Enfócate en el "QUÉ" no el "CÓMO"
- Usa historias de usuario claras
- Define criterios de aceptación explícitos
- Incluye casos límite
- SIN tech stack específico

# Evita:
- Mencionar tecnologías específicas
- Ser vago sobre resultados
- Omitir criterios de aceptación
- Historias demasiado largas
```

**Bueno:**
```
"Como vendedor, quiero filtrar productos por precio,
para encontrar opciones dentro de mi presupuesto.

Criterios:
- Filtro por rango: mín-máx
- Se aplica sin refrescar página
- Muestra cantidad de resultados"
```

**Malo:**
```
"Necesitamos un filtro SQL en el backend
con elasticsearch para búsqueda rápida
y caché en Redis"
```

### ✅ Al Crear Planes Técnicos

```markdown
# Haz:
- Justifica por qué cada tecnología
- Define contratos de API
- Especifica modelos de datos
- Identifica componentes reutilizables
- Documenta decisiones

# Evita:
- Over-engineering
- Tech stack sin justificación
- Componentes que no coinciden con spec
```

### ✅ Validación Cruzada

Antes de `implement`:

```bash
/speckit.analyze

# Verifica:
# ✓ Spec cubre todos los requisitos
# ✓ Plan implementa toda la spec
# ✓ Tasks cubre todo el plan
# ✓ No hay gaps o redundancias
```

### ✅ Iteración Controlada

```
Versión 1 → Feedback → Actualizar Spec
           ↓
           Actualizar Plan
           ↓
           Regenerar Tasks
           ↓
           Re-implement
```

---

## Troubleshooting

### Problema: "No se encuentran los comandos /speckit.*"

**Causa:** El proyecto no está inicializado correctamente

**Solución:**
```bash
# Verificar estructura
ls -la .specify/

# Reinicializar si es necesario
specify init . --force --ai claude
```

### Problema: El agente se "queda atrapado" investigando

**Causa:** Investigación sin dirección

**Solución:**
```
"Crea una lista específica de tareas que necesitan 
investigación. Para cada una, crea una tarea separada
de investigación paralela. No investigues amplios,
investiga específicamente."
```

### Problema: Código generado no compila

**Causa:** Posibles issues:
- Dependencias faltantes
- Rutas de archivos incorrectas
- Configuración incompleta

**Solución:**
```bash
# Ejecutar en directorio del agente
npm install    # o equivalente para tu tech stack
npm run build  # o equivalente

# Mostrar errores al agente
# El agente puede then ejecutar fixes
```

### Problema: Tasks.md no se genera correctamente

**Causa:** Plan.md incompleto

**Solución:**
```
/speckit.plan

# Valida que el plan incluya:
- Componentes principales
- Endpoints de API
- Modelos de datos
- Flujo de información
- Dependencias de componentes
```

### Problema: Agente "olvida" la constitución

**Causa:** Context window limitado

**Solución:**
```
"Revisa la constitución en .specify/memory/constitution.md
y asegúrate de que todos los principios se reflejan
en el plan actual"
```

### Variables de Entorno

```bash
# Para trabajar sin Git (monorepo personalizado)
export SPECIFY_FEATURE="001-photo-albums"

# El agente usará esta feature al hacer plan y implement
```

---

## Flujo Recomendado: Paso a Paso

```
┌─────────────────────────────────────┐
│ FASE 1: PREPARACIÓN                 │
├─────────────────────────────────────┤
│ 1. specify init proyecto --ai claude│
│ 2. /speckit.constitution            │
│ 3. Revisar constitution.md          │
└─────────────────────────────────────┘
              ↓
┌─────────────────────────────────────┐
│ FASE 2: ESPECIFICACIÓN              │
├─────────────────────────────────────┤
│ 1. /speckit.specify [tu requisito]  │
│ 2. /speckit.clarify                 │
│ 3. Revisar y ajustar spec.md        │
│ 4. Validar checklist de aceptación  │
└─────────────────────────────────────┘
              ↓
┌─────────────────────────────────────┐
│ FASE 3: PLANIFICACIÓN TÉCNICA       │
├─────────────────────────────────────┤
│ 1. /speckit.plan [tech stack]       │
│ 2. Revisar plan.md y data-model.md  │
│ 3. Validar contracts/ API specs     │
│ 4. Realizar research.md si es necesario
│ 5. Detectar over-engineering        │
└─────────────────────────────────────┘
              ↓
┌─────────────────────────────────────┐
│ FASE 4: DESGLOSE DE TAREAS          │
├─────────────────────────────────────┤
│ 1. /speckit.tasks                   │
│ 2. Revisar tasks.md                 │
│ 3. Verificar orden de dependencias  │
│ 4. Identificar tareas paralelas [P] │
└─────────────────────────────────────┘
              ↓
┌─────────────────────────────────────┐
│ FASE 5: IMPLEMENTACIÓN              │
├─────────────────────────────────────┤
│ 1. /speckit.implement               │
│ 2. Monitorear progreso              │
│ 3. Resolver errores de compilación  │
│ 4. Pruebas funcionales              │
└─────────────────────────────────────┘
              ↓
┌─────────────────────────────────────┐
│ FASE 6: VALIDACIÓN                  │
├─────────────────────────────────────┤
│ 1. Probar todas las historias de usuario
│ 2. Validar contra criterios de aceptación
│ 3. Ejecutar suite de tests          │
│ 4. Verificar performance            │
│ 5. Code review contra constitution  │
└─────────────────────────────────────┘
              ↓
┌─────────────────────────────────────┐
│ ✅ APLICACIÓN LISTA                 │
└─────────────────────────────────────┘
```

---

## Conclusión

**GitHub Spec Kit** revoluciona el desarrollo de software al convertir especificaciones en código ejecutable. A través de un proceso estructurado y guiado por IA:

1. **Define claramente** qué necesitas (sin tecnicismos)
2. **Planifica técnicamente** cómo lo lograrás
3. **Genera automáticamente** código funcional
4. **Iteras rápidamente** con feedback

### Resultados Clave

- ⚡ **4x más rápido**: Aplicaciones en horas, no semanas
- 📊 **Mayor calidad**: Especificaciones ricas = código mejor
- 🎯 **Menos ambigüedad**: Requisitos ejecutables
- 🔄 **Fácil evolución**: Cambios en especificaciones
- 🤖 **Potencia de IA**: Aprovecha modelos avanzados

### Próximos Pasos

1. Instala `specify-cli`: `uv tool install specify-cli --from git+https://github.com/github/spec-kit.git`
2. Inicializa tu proyecto: `specify init mi-proyecto --ai claude`
3. Sigue el flujo recomendado
4. ¡Construye tu aplicación!

### Referencias

- 📖 [Documentación Oficial](https://github.com/github/spec-kit)
- 🎥 [Video Demo](https://www.youtube.com/watch?v=a9eR1xsfvHg)
- 💬 [GitHub Discussions](https://github.com/github/spec-kit/discussions)
- 🐛 [Reportar Issues](https://github.com/github/spec-kit/issues)

---

**Licencia:** MIT  
**Creado por:** GitHub Inc.  
**Última actualización:** 2025
