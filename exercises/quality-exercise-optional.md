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

# 🔍 Ejercicio: Incorporar SonarQube MCP para Mantenibilidad

## Objetivo

Integrar **SonarQube como Model Context Protocol (MCP)** usando **docker-sonarqube-setup** en el flujo de desarrollo de Photo Album App para garantizar mantenibilidad automática a través del agente IA.

---

## Descripción del Ejercicio

### ¿Qué es SonarQube MCP?

MCP (Model Context Protocol) permite que tu agente IA (Claude, Copilot, etc) consulte SonarQube directamente:

```
Agente IA (Claude/Copilot)
        ↓
   MCP Server
        ↓
   SonarQube
        ↓
Análisis de calidad
```

El agente IA **recibe contexto en vivo** sobre calidad, en lugar de ejecutar comandos manualmente.

### ¿Por qué es importante?

La **Constitution** de Photo Album App especifica:
- Código legible y mantenible
- 80% cobertura de tests mínimo
- Sin vulnerabilidades de seguridad
- Baja complejidad

Con **MCP, el agente IA valida automáticamente** estos principios mientras desarrolla.

---

## Tareas del Ejercicio

### 1. Iniciar docker-sonarqube-setup

```bash
# Clonar repositorio
git clone https://github.com/emi-dm/docker-sonarqube-setup.git
cd docker-sonarqube-setup

# Iniciar servicios
./scripts/setup.sh start

# Verificar
./scripts/verify.sh
```

**Resultado esperado:**
- SonarQube corriendo en http://localhost:9000
- PostgreSQL en background
- Acceso: admin / admin

### 2. Generar Token de API

1. Accede a http://localhost:9000
2. Login: `admin` / `admin`
3. Ve a **My Account → Security → Tokens**
4. Crea nuevo token: `spec-kit-mcp`
5. Copia el token (aparece solo una vez)
6. Guárdalo en `.env` como:
   ```
   SONARQUBE_TOKEN=squ_xxxxx
   SONARQUBE_URL=http://sonarqube:9000/
   ```

**Entrega:**
- [ ] Token generado
- [ ] Token guardado en `.env`

### 3. Configurar MCP en tu Agente IA

**Para Claude Code:**

Edita `.claude.json` en tu proyecto:
```json
{
  "mcp": {
    "sonarqube": {
      "type": "stdio",
      "command": "docker",
      "args": [
        "run", "-i", "--rm", "--init",
        "--pull=always",
        "-e", "SONARQUBE_TOKEN",
        "-e", "SONARQUBE_URL",
        "--network", "sonarqube-net",
        "mcp/sonarqube"
      ],
      "env": {
        "SONARQUBE_TOKEN": "squ_xxxxx",
        "SONARQUBE_URL": "http://sonarqube:9000/"
      }
    }
  }
}
```

**Para otros agentes:** Consulta su documentación de MCP integration.

### 4. Abrir Photo Album App con Agente IA

Abre tu agente IA (Claude Code, etc) en el directorio de Photo Album App:

```bash
cd ../photo-album-app
# Abrir con tu agente IA
code .  # para VS Code + Claude Code
```

### 5. Consultar SonarQube a través del MCP

En tu agente IA, usa comandos como:

```
#sonarqube-tool (contexto adicional para guiar uso de tool)

"¿Cuáles son los principales problemas de calidad en este proyecto?"

"¿Cuál es el coverage actual?"

"¿Hay vulnerabilidades de seguridad?"

"¿Qué funciones tienen complejidad muy alta?"
```

El MCP responderá con análisis en vivo de SonarQube.

### 6. Documentar Hallazgos

Crea `SONARQUBE_ANALYSIS.md`:

```markdown
# Análisis SonarQube vía MCP

## Consultas Realizadas

### 1. Estado General
[Respuesta del MCP]

### 2. Coverage
[Respuesta del MCP]

### 3. Vulnerabilidades
[Respuesta del MCP]

### 4. Code Smells
[Respuesta del MCP]

## Planes de Mejora

[Basado en recomendaciones del MCP]
```

