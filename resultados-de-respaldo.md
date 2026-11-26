# Respaldos y recuperación del Jokxer HomeLab

[Volver al proyecto](README.md) · [Arquitectura pública](README.md#infraestructura-desplegada)

Corte: 25 de noviembre de 2026. Resultados observados durante las pruebas, no una comprobación nueva del servidor.

## Qué se comprobó

| Prueba | Resultado | Límite |
|---|---|---|
| Restauración desde copia independiente anterior | 142 archivos en 24 carpetas, sin errores de escaneo. Descarga autenticada idéntica y creación, verificación y eliminación de un archivo de control. | No se verificaron todos los archivos uno por uno ni se midió el tiempo de recuperación. |
| Transferencia de la exportación reproducible | SHA-256 coincidente entre el NAS y Windows. Tras regenerar la misma instantánea, Windows reconoció el archivo ya verificado y no lo descargó otra vez. | Reproducibilidad demostrada para la instantánea ensayada; falta restaurar desde el formato nuevo. |
| Tarea de Windows | Lanzamiento de prueba desde el Programador, autenticación SSH asistida, bitácora y código de salida 0. | En ese lanzamiento no había una transferencia pendiente; la transferencia con datos se ensayó por separado. |
| Auditoría de copias | Dos copias portátiles íntegras en el inventario final, incluida la histórica protegida; retención y bitácoras comprobadas. | Una copia independiente del equipo no equivale a una copia fuera de la ubicación física. |
| Imágenes Docker | 3/3 imágenes respaldadas, 36/36 capas únicas verificadas con SHA-256, copia independiente e importación de las tres en el host existente. | No incluye la restauración de datos y configuración en un host vacío. |

## Qué falta validar

- Primer respaldo diario disparado por el temporizador tras los ajustes y primera exportación dominical programada.
- Primera recepción dominical programada en Windows. La autenticación SSH y la limpieza de las exportaciones siguen siendo asistidas.
- Restauración funcional desde el formato reproducible, ensayo completo desde cero y una copia adicional fuera de la ubicación física.

Los indicadores de operación pendientes son **ejecuciones programadas exitosas / previstas** en un periodo definido y **tiempo de recuperación** hasta comprobar acceso autenticado a archivos. Las pruebas manuales no se cuentan como disparos automáticos.

[Volver a resultados en la portada](README.md#resultados-verificables)
