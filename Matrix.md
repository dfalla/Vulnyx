# Máquina Matrix
### Reconocimiento de la Ip de la máquina víctima

![alt text](image.png)

### Puertos abiertos

sudo nmap -sS --disable-arp-ping --min-rate 6000 -p- --open -vvv -Pn 192.168.5.177

![alt text](image-1.png)

### Servicios y versiones

sudo nmap -sVC --min-rate 6000 -p22,80 -vvv -Pn 192.168.5.177

![alt text](image-2.png)


### Fuzzing Web

feroxbuster --url http://192.168.5.177/ -r -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

![alt text](image-3.png)

Me fui a ver la web:

![alt text](image-4.png)

observé el código fuente

![alt text](image-5.png)

hice fuzzing para encontrar el archivo .pcap

feroxbuster --url http://192.168.5.177/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x pcap

![alt text](image-6.png)

lo descargué y lo abrí con wireshark

![alt text](image-7.png)

encontré nombres de usuarios y contraseñas

![alt text](image-8.png)

encontré una imagen:

![alt text](image-9.png)

la descargué, le cambié el nombre y le apliqué exiftool

![alt text](image-10.png)

encontré un subdominio:

![alt text](image-11.png)

lo agregué al /etc/hosts y entré por url

después de muchos intentos:

![alt text](image-12.png)

entré al archivo:

![alt text](image-13.png)

### Explotación

Interceptamos con burpsuite y lo mandamos al repeater

![alt text](image-14.png)

![alt text](image-15.png)

coloco el siguiente objeto:

![alt text](image-16.png)

lo encodeo:

![alt text](image-17.png)

ahora en la url:

![alt text](image-18.png)

verifico si está el binario python3

![alt text](image-19.png)

me envío una reverse shell por el puerto 443, me coloco en escucha por dicho puerto

![alt text](image-20.png)

![alt text](image-21.png)

veo los usuarios:

![alt text](image-22.png)

cambio al usuario smith ya que había encontrado la contraseña previamente


### Escalar privilegios

siendo el usuario smith

![alt text](image-23.png)

![alt text](image-24.png)

### user.txt

![alt text](image-25.png)

### root.txt

![alt text](image-26.png)