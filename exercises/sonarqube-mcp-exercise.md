# 🔍 Ejercicio: Integración de SonarQube MCP con Spec Kit

## Objetivo del Ejercicio

Integrar **SonarQube como Model Context Protocol (MCP)** en tu workflow de Spec-Driven Development para asegurar calidad de código automática en cada fase.

---

## 📚 Contexto: ¿Qué es MCP?

### Model Context Protocol (MCP)

**MCP** permite que herramientas externas (como SonarQube) se integren como "servidores de contexto" que los agentes IA pueden consultar.

```
┌──────────────────────────────────────┐
│     Tu Agente IA (Claude, etc)       │
└────────────────┬─────────────────────┘
                 │ Consulta
                 ▼
┌──────────────────────────────────────┐
│   Model Context Protocol (MCP)       │
├──────────────────────────────────────┤
│ • SonarQube Server                   │
│ • Code Analysis Tools                │
│ • Git History                        │
│ • Testing Frameworks                 │
└────────────────┬─────────────────────┘
                 │ Responde con contexto
                 ▼
┌──────────────────────────────────────┐
│   Contexto Enriquecido para IA       │
│  "El código tiene code smell aquí"   │
└──────────────────────────────────────┘
```

### ¿Por Qué SonarQube MCP en Spec Kit?

| Fase | Beneficio de SonarQube MCP |
|------|---------------------------|
| **Constitution** | Validar que principios de calidad son testables |
| **Specification** | Asegurar que requisitos incluyen testabilidad |
| **Plan** | Arquitectura que facilita análisis automático |
| **Tasks** | Generación de tasks enfocados en calidad |
| **Implementation** | Feedback en vivo durante coding |

---

## 🔧 Parte 1: Configurar SonarQube MCP

### 1.1 Instalar SonarQube Localmente

**Tareas:**
1. Descarga e instala SonarQube (usa Docker o descarga directa)
2. Inicia el servicio
3. Verifica que esté corriendo en http://localhost:9000

**Requisitos:**
- Docker instalado (opción recomendada) O
- Java 11+ instalado (para descarga directa)

**Entrega esperada:**
- [ ] SonarQube corriendo en :9000
- [ ] Acceso web verificado
- [ ] Screenshot de la interfaz

---

### 1.2 Acceder a SonarQube y Crear Token

**Tareas:**
1. Accede a la interfaz web de SonarQube
2. Inicia sesión con credenciales por defecto
3. Crea un nuevo token de API
4. Nombra el token: `spec-kit-integration`
5. Guarda el token en un lugar seguro

**Requisitos:**
- SonarQube corriendo
- Acceso a interfaz web

**Entrega esperada:**
- [ ] Token generado
- [ ] Token guardado en archivo `.env` o similar
- [ ] Verificación de que token funciona

---

### 1.3 Instalar herramientas necesarias

**Tareas:**
1. Instala `sonar-scanner` globalmente
2. Verifica la instalación
3. Configura el path si es necesario

**Requisitos:**
- npm o similar gestor de paquetes
- Terminal/CLI acceso

**Entrega esperada:**
- [ ] `sonar-scanner --version` funciona
- [ ] Output muestra versión actual

---

## 🎯 Parte 2: Configurar MCP Server para SonarQube

### 2.1 Planificar arquitectura del MCP Server

**Tareas:**
1. Diseña la arquitectura del MCP Server
2. Define qué endpoints expondrá
3. Especifica qué datos consultará de SonarQube
4. Documenta el diagrama de flujo

**Requisitos:**
- Entender API de SonarQube
- Diseño de arquitectura

**Preguntas a responder:**
- [ ] ¿Qué endpoints expondrá el MCP?
- [ ] ¿En qué puerto correrá?
- [ ] ¿Qué formato de respuesta dará?
- [ ] ¿Cómo se autenticará con SonarQube?

**Entrega esperada:**
- [ ] Documento de arquitectura
- [ ] Diagrama de flujo
- [ ] Especificación de endpoints

---

### 2.2 Crear archivo de configuración

**Tareas:**
1. Crea archivo `sonar-project.properties` en tu proyecto
2. Configura todos los parámetros necesarios:
   - Project key
   - Project name
   - Rutas de código fuente
   - Rutas de tests
   - Exclusiones
   - URL de SonarQube
   - Token de autenticación

**Requisitos:**
- Acceso a SonarQube
- Token creado en 1.2

