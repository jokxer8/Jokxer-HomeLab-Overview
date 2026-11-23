<div align="center">

<h1 align="center"><img src="assets/readme-banners/homelab-publico.svg" alt="Laboratorio tecnológico en casa (Home Technology Lab)" width="100%"></h1>

### Aprender · experimentar · construir servicios propios

**Un HomeLab operativo, desarrollado por etapas en equipos reutilizados y con herramientas gratuitas.**

![Proyecto](https://img.shields.io/badge/proyecto-laboratorio-2563eb?style=for-the-badge)
![Estado](https://img.shields.io/badge/estado-servicios%20activos%20y%20hardening-f59e0b?style=for-the-badge)
![Alcance](https://img.shields.io/badge/documentaci%C3%B3n-resumen%20p%C3%BAblico-334155?style=for-the-badge)

[🧭 Visión](#visión) · [🧰 Servicios](#servicios-implementados) · [🗺️ Ruta](#próximas-etapas) · [🔒 Privacidad](#privacidad-del-proyecto)

</div>

## Visión

Este laboratorio explora cómo construir y proteger servicios domésticos sobre hardware reutilizado. El trabajo incluye instalación del servidor, almacenamiento, administración remota, nube privada, contenedores y alojamiento web básico. Cada servicio se añade gradualmente y se documentan sus límites y tareas pendientes.

## Servicios implementados

La Dell reutilizada ejecuta **Debian 13** y actualmente ofrece:

- Almacenamiento en red mediante SMB y NFS.
- Acceso SSH para administración.
- Nube privada con Nextcloud, accesible por la red privada Tailscale.
- Docker y Docker Compose para alojar servicios.
- Páginas web sencillas de laboratorio.
- Firewall activo y conectividad Ethernet validada.

Tailscale permite el acceso remoto privado probado. La activación automática del cliente en Windows y la recuperación de los datos siguen pendientes. SMB y NFS se mantienen fuera de Internet.

## Estado al 23 de noviembre de 2026

| Área | Estado |
|---|---|
| Sistema base y almacenamiento | Debian 13 y LVM operativos; diseño del SSD existente se conserva |
| NAS y nube | SMB/NFS y Nextcloud desplegados; permisos y copias en validación |
| Contenedores y web | Docker activo y páginas de laboratorio disponibles |
| Acceso remoto | Tailscale probado; inicio automático de Windows pendiente |
| Nextcloud | Servicio operativo; endurecimiento y revisión de configuración en curso |
| Servicios futuros | Snapshots, monitoreo, proxy inverso y VMs siguen planificados |

El disco externo de 5 TB está preparado como volumen de datos de nube. La ubicación de la copia previa del disco de 1 TB y su restauración deben comprobarse antes de depender de esos datos.

## Próximas etapas

1. Confirmar y ensayar la restauración de los datos de respaldo.
2. Validar permisos SMB/NFS desde los equipos cliente.
3. Completar el endurecimiento y las copias de Nextcloud.
4. Automatizar el inicio de Tailscale en Windows.
5. Ampliar los servicios después de verificar seguridad y recuperación.

El desarrollo técnico completo está en el [repositorio privado Jokxer-HomeLab](https://github.com/jokxer8/Jokxer-HomeLab).

## Privacidad del proyecto

Este repositorio ofrece un resumen público. Las direcciones de red, identificadores de equipos, claves, credenciales, reglas detalladas y procedimientos de administración permanecen fuera de esta página. Los servicios futuros indicados como planificados aún no están desplegados.