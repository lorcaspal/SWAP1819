#**Práctica 1. Servidores Web de Altas Prestaciones**

##Preparación de las herramientas

1. El profesor nos proporcionó la imagen de UbuntuServer por lo que una vez guardada en nuestro PC, pasamos ha crear la máquina virtual (en mi caso con VirtualBox).
2. Configuramos la primera máquina virtual con la iso de UbuntuServer la cual llamaremos "maquina1". En VirtualBox debemos entrar en configuración > adaptador de red y crear un segundo adaptador, marcando la casilla de "Habilitar red" y  seleccionando en la pestaña "Red interna". 
3. Seguimos paso a paso el proceso de instalación, que encontramos en el documento proporcionado por el profesor.
4. Definimos password root
  
  ` sudo passwd root`

5. Instalamos Apache, PHP, MySQL y cURL
  `sudo apt-get install apache2 mysql-server mysql-client 
   sudo apt install curl `

6. Una vez realizado esto, clonamos la máquina 1 y le cambiamos el hostname por maquina2.
7. Modificamos en ambas máquinas el archivo "interfaces" que se encuentra situado en "/etc/network/" y añadimos la interfaz secundaria con la IP de nuestras máquinas, como se muestran en las imágenes 1 y 2.
![img](https://github.com/lorcaspal/SWAP1819/blob/master/images/IPmaquina1.PNG)
![img](https://github.com/lorcaspal/SWAP1819/blob/master/images/IPmaquina2.PNG)