**Entrega esperada:**
- [ ] Archivo `sonar-project.properties` creado
- [ ] Todos los parámetros configurados
- [ ] Archivo probado (sin errores de validación)

---

### 2.3 Implementar MCP Server

**Tareas:**
1. Crea un servidor MCP que:
   - Lee la URL y token de SonarQube desde env
   - Expone endpoints HTTP
   - Consulta la API de SonarQube
   - Transforma datos para el agente IA
   - Maneja errores correctamente

2. El servidor debe soportar estos endpoints:
   - `/issues` - Obtiene problemas de calidad
   - `/code-smells` - Filtra solo code smells
   - `/security` - Filtra solo hotspots de seguridad
   - `/coverage` - Obtiene métricas de cobertura
   - `/report` - Genera reporte resumido

**Requisitos:**
- Conocimiento de HTTP/REST
- Familiaridad con APIs
- Lenguaje: Node.js, Python, Go (tu elección)

**Restricciones:**
- El servidor debe ser stateless
- Debe manejar múltiples requests simultáneos
- Debe loguear todas las interacciones
- Debe tener timeout en requests a SonarQube

**Entrega esperada:**
- [ ] Servidor MCP implementado
- [ ] Todos los 5 endpoints funcionando
- [ ] Error handling robusto
- [ ] Logs habilitados

---

### 2.4 Integrar MCP en tu Agente IA

**Tareas:**
1. Configura tu agente IA para usar el MCP Server
2. Actualiza archivos de configuración del agente
3. Verifica que el agente puede consultar el MCP
4. Prueba con una consulta simple

**Requisitos:**
- Agente IA instalado (Claude Code, Copilot, etc)
- MCP Server corriendo

**Procesos:**
- Para Claude Code: Edita `.claude.json`
- Para GitHub Copilot: Usa extensión MCP
- Para otros: Consulta documentación específica

**Entrega esperada:**
- [ ] Archivos de configuración actualizados
- [ ] Agente reconoce el MCP Server
- [ ] Primera consulta exitosa

---

## 🚀 Parte 3: Integración en Workflow Spec-Driven

### 3.1 Enriquecer Constitution con métricas de calidad

**Tareas:**
1. Abre `constitution.md` de tu proyecto Photo Album App
2. Añade nueva sección: "Métricas de Calidad (Validadas por SonarQube)"
3. Define métricas específicas y medibles:
   - Cobertura de tests
   - Densidad de code smells
   - Complejidad cognitiva
   - Rating de seguridad
   - Líneas duplicadas

4. Cada métrica debe tener:
   - Valor objetivo
   - Cómo se mide
   - Por qué es importante
   - Cómo se valida

**Requisitos:**
- Entender constitution.md actual
- Conocer métricas de SonarQube

**Entrega esperada:**
- [ ] Nueva sección en constitution.md
- [ ] Mínimo 5 métricas definidas
- [ ] Cada métrica es medible
- [ ] Vinculado a requisitos de project

---

### 3.2 Usar SonarQube en fase de Specification

**Tareas:**
1. Revisa tu `spec.md` actual
2. Identifica requisitos no-funcionales que implican calidad
3. Reescribe esos requisitos para que sean:
   - Validables por SonarQube
   - Mensurables
   - Verificables automáticamente

4. Documenta cómo cada requisito será validado

**Requisitos:**
- Entender spec.md actual
- Conocer capacidades de SonarQube

**Ejemplo esperado:**
```
Requisito: "El código debe ser mantenible"
↓ Específico y medible:
"Cobertura ≥ 80%, Complejidad < 10, Code smells < 3"
↓ Validable:
"SonarQube reportará estos números"
```

**Entrega esperada:**
- [ ] spec.md actualizado
- [ ] RNF relacionados con calidad son medibles
- [ ] Validación con SonarQube clara

---

### 3.3 Plan con validación automática

**Tareas:**
1. Abre tu `plan.md`
2. Añade sección nueva: "Validación Automática de Calidad"
3. Diseña cómo se validarán los requisitos:
   - Cuándo se ejecuta SonarQube
   - Qué gates de calidad se enforzan
   - Cómo el agente IA recibirá feedback
   - Qué hacer si falla validación

4. Especifica integración con CI/CD (si aplica)

**Requisitos:**
- plan.md existente
- Entender CI/CD pipelines

