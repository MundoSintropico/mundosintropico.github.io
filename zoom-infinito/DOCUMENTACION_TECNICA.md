# Zoom Infinito: Patrones de esclavitud, deuda, FIAT, algoritmos y clima

Documento técnico y metodológico del dashboard interactivo desarrollado para explorar patrones históricos y prospectivos de coerción social, desde el Neolítico hasta escenarios contemporáneos y futuros asociados a Internet, capitalismo de vigilancia, CBDCs, carbono y escasez energética.

## Resumen del proyecto

**Zoom Infinito** es una aplicación web interactiva construida como dashboard de investigación. Su objetivo es permitir una consulta rápida, visual y narrativa de distintas formas de coerción humana y social a lo largo del tiempo: esclavitud formal, servidumbre, deuda, tributación estatal, salario disciplinado, dinero fiduciario, vigilancia digital, dinero programable y control climático del consumo.

La aplicación no plantea que todas estas capas sean equivalentes. Distingue entre:

- **Capas históricas**: Neolítico, Mesopotamia, Egipto, Grecia, Roma, China, Feudalismo, Revolución Industrial.
- **Capas institucionales**: nacimiento del Estado fiscal, deuda, FIAT.
- **Capas contemporáneas/prospectivas**: Internet, capitalismo de vigilancia, CBDCs, feudalismo digital, escasez energética y esclavitud climática.

Cada sistema se presenta con rangos estimativos, métodos de control, nivel de confianza y fuentes documentales.

## Objetivos funcionales

La app se diseñó para cumplir estos objetivos:

- **Explorar una línea temporal amplia**: desde aproximadamente 9000 a. C. hasta 2050.
- **Filtrar por sistemas históricos y prospectivos**: Neolítico, Mesopotamia, Estado fiscal, Egipto, Grecia, Roma, China, Feudalismo, Industrial, FIAT, Internet, Vigilancia, CBDC y Clima.
- **Comparar intensidad de coerción**: usando dos métricas principales, porcentaje de población esclava y dependencia no libre.
- **Visualizar métodos de control social**: deuda, mercado, guerra, ley, salario, datos, algoritmo, CBDC, carbono, energía, etc.
- **Consultar rápidamente cualquier época**: la ficha activa cambia dinámicamente según el año central seleccionado.
- **Navegar por una narrativa de investigación**: 12 capítulos interpretativos conectados al timeline.
- **Exportar datos**: descarga en CSV y copia de síntesis textual.
- **Distinguir niveles de confianza**: cada sistema incluye una confianza alta, media o baja según la solidez histórica o el carácter prospectivo.

## Stack tecnológico

La aplicación está desarrollada como una web app React moderna.

- **Frontend**: React + TypeScript.
- **Bundler**: Vite.
- **UI**: Tailwind CSS + componentes shadcn/ui.
- **Gráficos**: Recharts.
- **Routing**: Wouter con hash routing para compatibilidad con despliegues embebidos.
- **Iconografía**: Lucide React.
- **Estado**: React state local.
- **Persistencia**: no usa localStorage, sessionStorage, cookies ni base de datos.
- **Build**: `npm run build`.
- **Typecheck**: `npm run check`.

## Estructura conceptual de datos

La unidad principal de análisis es un `Pattern`, que representa una etapa, sistema o capa de control social.

Campos principales:

```ts
type Pattern = {
  id: string;
  empire: Empire;
  label: string;
  start: number;
  end: number;
  slaveRange: [number, number];
  unfreeRange: [number, number];
  confidence: "Alta" | "Media" | "Baja";
  control: string[];
  transition: string;
  note: string;
  sourceIds: string[];
  color: string;
};
```

### Sistemas incluidos

