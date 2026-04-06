# TASKS — Modern Studio

**Leyenda:** P0 = Blocker | P1 = Alta | P2 = Media | P3 = Baja
**Estado:** [ ] Pendiente | [>] En progreso | [x] Completado

---

## FASE 0: Fundación _(~19h)_

### TAREA-001 — Migración a Astro
- **Prioridad:** P0 | **Estimación:** 8h | **Estado:** [ ]
- Inicializar proyecto Astro. Migrar HTML del prototipo como `Layout.astro`. Extraer CSS a archivo global. Configurar estructura `/src/pages`, `/src/components`, `/src/layouts`, `/src/data`.
- **Criterios de aceptación:**
  - `npm run dev` levanta el sitio idéntico al prototipo
  - Sin regresiones visuales en desktop
- **Dependencias:** Ninguna

---

### TAREA-002 — Design Tokens y Variables Globales
- **Prioridad:** P0 | **Estimación:** 3h | **Estado:** [ ]
- Extraer custom properties CSS a `tokens.css` centralizado. Agregar tokens de breakpoints, espaciados, sombras y border-radius.
- **Criterios de aceptación:**
  - Un único punto de verdad para colores, tipografía y espaciado
  - Cambiar `--gold` en un lugar impacta todo el sitio
- **Dependencias:** TAREA-001

---

### TAREA-003 — Esquema de Datos de Productos
- **Prioridad:** P0 | **Estimación:** 4h | **Estado:** [ ]
- Definir interfaz TypeScript `Product`. Crear `products.json` con mínimo 20 productos en 6 categorías. Campos: id, slug, name, brand, price, category, images[], description, dimensions, variants[], inStock, isNew, isFeatured.
- **Criterios de aceptación:**
  - JSON válido contra el tipo TypeScript definido
  - Al menos 4 productos por categoría principal
- **Dependencias:** TAREA-001

---

### TAREA-004 — Setup de Componentes Base
- **Prioridad:** P0 | **Estimación:** 4h | **Estado:** [ ]
- Crear `Header.astro`, `Footer.astro`, `AnnouncementBar.astro`, `Button.astro`. El `Layout.astro` los consume.
- **Criterios de aceptación:**
  - Cada componente tiene scope de estilos propio
  - HTML generado idéntico al prototipo
  - Sin duplicación de markup
- **Dependencias:** TAREA-001, TAREA-002

---

## FASE 1: Responsividad _(~22h)_

### TAREA-005 — Responsive Header y Nav Mobile
- **Prioridad:** P0 | **Estimación:** 10h | **Estado:** [ ]
- Bajo 768px: logo centrado, hamburger a la izquierda, carrito/cuenta a la derecha. Drawer lateral con menú en acordeón.
- **Criterios de aceptación:**
  - Drawer abre/cierra con animación 300ms
  - Focus trap activo dentro del drawer
  - Cerrar con Escape o clic fuera
- **Dependencias:** TAREA-004

---

### TAREA-006 — Responsive Hero
- **Prioridad:** P1 | **Estimación:** 4h | **Estado:** [ ]
- En mobile: banner inferior en columna, padding lateral 20px, texto reducido. `min-height: 100svh`.
- **Criterios de aceptación:**
  - Sin overflow horizontal en 320px
  - Botón "COMPRAR AHORA" con tap target mínimo 44px
- **Dependencias:** TAREA-004

---

### TAREA-007 — Responsive Grids (Colecciones y Productos)
- **Prioridad:** P1 | **Estimación:** 5h | **Estado:** [ ]
- Colecciones: 2×2 en tablet+, 1×4 en mobile. Productos: 4 cols desktop, 2 cols tablet, 1 col mobile.
- **Criterios de aceptación:**
  - Media queries en breakpoints 480px, 768px, 1024px
  - Imágenes con `aspect-ratio` y `object-fit: cover`
- **Dependencias:** TAREA-004

---

### TAREA-008 — Responsive Footer
- **Prioridad:** P1 | **Estimación:** 3h | **Estado:** [ ]
- 4 columnas → 2 cols tablet → 1 col mobile. `.footer-bottom` apila verticalmente en mobile.
- **Criterios de aceptación:**
  - Sin texto cortado en ningún breakpoint
  - Links totalmente tocables en mobile
- **Dependencias:** TAREA-004

---

## FASE 2: Páginas Internas _(~60h)_

### TAREA-009 — Página de Listado de Productos (PLP)
- **Prioridad:** P0 | **Estimación:** 14h | **Estado:** [ ]
- `/coleccion/[categoria].astro`. Grid de product cards con filtros (precio, marca, material) y ordenamiento. URL refleja filtros activos.
- **Criterios de aceptación:**
  - Las 6 rutas de categoría funcionan
  - Filtros reducen listado en tiempo real (client-side)
  - URL compartible con filtros activos
  - Responsive con filtros en drawer en mobile
- **Dependencias:** TAREA-003, TAREA-004

