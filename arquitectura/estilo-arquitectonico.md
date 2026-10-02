# Enfoque Arquitectónico: Clean Architecture

## Resumen del Enfoque

| Elemento | Descripción aplicada al Marketplace |
| :--- | :--- |
| **Patrón / Enfoque arquitectónico** | Clean Architecture (Arquitectura Limpia). |
| **Objetivo** | Separar responsabilidades y controlar las dependencias hacia el dominio. |
| **¿Qué problema resuelve?** | Evita el acoplamiento entre la interfaz Angular, las reglas del negocio y las tecnologías externas (bases de datos, API y servicios de pago). |
| **Capas definidas** | Presentación, Aplicación, Dominio e Infraestructura. |
| **Beneficios** | • Facilita el mantenimiento y las pruebas unitarias.<br>• Permite cambiar implementaciones técnicas sin modificar las reglas de negocio.<br>• Mejora la organización y separación de responsabilidades del código. |

## Diagrama de Clean Architecture (GoPet Marketplace)

```mermaid
graph TD
    subgraph Adaptadores y Frameworks - Angular
        subgraph Presentación
            UI1[CatalogoComponent]
            UI2[DetalleCarrito]
            UI3[CarritoComponent]
            UI4[AppComponent]
        end

        subgraph Aplicación - Casos de Uso
            UC1[ConsultarCatalogoUseCase]
            UC2[AgregarAlCarritoUseCase]
            UC3[RegistrarCompraUseCase]
        end

        subgraph Dominio - Core / Reglas de Negocio
            subgraph Modelos
                E1[Producto]
                E2[Carrito]
                E3[Pedido]
            end
            subgraph Contratos / Puertos
                R1[RepositorioProducto]
                R2[RepositorioPedido]
                R3[ProcesadorPagos]
                R4[NotificadorCliente]
            end
        end

        subgraph Infraestructura
            I1[RepositorioProductoMemoria]
            I2[RepositorioPedidoMemoria]
            I3[ProcesadorPagosSimulado]
            I4[NotificadorConsole]
        end
    end

    subgraph Sistemas Externos
        API[Marketplace API REST]
    end

    UI1 & UI2 & UI3 --> UC1 & UC2 & UC3
    UC1 & UC2 & UC3 --> E1 & E2 & E3
    UC1 & UC2 & UC3 --> R1 & R2 & R3 & R4

    I1 -.->|Implementa| R1
    I2 -.->|Implementa| R2
    I3 -.->|Implementa| R3
    I4 -.->|Implementa| R4

    I1 & I2 & I3 & I4 -->|HTTP / REST| API
```
