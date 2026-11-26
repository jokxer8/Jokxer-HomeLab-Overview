<div align="center">

<h1 align="center"><img src="assets/readme-banners/homelab-publico.svg" alt="Jokxer HomeLab · Laboratorio tecnológico en casa" width="100%"></h1>

### NAS, nube privada y recuperación de datos

Caso práctico de infraestructura doméstica: qué implementé, qué probé y qué sigue pendiente.

![Sistema: Debian 13](https://img.shields.io/badge/Sistema-Debian%2013-1E3A5F?style=for-the-badge)
![Restauración: Incremental validada](https://img.shields.io/badge/Restauraci%C3%B3n-Incremental%20validada-176754?style=for-the-badge)
![Imágenes Docker: 3 protegidas](https://img.shields.io/badge/Docker-3%20im%C3%A1genes%20protegidas-176754?style=for-the-badge)
![Automatización: Programada](https://img.shields.io/badge/Automatizaci%C3%B3n-Programada-94520B?style=for-the-badge)

[🏠 Proyecto](#el-proyecto) · [✅ Resultados](#resultados-verificables) · [🧰 Infraestructura](#infraestructura-desplegada) · [🗺️ Catálogo de servicios](#catálogo-de-servicios) · [🗂️ Evidencia y alcance](resultados-de-respaldo.md) · [🌐 Hosting y portal](hosting-web.md) · [📍 Próxima etapa](#siguiente-etapa)

**Ruta de lectura:** [Plan Maestro](PLAN-MAESTRO.md) · [En palabras simples](EN-PALABRAS-SIMPLES.md)

</div>

**Tecnologías en uso:** Debian y Docker para la nube privada, Tailscale para el acceso autorizado, Cloudflare Tunnel para la portada pública del portal y Resend para correo transaccional. [Qué hace cada herramienta](PLAN-MAESTRO.md#tecnologías-y-para-qué-las-uso).

## El proyecto

Jokxer HomeLab es un laboratorio doméstico orientado a aprender administración de sistemas, almacenamiento, redes, contenedores, nube privada y recuperación ante fallos. Se desarrolla sobre una Dell reutilizada con Debian 13, priorizando estabilidad, seguridad y las herramientas disponibles.

El trabajo ya cubre mucho más que la instalación inicial: el NAS comparte archivos, Nextcloud sincroniza con Windows, Tailscale habilita acceso privado, Docker ejecuta los servicios y ya cuenta con un proceso de respaldo implementado y pruebas de recuperación documentadas.

> **Ensayo de recuperación externa · 25 de noviembre de 2026.** La copia independiente se restauró en un entorno aislado. El escaneo recorrió 142 archivos en 24 carpetas sin errores; se verificaron descarga autenticada con contenido idéntico, escritura con comprobación del contenido y eliminación del archivo de prueba. Esto no mide el tiempo de recuperación ni verifica todos los archivos individualmente.

## Resultados verificables

**Corte: 26 de noviembre de 2026 · paso 842.3.** El primer respaldo diario de Nextcloud tras los ajustes se ejecutó automáticamente. En hosting, verifiqué una recuperación de muestra, una copia independiente recibida en Windows y la salida HTTPS de la primera portada de terceros. [Ver portada provisional](https://mukien.jokxer.dev/).

| Hito | Resultado comprobado | Alcance |
|---|---|---|
| Recuperación desde copia independiente | **142 archivos en 24 carpetas**, sin errores de escaneo; descarga, escritura y eliminación autenticadas | Entorno aislado y archivo de control; no se verificó cada archivo individualmente |
| Protección de dependencias Docker | **3 de 3 imágenes** respaldadas e importadas; **36 de 36 capas únicas** verificadas con SHA-256 | Importación en el host existente, no recuperación desde cero |
| Respaldo programado | Primer respaldo diario de Nextcloud validado tras los ajustes; tarea de Windows ensayada de forma asistida | Faltan los disparos programados del hosting y las exportaciones semanales |

[Ver las pruebas, sus límites y los siguientes hitos](resultados-de-respaldo.md).

## Infraestructura desplegada

El HomeLab tiene dos equipos. **Debian** concentra almacenamiento, Nextcloud, respaldos, hosting y servicios ligeros. **AnduinOS** queda asignado a servidores de juegos, virtualización, IA local y multimedia; la asignación no equivale a que todos esos servicios estén desplegados.

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

## Catálogo de servicios

El catálogo reúne **16 iniciativas: 3 operativas, 1 implementada, 2 en validación y 10 planificadas**. Este recuento se limita al catálogo y no reemplaza el inventario técnico.

| Servicio | Propósito | Estado |
|---|---|---|
| Nube privada Nextcloud | Archivos y sincronización | 🟢 Operativo |
| Sistema de respaldos | Protección y recuperación | 🟢 Implementado |
| Acceso remoto Tailscale | Conectividad privada segura | 🟢 Operativo |
| Docker | Infraestructura de contenedores | 🟢 Operativo |
| Hosting web multiproyecto | Alojar páginas web propias y de terceros | 🟡 Piloto validado |
| [Primer sitio web de terceros](https://mukien.jokxer.dev/) | Portal académico alojado en el NAS | 🟡 Portada provisional publicada |
| Servidor SFTP | Transferencia segura de archivos | 🔵 Planificado |
| Biblioteca de videojuegos | Catálogo y descarga privada | 🔵 Planificado |
| Servidor multimedia | Películas, música y fotografías  (AnduinOS) | 🔵 Planificado |
| Gestor de documentos | Digitalización y clasificación | 🔵 Planificado |
| Servidores de videojuegos | Minecraft y otros juegos compatibles  (AnduinOS) | 🔵 Planificado |
| Bases de datos | Aplicaciones y proyectos de desarrollo | 🔵 Planificado |
| Inteligencia artificial local | Modelos y asistentes privados  (AnduinOS) | 🔵 Planificado |
| Máquinas virtuales | Laboratorios y experimentación  (AnduinOS) | 🔵 Planificado |
| Monitorización centralizada | Rendimiento y disponibilidad | 🔵 Planificado |
| Portal de servicios Jokxer | Administración y acceso centralizado | 🔵 Planificado |

El primer respaldo diario de Nextcloud ya está validado. El hosting multiproyecto tiene un piloto y una primera portada provisional de terceros; aún no representa una plataforma multiproyecto en producción. MariaDB ya funciona para Nextcloud; ofrecer bases de datos a otros proyectos sigue planificado. El portal central Jokxer sigue planificado y no es la portada académica.

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
- El primer disparo diario posterior a los ajustes terminó con éxito el 26 de noviembre. Se verificaron SHA-256 y salida del modo de mantenimiento. La exportación semanal y la recepción asistida se validan por separado.
- Se verificaron copias independientes en Windows con SHA-256, BitLocker y permisos restrictivos. La retención separa las ventanas semanales y mensuales de la copia histórica protegida.
- Se corrigió la reexportación para poder regenerar la misma instantánea sin cambiar el archivo comprimido en el caso probado. El receptor conserva el control de integridad y evita duplicados.
- Se respaldaron y volvieron a importar las imágenes de Nextcloud, MariaDB y Redis. Las imágenes y los datos se conservan por separado.

### 4. Piloto de hosting y primer portal

- Nginx sirvió el sitio de muestra y la portada de la Dra. Mu-kien Sang Ben. Solo la portada provisional se publicó por el túnel HTTPS; Nextcloud siguió privado.
- El sitio de muestra se restauró en Nginx aislado con HTTP 200 y contenido idéntico. El respaldo integral que incluye la portada provisional llegó a Windows con SHA-256 coincidente, en una ejecución asistida.
- Se validó y aplicó la recarga atómica del firewall conservando las reglas de acceso. El sondeo desde el cliente Windows autorizado confirmó conectividad TCP a SSH y HTTPS por la red local; los servicios internos ensayados permanecieron aislados. [Resultados de hosting](hosting-web.md) · [Caso del portal](https://github.com/jokxer8/Portal-Mukien-Sang-Ben-Overview).

## Cómo verifico los respaldos

![Flujo de respaldo y verificación de Nextcloud y Docker](assets/flujo-verificacion-respaldos.svg)

1. **Debian:** genera las copias internas y aplica la retención.
2. **Exportación:** al regenerar la misma instantánea en la prueba, el archivo conservó su SHA-256.
3. **Windows:** recibe la copia con autenticación asistida, verifica su integridad y aplica la retención.

**Pruebas por separado:** la restauración de datos se hizo en un entorno aislado con una copia anterior. Las tres imágenes Docker se importaron en el host existente y se verificaron 36 capas. [Ver resultados y límites](resultados-de-respaldo.md).

## Decisiones de seguridad y estabilidad

- **Acceso privado:** Nextcloud se mantiene dentro de la LAN y Tailscale; no se publica directamente en Internet ni se abren puertos WAN para el servicio.
- **Mínimo acceso:** el firewall mantiene reglas restrictivas y SMB/NFS quedan para redes privadas.
- **Pruebas aisladas:** la restauración se valida en un entorno separado para reducir el riesgo a los datos de producción.
- **Autenticación:** las cuentas de Nextcloud tienen TOTP y códigos de recuperación configurados; el correo saliente tuvo una prueba exitosa.
- **Almacenamiento protegido:** no se modifica el particionado ni los volúmenes LVM del SSD Kingston de 2 TB.
- **Disco de laboratorio:** el HDD de 1 TB, con antecedente de sectores pendientes, no se usa para información crítica ni como copia fiable.
- **Privacidad de publicación:** no se incluyen credenciales, claves, tokens, direcciones internas ni identificadores de los discos.

## Siguiente etapa

1. Confirmar el primer respaldo diario de hosting, los disparos de ambas exportaciones semanales y sus recepciones asistidas en Windows.
2. Restaurar Nextcloud en un entorno aislado desde el nuevo formato reproducible y medir el tiempo hasta verificar el acceso.
3. Ensayar la recuperación completa en un host vacío y evaluar una copia fuera de la ubicación física.

Las validaciones de permisos SMB/NFS, diagnóstico del disco de laboratorio, monitorización y nuevos servicios conservan su alcance anterior.

## Documentación y alcance

[Portada provisional de la Dra. Sang Ben](https://mukien.jokxer.dev/) · [Caso del portal](https://github.com/jokxer8/Portal-Mukien-Sang-Ben-Overview)

[Resultados de respaldo](resultados-de-respaldo.md) · [Volver al HomeLab en el perfil de Jokxer8](https://github.com/jokxer8#homelab-y-nas)

La bitácora operativa no forma parte de la publicación. Este resumen no incluye direcciones, rutas internas, identificadores, bitácoras en bruto ni secretos.