---

### TAREA-010 — Página de Detalle de Producto (PDP)
- **Prioridad:** P0 | **Estimación:** 16h | **Estado:** [ ]
- `/producto/[slug].astro`. Galería izquierda + info derecha: marca, nombre, precio, variantes, descripción, dimensiones, tiempo de entrega, botón agregar al carrito. Sección de productos relacionados. Breadcrumb.
- **Criterios de aceptación:**
  - Galería con swipe en mobile y click en desktop
  - Botón carrito actualiza contador del header inmediatamente
  - Schema.org `Product` en el `<head>`
- **Dependencias:** TAREA-003, TAREA-004, TAREA-011

---

### TAREA-011 — Carrito (Drawer + Estado)
- **Prioridad:** P0 | **Estimación:** 12h | **Estado:** [ ]
- Isla de React (`CartDrawer.tsx`). Estado global con Nanostores. Drawer con imagen, nombre, variante, cantidad, precio, subtotal. Total al pie con botón checkout. Persistencia en `localStorage`.
- **Criterios de aceptación:**
  - Estado persiste al recargar
  - Agregar mismo producto aumenta quantity (no duplica fila)
  - Drawer accesible por teclado con focus trap
  - Sin layout shift en header al cargar el contador
- **Dependencias:** TAREA-004

---

### TAREA-012 — Búsqueda con Modal
- **Prioridad:** P1 | **Estimación:** 8h | **Estado:** [ ]
- Modal full-width oscuro al clic en lupa. Búsqueda client-side con Fuse.js (nombre, marca, categoría). Resultados con imagen + nombre + precio. Debounce 300ms.
- **Criterios de aceptación:**
  - Modal abre/cierra con Escape y clic fuera
  - Focus automático en input al abrir
  - Mínimo 3 caracteres para buscar
  - Mensaje "Sin resultados" cuando no hay coincidencias
- **Dependencias:** TAREA-003, TAREA-011

---

### TAREA-013 — Checkout Básico
- **Prioridad:** P1 | **Estimación:** 10h | **Estado:** [ ]
- Página `/checkout`. Formulario de contacto y envío. Integración con Stripe Checkout Session (serverless function). Redirección a `/pedido-confirmado/[id]` al completar pago.
- **Criterios de aceptación:**
  - Validación inline de formulario
  - Botón pagar deshabilitado hasta formulario válido
  - Stripe Session usa items reales del carrito
  - Carrito se limpia tras pago exitoso
- **Dependencias:** TAREA-011

---

## FASE 3: SEO, Performance y Accesibilidad _(~23h)_

### TAREA-014 — SEO Técnico
- **Prioridad:** P1 | **Estimación:** 6h | **Estado:** [ ]
- Componente `SEOHead.astro`. Schema.org `Product` en PDP, `BreadcrumbList` en PLP/PDP, `Organization` en Layout. Sitemap dinámico. `robots.txt`.
- **Criterios de aceptación:**
  - Google Rich Results Test sin errores
  - Sitemap accesible en `/sitemap.xml`
  - Cada página con title < 60 chars y description < 160 chars
- **Dependencias:** TAREA-009, TAREA-010

---

### TAREA-015 — Performance de Imágenes
- **Prioridad:** P1 | **Estimación:** 5h | **Estado:** [ ]
- Componente `<Image>` de Astro con dimensiones explícitas. `loading="lazy"` salvo hero (`fetchpriority="high"`). Generar WebP/AVIF. `width` y `height` explícitos en todas las imágenes.
- **Criterios de aceptación:**
  - LCP < 2.5s en 4G simulado (Lighthouse)
  - CLS < 0.1 en todas las páginas
  - Lighthouse Performance > 90 en mobile
- **Dependencias:** TAREA-009, TAREA-010

---

### TAREA-016 — Accesibilidad (WCAG 2.1 AA)
- **Prioridad:** P1 | **Estimación:** 8h | **Estado:** [ ]
- Auditar con axe-core y corregir: contraste nav sobre hero, `aria-label` en botones, dropdown accesible por teclado, `role="dialog"` en drawers, focus traps, alt text descriptivo.
- **Criterios de aceptación:**
  - 0 errores críticos en axe-core en todas las páginas
  - Navegación completa con solo teclado
  - Contraste mínimo 4.5:1 en todo el texto
  - Lighthouse Accessibility > 95
- **Dependencias:** TAREA-005, TAREA-011, TAREA-012

---

### TAREA-017 — Analytics y Tracking de Eventos
- **Prioridad:** P2 | **Estimación:** 4h | **Estado:** [ ]
- Integrar Plausible Analytics (o GA4). Eventos clave: `add_to_cart`, `begin_checkout`, `purchase`, `search`, `collection_click`.
- **Criterios de aceptación:**
  - Dashboard muestra pageviews en tiempo real
  - Los 5 eventos aparecen correctamente
  - Script no bloquea el render (async)
- **Dependencias:** TAREA-013

