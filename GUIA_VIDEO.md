# Guía para la defensa individual — David Rodríguez Fragoso, A01748760

Duración máxima: cinco minutos. Esta guía prepara la explicación; al grabar debes responder las dos preguntas que se elijan del banco oficial. No se ha localizado ese banco en el repositorio. Las preguntas de práctica de abajo no lo sustituyen.

## Recorrido sugerido: 4 minutos y 55 segundos

| Tiempo | Mostrar | Qué explicar |
|---|---|---|
| 0:00–0:20 | Identification y mapa de la instancia | Tu nombre, matrícula y el problema que resolviste. |
| 0:20–1:00 | Formulation y esquema del híbrido | Sensores y potencias acoplados; objetivo maximizado; presupuesto único de 5,000 llamadas. |
| 1:00–1:40 | Comparación global ampliada y tabla | SA y el híbrido; diferencia emparejada, evidencia estadística y alcance. |
| 1:40–2:10 | Una gráfica del mecanismo y el grid | ACO con/sin límites, o reparto 40/60, según lo que ayude a la explicación. |
| 2:10–3:25 | Evidencia pertinente del notebook | Primera pregunta elegida al grabar. |
| 3:25–4:40 | Evidencia pertinente del notebook | Segunda pregunta elegida al grabar. |
| 4:40–4:55 | Analysis y cierre | Tu contribución, limitación principal y experimento que podría cambiar la conclusión. |

Los tiempos son una referencia para practicar, no una regla adicional del curso. Las respuestas a las preguntas oficiales tienen prioridad; abre antes las secciones que necesitarás mostrar para no perder tiempo navegando.

## Base de explicación para adaptar con tus palabras

**Presentación y problema.** «Soy David Rodríguez Fragoso, A01748760. Estudié la ubicación de sensores de mi instancia: hay 80 sitios candidatos y debemos decidir cuáles activar y qué potencia asignarles. Maximizo cobertura ponderada, descontando energía, interferencia y penalizaciones por desconexión.»

**Acoplamiento y diseño.** «Las dos capas interactúan: modificar potencia cambia cobertura y conectividad, así que puede cambiar qué selección conviene. Combinamos ACO para elegir sitios con PSO ring para ajustar potencias. Ambas etapas comparten las mismas 5,000 evaluaciones. El grid comparó 40/60, 60/40 y 80/20 con 30 semillas de ajuste y eligió 40/60 por su mediana. Eso significa 2,000 llamadas para selección y 3,000 para ajuste.»

**Resultado principal.** «En las 30 semillas finales, SA obtuvo mediana 0.714655 y el híbrido 0.704544. SA ganó 25 semillas y perdió cinco. La mediana de las diferencias emparejadas fue +0.009575 a favor de SA y el p ajustado por Holm fue 0.00256. Esto respalda la ventaja de esa configuración de SA en esta instancia, no que siempre sea mejor.»

**Mecanismo.** «SA puede seguir proponiendo cambios en cualquiera de las dos capas durante la corrida; cada movimiento cambia una de ellas. En el híbrido secuencial, PSO queda condicionado al subconjunto que recibió y no puede sustituir sitios. Esa restricción es una explicación posible del resultado, pero la comparación no la aísla de todas las demás diferencias entre métodos.»

**Otra evidencia útil.** «Sin límites de feromona, la mediana final de subconjuntos distintos por iteración cayó a uno; con límites permaneció en diez. El piso de feromona conservó alternativas en esta configuración. La entropía no tiene que llegar a cero cuando todas las hormigas construyen el mismo conjunto, porque sus miembros aún pueden elegirse en distinto orden.»

**Contribución y límites.** «Participé en la interpretación y revisión de resultados, propuse discutir eficiencia del presupuesto y probar una colonia mayor, revisé el reparto entre etapas y ejecuté el notebook completo en mi venv. La asistencia de IA y sus correcciones están documentadas. No conocemos el óptimo ni demostramos transferencia a otras instancias; un seguimiento con configuraciones congeladas, semillas nuevas y otra instancia podría cambiar la conclusión.»

No leas todos estos bloques si impiden responder las preguntas oficiales dentro de los cinco minutos. Úsalos como material para ensayar respuestas breves.

## Cifras que debes distinguir

