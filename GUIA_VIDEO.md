# Defensa individual — Q11 y Q23

**David Rodríguez Fragoso · A01748760 · TC6035**

La hoja oficial `video-assignments.pdf`, fechada el 27 de octubre de 2026, asigna a A01748760 **Q11 y Q23** (tabla de la página 2). Debes decir ambos números al inicio, responder solo esas dos preguntas, usar tus propias figuras/resultados y durar como máximo cinco minutos. La asignación ya está hecha: el documento dice que no hay nada que ejecutar para elegir preguntas. Esta guía sustituye el recorrido general anterior.

## Recorrido sugerido — 4:55

| Tiempo | Contenido | Mostrar |
|---|---|---|
| 0:00–0:15 | Nombre, matrícula y «respondo Q11 y Q23». | Identification. |
| 0:15–2:20 | Q11: predicción primero y justificación teórica después. | M2: Deterministic coefficient stability, fórmula y coeficientes. |
| 2:20–4:40 | Q23: ranking observado, experimento de transferencia y resultado que cambiaría su alcance. | M3: tabla global, curva ampliada y diferencias SA−híbrido. |
| 4:40–4:55 | Cierre: alcance de la evidencia y siguiente comprobación. | Analysis o tabla global. |

Practica el recorrido con cronómetro. Los tiempos son una ayuda de preparación, no un requisito adicional del curso.

## Q11 — Subir la inercia de PSO a 0.95

**Pregunta oficial:** “What happens to your PSO if you raise w to 0.95? Predict it first, then justify the prediction from theory rather than from having tried it.”

### Predicción que debe ir primero

«Predigo que el movimiento conservaría más de su velocidad anterior y que las oscilaciones se amortiguarían más lentamente. Con nuestros coeficientes seguiría dentro de la región estable del modelo determinista. No puedo asegurar que mejore el objetivo final: eso requeriría otro experimento, que no estoy usando para justificar esta predicción.»

### Justificación con tu configuración

Los coeficientes son **w = 0.7, c1 = c2 = 1.4**, de modo que **phi = c1+c2 = 2.8**. La región estudiada en M2 exige:

\[
0\le w<1,\qquad 0<\varphi<2(1+w).
\]

| Caso | Inercia w | phi | Cota 2(1+w) | Dentro de la región del modelo |
|---|---:|---:|---:|---|
| Configuración utilizada | 0.70 | 2.8 | 3.4 | Sí |
| Cambio hipotético de Q11 | 0.95 | 2.8 | 3.9 | Sí |

En el término de inercia, **0.7 v** pasaría a **0.95 v** antes de sumar las atracciones y aplicar límites. Esto retiene más movimiento previo; c1 y c2 no cambian.

La recurrencia de desplazamiento respecto a una referencia fija que ya explicaste en M2 es:

\[
x_{k+1}=(1+w-\varphi)x_k-wx_{k-1}.
\]

Que el desplazamiento tienda a cero significa acercarse a la referencia, no apagar los sensores ni llevar sus potencias a cero.

### Apoyo teórico opcional para una explicación más precisa

La ecuación característica es **lambda² − (1+w−phi)lambda + w = 0**. En estos dos casos sus raíces son complejas conjugadas y el producto de ambas es w. Por eso el módulo de cada una es **sqrt(w)**:

- Con w=0.7, el módulo es aproximadamente **0.83666**.
- Con w=0.95, es aproximadamente **0.97468**.

Ambos módulos son menores que uno: el modelo sigue amortiguando. El segundo está más cerca de uno, por lo que decae más lentamente. Esta conclusión sale del análisis de la recurrencia, no de haber corrido PSO con w=0.95. No hace falta leer las raíces complejas completas en el video.

### Guion breve para adaptar

«Mi PSO usa inercia 0.7 y coeficientes cognitivo y social de 1.4. Primero mi predicción: subir la inercia a 0.95 mantendría más movimiento previo y amortiguaría las oscilaciones más lentamente. No predigo divergencia obligatoria ni una mejor solución final.

La condición estudiada exige w menor que uno y que la suma de los coeficientes sea menor que dos por uno más w. Nuestra suma es 2.8. Con w=0.95, la cota sube a 3.9 y 0.95 sigue siendo menor que uno: permanece dentro de esa región.

Sin embargo, estar dentro de la región no significa amortiguar igual de rápido. En nuestra recurrencia de desplazamiento, el módulo de las raíces pasa de aproximadamente 0.837 a 0.975. Al acercarse a uno, el movimiento decae más lentamente.

Esto corresponde a una referencia fija en un modelo determinista. El PSO real cambia sus memorias, incorpora factores aleatorios y limita velocidad y potencias. Por eso esta teoría no garantiza convergencia del optimizador real, optimalidad ni una ganancia de desempeño. No ejecuté la variante 0.95 para justificar la respuesta.»

