# PostGIS minimum


## Zaklady prace s geodatabazi PostGIS ## 


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

SELECT postgis_full_version;

\conninfo;









### 2. Vytvarime prostorovou databazi ### 
[CREATEDB, CREATE TABLE]

ALTER ROLE <user_name> SUPERUSER; 

CREATE EXTENSION postgis;

ALTER ROLE <user_name> NONSUPERUSER;

\dt
\h -- help
\q -- odchod z psql

SELECT *
FROM spatial_ref_sys
WHERE SRID==5514;

-- createdb

createdb mydb -U jnovak -h server 

psql -d mydb -h server 


-- CREATE TABLE 

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
[INSERT, DELETE, WKT, WKB, shp2pgsql, ogr2ogr] 

-- INSERT

INSERT INTO tbl_mesta(id, mesto, geom, ulice)	
VALUES 
(1,'Mesto1', ST_GeomFromEWKT('SRID=4326;POINT(14.42450567543761863 50.06887390896474699)'), 'Ulice1'), 
(2,'Mesto2', ST_GeomFromEWKT('SRID=4326;POINT(14.42350490489711845 50.08645450656709386)'), 'Ulice2'), 
(3,'Mesto3', ST_GeomFromEWKT('SRID=4326;POINT(14.42399707376493545 50.08708758612597478)'), 'Ulice3'); 

-- Prostorove konstruktory
ST_GeomFromWKB(bytea, SRID) -> geometrie
ST_GeomFromText(text, SRID) -> geometrie

-- WKT/WKB
ST_AsBinary(geometrie) -> WKB
ST_AsText(geometrie)    -> WKT


DELETE FROM tbl_mesta WHERE id=1;


SELECT DropGeometryColumn('tbl_mesta', 'geom');

SELECT AddGeometryColumn('tbl_mesta', 'geom', 4326, 'POINT', 2);


$shp2pgsql -s 5514 SidlaBody.shp public.sidla > sidla.sql

$psql -U jnovak -d mydb -a -f sidla.sql

$ogr2ogr -f PostgreSQL \
PG:"dbname=mydb  host=server user=jnovak password=******** \
active_schema=public" \
SidlaBody.shp \
-a_srs EPSG:5514





### Reference: ###
http://postgis.net/docs/manual-2.1/

#----------------------------------

### SQL opakovani ###

-- vyber z tabulky (SELECT)

SELECT 		nazevatributu
FROM    	nazevtabulky
WHERE 		nazevatributu = 'hodnota'

-- tvorba tabulky 

CREATE TABLE	mojeDB
   (atribut1 integer NOT NULL, 
   atribut2 character(20) NOT NULL, 
   CONSTRAINT pk_id PRIMARY KEY (atribut1)
   );

-- Vkladani dat do tabulky (INSERT)

INSERT INTO tbl_neco(atribut1, atribut2)
VALUES (1, ‘Praha’);