| Sistema | Rango temporal | Interpretación |
|---|---:|---|
| Neolítico | 9000-3500 a. C. | Agricultura temprana, cautiverio, excedente y violencia organizada. |
| Mesopotamia | 3500-539 a. C. | Deuda, contratos, palacio-templo y dependencia familiar. |
| Estado fiscal | 3300-1200 a. C. | Nacimiento del Estado como máquina de cuenta, censo, archivo y tributo. |
| Egipto | 3100-332 a. C. | Corvea estatal, fisco, prisioneros y trabajo obligatorio. |
| Grecia | 800-146 a. C. | Ciudadanía, esclavitud extranjera, minas, mercado y domesticidad. |
| Roma | 509 a. C.-476 d. C. | Conquista, ley, mercado, latifundio y manumisión. |
| China | 221 a. C.-220 d. C. | Esclavitud penal, burocracia, clan y servidumbre doméstica. |
| Feudalismo | 800-1500 d. C. | Servidumbre territorial, renta, herencia y jurisdicción señorial. |
| Industrial | 1600-1914 d. C. | Plantación, algodón, fábrica, salario, colonia y deuda. |
| FIAT | 1690-1971 d. C. | Deuda pública, banco central, inflación, salario y soberanía monetaria. |
| Internet | 1991-2050 d. C. | Captura de atención, datos, plataformas y modulación algorítmica. |
| Vigilancia | 2007-2050 d. C. | Capitalismo de vigilancia, nube, reputación y feudalismo digital. |
| CBDC | 2020-2050 d. C. | Dinero programable, identidad digital, privacidad y autorización de gasto. |
| Clima | 2020-2050 d. C. | Escasez energética, carbono, racionamiento, movilidad y consumo. |

## Métricas

La aplicación usa dos métricas comparativas:

### Porcentaje de población esclava

Representa el rango estimado de población sometida a esclavitud formal o formas equivalentes de propiedad directa sobre personas, cuando aplica históricamente.

### Dependencia no libre

Representa un rango más amplio de subordinación no libre o semilibre:

- servidumbre,
- corvea,
- deuda,
- dependencia territorial,
- trabajo semicoaccionado,
- control salarial,
- dependencia algorítmica,
- restricciones por permisos energéticos o de carbono.

En capas prospectivas como CBDC, vigilancia o clima, esta métrica se usa como **indicador conceptual de dependencia sistémica**, no como dato demográfico cerrado.

## Ficha activa dinámica

Uno de los cambios finales más importantes fue reemplazar la ficha fija inicial por una ficha dinámica.

Antes, la app cargaba Roma como ficha activa por defecto. Esto generaba una lectura sesgada, porque el dashboard ya no trata solo de la Antigüedad.

Ahora la ficha activa se calcula según:

1. El año central seleccionado en el navegador temporal.
2. Los sistemas visibles dentro de la ventana de zoom.
3. Los filtros activos.
4. La búsqueda textual.
5. La duración y cercanía temporal de cada sistema.

### Regla de selección automática

La función `pickPatternForYear` prioriza:

1. Sistemas que contienen el año consultado.
2. Entre sistemas que contienen el año, el más cercano al centro de su propio periodo.
3. Si hay empate, el de menor duración, porque suele ser más específico.
4. Si aún hay empate, el más reciente.

Esto permite consultas rápidas:

- Año 2040: muestra “Escasez energética, carbono y esclavitud climática”.
- Año 1000: muestra “Servidumbre territorial europea”.
- Año 1780: muestra “Plantación, fábrica y salario disciplinado”.
- Año -450: muestra “Atenas como sociedad esclavista”.

### Modo manual

Si el usuario pulsa una barra, tarjeta o capítulo narrativo, la app respeta esa selección y enfoca el timeline en esa etapa.

Los sliders y filtros vuelven a activar el modo automático.

## Timeline y zoom temporal

El timeline muestra los sistemas que cruzan la ventana temporal activa. Las barras se recortan al borde de la ventana, lo que permite visualizar sistemas largos sin perder el foco del periodo consultado.

Ejemplo:

- Si la ventana es 1800 a. C. a 800 d. C., Mesopotamia y Egipto aparecen recortados en el borde izquierdo porque empezaron antes de la ventana visible.

El eje temporal usa tres ticks lineales:

- inicio de ventana,
- centro real de ventana,
- final de ventana.

Esto evita interpretaciones erróneas cuando la ventana cruza el año 0.

## Vista narrativa de investigación

La aplicación incluye una vista narrativa con 12 hipótesis. Cada capítulo contiene:

- título,
- periodo,
- tesis,
- indicios de lectura,
- pregunta de investigación,
- botón para enfocar el timeline en ese capítulo.

### Capítulos incluidos

1. Del excedente al cautiverio.
2. La deuda como captura social.
3. Nacimiento del Estado como ente de control.
4. Ciudadanía para unos, esclavitud para otros.
5. Imperio, mercado y manumisión.
6. El cuerpo se ata a la tierra.
7. Plantación, fábrica y salario.
8. FIAT, deuda pública y Estado monetario.
9. Internet y captura de atención.
10. Capitalismo de vigilancia y feudalismo digital.
11. CBDC, identidad y consumo programable.
12. Escasez energética y esclavitud climática.

## Métodos de control social

La app agrega métodos de control en una visualización lateral de intensidad.

Ejemplos:

