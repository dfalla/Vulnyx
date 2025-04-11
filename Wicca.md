# Máquina Wicca

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.159

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sV --script vuln -p22,80,5000 --min-rate 6000 -vvv 192.168.42.159

![alt text](image-2.png)

### Entramos en la web

![alt text](image-3.png)

jugamos con el input

![alt text](image-4.png)

jugamos con la url con el token

![alt text](image-5.png)

### Explotación

Colocamos un reverse shell en el token

![alt text](image-6.png)

nos ponemos en escucha 


### Escalar privilegios

![alt text](image-7.png)

ejecutamos

sudo /usr/bin/links -no-g

![alt text](image-8.png)

![alt text](image-9.png)

### user.txt

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)