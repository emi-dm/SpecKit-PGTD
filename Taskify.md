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

## Ejemplo Práctico: Aplicación Taskify

### Caso de Uso: Sistema de Gestión de Tareas en Equipo

#### PASO 1: Constitución

```markdown
# Principios del Proyecto Taskify

## Calidad de Código

- Código limpio y legible
- Nomenclatura consistente
- Máximo 100 líneas por función

## Estándares de Pruebas

- 80% cobertura de código
- Pruebas unitarias para lógica
- Pruebas E2E para flujos críticos

## Consistencia UX

- Paleta de colores definida
- Tamaño mínimo de botones: 44px
- Tiempo de respuesta < 200ms

## Performance

- First Contentful Paint < 2s
- Tareas se cargan sin refrescar página
```

#### PASO 2: Especificación

```
/speckit.specify

"Desarrollar Taskify, una plataforma de productividad para equipos.
- Usuarios: 5 predefinidos (1 PM + 4 ingenieros)
- Proyectos: 3 proyectos de ejemplo
- Tablero Kanban: Columnas 'To Do', 'In Progress', 'In Review', 'Done'
- Características:
  * Arrastrar y soltar tareas entre columnas
  * Comentarios ilimitados por tarea
  * Asignar usuarios a tareas
  * Editar/eliminar comentarios propios
  * Tareas asignadas destacadas en color diferente
- No requiere login inicial"
```

**Resultado:** `spec.md` con historias de usuario

```markdown
## Historias de Usuario

### HU-1: Usuario selecciona su identidad

**Como** miembro del equipo
**Quiero** seleccionar mi usuario sin contraseña
**Para que** pueda acceder rápidamente a las tareas

**Criterios de Aceptación:**

- [ ] Se muestra lista de 5 usuarios
- [ ] Click en usuario carga vista principal
- [ ] No se requiere contraseña

### HU-2: Ver proyectos

**Como** usuario autenticado
**Quiero** ver lista de proyectos disponibles
**Para que** pueda seleccionar en cuál trabajar

### HU-3: Ver tablero Kanban

**Como** usuario en un proyecto
**Quiero** ver las tareas organizadas en columnas Kanban
**Para que** entienda el estado de las tareas
```

#### PASO 3: Plan Técnico

```
/speckit.plan

"Tech Stack:
- Frontend: Blazor Server con componentes interactivos
- Backend: ASP.NET Core REST API
- Base de Datos: PostgreSQL
- Real-time: SignalR para actualizaciones en tiempo real
- Drag&Drop: Biblioteca blazor-drag-drop

Arquitectura:
- API Projects Controller
- API Tasks Controller
- API Comments Controller
- SignalR Hub para notificaciones
- Database models: User, Project, Task, Comment"
```

**Resultado:** `plan.md`, `data-model.md`, `contracts/api-spec.json`

```json
{
  "api": {
    "projects": {
      "GET /api/projects": "Listar todos los proyectos",
      "GET /api/projects/{id}": "Obtener proyecto específico",
      "POST /api/projects": "Crear nuevo proyecto"
    },
    "tasks": {
      "GET /api/projects/{projectId}/tasks": "Listar tareas",
      "POST /api/tasks": "Crear tarea",
      "PUT /api/tasks/{id}": "Actualizar tarea (incluye mover entre columnas)",
      "DELETE /api/tasks/{id}": "Eliminar tarea"
    },
    "comments": {
      "POST /api/tasks/{taskId}/comments": "Añadir comentario",
      "PUT /api/comments/{id}": "Editar comentario propio",
      "DELETE /api/comments/{id}": "Eliminar comentario propio"
    }
  }
}
```

#### PASO 4: Generar Tareas

```
/speckit.tasks
```

**Resultado:** `tasks.md`

```markdown
## Tareas por Historia de Usuario

### HU-1: Seleccionar Usuario

#### Task 1.1: Crear modelo User

- Archivo: `Models/User.cs`
- Propiedades: Id, Name, Role, Avatar
- [P] Puede ejecutarse en paralelo

#### Task 1.2: Crear endpoint GET /users

- Archivo: `Controllers/UsersController.cs`
- Retorna lista de 5 usuarios
- Dependencia: Task 1.1

#### Task 1.3: Crear componente Blazor UserSelector

- Archivo: `Components/UserSelector.razor`
- Muestra 5 usuarios en grid
- Click selecciona usuario
- Dependencia: Task 1.2

### HU-2: Ver Proyectos

#### Task 2.1: Crear modelo Project

- Archivo: `Models/Project.cs`
- Propiedades: Id, Name, Description, Tasks[]
- [P] Paralelo con Task 1.1

#### Task 2.2: Seed data con 3 proyectos

- Archivo: `Data/DatabaseSeeder.cs`
- Inserta proyectos de ejemplo

...
```

#### PASO 5: Implementar

```markdown
/speckit.implement
```

El agente:

1. ✅ Valida que existen todos los artefactos
2. ✅ Crea estructura de carpetas
3. ✅ Ejecuta tareas en orden (respetando dependencias)
4. ✅ Genera Models, Controllers, Components
5. ✅ Configura base de datos
6. ✅ Crea pruebas
7. ✅ Compila y verifica

#### PASO 6: Validar Calidad con SonarQube

¿Se os ocurre cómo validar calidad de código automáticamente? ¡Exacto! Usando SonarQube a través del MCP.
