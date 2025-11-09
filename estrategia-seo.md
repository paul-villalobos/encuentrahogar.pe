---
description: Estrategia completa de SEO para la plataforma inmobiliaria (Encuentra Hogar - Lima), incluyendo metadatos, datos estructurados, breadcrumbs y mejores prácticas implementadas.
alwaysApply: false
---

# name: seo-best-practices-inmobiliaria

# description: Reglas y mejores prácticas SEO implementadas en la plataforma de alquileres y ventas en Perú (Encuentra Hogar - Lima), optimizadas para indexación local, visibilidad geográfica y rendimiento en motores de búsqueda.

# globs: ["src/pages/**/*.astro", "src/layouts/**/*.astro", "src/components/**/*.astro"]

# alwaysApply: true

## 🎯 Objetivo

Garantizar que todas las páginas del sitio inmobiliario implementen las mejores prácticas SEO para maximizar su visibilidad en Google y portales locales, aplicando metadatos dinámicos, datos estructurados JSON-LD, breadcrumbs y optimizaciones técnicas para SEO local (Lima y provincias).

---

## ✅ REQUISITOS OBLIGATORIOS PARA TODAS LAS PÁGINAS

### 1. Metadatos SEO Dinámicos

**SIEMPRE** pasar props a `MainLayout` para cada tipo de página (inmueble, distrito, categoría, agente).

Ejemplo para página de inmueble:

```astro
import { generatePropertyMeta } from '../utils/seoUtils';
const meta = generatePropertyMeta(property);

<MainLayout
  title={meta.title}
  description={meta.description}
  keywords={meta.keywords}
  canonical={meta.canonical}
  ogImage={meta.ogImage}
  ogType={meta.ogType}
  structuredData={propertyStructuredData}
>
```

### 2. Funciones de Generación de Metadatos

Ubicar en `src/utils/seoUtils.ts`

```typescript
export function generatePropertyMeta(property) {
  const siteUrl = "https://encuentrahogar.pe";
  const pageUrl = `${siteUrl}/propiedad/${property.slug}`;

  return {
    title: `${property.titulo} en alquiler | ${property.distrito} | Encuentra Hogar`,
    description: `Alquila ${property.tipo} en ${property.distrito}. ${property.habitaciones} habitaciones, ${property.metros} m². Precio: S/${property.precio}.`,
    keywords: `${property.tipo}, alquiler en ${property.distrito}, departamentos en Lima, inmuebles Perú`,
    canonical: pageUrl,
    ogImage: property.imagenDestacada || `${siteUrl}/images/og-default.jpg`,
    ogType: "product",
  };
}
```

### 3. Datos Estructurados JSON-LD

Implementar **Property**, **Place**, **Offer** y **BreadcrumbList** según la página.

```typescript
export function generatePropertyStructuredData(property) {
  const siteUrl = "https://encuentrahogar.pe";
  const pageUrl = `${siteUrl}/propiedad/${property.slug}`;

  return {
    "@context": "https://schema.org",
    "@type": "Product",
    name: property.titulo,
    image: property.imagenDestacada,
    description: property.descripcion,
    brand: { "@type": "Organization", name: "Encuentra Hogar" },
    offers: {
      "@type": "Offer",
      priceCurrency: "PEN",
      price: property.precio,
      availability: "https://schema.org/InStock",
      url: pageUrl,
    },
    address: {
      "@type": "PostalAddress",
      addressLocality: property.distrito,
      addressRegion: "Lima",
      addressCountry: "PE",
    },
  };
}
```

### 4. Breadcrumbs

Incluir breadcrumbs en todas las páginas que no sean la home:

```typescript
const breadcrumbs = [
  { name: "Inicio", url: "https://encuentrahogar.pe" },
  { name: "Lima", url: "https://encuentrahogar.pe/lima" },
  {
    name: property.distrito,
    url: `https://encuentrahogar.pe/lima/${property.distritoSlug}`,
  },
  {
    name: property.titulo,
    url: `https://encuentrahogar.pe/propiedad/${property.slug}`,
  },
];
```

---

## 🖼️ OPTIMIZACIÓN DE IMÁGENES

Todas las imágenes deben tener dimensiones explícitas, alt dinámico y `loading="lazy"`.  
Usar formatos **WebP** o **AVIF**.

---

## 📝 CANONICAL URLs Y LOCAL SEO

- Canonical debe ser **único por propiedad**.
- Incluir metadatos locales (`geo.region`, `geo.position`, `ICBM`).
- Cada propiedad debe incluir información geográfica en su structured data.

---

## 📋 PATRONES POR TIPO DE PÁGINA

### Página Principal (Home)

- JSON-LD: `WebSite`
- Title: "Encuentra Hogar | Alquiler y Venta de Departamentos y Casas en Lima"
- Description: "Encuentra alquileres, casas y departamentos en Lima y todo el Perú. Busca por distrito, precio o tipo de inmueble."

### Página de Distrito

- JSON-LD: `Place`
- Title: "Departamentos en alquiler en Miraflores | Encuentra Hogar"
- Description: "Explora inmuebles en alquiler en Miraflores, Lima. Encuentra el lugar ideal para vivir."

### Página de Propiedad

- JSON-LD: `Product + Offer + BreadcrumbList`
- Title y descripción generados dinámicamente según propiedad.

### Página de Contacto / Agente

- JSON-LD: `RealEstateAgent`

---

## ✅ CHECKLIST SEO PARA NUEVAS PÁGINAS

- [ ] Crear función `generate[Nombre]Meta()` en `seoUtils.ts`
- [ ] Incluir datos estructurados adecuados (`Property`, `Place`, etc.)
- [ ] Incluir breadcrumbs
- [ ] Incluir `width` y `height` en imágenes
- [ ] Verificar canonical único
- [ ] No usar scripts inline
- [ ] Validar en Google Rich Results y Schema.org Validator

---

## 🚀 PRIORIDADES

1. **CRÍTICO:** Metadatos dinámicos, datos estructurados, canonical únicos
2. **IMPORTANTE:** Breadcrumbs, optimización de imágenes, SEO local
3. **MEJORAS:** Integración con Google Maps y Search Console
