# ACTIVITAT MOODLE 


### INSTAL·LEM L'APACHE

Instal·lem l'Apache
```
sudo apt-get install apache2
```
![image](https://user-images.githubusercontent.com/114162276/203822015-99774938-b499-48e3-aded-be6a4b4d578b.png)


### INSTAL·LEM EL MARIADB

Instal·lem el MariaDB
```
sudo apt-get install mariadb-server
```
![image](https://user-images.githubusercontent.com/114162276/203822532-5a67ad55-343e-49cd-8cc1-66b6ec41359c.png)

Ara executem la configuració de seguritat del servidor MariaDB
```
sudo mysql_secure_installation
```
![image](https://user-images.githubusercontent.com/114162276/203823658-a0c34dbe-7b5a-4869-bd95-0bb2d2555fd5.png)

Posem la següent comanda per a que demani contrasenya als usuaris que intenten connectar-se com a root

```
sudo mysql -u root -p
```
![image](https://user-images.githubusercontent.com/114162276/203825097-8483bfc2-0faa-46e4-87f5-9492db216d33.png)


### INSTAL·LAR EL PHP

Instal·larem la versió 7.3 del PHP, perquè l'ultima versio del PHP no es compatible amb l'ultima versio del Moodle
```
sudo aptitude install php7.3 php7.3-mysql php7.3-intl php7.3-curl php7.3-xml php7.3-gd
```
![image](https://user-images.githubusercontent.com/114162276/203827179-9031d5a4-19b1-427e-b9fd-4b17fe0edb95.png)

Ara canviarem la prioritat del fitxer php a la configuració de Apache per a que ens mostri primer el **index.php** i no el **index.html**
```
sudo nano /etc/apache2/mods-enabled/dir.conf

```
![image](https://user-images.githubusercontent.com/114162276/203828797-c3bd5929-c128-4f6b-bf00-9c2a7880d669.png)

Per a que els canvis es guarden tenim que reiniciar el servidor Apache
```
sudo service apache2 restart
```
![image](https://user-images.githubusercontent.com/114162276/203829161-1cb31e5d-9fd7-45c2-84d4-0d68c8987ce2.png)

Comprovem el seu estat
```
sudo service apache2 status
```
![image](https://user-images.githubusercontent.com/114162276/203829294-ed6c6519-f052-4fe3-b8c0-af56212c924c.png)

El apache esta actiu pero ho comprovarem d'una altra manera per a assegurar-nos millo, creem un fitxer a **/var/www/html/** amb el nom de index.php
```
sudo nano /var/www/html/index.php
```
Dins del fitxer escrivim la següent linia
```
<?php phpinfo(); ?>
```
![image](https://user-images.githubusercontent.com/114162276/203831281-397a7262-9bc0-4f29-9488-ca2ce53b852b.png)

Si afegim a la barra del buscada **localhost** o **la IP de la maquina** ens apareixera lo següent
![image](https://user-images.githubusercontent.com/114162276/203831706-d82f45e0-36a4-4ff6-b833-699529a7453c.png)

Per seguretat borrem l'arxiu que hem creat anteriorment
```
sudo rm  /var/www/html/index.php
```
![image](https://user-images.githubusercontent.com/114162276/203832217-b8a050ad-3c77-4e36-a7ab-a6219a453cd3.png)


### INSTAL·LACIÓ DEL MOODLE

Anem a la pàgina oficial de Moodle i descarguem l'ultima versió.
![image](https://user-images.githubusercontent.com/114162276/203820107-1f21f59e-2150-4eb3-aecd-5a6752feb6d8.png)

Posem al terminal la següent comanda per a instal·lar el Moodle 
```
wget https://download.moodle.org/download.php/direct/stable400/moodle-latest-400.zip
```
![image](https://user-images.githubusercontent.com/114162276/203820522-1ccd1e3d-6afa-4f36-a36b-1da103f67b67.png)

Actualitzem tots els paquets del sistema
```
sudo apt-get update
```
![image](https://user-images.githubusercontent.com/114162276/203821696-6aba8508-0a4a-4c4b-bd9a-1411d237090e.png)

Descomprimim l'arxiu i el coloquem al directori /var/www/html/
```
sudo unzip moodle-latest-38.zip -d /var/www/html/
```
![image](https://user-images.githubusercontent.com/114162276/203833266-0743b12e-9365-4469-b1ec-c18ef6ae76c4.png)

Ara canviem els permisos del directori per a que Apache pugui modificar
```
sudo chown www-data:www-data /var/www/html/moodle
```
![image](https://user-images.githubusercontent.com/114162276/203833769-1ece2c47-8b6a-408c-b3ec-4716169fc530.png)

### CREACIÓ DEL DIRECTORI DE FITXERS

Creem el directori on Moodle guardara els fitxers dels usuaris i canvia els permisos d'aquest per a que pugui accedir Apache.
```
cd /home
sudo mkdir moodledata
sudo chown www-data:www-data moodledata/
```
![image](https://user-images.githubusercontent.com/114162276/203834355-39b051d7-9a6c-4870-8737-76f2af450678.png)

En aquest directori es pujaran els fitxers que estaran als cursos del Moodle

### CONFIGURAR BASE DE DADES

Accedim a la base de dades
```
mysql -u root -p
```
![image](https://user-images.githubusercontent.com/114162276/203845258-82dae297-a282-4783-b283-077a3b88de33.png)

Crea un usuari per al Moodle
```
CREATE USER 'moodlemanager'@'localhost' IDENTIFIED BY 'managermoodle';
```
![image](https://user-images.githubusercontent.com/114162276/203845440-70173dd7-637d-46c4-aeab-60ad0726d58f.png)

Creem la base de dades per a l'us del moodle

```
CREATE DATABASE moodle;
```
![image](https://user-images.githubusercontent.com/114162276/203845671-fd7c0aaa-5019-4ad2-b6da-8ca25ef49a9a.png)

Finalment concedeix control sobre la base de dades moodle a l'usuari que hem creat anteriorment 
```
GRANT ALL PRIVILEGES ON moodle.* TO 'moodlemanager'@'localhost';
FLUSH PRIVILEGES;
```
![image](https://user-images.githubusercontent.com/114162276/203845952-5bc093b4-255c-4e6e-aebc-e699f766b7fb.png)


### CONFIGURAR MOODLE

Obrim el navegador i al buscador posem **localhost/moodle** o **IP de la maquina/moodle** i ens apareixera el següent
![image](https://user-images.githubusercontent.com/114162276/203846190-2383a429-2eb5-4445-8d09-11121e2bcdd4.png)

Li indiquem l'idioma que volem utilitzar per al nostre moodle, en el meus cas es el Catala
![image](https://user-images.githubusercontent.com/114162276/205075628-3e13438b-4d57-426b-a75c-8dbde975a323.png)

El moodle realitzara una comprovació de requisits, en el meu cas hem demana una extenció de PHP Zip
![image](https://user-images.githubusercontent.com/114162276/205076788-e487e10c-302d-46c3-a184-82125a4192f5.png)

Busquem amb la següent comanda els paquets per al zip, i instal·lem el php7.3-zip
![image](https://user-images.githubusercontent.com/114162276/205078041-d9c8f2eb-d882-43d8-8841-cddee61d31d2.png)
![image](https://user-images.githubusercontent.com/114162276/205079523-57d7c6db-444c-4610-95e2-a2a501fbbf7b.png)

Reiniciem el servidor apache

![image](https://user-images.githubusercontent.com/114162276/205078780-d5fe5d9a-cdb9-4e92-b245-ef15e21fe06f.png)

Ara ens pregunta l'URL de moodle i on esta el directori de moodle li posem el que hem creat anteriorment
![image](https://user-images.githubusercontent.com/114162276/205080611-76d50120-64de-4e83-813a-c2d28b614904.png)

Ara ens preguntara el controlador de la base de dades que utilitzara, en el nostre cas li indiquem MariaDB que es la que hem instal·lat anteriorment
![image](https://user-images.githubusercontent.com/114162276/205081187-cde5fcc3-04ca-4fe1-b105-5ccf775e9366.png)

En aquesta pagina ens pregunta la direcció de la base de dades (localhost), el de la base de dades (moodle), el usuari (moodlemanager) i la seva contrasenya (managermoodle), els altres apartats els deixem en blanc
![image](https://user-images.githubusercontent.com/114162276/205082342-e35c378d-db61-4473-857b-0c45c31ae49e.png)

En el meu cas m'ha aparegut aquest error
![image](https://user-images.githubusercontent.com/114162276/205084463-1772ca64-9832-43ef-be02-a4533632e489.png)

Utilitzarem la següent comanda per a busca la versió del **mbstring**
![image](https://user-images.githubusercontent.com/114162276/205084903-e586b6a3-de72-4642-adec-a65a45a4af35.png)

Ara instal·lem l'extensió en la versio 7.3 que es la mateixa que la del PHP
![image](https://user-images.githubusercontent.com/114162276/205085355-0ba59bb2-6308-401f-b289-6c58ed6f3ba0.png)

Reiniciem el servei apache
![image](https://user-images.githubusercontent.com/114162276/205086507-219e0fb2-ea3d-435a-ac28-a30f90db32d0.png)


















