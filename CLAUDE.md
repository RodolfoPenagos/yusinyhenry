# Invitación de Boda — Yusin & Henry

Sitio web de invitación de boda. Single-page, HTML/CSS/JS vanilla, sin frameworks ni build step. Optimizado para móvil (la mayoría de invitados lo abrirá desde WhatsApp).

## Estructura y deploy
- **`index.html`** — archivo canónico del sitio (editar este). Incluye meta tags Open Graph con URLs absolutas al sitio publicado.
- **`assets/`** — las 7 fotos (hero portrait/landscape, galería 1–4, banner), extraídas del base64 original.
- **`invitacion-yusin-henry-v6.html`** — artefacto original de Cowork con fotos embebidas en base64; se conserva como respaldo histórico, NO editar.
- **Publicado en GitHub Pages:** https://rodolfopenagos.github.io/yusinyhenry/ — repo `RodolfoPenagos/yusinyhenry` (público), rama `master`, raíz. Cada `git push` republica automáticamente (~30 s).
- La vista previa de WhatsApp usa `og:image` → `assets/banner.jpg`; si se renombra o cambia esa foto, actualizar los meta tags.

## Datos del evento (NO modificar sin confirmación)
- **Novios:** Yusin Penagos Ruiz & Henry Ayala García
- **Fecha:** Sábado 14 de noviembre de 2026
- **Ceremonia:** Iglesia San Pedro y San Pablo, Tampico, Tamaulipas — 8:30 pm
- **Recepción:** Salón Deportivo Español, Tampico, Tamaulipas — 9:30 pm
- **Padres de la novia:** José Rodolfo Penagos García ✝ (finado — siempre con cruz) y Yusin Ruiz Vargas
- **Padres del novio:** Enrique Ayala Piñeyro y Laura Lilia García Ponce
- **Dress code:** Formal de noche (caballeros: traje formal · damas: vestido largo de noche)
- **Solo adultos** (redactado de forma amable en la sección dress code)
- **RSVP:** WhatsApp +52 833 148 8043, fecha límite 14 de octubre de 2026
- **Regalos:** Liverpool evento 51974215 · Amazon amazon.com.mx/wedding/share/YusinyHenry · BBVA (datos en la sección, con botones de copiar)

## Sistema de diseño

### Paleta (de su moodboard oficial)
```
--ivory:     #F5F0EB  (base / fondos)
--blush:     #C2B1A7  (tonos suaves)
--taupe:     #B49F92  (principal)
--dusty:     #A78D7C  (acentos románticos)
--mocha:     #96745D  (contraste cálido, títulos)
--mocha-deep:#7A5C47  (footer, hovers)
--champagne: #D6C4A3  (acento metálico, ornamentos)
--ink:       #6E5A4C  (texto body)
--white:     #FDFBF8
```

### Espaciado — REGLA DE 8px (estricta)
Tokens en `:root`: `--s1:8 --s2:16 --s3:24 --s4:32 --s5:40 --s6:48 --s8:64 --s12:96 --s15:120`
- 96px entre secciones · 48px título→contenido · 24px entre hermanos (cards, gaps)
- 16px etiqueta→texto · 8px pares íntimos (label/valor, icono/texto)
- Nunca introducir valores fuera de la escala.

### Tipografía — escala en pasos de 8
Tokens: `--fs-caption:12 --fs-small:16 --fs-body:20 --fs-lead:24` + h2 `clamp(32,5.5vw,40)` + display 48 + h1 `clamp(64,12.5vw,96)`
- **Great Vibes** (script): h1 nombres, footer, banner
- **Cormorant Garamond** (serif): h2, body, horas, countdown
- **Jost** (sans, light, versalitas con tracking): eyebrows, h3, botones, labels
- Body serif a 20px es ajuste óptico deliberado (Cormorant tiene x-height baja; 20px ≈ 16px de una sans). Los line-heights caen en retícula de 8 (body 32, lead 40, quote 48).

### Iconos — Tabler Icons OBLIGATORIO
- SVG inline con paths **verbatim del repo oficial** (MIT). NO dibujar iconos a mano, NO aproximar paths.
- Estilo: `fill:none`, `stroke-linecap:round`, `stroke-linejoin:round`, trazo fino (0.6–1.5 según tamaño de render), colores de la paleta.
- En uso: building-church, glass-champagne, moon-stars, tie, hanger, gift, credit-card, map-pin, calendar-heart, music, brand-whatsapp, heart, chevron-left/right.
- Los ornamentos florales (ramitas, flourishes de esquina) sí son SVG propios en `<defs>` — esos se conservan.

## Decisiones tomadas (no revertir)
- **Sin animación de sobre al inicio** (se eliminó; se retomará como mejora en Claude Design más adelante)
- **Hero:** foto full-bleed cubriendo 100svh, con velo degradado café oscuro y tipografía clara (blanco/ivory/champagne) para contraste. `<picture>`: foto vertical en orientación portrait, horizontal en landscape. Pétalos cayendo (CSS, respeta `prefers-reduced-motion`).
- **Galería:** carrusel horizontal con scroll-snap, flechas, dots, auto-avance 5.2s solo cuando es visible.
  - ⚠️ **NUNCA usar `scrollIntoView` en el carrusel** — desplaza la página verticalmente (bug ya corregido). Usar solo `track.scrollTo({left})`.
- Fotos en `/assets` como archivos jpg con `loading="lazy"` en la galería (extraídas del base64 original al montar el repo).
- Botón de música flotante listo pero sin fuente de audio (`<audio>` con src vacío); falta el MP3 de la pareja.

## Pendientes conocidos
- [ ] Texto real de "Nuestra historia" (el actual es placeholder escrito por Claude)
- [ ] MP3 de la canción de la pareja para el botón de música
- [ ] Posible reintroducción del sobre animado (nivel de calidad premium, en Claude Design)
- [x] Deploy — hecho en GitHub Pages: https://rodolfopenagos.github.io/yusinyhenry/ (pendiente opcional: dominio propio o URL corta)
- [ ] Considerar icono de vestido (Phosphor, MIT) si el hanger de Tabler no convence para "Damas"

## Comandos
Sin build. Servir localmente con `python -m http.server 8123` (hay config de preview en `.claude/launch.json`). Publicar cambios: `git add` + `git commit` + `git push` (GitHub Pages reconstruye solo).
