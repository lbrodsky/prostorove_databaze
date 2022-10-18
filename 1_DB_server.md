# Databazovy server 

* [PostgreSQL](https://www.postgresql.org/) / [PostGIS](https://postgis.net/) 
[<img src="https://postgis.net/logos/postgis-logo-small.png">](PostGIS)
* [SQLite](https://www.sqlite.org/index.html) / [SpatiaLite](https://www.gaia-gis.it/fossil/libspatialite/index)
[<img src="https://www.gaia-gis.it/fossil/libspatialite/logo">](Spatialite)

Systemy s DB serverem: 
1. Varianta: GIS.lab system
2. Varianta: predinstalovany server v OSGeo live
3. Varianta: localhost (vlastni notebook nebo desktop)

## 1. GIS.lab
[<img src="https://gislab.readthedocs.io/en/latest/_images/client-layout.png">](GIS.lab desktop layout)

Hlavni panel:
1. pousteni aplikaci 
2. ikonky vybranych 
3. virtualni desktopy
4. spustene aplikace
5. klavesnice 
6. bateria (u notebooku)
7. chat v siti GIS.lab
8. zvuk 
9. cas a kalendar

[Dokumentace GIS.lab systemu](https://gislab.readthedocs.io/en/latest/client-layout/index.html)

Do GIS.lab klienta se pripojime bootem pres sitvou kartu pri startu PC. 
Je nutne vyvolat vstup do BIOSu (F2 / DEL) a pote Ctrl+Alt+Del 

[<img src="https://gislab.readthedocs.io/en/latest/_images/client-layout-qgis.png">](Desktop klienta s Qgis)

- Desktop aplikace: QGIS
- Geodatabaze: PostgreSQL/PostGIS server a PgAdmin III, SpatiaLite
- Text editor: Leafpad
- Linux terminal: $  

[Vice o instalci zde](https://gislab.readthedocs.io/en/latest/client-layout/index.html)


## 2. OSGeo live
K vyuziti OSGeo live je treba instalovat: 
* VirtualBox (Oracle VM VirtualBox) https://www.virtualbox.org 
* OSGeo live, v.9/10 (linux) a vyssi https://live.osgeo.org/en/download.html

Potrebne sw aplikace: 
- Desktop aplikace: QGIS
- Geodatabaze: PostgreSQL/PostGIS server a PgAdmin III, SpatiaLite
- Text editor: Leafpad
- Linux terminal: $  (TODO nazev)

Soubor ../OSGeo/osgeolive-vm-9.0/osgeo-live-9.0.vmdk (nebo jina verze) je treba pripojit do VirtualBoxu.  

VirtualBox: New -> Name: OSGeo9.0, Linux, Ubuntu (64b) -> RAM: napr. 4GB a vice  
-> Use an existing …  Choose a virtual hard disk file (.. /OSGeo/osgeolive-vm-9.0/osgeo-live-9.0.vmdk)
-> Create -> Start


TODO: vlastni lokalni instalace
## 3. Lokalni instalce (localhost) 

### 3.1 Windows 

### 3.2 GNU/Linux 

[PostgreSQl](https://www.postgresql.org/)

#### Instalace PostgreSQL na Linuxu

Download -> Linux -> Ubuntu 

```$```je prompt terminalu. 

```
$ sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

$ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

$ sudo apt-get update

# posgresl-15 
$ sudo apt-get -y install postgresql

# check version 
$ apt show posgresql 
```

Prvni kroky v Postgresql

```

1. Pripojte se do DB pomoci defaultniho uzivatelepostgres:

$ sudo -u postgres psql template1

2. Nastavte heslo pro uzivatele postgres, pak exit psql (Ctrl-D):

$ ALTER USER postgres with encrypted password 'xxxxxxx';

3. Editujte konfiguraci pg_hba.conf pro danou verzi:

$ sudo vim /etc/postgresql/15/main/pg_hba.conf

a zmente "peer" na "md5" na radce pro postgres:

    local      all     postgres     peer md5

4. Restart the database :

$ sudo /etc/init.d/postgresql restart

5. Vytvorte uzivatele se stejnym jmenem jako jste v linuxu prihlaseny. 

$ sudo createuser -U postgres -d -e -E -l -P -r -s <my_name>

# The options tell postgresql to create a user that can login, create databases, create new roles, is a superuser, and will have an encrypted password. The really important ones are -P -E, so that you're asked to type the password that will be encrypted, and -d so that you can do a createdb.

# Beware of passwords: it will first ask you twice the new password (for the new user), repeated, and then once the postgres password (the one specified on step 2).

6. Opet opravte pg_hba.conf 

local      all     all     md5

7. Restartujte stjne jako v kroku 4 
a overte logovani bez  -U postgres:

$ psql template1

# Note that if you do a mere psql, it will fail since it will try to connect you to a default database having the same name as you (i.e. whoami). template1 is the admin database that is here from the start.

    
8. Nyni vytvorte svoji novou databazi 

$ createdb <dbname> should work.

```


#### Instalace PgAdmin na Linuxu


[PgAdmin](https://www.pgadmin.org/)

Download -> APT 

```
# Instrukce: 
#
# Setup the repository
#

# Install the public key for the repository (if not done previously):
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg

# Create the repository configuration file:
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

#
# Install pgAdmin
#

# Install for both desktop and web modes:
sudo apt install pgadmin4

# Install for desktop mode only:
sudo apt install pgadmin4-desktop

# Install for web mode only: 
sudo apt install pgadmin4-web 

# Configure the webserver, if you installed pgadmin4-web:
sudo /usr/pgadmin4/bin/setup-web.sh

```

TODO: setup web PgAdmin to run it! 