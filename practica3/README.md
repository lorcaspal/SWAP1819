<H1>Práctica 3. Servidores Web de Altas prestaciones</H1>

En esta práctica configuraremos una red entre varias máquinas de forma que tengamos un balanceador que reparta la carga entre varios servidores finales. Para ello vamos a usar dos servidores web el nginx y el haproxy. Seguimos los siguientes pasos:

<H2>Balanceo de carga con NGINX</H2>
1. Clonamos una de las máquinas ya creadas, la cual usaremos como balanceador. Una vez creada instalamos "ngnix".

        sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove
        sudo apt-get install nginx
        sudo systemctl start nginx

2. Modificamos el fichero de configuración /etc/nginx/conf.d/default.conf para que sean nuestras máquinas las que se usen para realizar el reparto del tráfico:

    ![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica3/images/Captura1.PNG)

3. Una vez que lo tenemos configurado, podemos lanzar el servicio nginx como sigue:

        sudo systemctl start nginx

4. Si no obtenemos ningún mensaje de error, todo está funcionando correctamente y ya podemos probar la configuración haciendo peticiones a la IP de esta máquina balanceador: 

        curl http://172.16.168.132

    ![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica3/images/Captura2.PNG)

    Y lo realizamos de nuevo:

        curl http://172.16.168.132

    ![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica3/images/Captura3.PNG)


    Como podemos ver en las imágenes el balanceador realiza su trabajo correctamente. En el caso de que al lanzarlo hubiesemos tenido un error significa que no está funcionando el balanceador, por lo que hay que eliminar una línea que configura nginx como servidor web en el archivo /etc/nginx/nginx.conf 

    ![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica3/images/Captura4.PNG)

<H2>Balanceo de carga con HAPROXY</H2>

1. Instalamos "haproxy"

       sudo apt-get install haproxy

 