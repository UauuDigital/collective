## Paleta de colores

- Fondo oscuro principal: #221F1E
- Fondo claro / crema: #F2EFEE
- Texto sobre fondo claro: #221F1E
- Texto sobre fondo oscuro: #FFFFFF
- Texto secundario (oscuro): rgba(34,31,30,0.7)
- Texto secundario (claro): rgba(255,255,255,0.6)
- Bordes sutiles (oscuro): rgba(34,31,30,0.08–0.22)
- Bordes sutiles (claro): rgba(255,255,255,0.15–0.4)

## Tipografía

- **Display / títulos grandes**: Ogg Medium (local, .otf/.ttf) — font-weight: 500
  - Características: letter-spacing: -0.025em, line-height: 1.05–1.12
- **UI / body / etiquetas**: Inter Variable (local, .ttf) — font-weight: 100–900
  - Características: letter-spacing variable según contexto
- Fallbacks: Georgia, serif

## Escala tipográfica

| Uso | Fuente | Tamaño | Weight |
|---|---|---|---|
| Hero / títulos principales | Ogg | clamp(30px, 4.2vw, 66px) | 500 |
| Títulos de sección | Ogg | clamp(22px, 2.8vw, 42px) | 500 |
| Navegación overlay | Ogg | 72px | 500 |
| Precios | Ogg | clamp(24px, 2.8vw, 46px) | 500 |
| Títulos UI | Inter | clamp(22px, 2.6vw, 38px) | 600 |
| Body / features | Inter | 14–16px | 300 |
| Etiquetas / caps | Inter | 10–13px | 400, letter-spacing: 0.06–0.14em, uppercase |
| Notas / fine print | Inter | 10–11px | 300 |

## Layout y espaciado

- Padding lateral principal: 10% (desktop), 14px–20px (mobile)
- Header height: 80px desktop / 60px mobile
- Border-radius tarjetas: 16–18px
- Border-radius pills/botones: 100px

## Componentes y patrones

### Botón principal (CTA)
- Borde 1px, border-radius 100px, padding 15px 28px 15px 32px
- Fondo transparente con hover: rgba(255,255,255,0.07)
- Con flecha animada inline (gap se expande en hover)
- Texto: Inter, 11px, uppercase, letter-spacing: 0.14em

### Pills / filtros
- Inter, 10px, uppercase, letter-spacing: 0.09em
- Borde 1px sutil, border-radius 100px

### Transiciones
- Estándar: 0.3–0.4s ease
- Movimiento suave (expo-out): cubic-bezier(.22,1,.36,1)
- Página/overlay: 0.38–0.62s

## Fondos y overlays

- Overlay de vídeo: linear-gradient to bottom, rgba(34,31,30,0.82) 0% → 0.38 resto
- Mask en wheel: fade top/bottom transparent → black al 21%/79%
- Lightbox: rgba(34,31,30,0.96)

## Breakpoints responsive

- Tablet/móvil: max-width: 1024px
- Móvil pequeño: max-width: 480px

## Referencias visuales

Ver `_refs/referencia-estilo.jpg` para el estilo visual de referencia.

---

## Arquitectura del proyecto

Todo el proyecto es un único `index.html` con CSS, JS y datos completamente inline. No hay build system, ni bundler, ni archivos JS/CSS externos propios. Los assets estáticos son fonts (locales, carpeta `fonts/`) y logos (`logos/`). Los medias (vídeos e imágenes de colaboradores) se sirven desde `https://uauu.cat/media/collective/`.

## Estructura de datos — colaboradores

Los datos viven en el array `categoryData` dentro del JS inline de `index.html`. Cada sección tiene esta forma:

```js
{
  id: 'slug-seccion',
  carousel: true,          // true = cards con carrusel de vídeo/foto
  video: 'url.mp4',        // vídeo de portada de la sección (solo si carousel: true)
  image: 'url.webp',       // imagen de portada (si no tiene vídeo)
  collaborators: [ ... ]
}
```

### Colaborador con carrusel de vídeo/imagen mixto

```js
{
  name: 'Nombre',
  tags: { ca: '...', es: '...', en: '...' },
  loc: '',                  // idiomas si aplica, ej: 'CA · ES · EN'
  phone: '+34 600 000 000',
  email: 'mail@example.com',
  web: 'https://...',
  social: '@handle',
  socialFirst: true,        // muestra Instagram como primer enlace
  note: null,               // o { ca: '...', es: '...', en: '...' } para descuentos/notas
  videos: ['url1.mp4', 'url2.mp4', 'url3.webp', ...],  // soporta .mp4 y .webp/.jpg mezclados
  positions: ['center', 'center', 'center 30%', ...]   // object-position por índice (opcional)
}
```

### Colaborador con carrusel de fotos

```js
{
  // ... campos comunes ...
  photos: ['url1.webp', ...],
  positions: ['top', 'center 20%', ...]   // object-position por índice (opcional)
}
```

### Colaborador con imagen única

```js
{
  // ... campos comunes ...
  image: 'url.webp'
}
```

### URLs de medias

Patrón: `https://uauu.cat/media/collective/{categoria}/{colaborador}/{archivo}`  
Ejemplo: `https://uauu.cat/media/collective/content_creator/memoir/memoir_1.mp4`

## Sistema de caché

- **`.htaccess`**: `index.html` con `Cache-Control: no-cache, must-revalidate`. Assets estáticos (fonts, logos) con caché de 1 año.
- **JS inline** (al final del `<body>`): en el evento `visibilitychange`, hace un `HEAD` request a `index.html` comparando el `ETag`/`Last-Modified`. Si cambió, recarga automáticamente. Mínimo 5 min entre checks.

Para forzar actualización en todos los usuarios: simplemente despliega el nuevo `index.html`.

## Patrones técnicos importantes

- **Hover scale solo en cards de imagen única**: `.collab-photo:not([data-carousel]) img { transform: scale(1.06) }`. Las imgs dentro de carruseles NO deben escalar en hover — las imgs de slides no visibles se desplazarían ~3% hacia el área visible.
- **Overflow clip del carrusel**: `.collab-photo` tiene `transform: translateZ(0)` para forzar compositing layer y que `overflow: hidden` funcione correctamente en Safari cuando el padre `.collab-card` tiene transform.
- **Slides del carrusel**: usan `flex: 0 0 100%` (no `width: 100%`) para evitar ambigüedad en el cálculo de tamaño en flex containers.