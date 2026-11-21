# Memo ejecutivo — Conecta+

## Decisión

El objetivo es priorizar clientes con mayor probabilidad estimada de cancelar y contactar solo cuando el valor esperado neto sea positivo. La probabilidad predice riesgo; no garantiza que una llamada evite la cancelación.

## Hallazgos principales

- La tabla histórica contiene 4.758 observaciones y el corte de diciembre contiene 1.549 clientes.
- En septiembre de 2025, la exposición previa a eventos de la versión 5.3.0 se asoció descriptivamente con 144 cancelaciones de 554 clientes (25,99%), frente a 123 cancelaciones de 1.174 clientes no expuestos (10,48%). La diferencia fue de aproximadamente 15,52 puntos porcentuales. Esta comparación es asociativa, no causal: la exposición coincide con diferencias de fecha, plataforma y actividad.
- La señal está concentrada en el corte de septiembre y en actividad móvil. También hay diferencias de uso entre grupos; por eso no se puede afirmar que la versión sea la causa.

## Modelo definitivo y recomendación económica

La versión definitiva B utiliza 41 variables predictoras, regresión logística sin ponderación de clases (`logistic_unweighted`) y calibración sigmoide. En la evaluación de septiembre obtuvo ROC-AUC 0,698060, PR-AUC 0,316809 y Brier Score 0,123211. La comparación con la versión A de 56 variables fue exploratoria y no constituye una prueba independiente de superioridad.

Con las probabilidades calibradas, costo de contacto de 25.000 COP, efectividad supuesta de 40% y valor de 12 mensualidades, se recomienda contactar a 818 clientes (52,81%). El costo estimado es 20.450.000 COP, las cancelaciones evitadas esperadas son aproximadamente 70,00, el valor bruto esperado es 35.725.235,25 COP y el beneficio neto esperado es 15.275.235,25 COP.

Estos valores son escenarios calculados bajo supuestos, no resultados garantizados. Como referencia, contactar a todos produciría un beneficio neto esperado de aproximadamente 9.395.358,86 COP y no contactar a nadie produciría 0 COP bajo la misma fórmula.

## Limitaciones y siguiente control

La exposición a 5.3.0 no fue aleatoria, septiembre ya fue observado durante el desarrollo y el modelo no estima el efecto causal de contactar. En la auditoría temporal se detectó que ciertos estados modernos de tickets no tienen `resolved_at` y que los mensajes no incluyen timestamps; por política conservadora se retiraron 15 variables ambiguas, sin demostrar una fuga temporal confirmada. Debe mantenerse un grupo de control aleatorio entre clientes elegibles y medirse cancelación a 90 días, calidad de servicio, costo y beneficio neto antes de ampliar la campaña. También deben monitorearse deriva de datos, calibración, cobertura de identificadores, disponibilidad histórica de tickets y cambios en planes o precios.
