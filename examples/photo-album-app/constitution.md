# 📋 Constitution - Photo Album App

## Principios Fundacionales del Proyecto

Este documento establece los principios, estándares y directrices que guían todas las decisiones técnicas y de desarrollo en Photo Album App.

---

## 1. 🎯 Calidad de Código

### Estándares Generales

- **Legibilidad**: Código autodocumentado, nombres descriptivos
- **Complejidad**: Máximo 10 líneas de lógica por función
- **Modularidad**: Cada componente tiene una responsabilidad única
- **Type Safety**: TypeScript strict mode en 100% del código
- **Linting**: ESLint + Prettier configurados y obligatorios

### Convenciones

```typescript
// Componentes Vue
// Archivos: PascalCase (AlbumGrid.vue)
// Props: camelCase
// Events: kebab-case (album-created)

// Stores Pinia
// Archivos: camelCase (albumStore.ts)
// Acciones: verbs (getAlbum, updateAlbum)

// Services
// Archivos: camelCase (storageService.ts)
// Métodos: verbs (saveAlbum, deleteAlbum)

// Constants
// Formato: UPPER_SNAKE_CASE
// Ubicación: constants.ts en cada módulo
```

### Código Review Checklist

- [ ] Código pasa TypeScript strict
- [ ] No hay `any` types
- [ ] Funciones tienen máximo 10 líneas
- [ ] Nombres son descriptivos
- [ ] No hay console.log en producción
- [ ] Sigue convenciones del proyecto

---

## 2. ✅ Estándares de Pruebas

### Cobertura Requerida

| Tipo | Cobertura | Categoría |
|------|-----------|----------|
| **Statements** | 80% | Obligatorio |
| **Branches** | 75% | Obligatorio |
| **Functions** | 80% | Obligatorio |
| **Lines** | 80% | Obligatorio |

### Pirámide de Testing

```
        /\
       /E2E\         5% - Flujos end-to-end críticos
      /    \
     /------\
    / Integr.\       20% - Integración entre servicios
   /  Tests \
  /__________\
 /           \
/  Unit Tests \   75% - Lógica unitaria
/___________  \
```

### Tipos de Pruebas

**Unit Tests**
- Servicios de almacenamiento
- Transformación de datos
- Validación de entrada
- Tool: Vitest

**Integration Tests**
- Interacción componentes + stores
- API calls + procesamiento
- Storage + retrieval

**E2E Tests**
- Flujo de usuario completo
- Crear álbum → subir fotos → galería
- Drag & drop en acción
- Tool: Playwright o Cypress

### Ejemplos de Pruebas

```typescript
// ✅ Unit Test
describe('albumService', () => {
  it('debe crear un álbum con metadatos', () => {
    const album = createAlbum('Vacaciones 2024', '2024-01-15');
    expect(album.name).toBe('Vacaciones 2024');
    expect(album.createdDate).toEqual('2024-01-15');
  });
});

// ✅ Integration Test
describe('AlbumStore + StorageService', () => {
  it('debe guardar álbum en IndexedDB al actualizar', async () => {
    const store = useAlbumStore();
    await store.addAlbum(newAlbum);
    const saved = await storageService.getAlbum(newAlbum.id);
    expect(saved).toEqual(newAlbum);
  });
});
```

---

## 3. 🎨 Consistencia UX/UI

### Principios de Diseño

1. **Simplicidad**: Interfaz limpia y sin distracciones
2. **Intuitividad**: Los usuarios entienden sin tutorial
3. **Consistencia**: Patrones repetidos en toda la app
4. **Accesibilidad**: WCAG 2.1 AA mínimo
5. **Feedback**: Usuarios saben qué está pasando

### Paleta de Colores

```
Primary:   #3B82F6   (Blue - Acciones principales)
Secondary: #10B981   (Green - Éxito)
Danger:    #EF4444   (Red - Destructivo)
Warning:   #F59E0B   (Amber - Atención)
Neutral:   #6B7280   (Gray - Texto secundario)
```

### Tipografía

```
Font: Inter (Google Fonts)
H1: 32px, bold (títulos principales)
H2: 24px, semibold (subtítulos)
Body: 16px, regular (texto normal)
Caption: 12px, regular (metadatos)
```

### Componentes Reusables

```
✅ Button (primary, secondary, danger, loading)
✅ Card (contenedor)
✅ Modal (diálogos)
✅ Input (texto, fecha, archivo)
✅ Spinner (carga)
✅ Alert (mensajes)
✅ Badge (etiquetas)
```

### Responsive Design

```
Mobile:  320px - 767px   (1 columna)
Tablet:  768px - 1023px  (2 columnas)
Desktop: 1024px+         (3-4 columnas)

Breakpoints en Tailwind:
sm: 640px
md: 768px
lg: 1024px
xl: 1280px
```

### Accesibilidad

- [ ] Todos los inputs tienen labels
- [ ] Colores no son única forma de diferenciación
- [ ] Keyboard navigation funciona
- [ ] ARIA labels donde sea necesario
- [ ] Contraste mínimo WCAG AA
- [ ] Alt text en todas las imágenes

---

## 4. 🚀 Requisitos de Performance

### Métricas Core Web Vitals

| Métrica | Target | Descripción |
|---------|--------|-------------|
| **LCP** | < 2.5s | Largest Contentful Paint |
| **FID** | < 100ms | First Input Delay |
| **CLS** | < 0.1 | Cumulative Layout Shift |

