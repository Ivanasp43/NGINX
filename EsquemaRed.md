# 🕹️ Esquema de Red 🕹️

Un servidor web con dos tarjetas de red, una interna y otra externa, permite configurar una infraestructura más robusta y segura, optimizando la comunicación tanto hacia el exterior (Internet) como hacia la red interna. A continuación, se detalla cómo se estructura y se utiliza este esquema de red en un servidor Nginx.

## Descripción del esquema

El servidor estará configurado con dos interfaces de red:

- Tarjeta de red externa (WAN): Conectada a Internet, recibe solicitudes externas desde clientes o usuarios finales. Esta tarjeta se utiliza para exponer servicios como sitios web y APIs públicas.
  
- Tarjeta de red interna (LAN): Conectada a la red privada o corporativa. Facilita la comunicación con bases de datos, servicios de backend y otros sistemas internos, aislando esta comunicación del acceso externo.
  
### Objetivos del esquema de red

- Mejorar la seguridad, evitando que los sistemas internos sean accesibles desde internet.

- Optimizar el rendimiento, separando el tráfico externo del interno.

- Facilitar la escalabilidad, permitiendo agregar más servicios o servidores en la red interna.

                             Internet (WAN)
                                 │
                     ┌────────────▼─────────────┐
                     │      Servidor Nginx      │
                     │ ┌─────────────────────┐  │
                     │ │ Tarjeta Externa     │  |
                     │ │ IP: xx              │  │
                     │ └─────────────────────┘  │
                     │ ┌─────────────────────┐  │
                     │ │ Tarjeta Interna     |  |
                     │ │ IP: xx              │  │
                     │ └─────────────────────┘  │
                     └────────────▲─────────────┘
                                  │
                          Red Interna (LAN)
         ┌────────────────────────┴────────────────────────┐
         │                                                 │
 ┌─────────────┐                                   ┌─────────────┐
 |Base de datos│                                   │   Backend   │
 │  (MySQL)    │                                   │ (API REST)  │
 │ IP: xx      |                                   |  IP: xx     |
 └─────────────┘                                   └─────────────┘
