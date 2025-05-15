# Máquina Hook

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.143

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.143

![alt text](image-2.png)


### Fuzing web

feroxbuster --url http://192.168.5.143 -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

entramos en la dirección marcada

![alt text](image-4.png)

veo una versión de htmLawed 1.2.5

hacemos fuzzing web a http://192.168.5.143/htmLawed/

![alt text](image-5.png)

### Explotación

Subo una reverse shell

![alt text](image-6.png)

me puse en escucha con netcat

y ejecuté

![alt text](image-7.png)

![alt text](image-8.png)

hice sudo -l siendo el usuario www-data

![alt text](image-9.png)

cambiando al usuario noname

![alt text](image-10.png)

### Escalar privilegios

siendo el usuario noname:

![alt text](image-12.png)

ejecuto sudo /usr/bin/iex

dentro de la consola interactiva

![alt text](image-11.png)


### user.txt

![alt text](image-13.png)

### root.txt

![alt text](image-14.png)