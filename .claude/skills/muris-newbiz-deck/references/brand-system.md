# Sistema visual Muris Brand — extraído de la landing de Verona

Valores tomados del CSS en producción de `murisbrand.com/es/pages/verona-by-muris-brand`
(septiembre 2026). Son los tokens reales, no una aproximación.

## Color

| Token | Valor | Uso |
|-------|-------|-----|
| `--ink` | `#171717` | Texto, botones, fondos oscuros. Nunca negro puro en texto |
| `--paper` | `#FFFFFF` | Fondo por defecto. El deck es blanco |
| `--mint` | `#8FFFC4` | Acento de marca. Barra de anuncio y botones secundarios en la web. En deck: una o dos slides de cierre/transición |
| `--plum` | `#614051` | Highlight de marca. Subrayados, detalles, texto sobre menta |
| `--grey` | `#8E8E8E` | Texto secundario, pies de foto, numeración de slide |
| `--hairline` | `rgba(23,23,23,.1)` | Líneas divisorias. Siempre 1px |

Sobre menta el texto va en `--ink`, nunca en blanco.
Sobre `--ink` el texto va en blanco.

## Tipografía

La web usa dos fuentes propietarias servidas desde su CDN:

- **Titulares**: `Awesome Serif` (archivo `AwesomeSerif-MediumRegular.otf`)
- **Texto**: `Sequel Sans Book Head` (archivo `Sequel_Sans_Book_Head.otf`)
- **Sistema/fallback real en la web**: `Inter` 400/500/700

**Sustitutos si no tienes los OTF**: `Instrument Serif` para titulares (Google Fonts,
la propia web la carga) e `Inter` para texto. La plantilla ya viene así.
Si el usuario aporta los OTF, mételos con `@font-face` y cambia las variables
`--font-display` y `--font-text` — no toques nada más.

Ajustes que definen el tono:

- Cuerpo y manifiesto: **mayúsculas**, peso 400, `line-height` 1.25, `letter-spacing` 0.
  Nunca negrita para enfatizar; enfatiza con salto de línea.
- Titulares serif: peso 400, `line-height` 1, `letter-spacing` 0. Grandes de verdad.
- Base de cuerpo: 17px en web → en deck de 1280px de ancho, 20–22px.

Escala de titulares (fluida, de la web):

```
--title-xl: clamp(3rem, 7.8vw, 5rem)
--title-lg: clamp(2.5rem, 3.4vw, 4rem)
--title-md: clamp(2rem, 3.4vw, 4rem)
--title-sm: clamp(1.56rem, 2.5vw, 3.06rem)
```

## Espaciado y retícula

- Contenedor máximo: `1800px`; padding de página `1.25rem`.
- Gap de rejilla: `clamp(40px, 20vw, 60px)` — el aire entre bloques es grande a propósito.
- Escala de espaciado en múltiplos de `0.25rem` (4px). Usa 20 / 40 / 60 / 80 / 120.

## Formas

- Radio de botones e inputs: **6px**. Es el detalle que evita que parezca genérico.
- Radio de tarjetas/bloques: `clamp(0.625rem, 1.05vw, 1.25rem)`.
- Sombras: **no**. `--card-shadow-opacity` está a 0.1 y en la práctica no se ven.
- Bordes: 1px, opacidad 0.1 sobre la tinta.

## Botones y CTAs

Fondo `--ink`, texto blanco, radio 6px, padding `18px 26px`, peso 500, sin mayúsculas.
El secundario es menta con texto `--ink`.

## Movimiento

Las transiciones de la web, por si animas el deck:

```
--animation-primary: .5s cubic-bezier(.3, 1, .3, 1)
--animation-smooth:  .7s cubic-bezier(.7, 0, .3, 1)
--animation-fast:    .3s cubic-bezier(.7, 0, .3, 1)
```

Fade + desplazamiento de 12px. Nada de zooms ni rebotes.

## Imagen

- A sangre, formato vertical o cuadrado, luz natural, grano, escenas de calle.
- Sin filtros de color ni overlays salvo un velo de tinta al 20–30% cuando
  haya texto encima.
- Los mosaicos son de 3 imágenes con alturas desiguales, nunca una rejilla regular.
