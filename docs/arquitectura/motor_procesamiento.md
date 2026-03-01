# ⚙️ Ecosistema de Motores de Procesamiento

El **Data Fabric** de WOM utiliza un modelo híbrido para garantizar que el procesamiento de datos sea escalable, seguro y eficiente. 

---

## 1. Motores de Transformación (ETL/ELT)

### 🐍 Python Data Engine (Producción)
Motor principal para transformaciones complejas, normalización de texto y aplicación de contratos de datos.
* **Entorno de Producción:** Servidor Linux dedicado (Debian/Ubuntu) para ejecución programada de flujos.
* **Entorno de Ingeniería:** Uso de **WSL (Windows Subsystem for Linux)** como entorno de desarrollo local y gestión de documentación activa (**MkDocs**).
* **Gestión de Stage:** Protocolo mandatorio de limpieza de archivos temporales post-carga para optimizar el almacenamiento del servidor.

### 🏛️ Oracle Cloud Infrastructure (OCI / ADW)
Capa de persistencia y procesamiento de grandes volúmenes mediante SQL.
* **Eficiencia SQL:** Ejecución de agregaciones masivas directamente en el Autonomous Data Warehouse.
* **Integridad de Índices:** Uso del estándar **TRUNCATE & RESET IDENTITY** en procesos de recarga para mantener la coherencia de las llaves subrogadas (SK).

---

## 2. Estrategia de Almacenamiento y Particionamiento

Para soportar el alto volumen de datos de red (Radio) y asegurar tiempos de respuesta óptimos en Oracle, el diseño contempla:

* **Particionamiento por Día/Hora:** Implementado para permitir el *Partition Pruning*, asegurando que las consultas solo escaneen el segmento de tiempo necesario.
* **Normalización NFKD:** Aplicada en el motor de Python antes de la ingesta en el DWH para garantizar que la "Resolución de Entidades" (cruzar nombres de sitios) sea exacta.

---

## 3. Flujo de Trabajo (Lifecycle)

1. **Ingeniería (WSL):** Definición de contratos (YAML), glosarios y pruebas de scripts.
2. **Despliegue (Servidor):** Ejecución productiva de las ETLs con monitoreo de errores.
3. **Persistencia (OCI):** Disponibilidad de los datos en capas Silver/Gold para consumo políglota.

> 💡 **Nota Técnica:** Al separar el entorno de ingeniería del servidor de producción, garantizamos que la documentación y los contratos sean la "guía de navegación" antes de cualquier cambio en el entorno productivo.
