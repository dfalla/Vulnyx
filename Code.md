# Máquina Code

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.151

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.151

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.151/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

entramos en la web http://192.168.5.151/pluck/

![alt text](image-4.png)

luego click en admin

![alt text](image-5.png)

### Explotación

Buscamos un exploit para Pluck 4.7.13

![alt text](image-6.png)

lo ejecutamos de la siguiente manera:

![alt text](image-7.png)

luego copiamos la dirección en la url:

![alt text](image-8.png)


### Escalar privilegios

cambiamos al usuario dave:

![alt text](image-9.png)

siendo el usuario dave ejecutamos sudo -l

![alt text](image-12.png)

creamos el archivo exploit.conf en /tmp

![alt text](image-13.png)

![alt text](image-10.png)

![alt text](image-11.png)

### user.txt

![alt text](image-14.png)

### root.txt

![alt text](image-15.png)