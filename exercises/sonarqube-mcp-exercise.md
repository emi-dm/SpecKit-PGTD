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

```bash
# Opción 1: Docker (recomendado)
docker run -d --name sonarqube \
  -p 9000:9000 \
  sonarqube:latest

# Opción 2: Descarga directa
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.0.0.68432.zip
unzip sonarqube-10.0.0.68432.zip
```

### 1.2 Acceder a SonarQube

```
URL: http://localhost:9000
Usuario: admin
Password: admin
(Cambiar password en primer login)
```

### 1.3 Crear Token de API

1. Click en Avatar (arriba a la derecha)
2. Security → Tokens
3. Generate Token → Nombre: `spec-kit-token`
4. Guardar token (lo usaremos después)

---

## 🎯 Parte 2: Configurar MCP Server para SonarQube

### 2.1 Instalar herramientas necesarias

```bash
# Instalar sonar-cli para análisis
npm install -g sonar-scanner

# Verificar instalación
sonar-scanner --version
```

### 2.2 Crear archivo de configuración

Archivo: `sonar-project.properties`

```properties
sonar.projectKey=photo-album-app
sonar.projectName=Photo Album App
sonar.projectVersion=1.0.0
sonar.sources=src
sonar.tests=tests
sonar.exclusions=node_modules/**,dist/**,coverage/**
sonar.host.url=http://localhost:9000
sonar.login=<YOUR_TOKEN_HERE>
```

### 2.3 Configurar MCP en tu Agente IA

Para **Claude Code** o agentes que soporten MCP:

Archivo: `.claude.json`

```json
{
  "mcp": {
    "sonarqube": {
      "command": "node",
      "args": ["./mcp-servers/sonarqube-mcp.js"],
      "env": {
        "SONAR_URL": "http://localhost:9000",
        "SONAR_TOKEN": "<YOUR_TOKEN>"
      }
    }
  }
}
```

### 2.4 Crear MCP Server para SonarQube

Archivo: `mcp-servers/sonarqube-mcp.js`

```javascript
// MCP Server para integrar SonarQube
const http = require('http');
const url = require('url');

const SONAR_URL = process.env.SONAR_URL || 'http://localhost:9000';
const SONAR_TOKEN = process.env.SONAR_TOKEN;

class SonarQubeMCPServer {
  constructor() {
    this.projectKey = 'photo-album-app';
  }

  async getProjectIssues() {
    /**
     * Obtiene problemas de calidad del proyecto
     */
    const endpoint = `${SONAR_URL}/api/issues/search?componentKeys=${this.projectKey}`;
    return this._fetchFromSonar(endpoint);
  }

  async getCodeSmells() {
    /**
     * Obtiene code smells específicos
     */
    const endpoint = `${SONAR_URL}/api/issues/search?componentKeys=${this.projectKey}&types=CODE_SMELL`;
    return this._fetchFromSonar(endpoint);
  }

  async getSecurityHotspots() {
    /**
     * Obtiene vulnerabilidades de seguridad
     */
    const endpoint = `${SONAR_URL}/api/hotspots/search?projectKey=${this.projectKey}`;
    return this._fetchFromSonar(endpoint);
  }

  async getTestCoverage() {
    /**
     * Obtiene métricas de cobertura de tests
     */
    const endpoint = `${SONAR_URL}/api/measures/component?component=${this.projectKey}&metricKeys=coverage,lines_to_cover`;
    return this._fetchFromSonar(endpoint);
  }

  async _fetchFromSonar(endpoint) {
    return new Promise((resolve, reject) => {
      const options = {
        headers: {
          'Authorization': `Bearer ${SONAR_TOKEN}`,
          'Content-Type': 'application/json'
        }
      };

      http.get(endpoint, options, (res) => {
        let data = '';
        res.on('data', chunk => data += chunk);
        res.on('end', () => resolve(JSON.parse(data)));
      }).on('error', reject);
    });
  }

  generateReport() {
    /**
     * Genera reporte de contexto para el agente IA
     */
    return `
# SonarQube Analysis Report

## Quality Status
- Code Smell Density: [XX]%
- Security Rating: [A|B|C|D|E]
- Maintainability: [High|Medium|Low]

