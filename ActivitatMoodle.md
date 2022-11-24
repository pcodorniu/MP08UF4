# ACTIVITAT MOODLE 

## INSTAL·LACIÓ DEL MOODLE

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

## INSTAL·LEM L'APACHE

Instal·lem l'Apache
```
sudo apt-get install apache2
```
![image](https://user-images.githubusercontent.com/114162276/203822015-99774938-b499-48e3-aded-be6a4b4d578b.png)

## INSTAL·LEM EL MARIADB

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






























