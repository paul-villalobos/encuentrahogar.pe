# Plan de Desarrollo de Plataforma Inmobiliaria (Zillow Perú) - MVP Lima

## Resumen Ejecutivo
Construcción de una plataforma inmobiliaria centrada en alquiler de viviendas en Lima utilizando **Astro + Tailwind CSS**. Objetivo: lanzar un MVP rápido, SEO-optimizado y escalable, con arquitectura moderna y experiencia superior.

---

## Alcance del MVP
- Home + búsqueda por alquiler + páginas por distrito.
- CRUD de propiedades (propietarios/admin).
- Páginas de detalle con fotos, mapa y contacto.
- Formularios de lead.
- Integración con Algolia (búsqueda) y Mapbox (mapas).
- SEO técnico completo.
- Panel de administración básico.

---

## Stack Tecnológico
**Frontend:** Astro + React Islands + Tailwind CSS  
**Backend:** Node.js (Fastify/Express)  
**DB:** PostgreSQL  
**Búsqueda:** Algolia  
**Mapas:** Mapbox  
**Hosting:** Vercel (frontend) + Render/Fly.io (backend)  
**CI/CD:** GitHub Actions  
**Storage:** S3-compatible  
**CMS opcional:** Strapi / Directus

---

## Arquitectura General
- **Frontend:** SSR/SSG híbrido (Astro)
- **API REST:** CRUD listings, leads, auth
- **DB:** PostgreSQL
- **Search:** Algolia (sincronización desde DB)
- **Storage:** S3 (imágenes)
- **CDN:** Cloudflare / hosting integrado

---

## Esquema de Datos (simplificado)
```
users(id, name, email, role, phone, hashed_password)
listings(id, title, slug, price, currency, operation, city, district, address, lat, lon, area_m2, beds, baths, furnished, description, status, owner_id)
photos(id, listing_id, url, order, alt)
leads(id, listing_id, name, email, phone, message, created_at)
```
---

## Endpoints Clave
- `GET /api/v1/listings`
- `GET /api/v1/listings/{id}`
- `POST /api/v1/listings`
- `POST /api/v1/leads`
- `GET /api/v1/districts/{city}`

---

## SEO
- Estructura de URLs: `/alquiler/lima/miraflores`
- JSON-LD: `Offer`, `Apartment`, `ImageObject`
- Sitemaps dinámicos + canonical tags
- Meta y OG tags configurados
- Contenido generado (landing por distrito)
- Optimización de Core Web Vitals

---

## Diseño (UI/UX)
- Mobile-first
- Paleta neutra y tipografía clara
- Componentes reutilizables con Tailwind
- Imágenes optimizadas (WebP/AVIF)
- Layout: Header + Search + Filters + Listing Grid + Map

---

## Fases y Sprints

### **Fase 0: Preparación (Sprint 0)**
Setup de entorno, repositorios, CI/CD, dominios y diseño inicial.

### **Fase 1: Fundamentos (Sprint 1–2)**
Base del proyecto Astro + Tailwind + API inicial + autenticación básica.

### **Fase 2: Listings CRUD + Admin (Sprint 3–4)**
Publicar y editar propiedades con fotos.

### **Fase 3: Búsqueda + Index (Sprint 5–6)**
Integración Algolia, filtros y relevancia.

### **Fase 4: Páginas Públicas SEO (Sprint 7–8)**
Landing pages por distrito, JSON-LD, sitemaps.

### **Fase 5: Mapa y Sincronización (Sprint 9)**
Mapa interactivo (Mapbox) con clustering.

### **Fase 6: Leads y Contacto (Sprint 10)**
Formulario de contacto y base de leads.

### **Fase 7: QA, Rendimiento, Accesibilidad (Sprint 11)**
Testing, performance tuning, Lighthouse audit.

### **Fase 8: Lanzamiento (Sprint 12)**
Despliegue final, backup, monitoreo y SEO post-launch.

---

## Backlog de Epics
| Epic | Descripción | Resultado Esperado |
|------|--------------|--------------------|
| Publicar listing | CRUD propiedades | Propiedades visibles y gestionables |
| Búsqueda | Algolia + filtros | Resultados rápidos y relevantes |
| Detalle listing | Página detallada | Fotos, mapa, contacto, SEO |
| SEO | Landing + Schema | Indexación completa |
| Leads | Contacto + notificaciones | Leads capturados y almacenados |

---

## QA & CI/CD
- **Tests:** Unit (Jest/Vitest), E2E (Playwright/Cypress)
- **CI/CD:** GitHub Actions (lint, test, build, deploy)
- **Monitoreo:** Sentry, GA4, Search Console

---

## Riesgos y Mitigaciones
| Riesgo | Mitigación |
|--------|-------------|
| Indexación lenta | Sitemaps dinámicos + canónicas |
| Costos API | Control de tokens Mapbox/Algolia |
| Imágenes pesadas | Compresión automática |
| Spam | Captcha + rate limiting |

---

## Checklist de Lanzamiento
- [ ] URLs y sitemaps generados
- [ ] JSON-LD implementado
- [ ] GA4 + Search Console conectados
- [ ] CI/CD automatizado
- [ ] Backups activos
- [ ] Panel admin operativo
- [ ] SEO audit pasado
- [ ] Listings iniciales publicados

---

© 2025 Proyecto Inmobiliario Perú – Plan de Desarrollo by Paul Villalobos
