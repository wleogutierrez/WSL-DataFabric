# 🤝 Gestión de Contratos de Datos (Data Contracts)

El **Data Fabric** opera bajo un modelo de responsabilidad compartida. Este documento define el marco técnico para formalizar las reglas de intercambio de información y garantizar la interoperabilidad entre los equipos de desarrollo y el Data Warehouse (DWH).

---

## 1. Filosofía del Contrato
Un **Data Contract** es el acuerdo de nivel de servicio (SLA) técnico entre el generador de datos y el consumidor. Asegura que la información sea:

* **Predecible:** El esquema (nombres de columnas y tipos) es inmutable; cualquier cambio debe ser versionado.
* **Confiable:** Los umbrales de calidad técnica y de negocio son validados automáticamente.
* **Agnóstica:** El estándar es independiente de la plataforma (Python, Spark u Oracle Cloud).

---

## 2. El Contrato como Certificación de Entrega
Para agilizar la integración con el DWH y responder a la velocidad del negocio, el contrato habilita un flujo de **Autoservicio Gobernado**:

1. **Auditoría Automática:** El motor de procesamiento valida los datos contra la especificación YAML antes de cualquier publicación.
2. **Zona de Intercambio (Staging):** Los datos certificados se depositan en una capa de interfaz, permitiendo el consumo inmediato por parte del negocio.
3. **Migración Progresiva:** El contrato actúa como la documentación técnica para que el equipo de DWH realice la ingesta formal en OBI de manera paulatina, eliminando errores de interpretación de la lógica de origen.

---

## 3. Gestión de Evolutivos Técnicos
El contrato permite que el ecosistema evolucione sin romper los procesos existentes:
* **Versionamiento:** Si un análisis requiere nuevas columnas, se actualiza la especificación técnica y se notifica a los consumidores.
* **Sincronización:** Garantiza que la "vista" del desarrollador y la del DWH sean idénticas en términos de estructura y formato.

---

> 💡 **Nota de Operación:** El cumplimiento del contrato es el requisito mandatorio para el paso a producción. Si un lote de datos no satisface la especificación técnica, el sistema lo deriva automáticamente a la zona de cuarentena para su corrección.
