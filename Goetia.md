# Máquina Goetia

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 10.0.2.13

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 10.0.2.13

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://10.0.2.13/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

No se encontró nada.


### Explotación
Se permite ejecución remota de comandos

![alt text](image-3.png)

lancé una reverseshell 

![alt text](image-4.png)

me puse en escucha con netcat:

![alt text](image-5.png)

ejecuto ss -tuln para ver los servicios que corren internamente:

![alt text](image-6.png)

uso chisel para port fordwarding

En kali:

![alt text](image-7.png)

En la víctima:

![alt text](image-8.png)

Entro en la web de mi kali por el puerto 8080

![alt text](image-10.png)

Búsqueda de archivos ocultos mediante port fordwarding

wfuzz -c --hc=404 -t 200 -w /usr/share/seclists/Discovery/Web-Content/common.txt  -z list,php-txt-zip 'http://localhost:8080/FUZZ.FUZ2Z'

![alt text](image-9.png)

entro en hidden.php:

![alt text](image-11.png)

me descargo el archivo .zip

![alt text](image-12.png)

Usando la herramienta filters_chain_oracle_exploit.py

![alt text](image-13.png)

me conecto por ssh con el usuario ebathory

![alt text](image-14.png)

### Escalar privilegios



### user.txt



### root.txt

