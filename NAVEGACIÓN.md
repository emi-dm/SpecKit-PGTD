# 📖 GUÍA DE NAVEGACIÓN - Spec Kit Repository

## 🎯 ¿Por dónde empiezo?

### Si eres completamente nuevo en Spec Kit:

```
1. Lee README.md (este directorio)
   ↓
2. Lee SpecKit.md (guía completa)
   ↓
3. Estudia examples/photo-album-app/
   ├── Primero: README.md
   ├── Luego: constitution.md
   ├── Luego: spec.md
   └── Finalmente: plan.md → tasks.md
   ↓
4. Intenta el ejercicio: exercises/sonarqube-mcp-exercise.md
   ↓
5. Crea tu propio proyecto con Spec Kit
```

### Si quieres aprender rápido:

```
1. 5 min: Lee README.md
2. 30 min: Lee Photo Album App README.md
3. 15 min: Lee plan.md (énfasis en Contex7)
4. 1 hora: Haz el ejercicio de SonarQube MCP
```

### Si solo necesitas referencia:

```
- SpecKit.md → Busca en Ctrl+F lo que necesitas
- examples/photo-album-app/plan.md → Entiende Contex7
- exercises/sonarqube-mcp-exercise.md → Integra calidad
```

---

## 📂 Estructura Explicada

### Raíz del Repositorio

```
spec-kit-repo/
├── README.md                    ← Intro y estructura
├── SpecKit.md                   ← GUÍA PRINCIPAL (35KB)
├── NAVEGACIÓN.md                ← Este archivo
├── .gitignore
└── ejemplos y ejercicios
```

### 📁 examples/photo-album-app/

**¿Qué es?** Una aplicación completa de gestión de fotos, usando Spec-Driven Development.

**Archivos:**

```
photo-album-app/
├── README.md                    (5 min) Descripción general
│                               - Características
│                               - Tech stack
│                               - Estructura del proyecto
│
├── constitution.md              (10 min) Principios del proyecto
│                               - Calidad de código
│                               - Estándares de pruebas
│                               - UX/UI principles
│                               - Performance budget
│
├── spec.md                      (15 min) ¿QUÉ construir?
│                               - Requisitos funcionales (RF-1 a RF-7)
│                               - Requisitos no-funcionales
│                               - Historias de usuario (HU)
│                               - Out of scope
│                               📌 SIN tecnologías específicas
│
├── plan.md                      (20 min) ¿CÓMO construirlo?
│                               - Introducción a Contex7
│                               - ADRs (Architecture Decision Records)
│                               - Tech stack justificado
│                               - Data flow
│                               - Performance budget
│                               📌 Aquí es donde brilla Contex7
│
├── tasks.md                     (15 min) Tareas ejecutables
│                               - 35 tasks desglosadas
│                               - Dependencias claras
│                               - Parallelización [P]
│                               - Por fases
│
└── docker-compose.yml           (5 min) Infraestructura
                                - Dev server
                                - Test runner
                                - Preview server
```

### 📁 exercises/

**¿Qué es?** Ejercicios prácticos para profundizar conocimiento.

```
exercises/
└── sonarqube-mcp-exercise.md    (1-3 horas) Ejercicio de calidad
                                - Qué es MCP
                                - Instalar SonarQube
                                - Crear MCP server
                                - Integrar en Spec Kit
                                - 3 ejercicios prácticos
                                - Métricas a seguir
```

---

## ⏱️ Plan de Estudio Recomendado

### Día 1: Fundamentos (2-3 horas)

**Mañana:**
- [ ] Lee README.md (10 min)
- [ ] Lee SpecKit.md secciones 1-4 (45 min)
- [ ] Toma notas sobre conceptos clave

**Tarde:**
- [ ] Lee SpecKit.md secciones 5-6 (30 min)
- [ ] Revisa photo-album-app/README.md (15 min)
- [ ] Entiende flujo Spec-Driven

**Notas:**
```markdown
CONCEPTOS CLAVE Día 1:
1. Spec-Driven = Especificaciones ejecutables
2. Flujo: Constitution → Spec → Plan → Tasks → Implementation
3. Plan con Contex7 = Decisiones documentadas
```

---

### Día 2: Análisis Profundo (2-3 horas)

**Mañana:**
- [ ] Lee constitution.md (10 min)
- [ ] Lee spec.md completo (20 min)
- [ ] Estudia diferencia entre funcional y no-funcional

**Tarde:**
- [ ] Lee plan.md completo (30 min)
- [ ] ⭐ Enfócate en sección Contex7
- [ ] Entiende cada ADR (Architecture Decision Record)

**Ejercicio:**
```
Pregunta para ti mismo:
- ¿Por qué Vue 3 en lugar de React?
- ¿Por qué IndexedDB en lugar de localStorage?
- ¿Cuáles son las implicaciones?
```

---

### Día 3: Práctica (2-3 horas)

**Mañana:**
- [ ] Lee tasks.md (20 min)
- [ ] Identifica dependencias entre tasks
- [ ] Marca tasks que podrían ser paralelas [P]

**Tarde:**
- [ ] Comienza sonarqube-mcp-exercise.md (1 hora)
- [ ] Partes 1-2: Instalación y setup
- [ ] Familiarízate con SonarQube UI

---

### Día 4: Integración (2-3 horas)