## Q23 — Comprobar si el ranking se transfiere

**Pregunta oficial:** “Your ranking rests on the problem you ran it on. Name the experiment that would test whether it transfers, and say what result would change your conclusion.”

### Evidencia que sí tienes

En la instancia A01748760, el orden de medianas fue **SA > híbrido > tabú > ACO > Monte Carlo > PSO sobre subconjunto fijo**. El ranking no describe todos los posibles parámetros ni subconjuntos de PSO.

- SA: mediana **0.714655**.
- Híbrido: mediana **0.704544**.
- SA ganó **25/30** semillas; el híbrido ganó cinco.
- Mediana emparejada SA−híbrido: **+0.009575**.
- Wilcoxon con Holm para esa pareja: **p=0.00256**; efecto rank-biserial **+0.612903**.

Estos números respaldan la comparación en esa instancia y condiciones, no la transferencia a otras.

### Experimento propuesto, todavía no ejecutado

1. Elegir antes de correr varias instancias nuevas de la misma familia, con geometría, demanda y límites de potencia diferentes. No elegirlas por favorecer el ranking actual.
2. Congelar las seis configuraciones: misma política de inicialización de cada método, PSO ring y reparto 40/60 del híbrido. La regla de subconjunto fijo de PSO también se conserva; no se selecciona un subconjunto mejor después de ver resultados.
3. Usar 30 semillas de evaluación nuevas, pareadas entre los métodos, y 5,000 llamadas por método y corrida, con todo el híbrido dentro de ese total.
4. Comparar dentro de cada instancia medianas, IQR, rangos y diferencias emparejadas, con pruebas y tamaños de efecto. Definir previamente la familia de contrastes y la corrección por comparaciones múltiples.
5. Examinar si el orden se sostiene entre instancias. No tratar todas las semillas de distintos problemas como si fueran observaciones intercambiables de una sola instancia. Una evaluación del ranking entre problemas debe usar la instancia como unidad de comparación.

Si decidieras reajustar parámetros para cada instancia, sería otro experimento: tendría que separar semillas de ajuste y evaluación y cobrar ese costo. No sería una transferencia directa de las configuraciones congeladas.

### Qué resultado cambiaría el alcance de la conclusión

Una **reversión consistente de SA frente al híbrido en nuevas instancias**, con diferencias emparejadas favorables al híbrido y evidencia estadística, impediría extender la ventaja observada de SA a esa familia. La conclusión pasaría a depender de propiedades de las instancias. Un cambio de otras posiciones también cuestionaría la transferencia del ranking completo.

Un resultado no significativo exigiría prudencia y quizá más evidencia: no demostraría equivalencia. Tampoco borraría lo medido en A01748760; lo que se pondría a prueba es la extensión de ese resultado a otros problemas.

### Guion breve para adaptar

«Mi ranking proviene de una sola instancia. SA obtuvo mediana 0.714655 y el híbrido 0.704544. SA ganó 25 de las 30 semillas y la comparación emparejada siguió siendo significativa después de Holm. Esto apoya la ventaja observada en esta instancia, pero aún no demuestra transferencia.

Para comprobarla elegiría varias instancias nuevas de la misma familia antes de ver sus resultados. Mantendría congelados los parámetros de los seis métodos, incluido el reparto 40/60, y ejecutaría 30 semillas nuevas y compartidas entre métodos, con 5,000 evaluaciones por corrida. Así examinaría la transferencia de nuestras configuraciones, en vez de volver a ajustarlas para cada problema.

Compararía los resultados dentro de cada instancia y después la estabilidad de los rangos entre instancias. Mostraría dispersión, diferencias emparejadas y tamaños de efecto, además de las pruebas con corrección por comparaciones múltiples.

Cambiaría el alcance de mi conclusión si el híbrido superara consistentemente a SA en otras instancias con evidencia emparejada. Eso no eliminaría la ventaja medida de SA aquí, pero mostraría que depende del problema. Si no hubiera una diferencia clara, tampoco afirmaría empate. No Free Lunch refuerza el límite de una afirmación universal bajo sus supuestos, pero son estos nuevos experimentos los que comprobarían la transferencia en nuestra familia de problemas.»

## Antes de grabar

- Di **Q11 y Q23** al inicio; no hace falta sortear ni escoger otras preguntas.
- No ejecutes PSO con w=0.95 para construir la justificación: Q11 exige la predicción teórica.
- Abre M2 en la fórmula de estabilidad y M3 en la tabla/gráfica global. Mantén visibles tus propios resultados.
- Habla con tus palabras; las fórmulas y cifras respaldan la explicación, no deben convertirse en una lectura apresurada.
- Graba menos de cinco minutos, revisa audio y legibilidad y publica el enlace con acceso para el profesor.
- Pega el enlace real en `# Video`. Añadirlo no requiere repetir los experimentos.