## Recommendations
1. Fix critical issues first
2. Improve test coverage
3. Reduce cognitive complexity
    `;
  }
}

// Servidor MCP expone endpoints
const server = http.createServer(async (req, res) => {
  const sonar = new SonarQubeMCPServer();
  const parsedUrl = url.parse(req.url, true);

  res.setHeader('Content-Type', 'application/json');

  try {
    switch (parsedUrl.pathname) {
      case '/issues':
        res.end(JSON.stringify(await sonar.getProjectIssues()));
        break;
      case '/code-smells':
        res.end(JSON.stringify(await sonar.getCodeSmells()));
        break;
      case '/security':
        res.end(JSON.stringify(await sonar.getSecurityHotspots()));
        break;
      case '/coverage':
        res.end(JSON.stringify(await sonar.getTestCoverage()));
        break;
      case '/report':
        res.end(sonar.generateReport());
        break;
      default:
        res.statusCode = 404;
        res.end(JSON.stringify({ error: 'Endpoint not found' }));
    }
  } catch (error) {
    res.statusCode = 500;
    res.end(JSON.stringify({ error: error.message }));
  }
});

server.listen(3000, () => {
  console.log('SonarQube MCP Server running on :3000');
});
```

---

## 🚀 Parte 3: Integración en Workflow Spec-Driven

### 3.1 Enriquecer Constitution con Calidad

En `constitution.md`, añade sección de calidad medible:

```markdown
## Métricas de Calidad (Validadas por SonarQube)

- **Code Smell Density:** < 3%
- **Test Coverage:** ≥ 80%
- **Duplicated Lines:** < 3%
- **Cognitive Complexity:** < 10 por función
- **Security Rating:** A (sin vulnerabilidades)
```

### 3.2 Usar SonarQube en Specification Clarification

Comando sugerido en tu agente IA:

```
/speckit.specify

"Crear Photo Album App con:
- Requisitos testables (SonarQube validará)
- Test-first approach
- Coverage mínimo 80%
- Métricas: use /mcp sonarqube-check después"
```

### 3.3 Plan con Validación Automática

En `plan.md`, integra validaciones:

```markdown
## Validación de Plan (SonarQube MCP)

### Analisis Anterior (Baseline)
- Coverage: N/A (proyecto nuevo)
- Debt: 0

### Análisis Esperado (Después)
- Coverage: ≥ 80%
- Code Smells: < 5
- Security: 0 hotspots críticos

### CI/CD Integration
```yaml
- Run: sonar-scanner
- Check: SonarQube quality gate
- Fail if: Coverage < 80% OR critical issues
```
```

### 3.4 Tasks con Validación Automática

Añade task de validación:

```markdown
### Task: SonarQube Quality Gate

- **Archivos:** CI/CD configuration
- **Comando:** `sonar-scanner`
- **Criterios:**
  - [ ] No critical issues
  - [ ] Coverage ≥ 80%
  - [ ] Security A rating
  - [ ] Quality gate passed

- **En caso de fallo:** Agente IA recibe reporte MCP
```

---

## 🧪 Parte 4: Ejecutar Análisis SonarQube

### 4.1 Analizar Código Existente

```bash
# Ejecutar scanner
sonar-scanner

# Esperar a que complete (2-5 min)
# Resultado en: http://localhost:9000/projects
```

### 4.2 Interpretar Resultados

```
Quality Gate Status: ✅ PASSED / ❌ FAILED

Métricas Principales:
├── Lines of Code: 2,345
├── Duplicated Lines: 2% ✓
├── Coverage: 82% ✓
├── Code Smells: 3 (Minor)
├── Security Hotspots: 0 ✓
└── Cognitive Complexity: 8 (Avg)
```

### 4.3 Consultar via MCP en Agente IA

Comando para tu agente (ejemplo Claude):

```
/mcp sonarqube-report

Respuesta esperada:
"El análisis SonarQube muestra:
- Coverage excelente (82%)
- 3 code smells menores en AlbumGrid.vue (lines 45-50)
- Recomendación: refactorizar línea 50 para reducir complejidad
- Security: Sin vulnerabilidades 🎉"
```

---

## 📋 Parte 5: Ejercicio Práctico Guiado

### Ejercicio 5.1: Corregir Código Basado en SonarQube

**Instrucciones:**

1. **Ejecuta análisis:**
   ```bash
   sonar-scanner
   ```

2. **Identifica primer code smell:**
   - Abre http://localhost:9000
   - Proyecto → Issues
   - Haz click en primer issue

3. **En tu agente IA (Claude, etc):**
   ```
   /mcp sonarqube-code-smell
   
   Pide al agente:
   "Fix the first code smell found by SonarQube
   according to constitutional principles"
   ```

