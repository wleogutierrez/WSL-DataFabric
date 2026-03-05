# 🏛️ Modelo de Operación y Colaboración Federada

Este documento define el marco de gobernanza estratégica para la interacción entre los dominios de datos y el Data Warehouse (DWH) central, priorizando la agilidad sin comprometer la integridad de la arquitectura institucional.

## 1. Marco de Trabajo entre Equipos
Para garantizar la agilidad que el negocio exige, se establece un modelo de **responsabilidad compartida**. Los equipos de origen (Data Domains) lideran la lógica de negocio y aseguran la calidad del dato, permitiendo que el DWH funcione como el gran orquestador de la verdad institucional y plataforma de exposición masiva.

## 2. Flujo de Entrega y Evolución Técnica
Para eliminar cuellos de botella operativos y mitigar riesgos de seguridad, se define el siguiente protocolo de integración:

* **Certificación en Origen (Fase Ágil):** El equipo de analítica entrega bases de datos ya transformadas y limpias en una **Zona de Staging Certificada**. Esto habilita la disponibilidad inmediata para el negocio, eliminando la dependencia de los ciclos de desarrollo de OBI para evolutivos urgentes.
* **Integración Progresiva a OBI:** Este modelo no sustituye la arquitectura centralizada. Se establece una hoja de ruta para la **migración paulatina de procesos hacia OBI**, la cual será atendida por el equipo de DWH conforme a su disponibilidad de recursos y priorización estratégica.
* **Mitigación de Riesgos:** El intercambio se realiza mediante interfaces de tablas estandarizadas (Data Contracts). No se requiere acceso directo a los sistemas core de Oracle por personal externo al equipo de DWH.

## 3. El Rol del Data Owner y el Comité de Datos
La infraestructura es provista por el Data Fabric, pero la inteligencia y las reglas de negocio son arbitradas por el **Comité de Datos** y los **Data Owners**, con enfoque en:

### A. Gestión y Evolución de KPIs
* **Definición de Nuevos Indicadores:** Antes de implementar un nuevo KPI, el comité debe validar su fórmula, fuente de origen y nomenclatura para evitar duplicidad o ambigüedad en el ecosistema.
* **Control de Cambios en Definiciones:** Cualquier ajuste en la lógica de un indicador existente (ej. cambio de umbrales en HCC o reglas de agregación) debe ser oficializado en este foro. Esto garantiza que el cambio se refleje simultáneamente en el contrato técnico, la documentación y el Agente de IA.

### B. Unificación de Conceptos y Estándares
* **Garantía de Interoperabilidad:** Asegurar que términos maestros como `msisdn` o `codigo_dane` mantengan una definición semántica y técnica única en todos los dominios de la compañía.
* **Supervisión de Evolutivos:** Aprobar la incorporación de nuevos atributos en los contratos de datos y supervisar la transición de estos procesos hacia la arquitectura final en OBI.

---

> 💡 **Nota de Gobernanza:** El Comité de Datos actúa como un facilitador para la toma de decisiones rápida, eliminando la burocracia operativa y asegurando que "una sola versión de la verdad" sea compartida por todas las áreas de la organización.
