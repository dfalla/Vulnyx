# Máquina Observer
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.169

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.169

![alt text](image-2.png)

### Fuzzing Web

feroxbuster --url http://192.168.5.169/ -w /usr/share/seclists/Discovery/Web-Content/big.txt

no encuentro nada interesante

entro a la web:

![alt text](image-3.png)

guardo los nombres en un archivo para usarlos como usuarios y a la vez contraseñas en un ataque de hydra hacia ssh:

![alt text](image-4.png)

Al intentar conectarme por shh se cierra la sesión, le paso el parámetro -X y veo una pantalla emergente con las credenciales de remo

![alt text](image-5.png)

### Explotación

Me conecté por ssh con las credenciales encontradas de remo:

![alt text](image-6.png)

### Escalar privilegios

En el archivo .bashrc dentro del directorio remo, ví un id_rsa encriptada

![alt text](image-7.png)

la desencripté con base64 decode

![alt text](image-8.png)

![alt text](image-9.png)

me conecté con el usuario root y su id_rsa

![alt text](image-10.png)

### user.txt

![alt text](image-11.png)

### root.txt

![alt text](image-12.png)
