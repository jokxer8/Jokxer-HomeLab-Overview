# En palabras simples · HomeLab

[Inicio](README.md) · [Plan maestro](PLAN-MAESTRO.md) · [Resultados](resultados-de-respaldo.md)

## 1. Integridad de una copia y prueba de restauración

- **¿Por qué?** Una copia puede llegar sin cambios y aun así faltar lo necesario para recuperar el servicio.
- **¿Para qué?** Para separar dos comprobaciones: que el archivo llegó intacto y que una restauración devuelve las funciones esperadas.
- **¿Cómo?** Crea un archivo de texto sin datos personales, cópialo a otra carpeta, compara la huella SHA-256 de ambos y abre la copia. Anota qué comprueba cada paso. Para un servicio real, la recuperación se prueba restaurando en un entorno separado. No cambies permisos, firewall ni servicios del NAS para este ejercicio.
- **¿Cuándo usarlo?** Comprueba la huella al transferir una copia y prueba la restauración antes de depender de ella.

En la restauración documentada de este HomeLab, la aplicación escaneó 142 archivos y se comprobó la lectura, escritura y eliminación con un archivo de control. No se comprobó uno por uno el contenido de los 142.

## 2. Ejecución manual y programada

- **¿Por qué?** Un ensayo manual no prueba que la tarea se inicie sola.
- **¿Para qué?** Para distinguir qué produjo el trabajo y si el horario configurado realmente lo activó.
- **¿Cómo?** Compara la hora del disparo programado con el resultado registrado y el archivo que produjo. [Ver los dos tipos de prueba](resultados-de-respaldo.md).
- **¿Cuándo usarlo?** Al configurar un horario nuevo o investigar si se ejecutó un respaldo concreto.


## 3. Leer el panel sin confundir una alerta con falta de datos

- **¿Por qué?** Un dispositivo puede funcionar aunque no haya enviado una lectura reciente.
- **¿Para qué?** Para decidir si hace falta atender un fallo o confirmar la lectura antes de actuar.
- **¿Cómo?** Abre la [captura de demostración](control-center.md#vista-del-aplicativo). Ubica la hora de captura y compara una advertencia con un estado desconocido. La advertencia aporta una señal que puedes investigar; el estado desconocido pide comprobar la fuente y su antigüedad antes de sacar conclusiones.
- **¿Cuándo usarlo?** Cuando falte un dato en el panel o aparezca una alerta que no sabes interpretar. La captura es un ejercicio: no necesitas acceder al NAS.

## 4. Leer una tendencia con huecos

- **¿Por qué?** Un intervalo sin lectura no dice si el valor fue alto, bajo o cero.
- **¿Para qué?** Para distinguir cobertura de comportamiento: el gráfico puede representar bien los datos que sí recibió sin contar toda la historia.
- **¿Cómo?** Imagina que pides 24 horas y solo hay 36 de 288 bloques de cinco minutos con datos. Describe la tendencia solo dentro de los bloques observados y anota que el resto está sin evaluar. [Ver cómo se agrupan las lecturas](control-center.md#cómo-se-lee-el-histórico).
- **¿Cuándo usarlo?** Cuando acabas de encender un monitor, detienes la captura o eliges un período mayor que el histórico disponible.
