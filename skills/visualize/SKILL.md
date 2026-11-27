---
name: visualize
description: Crea visualizaciones limpias, precisas y verificadas visualmente (gráficas matemáticas en Python/matplotlib, esquemas técnicos en SVG renderizados o diagramas Mermaid) guardadas en graficos/. Úsala siempre que una geometría, gráfica, vector, circuito, dependencia o arquitectura sea más clara en imagen que en texto.
---

# Motor Visual Verificado (VISUALIZE)

Una imagen solo merece existir si muestra algo que las palabras no pueden transmitir con igual claridad: forma, dirección, relación de dependencia, geometría o comportamiento de una función.

**La regla de oro (innegociable):** **NUNCA entregues un gráfico sin haberlo renderizado a PNG y haberlo mirado visualmente tú mismo.** Que un script ejecute sin errores o que un SVG sea válido NO demuestra que las etiquetas no se pisen, que las flechas apunten bien o que la geometría sea cierta. Un gráfico erróneo o ilegible es peor que no poner ninguno.

## 1. Cuándo visualizar (y cuándo NO)
- **SÍ:** grafos de dependencias, flujos/arquitecturas, máquinas de estados, árboles, geometría espacial, ejes de coordenadas, cinemática de robots, vectores, circuitos, curvas matemáticas, respuestas en frecuencia, simulaciones o comparativas visuales.
- **NO:** diagramas decorativos que solo repiten una frase obvia o una única ecuación simple.

## 2. Dirección creativa: UNA sola idea, los mínimos elementos
El fallo nº 1 es **abarrotar el dibujo**. Antes de escribir una línea de código:
- Destila el concepto a **una sola idea central**.
- Revisa cada etiqueta/elemento y pregúntate: *"si borro esto, ¿la idea sigue estando clara?"* Si la respuesta es sí, bórralo.
- Límite orientativo: **máximo 5–7 elementos/nodos principales**. Etiquetas cortas (términos, no párrafos).

## 3. Elegir el motor correcto (guardando todo en `graficos/`)

Crea la carpeta `graficos/` en el workspace actual si no existe, usando nombres descriptivos en *kebab-case* (ej. `graficos/robot-diferencial-icr.png`).

1. **Gráficas matemáticas, curvas, campos vectoriales, trayectorias, señales o geometría exacta con coordenadas** → **Python (`matplotlib` + `numpy`) → PNG**:
   - Usa `dpi=180`, paleta limpia de alto contraste (preferiblemente fondo oscuro elegante `#111418` con texto claro `#E6EDF3` y acentos distinguibles, o fondo blanco limpio si es para imprimir), rejilla sutil, ejes etiquetados con unidades, relación de aspecto `equal` cuando sea geometría/cinemática real, y anotaciones con flechas limpias en los puntos críticos.
   - Guarda el PNG en `graficos/<slug>.png`. Si el estudiante quiere jugar con parámetros luego (ej. cambiar $L$ o $\omega$), conserva el script en `graficos/scripts/<slug>.py` para iterar en 1 segundo.

2. **Esquemas espaciales personalizados, diagramas de bloques técnicos, cuerpos libres, robots o mecanismos** → **SVG + render a PNG para inspección**:
   - Autoría en `graficos/<slug>.svg` con `viewBox` amplio, márgenes generosos, flechas definidas (`<marker>`), tipografía sans-serif legible y cero solapamientos.
   - Renderiza ese SVG a PNG temporal o final (usando Python/Playwright, `cairosvg`, `rsvg-convert` o Chromium headless disponible en el sistema) para poder **inspeccionarlo visualmente**. Si el entorno no tiene renderizador SVG→PNG instalado, usa **Python `matplotlib.patches`** (que renderiza directamente a PNG de altísima precisión y permite inspección visual garantizada).

3. **Grafos de dependencias, flujos, arquitecturas, secuencias o máquinas de estado** → **Mermaid**:
   - Ideal para los mapas de dependencias de `teach` (`graph TD` con verdades núcleo arriba fluyendo hacia conclusiones abajo).
   - Máximo ~7 nodos, etiquetas muy cortas. Si el diagrama es complejo y quieres guardarlo en `graficos/`, renderízalo a PNG e inspecciónalo visualmente.

## 4. El bucle obligatorio de Renderizar → Mirar → Corregir

Después de generar el PNG, **abre/lee la imagen generada** y haz una auditoría crítica real:
1. **Veracidad técnica:** ¿apunta cada flecha en la dirección correcta?, ¿los ejes, signos, proporciones y dependencias son 100 % fieles a la física/matemática?
2. **Legibilidad:** ¿hay algún texto cortado en los bordes, dos etiquetas solapadas, una flecha cruzando encima de una fórmula o colores poco legibles?
3. **Claridad inmediata:** ¿entiende el estudiante la idea mirando solo la imagen sin leer un párrafo largo?

Si falla cualquier punto, **corrige el código, vuelve a renderizar y vuelve a mirar** (2-3 pasadas rápidas son normales) hasta que quede impecable.

## 5. Entrega al estudiante
1. Indica la **ruta exacta** del archivo generado en `graficos/` para que pueda abrirlo en una pestaña al lado del chat (y muéstralo/incrusta la referencia si procede).
2. Acompaña la imagen con **máximo 3 viñetas cortas** indicando qué debe mirar exactamente en el dibujo (no narres de vuelta cada elemento).
3. Si es una gráfica parametrizable, ofrece una pregunta corta del tipo: *"¿Quieres que cambiemos algún parámetro (por ejemplo, duplicar $L$ o invertir $\omega_L$) para ver cómo cambia el dibujo?"*
