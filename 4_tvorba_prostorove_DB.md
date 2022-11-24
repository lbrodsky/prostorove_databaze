# Vytvoření prostorove databáze

### Nova DB:
-- Postgres utilita 
$ createdb moje_prostorova_databaze 

psql -d moje_prostorova_databaze
mpd-# \dt ... zatim zadne tabulky a prostorova data neumi 

### Extenze PostGIS
```
CREATE EXTENSION postgis; 
```
-- nyni uz DB umi prostorova data 

### Prostorova tabulka 
```
CREATE TABLE prostorova_tabulka (
    ids integer NOT NULL,
    nazev character, 
    geom geometry
);
```

pripadne aktualizace: 

```
ALTER TABLE table_name
ADD column_name datatype;

ALTER TABLE table_name 
RENAME COLUMN column_name TO     new_column_name;
``` 

vkladani dat: 

```
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
``` 

aktualizace zaznamu:
```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE predicate;
```

mazani tabulek, db: 

```
DROP TABLE table_name;

DROP DATABASE dbname; 
``` 