**Elementos a incluir:**
- [ ] Estrategia de análisis
- [ ] Quality gates
- [ ] Feedback loop
- [ ] Remediation process

**Entrega esperada:**
- [ ] Nueva sección en plan.md
- [ ] Validación automática diseñada
- [ ] Quality gates especificados
- [ ] Feedback mechanism documentado

---

### 3.4 Tasks con validación automática

**Tareas:**
1. Revisa tu `tasks.md`
2. Identifica tasks relacionadas con calidad/testing
3. Para cada una, añade:
   - Cómo se validará con SonarQube
   - Qué métrica debe mejorarse
   - Cómo verificar que pasó
4. Crea nueva task: "Ejecutar análisis SonarQube final"

**Requisitos:**
- tasks.md existente
- Entender estructura de tasks

**Entrega esperada:**
- [ ] Tasks de calidad marcadas
- [ ] Criterios de SonarQube añadidos
- [ ] Task final de análisis creada
- [ ] Validación clara para cada task

---

## 🧪 Parte 4: Ejecutar Análisis SonarQube

### 4.1 Analizar código existente

**Tareas:**
1. Navega a directorio del proyecto
2. Ejecuta sonar-scanner
3. Espera a que se complete el análisis
4. Verifica resultados en dashboard de SonarQube

**Requisitos:**
- SonarQube corriendo
- `sonar-project.properties` configurado
- Token válido
- Código para analizar

**Qué observar:**
- [ ] Scanner inicia sin errores
- [ ] Scanner completa (2-5 min típicamente)
- [ ] Dashboard muestra resultados
- [ ] Métricas son calculadas

**Entrega esperada:**
- [ ] Análisis completado
- [ ] Screenshot del dashboard
- [ ] Reporte de resultados

---

### 4.2 Interpretar resultados

**Tareas:**
1. Abre SonarQube dashboard
2. Documenta los resultados encontrados:
   - Líneas de código total
   - Porcentaje de duplicación
   - Cobertura de tests (%)
   - Code smells encontrados
   - Hotspots de seguridad
   - Complejidad cognitiva promedio

3. Compara con objetivos en constitution.md
4. Identifica brecha (si existe)

**Requisitos:**
- Análisis completado (4.1)
- Acceso a SonarQube dashboard

**Elementos a documentar:**
- [ ] Métricas principales
- [ ] Issues encontrados
- [ ] Comparación con objetivos
- [ ] Brecha de calidad

**Entrega esperada:**
- [ ] Documento con resultados
- [ ] Screenshots del dashboard
- [ ] Análisis de brecha
- [ ] Priorización de fixes

---

### 4.3 Consultar MCP en tu agente IA

**Tareas:**
1. En tu agente IA, realiza una consulta al MCP Server
2. Pregunta: "¿Cuáles son los problemas principales de calidad?"
3. Documenta la respuesta recibida
4. Verifica que la información es correcta vs dashboard

**Requisitos:**
- MCP Server corriendo (Parte 2.3)
- Agente IA configurado (Parte 2.4)
- Análisis completado (Parte 4.1)

**Entrega esperada:**
- [ ] Consulta exitosa al MCP
- [ ] Respuesta del MCP recibida
- [ ] Información coincide con dashboard
- [ ] Agente IA entiende contexto

---

## 📋 Parte 5: Ejercicio Práctico Guiado

### Ejercicio 5.1: Corregir Código Basado en SonarQube

**Enunciado:**

Tu equipo debe eliminar los code smells más graves encontrados por SonarQube.

**Tareas:**

1. **Identificar:** Abre SonarQube y ve a Issues. Filtra por "Code Smell" y ordena por severidad.

2. **Seleccionar:** Elige el primer code smell de la lista.

3. **Documentar:** Crea archivo `fixes/cs-fix-001.md` que contenga:
   - Código original (antes)
   - Explicación del problema
   - Cómo piensas corregirlo
   - Código corregido (después)

4. **Aplicar:** Implementa la corrección en el código real

5. **Validar:** Ejecuta SonarQube nuevamente
   ```
   sonar-scanner
   ```

6. **Verificar:** El code smell debe desaparecer del dashboard

7. **Repetir:** Haz lo mismo con los próximos 2 code smells

**Criterios de éxito:**
- [ ] Mínimo 3 code smells corregidos
- [ ] SonarQube lo reporta como "Resolved"
- [ ] Documentación de cambios completa
- [ ] Código sigue constitución del proyecto

