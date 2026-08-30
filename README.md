# AntiConvocatorIA

Contramedida docente de [ConvocatorIA](https://fborrasumh.github.io/convocatoria/). Aplicación de un solo fichero (`index.html`), sin servidor ni dependencias de build.

La tesis: **la respuesta correcta a un predictor de exámenes no es el secretismo, es publicar el plan de muestreo.** Si las reglas del sorteo son públicas, la predicción deja de dar ventaja y estudiar el temario completo pasa a ser la estrategia racional. El examen es impredecible; la serie es exhaustiva.

## Motor compartido

La auditoría y el bucle adversario ejecutan **el mismo código** que ConvocatorIA: `calcularMatriz`, `motorMatriz`, `motorProbabilidad` y `validacionCiega` son idénticos. El profesor se mide contra el predictor real que tienen sus estudiantes, no contra una versión más floja.

## Los cinco módulos

1. **Auditoría de previsibilidad** — corre el predictor contra tus propios exámenes: % de preguntas que caen en su top-5, Brier score validado a ciegas, mezcla cognitiva y lista de temas que tus estudiantes ya han abandonado con razón.
2. **Tabla de especificaciones** — temas × niveles cognitivos (recordar / aplicar / analizar / evaluar) con pesos derivados de los resultados de aprendizaje, no del historial. Editable. Es lo que se publica.
3. **Sorteo con deuda de rotación** — muestreo con semilla reproducible: cada tema acumula peso mientras no sale y en un ciclo de N convocatorias todo el temario queda cubierto. El **bucle adversario** mide la previsibilidad del examen sorteado y vuelve a sortear si supera el umbral, penalizando los temas esperados. Se muestran todos los intentos.
4. **Familias de ítems** — cada celda sorteada se redacta con variantes equivalentes (mismo tema, mismo nivel, distinto estímulo), de modo que filtrar un enunciado no da ventaja.
5. **Carta al estudiante** — publica la tabla y la regla de sorteo. Sin esto, lo anterior es solo un examen sorpresa.

Salvaguardas: **control de dificultad** entre convocatorias (imprevisible no puede significar más difícil) y un **acta de sorteo** con semilla y sello, para que el sorteo sea auditable y no cherry-picking.

## Publicar en GitHub Pages

1. Sube `index.html` y `README.md` al repo `anticonvocatoria` en la rama `main`.
2. Settings → Pages → Source: `main` / `/ (root)`.

## Privacidad

La clave de la API se guarda en `localStorage` (`ia_openai_key`, la misma que ConvocatorIA) y solo viaja a la API del modelo. Exámenes, tablas y sorteos se guardan en IndexedDB del navegador.

## Licencia

MIT.
