# Import & export geodat 
SW utility: shp2pgsql, ogr2ogr, pg_dump, pg_restore

### CSV -> tabulka s geometrii

```
COPY table1(att1, att2, att3, x_coord, y_coord)
     FROM ’/home/user/geodata.csv'
     DELIMITER ','
     CSV HEADER;
     
 ST_MakePoint(x_coord, y_coord) .. konstruktor pro převod x, y do geom 
 ST_SetSRID(ST_MakePoint(x_coord, y_coord), 5514)  .. nastaveni SRS   
    
``` 

v PSQL  \copy 

```
\copy tabulka     FROM ’/home/user/geodata.csv'
         DELIMITER ','    CSV HEADER;
``` 

### SHP2PGSQL 

```
$ shp2pgsql -s 5514 sidla_body.shp public.sidla > sidla.sql 

$ psql -U user -d pdb –h server -a -f sidla.sql

``` 

### OGR 

```
ogrinfo -sql “SELECT COUNT(*) FROM sidla” sidla.gpkg

ogr2ogr -f PostgreSQL \
  PG:"dbname=LBGEO  host=server \ user=lbrodsky password=k116 " \
  sidla_body.shp \
  -a_srs EPSG:5514 
``` 

### DUMP 

```
$ pg_dump -h localhost -d dbname -F c -f  file.dump

$ pg_restore -h localhost -U username  -f file.dump
``` 

-F .. specifikuje formát DB 

-c .. PostgreSQL komprimovaný formát 