**Entrega esperada:**
- [ ] 3 archivos `fixes/cs-fix-00X.md`
- [ ] Cambios aplicados en código
- [ ] Screenshot post-fix del dashboard
- [ ] Reporte de issues resueltas

---

### Ejercicio 5.2: Aumentar Test Coverage

**Enunciado:**

Tu aplicación tiene 82% de cobertura pero necesita llegar a 90% según constitution.md.

**Tareas:**

1. **Medir:** Ejecuta análisis con cobertura
   ```
   npm run test -- --coverage
   sonar-scanner
   ```

2. **Identificar:** En SonarQube, ve a Coverage y ve qué archivos tiene baja cobertura

3. **Seleccionar:** Elige 2-3 archivos con < 75% cobertura

4. **Analizar:** Para cada archivo:
   - Identifica qué líneas no están cubiertas
   - Entiende por qué (lógica no probada, edge cases, etc)
   - Documenta en `test-gaps/gap-001.md`

5. **Escribir tests:** Crea nuevos tests para cubrir gaps
   - Tests unitarios
   - Tests de integración
   - Edge cases

6. **Validar:**
   ```
   npm run test
   sonar-scanner
   ```

7. **Verificar:** Coverage debe aumentar

**Criterios de éxito:**
- [ ] Coverage total ≥ 90%
- [ ] Archivos seleccionados ≥ 85% cada uno
- [ ] Tests nuevos son significativos (no solo count lines)
- [ ] Tests pasan todos

**Entrega esperada:**
- [ ] Archivos `test-gaps/gap-00X.md`
- [ ] Nuevos tests implementados
- [ ] Screenshot del dashboard post-fix
- [ ] Coverage report comparativo (antes vs después)

---

### Ejercicio 5.3: Security Hotspot Analysis

**Enunciado:**

SonarQube ha identificado potenciales vulnerabilidades de seguridad. Tu tarea es analizarlas y determinar el riesgo.

**Tareas:**

1. **Identificar:** En SonarQube, ve a Security → Security Hotspots

2. **Documentar:** Para cada hotspot, crea archivo `security/hotspot-001.md`:
   - Descripción del hotspot
   - Tipo de vulnerabilidad (OWASP Top 10)
   - Severidad (Critical, High, Medium, Low)
   - Ubicación exacta (archivo + línea)
   - Código problemático

3. **Analizar:** Para cada hotspot:
   - ¿Es realmente un riesgo?
   - ¿Es falso positivo?
   - ¿Necesita fix?
   - ¿Cuál es el impacto?

4. **Planificar:** Decide para cada uno:
   - [ ] Necesita fix inmediato (Critical)
   - [ ] Necesita fix en próxima iteración (High)
   - [ ] Monitorear pero OK por ahora (Medium)
   - [ ] No es riesgo real (False positive)

5. **Documentar:** Crea `security/analysis-report.md` con:
   - Resumen ejecutivo
   - Lista de hotspots con recomendaciones
   - Plan de remediation
   - Priorización

6. **Comunicar:** Presenta hallazgos como si fueras a un security review

**Criterios de éxito:**
- [ ] Todos los hotspots analizados
- [ ] Riesgo clasificado correctamente
- [ ] Plan de remediation claro
- [ ] Decisiones justificadas

**Entrega esperada:**
- [ ] `security/hotspot-001.md`, `hotspot-002.md`, etc (uno por cada)
- [ ] `security/analysis-report.md` (consolidado)
- [ ] Recomendaciones claras
- [ ] Plan de acción

---

## 📊 Parte 6: Métricas a Seguir

### 6.1 Crear Dashboard Personalizado

**Tareas:**

1. En SonarQube, crea un dashboard personalizado para Photo Album App
2. Incluye widgets para:
   - Coverage trend (línea)
   - Code smells (número)
   - Duplicated lines (%)
   - Security rating (badge)
   - Reliability (badge)
   - Maintainability (badge)

3. Configura alertas para:
   - Coverage cae por debajo de 80%
   - Nuevos code smells introducidos
   - Nuevos security hotspots

4. Comparte screenshot del dashboard

**Requisitos:**
- Acceso a SonarQube
- Análisis completado

**Entrega esperada:**
- [ ] Dashboard personalizado creado
- [ ] Widgets configurados
- [ ] Alertas activas
- [ ] Screenshot compartido

