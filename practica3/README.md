<H1>Práctica 3. Servidores Web de Altas prestaciones</H1>
<H2>Balanceo de carga</H2>

En esta práctica configuraremos una red entre varias máquinas de forma que tengamos un balanceador que reparta la carga entre varios servidores finales. Para ello vamos a usar dos servidores web el nginx y el haproxy. Seguimos los siguientes pasos:

1. Clonamos una de las máquinas ya creadas, la cual usaremos como balanceador. Una vez creada instalamos "ngnix".

        sudo apt-get install nginx
        sudo systemctl start nginx

2. Modificamos el fichero de configuración /etc/nginx/conf.d/default.conf para que sean nuestras máquinas las que se usen para realizar el reparto del tráfico:

    ![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica3/images/Captura1.PNG)


