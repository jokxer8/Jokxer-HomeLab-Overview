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

> **Estado al 25 de noviembre de 2026:** el HomeLab ya superó una restauración incremental aislada y una prueba de recuperación tras interrumpir un respaldo y reiniciar el NAS. También se guardó y verificó una copia independiente. El primer ciclo programado falló por coincidir con una tarea de mantenimiento. Quedan por validar la corrección y la restauración desde esa copia externa.

## Resultados verificables

| ✅ Restauración incremental | ✅ Copia independiente | 🟡 Respaldo programado |
|---|---|---|
| Instancia aislada y operaciones de lectura y escritura comprobadas. | Integridad SHA-256 confirmada; restauración pendiente. | Ejecución manual correcta; falta un ciclo programado exitoso. |

## Infraestructura desplegada

| Área | Implementación | Estado |
|---|---|---|
| Sistema base | Debian 13 en una Dell reutilizada | Operativo |
| NAS | Compartición de archivos SMB/NFS | Servicios desplegados; validación final de permisos desde clientes pendiente |
| Contenedores | Docker y Docker Compose | Activos; los datos de Docker se mantienen en un volumen de servicios |
| Nube personal | Nextcloud 34.0.6 con MariaDB y Redis | Operativo en la última prueba; restauración incremental validada |
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

- El ciclo de respaldo comprueba la integridad con SHA-256, impide ejecuciones simultáneas y evita escribir cuando faltan montajes requeridos.
- Se validó una **restauración incremental aislada**: se restauraron la base de datos y los archivos, y se probaron descarga, escritura y eliminación sin alterar producción.
- Se interrumpió un respaldo de forma controlada y se reinició el NAS. La recuperación devolvió Nextcloud a funcionamiento normal y no dejó una recuperación pendiente.
- El ciclo terminó correctamente al iniciarlo manualmente mediante systemd. La programación diaria está habilitada; la primera ejecución disparada por el temporizador no completó el respaldo. La corrección está en validación.
- Se guardó una **copia independiente del NAS** y se comprobó con SHA-256. La integridad del archivo no sustituye una prueba de restauración desde esa copia.

## Decisiones de seguridad y estabilidad

- **Acceso privado:** Nextcloud se mantiene dentro de la LAN y Tailscale; no se publica directamente en Internet ni se abren puertos WAN para el servicio.
- **Mínimo acceso:** el firewall mantiene reglas restrictivas y SMB/NFS quedan para redes privadas.
- **Pruebas aisladas:** la restauración se valida en un entorno separado para reducir el riesgo a los datos de producción.
- **Autenticación:** las cuentas de Nextcloud tienen TOTP y códigos de recuperación configurados; el correo saliente tuvo una prueba exitosa.
- **Almacenamiento protegido:** no se modifica el particionado ni los volúmenes LVM del SSD Kingston de 2 TB.
- **Disco de laboratorio:** el HDD de 1 TB, con antecedente de sectores pendientes, no se usa para información crítica ni como copia fiable.
- **Privacidad de publicación:** no se incluyen credenciales, claves, tokens, direcciones internas ni identificadores de los discos.

## Siguiente etapa

1. Comprobar que la corrección permite que el ciclo programado complete un respaldo.
2. Ensayar la restauración desde la copia independiente, en un entorno aislado.
3. Revisar avisos de seguridad y actualizaciones de Nextcloud con una reversión preparada.
4. Validar permisos SMB/NFS desde los equipos cliente y el acceso remoto tras reinicios.
5. Diagnosticar el disco de laboratorio de 1 TB cuando cierre esta fase.

Los servicios futuros —monitorización, snapshots, virtualización y nuevos servidores— son objetivos posteriores, no instalaciones actuales.

## Documentación y alcance

La bitácora técnica y los procedimientos de operación se mantienen en el repositorio privado. Este resumen recoge los resultados y las decisiones que se pueden compartir.
