# 🏗️ Plan Técnico - Photo Album App con Contex7

## Introducción: ¿Por Qué Contex7 en la Fase de Plan?

Después de especificar **QUÉ** construir (spec.md), necesitamos planificar **CÓMO** implementarlo. Aquí es donde **Contex7** se vuelve crucial.

### ¿Qué es Contex7?

**Contex7** es un framework de gestión de contexto técnico que:

1. **Mapea dependencias complejas** entre componentes
2. **Documenta decisiones arquitectónicas** (ADRs)
3. **Rastrea contexto a través de iteraciones** 
4. **Facilita comunicación en equipos distribuidos**
5. **Automatiza generación de documentación técnica**

### ¿Por Qué lo Necesitamos Ahora?

```
ESPECIFICACIÓN (spec.md)
"Crear álbumes, drag-drop, galería"
          ↓ ¿Cómo?
DECISIONES CRÍTICAS (Contex7)
• ¿Frontend: Vue o React?
• ¿Storage: IndexedDB o SQLite?
• ¿Arquitectura: Monolítica o modular?
• ¿Quién decide qué?
          ↓
PLAN TÉCNICO (plan.md)
Tech stack definido con justificación
```

### Beneficios de Contex7 en Esta Fase

| Beneficio | Impacto | Ejemplo |
|-----------|--------|---------|
| **Rastrabilidad** | Sabemos por qué elegimos Vue | Decisión enlazada a requisitos |
| **Comunicación** | Equipo entiende el contexto | ADR visible para todos |
| **Mantenibilidad** | Futuras decisiones respetan contexto | Cambio de tech stack = nuevo ADR |
| **Automatización** | Documentación se genera sola | Tasks se derivan automáticamente |
| **Colaboración** | Equipos remotos en sincronía | Contexto compartido y versionado |

---

## 📊 Arquitectura de Contex7

### Estructura de Contexto

```
Context Layer (Contex7)
├── Decisiones Arquitectónicas (ADRs)
│   ├── ADR-001: Frontend Framework
│   ├── ADR-002: Storage Layer
│   └── ADR-003: Component Architecture
├── Dependencias Técnicas
│   ├── External Dependencies (libs)
│   ├── Internal Dependencies (módulos)
│   └── Data Flow
└── Constrains & Govenance
    ├── Tech Stack Limits
    ├── Performance Budgets
    └── Security Policies
          ↓
Plan Técnico (plan.md)
"Aquí está cómo implementar"
```

### Ejemplo: ADR con Contex7

```markdown
# ADR-001: Frontend Framework

## Status
Aceptada (2025-01-15)

## Context
- App requiere UI responsiva (móvil, tablet, desktop)
- Drag & drop es requisito crítico
- Performance < 2.5s LCP
- Developer experience importante (equipo de 3)

## Decision
Usar **Vue 3 + Vite** para frontend

## Consequences

### Positivos
✅ Excelente DX (hot reload < 1ms)
✅ Bundle pequeño (~250KB gzip)
✅ Built-in drag & drop ready
✅ TypeScript first-class

### Negativos
❌ Comunidad más pequeña que React
❌ Menos librerías de terceros
❌ iOS WebView tiene bugs ocasionales

## Alternatives Considered
- React: Más librerías, pero bundle más grande
- Svelte: Excelente, pero curva de aprendizaje
- Angular: Overkill para esta app

## Related ADRs
- ADR-003: Component Architecture
- ADR-004: State Management (Pinia)

## Links
- [Vue 3 Docs](https://vuejs.org)
- [Vite Guide](https://vitejs.dev)
```

---

## 🎯 Decisiones Arquitectónicas (ADRs)

### ADR-001: Frontend Framework Selection

**Decision:** Vue 3 + TypeScript + Vite

**Why:**
- Reactividad declarativa perfecta para galería dinámica
- Excelente rendimiento con Composition API
- Small bundle size vs feature-rich
- DX superior para equipo pequeño

**Trade-offs:**
- Community size < React, pero suficiente
- Menos librerías third-party, pero lo básico está

---

### ADR-002: State Management

**Decision:** Pinia (Vue 3 default)

**Why:**
- Diseñado específicamente para Vue 3
- Autocompletar TypeScript completo
- Simpler API que Vuex
- Dev tools excelentes

**Stores:**
```
albumStore
  - albums: Album[]
  - selectedAlbum: Album | null
  - getters: albumsByMonth()
  - actions: createAlbum(), deleteAlbum()

photoStore
  - photos: Map<AlbumId, Photo[]>
  - actions: uploadPhoto(), movePhoto()

uiStore
  - searchQuery: string
  - dateFilter: DateRange
  - selectedPhoto: Photo | null
```

---

### ADR-003: Storage Layer

**Decision:** IndexedDB (Primary) + Fallback localStorage

**Why:**
- Large volume storage (>50MB)
- Asynchronous (no UI blocking)
- Indices for fast queries
- Better privacy than localStorage

