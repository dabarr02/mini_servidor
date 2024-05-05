# Como crear un mini servidor en casa

## Material
* MiniPc, raspberry pi o similares con ubuntu/debian instalado.
* Discos duros.
* Un segundo dispositivo (o una panatalla, teclado y ratón conectados al dispositivo del servidor).

>:memo: **Nota:** Al MiniPC/raspberry lo llamaremos **Servidor** y al segundo dispositivo lo llamaremos **Auxiliar**.

## CasaOS
CasaOs es una especie de sistema operativo en la nube, código abierto, que se basa en la tecnología Docker para ofrecer una experiencia similar a la de un SO convencional pero que se accede a traves de un navegador web. Esto nos será muy útil ya que facilita mucho la gestión de contenedores, que usaremos más adelante, además de la gestión de archivos en remoto, ya que ofrece una interfáz bastante sencilla de entender y utilizar.
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
Donde nos dice la dirección Ip del Servidor (debería ser la misma que apuntamos) desde la que podemos acceder desde un navegador.

En el caso de que queramos desinstalar CasaOS podemos introducir el siguiente comando :

    casaos-uninstall

## Configurar CasaOS

Al acceder a la dirección Ip del Servidor por primera vez nos aparecerá la siguiente ventana :

![Welcome Casaos](/Imagenes/casaos_welcome.png)

Aquí tendremos que elegir un nombre de usuario y una contraseña para acceder a nuestro Servidor desde CasaOS, este usuario y contraseña pueden (y deben) ser diferentes del usuario y contraseña de inicio de sesión de *habitual* del Servidor. Con este sencillo paso ya tenemos CasaOS listo para usarse.

## Instalar *aplicaciones*

En CasaOS el equivalente de las aplicaciones son los contenedores. Para instalar las aplicaciones predeterminadas solo tenemos que pulsa en el icono que pone *App Store* y se nose desplegara la siguiente ventana :

![Tienda de aplicaciones](/Imagenes/AppStore_CasaOS.png)

Desde la que podemos buscar e instalar algunas aplicaciones "pre-configuradas".
Acontinuación veremos algunos ejemplos de instalación y configuración.

### FileBrowser

