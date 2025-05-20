# Máquina Unit

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.149

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,8080 -vvv -Pn 192.168.5.149

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.149/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No encontré nada


### Explotación

en el escaneo de servicios vi que tengo el método PUT y MOVE disponibles entonces subí un reverse shell en php pero con extensión txt y luego con el método MOVE le cambié la extensión a php, me puse en escucha con netcat y  luego hice curl al archivo php y listo tuve acceso

![alt text](image-3.png)


### Escalar privilegios

![alt text](image-4.png)

### user.txt

![alt text](image-5.png)

### root.txt

![alt text](image-6.png)