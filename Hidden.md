# Máquina Hidden

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.164

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.164

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.164/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No encontré nada

### Explotación

Encontré el puerto 69 UDP abierto y subí una reverse shell

![alt text](image-3.png)

me puse en escucha con netcat

y ejecuté:

curl http://192.168.5.164/rev.php

![alt text](image-4.png)

cambio al usuario satan:

![alt text](image-5.png)


### Escalar privilegios

![alt text](image-6.png)

![alt text](image-7.png)

copio el id_rsa y me conecto por ssh con el usuario root

![alt text](image-8.png)

### user.txt

![alt text](image-9.png)

### root.txt

![alt text](image-10.png)