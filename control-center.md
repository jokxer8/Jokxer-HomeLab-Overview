# Jokxer NAS Control Center

[Inicio](README.md) · [Plan Maestro](PLAN-MAESTRO.md) · [Respaldos](resultados-de-respaldo.md) · [Hosting](hosting-web.md)

**Corte:** 27 de noviembre de 2026, 19:20 AST. **Estado:** componentes implementados y probados en laboratorio; primera vista privada pendiente.

## Qué problema resuelve

Quiero saber si el NAS funciona, qué requiere atención y cuándo se comprobó. La interfaz debe emplear nombres claros en español con el término técnico entre paréntesis cuando ayude, y explicar qué significa cada indicador, qué riesgo implica y qué conviene revisar. Sin una lectura reciente no se puede concluir que un equipo esté sano ni que esté averiado. Por ejemplo, un disco externo puede estar montado y funcionando aunque su adaptador no entregue datos de salud (SMART); el panel debe mostrar ese diagnóstico como **no evaluado**, no como fallo.

## Evidencia y alcance

| Suite | Comprobaciones superadas | Qué quedó probado |
|---|---:|---|
| Contrato permanente de inventarios | **75** | Se distingue si una fuente está disponible y si su inventario es completo y confiable. Un inventario inválido, incompleto o sin verificar no permite inferir ausencias. Se comprobó la integridad de la base de prueba y que sus referencias permanecieran válidas. |
| Seguimiento adaptativo permanente | **133** | Solo se suma evidencia con mediciones nuevas: no duplicados, datos en caché ni lecturas vencidas. Una interrupción o un salto temporal invalida la continuidad; si el elemento reaparece, se limpia la evidencia acumulada. Se probaron reversión de cambios, aislamiento entre operaciones simultáneas e integridad referencial. |
| Ciclo integrado | **20** | Se probaron once fuentes; se mantuvieron deshabilitadas la certificación y la retirada por inventario vacío. Se conservaron el esquema y sus 41 reglas automáticas (disparadores de la base). |
| Capacidad del ciclo integrado | **19** | Se persistieron 2.000 identidades sintéticas y se ejecutaron seis ciclos. El más lento tardó 191 ms; se observaron 23,35 MiB de memoria pico del proceso y 772 KiB de almacenamiento final de prueba. La retirada permaneció deshabilitada. |

Los escenarios de seguimiento cubrieron categorías de sistema, red, hardware, servicios, almacenamiento, Nextcloud, hosting, Docker, salud de discos, volúmenes lógicos y respaldos. Las suites se ejecutaron por separado en un laboratorio temporal; **los recuentos no se suman como cobertura única, no equivalen a sensores activos y no miden disponibilidad del NAS**. Una ejecución inicial se detuvo al usar una medición de prueba vencida; la ejecución final completó la suite e incluyó el rechazo de lecturas caducadas entre los casos válidos.

### Prueba de historiales representativos

Otra suite, de **18 comprobaciones**, ensayó con 219 identidades sintéticas, 78 reglas de clasificación y cinco clases de métricas. Las 21.420 mediciones quedaron representadas en 2.628 resúmenes de cinco minutos y luego en 219 resúmenes horarios, preservando el conteo de muestras por clase. La ejecución final superó el problema de presupuesto del ensayo anterior para esa carga modelada y registró una memoria pico de 33,56 MiB. No fue una prueba de producción ni una garantía para otros volúmenes.

Los números de capacidad del ciclo integrado corresponden a seis ciclos sobre datos sintéticos; no son un compromiso de rendimiento, un límite recomendado ni una proyección de almacenamiento real.

Estas pruebas no demuestran que exista una base de producción activa, un tablero desplegado o mediciones programadas. Nextcloud, el hosting y los respaldos existentes se validan por separado y no dependen de este panel.

## Primera versión visible

Un cierre útil sería una **vista privada y de solo lectura** con tres indicadores: espacio disponible, último respaldo verificado y disponibilidad de los servicios seleccionados. Debe mostrar la hora de la última lectura, una tendencia sencilla cuando haya datos suficientes y un estado gris para datos ausentes, vencidos o no evaluados. El rojo debe reservarse para fallos confirmados. El panel puede demostrar su utilidad con un conjunto acotado de datos autorizados, sin retirar elementos ni configurar borrados automáticos.

**Después de la primera vista:** validar la persistencia y la recolección periódica por separado. Mantener fuera del piloto los cambios automáticos sobre servicios e inventarios.

Este documento no publica configuraciones internas, secretos ni registros sin depurar.
