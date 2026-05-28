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
