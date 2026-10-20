# AntiConvocatorIA

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22171162.svg)](https://doi.org/10.5281/zenodo.22171162)

**Aplicación:** https://fborrasumh.github.io/anticonvocatoria/

Contramedida docente de [ConvocatorIA](https://fborrasumh.github.io/convocatoria/). La tesis: **la respuesta correcta a un predictor de exámenes no es el secretismo, sino publicar el plan de muestreo.** Si las reglas del sorteo son públicas, la predicción deja de dar ventaja y estudiar todo el temario pasa a ser la estrategia racional. El examen es imprevisible; la serie es exhaustiva.

Aplicación de un solo fichero (`index.html`), sin servidor.

**Idiomas:** español (por defecto), inglés y portugués, con selector en la barra superior (o `?lang=en` / `?lang=pt` en la URL). La IA responde en el idioma elegido; el examen y la carta pueden redactarse además en otra variante (español latinoamericano, portugués de Brasil, catalán, valenciano, gallego, euskera…).

## Novedades de la versión 3.0

- Rediseño con la línea **Forja** de *Herramientas IA para la academia*: portada con autoría y ORCID, «Dónde va cada cosa», ayuda y navegación unificadas.
- **Tres idiomas** completos (interfaz, ejemplo, informes, examen y carta).
- **Tres proveedores de IA** con la clave de cada persona: OpenAI, Google Gemini y Anthropic Claude, con desplegable de los modelos disponibles en la clave.
- **La IA propone, el código comprueba**:
  - cada vez que la IA dice que un tema cayó en un examen aporta un fragmento literal de la pregunta, y el código lo busca en ese examen (si no aparece, la celda se marca con ⚠); lo mismo en la validación ciega;
  - el código cuenta por su cuenta las preguntas numeradas de cada examen y avisa si el recuento de la IA o su clasificación por niveles cognitivos no cuadra;
  - en la tabla de especificaciones, el código empareja los temas por nombre, rellena los que la IA omita, normaliza los niveles a 100 y descarta los códigos de resultados de aprendizaje que no estén en la lista del profesorado;
  - en el examen, tema, nivel y puntos los pone el sorteo, no la IA; el código revisa que las preguntas de test tengan opciones y una letra correcta que exista, y que no falten preguntas ni variantes;
  - la semilla no se envía nunca a la IA y, si apareciera en la carta, el código la borra.
- **Aviso previo al envío** con una muestra de lo que sale, y enmascarado de correos, teléfonos y documentos de identidad.
- Word generado en el propio navegador (sin librerías externas: funciona sin conexión y con bloqueadores), CSV, Markdown y JSON.
- **Compatibilidad**: el núcleo del sorteo no ha cambiado; los paquetes de verificación publicados con la versión 2 se siguen verificando, y los análisis guardados en el navegador con la versión 2 se recuperan solos.

## Cómo funciona

1. **Asignatura**: temario y resultados de aprendizaje (se pueden importar de SyllabusAI), número de preguntas, nota máxima según el país y ciclo de cobertura.
2. **Diagnóstico (opcional)**: con los exámenes anteriores, el mismo motor que ConvocatorIA calcula la previsibilidad de tu examen, la valida a ciegas con 3 exámenes o más (puntuación de habilidad de Brier frente a contar frecuencias), señala los temas que el estudiantado ya ha dejado de estudiar y estima la exigencia cognitiva histórica.
3. **Tabla de especificaciones**: peso de cada tema y reparto entre niveles cognitivos, derivada de los resultados de aprendizaje (no de lo que ha caído). Todas las celdas son editables.
4. **Sorteo (sin IA)**: las preguntas se sortean de la tabla con rotación (los temas olvidados ganan probabilidad), cierre del ciclo de cobertura, control de la exigencia y bucle adversario frente al predictor. Se publica antes una huella SHA-256 y después la semilla de 128 bits; cualquiera lo comprueba en «Ayuda → Verificar un sorteo». Los puntos suman exactamente la nota máxima.
5. **Examen**: cada pregunta sorteada se redacta como una familia de variantes equivalentes, de las que salen los modelos A, B, C (Word para estudiantes y versión del profesor con soluciones).
6. **Carta y publicación**: carta al estudiantado (tú, vos, ustedes o usted), documento público con tabla, regla y huella, paquete de verificación para después del examen y registro del examen aplicado en el ciclo.

El botón **Ver un ejemplo completo** recorre todo el flujo con exámenes ficticios de Bioestadística, en el idioma elegido, sin clave y sin usar la IA.

## Cómo se usa la IA

Con la propia clave de OpenAI, Google Gemini o Anthropic Claude (botón «IA»). La clave se guarda solo en el navegador (la de OpenAI se comparte con el resto del catálogo como `ia_openai_key`). El diagnóstico hace unas 7 llamadas; la tabla, el examen y la carta, una o pocas más. El sorteo y la verificación no usan la IA.

## Privacidad

Los exámenes se leen en el navegador (pdf.js y mammoth.js se cargan desde cdnjs, con jsDelivr de respaldo, solo cuando hacen falta) y todo se guarda en IndexedDB de ese navegador. Al usar la IA, el temario, los resultados de aprendizaje y el texto de los exámenes se envían al proveedor elegido, con correos, teléfonos y documentos de identidad enmascarados; antes del primer envío de la sesión se muestra una muestra. La semilla del sorteo nunca sale del navegador hasta que tú publicas el paquete de verificación. La política de seguridad de contenidos (CSP) solo permite conexiones con los tres proveedores.

## Límites

- Con menos de 3 exámenes no hay validación ciega: la previsibilidad es descriptiva.
- Los PDF escaneados necesitan OCR antes; los `.doc` antiguos y los RTF se convierten de forma aproximada.
- La IA puede etiquetar mal una pregunta: una cita localizada no garantiza que el tema asignado sea el correcto. El recuento del código solo funciona con preguntas numeradas al principio de línea.
- Las preguntas redactadas por la IA son un borrador: revísalas siempre. La responsabilidad del examen es del profesorado.
- La huella prueba que el sorteo no se cambió después de publicarla; no prueba que la tabla publicada sea buena.
- Probada con IA simulada (OpenAI, Gemini y Claude) en Chromium de escritorio y móvil; no con claves reales en esta versión.

## Motor compartido

El diagnóstico usa el mismo motor que [ConvocatorIA](https://fborrasumh.github.io/convocatoria/) 3: el profesorado se mide contra el predictor real que tiene su estudiantado.

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche) · ORCID [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573)

## Cómo citar

Borrás Rocher, F. (2026). *AntiConvocatorIA* (versión 3.0.0) [Software]. Universidad Miguel Hernández de Elche. https://doi.org/10.5281/zenodo.22171162

El DOI anterior es el de concepto: apunta siempre a la última versión. El DOI de cada versión concreta está en [Zenodo](https://doi.org/10.5281/zenodo.22171162). GitHub ofrece la cita en formato APA y BibTeX con el botón *Cite this repository*, a partir de `CITATION.cff`.

Forma parte del catálogo [Herramientas IA para la academia](https://fborrasumh.github.io/ia/).

## Licencia

MIT © 2026 Fernando Borrás Rocher · Universidad Miguel Hernández de Elche. Véase [LICENSE](LICENSE).
