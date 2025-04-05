# Máquina Agent

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.151

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 vvv -Pn 192.168.42.151

![alt text](image-2.png)

### Fuzzing Web

Cambiando el user-agent

wfuzz -c -t 200 --hc=404 -H "User-Agent: jorgas" -w /usr/share/seclists/Discovery/Web-Content/common.txt http://192.168.42.151/FUZZ

![alt text](image-3.png)

### Explotación

Entrando en http://192.168.42.151/websvn

![alt text](image-4.png)

buscamos un exploit en searchsploit

![alt text](image-5.png)

lo descargamos y modificamos:

![alt text](image-6.png)

lo ejecutamos:

![alt text](image-7.png)

nos ponemos en escucha con netcat en el puerto 443

![alt text](image-8.png)

### Escalar privilegios

![alt text](image-9.png)

Escalamos al usuario dustin

![alt text](image-10.png)

siendo el usuario dustin

![alt text](image-11.png)

### user.txt

![alt text](image-12.png)

### root.txt

![alt text](image-13.png)