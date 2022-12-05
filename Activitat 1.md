# Crear Categories i cursos
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
![1 1](https://user-images.githubusercontent.com/114423194/204348390-445dd153-a332-4b09-88b2-432a9a78ca0d.png)
Para comprobar que hemos instalado correctamente Apache en nuestra máquina podemos ir a nuestro navegador favorito e introducir localhost como dirección a visitar en la barra de direcciones, momento en que se nos mostrará algo similar a lo siguiente:

![1](https://user-images.githubusercontent.com/114423194/204348411-2b2e7c08-e656-4f42-88cb-6e5cf42d1623.png)
Apache nos muestra los ficheros que tengamos en /var/www/html/ por defecto, o lo que es lo mismo el fichero /var/www/html/index.html, que es el que observamos en la imagen anterior.

## Instal·lació de MariaDB

Instalamos la base de datos con el siguiente comando:
```
sudo apt-get install mariadb-server
```
![1 2](https://user-images.githubusercontent.com/114423194/204348373-2c42a5e6-9ea4-4f22-bf88-aa6a958ac515.png)
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
![1 3](https://user-images.githubusercontent.com/114423194/204348356-90799230-c718-4498-af3d-e97d08d81817.png)```
sudo apt install ca-certificates apt-transport-https software-properties-common
```
![1 4](https://user-images.githubusercontent.com/114423194/204348345-145833ef-b55f-4814-b8ad-9e65263c7d92.png)
Finalitzada la instal·lació de les dependències, ja hi podem afegir el PPA d'Ondrej . A la mateixa terminal, només necessitarem utilitzar l'ordre:
```
sudo add-apt-repository ppa:ondrej/php
```
![1 5](https://user-images.githubusercontent.com/114423194/204348327-6dbaf419-5d4b-4830-b88d-5d7ecfada731.png)
Després d'afegir el PPA al nostre equip, s'hauria de produir l'actualització de paquets disponibles des dels dipòsits.

Ara haurem d'instal·lar el PHP 8.0 amb el mòdul Apache. Per fer-ho només caldrà executar la següent comanda:
```
sudo apt install php8.0 libapache2-mod-php8.0
```
![1 6](https://user-images.githubusercontent.com/114423194/204348307-d3985a91-63cc-43be-b114-08844015ceae.png)
Un cop finalitzada la instal·lació, haurem de reiniciar el servidor web Apache per habilitar el mòdul amb la comanda:
```
sudo systemctl restart apache2
```
![1 7](https://user-images.githubusercontent.com/114423194/204348297-d8b11ca6-90d6-4845-b816-e032e04b94b0.png)
Arribats a aquest punt, ja podem confirmar la versió de PHP predeterminada al servidor:
```
php -v
```
![1 8](https://user-images.githubusercontent.com/114423194/204348278-22fe864d-d3f1-4135-83c1-b4027dd088bb.png)
## Instalar Moodle

Tindrem que descarregar el arxiu del moodle.
```
wget <Link de l'arxiu que hem descarregar>
```
![1 9](https://user-images.githubusercontent.com/114423194/204348265-e4bfa133-0956-405d-9a76-7c08fa4de0df.png)
Per descomprimir-lo i col·locar-lo al directori /var/www/html i fer-lo accessible via web executem la següent ordre:
```
sudo unzip <Link de l'arxiu que hem descarregar> -d /var/www/html/
```
![1 10](https://user-images.githubusercontent.com/114423194/204348245-d83291ee-f1d9-4493-9f66-1e298af38cd1.png)```
sudo chown www-data:www-data /var/www/html/moodle
```
![1 11](https://user-images.githubusercontent.com/114423194/204348201-00b5db32-bd0f-4c09-a68b-fa290088da96.png)

## Crear el directori de fitxers

Moodle utilitza un directori per desar fitxers dels usuaris, és recomanable que aquest directori no estigui al mateix directori que el servidor web, però ha de ser un directori amb accés per part del navegador.

Jo, per exemple, crearem el directori moodledata en home.
```
cd /home/
sudo mkdir moodledata
sudo chown www-data:www-data moodledata/
```
![1 12](https://user-images.githubusercontent.com/114423194/204348098-d623e546-35a6-41b8-bda7-e425f8c2bd17.png)![imatge]
![1 12 2](https://user-images.githubusercontent.com/114423194/204348171-296160a1-93a6-4f14-885b-58e3d83801a6.png)


## Configurar la base de dades

Ara haurem de crear una base de dades per al Moodle, per accedir a la base de dades MariaDB haurem d'introduir la seguent comanda:
```
sudo mysql -u root -p
```
![1 13](https://user-images.githubusercontent.com/114423194/204348003-da3f5ce1-171e-4928-bac1-f3a7d7886904.png)
Creem un usuari per a moodle, per exemple moodlemanager:
```
CREATE USER 'moodlemanager'@'localhost' IDENTIFIED BY 'managermoodle';
```
![1 14](https://user-images.githubusercontent.com/114423194/204347976-a7d103a3-1671-4dac-83a2-baab11d82ddb.png)
I crearem la base de dades per a l'ús de moodle:
```
CREATE DATABASE moodle;
```
![1 15](https://user-images.githubusercontent.com/114423194/204347927-78e92b04-f3c6-4543-a2fa-d9dd0c8b55dd.png)

Finalment, concedeix control sobre la base de dades moodle a l'usuari moodlemanager que hem creat abans:
```
GRANT ALL PRIVILEGES ON moodle.* TO 'moodlemanager'@'localhost';
FLUSH PRIVILEGES;
```

![1 16](https://user-images.githubusercontent.com/114423194/204347873-770c6c1c-f26f-4f16-90f6-140d0a01032f.png)


Amb aixo ya ho tindriem.
 
![image](https://user-images.githubusercontent.com/114423194/204347569-23dcf4d8-f176-4980-a573-2b56b20301e8.png)


