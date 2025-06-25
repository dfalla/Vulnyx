# Máquina War

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 10.0.2.22

![alt text](image-2.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p135,139,445,5040,8080,49664-49670 -vvv -Pn 10.0.2.22

![alt text](image-1.png)


### Fuzzing web

feroxbuster --url http://10.0.2.22:8080/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

no encontramos nada interesante

entramos a la web y entramoe en Manager App con las credenciales admin:tomcat

![alt text](image-3.png)


### Explotación

Creamos un Revserse shell con msfvenom y me pongo en escucha con netcat:

![alt text](image-4.png)

subo el reverse shell:

![alt text](image-5.png)

le doy clic:

![alt text](image-6.png)

tengo acceso:

![alt text](image-7.png)

### Escalar privilegios

ejecuto whoami /priv

![alt text](image-11.png)

utilizo la herramienta PrintSpoofer64.exe, la transfiero

en kali ejecuto:

![alt text](image-9.png)

me muevo a la carpeta TEMP

![alt text](image-8.png)

transfiero la herramienta:

![alt text](image-10.png)



### user.txt

![alt text](image-13.png)

### root.txt

![alt text](image-12.png)