- captura,
- excedente,
- deuda,
- tributo,
- censo,
- archivo,
- corvea,
- mercado,
- ciudadanía,
- ley,
- guerra,
- manumisión,
- tierra,
- renta,
- salario,
- colonia,
- FIAT,
- impuesto,
- banco central,
- inflación,
- atención,
- algoritmo,
- datos,
- plataforma,
- reputación,
- CBDC,
- identidad digital,
- carbono,
- energía,
- racionamiento,
- movilidad.

La intensidad se calcula de forma agregada según los sistemas visibles y la métrica activa.

## Exportación

La app permite:

- **Copiar síntesis**: genera un resumen textual de los sistemas visibles.
- **Exportar CSV**: descarga los datos filtrados con campos clave:
  - sistema,
  - inicio,
  - fin,
  - rango de esclavitud,
  - rango de dependencia no libre,
  - confianza,
  - métodos de control.

## Fuentes documentales

Las fuentes se agrupan dentro de la app y se muestran dinámicamente según los sistemas visibles.

### Fuentes históricas

- Britannica, Slave societies: https://www.britannica.com/topic/slavery-sociology/Slave-societies
- Britannica, Serfdom: https://www.britannica.com/summary/serfdom
- EH.net, The Economy of Ancient Greece: https://eh.net/encyclopedia/the-economy-of-ancient-greece/
- ANE Today, Rethinking Slavery in the Ancient Near East: https://anetoday.org/rethinking-slavery/
- UCLA Encyclopedia of Egyptology, Slavery and Servitude: https://escholarship.org/uc/item/8mx2073f
- Cambridge, Industrial Slavery in China During the Former Han Dynasty: https://www.cambridge.org/core/journals/journal-of-economic-history/article/industrial-slavery-in-china-during-the-former-han-dynasty-206-bcad-25/0B268B57193E3634DA61B8DEEBA38213
- ChinaKnowledge, nuli 奴隸: http://www.chinaknowledge.de/History/Terms/nuli.html
- PNAS, Early Neolithic massacre: https://pmc.ncbi.nlm.nih.gov/articles/PMC4568710/

### Deuda, Estado y FIAT

- Michael Hudson, Palatial Credit: https://michael-hudson.com/2018/04/palatial-credit-origins-of-money-and-interest/
- David Graeber, debt, slavery and freedom: https://davidgraeber.org/interviews/debt-slavery-and-our-idea-of-freedom/
- Oxford Academic, Currency-Slavery-Warfare Complex: https://academic.oup.com/book/44452/chapter/376382617
- Cobden Centre, Massachusetts 1690 fiat experiment: https://www.cobdencentre.org/2026/03/massachusetts-1690-the-first-western-fiat-experiment/

### Revolución Industrial y trabajo semicoaccionado

- History Workshop, slavery and industrial capitalism: https://www.historyworkshop.org.uk/empire-decolonisation/slavery-coerced-labour-and-the-development-of-industrial-capitalism-in-britain/
- CEPR, Slavery and the British Industrial Revolution: https://cepr.org/voxeu/columns/slavery-and-british-industrial-revolution
- OpenStax, Coerced and Semicoerced Labor: https://openstax.org/books/world-history-volume-2/pages/10-3-coerced-and-semicoerced-labor
- Cambridge, Debt Peonage in the Cotton South: https://www.cambridge.org/core/journals/journal-of-economic-history/article/debt-peonage-in-the-cotton-south-after-the-civil-war/03FABDF28A33D1673365CD08B5CBDE42

### Internet, vigilancia, tecnofeudalismo y algoritmos

- Harvard Gazette, surveillance capitalism: https://news.harvard.edu/gazette/story/2019/03/harvard-professor-says-surveillance-capitalism-is-undermining-democracy/
- Harvard Business School, The Age of Surveillance Capitalism: https://www.hbs.edu/faculty/Pages/item.aspx?num=56791
- Georgetown Law, attention economy: https://www.law.georgetown.edu/denny-center/blog/the-attention-economy/
- Yanis Varoufakis, Technofeudalism review: https://www.yanisvaroufakis.eu/2024/04/01/technofeudalism-reviewed-by-geert-lovink/
- AI Now Institute, algorithmic management: https://ainowinstitute.org/publications/algorithmic-management

### CBDCs, carbono y clima