**Schema:**
```javascript
// ObjectStores
albums: { keyPath: 'id', indices: ['createdDate', 'name'] }
photos: { keyPath: 'id', indices: ['albumId', 'uploadDate'] }
metadata: { keyPath: 'key' }

// Limits
- Max 50MB per origin (most browsers)
- Photo compression: JPG → 80% quality
- Index on createdDate para quick sorting
```

**Encryption:**
```typescript
// Sensitive data (future enhancement)
import TweetNaCl from 'tweetnacl';

async function encryptAlbum(album: Album) {
  const encrypted = TweetNaCl.secretbox(
    JSON.stringify(album),
    nonce,
    key
  );
  return await dbStore.save({ ...album, encrypted });
}
```

---

### ADR-004: Component Architecture

**Decision:** Component-Based with Composition API

**Component Structure:**
```
src/components/
├── Layout/
│   ├── Header.vue          (search, nav)
│   ├── Sidebar.vue         (filters)
│   └── Footer.vue          (info)
├── Albums/
│   ├── AlbumGrid.vue       (lista álbumes)
│   ├── AlbumCard.vue       (tarjeta individual)
│   ├── AlbumForm.vue       (crear/editar)
│   └── AlbumProvider.vue   (context provider)
├── Photos/
│   ├── PhotoGallery.vue    (grid de fotos)
│   ├── PhotoCard.vue       (tile individual)
│   ├── PhotoUpload.vue     (drag & drop upload)
│   ├── PhotoViewer.vue     (modal detalle)
│   └── DragDropManager.vue (orchestrate)
├── Common/
│   ├── Modal.vue
│   ├── Button.vue
│   ├── Input.vue
│   ├── Spinner.vue
│   └── Alert.vue

src/composables/
├── useAlbums.ts            (lógica álbumes)
├── usePhotos.ts            (lógica fotos)
├── useDragDrop.ts          (drag & drop)
├── useLocalStorage.ts      (persistencia)
└── useSearch.ts            (búsqueda)
```

---

### ADR-005: Drag & Drop Implementation

**Decision:** Usar HTML5 native + Vue composable

**Why:**
- No dependencies adicionales
- Nativo = mejor performance
- iOS/Android support con polyfills

**Implementation:**
```typescript
// composable
export const useDragDrop = () => {
  const draggedItem = ref<Album | null>(null);
  
  const handleDragStart = (album: Album) => {
    draggedItem.value = album;
    event.dataTransfer.effectAllowed = 'move';
  };
  
  const handleDrop = (targetAlbum: Album) => {
    if (draggedItem.value?.id !== targetAlbum.id) {
      reorderAlbums(draggedItem.value, targetAlbum);
    }
  };
  
  return { draggedItem, handleDragStart, handleDrop };
};
```

---

### ADR-006: Routing Strategy

**Decision:** Client-side routing (Vue Router)

**Why:**
- App es SPA (single-page)
- No requiere backend routes
- Faster navigation
- URL state para deep linking

**Routes:**
```
/                          → AlbumList
/album/:id                 → AlbumDetail
/album/:id/photo/:photoId  → PhotoViewer
/search?q=...             → Search Results
```

---

## 📦 Tech Stack Justificado

### Frontend Stack

```
Vue 3.4          → UI reactiva y performante
TypeScript 5.3   → Type safety, better DX
Vite 5.0         → Build tool ultrarrápido
Tailwind 3.3     → Utility CSS, fast
@heroicons/vue   → Icons
Pinia 2.1        → State management
```

**Bundle Target:** < 250KB gzip

### Storage Stack

```
IndexedDB        → Primary storage (50MB+)
localStorage     → Fallback small data
Compression      → Image optimization
```

### Development Stack

```
Vitest           → Unit testing
@vue/test-utils  → Component testing
Playwright       → E2E testing
ESLint           → Code linting
Prettier         → Code formatting
```

---

## 🔄 Data Flow Diagram

```
┌─────────────────┐
│    User Input   │
│  (Click, Upload)│
└────────┬────────┘
         │
         ▼
    ┌─────────────────────────┐
    │   Vue Component Layer   │
    │  (AlbumGrid, Gallery)   │
    └────────┬────────────────┘
             │
             ▼
    ┌─────────────────────────┐
    │  Pinia Store (State)    │
    │  (albumStore, photo)    │
    └────────┬────────────────┘
             │
             ▼
    ┌─────────────────────────┐
    │   Composables (Logic)   │
    │ (useAlbums, useDragDrop)│
    └────────┬────────────────┘
             │
             ▼
    ┌─────────────────────────┐
    │   Storage Service       │
    │   (IndexedDB API)       │
    └────────┬────────────────┘
             │
             ▼
    ┌─────────────────────────┐
    │    IndexedDB Storage    │
    │  (Persistent on Device) │
    └─────────────────────────┘
```

