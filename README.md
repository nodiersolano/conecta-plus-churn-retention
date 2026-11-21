# Prueba técnica de Ciencia de Datos — Conecta+

**[Open in Colab](https://colab.research.google.com/github/nodiersolano/conecta-plus-churn-retention/blob/main/solucion.ipynb)**

Solución reproducible para explorar el riesgo de cancelación, construir variables históricas, calibrar probabilidades y priorizar contactos bajo supuestos económicos explícitos.

## Estructura

- `solucion.ipynb`: notebook definitivo de la solución B, con 41 variables predictoras, auditoría, integración temporal, modelado, calibración, decisión económica y hallazgo senior.
- `predicciones.csv`: salida final con `cliente_id`, `probabilidad` y `contactar`.
- `MEMO.md`: resumen ejecutivo.
- `BITACORA_IA.md`: uso transparente de IA y decisiones documentadas; no tiene campos pendientes.
- `requirements.txt`: dependencias de Python.
- `datos_conecta/`: datos fuente privados excluidos de Git.

Los datos fuente originales (base SQLite y archivos JSONL), `datos_conecta.zip`, el PDF del enunciado y los registros individuales son privados y no deben publicarse. `predicciones.csv` sí es un entregable requerido expresamente para la evaluación.

## Ejecución local

Crear o activar un entorno Python compatible, instalar `requirements.txt` y abrir `solucion.ipynb` con Jupyter en VS Code. Las rutas son relativas al proyecto. La ejecución debe hacerse en orden y con las fuentes privadas presentes. El notebook utiliza SQLite en modo de solo lectura y no modifica las fuentes.

## Ejecución privada en Google Colab

Abre el notebook mediante el enlace **[Open in Colab](https://colab.research.google.com/github/nodiersolano/conecta-plus-churn-retention/blob/main/solucion.ipynb)**. Si prefieres cargarlo manualmente, selecciona **Archivo > Subir cuaderno** y sube `solucion.ipynb`. En el panel **Archivos**, sube también `requirements.txt`; abrir un notebook desde GitHub no descarga automáticamente los demás archivos del repositorio.

1. Ejecuta `%pip install -q -r requirements.txt` una sola vez en una celda de Colab.
2. Ejecuta la celda inicial de configuración; si `datos_conecta/` no existe, solicitará cargar privadamente `datos_conecta.zip`.
3. El ZIP debe contener `datos_conecta/conecta.db`, `datos_conecta/tickets.jsonl` y `datos_conecta/eventos.jsonl.gz` (o esos tres archivos en la raíz). La configuración valida la estructura y evita crear una carpeta anidada duplicada.
4. Ejecuta las celdas en orden hasta el final. El notebook definitivo contiene 61 celdas, incluidas 34 celdas de código, y no requiere una celda de instalación dentro del notebook. El archivo `predicciones.csv` se escribirá en el directorio de trabajo de Colab.

No subas el ZIP, la base SQLite, los JSONL ni registros individuales al repositorio. El notebook imprime resultados agregados y evita mostrar textos de tickets o muestras individuales de clientes.

## Reproducción y resultados verificados

La solución B conserva 41 variables predictoras y utiliza regresión logística sin ponderación de clases (`logistic_unweighted`) con calibración sigmoide. En la evaluación de septiembre obtuvo ROC-AUC 0,698060, PR-AUC 0,316809 y Brier Score 0,123211. La ejecución generó 1.549 filas, una por cliente a puntuar, sin IDs duplicados y con las tres columnas exigidas. Bajo los supuestos de 25.000 COP por contacto, 40% de efectividad y 12 mensualidades, la regla recomendó 818 contactos; el costo fue 20.450.000 COP, las cancelaciones evitadas esperadas fueron aproximadamente 70,00, el valor bruto esperado fue 35.725.235,25 COP y el beneficio neto esperado fue 15.275.235,25 COP. Son valores esperados, no garantías.

El texto de los tickets se exploró mediante reglas y perfiles agregados, sin publicar textos ni registros individuales. La versión B retira exclusivamente 15 variables derivadas de tickets cuya disponibilidad histórica no puede garantizarse: estados abiertos y conteos de palabras clave por ventana. Estas 15 variables ambiguas se excluyeron del modelo definitivo por la incertidumbre temporal; se conservan las demás fuentes y la ingeniería temporal. La comparación con la versión A fue exploratoria y no constituye una prueba independiente de superioridad.

El hallazgo senior mostró en septiembre de 2025 una asociación descriptiva entre exposición previa a 5.3.0 y cancelación: 144 de 554 clientes expuestos (25,99%) frente a 123 de 1.174 clientes no expuestos (10,48%), una diferencia aproximada de 15,52 puntos porcentuales. La exposición coincide con diferencias de fecha, plataforma y actividad; se requiere una evaluación controlada antes de atribuir causalidad.

## Limitaciones y sustentación

La etiqueta es observacional, la probabilidad calibrada no mide el efecto de una intervención y septiembre fue observado durante el desarrollo. Algunos estados modernos de tickets no tienen `resolved_at` y los mensajes no contienen timestamps; por ello se retiraron las 15 variables temporalmente ambiguas, aunque permanece una limitación de disponibilidad histórica que debe revisarse en producción. Deben explicarse los cortes temporales, la deduplicación, la cobertura de tickets, el tratamiento de faltantes, la calibración y la fórmula económica. En producción se debe mantener un grupo de control, monitorear calibración y deriva, y reentrenar solo después de revisar calidad y disponibilidad.
