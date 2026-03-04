# 🔍 Ejercicio: Incorporar SonarQube para Mantenibilidad

## Objetivo

Usar **docker-sonarqube-setup** para integrar SonarQube en el flujo de desarrollo de Photo Album App y garantizar que la aplicación sea mantenible, con código de calidad y libre de deuda técnica.

---

## Descripción del Ejercicio

### ¿Qué es SonarQube?

SonarQube es una herramienta que analiza automáticamente la calidad del código identificando:
- **Code Smells**: Código que funciona pero es difícil de mantener
- **Bugs**: Problemas potenciales
- **Vulnerabilidades**: Riesgos de seguridad
- **Cobertura**: Porcentaje de código testado
- **Duplicaciones**: Código repetido innecesariamente

### ¿Por qué es importante en Spec-Driven Development?

La **Constitution** de Photo Album App especifica que el código debe ser:
- Legible y mantenible
- Con 80% cobertura de tests mínimo
- Sin vulnerabilidades de seguridad
- Bajo en complejidad

**SonarQube valida automáticamente** que estos principios se cumplen.

---

## Tareas del Ejercicio

### 1. Clonar y Configurar docker-sonarqube-setup

```bash
# Clonar el repositorio
git clone https://github.com/emi-dm/docker-sonarqube-setup.git
cd docker-sonarqube-setup

# Instalar (usando el script)
./scripts/setup.sh start

# Verificar que funciona
./scripts/verify.sh
```

**Resultado esperado:**
- SonarQube corriendo en http://localhost:9000
- PostgreSQL en background
- Todos los checks pasando

### 2. Generar Token de API

1. Accede a http://localhost:9000
2. Login: `admin` / `admin`
3. Cambia la contraseña (recomendado)
4. Ve a **My Account → Security → Tokens**
5. Genera nuevo token y guárdalo

**Entrega:**
- [ ] Token generado y guardado en `.env`

### 3. Analizar Photo Album App

En el directorio de Photo Album App:

```bash
# Instalar sonar-scanner
npm install -g sonar-scanner

# Crear sonar-project.properties
cat > sonar-project.properties << EOF
sonar.projectKey=photo-album-app
sonar.projectName=Photo Album App
sonar.sources=src
sonar.tests=tests
sonar.host.url=http://localhost:9000
sonar.login=<TU_TOKEN_AQUÍ>
EOF

# Ejecutar análisis
sonar-scanner
```

**Entrega:**
- [ ] Análisis completado
- [ ] Resultados visibles en http://localhost:9000

### 4. Identificar Problemas de Mantenibilidad

Documenta en `SONARQUBE_REPORT.md`:

```markdown
# Reporte SonarQube - Photo Album App

## Métricas Actuales

- **Cobertura**: XX% (objetivo: 80%)
- **Code Smells**: XX encontrados
- **Complejidad promedio**: XX
- **Vulnerabilidades**: XX
- **Duplicaciones**: XX%

## Problemas Principales

1. [Listar code smells principales]
2. [Listar vulnerabilidades]
3. [Listar funciones complejas]

## Plan de Mejora

- [ ] Aumentar cobertura a 85%+
- [ ] Reducir code smells a < 3
- [ ] Refactorizar complejidad
- [ ] Eliminar duplicaciones
```

### 5. Integrar en Spec-Driven

**Actualiza constitution.md:**
```markdown
## Validación Automática (SonarQube)

- Coverage: ≥ 80%
- Code Smells: ≤ 3
- Vulnerabilidades: 0
- Complejidad: < 10 por función
```

**Actualiza plan.md:**
```markdown
## Garantía de Calidad

SonarQube valida automáticamente que:
- Código es legible y mantenible
- Tests cubren casos críticos
- No hay vulnerabilidades
```

**Actualiza tasks.md:**
```markdown
### Task Final: Validación SonarQube

- Ejecutar: sonar-scanner
- Verificar: Todos los gates pasan
- Criterio: Coverage ≥ 80%
```

### 6. Mejorar la Mantenibilidad

Basado en el análisis:

1. **Aumenta Coverage:**
   - Identifica archivos con < 80% cobertura
   - Escribe tests para los gaps
   - Re-ejecuta análisis

2. **Reduce Code Smells:**
   - Refactoriza funciones largas
   - Elimina duplicaciones
   - Mejora nombres de variables

3. **Elimina Vulnerabilidades:**
   - Revisa security hotspots
   - Implementa fixes
   - Verifica que se resuelven

### 7. Automatizar Quality Gate

Configura regla en SonarQube:

1. En SonarQube → Administration → Quality Gates
2. Crea gate: "Photo Album App"
3. Añade condiciones:
   - Coverage < 80% = FAIL
   - New code smells = FAIL
   - Critical vulnerability = FAIL

---

## Criterios de Éxito

- ✅ SonarQube corriendo con docker-sonarqube-setup
- ✅ Análisis inicial ejecutado
- ✅ Reporte documentado en `SONARQUBE_REPORT.md`
- ✅ Constitution, Plan y Tasks actualizados
- ✅ Coverage mejorado a ≥ 85%
- ✅ Code Smells reducidos a < 3
- ✅ Quality Gate creado y pasando
- ✅ Re-análisis confirmando mejoras

---

## Entrega

Crea carpeta `sonarqube/` con:

```
sonarqube/
├── sonar-project.properties      # Configuración
├── SONARQUBE_REPORT.md           # Análisis inicial
├── IMPROVEMENTS.md               # Cambios realizados
└── screenshots/                  # Dashboard antes/después
```

Además, actualiza:
- `constitution.md` - Con métricas SonarQube
- `plan.md` - Con estrategia de validación
- `tasks.md` - Con task de quality gate

---

## Beneficios

Al integrar SonarQube, garantizas que:

✅ La aplicación es **mantenible** según principios definidos  
✅ Los **cambios futuros** no degradan calidad  
✅ El **agente IA** tiene criterios objetivos de éxito  
✅ La **deuda técnica** se gestiona proactivamente  
✅ La **seguridad** se valida automáticamente  

---

## Referencias

- [docker-sonarqube-setup](https://github.com/emi-dm/docker-sonarqube-setup)
- [SonarQube Documentation](https://docs.sonarsource.com/sonarqube/)
- [Quick Start Guide](https://github.com/emi-dm/docker-sonarqube-setup#-quick-start)
