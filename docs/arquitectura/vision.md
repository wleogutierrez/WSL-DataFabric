# 🌐 Visión: Data Fabric Políglota

El **Data Fabric** de WOM no es una herramienta cautiva, sino un ecosistema abierto. Entendemos que diferentes equipos tienen diferentes *stacks* técnicos y accesos.

## 1. Independencia Tecnológica
Nuestro diseño permite que los grupos cross-funcionales consuman y aporten datos usando sus herramientas de preferencia:
* **Ingeniería de Datos:** Python (Pandas/Polars) sobre WSL.
* **Analítica & BI:** SQL puro sobre el DWH, Power BI o Tableau.
* **Data Science:** Notebooks en R o Databricks.

## 2. El Contrato como Lenguaje Universal
La clave de este modelo políglota es el **Data Contract (YAML)**. 
* No importa si el proceso se escribió en **Java** o en **SQL**; el resultado final en la capa Silver debe cumplir con el contrato definido (ej. `codigo_dane VARCHAR(5)` y limpieza de `stage`).
* El contrato asegura que, aunque usemos lenguajes distintos, el **Site 360** reciba datos siempre con la misma estructura y calidad.
