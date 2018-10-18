# PostGIS minimum


## Zaklady prace s geodatabazi ## 


### 0. GIS.lab ###
Do GIS.lab klienta se pripojime bootem pres sitvou kartu pri startu PC. 

Desktop klienta: http://gislab.readthedocs.io/en/latest/client-layout/index.html

- Desktop aplikace: QGIS
- Geodatabaze: Postgis server a PgAdmin III, SpatiaLite
- Text editor: Leafpad
- Linux terminal 


### 1. Pripojeni do PostGIS databaze ###
[psql]

$sudo -u postgres psql 
$psql mydb
 
SELECT version();

\conninfo;


ALTER ROLE <user_name> SUPERUSER;

CREATE EXTENSION postgis;

ALTER ROLE <user_name> NONSUPERUSER;

\dt
\h -- help
\q -- odchod z psql


### 2. Vytvarime prostorovou databazi ### 
[CREATEDB]

createdb mydb -U jnovak -h server 

psql -d mydb -h server 

CREATE TABLE tbl-mesta 
   (id integer NOT NULL, 
   mesto character(30), 
   psc character(6), 
   geom geometry, 
   CONSTRAINT pk_id PRIMARY KEY (id)
   ); 

DROP TABLE tbl-mesta; 

dropdb mydb -U jnovak -h server


### 3. Import a export prostorovych dat v PostGIS ###
[GUI / CLI]


### Reference: ###
http://postgis.net/docs/manual-2.1/

#----------------------------------

### SQL opakovani ###

-- vyber z tabulky 
SELECT 		nazevatributu
FROM    	nazevtabulky
WHERE 		nazevatributu = 'hodnota'

-- tvorba tabulky 

CREATE TABLE	mojeDB
   (atribut1 charakter NOT NULL, 
   atribut2 integet NOT NULL, 
   CONSTRAINT pk_id PRIMARY KEY (atribut1)
   );



