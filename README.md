# Ejercicio de Apache y DNS

## Creación

### Instalación

Para comenzar instalaremos los dos paquetes necesarios, **APACHE2** y **BIND9**.

`sudo apt install bind9 apache2`

![Instalando Bind y Apache](/img/1.png)

### Apache

Comenzaremos por configurar el servidor Apache.

* En primer lugar crearemos los directorios para cada una de las páginas web mediante `mkdir -p`.

![Crear carpetas](/img/2.png)

* En segundo lugar creamos el archivo de index en todos los directorios anteriormente creados.

![Index1](/img/3.png)

![Index2](/img/4.png)

![Index3](/img/5.png)

![Index4](/img/6.png)

* Después se copia el archivo de configuración por defecto del servidor para cada una de las webs mediante `cp`.

![CPing](/img/7.png)

* Modificamos los archivos copiados para añadirle los datos propios del servidor.

![Conf1](/img/8.png)

![Conf2](/img/9.png)

![Conf3](/img/10.png)

![Conf4](/img/11.png)

* Tras haber completado los ficheros, debemos de disponibilizar los sitios correspondientes, esto se realiza mediante `a2ensite`. De igual manera utilizaremos `a2dissite` para desactivar el sitio por defecto del archivo **000-default.conf**. Finalmente recargamos y reiniciamos el servicio **apache2**.

![EnDis](/img/12.png)

* Después crearemos la contraseña para la web _escherichiacoli.es_ mediante el comando `htpasswd` con su atributo `-c`, el cual crea el fichero de contraseñas (solo se utiliza en el primer uso).

![ColiPass](/img/13.png)

* Y tras esta crearemos las contraseñas para la web _chip555.org_, de nuevo mediante `htpasswd`.

![ChiPass](/img/14.png)

* Una vez se han creado las contraseñas hay que añadir el archivo de contraseñas a la configuración de apache `apache2.conf` en la sección correspondiente a las respectivas webs.

![apaconf](/img/15.png)

![apaconf2](/img/16.png)

* Una vez está todo esto hecho se recarga y reinicia el servicio de **apache2** y habremos terminado de configurar los sitios web.

![endApax](/img/17.png)

### Configuración adaptador de red

Antes de continuar con el servidor DNS hemos de configurar la dirección IP.

![interfaces](/img/18.png)

### DNS

* En primer lugar debemos de configurar el archivo `named.conf.local` para añadir las zonas de cada URL.

![confLoc1](/img/19.png)

![confLoc2](/img/20.png)

![confLoc3](/img/21.png)

* En segundo lugar se activan los forwarders en el archivo `named.conf.options`

![confOpt](/img/22.png)

* Una vez hecho esto se crean los archivos de configuración de cada una de las URLs, indicados anteriormente en el archivo de configuración local.

![gato.com](/img/23.png)

![mos.com](/img/24.png)

![coli.es](/img/25.png)

![chip.org](/img/26.png)

* Tras estos archivos configuramos el archivo de resolución inversa, también indicado anteriormente en el archivo de configuración local.

![reverse](/img/27.png)

* Para terminar se recarga y reinicia el servicio. Aunque es recomendable reiniciar el sistema completamente.

![ReRe](/img/28.png)

## Resultado

![cate](/img/29.png)

Accediendo a `www.gato.com`.

![mosky](/img/30.png)

Accediendo a `www.mosquito.com`.

![coliCon](/img/31.png)

Petición de contraseña en `www.escherichiacoli.es`.

![coli](/img/32.png)

Accediendo a `www.escherichiacoli.es` tras identificarse como **user01**.

![chipCon](/img/33.png)

Petición de contraseña en `www.chip555.org`.

![chip](/img/34.png)

Accediendo a `www.chip555.org` tras identificarse como **user02**.
