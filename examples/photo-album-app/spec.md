# 📸 Especificación - Photo Album App

## Descripción General

**Photo Album App** es una aplicación web para organizar y visualizar álbumes de fotos. Los usuarios pueden crear álbumes, agruparlos por fecha, reorganizarlos mediante drag-and-drop, y visualizar fotos en una galería de tiles.

**Nota Importante:** Esta especificación describe **QUÉ** se va a construir, **NO CÓMO**. No menciona tecnologías específicas.

---

## 🎯 Visión del Producto

Permitir que usuarios organicen sus fotos de manera intuitiva, sin necesidad de sistemas complejos de carpetas. La experiencia debe ser visual, rápida y satisfactoria.

### Propuesta de Valor

| Aspecto | Beneficio |
|---------|-----------|
| **Simplicidad** | Interfaz intuitiva sin curva de aprendizaje |
| **Local** | Datos nunca dejan el dispositivo |
| **Rápido** | Respuesta inmediata a acciones |
| **Visual** | Galería de fotos como interfaz principal |
| **Flexible** | Reorganizar álbumes sin restricciones |

---

## 👥 Personas Usuarias

### Persona 1: Ana - Fotógrafa Casual

**Perfil:**
- Edad: 32 años
- Ocupación: Marketing Manager
- Experiencia Tech: Media
- Dispositivos: Desktop + Tablet

**Necesidades:**
- Organizar fotos de viajes
- Compartir álbumes con amigos
- Encontrar fotos rápidamente

**Frustraciones:**
- Miedo de perder fotos
- Nube limitada
- Procesos tediosos

### Persona 2: Carlos - Tech Enthusiast

**Perfil:**
- Edad: 28 años
- Ocupación: Developer
- Experiencia Tech: Alta
- Dispositivos: Desktop

**Necesidades:**
- Control local total
- Datos privados
- Herramientas flexibles

**Frustraciones:**
- Privacidad en servicios cloud
- Límites de almacenamiento
- Interfaces genéricas

---

## 📋 Requisitos Funcionales

### RF-1: Gestión de Álbumes

#### RF-1.1 Crear Álbum

**Descripción:**
Un usuario puede crear un nuevo álbum especificando:
- **Nombre**: Texto descriptivo (ej: "Vacaciones 2024")
- **Fecha**: Mes/Año de creación
- **Descripción** (Opcional): Notas adicionales

**Criterios de Aceptación:**
- [ ] Form con campos: nombre, fecha, descripción
- [ ] Validación: nombre no vacío, máximo 100 caracteres
- [ ] Fecha por defecto es hoy
- [ ] Mensaje de confirmación al crear
- [ ] Nuevo álbum aparece en la lista principal
- [ ] Álbum inicia sin fotos

**Flujo:**
```
Usuario → Click "Crear Álbum" → Form Modal 
→ Rellena datos → Click "Guardar" 
→ Álbum creado y visible en lista
```

#### RF-1.2 Editar Álbum

**Criterios de Aceptación:**
- [ ] Click en álbum abre opciones de edición
- [ ] Puede cambiar: nombre, fecha, descripción
- [ ] Cambios se guardan automáticamente
- [ ] Confirmación visual de guardado

#### RF-1.3 Eliminar Álbum

**Criterios de Aceptación:**
- [ ] Opción "Eliminar" con confirmación
- [ ] Si contiene fotos: pregunta si eliminar fotos también
- [ ] Álbum desaparece de lista
- [ ] Fotos se eliminan si corresponde

#### RF-1.4 Listar Álbumes

**Criterios de Aceptación:**
- [ ] Vista principal muestra todos los álbumes
- [ ] Álbumes ordenados por fecha (más recientes primero)
- [ ] Cada álbum muestra: nombre, fecha, conteo de fotos
- [ ] Thumbnail: primer foto del álbum
- [ ] Buscar álbumes por nombre (filtro en vivo)

### RF-2: Organización por Fecha

#### RF-2.1 Agrupar por Mes/Año

**Descripción:**
Los álbumes se agrupan automáticamente por mes/año en la interfaz, permitiendo visualizar la cronología.

