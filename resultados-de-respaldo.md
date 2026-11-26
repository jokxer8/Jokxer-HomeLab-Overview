# Respaldos y recuperación del Jokxer HomeLab

[Volver al proyecto](README.md) · [Arquitectura pública](README.md#infraestructura-desplegada)

Corte: 26 de noviembre de 2026. Resultados observados durante las pruebas, no una comprobación nueva del servidor.

## Qué se comprobó

| Prueba | Resultado | Límite |
|---|---|---|
| Restauración desde copia independiente anterior | 142 archivos en 24 carpetas, sin errores de escaneo. Descarga autenticada idéntica y creación, verificación y eliminación de un archivo de control. | No se verificaron todos los archivos uno por uno ni se midió el tiempo de recuperación. |
| Transferencia de la exportación reproducible | SHA-256 coincidente entre el NAS y Windows. Tras regenerar la misma instantánea, Windows reconoció el archivo ya verificado y no lo descargó otra vez. | Reproducibilidad demostrada para la instantánea ensayada; falta restaurar desde el formato nuevo. |
| Tarea de Windows | Lanzamiento de prueba desde el Programador, autenticación SSH asistida, bitácora y código de salida 0. | En ese lanzamiento no había una transferencia pendiente; la transferencia con datos se ensayó por separado. |
| Auditoría de copias | Dos copias portátiles íntegras en el inventario final, incluida la histórica protegida; retención y bitácoras comprobadas. | Una copia independiente del equipo no equivale a una copia fuera de la ubicación física. |
| Imágenes Docker | 3/3 imágenes respaldadas, 36/36 capas únicas verificadas con SHA-256, copia independiente e importación de las tres en el host existente. | No incluye la restauración de datos y configuración en un host vacío. |

## Operación programada y hosting

| Comprobación | Resultado | Límite |
|---|---|---|
| Nextcloud diario | Primer disparo exitoso tras los ajustes: 26 de noviembre; 41 segundos, integridad SHA-256 y salida de mantenimiento correctas | Es una ejecución observada, no una tasa histórica |
| Hosting: sitio de muestra | HTTP 200 y contenido idéntico por SHA-256 tras restaurar en Nginx aislado | No equivale a restaurar el portal provisional |
| Hosting: copia integral | Recepción independiente en Windows con SHA-256 coincidente durante el ensayo asistido | No equivale a una recepción por horario natural ni a probar la recuperación integral |

Los registros diario, semanal y mensual del primer archivo local de hosting compartían un mismo archivo físico mediante enlaces duros. [Alcance del hosting](hosting-web.md).

## Qué falta validar

- Primer respaldo diario programado de hosting y primeras exportaciones dominicales programadas de Nextcloud y hosting.
- Primera recepción dominical programada en Windows. La autenticación SSH y la limpieza de las exportaciones siguen siendo asistidas.
- Restauración funcional del portal provisional y del nuevo formato de Nextcloud, ensayo completo desde cero y una copia adicional fuera de la ubicación física.

Los indicadores de operación pendientes son **ejecuciones programadas exitosas / previstas** en un periodo definido y **tiempo de recuperación** hasta comprobar acceso autenticado a archivos. Las pruebas manuales no se cuentan como disparos automáticos.

[Volver a resultados en la portada](README.md#resultados-verificables)
