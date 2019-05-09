<H1>Práctica 4. Asegurar la granja web</H1>

<H2>Objetivos de la práctica</H2>
El objetivo de esta práctica es llevar a cabo la configuración de seguridad de la granja
web. Para ello, llevaremos a cabo las siguientes tareas:

- Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.

- Configurar las reglas del cortafuegos para proteger la granja web.

<H2>Instalar un certificado SSL autofirmado para
configurar el acceso por HTTPS</H2>

El protocolo SSL (Secure Sockets Layer) es un protocolo de comunicación que se ubica en la pila de protocolos sobre TCP IP. SSL proporciona servicios de comunicación segura entre cliente y servidor, como por ejemplo autenticación (usando
certificados), integridad (mediante firmas digitales), y privacidad (mediante encriptación).

Existen diversas formas de obtener un certificado SSL e instalarlo en nuestro servidor
web para poder servir páginas mediante el protocolo HTTPS, para ello, lo principal es
conseguir un certificado que podremos conseguir de las siguientes formas:

- Mediante una autoridad de certificación.
- Crear nuestros propios certificados SSL auto-firmados usando la herramienta openssl.
- Utilizar certificados del proyecto Certbot (antes Let’s Encrypt).

<H3>Generar e instalar un certificado autofirmado</H3>
Para generar un certificado SSL autofirmado en Ubuntu Server solo debemos activar
el módulo SSL de Apache, generar los certificados y especificarle la ruta a los
certificados en la configuración. Así pues, como root ejecutaremos:

        a2enmod ssl
        service apache2 restart
        mkdir /etc/apache2/ssl
        openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout 
        /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt

Nos pedirá una serie de datos para configurar el dominio.

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica4/images/Captura1.PNG)

Editamos el archivo de configuración del sitio default-ssl:

        nano /etc/apache2/sites-available/default-ssl

Y agregamos las lineas que se ven a continuación marcadas en amarillo debajo de SSLEngine on:
![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica4/images/Captura2.PNG)

Activamos el sitio default-ssl y reiniciamos apache:

        a2ensite default-ssl
        service apache2 reload

Ya podemos hacer peticiones por HTTPS con curl:

        curl -k https://192.168.1.100/index.html

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica4/images/Captura3.PNG)

Por último, y como queremos que la granja nos permita usar el HTTPS, debemos configurar el balanceador para que también acepte este tráfico (puerto 443). Para hacer esto, copiaremos la pareja de archivos (el .crt y el .key) a todas las máquinas de la granja web. No debemos generar más certificados, sino que los archivos apache.crt y apache.key que generamos en el primer servidor en el paso anterior vamos a copiarlos al otro servidor y al balanceador. Para copiarlos podemos usar scp o rsync.

rsync -avz -e ssh maquina1@192.168.1.100:/etc/apache2/ssl/* /etc/apache2/ssl/

En el segundo servidor debemos activar el sitio default-ssl y reiniciar apache (como hicimos en el primer servidor). En el balanceador pondremos la ruta a la carpeta donde hayamos copiado el apache.crt y el apache.key. Después, en el balanceador nginx debemos añadir lo siguiente al archivo /etc/nginx/conf.d/default.conf y reiniciarlo:

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica4/images/Captura4.PNG)

Una vez hecho esto reiniciamos Nginx:

        sudo systemctl restart nginx       

<H2>Configuración del cortafuegos</H2>

Un cortafuegos es un componente esencial que protege la granja web de accesos indebidos. Son dispositivos colocados entre subredes para realizar diferentes tareas de manejo de paquetes. Actúa como el guardián de la puerta al sistema web,
permitiendo el tráfico autorizado y denegando el resto.

En general, todos los paquetes TCP/IP que entren o salgan de la granja web deben pasar por el cortafuegos, que debe examinar y bloquear aquellos que no cumplan los criterios de seguridad establecidos. Estos criterios se configuran mediante un conjunto de reglas, usadas para bloquear puertos específicos, rangos de puertos, direcciones IP, rangos de IP, tráfico TCP o tráfico UDP.

<H3>Configuración del cortafuegos</H3>
iptables es una herramienta de cortafuegos, de espacio de usuario, con la que el superusuario define reglas de filtrado de paquetes, de traducción de direcciones de red, y mantiene registros de log. Esta herramienta está construida sobre Netfilter, una parte del núcleo Linux que permite interceptar y manipular paquetes de red. Para más ayuda: 

     man iptables

o bien:

    iptables -h    


Para configurar adecuadamente iptables en una máquina Linux, conviene establecer como reglas por defecto la denegación de TODO el tráfico, salvo el que permitamos después explícitamente. Una vez hecho esto, a continuación definiremos nuevas reglas para permitir el tráfico solamente en ciertos sentidos necesarios, ya sea de entrada o de salida. Por último, definiremos rangos de direcciones IP a los cuales aplicar diversas reglas, y mantendremos registros (logs) del tráfico no permitido y de intentos de acceso para estudiar más tarde posibles ataques.

Si queremos comprobar el estado del cortafuegos, debemos ejecutar:

        iptables –L –n -v

<H3>Uso de la aplicación iptables</H3>