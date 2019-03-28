<H1>Práctica 2. Servidores Web de Altas prestaciones</H1>
<H2>Clonar la información de un sitio web</H2>
	1. Instalamos la herramienta rsync
	
  		`sudo apt-get install rsync`
  
 Para usar la herramienta y clonar un directoria cualquier: 
 
   		`rsync -avz -e ssh ipmaquina2:dirmaquina_2 dir_maquina1`
   
2. Acceder sin contrasesña con ssh de una máquina a la otra

	Escribimos en la Máquina secundaria:

  	`ssh-keygen -b 4096 -t rsa`
  
	Escribimos en la Máquina principal:

  	`chmod 600 ~/.ssh/authorized_keys`
  
  	`ssh-copy-id user_maquinasecundaria@direccionIPmaquinasecundaria`
  
3. Mostramos el clon de una maquina a la otra:
 	![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica2/images/ClonM1.PNG)
 4. Mostramos la copia y acceso desde ssh sin contraseña:
 	![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica2/images/copiaYaccesoSinClaveM1.PNG)
 5. Programar tareas con crontab (se ubica en /etc/crontab) cron es un administrador procesos en segundo plano que ejecuta procesos en el instante indicado en el fichero crontab (se encuentra en /etc/crontab).

  	Para automatizar un nuevo proceso hay que seguir el siguiente orden:

  	Minuto Hora DiaDelMes Mes DiaDeLaSemana Usuario Comando

  	30 15 * * * usuario_actual rsync -avz -e ssh usuario_actual@ip_maquina2:/

	![img](https://github.com/lorcaspal/SWAP1819/blob/master/practica2/images/Crontab.PNG)
