# Hosting web · resultados y límites

[Volver al proyecto](README.md) · [Resultados de respaldo](resultados-de-respaldo.md) · [Caso del portal](https://github.com/jokxer8/Portal-Mukien-Sang-Ben-Overview)

| Hito | Evidencia registrada al 26 de noviembre |
|---|---|
| Sitio de muestra | Nginx sirvió la página en local; se validaron rotación forzada, compresión y continuidad de la bitácora activa. |
| Recuperación | Una instancia aislada devolvió HTTP 200 y el contenido coincidió por SHA-256 con el sitio de muestra. |
| Primer proyecto de terceros | La [portada provisional](https://mukien.jokxer.dev/) devolvió HTTP 200 por HTTPS con TLS válido; HTML y CSS coincidieron con el origen. |
| Separación | Hosting público por túnel con origen local; nube y datos privados por separado. La actualización del firewall se probó en laboratorio antes de aplicarse sin cambiar las reglas de acceso. |
| Copias | La recepción asistida del archivo integral en Windows coincidió por SHA-256. La retención local no sustituye la copia independiente. |

La portada no es el portal completo. No se ha comprobado restaurar toda la infraestructura desde cero ni recuperar específicamente esta portada. Los disparos previstos del hosting y de las exportaciones semanales aún requerían evidencia en este corte.
