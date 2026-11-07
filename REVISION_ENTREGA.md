# Revisión final — TC6035, A01748760

Basada en `assignment-spec.pdf`, especialmente secciones 5–10 y rúbrica. Revisión posterior a la ejecución local completa del commit `1af57e7`. Las correcciones finales de esta revisión son de texto; no cambian código ni resultados.

| Requisito | Estado | Evidencia o acción |
|---|---|---|
| Una instancia identificada y ruta declarada | Cumple | David Rodríguez Fragoso, A01748760, salt 0, problema mixto proporcionado. |
| Estructura principal obligatoria y orden | Cumple | Identification, Formulation, Implementations, M0, M1, M2, M3, Analysis, AI Ledger, Video. |
| Seis métodos y registro dentro del notebook | Cumple | Implementaciones inline y seis entradas en ALGORITHMS; PSO individual y condicionado se distinguen. |
| Referencias al hito previo mediante variables en código | Cumple | M1 usa MC_BASELINE_MEDIAN/NOMINAL_POWER/rho_1; M2 usa PSO_PARAMS y las entradas de M1; M3 recupera M3_PSO_PARAMS y M3_ACO_PARAMS de los registros de M2. |
| Cada hito termina con `## Carry forward` | Corregido | Encabezados uniformados; el cierre de M3 ahora tiene su propia celda. |
| Formulación, factibilidad y acoplamiento M0 | Cumple | Objetivo y penalización, ejemplo de conectividad y comparación conjunta/por etapas. |
| Monte Carlo y SA con justificación medida | Cumple | 30 semillas; diagnóstico de aceptación de empeoramientos al principio/final. |
| Memoria tabú, PSO y comparación de alcance M1 | Cumple | Tuning separado; reglas, validaciones y costos de las etapas explícitos. |
| Topología, estabilidad, mejoras tardías y ACO M2 | Cumple | Ring/gbest, recurrencia determinista y límites de interpretación; registros internos. |
| Híbrido justificado antes del resultado | Cumple | ACO → PSO ring; grid de reparto y regla de selección previos a las corridas finales. |
| Un presupuesto compartido del híbrido | Cumple | Un evaluador; 2,000 ACO +3,000 PSO; transferencia reevaluada dentro de la segunda etapa. |
| 30 semillas pareadas y 5,000 llamadas finales | Cumple | Verificación de trazas, presupuestos y protocolos; 180 registros en el estudio global. |
| Mediana/IQR, pruebas y tamaños de efecto | Cumple | Friedman, sensibilidad por permutaciones, 15 Wilcoxon con Holm y efectos firmados. |
| Figura de estado interno y explicación | Cumple | Feromonas/diversidad ACO, dispersión PSO y mecanismo tabú. |
| Conclusiones limitadas y experimento falsador | Cumple | SA frente a este híbrido en una instancia; nuevas semillas/instancias podrían cambiar la conclusión. |
| Error concreto de IA y verificación | Cumple | Ejemplos de formato, repetición editorial y expectativa incorrecta en la prueba del reparto; evidencia y correcciones en Ledger. |
| Identificación exacta de herramienta/modelo | Parcial | ChatGPT/Codex declarados. Identificadores exactos de sesiones anteriores no recuperados; no se inventan. Añadirlos solo si se pueden verificar. |
| Notebook ejecutado completo y salidas coherentes | Cumple | 72 celdas de código ejecutadas en orden, sin errores; código/salidas preservados en esta revisión. |
| Tamaño menor de 20 MB | Cumple | Aproximadamente 2.82 MB antes de la revisión; comprobar tamaño final al guardar el enlace. |
| Video individual, hasta cinco minutos | Pendiente | Grabar mostrando instancia/resultados y respondiendo dos preguntas elegidas al grabar del banco oficial. |
| Enlace del video dentro de `# Video` | Pendiente | Añadir URL real y comprobar acceso del evaluador. |
| Un único notebook como entrega | Preparado | `tc6035-A01748760.ipynb`. Los logs y esta guía se conservan fuera de la entrega, salvo instrucción del profesor. |

## Preparación para una reevaluación del notebook

Los métodos de optimización están dentro del notebook. Los lectores de resultados principales aparecen después de las celdas que los generan. La biblioteca `tc6035` es la suministrada por el curso. La ejecución desde cero genera sus archivos; las salidas visibles por sí solas no los reemplazan. Los checkpoints existentes solo se reutilizan cuando coincide su protocolo: usa los registros de tu venv o una carpeta de resultados compatible, no una mezcla de entornos.

La ejecución local verificada usa Python 3.13.2, NumPy 2.5.4 y SciPy 1.18.1; las figuras subidas identifican Matplotlib 3.11.2. El `requirements.lock` del repositorio conserva pins de NumPy 2.5.2 y Matplotlib 3.11.1 del entorno anterior. Eso no invalida la corrida ya verificada. Si necesitas recrear el venv, el registro de versiones efectivamente usadas debe prevalecer; no se afirma que todo el lock sea una captura exacta del venv final.

## Antes de enviar

1. Revisar el texto final y practicar con `GUIA_VIDEO.md`.
2. Obtener el banco oficial y seguir su procedimiento de elección al grabar.
3. Grabar, comprobar duración/audio y acceso al video, y colocar su enlace en `# Video`.
4. Guardar el notebook conservando las salidas verificadas. Añadir el enlace no requiere repetir experimentos.
5. Entregar únicamente el `.ipynb` solicitado. Mantener `results/`, figuras y respaldos para reproducibilidad fuera del adjunto de entrega.

El PDF consultado consigna 26 de octubre de 2026 como fecha original. Como esta revisión es posterior, cualquier prórroga o instrucción vigente debe confirmarse en Canvas; no se deduce una fecha nueva del repositorio.
