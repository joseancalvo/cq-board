# AGENTS.md

Guía de contexto y convenciones para agentes de IA que trabajen en este repositorio.

---

## 1. Visión general del proyecto

Este repositorio aloja el **sitio web oficial (landing page) y la política de privacidad** de **CQ Board** (`https://joseancalvo.github.io/cq-board/`), una aplicación móvil para radioaficionados (SOTA, POTA y operación diaria) desarrollada por **EA2EYI**.

- **Propósito del repositorio**: Presentar las funcionalidades de la app, enlazar a las tiendas de aplicaciones (App Store y Google Play), ofrecer soporte y alojar la página de política de privacidad exigida por las tiendas.
- **Naturaleza técnica**: Sitio web **100% estático** en HTML5 y CSS3 puro, sin bundlers, frameworks JS ni dependencias (`package.json` inexistente).

---

## 2. Estructura del repositorio

```text
.
├── .github/
│   └── workflows/
│       └── deploy-pages.yml  # Despliegue automático en GitHub Pages al hacer push a `main`
├── assets/
│   ├── CQBoard-icon.png      # Icono / favicon de la aplicación (256x256)
│   ├── IMG_3526.PNG          # Captura: Relojes y notas de activación
│   ├── IMG_3527.PNG          # Captura: Modo noche (tema oscuro)
│   └── IMG_3528.PNG          # Captura: Modo día (tema claro)
├── css/
│   └── styles.css            # Hoja de estilos única (variables CSS, layout, responsive)
├── index.html                # Landing page principal (Funciones, Capturas, Privacidad, Soporte)
├── privacy.html              # Política de privacidad oficial para App Store / Google Play
└── README.md                 # Documentación general del repositorio
```

---

## 3. Stack tecnológico y convenciones de código

### HTML (`index.html`, `privacy.html`)
- **Idioma**: Español (`<html lang="es">`). Mantén siempre el tono claro, directo y cercano a la comunidad de radioaficionados.
- **Semántica y accesibilidad**: Uso de etiquetas semánticas (`<header>`, `<main>`, `<section>`, `<figure>`, `<footer>`), atributos `aria-label` / `aria-disabled` y textos alternativos (`alt`) descriptivos en imágenes.
- **Rutas relativas**: Dado que el sitio se sirve bajo el subdirectorio `/cq-board/` en GitHub Pages, **todas las rutas a recursos internos y enlaces entre páginas deben ser relativas** (ej. `css/styles.css`, `assets/...`, `index.html`, `privacy.html`), nunca absolutas desde la raíz (`/css/...`).
- **JavaScript**: Mínimo e inline únicamente para actualizar el año actual en el pie de página (`#y`). Evita añadir scripts externos, trackers o librerías.

### CSS (`css/styles.css`)
- **Tokens de diseño**: Centralizados en `:root`:
  - Fondos oscuros: `--bg: #141716`, `--bg-card: #1c2220`
  - Texto: `--text: #eff3f1`, `--muted: #9aa5a0`
  - Acentos (ámbar/dorado): `--accent: #e5b438`, `--accent-2: #f3c64f`
  - Bordes y estado: `--line: #2b3531`, `--ok: #6bcf8e`
  - Layout: `--radius: 14px`, `--max: 720px`
- **CSS moderno**: Uso nativo de `color-mix(in srgb, ...)`, `clamp()`, `min()`, CSS Grid (`auto-fit` / `minmax`) y Flexbox.
- **Responsive**: Punto de corte móvil en `@media (max-width: 540px)` con navegación horizontal desplazable sin barra visible.

---

## 4. Desarrollo local y despliegue

- **Previsualización local**: No requiere compilación. Puedes abrir `index.html` directamente o levantar un servidor estático local:
  ```bash
  python3 -m http.server 8000
  ```
- **Despliegue (CI/CD)**: El workflow `.github/workflows/deploy-pages.yml` publica directamente la raíz del repositorio (`path: "."`) en GitHub Pages en cada `push` a la rama `main` o mediante ejecución manual (`workflow_dispatch`).

---

## 5. Reglas e invariantes para agentes

1. **No introducir herramientas de build ni dependencias**: Mantén el proyecto libre de `node_modules`, frameworks o preprocesadores salvo petición explícita del usuario.
2. **Coherencia con los principios de privacidad**: CQ Board destaca por no usar cuentas, servidores ni telemetría. No agregues recursos de terceros en la web (como Google Fonts externas, CDNs de scripts o analíticas) que comprometan la privacidad o la carga autónoma de la página.
3. **Cuidado con `privacy.html`**: Es un documento vinculante para la revisión en App Store y Google Play. Si se modifica información sobre permisos, tratamiento de datos o contacto, asegúrate de actualizar también la fecha de *"Última actualización"* en `<p class="meta">`.
4. **Enlaces a tiendas y contacto**:
   - **iOS (App Store)**: Activo (`https://apps.apple.com/es/app/cq-board/id6807329150`).
   - **Android (Google Play)**: Activo (`https://play.google.com/store/apps/details?id=com.eyilabs.cqboard`).
   - **Contacto y soporte**: `jose@eyilabs.com` (presente en `index.html`, `privacy.html` y `README.md`).
