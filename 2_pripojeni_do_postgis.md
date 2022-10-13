# Pripojeni do PostgreSQL/PostGIS

### 1. Pristup pres **QGIS** 

1.1 QGIS menu / ikony

Add Layer -> Add PostGIS layer -> New (connection) 

Name: moje_databaze 

Host: 10.30.6.170 (nebo gislab.natur.cuni.cz)

Port: 5432

Database: pdb (nebo gismentors apod.)

User: k01 (jiny)

1.2 QGIS menu 

Database -> DB manager -> PostGIS -> PDB 
-> SQL dotaz 

### 2.Pristup pres **terminal** 

$ psql -h 10.30.6.170 -d pdb -U k01 

(heslo zadame po dotazu terminalu)