4. **El agente:**
   - Consulta SonarQube MCP
   - Lee constitution.md
   - Genera fix
   - Muestra cambios

5. **Vuelve a ejecutar:**
   ```bash
   sonar-scanner
   ```

6. **Verifica:**
   - Issue debe desaparecer
   - Coverage se mantiene o mejora

---

### Ejercicio 5.2: Test Coverage Gap

**Objetivo:** Aumentar cobertura de 82% a 90%

1. **Ejecutar análisis:**
   ```bash
   npm run test -- --coverage
   sonar-scanner
   ```

2. **Ver gaps:**
   ```bash
   open http://localhost:9000/dashboard?id=photo-album-app
   Haz click en "Coverage"
   ```

3. **Pedir al agente IA:**
   ```
   /mcp sonarqube-coverage-gap
   
   "Write tests for uncovered lines in:
   - AlbumStore.ts (lines 45-67)
   - PhotoService.ts (lines 102-115)
   
   Target: 90% coverage"
   ```

4. **Agente genera tests**

5. **Verifica:**
   ```bash
   npm run test
   sonar-scanner
   ```

---

### Ejercicio 5.3: Security Hotspot Analysis

**Objetivo:** Asegurar código contra vulnerabilidades

1. **Ejecutar scan:**
   ```bash
   sonar-scanner
   ```

2. **Revisar Security Hotspots:**
   - Dashboard → Security
   - Ver cualquier hotspot encontrado

3. **Consultar MCP:**
   ```
   /mcp sonarqube-security
   
   "Review all security hotspots and explain
   the risk using OWASP Top 10 framework"
   ```

4. **Agente analiza y recomienda fixes**

---

## 📊 Parte 6: Métricas a Seguir

### Dashboard Recomendado

Crea un dashboard personal en SonarQube:

```
┌─────────────────────────────────────┐
│  Photo Album App - Quality Overview │
├─────────────────────────────────────┤
│ Coverage:          ████████░░ 82%   │
│ Duplications:      ██░░░░░░░░ 2%    │
│ Code Smells:       ███░░░░░░░ 3     │
│ Security Rating:   A (No issues)    │
│ Reliability:       A (No bugs)      │
│ Maintainability:   A (Good)         │
└─────────────────────────────────────┘
```

### Métricas por Archivo

Monitorear cambios en archivos clave:

```
AlbumStore.ts
- Coverage: 90%
- Code Smells: 1 (Minor)
- Cognitive Complexity: 7
- Trend: ↑ (improving)

PhotoService.ts
- Coverage: 75%
- Code Smells: 2 (Minor)
- Cognitive Complexity: 9
- Trend: ↓ (needs attention)
```

---

## ✅ Checklist Final del Ejercicio

- [ ] SonarQube instalado y ejecutando en :9000
- [ ] Token generado y guardado
- [ ] MCP server escrito y funcionando
- [ ] Integración en `.claude.json` o equivalente
- [ ] Constitution.md incluye métricas de calidad
- [ ] Análisis inicial ejecutado
- [ ] 5.1: Code smell corregido
- [ ] 5.2: Coverage > 90%
- [ ] 5.3: Security hotspots revisados
- [ ] Dashboard personalizado creado

---

## 🎓 Lecciones Clave

1. **SonarQube MCP** enriquece el contexto del agente IA
2. **Métricas objetivas** reemplazan intuición sobre calidad
3. **Spec-Driven + SonarQube** = desarrollo confiable
4. **Feedback en vivo** acelera detección de issues
5. **Constitution validada** asegura consistencia

---

## 📚 Recursos Adicionales

### Documentación
- [SonarQube Official Docs](https://docs.sonarsource.com/sonarqube/)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [SonarQube API](https://sonarqube.domain.com/web_api)

### Herramientas
- SonarQube Docker: `docker pull sonarqube:latest`
- Sonar Scanner: `npm install -g sonar-scanner`
- Quality Gates: Configurables en SonarQube UI

### Ejemplos
- [Spec Kit + Quality Gates](https://github.com/github/spec-kit/examples/quality)
- [MCP Toolkit](https://github.com/modelcontextprotocol/toolkit)

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
**Tiempo Estimado:** 2-3 horas  
**Requisitos Previos:** Haber completado ejemplo photo-album-app

**¡Éxito con tu integración de SonarQube MCP! 🎉**
