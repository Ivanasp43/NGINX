# 🕹️ Esquema de Red 🕹️

Un servidor web con dos tarjetas de red, una interna y otra externa, permite configurar una infraestructura más robusta y segura, optimizando la comunicación tanto hacia el exterior (Internet) como hacia la red interna. 
En este apartado vamos a configurar el esquema de red para el servidor Nginx en una máquina virtual basada en Debian. Esta elección se debe a varias razones técnicas y prácticas que aseguran un entorno óptimo para el despliegue de este servidor web.
A continuación, se detalla cómo se estructura y se utiliza este esquema de red en un servidor Nginx.

## Descripción del esquema

El servidor estará configurado con [dos interfaces de red](IMAGENES/red_interna_y_externa.png):

- Tarjeta de red externa (WAN): Conectada a Internet, recibe solicitudes externas desde clientes o usuarios finales. Esta tarjeta se utiliza para exponer servicios como sitios web y APIs públicas.  
- Tarjeta de red interna (LAN): Conectada a la red privada o corporativa. Facilita la comunicación con bases de datos, servicios de backend y otros sistemas internos, aislando esta comunicación del acceso externo.
  
### Objetivos del esquema de red

- Mejorar la seguridad, evitando que los sistemas internos sean accesibles desde internet.
- Optimizar el rendimiento, separando el tráfico externo del interno.
- Facilitar la escalabilidad, permitiendo agregar más servicios o servidores en la red interna.

## Configuración de las redes

Para configurar las dos redes, abriremos el archivo [***/etc/network/interfaces***](IMAGENES/configuracion_archivo_interfaces.png) y procederemos a modificarlo para que las dos redes sean efectivas. Le daremos a la red externa (NAT) una ip dinámica dhcp y la red externa una ip fija. Una vez configurado, procedemos a hacer un [***ip a***](IMAGENES/ip_a.png) para comprobar que tenemos perfectamente configuradas nuestras redes.

     
