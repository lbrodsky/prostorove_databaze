# Práce s geometrickými prvky OGC SF 


ST_GeomFromText(text)

### WKT: 
'POINT(2 2)'

ST_GeomFromText('POINT(2 2)',SRID=4326)

ST_SetSRID(geom)
ST_SetSRID(ST_GeomFromText('POINT(2 2)'),4326)
ST_SRID(geom) 
ST_AsText(geom)
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