**Completo:**
- [ ] Termina sonarqube-mcp-exercise.md
- [ ] Ejecuta Parte 4 (análisis)
- [ ] Haz Parte 5 (ejercicios prácticos)
- [ ] Completa Parte 6 (métricas)

**Resultado:**
✅ SonarQube MCP integrado  
✅ Entiendes cómo validar calidad  
✅ Listo para tu propio proyecto

---

### Día 5+: Tu Propio Proyecto

Usa este repositorio como referencia para:

1. **Crear un nuevo proyecto con Spec Kit:**
   ```bash
   specify init mi-proyecto --ai claude
   ```

2. **Seguir el flujo:**
   - `/speckit.constitution` - Define principios
   - `/speckit.specify` - Describe tu app
   - `/speckit.plan` - Planifica tech stack (con Contex7)
   - `/speckit.tasks` - Genera tareas
   - `/speckit.implement` - Implementa

3. **Integrar SonarQube:**
   - Sigue pasos del ejercicio
   - Adapta a tu proyecto
   - Valida calidad en cada iteración

---

## 🔍 Búsqueda Rápida

### Busco información sobre...

**Spec-Driven Development**
→ SpecKit.md, sección "¿Qué es Spec-Driven Development?"

**Contex7 / Architecture Decisions**
→ examples/photo-album-app/plan.md, secciones 1-2

**Tech Stack Específico**
→ examples/photo-album-app/plan.md, sección "Tech Stack Justificado"

**Cómo Estructurar un Proyecto**
→ examples/photo-album-app/tasks.md

**SonarQube y Calidad de Código**
→ exercises/sonarqube-mcp-exercise.md

**Model Context Protocol (MCP)**
→ exercises/sonarqube-mcp-exercise.md, Parte 1

**Mejores Prácticas**
→ SpecKit.md, sección "Mejores Prácticas"

**Troubleshooting**
→ SpecKit.md, sección "Troubleshooting"

---

## 💡 Tips de Lectura

### Lectura Efectiva de Archivos MD

```markdown
1. Lee el título y descripción
   ↓
2. Revisa tabla de contenidos
   ↓
3. Lee introducción
   ↓
4. Busca secciones relevantes para ti
   ↓
5. Regresa a conceptos que no entendiste
   ↓
6. Toma notas clave
```

### Usa Estos Patrones:

**`[P]`** = Puede hacerse en paralelo  
**`→`** = Depende de  
**`✅`** = Completado  
**`📌`** = Importante  
**`⚠️`** = Advertencia  

---

## 🎓 Conceptos Clave del Repositorio

### 1. Especificación Funcional vs Técnica

```
SPEC.MD (Funcional)
"Crear álbumes, subir fotos, galería"
↓ SIN detalles técnicos
↓ Describe QUÉ, no CÓMO

PLAN.MD (Técnico)
"Vue 3, IndexedDB, Pinia"
↓ CON detalles técnicos
↓ Describe CÓMO y por QUÉ
```

### 2. Contex7: Decisiones Documentadas

```
Cada decisión arquitectónica tiene:
- Contexto (por qué surgió la decisión)
- Decisión (qué se decidió)
- Consecuencias (qué cambió)
- Alternativas consideradas (por qué no)
```

### 3. Tasks: Trabajo Organizado

```
Cada task es:
- Independiente pero con dependencias claras
- Asignable a un desarrollador
- Ejecutable en orden
- Testeable
```

---

## ❓ FAQ del Repositorio

**P: ¿Necesito hacer todo en orden?**  
R: No. Puedes saltar entre secciones. Pero primer viaje, recomendamos orden.

**P: ¿Puedo usar esto como template?**  
R: ¡Sí! Copia ejemplos/photo-album-app/ y adapta a tu proyecto.

**P: ¿Dónde pongo mi código?**  
R: Crea un nuevo directorio: `examples/mi-app/`

**P: ¿Qué si no entiendo Contex7?**  
R: Lee plan.md sección "Introducción: ¿Por Qué Contex7 en la Fase de Plan?"

**P: ¿SonarQube es obligatorio?**  
R: No, pero recomendado. El ejercicio es opcional pero muy valioso.

**P: ¿Puedo modificar estos archivos?**  
R: ¡Por supuesto! Son educativos. Haz mejoras y propón cambios.

---

## 🚀 Próximos Pasos

Después de leer este repositorio:

1. **Comprende** Spec-Driven Development
2. **Practica** con Photo Album App ejemplo
3. **Aprende** SonarQube MCP integration
4. **Crea** tu propio proyecto
5. **Comparte** tu experiencia

---

## 📞 Ayuda y Soporte

Si tienes preguntas:

1. **Revisa SpecKit.md** - Sección Troubleshooting
2. **Busca en este archivo** - CTRL+F
3. **Consulta links externos** - En cada documento
4. **Abre una issue** - En GitHub si es necesario

---

## 📊 Resumen del Repositorio

| Elemento | Tiempo | Dificultad | Valor |
|----------|--------|-----------|-------|
| SpecKit.md | 2 horas | Fácil | Alto |
| Photo Album App | 1.5 horas | Media | Alto |
| SonarQube Exercise | 2-3 horas | Media | Muy Alto |
| Total | 5-6 horas | Media | ⭐⭐⭐⭐⭐ |

---

**¡Bienvenido a Spec-Driven Development! 🎉**

Comienza leyendo **README.md** o salta directamente a **SpecKit.md**.
