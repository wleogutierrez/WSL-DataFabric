# 🤝 Gobernanza y Contratos de Datos (Data Contracts)

El **Data Fabric** de WOM opera bajo un modelo de responsabilidad compartida. Este documento define el marco de trabajo para formalizar las reglas de negocio y garantizar la interoperabilidad entre equipos.

---

## 1. Filosofía de los Contratos de Datos
Un **Data Contract** es un acuerdo técnico y funcional entre los generadores de datos y sus consumidores. Usamos el término en plural porque cada dominio de información (Red, Comercial, Valor de Cliente) posee su propia especificación técnica.

El contrato asegura que la data sea:
* **Predecible:** El esquema (columnas y tipos) no cambia sin aviso.
* **Confiable:** Los umbrales de calidad definidos por el negocio son respetados.
* **Agnóstica:** El estándar se cumple sin importar si el motor es SQL, Python o Spark.

---

## 2. El Rol del Data Owner (Negocio)
El Data Fabric provee la infraestructura, pero los **Data Owners** son los encargados de dictar las reglas de oro:
1. **Definición de KPIs:** Validación de fórmulas y umbrales (ej. las 150h para HCC).
2. **Lineamientos de Calidad:** Identificación de campos obligatorios.
3. **Validación de Resultados:** Aprobación de la lógica antes de su exposición en **Site 360**.

---

## 3. Implementación Políglota
El contrato actúa como un **Lenguaje Universal**. No importa si un equipo trabaja en Oracle Cloud (SQL) y otro en servidores Linux (Python); ambos deben cumplir la especificación definida en los archivos de contrato (`specs/*.yaml`). 

Esto permite que grupos cross-funcionales colaboren sin fricciones tecnológicas.

---

> 💡 **Nota de Presentación:** Este modelo permite que el ecosistema crezca orgánicamente. A medida que nuevos dominios se integren, los Data Owners solo deben "firmar" su contrato técnico para entrar al flujo de calidad automatizado.
