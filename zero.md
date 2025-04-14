# Máquina zero

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.170

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,8080 -vvv -Pn 192.168.42.170

![alt text](image-2.png)

### Explotación

existe un exploit en searchsploit -> PHP 8.1.0-dev - 'User-Agentt' Remote Code Execution

lo descargamos 

searchsploit -m php/webapps/49933.py

![alt text](image-3.png)

observo el history y me conecto por ssh

![alt text](image-4.png)

### Escalar privilegios

![alt text](image-5.png)

![alt text](image-6.png)

### user.txt

![alt text](image-7.png)

### root.txt

![alt text](image-8.png)
