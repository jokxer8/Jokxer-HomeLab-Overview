<div align="center">

### Jokxer HomeLab · NAS · nube privada · servicios propios

**Un laboratorio doméstico desarrollado por etapas sobre hardware reutilizado, con foco en aprender, operar y recuperar servicios de forma segura.**

![Proyecto](https://img.shields.io/badge/proyecto-HomeLab-2563eb?style=for-the-badge)
![Estado](https://img.shields.io/badge/estado-recuperaci%C3%B3n%20y%20hardening%20en%20curso-f59e0b?style=for-the-badge)
![Actualizado](https://img.shields.io/badge/estado-documentado%2024--11--2026-334155?style=for-the-badge)

[🧭 Proyecto](#visión) · [🧰 Servicios](#infraestructura-implementada) · [📈 Avances](#avances-recientes) · [🗺️ Próximos pasos](#siguiente-tramo) · [🔒 Privacidad](#seguridad-y-privacidad)

</div>

## Visión

Jokxer HomeLab es un proyecto práctico de infraestructura personal. Construyo y administro un NAS, una nube privada y servicios de laboratorio en una Dell reutilizada con Debian 13. El desarrollo avanzó desde la instalación del sistema y los discos hasta sincronización entre equipos, acceso remoto cifrado y automatización de respaldos y recuperación.

La documentación separa lo desplegado de lo que aún se está probando. **La fase actual se concentra en demostrar que Nextcloud y sus datos se pueden recuperar antes de ampliar el laboratorio.**

## Infraestructura implementada

- Debian 13, SSH, Ethernet y firewall nftables con política restrictiva.
- Almacenamiento en red con SMB/NFS para uso privado.
- Docker y Docker Compose para servicios persistentes.
- Nextcloud Hub 26 Spring 34.0.6, con MariaDB y Redis.
- Nginx para HTTPS local y Tailscale/Serve para acceso remoto privado.
- Sincronización Nextcloud en Windows con una única cuenta y carpeta, usando archivos bajo demanda.
- Sitios web sencillos de laboratorio.
- UPnP desactivado en el router. Nextcloud no se publica directamente en Internet ni requiere puertos públicos.

## Avances recientes

### Datos y sincronización

Se probó la sincronización en ambos sentidos entre Windows y Nextcloud. En la comparación de un conjunto restaurado se revisaron **67 archivos (63 MiB)**. Se encontró una diferencia en un archivo de prueba que fue editado en producción después de crear la copia; esa diferencia quedó explicada y no se confundió con una falla general de restauración.

### Respaldo y recuperación

- Se generó un respaldo de MariaDB de **929 KB** y otro de archivos/configuración de **403 MB**.
- La automatización ya incorpora verificación SHA-256, bloqueo de ejecuciones simultáneas, coordinación con las tareas programadas y protección ante montajes requeridos ausentes.
- Se ensayó recuperación coordinada con systemd y se preparó una instancia temporal aislada, limitada en recursos y sin puertos publicados.
- La restauración SQL terminó en el paso 262. El paso 263 verificará las tablas de la base restaurada.
- **La restauración integral aún no está cerrada:** falta completar una simulación de interrupción del respaldo, reiniciar Nextcloud de forma controlada y comprobar la aplicación y sus dependencias.
- Las copias actuales están en el propio NAS. Todavía falta establecer una copia independiente que cubra la pérdida del equipo.

## Decisiones de seguridad

- Acceso a Nextcloud solo por LAN/Tailscale, sin exposición pública directa.
- Firewall con reglas mínimas; administración y SMB/NFS se mantienen privados.
- Autenticación TOTP y códigos de recuperación configurados para las cuentas. El correo saliente tuvo una prueba exitosa.
- Separación de las pruebas de restauración para no alterar datos de producción.
- El SSD Kingston de 2 TB y su LVM actual se conservan sin reformatear, reparticionar ni redimensionar.
- El disco de laboratorio de 1 TB tuvo sectores pendientes en una lectura SMART previa; no se destina a datos críticos ni se considera copia fiable.
- Secretos, direcciones internas, identificadores de discos y detalles de acceso se omiten de esta publicación.

## Siguiente tramo

1. Completar el paso 263 y documentar las tablas restauradas.
2. Terminar la prueba de interrupción y recuperación del respaldo.
3. Reiniciar Nextcloud de forma controlada y verificar aplicación, base de datos, Redis, tareas, HTTPS local y Tailscale.
4. Completar el ensayo de recuperación de base de datos, archivos y configuración.
5. Definir y comprobar una copia independiente del NAS.
6. Revisar los avisos y actualizaciones de Nextcloud con evidencia actual y una reversión preparada.
7. Cerrar pruebas de SMB/NFS y reconexión de Tailscale tras reinicio.
8. Diagnosticar el disco de laboratorio solo después de completar la prioridad Nextcloud.

## Documentación

El [repositorio privado Jokxer-HomeLab](https://github.com/jokxer8/Jokxer-HomeLab) conserva la bitácora técnica, arquitectura, inventario, decisiones, fases y controles de recuperación.

## Seguridad y privacidad

Este repositorio resume el proyecto y sus decisiones sin publicar credenciales, claves, tokens, direcciones internas, UUID, datos personales ni procedimientos de acceso sensibles. Los servicios futuros —como monitorización, VMs y nuevos servidores— siguen siendo objetivos y no se describen como instalados.