### Presupuesto de Recursos

```
Total Bundle:      < 500KB (gzip)
JavaScript:        < 250KB (gzip)
CSS:               < 100KB (gzip)
Imágenes:          < 150KB por página
Fonts:             < 100KB (woff2)
```

### Optimization Strategy

**Code Splitting**
```typescript
// ✅ Lazy load rutas no críticas
const AdminPanel = lazy(() => import('./AdminPanel.vue'));

// ✅ Async components
import { defineAsyncComponent } from 'vue';
const PhotoGallery = defineAsyncComponent(
  () => import('./PhotoGallery.vue')
);
```

**Asset Optimization**
```javascript
// ✅ Imágenes: WebP + fallback
// ✅ Fonts: WOFF2 variable fonts
// ✅ CSS: Purge unused con Tailwind
// ✅ JS: Tree-shake con Vite
```

**Caching Strategy**
```
Estático:   Cache-Control: max-age=31536000
Dinámico:   Cache-Control: max-age=3600
API:        Validar con ETag
```

---

## 5. 🔐 Seguridad y Privacidad

### Principios

1. **Local-First**: Datos nunca salen del dispositivo del usuario
2. **Encryption**: Datos sensibles encriptados en storage
3. **No Tracking**: Sin analytics que invadan privacidad
4. **Input Validation**: Validar todas las entradas
5. **CSP Headers**: Content Security Policy estricta

### Implementación

**Local Storage**
```javascript
// ✅ Álbumes en IndexedDB (no en localStorage)
// ✅ Encriptar antes de guardar
// ✅ Never store passwords o tokens
```

**Input Validation**
```typescript
// ✅ Validar nombre de álbum
// ✅ Validar tipos de foto (jpg, png, webp)
// ✅ Validar tamaño (max 50MB por foto)
// ✅ Sanitizar URLs
```

**Content Security Policy**
```
default-src 'self'
script-src 'self' 'unsafe-inline'
img-src 'self' data:
style-src 'self' 'unsafe-inline'
```

---

## 6. 🔄 Gobernanza Técnica

### Decisiones Arquitectónicas

**Por qué Vue 3 + TypeScript**
- Type safety sin overhead
- Reactividad declarativa
- Excelente DX
- Comunidad activa

**Por qué SQLite Local**
- No requiere backend
- Datos permanecen en dispositivo
- Estándar en la industria
- IndexedDB para acceso en navegador

**Por qué Vite**
- Hot reload ultrarápido
- Bundle optimizado
- Configuración mínima
- Excelente DX

### Cambios Arquitectónicos

Cualquier cambio importante requiere:
1. Documento ADR (Architecture Decision Record)
2. Discussion en equipo
3. Impact analysis
4. Aprobación del tech lead

### Versionado

```
MAJOR: Breaking changes
MINOR: Nuevas características
PATCH: Bug fixes

Ejemplo: 1.2.3
```

---

## 7. 📦 Dependencias Externas

### Aprobadas

```json
{
  "core": {
    "vue": "^3.4",
    "typescript": "^5.3",
    "vite": "^5.0"
  },
  "ui": {
    "tailwindcss": "^3.3",
    "@heroicons/vue": "^2.0"
  },
  "state": {
    "pinia": "^2.1"
  },
  "testing": {
    "vitest": "^1.0",
    "@vue/test-utils": "^2.4"
  },
  "utils": {
    "date-fns": "^2.30",
    "uuid": "^9.0"
  }
}
```

### Política de Actualizaciones

- **Security patches**: ASAP
- **Minor updates**: Mensual
- **Major updates**: Trimestral con testing completo
- **Nuevas librerías**: Requieren aprobación

---

## 8. 📚 Documentación

Requerimientos:
- [ ] Código comentado para lógica compleja
- [ ] Funciones tienen JSDoc
- [ ] README.md actualizado
- [ ] CONTRIBUTING.md para contribuidores
- [ ] ADR para decisiones importantes

### JSDoc Ejemplo

```typescript
/**
 * Crea un nuevo álbum de fotos
 * @param name - Nombre del álbum
 * @param date - Fecha de creación (YYYY-MM-DD)
 * @returns Album creado con ID único
 * @throws Error si el nombre está vacío
 * @example
 * const album = createAlbum('Vacaciones', '2024-01-15');
 */
function createAlbum(name: string, date: string): Album {
  // ...
}
```

---

## 9. 🎯 Revisión de Conformidad

Antes de cada release:

- [ ] Code review completado
- [ ] Tests pasan (80% cobertura)
- [ ] Performance OK (Core Web Vitals)
- [ ] Accesibilidad verificada
- [ ] Documentación actualizada
- [ ] Security audit completado
- [ ] Release notes preparadas

---

## 10. 📞 Escalación

**Dudas sobre constitución?**
1. Pregunta en equipo
2. Abre discussion
3. Propone enmienda si es necesario

**Cambios importantes?**
1. Crea ADR
2. Discute con team
3. Aprobación requerida

---

**Documento válido desde:** v1.0.0  
**Última actualización:** 2025  
**Próxima revisión:** 2025-Q2

Este documento vincula todas las decisiones de desarrollo. Ante conflictos, esta constitución es la autoridad.
