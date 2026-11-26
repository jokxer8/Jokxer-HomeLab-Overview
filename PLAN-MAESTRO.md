# Plan maestro público · Jokxer HomeLab

[Inicio](README.md) · [Resultados de respaldo](resultados-de-respaldo.md) · [Hosting](hosting-web.md) · [Aprender con el proyecto](EN-PALABRAS-SIMPLES.md)

**Corte:** 26 de noviembre de 2026 · paso 842.3. Caso de aprendizaje con Debian para almacenamiento y servicios ligeros, y AnduinOS para cargas intensivas. El trabajo se organiza por resultados comprobables.

| Fase | Qué se puede comprobar | Qué sigue |
|---|---|---|
| Nube privada | Nextcloud operativo y uso desde clientes autorizados. | Completar pruebas de clientes para la compartición de archivos. |
| Copias y recuperación | Restauración aislada; 142 archivos escaneados en 24 carpetas sin errores; tres imágenes Docker respaldadas. Primer respaldo diario de Nextcloud verificado tras el ajuste. | Validar exportación semanal y recepción asistida, y restaurar el formato reproducible. |
| Hosting web | Un sitio de muestra regresó con HTTP 200 y contenido idéntico tras restaurarse. El primer sitio de terceros tiene una portada provisional. | Comprobar respaldo programado del hosting y restauración específica del portal. |
| Expansión | [Catálogo por estado](README.md#catálogo-de-servicios). | Evaluar cada servicio antes de desplegarlo. |

**Meta de aprendizaje:** explicar por qué se separan los accesos, cómo se verifica una copia y qué evidencia hace falta antes de afirmar que una recuperación funciona. No se publican configuraciones sensibles ni accesos privados.
