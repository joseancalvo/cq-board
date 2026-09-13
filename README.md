# CQ Board — web para GitHub Pages

Landing pública de la app (no incluye el código fuente de iOS/Android).

## Archivos

- `index.html` — portada (nombre, funciones, capturas placeholder, tiendas, soporte)
- `privacy.html` — política de privacidad (necesaria para App Store / Play)
- `css/styles.css` — estilos
- `assets/` — aquí van capturas reales (`shot-1.png`, etc.)

## Antes de publicar

1. Sustituye `SOPORTE@ejemplo.com` en `index.html` y `privacy.html` por tu email real.
2. Cuando tengas URLs de App Store y Google Play, quita la clase `btn--disabled` de esos botones y pon el `href` real.
3. Sustituye los placeholders de capturas por imágenes en `assets/`.

## Publicar en GitHub Pages

1. Crea un repositorio vacío, por ejemplo `cq-board` (solo esta web).
2. Sube el contenido de esta carpeta a la rama `main` (los HTML en la raíz del repo).
3. En el repo: **Settings → Pages → Deploy from a branch → `main` / root**.
4. La URL quedará tipo: `https://TU_USUARIO.github.io/cq-board/`
5. En App Store Connect / Play Console, pon esa URL (y la de `/privacy.html`) donde pidan el sitio y la privacidad.

## Probar en local

Abre `index.html` en el navegador, o desde esta carpeta:

```bash
python3 -m http.server 8080
```

Luego visita `http://localhost:8080`.
