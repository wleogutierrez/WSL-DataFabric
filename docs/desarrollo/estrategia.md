# 🗺️ Estrategia de Desarrollo y Escalabilidad

El portal de **Data Fabric** sigue una filosofía de **"Simplicidad Evolutiva"**. Priorizamos la entrega de valor inmediata sobre la sobreingeniería inicial.

---

## 1. Arquitectura: Monolito Modular

Hemos optado por un **Monolito Modular** basado en Django, ejecutado en servidores **On-Premise**.

### ¿Por qué esta elección?
* **Velocidad de Desarrollo:** Un solo repositorio facilita la gestión de tipos, esquemas de base de datos y autenticación.
* **Baja Latencia Interna:** Al estar en servidores On-Premise, la comunicación entre el Front, el Back y las bases de datos PostgreSQL es directa y optimizada.
* **Coherencia de Datos:** Compartimos el motor de validación de **Data Contracts** en un solo lugar.

### Hoja de Ruta de Escalabilidad (Roadmap)
Si un módulo específico (ej. el motor de cálculo de Rentabilidad o el procesador de Mapas) incrementa su carga significativamente:
1. **Identificación:** Monitoreo de recursos en el servidor On-Premise.
2. **Desacoplamiento:** Extracción de la lógica hacia un **Microservicio** independiente.
3. **Contenerización Estricta:** Uso de Docker para aislar el nuevo servicio sin afectar al resto del portal.

---

## 2. Infraestructura On-Premise

Operamos sobre infraestructura física propia para garantizar el control total de los datos de red.

| Componente | Entorno | Especificación Técnica |
| :--- | :--- | :--- |
| **Backend** | VM Dedicada | Django / Gunicorn / Nginx |
| **Frontend** | VM Dedicada | React (Build estático servido por Nginx) |
| **Persistencia** | Docker Containers | PostgreSQL 15 + PostGIS (Extensión Espacial) |
| **Red** | Interna WOM | Segmentación de IPs para comunicación Front-Back |

---

## 3. Ciclo de Vida del Código (GitLab)

Utilizamos **GitLab** no solo como repositorio, sino como el orquestador de nuestra calidad:

1. **Branching:** `main` (Producción), `develop` (Pruebas).
2. **Validación:** Antes de cada Merge, se verifica que los cambios no rompan la estructura del `codigo_dane` ni los contratos de integración.
3. **Deployment:** Proceso manual/semiautomático hacia las VMs de destino mediante SSH/Docker-Compose.

> 💡 **Principio de Diseño:** "Construye para hoy, diseña para mañana". Nuestra estructura modular permite que el portal crezca orgánicamente sin deuda técnica inmanejable.
