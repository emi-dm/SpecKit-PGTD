# ✅ Tasks - Photo Album App

## Introducción

Este documento es el **desglose ejecutable** derivado del plan.md. Cada tarea tiene:
- Dependencias claras
- Archivos específicos
- Criterios de aceptación
- Tiempo estimado

### Convenciones

- `[P]` = Puede ejecutarse en paralelo
- `→` = Depende de
- ✓ = Completada

---

## Fase 1: Fundación (Semana 1-2)

### Task 1.1: Setup Proyecto Vite + Vue
- **Archivos:** `vite.config.ts`, `tsconfig.json`, `package.json`
- **Tiempo:** 30 min
- **Criterios:**
  - [ ] Proyecto inicia con `npm run dev`
  - [ ] Hot reload funciona
  - [ ] TypeScript strict mode activo
  - [ ] Eslint + Prettier configurados

---

### Task 1.2: Estructura de Carpetas Base
- **Archivos:** Crear directorios principales
  ```
  src/
  ├── components/
  ├── stores/
  ├── composables/
  ├── services/
  ├── types/
  ├── utils/
  └── assets/
  ```
- **Tiempo:** 15 min
- **Dependencia:** Task 1.1

---

### Task 1.3: Configurar Tailwind CSS
- **Archivos:** `tailwind.config.ts`, `src/index.css`
- **Tiempo:** 20 min
- **Criterios:**
  - [ ] Tailwind funciona en componentes
  - [ ] Colores custom definidos
  - [ ] Responsive breakpoints listos
- **Dependencia:** Task 1.1

---

### Task 1.4: [P] Configurar TypeScript Paths
- **Archivos:** `tsconfig.json`, `vite.config.ts`
- **Ejemplo:**
  ```typescript
  import { useAlbums } from '@/composables/useAlbums'
  // en lugar de '../../../composables/useAlbums'
  ```
- **Tiempo:** 15 min

---

### Task 1.5: [P] Setup Pinia Store
- **Archivos:** `src/stores/index.ts`, `src/main.ts`
- **Tiempo:** 30 min
- **Criterios:**
  - [ ] Pinia está registrado en main.ts
  - [ ] Store ejemplo funciona
  - [ ] DevTools habilitados
- **Dependencia:** Task 1.1

---

### Task 1.6: [P] Setup Vitest + @vue/test-utils
- **Archivos:** `vitest.config.ts`, `tests/setup.ts`
- **Tiempo:** 30 min
- **Criterios:**
  - [ ] `npm run test` funciona
  - [ ] Cobertura se reporta
  - [ ] Vue components son testables
- **Dependencia:** Task 1.1

---

### Task 1.7: Crear Tipos Base
- **Archivos:** `src/types/models.ts`
- **Contenido:**
  ```typescript
  export interface Album {
    id: string;
    name: string;
    createdDate: Date;
    description: string;
    photoCount: number;
  }
  
  export interface Photo {
    id: string;
    albumId: string;
    filename: string;
    uploadDate: Date;
    size: number;
    data: Blob;
  }
  ```
- **Tiempo:** 20 min
- **Dependencia:** Task 1.3

---

### Task 1.8: IndexedDB Service Setup
- **Archivos:** `src/services/storageService.ts`
- **Métodos:**
  ```typescript
  initDB(): Promise<IDBDatabase>
  createAlbum(album: Album): Promise<void>
  getAlbums(): Promise<Album[]>
  getAlbumById(id: string): Promise<Album>
  deleteAlbum(id: string): Promise<void>
  ```
- **Tiempo:** 1 hora
- **Criterios:**
  - [ ] ObjectStores creados correctamente
  - [ ] Queries funcionan
  - [ ] Error handling robusto
- **Dependencia:** Task 1.7

---

## Fase 2: Stores (Semana 1-2)

### Task 2.1: Crear albumStore con Pinia
- **Archivos:** `src/stores/albumStore.ts`
- **Métodos:**
  ```typescript
  state: { albums, selectedAlbum, loading }
  getters: { albumsByMonth(), searchResults() }
  actions: {
    fetchAlbums(),
    createAlbum(album),
    updateAlbum(album),
    deleteAlbum(id),
    selectAlbum(id)
  }
  ```
