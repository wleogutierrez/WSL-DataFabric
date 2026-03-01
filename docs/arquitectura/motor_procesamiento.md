# ⚙️ Motor de Procesamiento y Pipeline de Datos

El **Data Fabric** de WOM utiliza un ecosistema políglota donde el procesamiento se distribuye estratégicamente entre motores de transformación en Python y la capacidad de cómputo de Oracle Cloud.

---

## 1. Motores de Transformación (ETL/ELT)

### 🐍 Python Data Engine (Producción)
Es el motor principal para transformaciones complejas, normalización de texto y aplicación de contratos de datos.

* **Entorno de Producción:** Servidor Linux dedicado (Debian/Ubuntu) para la ejecución programada de flujos de alta disponibilidad.
* **Entorno de Ingeniería:** Uso de **WSL (Windows Subsystem for Linux)** como entorno de desarrollo local, pruebas de scripts y gestión de documentación activa (**MkDocs**).
* **Gestión de Stage:** Implementación del protocolo mandatorio de limpieza de archivos temporales post-carga para optimizar el almacenamiento del servidor y mantener la higiene del sistema.

### 🏛️ Oracle Cloud Infrastructure (OCI / ADW)
Capa de persistencia y procesamiento masivo mediante SQL para grandes volúmenes de datos.

* **Eficiencia SQL:** Ejecución de agregaciones pesadas directamente en el Autonomous Data Warehouse para minimizar el movimiento de datos.
* **Integridad de Índices:** Uso del estándar **TRUNCATE & RESET IDENTITY** en procesos de recarga para mantener la coherencia secuencial de las llaves subrogadas (SK) y la integridad referencial.

---

## 2. Flujo Lógico de Procesamiento (Data Pipeline)

Nuestra arquitectura actúa como un "Gatekeeper" de calidad, asegurando que solo los datos que cumplen con el **Data Contract** lleguen a las capas analíticas:

```mermaid
graph LR
    A[Fuentes Multi-Vendor] --> B(Python Engine / WSL)
    B -->|Valida Contrato| C{¿Data Limpia?}
    C -->|No| D[Log de Error / Alerta]
    C -->|Sí| E[Oracle Cloud / DWH]
    E --> F[Site 360 / OBI]
    
    style B fill:#f96,stroke:#333,color:#000
    style E fill:#0f9,stroke:#333,color:#000
    style C fill:#fff,stroke:#333,color:#000
    style D fill:#ff4d4d,stroke:#333,color:#fff
```
