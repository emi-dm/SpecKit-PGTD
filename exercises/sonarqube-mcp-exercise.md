# 🔍 Ejercicio: Incorporar SonarQube para Mantenibilidad

## Objetivo

Integrar **SonarQube** en el flujo de desarrollo de Photo Album App para garantizar que la aplicación sea mantenible, con código de calidad y libre de deuda técnica.

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

### 1. Instalar y Configurar SonarQube

Instala SonarQube (Docker recomendado):
```bash
docker run -d -p 9000:9000 sonarqube:latest
```

Accede a http://localhost:9000 y crea un token de API para autenticación.

### 2. Analizar Photo Album App

Configura SonarQube para analizar el código de Photo Album App:
- Crea archivo `sonar-project.properties`
- Ejecuta `sonar-scanner` en el directorio del proyecto
- Revisa el dashboard de resultados

### 3. Identificar Problemas de Mantenibilidad

Documenta en `SONARQUBE_REPORT.md`:
- **Cobertura actual** vs objetivo (80%)
- **Code Smells** encontrados
- **Complejidad** de funciones principales
- **Vulnerabilidades** de seguridad
- **Duplicaciones** de código

### 4. Integrar en Spec-Driven

Actualiza los documentos de Photo Album App:

**constitution.md:**
- Añade métricas de SonarQube como principios validables
- Define qué cobertura, complejidad y seguridad son aceptables

**plan.md:**
- Documenta cómo se valida calidad con SonarQube
- Especifica que análisis se ejecutan en cada fase

**tasks.md:**
- Añade task final: "Pasar quality gate de SonarQube"
- Incluye criterios: Coverage ≥ 80%, Sin hotspots críticos, Deuda técnica aceptable

### 5. Mejorar la Mantenibilidad

Basado en el análisis de SonarQube:
- Aumenta cobertura de tests hasta 85%+
- Reduce code smells mayores a 3
- Refactoriza funciones con complejidad > 10
- Elimina código duplicado

Re-ejecuta análisis y verifica mejoras.

### 6. Automatizar Validación

Configura SonarQube Quality Gate:
- Establece reglas que deben cumplirse
- El pipeline rechaza cambios que violan calidad
- El agente IA recibe feedback de SonarQube antes de mergear

---

## Criterios de Éxito

- ✅ SonarQube configurado y ejecutándose
- ✅ Análisis inicial realizado en Photo Album App
- ✅ Reporte de problemas documentado
- ✅ Constitution y Plan actualizados con validación
- ✅ Tasks incluyen calidad como criterio
- ✅ Coverage mejorado a ≥ 85%
- ✅ Code Smells reducidos
- ✅ Quality Gate establecido

---

## Entrega

Crea carpeta `sonarqube/` con:
- `sonar-project.properties` - Configuración
- `SONARQUBE_REPORT.md` - Análisis inicial
- `IMPROVEMENTS.md` - Cambios realizados
- Screenshot del dashboard de SonarQube

---

## Beneficio

Al integrar SonarQube, garantizas que:
- La aplicación es **mantenible** según principios definidos
- Los **cambios futuros** no degradan calidad
- El **agente IA** tiene criterios objetivos de éxito
- La **deuda técnica** se gestiona proactivamente
