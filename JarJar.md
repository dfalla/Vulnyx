# Máquina JarJar
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.186

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.186

![alt text](image-2.png)

### Fuzzing Web

feroxbuster --url http://192.168.5.186/ -r -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

![alt text](image-4.png)

entro a la web y analizando el código fuente.

![alt text](image-3.png)

lo agrego al /etc/hotst

feroxbuster --url http://jarjar.nyx/ -r -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

![alt text](image-5.png)

### Explotación

Capturamos la petición con el burpsuite tratando de ingresar a admin.php para luego mandarlo al repeater y encontramos un archivo error.log que al parecer sería un LFI.

![alt text](image-6.png)

![alt text](image-7.png)

Hacemos path traversal saliendo de la carpeta logs:

![alt text](image-8.png)

busqué el archivo id_rsa del usuario jarjar

![alt text](image-9.png)

lo copié, le di permisos 600, lo crackié con la herramienta RSACrack e ingresé por ssh

![alt text](image-10.png)

### Escalar privilegios

ejecuté el comando find / -perm -4000 2>/dev/null

![alt text](image-11.png)

me pasé el /etc/shadow a mi kali

![alt text](image-12.png)

copié el hash y lo crackié

![alt text](image-13.png)

![alt text](image-14.png)

### user.txt

![alt text](image-15.png)

### root.txt

![alt text](image-16.png)