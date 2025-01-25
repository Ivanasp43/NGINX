# 🕹️ Casos Prácticos 🕹️

# TAREA
Acabamos de terminar el CFGS ASIR y encuentramos trabajo en la empresa Servicios Web RC, SA en Huelva.  Anteriormente utilzaban Apache como servidor web y quiere migrar a Nginx. Una vez instalado y configurado procedemos a realizar todos los casos prácticos solicitados.

[A- Versión de Nginx instalado](). Abriremos un terminal en el servidor donde está instalado Nginx y procedemos a ejecutar el comando ***nginx -v***

B- Servicio asociado. Verificamos que el servicio de Nginx esté configurado correctamente y en ejecución con [***systemctl status nginx***](). Esto muestra si el servicio está activo, habilitado al inicio y si hay errores recientes. 

- Para gestionar el servicio tenemos los siguientes comandos:
  
      - Inciar Nginx: ***sudo systemctl start nginx***
      - Detener Nginx: ***sudo systemctl stopr nginx***
      - Reiniciar Nginx: ***sudo systemctl restart nginx***
      - Recargar la configuración sin detener el servicio: ***sudo systemctl reload nginx***

C- Inspeccionar los ficheros de configuración. la ubicación predeterminada de los archivos es la de [***/etc/nginx***](). Con un ls podemos ver todos los archivos que componen la configuración de Ngnix. Entre ellos el archivo principal es el [***nginx.conf***]().
  
D- Modificación de la [página web por defecto](). Para personalizar la página que lanza Nginx por defecto, lo que haremos será modificar el archivo [***/var/www/html/index.nginx-debian.html***]().

E- Virtual Hosting. Nuestro servidor ofrecerá 2 sitios web. Para dicha configuración, seguiremos los siguientes pasos:
    [- Creación de los directorios]() de cada sitio web con el comando ***mkdir*** y su ruta correspondiente.
    - Asignamos los [permisos]() necesarios con los comandos ***chown*** y ***chmod***.
    - Creamos las páginas index.html para cada sitio con el editor de texto en la ruta [***/var/www/web(x)/index.html***](), añadiendo el contenido que queremos que se vea en la red.
     [- Creamos los archivos sites-available]() con el editor de texto para cada sitio, proporcionándoles el nombre del dominio, el directorio raíz, el puerto, los protocolos y cualquier configuración específica. Se trata del archivo en donde se almacenan las configuraciones individuales de cada sitio web. Cada vez que modificamos este archivo tendremos que aplicar los cambios con ***sudo systemctl reload nginx***
     - Creamos enlaces simbólicos en el [directorio sites-enabled](), archivo donde se seleccionan las configuraciones que estarán activas.
     - Configuramos el [archivo hosts]() para pruebas locales] con ***sudo nano /etc/hots***
     [- Resultado final](). Hacemos las comprobaciones en el navegador accediendo con ***http://www.web(x).org***.
     
  F- Autenticación, Autorización y control de acceso. www.web1.org puede acceder desde la red externa y la red interna, pero wwww.web2.org sólo puede acceder desde la red interna. Los pasos a seguir son:
      - Configuración del [archivo sites-available]() de cada uno.
      - Configuración del [archivo hosts]() Añadimos las ip correspondientes a la red interna y la red externa.
      [- Comprobación de ambas en la red interna](). Utilizaremos el comando ***curl --interface enp0s8 hhttp//www.web(x).org***
      [- Comprobación de ambas en la red externa]()
      
  G- Autenticación, Autorización y Control de acceso. www.web1.org contiene un directorio privado al que sólo pueden acceder usuario válidos. Pasos:
      - Creación directorio privado con un mensaje. Primero crearemos el direcorio para web1 con el comando mkdir y posteriormente le añadiremos con el editor de texto un fichero index.html con el mensaje correspondiente.***sudo mkdir /var/www/web1/privado*** y ***sudo nano /var/www/web1/privado/index.html*** 
      - Instalamos el paquete ***apache2-utils***  y procedemos a crear un archivo para guardar las credenciales de usuarios con ***sudo htpasswd -c /etc/nginx/.htpasswd usurio1***.
      - Abrimos de nuevo el archivo [sites-available de web1](), y lo configuramos para la nueva restrincción.
      [- Comprobación]() 
      
  H- Autenticación, Autorización y Control de acceso. www.web1.or contiene un directorio llamado privado. Desde la red externa pide autorización y desde la interna no. Pasos:
      - Configuramos el archivo [sites-available]() de web1
      - Vuelvo a crear una nueva credencial a un nuevo usuario con ***sudo htpasswd -c /etc/nginx/.htpasswd usurio***.
      - Comprobaciones: [Desde la red externa]() [Desde la red interna]()
      
  I- Seguridad. Configuración del sitio virtual www.web1 para que el sitio sea seguro. Como lo vamos a hacer desde una red privada en vez de pública, haremos los siguientes pasos:
      - Generamos un [certificado autofirmado]() con el comando ***sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/selfsigned.key -out /etc/ssl/certs/selfsigned.crt***
      - Modificamos el archivo [sites-available]() de web1.
      [- Comprobación]()
