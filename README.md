# Prueba técnica de Ciencia de Datos — Conecta+

Solución reproducible para explorar el riesgo de cancelación, construir variables históricas, calibrar probabilidades y priorizar contactos bajo supuestos económicos explícitos.

## Estructura

- `solucion.ipynb`: notebook de exploración, auditoría, integración temporal, modelado, calibración, decisión económica y hallazgo senior.
- `predicciones.csv`: salida final con `cliente_id`, `probabilidad` y `contactar`.
- `MEMO.md`: resumen ejecutivo.
- `BITACORA_IA.md`: uso transparente de IA y decisiones pendientes de completar.
- `requirements.txt`: dependencias de Python.
- `inicio.ipynb`: notebook original entregado; no se modifica.
- `datos_conecta/`: fuentes privadas excluidas de Git.

La base SQLite, los JSONL, el ZIP, el PDF del enunciado y los registros individuales no deben publicarse.

## Ejecución local

Crear o activar un entorno Python compatible, instalar `requirements.txt` y abrir `solucion.ipynb` con Jupyter en VS Code. Las rutas son relativas al proyecto. La ejecución debe hacerse en orden y con las fuentes privadas presentes. El notebook utiliza SQLite en modo de solo lectura y no modifica las fuentes.

## Ejecución privada en Google Colab

En Colab, cargar privadamente `datos_conecta.zip` desde el panel de archivos o desde una ubicación autorizada y descomprimirlo en la raíz de trabajo. No incrustar el ZIP ni registros en el repositorio. Después subir o clonar el repositorio y abrir `solucion.ipynb`.

[Open in Colab](https://colab.research.google.com/github/REEMPLAZAR_ORGANIZACION/REEMPLAZAR_REPOSITORIO/blob/main/solucion.ipynb)

El enlace anterior es una plantilla: debe reemplazarse con la URL definitiva del repositorio antes de publicar.

## Reproducción y resultados verificados

La ejecución generó 1.549 filas, una por cliente a puntuar, sin IDs duplicados y con las tres columnas exigidas. Bajo los supuestos de 25.000 COP por contacto, 40% de efectividad y 12 mensualidades, la regla recomendó 920 contactos; el costo fue 23.000.000 COP y el beneficio neto esperado fue 17.176.835,60 COP. Son valores esperados, no garantías.

El hallazgo senior mostró una asociación descriptiva entre exposición previa a 5.3.0 y cancelación: 25,99% frente a 12,16% sin exposición. La exposición coincide con diferencias de fecha, plataforma y actividad; se requiere una evaluación controlada antes de atribuir causalidad.

## Limitaciones y sustentación

La etiqueta es observacional, la probabilidad calibrada no mide el efecto de una intervención y septiembre fue observado durante el desarrollo. Deben explicarse los cortes temporales, la deduplicación, la cobertura de tickets, el tratamiento de faltantes, la calibración y la fórmula económica. En producción se debe mantener un grupo de control, monitorear calibración y deriva, y reentrenar solo después de revisar calidad y disponibilidad.