- **Tiempo:** 1 hora
- **Criterios:**
  - [ ] Estado actualiza correctamente
  - [ ] Getters derived reactivamente
  - [ ] Actions integradas con storageService
- **Dependencia:** Task 1.8

---

### Task 2.2: Crear photoStore con Pinia
- **Archivos:** `src/stores/photoStore.ts`
- **Métodos:**
  ```typescript
  state: { photos (Map<albumId, Photo[]>) }
  actions: {
    uploadPhoto(albumId, file),
    deletePhoto(albumId, photoId),
    movePhoto(photoId, targetAlbumId),
    getPhotosByAlbum(albumId)
  }
  ```
- **Tiempo:** 1 hora
- **Dependencia:** Task 2.1

---

### Task 2.3: [P] Crear uiStore
- **Archivos:** `src/stores/uiStore.ts`
- **Estado:**
  ```typescript
  searchQuery: string
  dateFilter: { start, end }
  selectedPhoto: Photo | null
  isModalOpen: boolean
  notifications: Notification[]
  ```
- **Tiempo:** 30 min
- **Dependencia:** Task 1.5

---

## Fase 3: Composables (Semana 1-2)

### Task 3.1: useAlbums Composable
- **Archivos:** `src/composables/useAlbums.ts`
- **Funciones:**
  ```typescript
  const albums = ref([])
  const { create, update, delete, fetch } = useAlbums()
  ```
- **Tiempo:** 45 min
- **Dependencia:** Task 2.1

---

### Task 3.2: usePhotos Composable
- **Archivos:** `src/composables/usePhotos.ts`
- **Funciones:**
  ```typescript
  const photos = ref([])
  const { upload, delete, move, getByAlbum } = usePhotos()
  ```
- **Tiempo:** 45 min
- **Dependencia:** Task 2.2

---

### Task 3.3: useDragDrop Composable
- **Archivos:** `src/composables/useDragDrop.ts`
- **Funciones:**
  ```typescript
  const { draggedItem, handleDragStart, handleDrop } = useDragDrop()
  ```
- **Tiempo:** 1 hora
- **Criterios:**
  - [ ] HTML5 drag events funciona
  - [ ] Visual feedback durante drag
- **Dependencia:** Task 3.2

---

### Task 3.4: [P] useSearch Composable
- **Archivos:** `src/composables/useSearch.ts`
- **Funciones:**
  ```typescript
  const results = useSearch(query, albums)
  ```
- **Tiempo:** 30 min

---

## Fase 4: Componentes Base (Semana 2-3)

### Task 4.1: Crear componentes Common
- **Archivos:** 
  ```
  src/components/Common/
  ├── Button.vue
  ├── Modal.vue
  ├── Input.vue
  ├── Select.vue
  ├── Spinner.vue
  └── Alert.vue
  ```
- **Tiempo:** 2 horas
- **Criterios:**
  - [ ] Todos accesibles
  - [ ] Tailwind styling
  - [ ] Props documentadas

---

### Task 4.2: Header Component
- **Archivos:** `src/components/Layout/Header.vue`
- **Features:**
  - [ ] Logo + título
  - [ ] Search bar
  - [ ] Navigation
- **Tiempo:** 1 hora
- **Dependencia:** Task 4.1

---

### Task 4.3: [P] Sidebar Component
- **Archivos:** `src/components/Layout/Sidebar.vue`
- **Features:**
  - [ ] Filtros de fecha
  - [ ] Categorías
  - [ ] Settings
- **Tiempo:** 1 hora
- **Dependencia:** Task 4.1

---

## Fase 5: Album Features (Semana 3)

### Task 5.1: AlbumCard Component
- **Archivos:** `src/components/Albums/AlbumCard.vue`
- **Props:** `{ album }`
- **Features:**
  - [ ] Thumbnail con primer foto
  - [ ] Nombre, conteo de fotos
  - [ ] Hover effects
- **Tiempo:** 45 min
- **Dependencia:** Task 4.1

---

### Task 5.2: AlbumGrid Component
- **Archivos:** `src/components/Albums/AlbumGrid.vue`
- **Features:**
  - [ ] Grid responsive
  - [ ] Ordena por fecha
  - [ ] Agrupa por mes
