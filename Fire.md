# Máquina Fire

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.152

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p21,22,80,9090 -vvv -Pn 192.168.5.152

![alt text](image-2.png)

![alt text](image-3.png)

### Fuzzing web

feroxbuster --url http://192.168.5.152/ -w /usr/share/seclists/Discovery/Web-Content/big.txt


### Explotación

Me logueo en ftp con el usuario anonymous y descargo backup.zip

![alt text](image-4.png)

al descomprimir la el archivo backup.zip me aparece una carpeta llamada mozilla y dentro de ella una carpeta llamada firefox, entonces utilizo la herramienta: https://github.com/unode/firefox_decrypt/blob/main/firefox_decrypt.py

la descargo y la ejecuto

![alt text](image-5.png)

ahora entro a la web por el puerto 9090:

![alt text](image-6.png)

coloco las credenciales de marco, luego me dirijo a Terminal

![alt text](image-7.png)

### Escalar privilegios

ejecuté sudo -l:

![alt text](image-8.png)

Tengo la posibilidad de ver archivos:

![alt text](image-9.png)

copio el id_rsa del usuario root, lo ordeno y luego me conecto por ssh:

![alt text](image-10.png)

### user.txt

![alt text](image-11.png)

### root.txt

![alt text](image-12.png)