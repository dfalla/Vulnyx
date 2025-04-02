# Máquina Blogger

### Reconocimiento de la Ip de la máquina víctima

![alt text](image-13.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.142

![alt text](image.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 vvv -Pn 192.168.42.142

![alt text](image-1.png)

### Fuzing web

gobuster dir -t 200 -u http://192.168.42.142/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-2.png)

al intentar acceder a http://192.168.42.142/wordpress/admin/ me sale lo siguiente:

![alt text](image-3.png)

lo agregamos al /etc/hosts

![alt text](image-4.png)

volví hacer gobuster esta vez al dominio.

![alt text](image-6.png)

gobuster dir -t 200 -u http://megablog.nyx/wordpress/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-5.png)

Enumeramos usuarios con wpscan:

wpscan --url http://megablog.nyx/wordpress -e p,u

![alt text](image-7.png)

hacemos ataque de fuerza bruta con wpscan:

wpscan --url http://megablog.nyx/wordpress/wp-login.php --usernames peter --passwords /usr/share/wordlists/rockyou.txt

![alt text](image-8.png)

### Explotación

Subí un plugin .zip con shell reverso en php

![alt text](image-9.png)

luego lo comprimí

![alt text](image-10.png)

luego subí el plugin y lo activé

me puse en escucha con netcat en el puerto 443

![alt text](image-11.png)


![alt text](image-12.png)


### Escalar privilegios

visualicé el archivo wp-config.php y pude encontrar las credenciales de root:

![alt text](image-13.png)

![alt text](image-14.png)

### user.txt

![alt text](image-15.png)

### root.txt

![alt text](image-16.png)