| Dato | Interpretación correcta |
|---|---|
| 30 semillas finales por método | Corridas comparadas; no 30 sensores. |
| 15 sitios por solución ACO | Cardinalidad fija de la construcción, no número de hormigas. |
| 10 hormigas | Diez construcciones por iteración ACO completa. |
| 5,000 evaluaciones finales | Presupuesto por corrida de cada configuración, incluido todo el híbrido. |
| 450,000 evaluaciones del grid | Costo adicional de elegir reparto: 3 × 30 × 5,000. |
| 40/60 frente a 60/40 | Mayor mediana del primero, menor IQR del segundo; diferencia estadística no clara. |
| 25/30 victorias SA | Resultado por semillas; no una probabilidad universal de ganar. |
| +0.009575 | Mediana de 30 diferencias SA−híbrido; no diferencia de las medianas publicadas. |
| p Holm = 0.00256 | Evidencia de diferencia según la prueba; no probabilidad de que SA sea mejor. |
| Efecto rank-biserial = +0.612903 | Balance de rangos firmados favorable a SA; no mejora porcentual. |
| PSO individual = 0.254404 | Potencias sobre un subconjunto fijo sin optimizar; distinto de PSO sobre subconjuntos tabú. |

## Preguntas de práctica — no son el banco oficial

1. **¿Por qué un híbrido puede perder frente a SA?** Complementariedad no garantiza ventaja. Las etapas compiten por presupuesto y la segunda no revisa la selección de la primera; además cambian otros mecanismos. La evidencia favorece a SA bajo las condiciones probadas.
2. **¿Cómo evitaste duplicar el presupuesto?** Un solo evaluador, `problem.limited()` para la etapa ACO y el remanente para PSO. La reevaluación de la solución recibida se cobra dentro de PSO.
3. **¿Por qué no seleccionaste 60/40 si tuvo menor dispersión?** La regla previa era la mayor mediana. Se conservó después de ver los datos, y se reconoció que la diferencia entre ambos repartos quedó sin resolver estadísticamente.
4. **¿Qué aportan Friedman, Wilcoxon y Holm?** Friedman examina diferencias globales de rangos; Wilcoxon usa las diferencias de cada pareja de métodos sobre las mismas semillas; Holm controla el riesgo de falsos positivos de la familia de 15 comparaciones. Reportamos también tamaños de efecto.
5. **¿Un p no significativo demuestra empate?** No: indica evidencia insuficiente contra el modelo de la prueba. No prueba equivalencia ni un óptimo compartido.
6. **¿Por qué la dispersión pequeña de PSO no demostró estancamiento?** Los registros conservaron mejoras tardías. La diversidad y el incremento del objetivo describen aspectos diferentes; necesitamos mirar ambos.
7. **¿Por qué importa el piso de feromona?** Evita que la evaporación reduzca indefinidamente el peso de sitios poco reforzados. Los diagnósticos muestran que aquí conservó diversidad de construcción. El tope superior no fue vinculante bajo la actualización utilizada.
8. **¿Qué dice No Free Lunch aquí?** Su resultado requiere los supuestos de promediar sobre todas las funciones objetivo; no promete que mezclar métodos ayude. Nuestra evidencia se limita a esta instancia estructurada y estas configuraciones.
9. **¿Cómo refutarías la conclusión principal?** Congelar SA y el híbrido, predefinir una ventaja práctica y comparar nuevas semillas e instancias con el mismo presupuesto. Una reversión o ausencia de ventaja relevante exigiría limitar la conclusión.
10. **¿Qué error de IA quedó documentado?** Una prueba esperaba rechazar split=0.999 con presupuesto 10, aunque asigna 9 llamadas a ACO y una a PSO: ambas etapas son válidas. Se corrigió la expectativa. También se documentaron errores de formato y revisiones solicitadas por el estudiante; explica la evidencia sin atribuirte verificaciones que no hiciste.

## Grabación y entrega

- Sigue el procedimiento del curso para elegir las dos preguntas al grabar. No sustituyas ese sorteo por las preguntas de práctica.
- Muestra tu instancia y tus salidas reales. Puedes dejar abiertas la tabla global, la gráfica ampliada y la figura de límites.
- Comprueba la duración total y que se entiendan audio, números y etiquetas.
- Sube el video donde indique el curso, verifica que el enlace pueda abrirlo el evaluador y añádelo en `# Video` del notebook.
- La entrega solicitada es el notebook. Esta guía y los registros son material de preparación/local; no forman parte del archivo que debes adjuntar salvo indicación expresa del profesor.
