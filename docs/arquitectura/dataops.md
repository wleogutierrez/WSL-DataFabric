# ♾️ Metodología DataOps
La agilidad y confiabilidad del **Data Fabric** se basan en principios de **DataOps**. Este enfoque garantiza que el ciclo de vida del dato sea automatizado, auditable y libre de errores manuales.

---

## 1. Ciclo de Vida y Calidad (Data Contracts)
A diferencia de los procesos ETL tradicionales, nuestro motor de procesamiento no ejecuta transformaciones a ciegas. 

* **Validación en Runtime:** El motor de Python consulta el archivo `specs/*.yaml` antes de procesar. Si el origen cambia un tipo de dato o desaparece una columna, el proceso se detiene antes de contaminar el DWH.
* **Consistencia Semántica:** El uso del **Glosario Central** asegura que un KPI (como HCC) signifique lo mismo en el reporte de red que en el **Site 360**.

---

## 2. Protocolos de Higiene Operativa
Para mantener la salud de los servidores de producción y el almacenamiento en **OCI**, aplicamos reglas estrictas de mantenimiento:


### 🧹 Gestión de Stage (Cleanup)

* **Regla:** Ningún archivo temporal (`.csv`, `.parquet`, `.tmp`) debe residir en el servidor post-ejecución.
* **Automatización:** El motor invoca una rutina de limpieza de la carpeta `stage/` tras cada confirmación de carga (Load Commit). Esto evita la degradación del sistema de archivos por acumulación de logs o temporales.

### 🔄 Integridad de Índices (Maintenance)
Para garantizar que las dimensiones y hechos (Facts) sean consistentes en recargas históricas:

* **Protocolo:** Uso mandatorio de `TRUNCATE` con `RESET IDENTITY` (o su equivalente según el motor SQL).
* **Objetivo:** Asegurar que las llaves subrogadas (**SK**) mantengan su integridad secuencial, evitando saltos de numeración innecesarios que dificulten la trazabilidad de los registros.

---

## 3. Resiliencia y Recuperación

### 📅 Estrategia de Particionamiento
El diseño de tablas contempla un **particionamiento por Día y sub-particionamiento por Hora**. 

* **Beneficio Operativo:** En caso de falla en una fuente de origen (ej. caída de un nodo de Nokia un martes a las 14:00), el equipo de DataOps puede reprocesar únicamente esa "rebanada" de tiempo sin afectar la disponibilidad del resto del mes.

### 🔤 Resolución de Entidades (Normalización)
Dado que los Site IDs pueden variar entre fabricantes (ZTE vs Huawei), el DataOps integra una capa de **Normalización Unicode NFKD**.

* Esto garantiza que la unión de datos (Joins) no dependa de la "limpieza manual" del origen, sino de una lógica programática estándar.

---

## 4. Observabilidad y Documentación Viva

* **Documentación como Código (MkDocs):** Este portal no es un documento estático; es la representación fiel del código en producción.
* **Transparencia:** Cualquier integrante de los grupos cross-funcionales puede consultar los contratos y protocolos de operación aquí definidos.
