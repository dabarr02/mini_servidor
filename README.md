# Como crear un mini servidor en casa

## Material
* MiniPc, raspberry pi o similares con ubuntu/debian instalado.
* Discos duros.
* Un segundo dispositivo (o una panatalla, teclado y ratón conectados al dispositivo del servidor).

>:memo: **Nota:** Al MiniPC/raspberry lo llamaremos Servidor y al segundo dispositivo lo llamaremos Auxiliar.

# CasaOS
CasaOs es una especie de sistema operativo en la nube, código abierto, que se basa en la tecnología Docker para ofrecer una experiencia similar a la de un SO convencional pero que se accede a traves de un navegador web. Esto nos será muy útil ya que facilita mucho la gestión de contenedores, que usaremos más adelante, además de la gestión de archivos en remoto. Ya que ofrece una interfaz bastante sencilla de entender y utilizar.
Desde su página oficial se pude probar una versión Demo : [casaos.io](https://casaos.io)

## Instalación de CasaOS
Tenemos dos formas de instalar CasaOS.

## Desde el Servidor
En este caso lo unico que tenemos que hacer es :

1. Abrir la terminal (en el caso que hallamos instalado una versión con escritorio)
2. Introducir el siguiente comando:

        curl -fsSL https://get.casaos.io | sudo bash

## Desde el Auxiliar (SSH)
Para este caso es necesario que conozcamos la dirección IP de nuestro Servidor.
### Buscar dirección IP
Para ello utilizamos una herramienta como [Advanced IP Scanner](https://www.advanced-ip-scanner.com/es/), aunque se puede utilizar cualquier herramienta de este estilo.
Una vez instalado en Auxiliar y estando conectados en la misma red que el Servidor buscamos la IP de este y la guardamos.

![Ejempl IP Scanner](/Imagenes/Ip_Scanner.png "Ejemplo IP Scanner")

*Ejemplo Advanced IP Scanner*