### 7. Usar MCP para Mejorar Código

**Solicita al agente (con MCP disponible):**

```
"Basado en el análisis de SonarQube:
1. Aumenta coverage a 85%
2. Refactoriza funciones con complejidad > 10
3. Elimina code smells principales

Usa @sonarqube para verificar mejoras"
```

El agente IA:
- Consulta SonarQube vía MCP
- Ve exactamente qué está mal
- Genera fixes específicos
- Verifica que se resuelve con MCP

### 8. Integrar en Spec-Driven

**Actualiza constitution.md:**
```markdown
## Validación Automática (SonarQube MCP)

Toda la validación de calidad ocurre automáticamente a través del MCP:
- Coverage: ≥ 80% (validado por MCP)
- Code Smells: ≤ 3 (detectados por MCP)
- Vulnerabilidades: 0 (reportadas por MCP)
```

**Actualiza plan.md:**
```markdown
## Garantía de Calidad con MCP

El agente IA tiene acceso a SonarQube vía MCP:
- Consulta calidad en vivo
- Recibe recomendaciones específicas
- Valida fixes automáticamente
```

**Actualiza tasks.md:**
```markdown
### Task: Validación SonarQube MCP

- Usar: @sonarqube en agente IA
- Verificar: Coverage ≥ 85%
- Criterio: Code Smells < 3
- Método: MCP queries + fixes
```

---

## Criterios de Éxito

- ✅ docker-sonarqube-setup corriendo
- ✅ Token de SonarQube generado
- ✅ MCP configurado en agente IA
- ✅ Consultas MCP funcionando (@sonarqube)
- ✅ Hallazgos documentados en markdown
- ✅ Coverage mejorado a ≥ 85% (verificado con MCP)
- ✅ Code Smells reducidos (verificado con MCP)
- ✅ Spec-Driven documents actualizados

---

## Entrega

Crea carpeta `sonarqube-mcp/` con:

```
sonarqube-mcp/
├── .env                         # Token configurado
├── SONARQUBE_ANALYSIS.md        # Hallazgos del MCP
├── IMPROVEMENTS.md              # Mejoras realizadas
└── mcp-queries.log              # Transcript de @sonarqube
```

Además, actualiza:
- `constitution.md` - Con validación MCP
- `plan.md` - Con estrategia MCP
- `tasks.md` - Con criterios MCP

---

## Flujo Completo

```
1. docker-sonarqube-setup start
        ↓
2. Generar token SonarQube
        ↓
3. Configurar .claude.json (MCP)
        ↓
4. Abrir proyecto con agente IA
        ↓
5. @sonarqube "¿Problemas de calidad?"
        ↓
6. MCP responde con análisis
        ↓
7. Agente IA mejora código basado en MCP
        ↓
8. @sonarqube "¿Se resolvió?"
        ↓
9. Documentar mejoras
        ↓
10. Actualizar Spec-Driven documents
```

---

## Ventajas vs sonar-scanner

| Aspecto | sonar-scanner | MCP |
|---------|---------------|-----|
| **Automatización** | Manual | Automática |
| **Integración IA** | No | Sí |
| **Feedback tiempo-real** | No | Sí |
| **Desarrollo iterativo** | Lento | Rápido |
| **Contexto en IA** | No | Completo |

---

## Beneficios

Al usar SonarQube MCP:

✅ El agente IA **ve** problemas de calidad  
✅ Genera **fixes específicos** basado en análisis  
✅ **Valida** automáticamente que se resuelven  
✅ Mantiene código **mantenible** durante desarrollo  
✅ No requiere comandos manuales  
✅ **Feedback en vivo** mientras desarrollas  

---

## Referencias

- [docker-sonarqube-setup](https://github.com/emi-dm/docker-sonarqube-setup)
- [MCP Integration Guide](https://github.com/emi-dm/docker-sonarqube-setup#-mcp-integration)
- [Model Context Protocol](https://modelcontextprotocol.io/)
