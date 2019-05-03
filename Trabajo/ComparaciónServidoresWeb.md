<H1>Comparación Servidores Web</H1>

- Pablo Gervilla Palomar 
- Lorena Castillo Palomo

<H2>Índice</H2>

1.<a href="#id1" style="color:white"> ¿Qué es un servidor? </a>

2.<a href="#id2" style="color:white"> Características de los servidores </a>

3.<a href="#id3" style="color:white"> Ejemplos comparativos </a>

4.<a href="#id4" style="color:white"> Conclusiones </a>

5.<a href="#id5" style="color:white"> Bibliografía </a>



<H2 id="id1">¿Qué es un servidor?</H2>
Un servidor web es un programa informático que procesa una aplicación del lado del servidor, realizando así conexiones con el cliente ya sean unidireccionales o bidireccionales y síncronas o asíncronas. 

De forma más simplificada, imaginemos que queremos hacer una tarta. El servidor es como una despensa. Tenemos que acudir a él para obtener el bizcocho, el chocolate y la nata, que podrían ser los mensajes de correo, la web y los archivos en la nube.

Es lo que se conoce como el modelo cliente-servidor: el cliente pide y el servidor le abastece de los recursos que necesita.

Los servidores web que vamos a tratar son, unos más conocidos como; Apache, Nginx, Google Web Server y IIS de Microsoft y en menor medida, otros menos usados como; Cherokee, Lite Speed, NodeJS, Lighttpd y Sun Java Sysem Application Server.

<H2 id="id2">Características de los servidores</H2>
<H3>Apache</H3>
Apache es el servidor web HTTP más usado, cuyo código inicial está basado en el popular NCSA HTTPd (1995), aunque más tarde se reescribió desde 0.

Su nombre se debe a que alguien quería que tuviese la connotación de algo que es firme y enérgico pero no agresivo, y la tribu Apache fue la última en rendirse al que pronto se convertiría en gobierno de Estados Unidos.

Tiene una estructura basada en módulos; seguridad, almacenamiento en caché, reescritura de URL, autenticación de contraseña, etc.

Como ventajas podemos destacar que Apache es gratuito y de código abierto, estable, flexible y con frecuencia de actualizaciones. Sin embargo, presenta problemas de rendimiento bajo tráfico alto y puede generar vulnerabilidades de seguridad.

<H3>Nginx</H3>
Nginx es un servidor web ligero de alto rendimiento y código abierto, diseñado para ofrecer un bajo uso de memoria y alta concurrencia. Este servidor consume muchos menos recursos al servir contenido estático, lo que lo hace una excelente opción para funcionar como proxy inverso o balanceador de carga como hemos visto en clase. 


Una de la características a destacar es su arquitectura, que permite responder a millones de peticiones por segundo, gracias a que aprovecha el máximo de sus recursos.



<H3>Microsoft IIS</H3>
Internet Information Services (IIS) es un servidor web y un conjunto de servicios para el sistema operativo Microsoft Windows, el cual al ser desarrollado por Windows, no es de código abierto. Es epecialmente usado en servidores web y actualmente es el segundo sistema de servidor web más popular ( funciona en el 35% de los servidores de todos los sitios web). Los servicios que ofrece son: FTP, SMTP, NNTP y HTTP/HTTPS. 

Una de las características más importantes es la presencia del protocolo HTTP 1.1 que ofrece notables mejoras de las prestaciones, así como la disminución de los tiempos de respuesta en la transmisión.

Por contrapartida nos encontramos con que actualmente IIS está disponible sólo para el uso en la plataforma Windows NT, cosa que otros servidores, como por ejemplo Apache, pueden correr en la mayoría de plataformas.

<H3>Google Web Server</H3>
Google Web Server, también conocido como GWS, es el servidor web que Google utiliza en sus infraestructuras y que alberga aproximadamente un 10 % de todas las páginas web activas del mundo. Es el cuarto servidor web más popular por detras de Apache, Nginx y Microsoft IIS.

Las solicitudes de página web en la mayoría de las páginas de Google proporcionan "gws" (sin un número de versión) en el encabezado HTTP como una indicación del software del servidor web que se está utilizando.

Al ser Google el propietario existe poca información sobre GWS, lo que dificulta saber más sobre su infraestructura, arquitectura, etc.

<H3>NodeJS</H3>
NodeJS es un entorno en tiempo de jecución multiplataforma, de código abierto de JavaScript que está diseñado para generar aplicaciones web de forma altamente optimizada.

Aprovechando el motor V8 permite a Node proporciona un entorno de ejecución del lado del servidor que compila y ejecuta javascript a velocidades increíbles.

<H3>Cherokee</H3>
Cherokee es un servidor web multiplataforma. Es muy rápido y completamente funcional, sin dejar de ser liviano comparado con otros servidores web. Acepta más peticiones por segundo (hasta 6 veces más rápido que Apache) pero sin embargo, es menos versátil. 

<H3>Lite Speed</H3>
Lite Speed es un servidor web que basa su arquitectura entorno al uso de procesos, y no eventos porque con eso usa muchos menos procesos, ahorra recursos, logra un alto rendimiento y velocidad de despacho de la web. 

El principal inconveniente de Lite Speed es que es de pago.

<H3>Lighttpd</H3>
Lighttpd es un servidor web diseñado para ser rápido, seguro, flexible y optimizado para ambientes de alto rendimiento. Se ocupa de balancear la CPU y además gracias a ciertas características avanzadas (FastCGI, Auth) hace que Lighttpd sea perfecto para aquellos servidores con problemas de balanceo.

<H3>Sun Java Sysem Application Server</H3>
Java también tiene su propio servidor web llamado Sun Java Sysem Application Server o SJSAS, está basado en Java EE y tiene soprote integrado para interfaces de desarrollo como Sun Java Studio Enterprise/Creator y NetBeans. Desde la versión 9 se desarrolla bajo el nombre de GlassFish.

<H2 id="id3">Ejemplos comparativos</H2>
<H3>Uso de los servidores Web a lo largo del tiempo</H3>

![img](https://github.com/lorcaspal/SWAP1819/blob/master/Trabajo/images/Grafica1.PNG)

![img](https://github.com/lorcaspal/SWAP1819/blob/master/Trabajo/images/Tabla1.PNG)

Como podemos observar en la gráfica el servidor web más usado a lo largo del tiempo ha sido Apache. Desde los últimos años ha habido un balanceo positivo con respecto a los otros servidores web, los cuales se han ido usando cada vez más, mientras que Apache ha caído. Podemos destacar Nginx, Microsoft y otros servidores menores. Por esta razón, todos los nuevos servidores han sentado su tenido como objetivo "machacar" a Apache.

<H3>Uso de los servidores Web a lo largo del tiempo</H3>


<H2 id="id4">Conclusiones</H2>
<H2 id="id5">Bibliografía</H2>