- BIS, privacy and security for CBDCs: https://www.bis.org/publ/othp80.pdf
- European Data Protection Supervisor, CBDC: https://www.edps.europa.eu/system/files/2023-03/23-03-29_techdispatch_cbdc_en.pdf
- Tyndall Centre, personal carbon trading: https://tyndall.ac.uk/wp-content/uploads/2021/11/twp136.pdf
- Taylor & Francis, rationing and climate mitigation: https://www.tandfonline.com/doi/full/10.1080/21550085.2023.2166342
- Anthropocene Magazine, personal carbon accounts: https://www.anthropocenemagazine.org/conservation/2008/07/personal-carbon-accounts/

## Metodología y limitaciones

Este dashboard es una herramienta de investigación visual, no una base estadística definitiva.

### Limitaciones principales

- Las cifras antiguas son aproximadas y dependen de fuentes fragmentarias.
- Los conceptos de esclavitud, servidumbre, corvea, deuda y trabajo semicoaccionado no son idénticos.
- Las capas contemporáneas y futuras no deben interpretarse como esclavitud legal, sino como hipótesis sobre dependencia sistémica.
- FIAT, CBDCs y carbono se modelan como tecnologías institucionales de coordinación/control, no como equivalentes automáticos de esclavitud.
- El término “esclavitud climática” se usa como categoría crítica para explorar escenarios de restricción asimétrica de energía, movilidad y consumo.

### Criterio de confianza

- **Alta**: evidencia histórica relativamente sólida y categorías comparables.
- **Media**: evidencia histórica razonable, pero con diferencias regionales o conceptuales importantes.
- **Baja**: evidencia fragmentaria, capa transversal o hipótesis prospectiva.

## Instalación local

```bash
npm install
```

## Desarrollo

```bash
npm run dev
```

La app se sirve localmente en el puerto configurado por el entorno de desarrollo.

## Build de producción

```bash
npm run build
```

## Verificación TypeScript

```bash
npm run check
```

## Despliegue

La app se despliega como sitio estático desde:

```text
dist/public
```

El entry point es:

```text
index.html
```

## Accesibilidad y diseño

Decisiones implementadas:

- Interfaz responsive.
- Sin scroll horizontal en móvil.
- Modo claro/oscuro.
- Botones con `data-testid`.
- Contraste alto en tarjetas, chips y controles.
- Timeline con eje lineal.
- Textos de advertencia metodológica para evitar falsas equivalencias.
- Filtros diferenciados de sistemas visibles en ventana.

## QA realizado

Se verificó:

- Build correcto.
- TypeScript correcto.
- Filtros activos.
- Timeline extendido hasta 2050.
- Ficha activa dinámica.
- Capítulos narrativos.
- Selección manual por tarjetas, barras y capítulos.
- Reversión a modo automático al mover sliders o cambiar filtros.
- Vista móvil sin scroll horizontal.
- Exportación CSV.
- Copia de síntesis.

## Decisiones de diseño importantes

### No usar ficha fija

Se eliminó Roma como ficha fija inicial. La ficha activa ahora responde al año consultado.

### Diferenciar filtros de visibilidad

Los chips laterales son filtros activos, no una lista de sistemas necesariamente visibles. El timeline solo muestra sistemas que cruzan la ventana temporal.

### Mantener capas prospectivas separadas

Internet, Vigilancia, CBDC y Clima se incluyen como capas de investigación prospectiva con confianza baja. Esto evita presentarlas como hechos históricos cerrados.

### Evitar falsa equivalencia

La app no afirma que FIAT, CBDCs, carbono o algoritmos sean “esclavitud” en sentido jurídico. Los presenta como posibles tecnologías de dependencia, control o subordinación social.

## Posibles mejoras futuras

- Añadir modo “Bitcoin / salida del FIAT”.
- Añadir comparativa de fuentes por sistema.
- Añadir vista de red causal entre métodos de control.
- Añadir editor de datos en JSON.
- Añadir modo presentación para vídeo o clase.
- Añadir tests automatizados de UI.
- Separar datos en un archivo independiente para facilitar contribuciones en GitHub.
- Añadir licencia explícita.

## Licencia sugerida

Pendiente de definir. Recomendaciones posibles:

- MIT, si se quiere permitir reutilización amplia del código.
- Creative Commons BY-SA para el contenido metodológico.
- Doble licencia: MIT para código y CC BY-SA para contenido.

## Nota final

Este proyecto funciona como mapa de hipótesis, no como sentencia histórica definitiva. Su valor está en permitir comparar patrones de coerción social a través del tiempo, ver continuidades y rupturas, y abrir preguntas críticas sobre cómo las formas de control migran del cuerpo a la tierra, de la tierra a la deuda, de la deuda al salario, del salario al dato y del dato al carbono.
