# Máquina Druid

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.150

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.150

![alt text](image-2.png)

### Fuzzing web

gobuster dir -w /usr/share/seclists/Discovery/Web-Content/big.txt -u http://192.168.5.150/ -b 404,403

No encontramos nada interesante.

entramos en la web

![alt text](image-3.png)

encontré el dominio hotel.nyx y lo agregué al /etc/hosts

Busco subdominios:

![alt text](image-4.png)

lo agrego al /etc/hosts

Busco directorios en el subdominio reservations.hotel.nyx

gobuster dir -w /usr/share/seclists/Discovery/Web-Content/big.txt -u http://reservations.hotel.nyx/ -b 404,403

![alt text](image-5.png)

al entrar en la web veo de que se trata de Hotel Druid 3.0.3

![alt text](image-11.png)

### Explotación

Busco un exploit

![alt text](image-7.png)

lo descargo y lo ejecuto

![alt text](image-8.png)

ejecutamos:

![alt text](image-9.png)

### Escalar privilegios

cambiamos al usuario sun:

![alt text](image-10.png)

![alt text](image-6.png)

![alt text](image-12.png)

copiamos el id_rsa y utilizamos RSAcrack para crackear el passphrase

![alt text](image-13.png)

me conecto por ssh

![alt text](image-14.png)

### user.txt

![alt text](image-15.png)

### root.txt

![alt text](image-16.png)