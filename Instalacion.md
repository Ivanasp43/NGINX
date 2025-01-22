# 🕹️ Instalación de Nginx 🕹️

La instalación de Nginx varía dependiendo del sistema operativo y de las necesidades específicas del entorno en el que se desplegará. A continuación, se detallan los pasos principales para instalar Nginx en los sistemas operativos más comunes, junto con algunos consejos prácticos para configurarlo correctamente.

## Instalación en Sistemas Basados en Linux Ubuntu/Debian

1- Actualizar sistema. Antes de instalar cualquier paquete, es recomendable actualizar los repositorios con:

  - ***sudo apt update***
    
  - ***sudo apt upgrade***
    
2- Instalamos Nginx utilizando el gestor de paquetes APT:

  - ***Sudo apte install nginx***
    
3- Una vez instalado, activamos y verificamos que Nginx está funcionando:

  - ***sudo systemctl start nginx***
    
  - ***sudo systemctl enable nginx***
    
  - ***sudo systemctl status nginx***
    
4- Como algo opcional podemos configurarmos el cortafuegos con sudo ufw allow 'Nginx Full'.

5- Configuración básica de Nginx. La configuración principal de Nginx se encuentra en el archivo  ***/etc/nginx/nginx.conf***. Sin embargo, la configuración específica de los sitios web se maneja en archivos separados ubicados en ***/etc/nginx/sites-available/*** y ***/etc/nginx/sites-enabled/***.


## Instalación en Sistemas Basados en Windows

Aunque Nginx no es comúnmente utilizado en sistemas Windows, es posible instalarlo y ejecutarlo.

1- Descargar el paquete con la versión compatible con Windows desde el sitio oficial de Nginx.

2- Extraer el contenido del archivo Zip en la ubicación seleccionada.

3- Ejecutamos Nginx desde el CMD con el comando ***start nginx***

## Verificación de la instalación

Independientemente del método de instalación, puedes comprobar que Nginx está funcionando correctamente abriendo un navegador y accediendo a:

- http://localhost en un entorno local.
  
- La dirección IP o el dominio asociado al servidor en un entorno remoto.
  
Veremos  una página predeterminada de bienvenida de Nginx. Si no aparece, tendremos que revisar los registros de errores del servidor ubicados en ***/var/log/nginx/error.log*** o el equivalente en tu sistema operativo.

## Resumen

Hemos repasao el proceso de instalación de Nginx en los sistemas operativos Windows y Linux. Siguiendo los pasos descritos para tu plataforma específica, ahora deberías tener una instalación de Nginx en funcionamiento, lista para gestionar tus tareas de servidor web y proxy inverso.
Te animo a que empieces a utilizar Nginx para tus aplicaciones web, ya que ofrece un rendimiento, una escalabilidad y una flexibilidad excelentes. A medida que sigas trabajando con Nginx, encontrarás una gran cantidad de recursos disponibles en línea para ayudarte a aprender más y a solucionar cualquier problema que puedas encontrar. La documentación oficial de Nginx es un buen punto de partida, así como diversos foros y blogs de la comunidad.

Por último, si buscas una solución de alojamiento fiable para tus aplicaciones basadas en Nginx, te recomendamos Kinsta Application Hosting. Kinsta proporciona un entorno de alojamiento gestionado de alto rendimiento optimizado para Nginx, que garantiza que tus aplicaciones funcionen sin problemas y de forma segura.


  