**Criterios de Aceptación:**
- [ ] Álbumes agrupados en secciones colapsables
- [ ] Encabezado de sección: "Enero 2024"
- [ ] Contador de álbumes por mes
- [ ] Secciones se expanden/contraen al hacer click
- [ ] El mes actual está expandido por defecto

**Ejemplo:**
```
▼ Enero 2024 (3 álbumes)
  • Vacaciones
  • Cumpleaños Ana
  • Fotos de Nieve

▶ Diciembre 2023 (2 álbumes)
  ▶ Noviembre 2023 (1 álbum)
```

### RF-3: Galería de Fotos

#### RF-3.1 Ver Galería de Álbum

**Descripción:**
Al abrir un álbum, el usuario ve sus fotos en una galería de tiles.

**Criterios de Aceptación:**
- [ ] Fotos mostradas en grid de tiles
- [ ] Responsive: 1 columna en móvil, 2 en tablet, 3-4 en desktop
- [ ] Cada tile muestra thumbnail de foto
- [ ] Hover muestra nombre de la foto
- [ ] Click en tile abre vista de detalle (modal)
- [ ] Volver a lista de álbumes con botón "Atrás"

#### RF-3.2 Vista Detalle de Foto

**Criterios de Aceptación:**
- [ ] Modal con foto grande
- [ ] Nombre, tamaño, fecha de carga
- [ ] Navegación: flecha anterior/siguiente
- [ ] Botón: Descargar, Eliminar
- [ ] Botón: Cerrar modal

### RF-4: Drag & Drop

#### RF-4.1 Reorganizar Álbumes

**Descripción:**
Usuario puede arrastrar álbumes para reorganizarlos sin límites de estructura.

**Criterios de Aceptación:**
- [ ] Álbumes en lista son draggable
- [ ] Indicador visual durante drag
- [ ] Drop actualiza orden inmediatamente
- [ ] Orden persiste en almacenamiento
- [ ] Animación suave al completar

#### RF-4.2 Mover Fotos Entre Álbumes

**Descripción:**
Usuario puede arrastrar fotos de un álbum a otro.

**Criterios de Aceptación:**
- [ ] Fotos son draggable dentro de galería
- [ ] Drop en otro álbum mueve la foto
- [ ] Confirmación visual: "Foto movida a [Álbum]"
- [ ] Foto desaparece del álbum original
- [ ] Contador de fotos se actualiza

### RF-5: Búsqueda y Filtrado

#### RF-5.1 Buscar Álbumes

**Criterios de Aceptación:**
- [ ] Campo de búsqueda en header
- [ ] Filtro en vivo mientras escribe
- [ ] Busca por: nombre, descripción
- [ ] Resalta coincidencias
- [ ] Limpiar búsqueda con botón X

#### RF-5.2 Filtrar por Fecha

**Criterios de Aceptación:**
- [ ] Filtro de rango de fechas
- [ ] Muestra solo álbumes en rango
- [ ] Filtro persistente hasta cambiar

### RF-6: Cargar Fotos

#### RF-6.1 Subir Fotos a Álbum

**Descripción:**
Usuario puede subir imágenes a un álbum existente.

**Criterios de Aceptación:**
- [ ] Botón "Agregar Fotos" dentro del álbum
- [ ] Soporta drag & drop de archivos
- [ ] Soporta click para seleccionar archivos
- [ ] Formatos: JPG, PNG, WebP
- [ ] Máximo 50MB por foto
- [ ] Máximo 100 fotos por álbum
- [ ] Progress bar durante carga
- [ ] Mensajes de error si excede límites
- [ ] Fotos inmediatamente visibles en galería

### RF-7: Almacenamiento y Persistencia

#### RF-7.1 Guardar Localmente

**Criterios de Aceptación:**
- [ ] Datos se guardan en dispositivo (no en cloud)
- [ ] Álbumes persisten al cerrar navegador
- [ ] Fotos persisten (comprimidas)
- [ ] Metadatos guardados (fecha, nombre)
- [ ] No se pierde información al recargar

#### RF-7.2 Exportar Álbum

**Criterios de Aceptación:**
- [ ] Opción "Exportar" en álbum
- [ ] Descarga ZIP con fotos + metadatos
- [ ] Formato JSON para metadatos
- [ ] Compresión automática