---

## 📈 Performance Budget

### Core Web Vitals

```
LCP (Largest Contentful Paint):  < 2.5s  ✓
FID (First Input Delay):         < 100ms ✓
CLS (Cumulative Layout Shift):   < 0.1   ✓
TTFB (Time to First Byte):       < 600ms ✓
```

### Bundle Breakdown

```
JavaScript:   ~200KB (gzip)
CSS:          ~50KB (gzip)
Fonts:        ~30KB (woff2)
─────────────────────────
Total:        ~280KB (gzip target: <250KB)
```

### Optimization Strategies

1. **Code Splitting**
   - Route lazy loading
   - Component async loading

2. **Tree Shaking**
   - Vite auto-optimiza unused code
   - Import { feature } from lib

3. **Asset Optimization**
   - Images: WebP + fallback
   - Fonts: Variable woff2
   - CSS: Tailwind purge

---

## 🔐 Security Architecture

### Input Validation

```typescript
// Validar uploads
const validatePhotoUpload = (file: File) => {
  const MAX_SIZE = 50 * 1024 * 1024; // 50MB
  const ALLOWED_TYPES = ['image/jpeg', 'image/png', 'image/webp'];
  
  if (file.size > MAX_SIZE) throw new Error('File too large');
  if (!ALLOWED_TYPES.includes(file.type)) throw new Error('Invalid type');
  
  return true;
};
```

### Local Storage Encryption (Future)

```typescript
import * as sodium from 'libsodium.js';

async function encryptStorage() {
  const key = sodium.crypto_secretbox_keygen();
  // Use for sensitive data encryption
}
```

### CSP Headers (if served from server)

```
Content-Security-Policy: 
  default-src 'self';
  script-src 'self' 'unsafe-inline';
  img-src 'self' data:;
  style-src 'self' 'unsafe-inline';
```

---

## 🧪 Testing Strategy

```
Unit Tests (75%)        → Logic, services, stores
├── albumService.spec.ts
├── photoService.spec.ts
└── composables/*.spec.ts

Integration Tests (20%) → Component + Store
├── AlbumGrid + albumStore
└── PhotoGallery + photoStore

E2E Tests (5%)          → Critical paths
├── Create album → Upload photos → View gallery
└── Drag & drop reorder
```

---

## 📋 Implementation Roadmap

### Phase 1: Foundation (Week 1-2)
- [ ] Project setup (Vite + Vue + TypeScript)
- [ ] Component scaffolding
- [ ] Pinia stores setup
- [ ] IndexedDB service

### Phase 2: Core Features (Week 3-4)
- [ ] Album CRUD (create, read, update, delete)
- [ ] Photo upload & storage
- [ ] Basic gallery view
- [ ] Search functionality

### Phase 3: UX Polish (Week 5)
- [ ] Drag & drop
- [ ] Animations
- [ ] Responsiveness
- [ ] Accessibility

### Phase 4: QA & Optimization (Week 6)
- [ ] Testing (unit, integration, E2E)
- [ ] Performance optimization
- [ ] Security audit
- [ ] Cross-browser testing

---

## 🚀 Deployment Strategy

### Development
```bash
npm run dev  # Hot reload en http://localhost:5173
```

### Production Build
```bash
npm run build    # Optimized bundle
npm run preview  # Test production build locally
```

### Hosting Options

1. **Static Hosting** (Recommended for local-first)
   - GitHub Pages
   - Vercel
   - Netlify

2. **Requirements**
   - HTTP/2 support
   - Gzip compression
   - Cache headers
   - HTTPS

---

## 📊 Contex7 Integration Points

**Contex7 rastrea:**

✅ **Decision Dependencies**
- ADR-001 (Vue) → ADR-004 (Composition API)
- ADR-002 (Pinia) → ADR-004 (Store integration)

✅ **Impact Analysis**
- Si cambiamos storage → qué componentes afecta?
- Si cambiamos framework → qué decisiones se invalidan?

✅ **Validation Rules**
- No usar librerías no-aprobadas
- Bundle debe mantenerse < 250KB
- Tests siempre antes de merge

✅ **Documentation Generation**
- Tasks derivan automáticamente de ADRs
- Documentación se mantiene sincronizada
- Cambios se rastrean por versión

---

## ✅ Verificación de Plan

Antes de pasar a tasks.md:

- [ ] ADRs justifican cada decisión arquitectónica
- [ ] Tech stack es coherente y sin conflictos
- [ ] Performance budget es realista
- [ ] Security strategy es sound
- [ ] Testing strategy es completa
- [ ] Roadmap es alcanzable
- [ ] Equipo entiende el contexto

---

**Plan Versión:** 1.0  
**Creado con:** Contex7 v2.1  
**Fecha:** 2025

**Siguiente:** [tasks.md](./tasks.md) - Tareas Ejecutables derivadas de este Plan
