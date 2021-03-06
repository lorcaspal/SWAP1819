<H1>Práctica 5. Replicación de bases de datos MySQL</H1>

<H2>Objetivos de la práctica</H2>
A la hora de hacer copias de seguridad de nuestras bases de datos (BD) MySQL, una opción muy común suele ser la de usar una réplica maestro-esclavo, de manera que nuestro servidor en producción hace de maestro y otro servidor de backup hace de
esclavo.

Podemos hacer copias desde el servidor de backup sin que se vea afectado el rendimiento del sistema en producción y sin interrupciones de servicio.

Tener una réplica en otro servidor también añade fiabilidad ante fallos totales del sistema en producción, los cuales, tarde o temprano, ocurrirán. Por ejemplo, podemos tener un pequeño servidor actuando como backup en nuestra oficina sincronizado mediante réplicas con nuestro sistema en producción.

Esta opción, además, añade fiabilidad ante posibles interrupciones de servicio permanentes del servidor maestro por cualquier escenario catastrófico que nos podamos imaginar. En ese caso, tendremos posiblemente decenas de clientes y
servicios parados sin posibilidad de recuperar sus datos si no hemos preparado un buen plan de contingencias. Tener un servidor de backup con MySQL actuando como esclavo de replicación es una solución asequible y no consume demasiado ancho de banda en un sitio web de tráfico normal, además de que no afecta al rendimiento del maestro en el sistema en producción.

Los objetivos concretos de esta práctica son:
- Copiar archivos de copia de seguridad mediante ssh.
- Clonar manualmente BD entre máquinas.
- Configurar la estructura maestro-esclavo entre dos máquinas para realizar el clonado automático de la información.

<H2>Crear una BD e insertar datos</H2>
Para el resto de la práctica debemos crearnos una BD en MySQL e insertar algunos datos. Así tendremos datos con los cuales hacer las copias de seguridad. En todo momento usaremos la interfaz de línea de comandos del MySQL:

   ![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura1.PNG)

   ![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura2.PNG)

Ya tenemos datos (un registro) insertados en nuestra BD llamada “datos”. Podemos haber insertado más registros. Veamos cómo entrar y hacer una consulta:

   ![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura3.PNG)

   ![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura4.PNG)

<H2>Replicar una BD MySQL con mysqldump</H2>

MySQL ofrece la una herramienta para clonar las BD que tenemos en nuestra máquina. Esta herramienta es mysqldump. Concretamente, las opciones --quick o --opt hacen que MySQL cargue el resultado entero en memoria antes de volcarlo a fichero, lo que puede ser un problema si se trata de una BD grande. Sin embargo, la opción --opt está activada por defecto.
La sintaxis de uso es:

        mysqldump ejemplodb -u root -p > /root/ejemplodb.sql

Esto puede ser suficiente, pero tenemos que tener en cuenta que los datos pueden estar actualizándose constantemente en el servidor de BD principal. En este caso, antes de hacer la copia de seguridad en el archivo .SQL debemos evitar que se
acceda a la BD para cambiar nada.

Así, en el servidor de BD principal (maquina1) hacemos:

        mysql -u root –p
        mysql> FLUSH TABLES WITH READ LOCK;
        mysql> quit

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura5.PNG)

Ahora ya sí podemos hacer el mysqldump para guardar los datos. En el servidor principal (maquina1) hacemos:

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura6.PNG)

Como habíamos bloqueado las tablas, debemos desbloquearlas (quitar el “LOCK”):

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura7.PNG)

En la siguiente imagen vemos que la acción se ha realizado correctamente: 

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura8.PNG)

Ya podemos ir a la máquina esclavo (maquina2, secundaria) para copiar el archivo .SQL con todos los datos salvados desde la máquina principal (maquina1).

Con el archivo de copia de seguridad en el esclavo ya podemos importar la BD completa en el MySQL. Para ello, en un primer paso creamos la BD:

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura9.PNG)

En un segundo paso restauramos los datos contenidos en la BD (se crearán las tablas en el proceso):

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura10.PNG)

Y vemos que se ha realizado:

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura11.PNG)

<H2>Replicación de BD mediante una configuración
maestro-esclavo</H2>

Lo primero que debemos hacer es la configuración de mysql del maestro. Para ello editamos, como root, el /etc/mysql/mysql.conf.d/mysqld.cnf para realizar las modificaciones que se muestran a continuación y reiniciamos el servicio:

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura12.PNG)

Si no nos ha dado ningún error la configuración del maestro, podemos pasar a hacer la configuración del mysql del esclavo.

La configuración es similar a la del maestro, con la diferencia de que el server-id en esta ocasión será 2 y reiniciamos el servicio en el esclavo:

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura13.PNG)


Ahora ya podemos volver al maestro para crear un usuario y darle permisos de acceso para la replicación.

Entramos en mysql y ejecutamos las siguientes sentencias:

        mysql> CREATE USER esclavo IDENTIFIED BY 'esclavo';
        mysql> GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%'
        IDENTIFIED BY 'esclavo';
        mysql> FLUSH PRIVILEGES;
        mysql> FLUSH TABLES;
        mysql> FLUSH TABLES WITH READ LOCK;

Para finalizar con la configuración en el maestro, obtenemos los datos de la BD que vamos a replicar para posteriormente usarlos en la configuración del esclavo:

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura14.PNG)

Volvemos a la máquina esclava, entramos en mysql y le damos los datos del maestro. En el entorno de mysql ejecutamos la siguiente sentencia:

        mysql> CHANGE MASTER TO MASTER_HOST='192.168.1.100',
        MASTER_USER='esclavo', MASTER_PASSWORD='esclavo',
        MASTER_LOG_FILE='mysql-bin.000001', MASTER_LOG_POS=154,
        MASTER_PORT=3306;

Por último, arrancamos el esclavo y ya está todo listo para que los demonios de MySQL de las dos máquinas repliquen automáticamente los datos que se introduzcan/modifiquen/borren en el servidor maestro:

        mysql> START SLAVE;

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura15.PNG)

Ahora, podemos hacer pruebas en el maestro y deberían replicarse en el esclavo automáticamente.

Por último, volvemos al maestro y volvemos a activar las tablas para que puedan meterse nuevos datos en el maestro:

        mysql> UNLOCK TABLES;

Ahora, si queremos asegurarnos de que todo funciona perfectamente y que el esclavo no tiene ningún problema para replicar la información, nos vamos al esclavo y con la
siguiente orden:

        mysql> SHOW SLAVE STATUS\G

revisamos si el valor de la variable “Seconds_Behind_Master” es distinto de “null”. En ese caso, todo estará funcionando perfectamente. Si no es así, es que hay algún error y los valores de las demás variables indicarán cuál es el problema y cómo arreglarlo para que todo funcione bien.

A continuación vemos que el valor de la variable “Seconds_Behind_Master” es 0, por lo que no hay ningún error y todo funciona como debe:

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura16.PNG)

Para comprobar que todo funciona, debemos ir al maestro e introducir nuevos datos a la base de datos. A continuación vamos al esclavo para revisar si la modificación se ha reflejado en la tabla modificada en el maestro:

![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica5/images/Captura17.PNG)

Como podemos observar todo funciona correctamente.