---

## 🎨 Requisitos No-Funcionales

### RNF-1: Performance

- **Tiempo de carga**: < 2 segundos (página inicial)
- **Responsividad**: Acciones (crear, eliminar) < 500ms
- **Galería**: Scroll suave incluso con 100+ fotos
- **Drag & drop**: Sin lag notorio

### RNF-2: Accesibilidad

- **WCAG 2.1 AA**: Cumplimiento mínimo
- **Navegación teclado**: Completa funcionalidad
- **Screen readers**: Compatibilidad
- **Contraste**: 4.5:1 para texto

### RNF-3: Seguridad

- **Local storage**: Encriptación de datos sensibles
- **Input validation**: Todas las entradas validadas
- **XSS prevention**: Sanitización de inputs
- **CORS**: Si hay backend, configuración estricta

### RNF-4: Compatibilidad

- **Navegadores**: Chrome, Firefox, Safari, Edge (últimas 2 versiones)
- **Dispositivos**: Desktop, Tablet, Mobile
- **Resoluciones**: 320px a 4K

### RNF-5: Escalabilidad

- **Álbumes**: Mínimo 1000 sin degradación
- **Fotos por álbum**: Mínimo 100
- **Almacenamiento**: Máximo 5GB en dispositivo

---

## 📖 Historias de Usuario

### HU-1: Crear Primer Álbum

**Como** usuario nuevo  
**Quiero** crear mi primer álbum de fotos  
**Para que** pueda comenzar a organizar mis imágenes

**Criterios de Aceptación:**
- [ ] Botón evidente "Crear Álbum" en página vacía
- [ ] Form modal intuitivo
- [ ] Validación de campos clara
- [ ] Confirmación de éxito

**Flujo de Prueba:**
1. Abrir aplicación (vacía)
2. Click "Crear Álbum"
3. Rellenar: nombre="Mi Primer Álbum", fecha="2024-01-15"
4. Click "Guardar"
5. Álbum aparece en lista

---

### HU-2: Organizar Fotos en Álbumes

**Como** usuario  
**Quiero** arrastrar mis fotos entre álbumes  
**Para que** pueda reorganizar sin tener que eliminar y recrear

**Criterios de Aceptación:**
- [ ] Drag & drop funciona entre álbumes
- [ ] Feedback visual durante arrastre
- [ ] Foto desaparece del origen y aparece en destino
- [ ] Contador de fotos se actualiza

---

### HU-3: Encontrar Fotos Antiguamente

**Como** usuario con muchos álbumes  
**Quiero** buscar álbumes por nombre  
**Para que** no tenga que scrollear mucho

**Criterios de Aceptación:**
- [ ] Campo de búsqueda visible
- [ ] Resultados filtran en vivo
- [ ] Busca insensitiva a mayúsculas
- [ ] Botón limpiar búsqueda

---

### HU-4: Visualizar Galería Rápidamente

**Como** usuario  
**Quiero** que la galería cargue rápido incluso con muchas fotos  
**Para que** no pierda tiempo esperando

**Criterios de Aceptación:**
- [ ] Galería muestra primeras 12 fotos al instante
- [ ] Lazy loading de más fotos al scrollear
- [ ] Scroll suave sin lag

---

## ✅ Checklist de Aceptación Final

Antes de considerar completa la especificación:

- [ ] Todas las historias de usuario tienen criterios claros
- [ ] Requisitos no funcionales son medibles
- [ ] No hay conflictos entre requisitos
- [ ] Personas usuarias están bien definidas
- [ ] Scope está claro (qué SÍ, qué NO)
- [ ] Stakeholders han aprobado

---

## 🚫 Out of Scope (Fase Inicial)

- ❌ Sharing de álbumes con otros usuarios
- ❌ Edición de fotos (crop, filter)
- ❌ Sincronización en cloud
- ❌ Importación de redes sociales
- ❌ Reconocimiento facial
- ❌ Impresión de fotos

---

**Especificación Versión:** 1.0  
**Aprobada por:** Product Owner  
**Fecha:** 2025

**Siguiente Fase:** [plan.md](./plan.md) - Plan Técnico con Contex7
