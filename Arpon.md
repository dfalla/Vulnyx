# Máquina Arpon

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.142

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.142

![alt text](image-2.png)


### Fuzing web

feroxbuster --url http://192.168.5.142 -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)


entramos en /backup/

![alt text](image-4.png)

### Explotación

Lo que hice fue subir un archivo .phar que contenía una reverse shell en php

![alt text](image-5.png)

luego como no sabía dónde se guardó hice una búsqueda recursiva por extensión con feroxbuster

feroxbuster --url http://192.168.5.142 -w /usr/share/seclists/Discovery/Web-Content/big.txt -x phar -d 5 --threads 50

![alt text](image-6.png)

lo encontró

ahora me puse en escucha con netcat y ejecuté:

curl http://192.168.5.142/backup/empty/rev.phar

![alt text](image-7.png)

Encontré un archivo interesante:

/var/www/html/backup/empty/.hidden/backup_id.zip

lo descargamos a la máquina atacante

al tratar de descomprimir me doy con la sorpresa que me pide contraseña

utilicé la herramieta fcrackzip

![alt text](image-8.png)

![alt text](image-9.png)

entonces verifico si existe ese usuario en el sistema de la víctima

![alt text](image-10.png)

utilicé RSAcrack para descifrar el passphrase:

![alt text](image-11.png)

me conecté con el usuario calabrote:

![alt text](image-12.png)

hice sudo -l 

![alt text](image-13.png)

analicé el archivo .bash_history de foque

![alt text](image-14.png)

analicé el archivo script_net_backup.sh

![alt text](image-15.png)

ví el id_rsa de foque

![alt text](image-16.png)

copio el contenido como id_rsa_foque y aplico el siguiente comando:

grep -v '^arp:' id_rsa_foque | sed 's/^>> //' > id_rsa

le di permisos 600 y me conecté con foque

![alt text](image-17.png)

### Escalar privilegios

siendo el usuario foque

![alt text](image-18.png)

### user.txt

![alt text](image-19.png)

### root.txt

![alt text](image-20.png)