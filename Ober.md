# Máquina Ober
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.130

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,111,135,139,445 -vvv -Pn 192.168.5.130

![alt text](image-2.png)

### Fuzzing Web

feroxbuster --url http://192.168.5.130/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

### Explotación

Inicié sesión con las credenciales admin:admin en : http://192.168.5.130/backend/backend/auth/signin

![alt text](image-4.png)

![alt text](image-5.png)

![alt text](image-6.png)

me puse en escucha con netcat y ejecuto

![alt text](image-7.png)

encuentro un archivo database.php

/var/www/html/octobercms/config/database.php

![alt text](image-8.png)

### Escalar privilegios

hago su root y escribo la contraseña de la base de datos mysql

![alt text](image-9.png)

### user.txt

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)
