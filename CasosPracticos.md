# 🕹️ Casos Prácticos 🕹️

# TAREA
Acabamos de terminar el CFGS ASIR y encuentramos trabajo en la empresa Servicios Web RC, SA en Huelva.  Anteriormente utilzaban Apache como servidor web y quiere migrar a Nginx. Una vez instalado y configurado procedemos a realizar todos los casos prácticos solicitados.

## A- [Versión](imagenes/versionnginx.png) de Nginx instalado

Abriremos un terminal en el servidor donde está instalado Nginx y procedemos a ejecutar el comando ***nginx -v***.


## B- Servicio asociado

Verificamos que el servicio de Nginx esté configurado correctamente y en ejecución con [***systemctl status nginx***](imagenes/estatusgnix.png). Esto muestra si el servicio está activo, habilitado al inicio y si hay errores recientes. 

- Para gestionar el servicio tenemos los siguientes comandos:
  
      - Inciar Nginx: ***sudo systemctl start nginx***
      - Detener Nginx: ***sudo systemctl stopr nginx***
      - Reiniciar Nginx: ***sudo systemctl restart nginx***
      - Recargar la configuración sin detener el servicio: ***sudo systemctl reload nginx***
  

## C- Inspeccionar los ficheros de configuración

La ubicación predeterminada de los archivos es la de [***/etc/nginx***](imagenes/ficherosgnginx.png). Con un ls podemos ver todos los archivos que componen la configuración de Ngnix. Entre ellos el archivo principal es el [***nginx.conf***](imagenes/ficheronginx.conf.png).

  
## D- Modificación de la [página web](imagenes/paginawebModificada.png)

Para personalizar la página que lanza Nginx por defecto, lo que haremos será modificar el archivo [***/var/www/html/index.nginx-debian.html***](imagenes/htmlPaginaPrincipal.png).


## E- Virtual Hosting

Nuestro servidor ofrecerá 2 sitios web. Para dicha configuración, seguiremos los siguientes pasos:<br>   
    1- [Creación de los directorios](imagenes/mkdirweb.png) de cada sitio web con el comando ***mkdir*** y su ruta correspondiente.<br>   
    2- Asignamos los [permisos](imagenes/permisosweb.png) necesarios con los comandos ***chown*** y ***chmod***.<br>  
    3- Creamos las páginas index.html para cada sitio con el editor de texto en la ruta [***/var/www/web(x)/index.html***](imagenes/htmlwebs.png), añadiendo el contenido que queremos que se vea en la red.<br>  
     4- [Creación de los archivos sites-available](imagenes/sitesavilable1.png) con el editor de texto para cada sitio, proporcionándoles el nombre del dominio, el directorio raíz, el puerto, los protocolos y cualquier configuración específica. Se trata del archivo en donde se almacenan las configuraciones individuales de cada sitio web. Cada vez que modificamos este archivo tendremos que aplicar los cambios con ***sudo systemctl reload nginx***.<br>  
     5- Creamos enlaces simbólicos en el [directorio sites-enabled](imagenes/sites-enabled.png), archivo donde se seleccionan las configuraciones que estarán activas.<br>  
     6- Configuramos el [archivo hosts](imagenes/hots1.png) para pruebas locales] con ***sudo nano /etc/hots***.<br>  
     7- [Resultado final](imagenes/web1yweb2.png). Hacemos las comprobaciones en el navegador accediendo con ***http://`www.web(x).org`***.
     
     
  ## F- Autenticación, Autorización y control de acceso  
  
  `www.web1.org` puede acceder desde la red externa y la red interna, pero `wwww.web2.org` sólo puede acceder desde la red interna. Los pasos a seguir son:<br>  
      1- Configuración del [archivo sites-available](imagenes/sites-availableF.png) de cada uno.<br>  
      2- Configuración del [archivo hosts](imagenes/hotsF.png) Añadimos las ip correspondientes a la red interna y la red externa.<br>  
      3- [Comprobación](imagenes/comprobacionredinternaF.png) de ambas en la red interna. Utilizaremos el comando ***curl --interface enp0s8 hhttp//`www.web(x).org`***.  <br>  
      4- [Comprobación](imagenes/redexternaF.png) de ambas en la red externa.  
      
      
  ## G- Autenticación, Autorización y Control de acceso  
  
  `www.web1.org` contiene un directorio privado al que sólo pueden acceder usuario válidos. Pasos:  <br>   
      1- Creación directorio privado con un mensaje. Primero crearemos el direcorio para web1 con el comando mkdir y posteriormente le añadiremos con el editor de texto un fichero index.html con el mensaje correspondiente.***sudo mkdir /var/www/web1/privado*** y ***sudo nano /var/www/web1/privado/index.html***.  <br>   
      2- Instalamos el paquete ***apache2-utils***  y procedemos a crear un archivo para guardar las credenciales de usuarios con ***sudo htpasswd -c /etc/nginx/.htpasswd usurio1***.  <br>     
      3- Abrimos de nuevo el archivo [sites-available de web1](imagenes/sitesavailableG.png), y lo configuramos para la nueva restrincción.  <br>  
      4- [Comprobación](imagenes/ComprobaciónG.png)   
      
      
  ## H- Autenticación, Autorización y Control de acceso  
  
  `www.web1.org` contiene un directorio llamado privado. Desde la red externa pide autorización y desde la interna no. Pasos:  <br>  
      1- Configuramos el archivo [sites-available](imagenes/sitesAvailableH.png) de web1.  <br>      
      2- Vuelvo a crear una nueva credencial a un nuevo usuario con ***sudo htpasswd -c /etc/nginx/.htpasswd usurio***.  <br>  
      3- Comprobaciones: [Desde la red externa](imagenes/ComprobaciónredexternaH.png) [Desde la red interna](imagenes/ComprobacionRedInternaH.png).  <br>  
      
  ## I- Seguridad  
  
  Configuración del sitio virtual `www.web1` para que el sitio sea seguro. Como lo vamos a hacer desde una red privada en vez de pública, haremos los siguientes pasos:<br>  
      1- Generamos un [certificado autofirmado](imagenes/generarCertificado.png) con el comando ***sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/selfsigned.key -out /etc/ssl/certs/selfsigned.crt***.<br>  
      2- Modificamos el archivo [sites-available](imagenes/sites-available-I.png) de web1.  <br>  
      3- [Comprobación](imagenes/Comprobación_I.png).  <br>  
