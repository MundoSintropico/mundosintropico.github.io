# Zoom Infinito: Patrones de esclavitud

Dashboard interactivo de investigación histórica y prospectiva sobre patrones de control social, dependencia no libre y transformación de la esclavitud desde el Neolítico hasta escenarios contemporáneos y futuros vinculados a internet, algoritmos, deuda, moneda FIAT, vigilancia digital, CBDCs, escasez energética y control climático.

La aplicación permite navegar una línea temporal amplia, filtrar por sistemas históricos, explorar métricas comparativas, consultar fichas dinámicas por época y recorrer una vista narrativa de hipótesis de investigación.

## Descripción breve para GitHub

Dashboard interactivo sobre patrones históricos y futuros de esclavitud, deuda, control social, vigilancia digital y esclavitud climática.

## About sugerido

**Zoom Infinito: Patrones de esclavitud** es un dashboard interactivo de investigación histórica y prospectiva que explora la evolución de los sistemas de control social desde el Neolítico hasta escenarios contemporáneos de vigilancia digital, deuda, CBDCs, escasez energética y esclavitud climática. Incluye timeline navegable, filtros por sistema histórico, métricas comparativas, ficha dinámica por época y vista narrativa basada en hipótesis documentadas.

## Topics sugeridos

```text
history
slavery
social-control
surveillance-capitalism
digital-feudalism
cbdc
climate-change
debt
fiat-money
react
typescript
dashboard
```

## Demo

Este repositorio está preparado para publicarse directamente con GitHub Pages. El archivo principal es `index.html` y los recursos compilados están en la carpeta `assets/`.

## Funcionalidades principales

- **Timeline navegable**: recorrido desde el Neolítico hasta escenarios 2050.
- **Zoom temporal**: control del año central y de la ventana visible.
- **Filtros por sistema**: Mesopotamia, Egipto, Grecia, Roma, China, feudalismo, Revolución Industrial, Estado fiscal, FIAT, internet, vigilancia, CBDC y clima.
- **Ficha activa dinámica**: la ficha de consulta rápida cambia según el foco temporal o la selección manual del usuario.
- **Vista narrativa**: doce hipótesis que conectan excedente, deuda, Estado, esclavitud, servidumbre, salario, FIAT, vigilancia digital y esclavitud climática.
- **Métricas comparativas**: porcentaje de población esclava estimada, dependencia no libre, intensidad de control y métodos dominantes.
- **Exportación**: descarga de datos visibles en CSV.
- **Modo claro y oscuro**: interfaz adaptada a lectura prolongada y análisis visual.

## Estructura del repositorio

```text
.
├── index.html
├── assets/
│   ├── index-CGB4zahh.css
│   └── index-DOtacNPI.js
├── README.md
├── DOCUMENTACION_TECNICA.md
├── DEPLOY_GITHUB_PAGES.md
├── .gitignore
└── .nojekyll
```

## Despliegue rápido en GitHub Pages

1. Crea un nuevo repositorio en GitHub.
2. Sube todos los archivos de esta carpeta a la raíz del repositorio.
3. En GitHub, entra en `Settings > Pages`.
4. En `Build and deployment`, selecciona:
   - Source: `Deploy from a branch`
   - Branch: `main`
   - Folder: `/docs`
5. Guarda la configuración.
6. Espera a que GitHub Pages publique el sitio.

Esta versión del paquete ya está organizada para publicar desde `/docs`.

## Documentación técnica

La explicación completa del desarrollo está en:

`DOCUMENTACION_TECNICA.md`

Ese documento incluye objetivos, arquitectura, stack, modelo de datos, capas históricas, decisiones de diseño, metodología, fuentes, QA, limitaciones y mejoras futuras.

## Stack original de desarrollo

La app fue desarrollada como una aplicación web moderna con:

- React
- TypeScript
- Vite
- Tailwind CSS
- shadcn/ui
- Recharts

Este repositorio contiene la versión estática compilada, lista para publicar sin instalar dependencias.

## Uso local

Puedes abrir `index.html` directamente en un navegador moderno. Para una prueba más fiel al entorno de producción, se recomienda servir la carpeta con un servidor local:

```bash
python3 -m http.server 8080
```

Después abre:

```text
http://localhost:8080
```

## Licencia sugerida

Contenido y código preparados para publicación privada o pública según la decisión de la autora. Si se desea abrir el proyecto, se recomienda añadir una licencia explícita, por ejemplo MIT para el código y Creative Commons para el contenido de investigación.