- **Tiempo:** 1 hora
- **Dependencia:** Task 5.1 → Task 3.1

---

### Task 5.3: AlbumForm Component
- **Archivos:** `src/components/Albums/AlbumForm.vue`
- **Features:**
  - [ ] Crear nuevo álbum
  - [ ] Editar álbum existente
  - [ ] Validación de campos
- **Tiempo:** 1.5 horas
- **Criterios:**
  - [ ] Nombre requerido, max 100 chars
  - [ ] Fecha por defecto hoy
  - [ ] Form modal dentro de Modal
- **Dependencia:** Task 4.1

---

### Task 5.4: Album CRUD Tests
- **Archivos:** `tests/unit/album.spec.ts`
- **Coverage:** 80%+
- **Tiempo:** 1 hora
- **Dependencia:** Task 1.6

---

## Fase 6: Photo Features (Semana 3-4)

### Task 6.1: PhotoCard Component
- **Archivos:** `src/components/Photos/PhotoCard.vue`
- **Features:**
  - [ ] Thumbnail responsive
  - [ ] Overlay con hover
  - [ ] Draggable
- **Tiempo:** 45 min
- **Dependencia:** Task 4.1

---

### Task 6.2: PhotoGallery Component
- **Archivos:** `src/components/Photos/PhotoGallery.vue`
- **Features:**
  - [ ] Grid de fotos 3-4 columnas
  - [ ] Lazy loading al scroll
  - [ ] Empty state
- **Tiempo:** 1.5 horas
- **Criterios:**
  - [ ] Scroll suave sin lag
  - [ ] Primeras 12 fotos cargan rápido
- **Dependencia:** Task 6.1 → Task 3.2

---

### Task 6.3: PhotoUpload Component
- **Archivos:** `src/components/Photos/PhotoUpload.vue`
- **Features:**
  - [ ] Drag & drop upload
  - [ ] Click to select files
  - [ ] Progress bar
  - [ ] Validación
- **Tiempo:** 1.5 horas
- **Criterios:**
  - [ ] Max 50MB por foto
  - [ ] Max 100 fotos por álbum
  - [ ] Formatos: JPG, PNG, WebP
- **Dependencia:** Task 3.2 → Task 4.1

---

### Task 6.4: PhotoViewer Modal
- **Archivos:** `src/components/Photos/PhotoViewer.vue`
- **Features:**
  - [ ] Foto grande
  - [ ] Metadatos
  - [ ] Navegación anterior/siguiente
  - [ ] Descargar, Eliminar
- **Tiempo:** 1 hora
- **Dependencia:** Task 6.1

---

## Fase 7: Integración y Drag & Drop (Semana 4)

### Task 7.1: Drag & Drop Albums
- **Archivos:** Actualizar `AlbumGrid.vue`
- **Features:**
  - [ ] Drag álbumes
  - [ ] Visual feedback
  - [ ] Reorder persistente
- **Tiempo:** 1 hora
- **Dependencia:** Task 3.3 → Task 5.2

---

### Task 7.2: Move Photos Between Albums
- **Archivos:** Actualizar `PhotoGallery.vue`, `PhotoCard.vue`
- **Features:**
  - [ ] Drag foto de un álbum a otro
  - [ ] Confirmación visual
  - [ ] Contador actualiza
- **Tiempo:** 1.5 horas
- **Dependencia:** Task 3.3 → Task 6.2

---

### Task 7.3: Search Integration
- **Archivos:** Actualizar `Header.vue`, `AlbumGrid.vue`
- **Features:**
  - [ ] Buscar por nombre
  - [ ] Filtro en vivo
  - [ ] Limpiar búsqueda
- **Tiempo:** 1 hora
- **Dependencia:** Task 3.4 → Task 5.2

---

## Fase 8: UX Polish (Semana 4-5)

### Task 8.1: Animaciones y Transiciones
- **Archivos:** `src/utils/animations.ts`, componentes
- **Features:**
  - [ ] Page transitions suaves
  - [ ] Modal entrada/salida
  - [ ] Skeleton loaders
- **Tiempo:** 1.5 horas
- **Dependencia:** Task 4.1

---

