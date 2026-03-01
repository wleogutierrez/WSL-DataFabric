# 📏 Estándares Técnicos de Ingeniería de Datos

Este documento detalla las reglas de transformación y mantenimiento que deben aplicar todos los motores de procesamiento para asegurar la integridad operativa del Data Fabric.

---

## 1. Normalización de Campos Descriptivos (Higiene de Texto)
Para asegurar que los cruces de datos (Joins) sean exactos y evitar fallas en las cargas masivas (Bulk Load) al DWH, se aplican las siguientes reglas:

* **Sanitización de Delimitadores (Crítico):** * Se eliminan obligatoriamente comas (`,`) y puntos y coma (`;`) de los campos de texto.
    * *Justificación:* Evita el desplazamiento de columnas en procesos de carga masiva donde la coma es el delimitador base, previniendo errores de ingesta en Oracle Cloud.
* **Protocolo Unicode (NFKD):** Eliminación de acentos, tildes y caracteres especiales.
* **Estandarización:** Transformación a **MAYÚSCULAS** y eliminación de espacios dobles o saltos de línea.

## 2. Estándar Geográfico (DANE)
Para garantizar la compatibilidad con el inventario comercial y mapas:
* **Formato:** El campo `codigo_dane` debe ser siempre `VARCHAR(5)`.
* **Tratamiento:** Si el origen tiene 4 dígitos, se realiza un relleno con cero a la izquierda (Zero-padding).

## 3. Protocolos de Mantenimiento (DataOps 2026)
Reglas de oro para la salud de los servidores y la base de datos:

### Integridad de Índices
* En procesos de carga inicial o reprocesos históricos, es obligatorio ejecutar un `TRUNCATE` seguido de un **Reset de las Llaves de Identidad (SK)**. Esto mantiene la coherencia secuencial de los índices.

### Gestión de Carpeta Stage
* Los archivos temporales (`.csv`, `.parquet`) en la zona de aterrizaje deben ser eliminados inmediatamente después de confirmada la carga. La permanencia de datos transitorios en el servidor está prohibida.

### Estructura de Almacenamiento
* Las tablas de alta volumetría deben implementar un **particionamiento por Día** y un **sub-particionamiento por Hora** para optimizar el rendimiento de las consultas y la recuperación ante fallos.
