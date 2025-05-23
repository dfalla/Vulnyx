# Máquina Slash

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.154

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.154

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.154/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

Buscamos entramos en /bak/default y se me descarga un archivo de configuración de nginx:

![alt text](image-4.png)

el error de configuración está en que en la parte de location debe ir como /bak/ y no como /bak, le falta el slash al final

feroxbuster --url http://192.168.5.154/bak../ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-5.png)

ahora buscamos archivos log

feroxbuster --url http://192.168.5.154/bak../log/ -w /usr/share/seclists/Discovery/Web-Content/big.txt -x log -d 5 --threads 50

![alt text](image-6.png)

al ver el auth.log, encontré un usuario llamado omar

![alt text](image-7.png)

Como está corriendo el servicio ssh, aplico hydra:

![alt text](image-8.png)


### Explotación 

Me conecto por ssh:

![alt text](image-9.png)

### Escalar privilegios

![alt text](image-10.png)

### user.txt

![alt text](image-11.png)

### root.txt

![alt text](image-12.png)