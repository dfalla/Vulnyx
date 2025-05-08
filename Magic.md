# Máquina Magic

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.137

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,139,445 -vvv -Pn 192.168.5.137

![alt text](image-2.png)

### Fuzing web

feroxbuster --url http://192.168.5.137/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

No encontré nada interesante

### Samba

Enumerando samba con enum4linux encuentro un usuario xerosec

enum4linux 192.168.5.137

![alt text](image-3.png)

hago fuerza bruta para encontrar la contraseña

nxc smb 192.168.5.137 -u "xerosec" -p "/usr/share/wordlists/rockyou.txt" --ignore-pw-decoding

![alt text](image-4.png)

ahora veo los recursos compartidos:

nxc smb 192.168.5.137 -u xerosec -p david1 --shares

![alt text](image-5.png)

### Explotación

me conecto con smbclient:

![alt text](image-6.png)

Analizo archivos conf.

feroxbuster --url http://192.168.5.137/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x conf,yaml,env,xml

![alt text](image-7.png)

http://192.168.5.137/backup/conf/smb.conf

al verificar el archivo smb.conf, veo una vulnerabilidad crítica magic script, que al subir un archivo config.sh con un código de reverse shell lo ejecuta automáticamente:

![alt text](image-8.png)

config.sh

![alt text](image-9.png)

me pongo en escucha con netcat por el puerto 443

y subo el archivo config.sh al servidor samba

![alt text](image-10.png)

![alt text](image-11.png)


### Escalar privilegios

veo las capabilities

![alt text](image-13.png)

ejecuto:

![alt text](image-12.png)

### user.txt

![alt text](image-14.png)

### root.txt

![alt text](image-15.png)
