# PracticaBaseDades

## Percona MySQL

Instal.larem els paquets corresponents...

$ sudo yum install percona-server-server

![image](https://user-images.githubusercontent.com/100163765/155021279-c4bc197c-c908-4f77-8841-9b168b739ec5.png)


Obrirem els ports:

•	3306 s'utilitza per a connexions de client MySQL i SST (Transferència d'instantània d'estat) mitjançant mysqldump.
•	4444 s'utilitza per a SST a través de Percona XtraBackup .
•	4567 s'utilitza per al trànsit de rèplica de conjunt d'escriptura (a través de TCP) i per a la rèplica de multidifusió (a través de TCP i UDP).
•	4568 s'utilitza per a IST (Transferència d'estat incremental).


•	Cal tenir en compte que la documentació va dirigida a tècnics informàtics i no a usuaris no experts.

•	Es valorarà la presentació, l'organització del text i la facilitat de lectura.

## 1.	Un cop realitzada la instal·lació realitza una securització de la mateixa. Quin programa realitza aquesta tasca? Realitza una securització de la instal·lació indicant que la contrasenya de root sigui patata.

Utilitzarem  mysql_secure_installation, que és un script d'intèrpret d'ordres disponible als sistemes Unix i  permet millorar la seguretat de l’instal·lació de Sql i percona de les maneres següents:

Podrem posar una contrasenya a les comptes de root, també podrem eliminar les contes de root que son vulnerables des de fora de el servidor local i ens podrem carregar la base de dades de prova que, si no ho fem, poden accedir usuaris anònims.

## 2.	Quines són les instruccions per arrancar / verificar status / apagar servei de la base de dades de Percona Server en el CentOS 7

Farem les típiques comandes de start, restart, stop:
Systemctl restart mysql.service
Systemctl stop mysql.service
Systemctl start mysql.service

![image](https://user-images.githubusercontent.com/100163765/155031902-0cb4e66e-afde-41de-8136-5de7aefde219.png)

![image](https://user-images.githubusercontent.com/100163765/155031910-c1486345-428e-4c56-9ac1-1910545ec14a.png)


## 3.	A on es troba i quin nom rep el fitxer de configuració del SGBD Percona Server?

Ho trobarem a: /etc/my.cnf el nom fa referencia al propi MySql, my.cnf ens permetrà configurar els valors clau per fer funcionar bé la nostra maquina:

![image](https://user-images.githubusercontent.com/100163765/155031944-dc35719e-0de0-450c-95e7-ccb830464f63.png)


## 4.	A on es troben físicament els fitxers de dades (per defecte). Com ho has sabut?

Els fitxers sql es guarden a la seva carpeta /var/lib/mysql, ja instal·lem un percona un mongo db o cualsevol altre Gestor de base de dades. 

Fent un Ls per exemple podem veure els arxius.

![image](https://user-images.githubusercontent.com/100163765/155031983-afb43781-7af5-4665-929d-8b42be1ad08c.png)

## 5.	Crea un usuari anomenat asix en el sistema operatiu i en SGBD de tal manera que aquest usuari del sistema operatiu no hagi d'introduir l'usuari i password cada vegada que cridem al client mysql?

i.	https://dev.mysql.com/doc/refman/8.0/en/password-security-user.html
ii.	Usuari SO-→ asix / patata
Primer afegeixo l’usuari i li assigno una contrasenya:

![image](https://user-images.githubusercontent.com/100163765/155032040-444c5272-1b7e-4465-ae57-bf7ec1b30d1c.png)

iii.	Usuari MySQL → asix / patata

Ara haurem de canviar la contrasenya de el mysql per poder entrar, primer aconseguirem la contrasenya aleatòria que se ens ha assignat: 

![image](https://user-images.githubusercontent.com/100163765/155032074-e6334eec-c0bc-434d-8c0a-98eebf0b9e06.png)

I la canviarem:
![image](https://user-images.githubusercontent.com/100163765/155032142-9674fd9c-d5be-463d-9986-866ecd80d1a1.png)
![image](https://user-images.githubusercontent.com/100163765/155032147-2529c92f-ada6-4a1a-93b3-496b40f0b4a4.png)


Ara ja tindrem accés a la consola SQL:

![image](https://user-images.githubusercontent.com/100163765/155032164-49af7ed4-f2eb-4376-94a1-7c0714864a5b.png)

Ara crearem l’usuari, li posarem una contrasenya diferent, ja que amb les polítiques de contrasenyes del mysql no podem posar una contrasenya que no tingui una certa dificultat:

![image](https://user-images.githubusercontent.com/100163765/155032179-6631e68b-3be2-4816-a945-2e82344a3700.png)

I li donarem els privilegis adients:

![image](https://user-images.githubusercontent.com/100163765/155032208-a9d468d4-ec0e-429f-b421-f0d15c9805f4.png)


## 6.	El servei de MySQL (mysqld) escolta al port 3306. Quina modificació/passos caldrien fer per canviar aquest port a 33306 per exemple?
## 7.	Important: No realitzis els canvis. Només indica els passos que faries.

Simplement entrarem al arxiu de configuració, i li direm:

Port = 33306

![image](https://user-images.githubusercontent.com/100163765/155032246-6b8991fd-27ac-495d-8c51-b8aec4ec6937.png)

Farem control + x i li direm que no volem guardar per no aplicar els canvis.

## 8.	Ensenya al professor que us podeu connectar al SGBD.

Per  comprovar si em puc connectar a la base de dades, utilitzaré el MYSQL Workbench, que es un entorn  d’interfície gràfica  per gestionar mysql que es fàcil  d’entendre. Afegirem a l’usuari ASIX

![image](https://user-images.githubusercontent.com/100163765/155032305-df47b2c2-e9c7-4986-9648-23c9305a2227.png)

Aquest es el menú per afegir un nou settup, abans haurem d’obrir el port 3306 al mysql, sinó, no hi podrem accedir ja que el Firewall tallarà la connexió.

![image](https://user-images.githubusercontent.com/100163765/155032328-b0ce5be7-4e09-4039-a642-c3559303785a.png)

I haurem de fer un FLUSH PRIVILEGES:

![image](https://user-images.githubusercontent.com/100163765/155032344-b8621cf9-3c2a-4fd1-944a-dafbcf507ff7.png)

Ara ja podrem entrar:

![image](https://user-images.githubusercontent.com/100163765/155032365-9a168d90-70d9-4090-8cb5-cae50ce69e26.png)

Per fer una prova he baixat el nivell de la seguretat de les polítiques per posar la contrasenya que volguem:

![image](https://user-images.githubusercontent.com/100163765/155032383-dfef09f8-5736-4afe-bb29-2595f7205c43.png)

I ara ja li podrem posar la contrasenya patata.

![image](https://user-images.githubusercontent.com/100163765/155032404-c40b7012-8b25-44bd-803b-cf87e60f7a47.png)







