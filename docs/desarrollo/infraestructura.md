# 🛠️ Detalles de Infraestructura Técnica

Este documento consolida el inventario de recursos, configuraciones de bajo nivel y la evaluación de resiliencia del ecosistema **Data Fabric**.

## 1. Inventario de Servidores (Nodos Rocky Linux)

El ecosistema se distribuye en cinco nodos dedicados, garantizando capacidad de cómputo para el procesamiento de datos y la ejecución del Agente de IA.

| Dirección IP | Finalidad | Recursos | Sistema Operativo |
| :--- | :--- | :--- | :--- |
| **10.40.111.130** | Frontend Dev | 12 CPUs / 30GB RAM | Rocky Linux |
| **10.40.111.131** | Backend Env | 12 CPUs / 30GB RAM | Rocky Linux |
| **10.40.111.132** | Backend Data | 12 CPUs / 30GB RAM | Rocky Linux |
| **10.40.111.133** | Data Testing | 12 CPUs / 30GB RAM | Rocky Linux |
| **10.40.111.108** | **Hub de Datos** | Host de Base de Datos | Linux |

## 2. Hub Central de Datos: PostgreSQL + PostGIS

La persistencia de datos está centralizada en el servidor `digitalizacion02` (`10.40.111.108`), el cual actúa como host de contenedores.

### A. Especificaciones del Contenedor

* **Nombre del Contenedor**: `postgres_saf`
* **Imagen Base**: `postgis/postgis:16-3.4-alpine` (PostgreSQL 16.4 / PostGIS 3.4.3)
* **Puerto de Acceso**: **`5433`** (Mapeado al puerto `5432` interno del contenedor)
* **Red Docker**: `dockerdata_saf_net` (IP interna: `172.18.0.2`)
* **Hostname Interno**: `a6ff7529f39f`

### B. Persistencia y Volúmenes (Bind Mounts)
Para garantizar la integridad de la información, se utilizan rutas físicas en el host mapeadas al contenedor:

* **Datos**: `/data/dockerdata/postgres/data` -> `/var/lib/postgresql/data`
* **Logs**: `/data/dockerdata/postgres/logs` -> `/var/log/postgresql`
* **Backups**: `/data/dockerdata/postgres/backups` -> `/backups`
* **Scripts Init**: `/data/dockerdata/postgres/init` -> `/docker-entrypoint-initdb.d`

## 3. Variables de Entorno y Seguridad
La conexión se realiza mediante las siguientes credenciales técnicas:

* **Base de Datos Principal**: `saf_data`
* **Usuario Propietario**: `collector_dg`
* **Mantenimiento de Logs**: Rotación automática de 5 archivos de máximo 50MB cada uno.