---

### 6.2 Definir métricas por componente

**Tareas:**

1. Documenta en `metrics/component-metrics.md`:
   - Para cada componente/módulo principal
   - Qué métricas le aplican
   - Qué valores son aceptables
   - Qué valores son alertas

2. Ejemplo:
   ```
   AlbumStore.ts:
   - Coverage: ≥ 90% (crítico)
   - Code Smells: ≤ 2
   - Complexity: ≤ 8
   - Duplicates: ≤ 2%
   ```

3. Crea tabla de componentes con métricas actuales

**Requisitos:**
- Análisis completado
- Acceso a SonarQube

**Entrega esperada:**
- [ ] `metrics/component-metrics.md`
- [ ] Mínimo 10 componentes documentados
- [ ] Tabla de valores actuales
- [ ] Identificados outliers (fuera de rango)

---

### 6.3 Tendencias y evolución

**Tareas:**

1. Cada semana (o después de cambios importantes), ejecuta análisis
   ```
   sonar-scanner
   ```

2. Documenta en `metrics/evolution.md`:
   - Fecha
   - Coverage (%)
   - Code Smells (count)
   - Security Issues (count)
   - Observaciones

3. Crea tabla o gráfico ASCII mostrando evolución

4. Identifica trends:
   - ¿Mejorando?
   - ¿Empeorando?
   - ¿Estable?

**Requisitos:**
- Múltiples análisis a través del tiempo

**Entrega esperada:**
- [ ] `metrics/evolution.md`
- [ ] Mínimo 3 mediciones
- [ ] Gráfico ASCII o tabla
- [ ] Análisis de tendencia

---

## ✅ Checklist Final del Ejercicio

- [ ] **Parte 1:** SonarQube instalado y token creado
- [ ] **Parte 2:** MCP Server implementado y configurado
- [ ] **Parte 3:** Constitution, Spec, Plan, Tasks actualizados
- [ ] **Parte 4:** Primer análisis ejecutado e interpretado
- [ ] **Parte 5.1:** 3 Code Smells corregidos
- [ ] **Parte 5.2:** Coverage aumentado a 90%
- [ ] **Parte 5.3:** Security hotspots analizados
- [ ] **Parte 6.1:** Dashboard personalizado creado
- [ ] **Parte 6.2:** Métricas por componente documentadas
- [ ] **Parte 6.3:** Evolución de métricas rastreada

---

## 📚 Recursos Necesarios

### Documentación Externa
- SonarQube Official Docs
- SonarQube API Reference
- Model Context Protocol Specification
- OWASP Top 10

### Herramientas Requeridas
- SonarQube (local o cloud)
- sonar-scanner CLI
- Tu lenguaje preferido (JS, Python, Go, etc) para MCP Server
- Tu agente IA (Claude, Copilot, etc)

### Archivos a Crear
```
proyecto/
├── sonar-project.properties
├── mcp-server/
│   └── server.js (o .py, .go, etc)
├── fixes/
│   ├── cs-fix-001.md
│   ├── cs-fix-002.md
│   └── cs-fix-003.md
├── test-gaps/
│   ├── gap-001.md
│   ├── gap-002.md
│   └── nuevos-tests.ts
├── security/
│   ├── hotspot-001.md
│   ├── hotspot-002.md
│   └── analysis-report.md
└── metrics/
    ├── component-metrics.md
    └── evolution.md
```

---

## 🎓 Lecciones Clave

1. **SonarQube MCP** enriquece el contexto del agente IA
2. **Métricas objetivas** reemplazan intuición sobre calidad
3. **Spec-Driven + SonarQube** = desarrollo confiable
4. **Feedback automático** acelera detección y fix de issues
5. **Constitution validada** asegura consistencia

---

## 🚀 Próximos Pasos

1. ✅ Completa todos los ejercicios de esta sección
2. ✅ Integra SonarQube en tu CI/CD pipeline
3. ✅ Aplica a tu propio proyecto Photo Album App
4. ✅ Extiende con otros MCPs (testing, git, etc)
5. ✅ Documenta decisiones en ADRs

---

**Ejercicio Versión:** 1.0  
**Dificultad:** Intermedio  
**Tiempo Estimado:** 6-8 horas (desglosado)  
**Requisitos Previos:** Haber completado ejemplo photo-album-app

**¡Éxito con tu integración de SonarQube MCP! 🎉**
