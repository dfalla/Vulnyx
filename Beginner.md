# Máquina Beginner

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.175

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sV --script vuln -p22,80 --min-rate 6000 -vvv 192.168.42.175

![alt text](image-2.png)

### Entramos en la web

![alt text](image-3.png)

### Escaneo de puerto UDP

![alt text](image-4.png)


usando metasploit podemos ver que hay dentro de tftp

![alt text](image-5.png)

bajamos el archivo:

![alt text](image-6.png)

visualizo el tipo de archivo que es:

![alt text](image-7.png)

lo descomprimo:

![alt text](image-8.png)

entonces me descomprime una carpeta backup y dentro de ella archivos id_rsa y sshd_config, abrimos el archivo sshd_config

![alt text](image-9.png)

y visualiso un usuario boris:

![alt text](image-10.png)

entonces por ende el id_rsa le pertenece a boris



### Explotación

le damos pemrisos 600 al id_rsa y nos conectamos:

![alt text](image-11.png)


### Escalar privilegios

![alt text](image-12.png)

entonces vemos el id_rsa de root para conectarme:

![alt text](image-13.png)

![alt text](image-14.png)

### user.txt

![alt text](image-15.png)

### root.txt

![alt text](image-16.png)