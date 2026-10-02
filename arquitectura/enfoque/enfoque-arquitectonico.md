# Estilo Arquitectónico

## Descripción
Se selecciona el estilo **Monolito Modular con Arquitectura en Capas** para la estructura global del sistema[cite: 4, 8].

* **Monolito Modular:** Representa la unidad de despliegue principal en un solo proceso ejecutable[cite: 4, 9].
* **Capas Lógicas:** Divide el sistema internamente en Presentación, Lógica de Negocio y Datos[cite: 9].

## Diagrama del Estilo Arquitectónico

```mermaid
graph TD
    subgraph Cliente
        C[Cliente Web / Móvil]
    end

    subgraph Monolito Marketplace Backend
        subgraph Middlewares Express
            M[Auth JWT / Validaciones / Logger]
        end

        subgraph Capa de Presentación
            P1[Módulo Usuarios]
            P2[Módulo Sellers]
            P3[Módulo Catálogo]
            P4[Módulo Carrito]
            P5[Módulo Pedidos]
        end

        subgraph Capa de Lógica de Negocio
            L1[usuarios.service]
            L2[sellers.service]
            L3[catalogo.service]
            L4[carrito.service]
            L5[pedidos.service]
        end

        subgraph Capa de Datos
            D1[usuarios.repository]
            D2[sellers.repository]
            D3[catalogo.repository]
            D4[carrito.repository]
            D5[pedidos.repository]
        end
    end

    subgraph Sistemas Externos
        EXT1[Pasarela de Pagos]
        EXT2[Servicio de Envíos]
    end

    subgraph Base de Datos
        DB[(PostgreSQL)]
    end

    C -->|HTTPS / REST| M
    M --> P1 & P2 & P3 & P4 & P5
    P1 --> L1
    P2 --> L2
    P3 --> L3
    P4 --> L4
    P5 --> L5

    L1 --> D1
    L2 --> D2
    L3 --> D3
    L4 --> D4
    L5 --> D5

    L5 -->|HTTPS / REST| EXT1
    L5 -->|HTTPS / REST| EXT2

    D1 & D2 & D3 & D4 & D5 -->|SQL| DB
```
