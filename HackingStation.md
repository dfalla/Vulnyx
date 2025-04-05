# Máquina HackingStation

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.149

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 vvv -Pn 192.168.42.149

![alt text](image-2.png)

### Explotación

Entramos en la web

![alt text](image-3.png)

y en el input de busqueda escribimos hola;id

![alt text](image-4.png)

entonces nos enviamos una bash

urlencodeamos con burp Suite

![alt text](image-5.png)

nos ponemos en escucha por el puerto 443

pegamos el bash urlencodeado en la url:

![alt text](image-6.png)

listo estamos dentro:

![alt text](image-7.png)

### Escalar privilegios

![alt text](image-8.png)

![alt text](image-9.png)

### user.txt

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)