---

## FASE 4: Features de Conversión _(~40h)_

### TAREA-018 — Wishlist / Lista de Deseos
- **Prioridad:** P2 | **Estimación:** 6h | **Estado:** [ ]
- Ícono corazón en product cards y PDP. Persistencia en localStorage. Página `/wishlist` con opción de mover al carrito o eliminar.
- **Criterios de aceptación:**
  - Corazón togglea visualmente (vacío/relleno)
  - Persistencia tras reload
  - Página de wishlist funcional
- **Dependencias:** TAREA-010, TAREA-011

---

### TAREA-019 — Cuenta de Usuario
- **Prioridad:** P2 | **Estimación:** 16h | **Estado:** [ ]
- Registro + login con email/contraseña + OAuth Google (Auth.js). DB en Supabase o PlanetScale. Historial de pedidos. Wishlist sincronizada. Dirección guardada.
- **Criterios de aceptación:**
  - Login con Google en < 3 clics
  - Historial muestra pedidos de Stripe vinculados al email
  - Password recovery funcional vía email
- **Dependencias:** TAREA-013, TAREA-018

---

### TAREA-020 — Cuenta Profesional
- **Prioridad:** P2 | **Estimación:** 8h | **Estado:** [ ]
- Formulario de aplicación (nombre, empresa, NIF, web, tipo proyecto). Revisión manual con notificación por email. Al aprobarse: 15% descuento automático en checkout. Badge "Precio Profesional" en PDP.
- **Criterios de aceptación:**
  - Formulario envía email al admin (SendGrid o Resend)
  - Descuento aplicado correctamente en Stripe Session
  - Usuarios pro ven precio con y sin descuento
- **Dependencias:** TAREA-013, TAREA-019

---

### TAREA-021 — Reseñas y Calificaciones
- **Prioridad:** P3 | **Estimación:** 10h | **Estado:** [ ]
- Sistema de reseñas para compradores verificados. 1–5 estrellas + texto. Moderación antes de publicar. Rating promedio en PDP y PLP.
- **Criterios de aceptación:**
  - Formulario visible solo para compradores del producto
  - Schema.org `AggregateRating` en PDP
- **Dependencias:** TAREA-019

---

## FASE 5: Content y CMS _(~30h)_

### TAREA-022 — Integración CMS Headless
- **Prioridad:** P2 | **Estimación:** 20h | **Estado:** [ ]
- Migrar `products.json` a Sanity.io o Directus. Schemas para Producto, Colección, Marca, Blog. Webhooks disparan redeploy en Vercel al publicar.
- **Criterios de aceptación:**
  - Producto nuevo en Sanity aparece en el sitio en < 2 min
  - Imágenes servidas desde CDN del CMS
  - Schema cubre todos los campos del tipo `Product`
- **Dependencias:** TAREA-003, TAREA-009, TAREA-010

---

### TAREA-023 — Blog de Diseño
- **Prioridad:** P3 | **Estimación:** 10h | **Estado:** [ ]
- Sección `/blog` con listado paginado y páginas `/blog/[slug]`. Categorías: Tendencias, Inspiración, Guías. Links internos a productos. Schema.org `Article`.
- **Criterios de aceptación:**
  - Listado paginado (6 artículos/página)
  - Mínimo 3 artículos de ejemplo al lanzar
- **Dependencias:** TAREA-022

---

## Resumen

| Fase | Tareas | Horas |
|------|--------|-------|
| Fase 0: Fundación | 001–004 | ~19h |
| Fase 1: Responsividad | 005–008 | ~22h |
| Fase 2: Páginas Internas | 009–013 | ~60h |
| Fase 3: SEO / Performance / A11y | 014–017 | ~23h |
| Fase 4: Conversión | 018–021 | ~40h |
| Fase 5: Content / CMS | 022–023 | ~30h |
| **Total** | **23 tareas** | **~194h** |

**MVP funcional (Fases 0–3):** ~5–6 semanas (1 developer, 40h/sem)
**Producto completo:** ~10–12 semanas

---

## Árbol de Dependencias

```
TAREA-001 (Astro setup)
  ├── TAREA-002 (tokens CSS)
  ├── TAREA-003 (datos JSON)
  │     ├── TAREA-009 (PLP)
  │     ├── TAREA-010 (PDP) ──────────────┐
  │     └── TAREA-012 (búsqueda)          │
  └── TAREA-004 (componentes base)        │
        ├── TAREA-005 (nav mobile)        │
        ├── TAREA-006 (hero responsive)   │
        ├── TAREA-007 (grids)             │
        ├── TAREA-008 (footer)            │
        └── TAREA-011 (carrito) ──────────┤
              ├── TAREA-012 (búsqueda)    │
              └── TAREA-013 (checkout) ───┘
                    ├── TAREA-017 (analytics)
                    └── TAREA-019 (cuentas)
                          ├── TAREA-020 (profesional)
                          └── TAREA-021 (reviews)
```
