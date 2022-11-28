# Instalar y configurar Moodle en Linux
SMX-B MP08

####  Alumnes
* Marc Muria 


#### Professor
* Javier Sancho 

## Índex 
* Apache2
* MariaDB
* PHP 
* Moodle

## Actualizar los paquetes de Ubuntu.

Lo primero que vamos a hacer es actualizar el repositorio de nuestra distribución para asegurarnos que instalemos los últimos paquetes de cada programa. Para ello introducimos en el terminal el siguiente comando:
```
sudo apt-get update
```
## Instal·lació Apache2

En cuanto se hayan actualizado los paquetes, con el comando anterior, instalamos el servidor web Apache con el siguiente comando:
```
sudo apt-get install apache2
```
![imatge](1.1.png)

Para comprobar que hemos instalado correctamente Apache en nuestra máquina podemos ir a nuestro navegador favorito e introducir localhost como dirección a visitar en la barra de direcciones, momento en que se nos mostrará algo similar a lo siguiente:

![imatge](1.png)

Apache nos muestra los ficheros que tengamos en /var/www/html/ por defecto, o lo que es lo mismo el fichero /var/www/html/index.html, que es el que observamos en la imagen anterior.

## Instal·lació de MariaDB

Instalamos la base de datos con el siguiente comando:
```
sudo apt-get install mariadb-server
```
![imatge](1.2.png)

Durante la instalación solicitará la contraseña para el usuario root de la base de datos.

Cuando se haya terminado de instalar deberás ejecutar la configuración de seguridad del servidor MariaDB con el siguiente comando:
```
sudo mysql_secure_installation
```
A continuacio tindrem que habilitar i deshabilitar lo seguent.
* Deshabilitar usuaris anònims.
* Desactivar accés remot com a root.
* Eliminar les bases de dades de testeig i accedir-hi.
* Actualitzar les taules de privilegis.

I Reiniciarem MariaDB 
```
sudo service mariadb.service restart
```
## Instal·lació de PHP

Abans de procedir a la instal·lació haurem d'obrir una terminal i actualitzar els paquets del sistema. A més instal·larem algunes dependències amb la comanda següent:
```
sudo apt update; sudo apt upgrade
```
![imatge](1.3.png)
```
sudo apt install ca-certificates apt-transport-https software-properties-common
```
![imatge](1.4.png)

Finalitzada la instal·lació de les dependències, ja hi podem afegir el PPA d'Ondrej . A la mateixa terminal, només necessitarem utilitzar l'ordre:
```
sudo add-apt-repository ppa:ondrej/php
```
![imatge](1.5.png)

Després d'afegir el PPA al nostre equip, s'hauria de produir l'actualització de paquets disponibles des dels dipòsits.

Ara haurem d'instal·lar el PHP 8.0 amb el mòdul Apache. Per fer-ho només caldrà executar la següent comanda:
```
sudo apt install php8.0 libapache2-mod-php8.0
```
![imatge](1.6.png)

Un cop finalitzada la instal·lació, haurem de reiniciar el servidor web Apache per habilitar el mòdul amb la comanda:
```
sudo systemctl restart apache2
```
![imatge](1.7.png)

Arribats a aquest punt, ja podem confirmar la versió de PHP predeterminada al servidor:
```
php -v
```
![imatge](1.8.png)

## Instalar Moodle

Tindrem que descarregar el arxiu del moodle.
```
wget <Link de l'arxiu que hem descarregar>
```
![imatge](1.9.png)

Per descomprimir-lo i col·locar-lo al directori /var/www/html i fer-lo accessible via web executem la següent ordre:
```
sudo unzip <Link de l'arxiu que hem descarregar> -d /var/www/html/
```
![imatge](1.10.png)
```
sudo chown www-data:www-data /var/www/html/moodle
```
![imatge](1.11.png)

## Crear el directori de fitxers

Moodle utilitza un directori per desar fitxers dels usuaris, és recomanable que aquest directori no estigui al mateix directori que el servidor web, però ha de ser un directori amb accés per part del navegador.

Jo, per exemple, crearem el directori moodledata en home.
```
cd /home/
sudo mkdir moodledata
sudo chown www-data:www-data moodledata/
```
![imatge](1.12.png)
![imatge](1.12.1.png)

## Configurar la base de dades

Ara haurem de crear una base de dades per al Moodle, per accedir a la base de dades MariaDB haurem d'introduir la seguent comanda:
```
sudo mysql -u root -p
```
![imatge](1.13.png)

Creem un usuari per a moodle, per exemple moodlemanager:
```
CREATE USER 'moodlemanager'@'localhost' IDENTIFIED BY 'managermoodle';
```
![imatge](1.14.png)

I crearem la base de dades per a l'ús de moodle:
```
CREATE DATABASE moodle;
```
![imatge](1.15.png)

Finalment, concedeix control sobre la base de dades moodle a l'usuari moodlemanager que hem creat abans:
```
GRANT ALL PRIVILEGES ON moodle.* TO 'moodlemanager'@'localhost';
FLUSH PRIVILEGES;
```
![imatge](1.16.png)

Amb aixo ya ho tindriem.
 
![imatge](1.17.png)


![image](https://user-images.githubusercontent.com/114423194/204347569-23dcf4d8-f176-4980-a573-2b56b20301e8.png)


