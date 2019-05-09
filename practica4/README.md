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

Y agregamos las lineas que se ven a continuación marcadas en amarillo.
![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica4/images/Captura2.PNG)