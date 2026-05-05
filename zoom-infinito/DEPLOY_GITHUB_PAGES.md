# Guía de despliegue en GitHub Pages

Esta carpeta ya contiene una versión estática completa de la aplicación. No necesitas ejecutar `npm install`, `npm run build` ni configurar Vite para publicarla.

## Opción recomendada: publicar desde la raíz

1. Crea un repositorio en GitHub.
2. Sube todos los archivos de esta carpeta a la raíz del repositorio.
3. Ve a `Settings > Pages`.
4. En `Build and deployment`, selecciona `Deploy from a branch`.
5. Selecciona la rama `main`.
6. En carpeta, selecciona `/root`.
7. Guarda.

GitHub generará una URL similar a:

```text
https://usuario.github.io/nombre-del-repositorio/
```

## Alternativa: publicar desde `/docs`

Si prefieres mantener otros archivos en la raíz del repositorio:

1. Crea una carpeta `docs`.
2. Mueve dentro de `docs` estos elementos:
   - `index.html`
   - `assets/`
   - `.nojekyll`
3. Mantén `README.md` y `DOCUMENTACION_TECNICA.md` en la raíz si lo prefieres.
4. En `Settings > Pages`, selecciona `/docs` como carpeta de publicación.

## Por qué existe `.nojekyll`

GitHub Pages usa Jekyll por defecto en algunos repositorios. El archivo `.nojekyll` desactiva ese procesamiento y evita problemas con carpetas o assets generados automáticamente.

## Comprobación después del despliegue

Una vez publicada la web, revisa:

- Que carga la interfaz completa.
- Que se ve el timeline.
- Que los sliders funcionan.
- Que la ficha activa cambia al mover el año central.
- Que los filtros por sistema modifican los datos visibles.
- Que la vista narrativa se abre correctamente.
- Que el modo claro/oscuro responde.
- Que la exportación CSV funciona.

## Nota sobre rutas

El `index.html` usa rutas relativas del tipo `./assets/...`, por lo que puede funcionar tanto en una página raíz como en una página de proyecto de GitHub Pages.

