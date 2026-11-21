# Memo ejecutivo — Conecta+

## Decisión

Se recomienda contactar a 818 clientes del corte de diciembre, porque son los casos en los que el beneficio esperado de una intervención supera su costo. La estimación de riesgo sirve para priorizar esfuerzos; no garantiza que una llamada evite una cancelación.

## Hallazgos principales

- La información histórica contiene 4.758 observaciones y el corte de diciembre contiene 1.549 clientes.
- En septiembre de 2025, la exposición previa a eventos de la versión 5.3.0 se relacionó con 144 cancelaciones de 554 clientes (25,99%), frente a 123 de 1.174 clientes no expuestos (10,48%). La diferencia fue de aproximadamente 15,52 puntos porcentuales.
- Esta comparación muestra una relación, pero no demuestra que la versión 5.3.0 haya causado las cancelaciones. Los grupos también difieren en fecha, plataforma y actividad.

## Recomendación económica

Con un costo de contacto de 25.000 COP, una efectividad supuesta de 40% y un valor de 12 mensualidades, se recomienda contactar a 818 clientes (52,81%). El costo estimado es 20.450.000 COP, las cancelaciones evitadas esperadas son aproximadamente 70,00, el valor bruto esperado es 35.725.235,25 COP y el beneficio neto esperado es 15.275.235,25 COP.

Estos valores son escenarios bajo supuestos y no resultados garantizados. Como referencia, contactar a todos produciría un beneficio neto esperado aproximado de 9.395.358,86 COP; no contactar a nadie produciría 0 COP bajo la misma fórmula.

## Acciones recomendadas, riesgos y siguiente validación

1. Priorizar los 818 contactos y registrar el resultado de cada intervención.
2. Mantener un grupo de control elegido aleatoriamente entre clientes elegibles para medir el efecto real del contacto.
3. Medir durante 90 días las cancelaciones, la calidad del servicio, el costo y el beneficio neto antes de ampliar la campaña.

La exposición a 5.3.0 no fue aleatoria y septiembre ya se había observado durante el desarrollo. Además, ciertos estados modernos de tickets no tienen fecha de resolución y los mensajes no contienen marcas de tiempo. Por una política conservadora se retiraron 15 señales de tickets cuya disponibilidad histórica no podía garantizarse; la auditoría no demostró una fuga temporal confirmada. Deben revisarse la disponibilidad histórica de tickets, la estabilidad de los datos y los cambios en planes o precios antes de reutilizar la decisión en producción.