### Task 8.2: Accesibilidad WCAG 2.1
- **Archivos:** Review todos los componentes
- **Checklist:**
  - [ ] Keyboard navigation completa
  - [ ] Labels en inputs
  - [ ] ARIA labels donde sea necesario
  - [ ] Contraste WCAG AA
- **Tiempo:** 2 horas
- **Dependencia:** Todas las fases previas

---

### Task 8.3: Responsiveness Testing
- **Dispositivos:**
  - [ ] Mobile (320px)
  - [ ] Tablet (768px)
  - [ ] Desktop (1024px)
  - [ ] Large (1920px)
- **Tiempo:** 1.5 horas

---

## Fase 9: Testing (Semana 5)

### Task 9.1: Unit Tests - Stores
- **Archivos:** `tests/unit/stores/`
- **Target:** 80%+ coverage
- **Tiempo:** 2 horas
- **Dependencia:** Task 2.1, 2.2, 2.3

---

### Task 9.2: Unit Tests - Composables
- **Archivos:** `tests/unit/composables/`
- **Tiempo:** 1.5 horas
- **Dependencia:** Task 3.1-4

---

### Task 9.3: Integration Tests
- **Archivos:** `tests/integration/`
- **Scenarios:**
  - [ ] Create album → upload photo → view gallery
  - [ ] Search album
  - [ ] Drag & drop reorder
- **Tiempo:** 2 horas

---

### Task 9.4: E2E Tests (Playwright)
- **Archivos:** `tests/e2e/`
- **Críticas paths:**
  - [ ] Full user journey
  - [ ] Drag & drop
  - [ ] Export
- **Tiempo:** 2 horas

---

## Fase 10: Optimización (Semana 5-6)

### Task 10.1: Performance Optimization
- **Checklist:**
  - [ ] LCP < 2.5s
  - [ ] Bundle < 250KB gzip
  - [ ] Lazy load components
  - [ ] Tree-shake unused code
- **Tiempo:** 2 horas

---

### Task 10.2: Image Optimization
- **Features:**
  - [ ] WebP conversion
  - [ ] Compression
  - [ ] Lazy loading
- **Tiempo:** 1 hora

---

### Task 10.3: Security Audit
- **Checklist:**
  - [ ] Input validation
  - [ ] XSS prevention
  - [ ] No console.logs en prod
  - [ ] CSP headers (si aplicable)
- **Tiempo:** 1.5 horas

---

## 📊 Resumen de Tasks

```
Total Tasks: 35
Estimado: 60 horas
En Paralelo ([P]): 8 tasks

Distribución por Fase:
Phase 1 (Fundación):     8 tasks  (~5 horas)
Phase 2 (Stores):        3 tasks  (~3.5 horas)
Phase 3 (Composables):   4 tasks  (~3.5 horas)
Phase 4 (Componentes):   3 tasks  (~4 horas)
Phase 5 (Albums):        4 tasks  (~5 horas)
Phase 6 (Photos):        4 tasks  (~6 horas)
Phase 7 (Integración):   3 tasks  (~3.5 horas)
Phase 8 (Polish):        3 tasks  (~5 horas)
Phase 9 (Testing):       4 tasks  (~7.5 horas)
Phase 10 (Optimización): 3 tasks  (~4.5 horas)
```

---

## ✅ Orden de Ejecución Recomendado

1. **Day 1:** Tasks 1.1, 1.2, 1.3, 1.4, 1.5, 1.6 (setup)
2. **Day 1-2:** Tasks 1.7, 1.8, 2.1, 2.2, 2.3 (stores)
3. **Day 2-3:** Tasks 3.1-3.4 (composables)
4. **Day 3:** Tasks 4.1, 4.2, 4.3 (componentes base)
5. **Day 4:** Tasks 5.1-5.3 (albums)
6. **Day 5-6:** Tasks 6.1-6.4 (photos)
7. **Day 6:** Tasks 7.1-7.3 (integración)
8. **Day 7:** Tasks 8.1-8.3 (polish)
9. **Day 8:** Tasks 9.1-9.4 (testing)
10. **Day 8-9:** Tasks 10.1-10.3 (optimization)

---

**Tasks Versión:** 1.0  
**Derivado de:** plan.md  
**Fecha:** 2025

**Siguiente:** Ejecutar con `/speckit.implement` en tu agente IA
