# Máquina shock

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 10.0.2.11

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 10.0.2.11

![alt text](image-2.png)

### Fuzing web

wfuzz -c -t 200 --hc=404 --hw=1 -w /usr/share/seclists/Discovery/Web-Content/common.txt "http://10.0.2.11/FUZZ/"

![alt text](image-3.png)

cgi-bni es una carpeta utilizada para alojar scripts que interactuarán con el navegador web, en esta carpeta se alojan archivos como .sh, .cgi

hacemos una búsqueda de archivos:

![alt text](image-4.png)

accedemos al archivo por la web

![alt text](image-5.png)

### Explotación

con el archivo encontrado anteriormente me permite ejecutar comandos

![alt text](image-7.png)

nos ponemos en escucha con el puerto 443

### Escalar privilegios

escalamos a will 

![alt text](image-6.png)

escalamos a root

![alt text](image-8.png)

ejecutamos

sudo /usr/bin/systemctl

![alt text](image-9.png)


### user.txt

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)
