# Respaldos y recuperación del Jokxer HomeLab

[Volver a la portada](README.md#resultados-verificables)

Corte: 25 de noviembre de 2026 (AST). Los estados reflejan resultados registrados, no una nueva ejecución.

| Hito | Evidencia | Límite |
|---|---|---|
| Restauración independiente | Instancia aislada iniciada; 142 archivos en 24 carpetas, sin errores en el escaneo; descarga, escritura y eliminación autenticadas con archivo de control. | No verifica todos los archivos individualmente ni mide el tiempo de recuperación. |
| Segunda transferencia supervisada | Una copia de aproximadamente 406 MiB llegó al destino y pasó su verificación SHA-256. | No es una prueba de restauración de esa copia ni de transferencia automática. |
| Retención controlada | Se rechazaron candidatos incompletos o corruptos en las pruebas pertinentes; una ejecución supervisada conservó el histórico protegido y la copia más reciente del corte. | No se ha demostrado una retención desatendida. |
| Programación | Respaldo interno diario y preparación semanal de copia externa configurados. Se observó ejecución manual exitosa. | Pendiente comprobar ejecuciones exitosas disparadas por ambos temporizadores y cerrar la recepción semanal. |
| Detección de discrepancia | El flujo de recepción detuvo la operación al detectar que una reexportación tenía otra huella del archivo comprimido. La copia local pasó su checksum original y coincidió el manifiesto interno. | No se afirma corrupción ni se ha resuelto todavía la causa o el procedimiento de reconciliación. |

El resumen público no contiene credenciales, direcciones, rutas operativas ni archivos de respaldo.
