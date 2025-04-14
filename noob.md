# Máquina noob

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.165

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.42.165

![alt text](image-2.png)


### Fuzzing web

gobuster dir -t 200 -u http://192.168.42.165 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,bak,sh,py,js,html,db,png,jpg,git,swp -b 403,404 2>/dev/null

![alt text](image-3.png)

entramos en /notes.txt

![alt text](image-4.png)

cuando se cierra un editor como por ejemplo vim sin que se haya guardado queda un archivo .swp como respaldo

hacemos gobuster para encontrar el archivo .swp

![alt text](image-5.png)

vemos el archivo por la web:

![alt text](image-6.png)

### Explotación

![alt text](image-7.png)

escribimos el passphrase:

![alt text](image-8.png)

### Escalar privilegios

Para escalar privilegios utilicé la herramienta https://github.com/d4t4s3c/suForce

![alt text](image-9.png)

### user.txt

![alt text](image-10.png)

### root.txt

![alt text](image-11.png)
