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

### 3. Prostorove funkce ### 

-- Mereni rozmeru 2D, 3D
-- ST_Distance vraci 2D vzdalenost v kartezkem souradnicovym systemu dvou geometrii v jednotkach projekce
float ST_Distance(geometry g1, geometry g2);

-- ST_Length vraci 2D delku geometrie pro typy LineString nebo MultiLineString
float ST_Length(geometry a_2dlinestring);

-- ST_Dwithin vraci True jestlize jsou geometrie v ramci zadane vzdalenosti, jedna se o filter
boolean ST_DWithin(geometry g1, geometry g2, double precision distance_of_srid);

--
-- Prostorove vztahy
-- ST_Intersects vraci True jestlize se dve geometrie prekryvaji (pracuje s obalkou) 
boolean ST_Intersects( geometry geomA , geometry geomB );

-- ST_Within vraci True jestlize geometrie A je kompletne uvnitr geometrie B; 
boolean ST_Within(geometry A, geometry B);


-- ST_Transform vraci geometrii transformovanou do zadane SRID (EPSG) projekce 
geometry ST_Transform(geometry g1, integer srid); 



### Reference: ###
http://postgis.net/docs/manual-2.1/

#----------------------------------

### SQL opakovani ###

-- Vyber z tabulky (SELECT)

SELECT 		nazevatributu
FROM    	nazevtabulky
WHERE 		nazevatributu = 'hodnota'

-- Agregacni funkce 
COUNT
SUM
MAX
MIN

-- Logicke operatory
AND
OR
NOT
IS NULL 
IS NOT NULL

-- Kvantifikace 
-- EXISTS operator testuje existenci zaznamu v pod-dotazu 
SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition); 

-- aliasy
-- atributove
SELECT column_name AS alias_name
FROM table_name;

-- tabulkove
SELECT column_name(s)
FROM table_name AS alias_name;


-- tvorba tabulky 

CREATE TABLE	mojeDB
   (atribut1 integer NOT NULL, 
   atribut2 character(20) NOT NULL, 
   CONSTRAINT pk_id PRIMARY KEY (atribut1)
   );

-- Vkladani dat do tabulky (INSERT)

INSERT INTO tbl_neco(atribut1, atribut2)
VALUES (1, ‘Praha’);

