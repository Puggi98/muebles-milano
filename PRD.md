# PRD — Modern Studio: Sitio Web de Muebles de Lujo

**Versión:** 1.0
**Fecha:** 30 de marzo de 2026
**Estado:** Borrador para revisión

---

## 1. Visión del Producto

Modern Studio es una tienda online de muebles modernos de lujo que compite en el segmento premium-aspiracional, comparable a referentes como Design Within Reach, Arhaus o Zanotta. La visión es construir una experiencia digital que refleje la misma calidad artesanal y sofisticación estética que los productos que vende: navegación fluida, imágenes de alta calidad, cero fricciones en el proceso de compra y una identidad visual coherente en todos los puntos de contacto.

El prototipo actual (`index.html`) establece una base visual sólida con identidad definida (paleta negro/blanco/dorado, tipografía Cormorant Garamond + Montserrat, logo geométrico). El trabajo pendiente es convertirlo en un sitio funcional, escalable y optimizado para conversión.

---

## 2. Usuarios Objetivo

### 2.1 Perfil Primario — Comprador Residencial Premium
- Hombres y mujeres de 35–60 años
- Ingresos altos, gusto por el diseño contemporáneo
- Renuevan espacios en casa o adquieren piezas únicas de marcas como Cassina, B&B Italia, Fritz Hansen
- Investigan online pero pueden cerrar compra en showroom
- Dispositivos: desktop en fase de exploración, móvil para referencias rápidas

### 2.2 Perfil Secundario — Profesional del Diseño
- Arquitectos, interioristas, diseñadores de interiores
- Requieren cuenta profesional con descuentos por volumen
- Necesitan fichas técnicas detalladas, muestras de materiales, plazos de entrega
- Gestionan múltiples proyectos simultáneos

### 2.3 Perfil Terciario — Comprador Corporativo
- Empresas amueblando oficinas, hoteles o espacios de hospitalidad
- Requieren cotizaciones, atención personalizada, facturación corporativa

---

## 3. Análisis del Prototipo Actual

### Lo que ya existe y está bien resuelto
- Identidad visual clara y coherente (paleta, tipografía, espaciado)
- Header flotante sobre hero con logo SVG geométrico
- Navegación con 8 categorías y dropdowns por hover
- Hero fullscreen con imagen + overlay oscuro
- Barra de anuncio superior y banner promocional inferior al hero
- Grid de colecciones 2×2 con efecto hover en imagen
- Banner promo "Diseño sin Compromiso"
- Grid de 4 productos destacados con marca, nombre y precio
- Footer de 4 columnas con links y copyright

### Gaps críticos identificados
- Sin responsividad (sin media queries)
- Sin JavaScript funcional (carrito sin lógica, búsqueda sin abrir)
- Sin páginas internas (PDPs, PLPs, checkout)
- Sin sistema de gestión de contenido ni datos de producto
- Sin manejo de estado (carrito vacío, sin contador de items)
- Sin accesibilidad básica (foco visible, contraste en nav)
- Sin SEO técnico (meta tags, Open Graph, structured data)
- Sin analytics

---

## 4. Features Requeridos (Must Have)

### F-01 Responsividad Completa
Toda la UI existente debe funcionar en móvil (320px), tablet (768px) y desktop (1280px+). El header flotante colapsa en hamburger en mobile.

### F-02 Carrito Funcional
Panel lateral deslizante (drawer) con productos, cantidades, subtotal y botón de checkout. Persistencia en `localStorage`. Contador visible en header.

### F-03 Búsqueda Funcional
Modal de búsqueda activado por el ícono de lupa. Búsqueda por nombre, categoría o marca dentro del catálogo.

### F-04 Página de Listado de Productos (PLP)
Una página por categoría con filtros por precio, material, marca. Ordenamiento y paginación.

### F-05 Página de Detalle de Producto (PDP)
Galería de imágenes con zoom, selección de variantes, descripción técnica, botón "Agregar al carrito" y productos relacionados.

### F-06 Menú Mobile (Hamburger)
Drawer lateral con todas las categorías en acordeón expandible.

### F-07 Sistema de Datos de Producto
Esquema JSON con campos: id, slug, nombre, marca, precio, imágenes, categoría, variantes, descripción, dimensiones.

### F-08 Checkout Básico
Formulario de envío + integración con Stripe Checkout o MercadoPago.

### F-09 SEO Técnico Base
`<title>` y `<meta description>` únicos, Open Graph, structured data `Product`, sitemap.xml, robots.txt.

### F-10 Performance Básica
Lazy loading, WebP/AVIF, fuentes optimizadas. Core Web Vitals: LCP < 2.5s, CLS < 0.1.

---

## 5. Features Nice-to-Have

| ID | Feature | Impacto | Complejidad |
|----|---------|---------|-------------|
| N-01 | Wishlist / Lista de Deseos | Alto | Baja |
| N-02 | Cuenta de Usuario | Alto | Alta |
| N-03 | Cuenta Profesional con descuento | Alto | Media |
| N-04 | Blog de Diseño | Medio | Media |
| N-05 | Configurador 3D/AR | Muy Alto | Muy Alta |
| N-06 | Chat de Atención al Cliente | Medio | Baja |
| N-07 | Reviews y Calificaciones | Alto | Media |
| N-08 | Comparador de Productos | Medio | Media |
| N-09 | Notificaciones de Stock | Medio | Baja |
| N-10 | Programa de Fidelidad | Alto | Alta |

---

## 6. Requerimientos Técnicos

### 6.1 Stack Recomendado

| Capa | Tecnología | Razón |
|------|-----------|-------|
| Framework | Astro 4.x | HTML-first, multi-page, máxima performance |
| UI Interactiva | React 18 (islas) | Carrito, búsqueda, filtros |
| Estilos | CSS Modules o Tailwind (config minimal) | Reutilizable, sin colisiones |
| Datos | JSON estático → Sanity/Directus (fase 2) | Escalable sin reescritura |
| Pagos | Stripe Checkout | Rápido de integrar, PCI compliant |
| Hosting | Vercel o Netlify | CDN global, deploy automático |
| Analytics | Plausible Analytics | Privacy-first, liviano |
| Imágenes | Astro Image + Cloudinary (fase 2) | Optimización automática |

### 6.2 Navegadores Soportados
Chrome 100+, Firefox 100+, Safari 15+, Edge 100+.

### 6.3 Accesibilidad
WCAG 2.1 nivel AA. Navegación por teclado, roles ARIA, contraste mínimo 4.5:1.

### 6.4 Seguridad
HTTPS obligatorio. Headers CSP, X-Frame-Options, HSTS. Sin datos de tarjeta en el servidor propio.

---

## 7. Métricas de Éxito

### Performance Técnica
- LCP < 2.5s | CLS < 0.1 | INP < 100ms
- Lighthouse Score > 90 en Performance, Accessibility y SEO

### Engagement
- Tasa de rebote < 55%
- Páginas por sesión > 4
- Tiempo promedio en sesión > 3 min

### Conversión
- Add to Cart Rate > 8% en PDP
- Checkout Completion Rate > 65%
- Tasa de conversión general > 1.5%
- AOV (Average Order Value) > $2,500 USD

### SEO
- Indexación completa en Google en < 30 días
- 0 errores críticos en Core Web Vitals a 60 días de lanzamiento
