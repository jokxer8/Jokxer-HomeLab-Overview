# Plan Maestro público · Jokxer HomeLab

[Inicio](README.md) · [Resultados de respaldo](resultados-de-respaldo.md) · [Hosting](hosting-web.md) · [Control Center](control-center.md) · [En palabras simples](EN-PALABRAS-SIMPLES.md)

## Propósito y alcance

Reutilizar equipos para aprender a operar una nube privada, recuperar datos y alojar proyectos web pequeños. Debian atiende almacenamiento y servicios ligeros; otro equipo con AnduinOS se reserva para juegos, virtualización, IA local y multimedia intensiva. La documentación pública explica el método sin exponer accesos ni configuraciones privadas.

## Estado actual

**Corte de monitorización: 27 de noviembre de 2026, 21:31 AST.** La interfaz se puede recorrer en desarrollo y la API privada de Debian respondió a consultas de monitorización e histórico. Falta validar el despliegue definitivo del frontend por HTTPS privado, su aislamiento de Internet y el funcionamiento sostenido. Nextcloud, la recuperación aislada y la portada pública provisional conservan su evidencia y alcance por separado.

## Historia y decisiones por fase

| Fase | Qué hice | Qué queda abierto |
|---|---|---|
| Base y almacenamiento | Reutilicé un equipo con Debian y reservé otro para cargas intensivas. | Revisar capacidad y continuidad antes de sumar servicios. |
| Nube privada | Desplegué Nextcloud, probé acceso autorizado y ejercité la sincronización en un escenario acotado. | Completar pruebas con más clientes de compartición. |
| Respaldo y recuperación | Incorporé controles de integridad, una copia independiente y restauraciones aisladas. Corregí una colisión de tareas y observé un disparo diario de Nextcloud tras el ajuste. | Verificar exportación y recepción semanales en su horario y ensayar la recuperación con el formato reproducible. |
| Hosting ligero | Separé los sitios de prueba, restauré una muestra y publiqué la primera portada de terceros por HTTPS. | Probar el respaldo de hosting en horario y la restauración específica del portal. |
| Control Center (monitorización) | Interfaz navegable de solo lectura en desarrollo; consultas de monitorización, alertas e histórico comprobadas en la API privada. | Validar el acceso privado por HTTPS y demostrar estados normal, fallido y sin datos. [Ver la interfaz](control-center.md#vista-del-aplicativo). |
| Nuevos servicios | Definí un [catálogo por estado](README.md#catálogo-de-servicios). | Priorizar y probar antes de desplegar. No se ha trasladado Jokxer.dev al NAS. |

## Tecnologías y para qué las uso

| Tecnología | Uso en el proyecto |
|---|---|
| Debian, Docker Compose, Nextcloud, MariaDB y Redis | Administrar la nube personal y mantener separados el servicio web, la base de datos y la caché. |
| Tailscale | Entrar a Nextcloud por una red privada desde equipos autorizados. No es la vía para visitar la portada pública. |
| Nginx y Cloudflare Tunnel | Servir páginas aisladas y publicar por HTTPS solo la portada provisional del portal académico, sin hacer pública la nube privada. [Caso de hosting](hosting-web.md). |
| Resend | Enviar correo transaccional desde Nextcloud; consta una prueba de envío, no una medición sostenida de entregabilidad. |
| SQLite (Control Center) | Guardar y consultar el histórico. Se probó primero en laboratorio y después respondió el estado del motor en el NAS; aún falta comprobar operación sostenida. |
| React, TypeScript, Vite y Recharts | Presentar indicadores, vistas de servicios y series de tiempo en un tablero de solo lectura. |
| systemd y SHA-256 | Programar trabajos y comprobar la integridad de los archivos de respaldo. Una copia íntegra aún debe probarse en una restauración. |

## Resultados y evidencia

- **Recuperación de Nextcloud:** 142 archivos en 24 carpetas escaneados sin errores. Se comprobó lectura, escritura y eliminación autenticadas usando un archivo de control; no se verificó cada archivo individualmente. [Resultados](resultados-de-respaldo.md).
- **Imágenes Docker:** 3 de 3 imágenes y 36 de 36 capas verificadas; importadas en el equipo existente, sin demostrar una recuperación en un host vacío. [Resultados](resultados-de-respaldo.md).
- **Programación:** un respaldo diario de Nextcloud completado en 41 segundos tras el ajuste. Es un evento observado, no una tasa de éxito ni evidencia de que los otros ciclos se hayan ejecutado en horario. [Resultados](resultados-de-respaldo.md).
- **Hosting:** un sitio de muestra restaurado respondió HTTP 200 y devolvió el mismo contenido. La portada provisional se verificó por HTTPS; su restauración específica todavía no se dio por cerrada. [Hosting](hosting-web.md).

- **Monitorización:** 75 comprobaciones del contrato de inventario, 133 del seguimiento adaptativo, 20 de integración y 19 de capacidad, superadas en suites separadas. Son resultados de laboratorio, no sensores desplegados ni disponibilidad medida. [Resultados y límites del Control Center](control-center.md).

## Pendientes priorizados y próximos hitos

1. **Medir la automatización real.** Registrar por separado los disparos de hosting y exportación semanal, los resultados y la recepción de copias verificadas.
2. **Ampliar las pruebas de recuperación.** Recuperar el sitio provisional y repetir la prueba de Nextcloud con la copia reproducible, en un entorno aislado.
3. **Validar la primera entrega por HTTPS privado.** Servir el tablero desde el acceso autorizado, probar que no responda desde Internet y cotejar hora de observación, tendencia y estados. Añadir la evidencia de la última copia verificada sin confundirla con el disparo del temporizador.
4. **Evaluar la expansión.** Revisar capacidad, acceso, copia independiente y reversión antes de activar cualquier nuevo servicio.

## Sugerencias

- Usar el mismo formato de resultados para cada prueba: escenario, evidencia y límite.
- Mostrar en el panel el último resultado verificado y distinguirlo de una tarea que solo arrancó.
