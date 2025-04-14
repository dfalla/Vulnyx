# Máquina real

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.167

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,6667,6697,8067 -vvv -Pn 192.168.42.167

![alt text](image-2.png)

vemos la version de UnrealIRCd

### Explotación

copiamos el exploit https://github.com/Ranger11Danger/UnrealIRCd-3.2.8.1-Backdoor/blob/master/exploit.py

previamente configuramos el exploit

![alt text](image-3.png)

![alt text](image-4.png)

### Escalar privilegios

ejecutando la herramienta pspy64

![alt text](image-5.png)

analizamos que hay en /opt/task

![alt text](image-6.png)

verificamos los permisos en /etc/hosts

![alt text](image-7.png)

modificamos el /etc/hosts

![alt text](image-8.png)

nos ponemos en escucha en el puerto 65000

![alt text](image-9.png)

### user.txt

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)
