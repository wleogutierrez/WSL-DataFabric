# 💻 Ecosistema de Desarrollo Web

El portal del **Data Fabric** no es solo un visor de datos; es una aplicación full-stack diseñada para la toma de decisiones.

---

## 1. Arquitectura de Referencia (Full-Stack)

Utilizamos un desacoplamiento entre el cliente (Frontend) y el servidor (Backend) para garantizar escalabilidad y mantenimiento independiente.
```mermaid
graph TD
    subgraph "Capa de Cliente (Frontend)"
        A[React App] -->|HTTPS / API| B(Nginx / Proxy)
    end

    subgraph "Capa de Aplicación (Backend)"
        B --> C[Django REST Framework]
        C --> D{Lógica de Negocio}
    end

    subgraph "Capa de Persistencia (Data)"
        D --> E1[(PostgreSQL / App DB)]
        D --> E2[(PostgreSQL + PostGIS / Spatial DB)]
        D --> F[Oracle DWH / Corporativo]
    end

    style A fill:#61dafb,stroke:#333,color:#000
    style C fill:#092e20,stroke:#333,color:#fff
    style E1 fill:#336791,stroke:#333,color:#fff
    style E2 fill:#4169E1,stroke:#333,color:#fff
    style F fill:#f80000,stroke:#333,color:#fff
```
