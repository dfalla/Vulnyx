# Máquina Air

### Reconocimiento de la Ip de la máquina víctima

![alt text](image-1.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 10.0.2.19

![alt text](image-2.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,9999 -vvv -Pn 10.0.2.19

![alt text](image-3.png)

### Fuzzing web

feroxbuster --url http://10.0.2.19/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No se encontró nada interesante en el puerto 80 ni el puerto 8080, lo que sí se encontró fue un dominio air.nyx en el escaneo de puertos, y lo agregué al /etc/hosts

hice fuzzing web a air.nyx:8080

feroxbuster --url http://air.nyx:8080/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-4.png)


### Explotación

![alt text](image-5.png)

Intercepté la petición de subir una imagen con burpsuite y subí una rev.php agregandole el número mágico GIF89a

![alt text](image-6.png)

me puse en escucha con netcat y ejecuté curl http://air.nyx:8080/uploads/rev.php

![alt text](image-7.png)

cambiamos al usuario sam y luego al usuario xiao

![alt text](image-8.png)

### Escalar privilegios

![alt text](image-9.png)

![alt text](image-10.png)

![alt text](image-11.png)

ejecutamos su root y escribo la contraseña que encontré

![alt text](image-12.png)

### user.txt

![alt text](image-13.png)

### root.txt

![alt text](image-14.png)