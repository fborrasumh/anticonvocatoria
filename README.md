# AntiConvocatorIA

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22171162.svg)](https://doi.org/10.5281/zenodo.22171162)

**Aplicación:** https://fborrasumh.github.io/anticonvocatoria/

Contramedida docente de [ConvocatorIA](https://fborrasumh.github.io/convocatoria/). La tesis: **la respuesta correcta a un predictor de exámenes no es el secretismo, sino publicar el plan de muestreo.** Si las reglas del sorteo son públicas, la predicción deja de dar ventaja y estudiar todo el temario pasa a ser la estrategia racional. El examen es imprevisible; la serie es exhaustiva.

Aplicación de un solo fichero (`index.html`), sin servidor.

## Novedades de la versión 2.0

- Interfaz guiada con el estilo de Forja y un ejemplo completo que funciona sin clave.
- **Sorteo verificable sin filtraciones.** Antes del examen se publica una huella SHA-256 y después la semilla, de 128 bits aleatorios. Cualquiera puede comprobarlo con el paquete de verificación dentro de la app. La versión 1 publicaba la semilla en la carta, lo que permitía reproducir el examen antes de hacerlo.
- **Predictor proporcional al temario.** Usa el 30 % de temas más probables, en vez de un top-5 fijo. El bucle adversario compara con lo que la tabla ya justifica por peso, de modo que no penaliza los temas nucleares.
- **Ventaja del predictor** frente a la simple frecuencia (puntuación de habilidad de Brier).
- **Los puntos suman exactamente la nota máxima.** Está comprobado en 15.000 sorteos; la versión 1 podía sumar, por ejemplo, 10,75 sobre 10.
- **Modelos A, B, C…** a partir de las familias de ítems, exportables a Word para el estudiantado y para el profesorado.
- **Escalas de nota por país**, carta con tú, vos, usted o ustedes, e importación desde SyllabusAI.

## Motor compartido

El diagnóstico usa el mismo motor que ConvocatorIA (`calcularMatriz`, `motorMatriz`, `motorProbabilidad`, `validacionCiega`). El profesorado se mide contra el predictor real que tiene su estudiantado.

## Privacidad

La clave se guarda en `localStorage` (`ia_openai_key`, la misma que ConvocatorIA) y solo viaja a la API del modelo. Exámenes, tablas y sorteos se guardan en IndexedDB del navegador. El sorteo y su verificación no usan la IA.

## Cómo citar

Borrás Rocher, F. (2026). *AntiConvocatorIA* (versión 2.0.0) [Software]. Universidad Miguel Hernández de Elche. https://doi.org/10.5281/zenodo.22171162

El DOI anterior es el de concepto: apunta siempre a la última versión. El DOI de cada versión concreta está en [Zenodo](https://doi.org/10.5281/zenodo.22171162). GitHub ofrece la cita en formato APA y BibTeX con el botón *Cite this repository*, a partir de `CITATION.cff`.

Forma parte del catálogo [Herramientas IA para la academia](https://fborrasumh.github.io/ia/).

## Licencia

MIT © 2026 Fernando Borrás Rocher · Universidad Miguel Hernández de Elche.
