<div align="center">

<h1 align="center"><img src="assets/readme-banners/homelab-publico.svg" alt="Jokxer HomeLab · Laboratorio tecnológico en casa" width="100%"></h1>

### NAS · nube privada · contenedores · acceso remoto seguro

**Un HomeLab real, construido por etapas sobre hardware reutilizado y documentado con sus avances, decisiones y límites.**

![Plan](https://img.shields.io/badge/plan-v2.5-7c3aed?style=for-the-badge)
![Sistema](https://img.shields.io/badge/sistema-Debian%2013-2563eb?style=for-the-badge)
![Estado](https://img.shields.io/badge/estado-recuperaci%C3%B3n%20en%20validaci%C3%B3n-f59e0b?style=for-the-badge)
![Privacidad](https://img.shields.io/badge/acceso-privado%20por%20Tailscale-059669?style=for-the-badge)

[🏠 El proyecto](#el-proyecto) · [🧰 Qué está desplegado](#infraestructura-desplegada) · [📈 Avances](#avances-que-ya-se-realizaron) · [🔐 Decisiones](#decisiones-de-seguridad-y-estabilidad) · [🗺️ Siguiente etapa](#siguiente-etapa)

</div>

## El proyecto

Jokxer HomeLab es un laboratorio doméstico orientado a aprender administración de sistemas, almacenamiento, redes, contenedores, nube privada y recuperación ante fallos. Se desarrolla sobre una Dell reutilizada con Debian 13, priorizando estabilidad, seguridad y las herramientas disponibles.

El trabajo ya cubre mucho más que la instalación inicial: el NAS comparte archivos, Nextcloud sincroniza con Windows, Tailscale habilita acceso privado, Docker ejecuta los servicios y se está construyendo un proceso repetible de respaldo y restauración.

> **Estado al 24 de noviembre de 2026:** la fase prioritaria es cerrar la recuperación de Nextcloud. El paso 262 completó la restauración SQL; el paso 263 verificará las tablas restauradas. En el último estado reportado, la aplicación Nextcloud estaba detenida mientras MariaDB y Redis seguían activos. Falta completar la prueba de interrupción y hacer un reinicio controlado antes de declarar el servicio recuperado.

## Infraestructura desplegada

| Área | Implementación | Estado |
|---|---|---|
| Sistema base | Debian 13 en una Dell reutilizada | Operativo |
| NAS | Compartición de archivos SMB/NFS | Servicios desplegados; validación final de permisos desde clientes pendiente |
| Contenedores | Docker y Docker Compose | Activos; los datos de Docker se mantienen en un volumen de servicios |
| Nube personal | Nextcloud 34.0.6 con MariaDB y Redis | Instalado; recuperación integral en validación |
| Acceso web | HTTPS local con Nginx y acceso remoto privado con Tailscale/Serve | Probado; no publicado directamente en Internet |
| Sincronización | Cliente oficial de Nextcloud en Windows, una cuenta y una carpeta | Sincronización bidireccional y archivos bajo demanda probados |
| Red | Ethernet y firewall nftables | Validados; reglas de acceso mínimas |
| Laboratorio web | Páginas sencillas para pruebas | Activas para experimentación |

## Avances que ya se realizaron

### 1. Base del NAS y almacenamiento

Se instaló Debian 13, se configuró la administración por SSH y se dejó el equipo operativo por Ethernet. El SSD Kingston de 2 TB usa LVM para el sistema, los servicios y los datos. Docker quedó separado en su área de servicios. Un disco externo de 5 TB aloja los datos de Nextcloud y existe un volumen aparte para el laboratorio.

La distribución del SSD está en uso y se conserva sin reformatear, reparticionar ni redimensionar. El disco de laboratorio de 1 TB registró sectores pendientes en una lectura SMART previa y no se considera adecuado para datos críticos.

### 2. Servicios y sincronización

Se desplegaron SMB/NFS, Docker, Nextcloud, MariaDB, Redis y páginas web de prueba. Se comprobó el acceso HTTPS local y el acceso remoto mediante la red privada Tailscale. En Windows se probó la navegación, apertura, carga y sincronización en ambos sentidos utilizando una sola cuenta y una sola carpeta.

### 3. Respaldos y recuperación de Nextcloud

- Se generó un respaldo de la base de datos de **929 KB** y otro de archivos/configuración de **403 MB**.
- La automatización incluye comprobaciones SHA-256, bloqueo de ejecuciones simultáneas, coordinación con las tareas programadas y controles para evitar escribir cuando faltan montajes requeridos.
- Se preparó una restauración temporal aislada, con límites de recursos y sin puertos publicados, para proteger la instancia de producción durante las pruebas.
- Se comparó un conjunto restaurado de **67 archivos (63 MiB)**. La diferencia detectada corresponde a un archivo de prueba que se modificó en producción después de crear el respaldo.
- La restauración SQL terminó en el paso 262; el paso 263 debe revisar la estructura de tablas.
- La recuperación coordinada por systemd se probó parcialmente. La simulación de interrupción, el reinicio controlado y la validación final de la aplicación siguen pendientes.
- Los respaldos actuales están guardados en el NAS. Hace falta una copia independiente para cubrir la pérdida del equipo.

Estos resultados muestran avances concretos, pero **crear y verificar respaldos no equivale todavía a demostrar una recuperación completa**.

## Decisiones de seguridad y estabilidad

- **Acceso privado:** Nextcloud se mantiene dentro de la LAN y Tailscale; no se publica directamente en Internet ni se abren puertos WAN para el servicio.
- **Mínimo acceso:** el firewall mantiene reglas restrictivas y SMB/NFS quedan para redes privadas.
- **Pruebas aisladas:** la restauración se valida en un entorno separado para reducir el riesgo a los datos de producción.
- **Autenticación:** las cuentas de Nextcloud tienen TOTP y códigos de recuperación configurados; el correo saliente tuvo una prueba exitosa.
- **Almacenamiento protegido:** no se modifica el particionado ni los volúmenes LVM del SSD Kingston de 2 TB.
- **Disco de laboratorio:** el HDD de 1 TB, con antecedente de sectores pendientes, no se usa para información crítica ni como copia fiable.
- **Privacidad de publicación:** no se incluyen credenciales, claves, tokens, direcciones internas ni identificadores de los discos.

## Siguiente etapa

1. Completar el paso 263 y registrar el resultado de las tablas restauradas.
2. Terminar la simulación de interrupción del respaldo.
3. Reiniciar Nextcloud de forma controlada y comprobar aplicación, base de datos, Redis y acceso privado.
4. Completar el ensayo integral de recuperación de base de datos, archivos y configuración.
5. Establecer y probar una copia independiente del NAS.
6. Revisar el estado actual de seguridad y las actualizaciones de Nextcloud con una reversión preparada.
7. Validar permisos SMB/NFS desde los equipos cliente y el acceso remoto tras reinicios.
8. Diagnosticar el disco de laboratorio de 1 TB cuando la fase de Nextcloud esté cerrada.

Los servicios futuros —monitorización, snapshots, virtualización y nuevos servidores— son objetivos posteriores, no instalaciones actuales.

## Documentación y alcance

El [repositorio privado Jokxer-HomeLab](https://github.com/jokxer8/Jokxer-HomeLab) contiene la bitácora técnica, el inventario, la arquitectura, las decisiones, las fases y los procedimientos detallados. Este README resume el progreso público sin divulgar datos operativos sensibles.