# Práce s geometrickými prvky OGC SF 

### Geometrie z textu 
ST_GeomFromText(text) ... vytvori geometrii z textu dle WKT notace 

### WKT: 
'POINT(2 2)' ... definice bodu 


ST_GeomFromText('POINT(2 2)') ... WKB z textu (WKT)

### WKT klicova slova: 
POINT, LINESTRING, POLYGON, MULTIPOINT, MULTILINESTRING, MULTIPOLYGON, GEOMETRYCOLLECTION

### Deinice SRS 
ST_SRID(geom) ... overeni definice SRS 

ST_SetSRID(ST_GeomFromText('POINT(2 2)'),4326) ... nastaveni SRS pri tvorbe geometrie, vnorene prikazy

ST_GeomFromText('POINT(2 2)',SRID=4326) ... WKB z textu (WKT), vcetne definice SRS (zde EPSG kod) 

### Souradnice geometrie z WKB 

ST_AsText(geom) ... vstupem je WKB, vystupem WKT 

### Informace a metadata geometrie

ST_GeometryType(geom) 

ST_CoordDim(geom) 

ST_Dimension(geom) 

ST_IsCollection(geom)

ST_NumGeometries(geom) 

ST_NumInteriorRings(geom) 

ST_IsValid(geom)

ST_IsClosed(geom) 

ST_IsRing(geom) 

ST_X(geom), ST_Y(geom)

ST_StartPoint(geom)

ST_EndPoint(geom)

ST_PointN(geom, n)


