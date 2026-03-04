# Spec Kit - Repositorio de Referencia

Este repositorio contiene una guía completa sobre **Spec-Driven Development** con GitHub Spec Kit, incluyendo una aplicación de ejemplo y ejercicios prácticos.

## 📁 Estructura del Repositorio

```
spec-kit-repo/
├── README.md                          # Este archivo
├── SpecKit.md                         # Guía completa de Spec Kit
├── examples/
│   └── photo-album-app/
│       ├── README.md                  # Documentación de la app
│       ├── spec.md                    # Especificación funcional
│       ├── plan.md                    # Plan técnico con Contex7
│       ├── constitution.md            # Principios del proyecto
│       ├── tasks.md                   # Lista de tareas
│       ├── src/                       # Código fuente (placeholder)
│       ├── tests/                     # Tests (placeholder)
│       └── docker-compose.yml         # Infraestructura
├── exercises/
│   └── sonarqube-mcp-exercise.md      # Ejercicio con SonarQube MCP
└── .gitignore                         # Git ignore
```

## 🎯 Contenido

### 1. **SpecKit.md**
Guía completa sobre Spec-Driven Development con:
- Conceptos fundamentales
- Flujo de trabajo paso a paso
- Comandos disponibles
- Mejores prácticas
- Troubleshooting

### 2. **Ejemplo: Photo Album App**
Aplicación de gestión de álbumes de fotos con:
- **Constitution**: Principios del proyecto
- **Specification**: Requisitos funcionales (sin tech)
- **Plan**: Implementación técnica con **Contex7**
- **Tasks**: Desglose de tareas
- **Estructura de código**: Estructura básica del proyecto

**Por qué Contex7 en la fase de plan:**
- Gestiona múltiples contextos técnicos
- Mapea dependencias complejas
- Documenta decisiones arquitectónicas
- Facilita colaboración en equipos distribuidos
- Permite rastrear cambios de contexto

### 3. **Ejercicio: SonarQube MCP Integration**
Ejercicio práctico que integra:
- SonarQube como Model Context Protocol (MCP)
- Análisis de código automático
- Validación de calidad
- Generación de reportes
- Integración con Spec Kit

## 🚀 Comenzar

### Opción 1: Explorar la Guía
```bash
cat SpecKit.md
```

### Opción 2: Estudiar el Ejemplo
```bash
cd examples/photo-album-app
cat README.md      # Overview
cat spec.md        # Qué construir
cat plan.md        # Cómo construirlo con Contex7
cat tasks.md       # Tareas específicas
```

### Opción 3: Hacer el Ejercicio
```bash
cd exercises
cat sonarqube-mcp-exercise.md
```

## 📊 Flujo Recomendado

```
1. Lee SpecKit.md
   ↓
2. Estudia photo-album-app/
   - spec.md → plan.md → tasks.md
   ↓
3. Completa sonarqube-mcp-exercise.md
   ↓
4. Crea tu propio proyecto con Spec Kit
```

## 🔗 Enlaces Útiles

- [GitHub Spec Kit](https://github.com/github/spec-kit)
- [Documentación Oficial](https://github.github.io/spec-kit/)
- [Contex7 Documentation](https://contex7.io)
- [SonarQube](https://www.sonarsource.com/products/sonarqube/)
- [Model Context Protocol](https://modelcontextprotocol.io/)

## 📚 Recursos Adicionales

- Agentes IA Soportados: Claude, Copilot, Cursor, Gemini, etc.
- Templates: Constitution, Spec, Plan, Tasks
- Scripts: Automatización de procesos
- Ejemplos: Diversas tech stacks

## 🤝 Contribuciones

Si encuentras mejoras o quieres añadir ejemplos:
1. Fork este repositorio
2. Crea una rama: `git checkout -b feature/mi-mejora`
3. Commit: `git commit -m "Añade mejora"`
4. Push: `git push origin feature/mi-mejora`
5. Abre un Pull Request

## 📄 Licencia

MIT License - Libre para usar, modificar y distribuir

---

**Creado con ❤️ para la comunidad de Spec-Driven Development**
