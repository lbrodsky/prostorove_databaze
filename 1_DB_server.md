# Databazovy server 
* [PostgreSQL](https://www.postgresql.org/) / [PostGIS](https://postgis.net/) 
* [SQLite](https://www.sqlite.org/index.html) / [SpatiaLite](https://www.gaia-gis.it/fossil/libspatialite/index)

Systemy s DB serverem: 
1. Varianta: GIS.lab system
2. Varianta: predinstalovany server v OSGeo live
3. Varianta: localhost (vlastni notebook nebo desktop)


## 1. GIS.lab
[GIS.lab system](https://gislab.readthedocs.io/en/latest/client-layout/index.html)

Do GIS.lab klienta se pripojime bootem pres sitvou kartu pri startu PC. 
Je nutne vyvolat vstup do BIOSu (F2 / DEL) a pote Ctrl+Alt+Del 

[Desktop klienta](https://gislab.readthedocs.io/en/latest/_images/client-layout-qgis.png) 

- Desktop aplikace: QGIS
- Geodatabaze: PostgreSQL/PostGIS server a PgAdmin III, SpatiaLite
- Text editor: Leafpad
- Linux terminal: $  

[Vice o instalci zde](https://gislab.readthedocs.io/en/latest/client-layout/index.html)


## 2. OSGeo live
K vyuziti OSGeo live je treba instalovat: 
* VirtualBox (Oracle VM VirtualBox) https://www.virtualbox.org 
* OSGeo live, v.9/10 (linux) a vyssi https://live.osgeo.org/en/download.html

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

