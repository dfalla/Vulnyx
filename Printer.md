# Máquina Printer

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.165

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,9999 -vvv -Pn 192.168.5.165

![alt text](image-2.png)

### Fuzzing web

feroxbuster --url http://192.168.5.165/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

entramos en la web

![alt text](image-4.png)

Buscamos el archivo por rango de 1 a 2000

wfuzz -c --hl=9 -t 200 -z range,1-2000 -z list,txt-json-php "http://192.168.5.165/api/printers/printerFUZZ.FUZ2Z"

![alt text](image-5.png)

lo buscamos en la web

![alt text](image-6.png)

### Explotación

Nos conectamos a la impresora mediante netcat con la contraseña encontrada y ejecutamos una reverse shell con bash, previamente me puse en escucha con netcat.

![alt text](image-7.png)

![alt text](image-8.png)

### Escalar privilegios

![alt text](image-9.png)

![alt text](image-10.png)

![alt text](image-11.png)

### user.txt

![alt text](image-12.png)

### root.txt

![alt text](image-13.png)