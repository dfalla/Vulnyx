# Máquina shock

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.5.133

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,79,80 -vvv -Pn 192.168.5.133

![alt text](image-2.png)

### Fuzing web

feroxbuster --url http://192.168.5.133 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

![alt text](image-3.png)

me dice que tengo una respuesta 401 al directorio /backup

![alt text](image-6.png)

### Explotación

Entro a la web: http://192.168.5.133/

![alt text](image-4.png)

Me descargo la imagen y la subo a google para ver información de ella.

Encuenntro esto:

![alt text](image-5.png)

ahora como tengo finger corriendo hago lo siguiente:

finger horus@192.168.5.133

![alt text](image-7.png)

con las credenciales horus:H0Ru$$3rv3 inicio sesión en /backup

![alt text](image-8.png)

me descargo database.db

![alt text](image-9.png)

la abro con sqlite

sqlite3 database.db y veo las tablas

![alt text](image-10.png)

creo una lista de contraseñas con las credenciales y una lista de usuarios con los usernames y hago un ataque co hydra al puerto ssh

![alt text](image-11.png)

me conecto por ssh.

ssh seth@192.168.5.133

![alt text](image-12.png)

### Escalar privilegios

ejecuto sudo -l y me aparece el error:

![alt text](image-13.png)

entonces busco el binario sudo con el comando:

find / -name sudo -type f -exec ls -ld {} \; 2>/dev/null

![alt text](image-14.png)

![alt text](image-15.png)

el binario /usr/bin/nmcli es la herramienta de línea de comandos (CLI) para interactuar con NetworkManager, un servicio que gestiona las conexiones de red en sistemas Linux.

ver redes almacenadas:

![alt text](image-16.png)

ahora busco información sobre la red wifi MikroTik_AP 

![alt text](image-17.png)

ver contraseñas:

![alt text](image-18.png)

hago su root y escribo la contraseña encontrada

![alt text](image-19.png)

### user.txt

![alt text](image-20.png)

### root.txt

![alt text](image-21.png)
