# ⚙️ Documentación de Backend (API & Logic)

Este archivo describe la lógica de negocio, servicios y conexiones del servidor de aplicaciones.

## 1. Stack Tecnológico

* **Lenguaje:** Python v. (completar)
* **Framework:** Django v. / Django REST Framework v.
* **ORM:** GeoDjango (para soporte PostGIS)
* **Drivers de Conexión:**
    * PostgreSQL: `psycopg2-binary`
    * Oracle: `cx_Oracle` o `python-oracledb`

## 2. Configuración de Base de Datos
> **Estándar Obligatorio:** Todo campo relacionado con geografía debe seguir la nomenclatura `codigo_dane VARCHAR(5)`.

* **DB Principal (PostGIS):** Apunta a `10.40.111.108:5433`.
* **DWH (Oracle):** (Indicar IP y Servicio de conexión).

## 3. Endpoints Principales

| Ruta | Método | Descripción |
| :--- | :--- | :--- |
| `/api/v1/auth/` | POST | Gestión de tokens de acceso. |
| `/api/v1/layers/` | GET | Listado de capas geográficas disponibles. |
| `/api/v1/data/` | GET/POST | Interfaz de datos alfanuméricos. |

## 4. Procesos de Datos (ETL)

* **Servidor .132 (Data):** Describir aquí si este nodo maneja tareas programadas (Crons/Celery).
* **Truncamiento de Tablas:** (Indicar aquí el procedimiento para resetear índices y truncar tablas según el estándar definido).

## 5. Despliegue (Deployment)

* **Servidor WSGI/ASGI:** (ej. Gunicorn / Uvicorn)
* **Gestor de Procesos:** (ej. Systemd / Docker)
* **Comando de inicio:** `(Escribir el comando aquí)`
