<H1>Ejercicios</H1>

<H2>Tema 1</H2>
<b>1. Buscar información sobre las tareas o servicios web para los que se usan más los programas que comentamos al
principio de la sesión:</b>

- <b>Apache</b>: El servidor HTTP Apache es un servidor web HTTP de código abierto, para plataformas Unix (BSD, GNU/Linux, etc.), Microsoft Windows, Macintosh y otras, que implementa el protocolo HTTP/1.1

- <b>Nginx</b>: es un servidor web de código abierto que, desde su éxito inicial como servidor web, ahora también es usado como proxy inverso, cache de HTTP, y balanceador de carga.

- <b>Thttpd</b>: es un servidor web de código libre disponible para la mayoría de las variantes de Unix.

    Se caracteriza por ser simple, pequeño, portátil, rápido, y seguro, ya que utiliza los requerimientos mínimos de un servidor HTTP. Esto lo hace ideal para servir grandes volúmenes de información estática.

- <b>Cherokee</b>: es un servidor web multiplataforma.2​ Su objetivo es ser rápido y completamente funcional, sin dejar de ser liviano comparado con otros servidores web.

    Es muy útil a la hora de administrar múltiples servidores web, por lo cual es ideal para ser utilizado en sistemas orientados a proveer de hosting y servicios de alojamiento compartido.

- <b>Node.js</b>: es un entorno en tiempo de ejecución multiplataforma, de código abierto, para la capa del servidor (pero no limitándose a ello) basado en el lenguaje de programación ECMAScript, asíncrono, con I/O de datos en una arquitectura orientada a eventos y basado en el motor V8 de Google. Fue creado con el enfoque de ser útil en la creación de programas de red altamente escalables, como por ejemplo, servidores web.


<H2>Tema 2</H2>

<b>1. Calcular la disponibilidad del sistema si tenemos dos
réplicas de cada elemento (en total 3 elementos en cada
subsistema).</b>

Vamos a ponernos siempre en el peor caso para este cálculo, que comprendería el hecho de que los componentes fuesen fallando de forma sucesiva uno tras otro.

Para estudiar este porcentaje con 1 única unidad de cada componente: 

        As = Ac1 * Ac2 * Ac3 * ... * Acn

La disponibilidad inicial equivale a:

        As = 85% * 90% * 99'9% * 98% * 85% * 99% * 99'99% * 95% = 59'86%

Ahora bien con componentes replicados, el valor de disponibilidad aproximada de éste sistema equivale a la siguiente ecuación:

        As = Ac1 + ( (1 - Ac1) * Ac2 )

Si replicamos el componente web la disponibilidad sería:

        As = 85% + ( (1 - 85%) * 85% ) = 97'75%

Con 3 elementos del subsistema: 

        COMPONENTE Web --> 99'6625% 
        App --> 99'9% 
        Database --> 99'999999% 
        DNS --> 99'9992% 
        Firewall --> 99'6625% 
        Switch --> 99'9999% 
        Data Center --> 99'999999% 
        ISP	--> 99'9875% 
        TOTAL --> 99'2135%

<b>2. Buscar frameworks y librerías para diferentes lenguajes que
permitan hacer aplicaciones altamente disponibles con
relativa facilidad. Como ejemplo, examina PM2 https://github.com/Unitech/pm2 que sirve para administrar clústeres de NodeJS.</b>

MySQL Router para balancear bases de datos MySQL

<b>3. ¿Cómo analizar el nivel de carga de cada uno de los
subsistemas en el servidor?
Buscar herramientas y aprender a usarlas.
...¡o recordar cómo usarlas!</b>

Ejecutando `top` en la terminal, nos muestra el uso de la memoria y procesador.

El comando linux `df` nos informa acerca del espacio total, ocupado y libre en nuestro sistema.