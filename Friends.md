# Máquina Friends

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.146

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p21,80,3306 -vvv -Pn 192.168.5.146

![alt text](image-2.png)

### Fuzing web

feroxbuster --url http://192.168.5.146/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

### Explotación

Entre en la web:

![alt text](image-5.png)

Descargué la imagen y la subí en google para buscar información:

![alt text](image-4.png)


hice un ataque de cracking online a mysql con el usuario beavis y vi la contraseña: rocknroll

me conecto a mysql:

![alt text](image-6.png)

y encuentro:

![alt text](image-7.png)

luego ejecuto reviso el index.php

![alt text](image-8.png)


subo un webshell a /M3t4LL1c@

![alt text](image-9.png)

envió una reverse shell:

![alt text](image-10.png)

### Escalar privilegios

cambio al usuario butthead con la contraseña encontrada en mysql:

![alt text](image-11.png)

### user.txt

![alt text](image-12.png)

### root.txt

![alt text](image-13.png)