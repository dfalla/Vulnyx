# Máquina Express
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.179

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.179

![alt text](image-2.png)

como es un CTF de vulnyx, le añadí el dominio express.nyx al /etc/hosts


### Fuzzing Web

feroxbuster --url http://express.nyx/ -r -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

![alt text](image-3.png)

entro en la web para verificar:

![alt text](image-4.png)

![alt text](image-5.png)

y son endpoints, los verifico con burpsuite

![alt text](image-6.png)

la que me llamó la atención fue: /api/users?key=${secretKey}, lo que hice fue cambiar al método POST y obtuve usuarios:

![alt text](image-7.png)

la otra que me pareció interesante fue: /api/admin/availability, tengo que mandarle un cuerpo modificando el Content-Type: application/json

entonces comprobé que se trata de un posible SSRF:

levanté un servidor web por el puerto 8081

![alt text](image-8.png)

![alt text](image-9.png)

### Explotación

Lance el siguiente comando para verificar los puertos internos que corren en el host víctima:

primero creo un archivo que tenga numeros del 1 al 65535 con el comando:

seq 65535 > ports.txt

luego ejecuto el comando:

wfuzz -u "http://express.nyx/api/admin/availability" -d '{ "id": 18, "roles": [ "admin" ], "token": "4493-3179-0912-0597", "username": "JESSS", "url": "http://127.0.0.1:FUZZ" }' -H 'Content-Type: application/json' -X POST -w ports.txt --hw 25

![alt text](image-10.png)

entonces verificando la respuesta:

![alt text](image-11.png)

![alt text](image-12.png)

![alt text](image-13.png)

STTI

![alt text](image-14.png)

confirmé que se trata STTI ahora verifico si es jinja2

![alt text](image-15.png)

se trata de jinja2

Verifico el tipo de usuario que soy

![alt text](image-16.png)

### Escalar privilegios

me envié una reverse shell

![alt text](image-17.png)

![alt text](image-18.png)

### user.txt

![alt text](image-19.png)

### root.txt

![alt text](image-20.png)