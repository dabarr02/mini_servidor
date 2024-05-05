# Como crear un mini servidor en casa

## Material
* MiniPc, raspberry pi o similares con ubuntu/debian instalado.
* Discos duros.
* Un segundo dispositivo (o una pantalla, teclado y ratón conectados al dispositivo del servidor).

>:memo: **Nota:** Al MiniPC/raspberry lo llamaremos **Servidor** y al segundo dispositivo lo llamaremos **Auxiliar**.

## CasaOS
CasaOs es una especie de sistema operativo en la nube, código abierto, que se basa en la tecnología Docker para ofrecer una experiencia similar a la de un SO convencional pero que se accede a traves de un navegador web. Esto nos será muy útil ya que facilita mucho la gestión de contenedores, que usaremos más adelante, además de la gestión de archivos en remoto, ya que ofrece una interfaz bastante sencilla de entender y utilizar.
Desde su página oficial se pude probar una versión Demo : [casaos.io](https://casaos.io)

## Instalación de CasaOS
Tenemos dos formas de instalar CasaOS.

### Desde el Servidor
En este caso lo único que tenemos que hacer es :

1. Abrir la terminal (en el caso que hallamos instalado una versión con escritorio)
2. Introducir el siguiente comando:

        curl -fsSL https://get.casaos.io | sudo bash

### Desde el Auxiliar (SSH)
Para este caso es necesario que conozcamos la dirección IP de nuestro Servidor.
### Buscar dirección IP
Para ello utilizamos una herramienta como [Advanced IP Scanner](https://www.advanced-ip-scanner.com/es/), aunque se puede utilizar cualquier herramienta de este estilo.
Una vez instalado en Auxiliar y estando conectados en la misma red que el Servidor buscamos la IP de este y la guardamos.

![Ejempl IP Scanner](/Imagenes/Ip_Scanner.png "Ejemplo IP Scanner")

*Ejemplo Advanced IP Scanner*

Ahora que tenemos la dirección IP tenemos que conectarnos al Servidor de manera remota, para ello hacemos lo siguiente :

1. Abrir una ventana de terminal en Auxiliar.
2. Introducimos el siguiente comando:

        ssh usuario@IP.Servidor
    Donde :
    
    * usuario: Es el usuario que usamos en Servidor
    * IP.Servidor: Es la dirección IP del servidor que hemos apuntado antes.

    Ejemplo (con usuario : Prueba e IP : 192.168.0.102):
            
            ssh Prueba@192.168.0.102
3. Introducimos la contraseña del usuario (*Prueba*, en el ejemplo) del Servidor.

Establecida la conexión, lo que tenemos en nuestra terminal es una sesión remota del Servidor y todos los comandos que escribamos aquí es como si los estuviesemos escribiendo en una terminal del propio Servidor.

Con la conexión establecida introducimos el siguiente comando :

    curl -fsSL https://get.casaos.io | sudo bash

Cuando termine las instalación nos saldrá algo parecido a esto:

![Instalación CasaOS](/Imagenes/Casaos_install.png)

*Fuente:*  https://www.instructables.com/Casa-OS-With-Raspberry-Pi/

Donde nos dice la dirección Ip del Servidor (debería ser la misma que apuntamos) desde la que podemos acceder desde un navegador.

En el caso de que queramos desinstalar CasaOS podemos introducir el siguiente comando :

    casaos-uninstall

## Configurar CasaOS

Al acceder a la dirección Ip del Servidor por primera vez nos aparecerá la siguiente ventana :

![Welcome Casaos](/Imagenes/casaos_welcome.png)


*Fuente:* https://www.instructables.com/Casa-OS-With-Raspberry-Pi/

Aquí tendremos que elegir un nombre de usuario y una contraseña para acceder a nuestro Servidor desde CasaOS, este usuario y contraseña pueden (y deben) ser diferentes del usuario y contraseña de inicio de sesión de *habitual* del Servidor. Con este sencillo paso ya tenemos CasaOS listo para usarse.

## Instalar *aplicaciones*

En CasaOS el equivalente de las aplicaciones son los contenedores. Para instalar las aplicaciones predeterminadas solo tenemos que pulsa en el icono que pone *App Store* y se nos desplegara la siguiente ventana :

![Tienda de aplicaciones](/Imagenes/AppStore_CasaOS.png)

Desde la que podemos buscar e instalar algunas aplicaciones "pre-configuradas".
Acontinuación veremos algunos ejemplos de instalación y configuración.

### FileBrowser

FileBrowser es una explorador de archivos que incluye funciones para compartir archivos que terceros de forma temporal. Para instalarlo simplemente lo buscamos en la *App Store* y pulsamos la opción de instalar.

>El usuario por defecto es : ***admin*** y la contraseña: ***admin***, con lo que es recomendable cambiarlo una vez que hayas iniciado sesion por primera vez.

Si FileBrowser no detecta los discos conectados por usb o algún disco duro extra que este instalado en Servidor tendremos que hacer la siguiente configuración, esto lo tendremos que hacer para todas las aplicaciones que queramos que tengan acceso a estos discos duros extras.

### Añadir discos extra

Con la aplicación ya instalada nos vamos a la ventana de inicio, buscamos el icono de la aplicación y pulsamos en los tres puntitos que aparecen al poner el cursor sobre el icono y clicamos en la opción de ajustes. Aparecerá la siguiente ventana :

![Configuración FIleBrowser](/Imagenes/FileBrowser_conf.png)

1. En la seccion de sección de volumenes pulsamos en *Añadir*
2. En el apartado de anfitrión tenemos que poner la ruta donde está montado el usb/disco extra, para que esto sea más fácil se pude pulsar en el icono cuadrado de la caja de texto y navegar por el explorador de archivos hasta encontrar el disco que queremos añadir.
3. En el apartado de Contendedor tenemos que poner lo siguiente :
    >/srv/Destino
    
    Donde **Destino** es el nombre que tendra la carpeta donde estará montado el usb/disco extra dentro de la aplicación. (En el ejemplo se llamará usbs).
4. Pulsamos en Guardar.

Ahora al abrir la aplición nos debería aparacer una carpeta con el nombre **Destino** (**usbs** en el ejemplo).

![usbs montado](/Imagenes/File_USB.png)

Tal y como tenemos configurado el Servidor ahora podriamos acceder a él solo si estamos conectados a la misma red y compartir nuestros archivos con terceros que tambien esten conectados a la misma red. Para poder acceder a nuestro servidor desde el exterior tendremos dar unos pasos más, primero insatalaremos un Proxy dentro del Servidor para que evitar exponer demasiados puertos de nuestra red local.

### Nginx Proxy Manager

La razón principal para insatlar un Proxy en nuestro servidor es para evitar abrir puertos en nuestro router pero tambien nos servirá para no tener que recordar en que puerto hemos "alojado" cada aplicación. Ya que todas, o casi todas, las conexiones que hagamos a nuestro servidor desde una red externa lo haremos a traves del puerto 80 (para http) o el 443 (para https), lo que vamos a cambiar para acceder a una aplicación u otra es el dominio de acceso.

![proxy explain](/Imagenes/ReverseProxy.jpg)

*Fuente:* https://www.wundertech.net/nginx-proxy-manager-raspberry-pi-install-instructions/

En la fuente de la imagen hay un ejemplo de instalación de Nginx Proxy Manager, sin embargo con CasaOS la instalación es, a mi juicio, más sencilla.

Antes de instalarlo debemos cambiar el puerto de acceso a la interfaz de CasaOS, para ello solo hay que pulsar en Ajustes desde la pantalla de inicio (segundo icono de arriba a la izquierda), donde poner **Puerto de la WebUI** pulsar en modificar y poner el nuevo puerto (por ejemplo: 5000) evitando los puertos 80, 81, 443 o cualquiera que hayamos usado en otras aplicaciones.
> :memo: Para saber que puertos usan otras aplicaciones tienes que ir a los ajustes de cada aplicación y en la sección de **Puerto** mirar cuales estan en uso dentro del apartado **Anfitrión**

Ahora cuando queramos acceder a la interfaz de CasaOS tendremos que poner lo siguiente en el navegador:
    
> IP_SERVIDOR:PUERTO_ELEJIDO 

Siguiendo con el ejemplo:

> 192.168.0.102:5000

Ahora podemos instalar la aplicaión, solo hay que buscarla en la App Store y pulsar en instalar.
