# Máquina Plex

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.147

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p21 -vvv -Pn 192.168.5.147

![alt text](image-2.png)

al parecer me encuentro ante una multiplexación de servicios.

Haciendo Banner grabbing:

![alt text](image-3.png)

![alt text](image-4.png)

están corriendo el servicio ssh y web en el puerto 21

### Fuzzing web

wfuzz -c --hc=404 -t 200 -w /usr/share/seclists/Discovery/Web-Content/big.txt 'http://192.168.5.147:21/FUZZ'

![alt text](image-5.png)

verificamos la información que hay en la web

![alt text](image-6.png)

encontré un jwt

### Explotación

utilizo la herramienta jwt.io y descifro credenciales:

![alt text](image-7.png)

me conecto por ssh:

![alt text](image-8.png)

### Escalar privilegios

![alt text](image-9.png)

cuando ejecutamos sudo /usr/bin/mutt, nos aparece una pantalla y presionamos shift + ! y en la parte dónde dice command shell escibimos /bin/bash luego enter

### user.txt

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)