# pratica-4
En esta practica vamos a utilizar las dos maquinas creadas en la anterior practica (mysql y apacache) mas una nueva que vamos a crear.
Nos vamos a crear una nueva maquina frond-end con servidor web apache.
Esta maquina no la crearemos con los puertos ssh,http,https.

En esta maquina haremos los siguientes pasos mediante un script que lo ejecutara y instalará todo de golpe:

#!/bin/bash
# Actualizar PC
apt-get update

# Instalamos adminer
cd /var/www/html
mkdir adminer
cd adminer
wget https://github.com/vrana/adminer/releases/download/v4.7.3/adminer-4.7.3-mysql.php
mv adminer-4.7.3-mysql.php index.php

# 2. Instalar apache2
sudo apt-get install apache2 -y

# Arrancar el apache2
systemctl start apache2

# Instalar paquete
apt-get install php libapache2-mod-php php-mysql -y

# Instalamos git
apt-get install git -y

# Instalamos la aplicacion
cd /var/www/html
git clone https://github.com/josejuansanchez/iaw-practica-lamp.git
chown www-data:www-data * -R

# configurar el archivo config.php (sed -i cambia s/localhost por 54.85.90.14 que es nuestra maquina mysql)
cd /var/www/html/iaw-practica-lamp/src/
sed -i "s/localhost/54.85.90.14/" config.php
cat config.php
# Para ver que conecta con mysql
telnet 54.85.90.14 3306

