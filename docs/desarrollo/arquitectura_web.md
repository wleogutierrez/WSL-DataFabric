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

    %% Estilos para Fondos Claros y Texto Negro Legible
    style A fill:#E1F5FE,stroke:#01579B,color:#000
    style B fill:#F5F5F5,stroke:#616161,color:#000
    style C fill:#E8F5E9,stroke:#2E7D32,color:#000
    style D fill:#FFFDE7,stroke:#FBC02D,color:#000
    style E1 fill:#E3F2FD,stroke:#1565C0,color:#000
    style E2 fill:#EDE7F6,stroke:#4527A0,color:#000
    style F fill:#FFEBEE,stroke:#C62828,color:#000
```
