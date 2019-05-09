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


![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica3/images/Captura6.PNG)