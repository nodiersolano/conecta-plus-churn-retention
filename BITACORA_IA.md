# Bitácora de uso de IA

Este documento registra el uso real de ChatGPT y Codex como apoyo técnico. La IA propuso código y criterios; las cifras incluidas se conservaron solo después de ejecutar comprobaciones en el entorno local. No se publicaron datos personales ni archivos de origen.

## Intervenciones principales

| Tema | Sugerencia de la IA | Qué se aceptó o corrigió | Justificación |
|---|---|---|---|
| Interpretación y planificación | Separar el trabajo en exploración, auditoría, integración temporal, modelado, calibración y decisión económica. | Aceptado. | Permitió validar cada etapa antes de avanzar. |
| Entorno | Usar `.venv`, rutas relativas y código compatible con Colab; no crear otro entorno. | Aceptado. | Mantiene reproducibilidad local y en Colab. |
| Exploración y limpieza | Auditar SQLite y JSONL sin modificar fuentes, normalizar fechas y trabajar con copias en memoria. | Aceptado. | Protege los datos originales y hace explícita la disponibilidad temporal. |
| Pérdida de celdas | Comprobar el JSON del notebook, crear respaldo y recuperar únicamente secciones faltantes. | Aceptado con revisión humana. | Se preservaron las secciones existentes y se evitaron sobrescrituras. |
| Identificadores de tickets | Convertir tanto el formato moderno numérico como el antiguo `CL-<número>` a un entero validado. | Aceptado. | La cobertura ejecutada pasó a incluir los 4.681 tickets, sin inventar IDs. |
| Facturas duplicadas | Deduplicar por `factura_id` y luego por cliente, suscripción y período cuando no había conflicto de cliente o monto. | Aceptado. | Evita doble contabilización; los grupos con conflicto se reportaron para revisión. |
| Ingeniería de características | Agregar fuentes a nivel `(cliente_id, fecha_corte)`, con ventanas y filtros de disponibilidad. | Aceptado. | Evita multiplicación de filas y fugas temporales. |
| Modelado | Comparar regresión logística, un modelo de mayor capacidad y una referencia con validación temporal. | Aceptado. | La elección se basó en métricas observadas, no en una preferencia previa. |
| Calibración | Comparar ponderación de clases, calibración sigmoide e isotónica usando periodos anteriores al evaluado. | Aceptado con advertencia. | Se reconoció el riesgo de selección adaptativa tras observar septiembre. |
| Decisión económica | Aplicar `probabilidad × efectividad × 12 mensualidades − costo` y análisis de sensibilidad. | Aceptado como escenario. | La fórmula no se interpretó como efecto causal garantizado. |
| Hallazgo senior | Comparar exposición previa a 5.3.0 y `CRASH_ON_START` con etiquetas históricas, sin afirmar causalidad. | Aceptado. | La exposición está asociada con fecha, plataforma y actividad; requiere experimento. |

## Correcciones y límites

- Se corrigió la gestión de conexión SQLite con `contextlib.closing` para asegurar el cierre, manteniendo solo lectura.
- Se evitó ejecutar o editar `inicio.ipynb` y no se agregaron registros individuales a documentos.
- La ejecución de celdas se hizo con el intérprete de `.venv` y se validó el JSON del notebook después de cada modificación relevante.
- La IA no conoce decisiones humanas no registradas. Tiempo dedicado, revisión final del autor, aprobación de supuestos y cualquier decisión comercial adicional: **[COMPLETAR POR EL AUTOR]**.
- Observaciones rechazadas o no adoptadas por la persona autora y su motivo: **[COMPLETAR POR EL AUTOR]**.
