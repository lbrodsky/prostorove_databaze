# Tvorba nove databaze v PostgreSQL / PostGIS 

### 1. Windows 

Spust SQL shell a vytvor novou DB: 

```
Server [localhost]: Enter
Database [postgres]: Enter
Port [5432]: Enter
Username [postgres]: Enter 
Password for user postgres: ***** 
```

<img width="425" alt="image" src="https://user-images.githubusercontent.com/11438547/197376106-5b4d9831-f1f5-4bc4-8f10-620a11259a8d.png">


```
postgres# CREATE DATABASE mojedb; 
```


### 2. Linux terminal 

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
