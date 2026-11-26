# En palabras simples · HomeLab

[Inicio](README.md) · [Plan maestro](PLAN-MAESTRO.md) · [Resultados](resultados-de-respaldo.md)

**Una copia no es una restauración.** Si una copia tiene el mismo SHA-256 en el NAS y en Windows, comprobaste que llegó sin cambios. Para saber si sirve, restaura en un entorno separado y prueba el resultado. En este HomeLab, la aplicación restaurada escaneó 142 archivos y se verificó la lectura, escritura y eliminación con un archivo de control. No se comprobó uno por uno el contenido de los 142.

**Ejercicio seguro:** crea un archivo de texto sin datos personales en tu equipo, copia el archivo a otra carpeta, compara sus huellas y abre la copia. Anota qué demuestra cada prueba. No cambies permisos, firewall ni servicios del NAS para realizar este ejercicio.

**La automatización también se prueba.** Ejecutar algo manualmente enseña qué hace; comprobar su ejecución programada enseña si sucede a la hora prevista. [Ver los dos tipos de prueba](resultados-de-respaldo.md).
