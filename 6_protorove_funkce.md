# Prostorove SQL funkce

### 1. Geometrické konstruktory 

Funkce vytvářející geometrii (návratová hodnota) ze strukturovaných seznamů souřadnic. Převádí formáty.

```
geometry ST_MakePoint(float x, float y);
geometry ST_MakeLine(geometry[] geoms_array);
geometry ST_MakePolygon(geometry linestring);
     ... 
geometry ST_GeomFromText(WKT);
``` 

### 2. Funkce přístupu ke geometrii (accessors)

‘acesory’ objekty rodělují na jednotlivé entity a tím umožňují pracovat s dílčími částmi geometrií.

```
float ST_X(geometry a_point); 
float ST_Y(geometry a_point);
integer ST_NumGeometries(geometry geom);
```

### 3. Prostorové editory
Funkce pro modifikaci existující geometrie.

```
geometry ST_AddPoint(geometry linestring,                                               
geometry point, integer position);
geometry ST_RemovePoint(geometry linestring, integer offset);
geometry ST_Transform(geometry g1, integer srid);
```

### 4. Prostorové operátory  (BBox operátor)
Operátory pracující s minimálním ohraničujícím obdélníkem  geometrických objektů. 

 ```
-- bbox operátory
A && B ... A a B se překrývají?
A & < B  ... A překrývá nebo leží vlevo od B
A && B ...  překryv minimálních ohraničujících obdélník

-- distance operators 
A <#> B …  vzdálenost minimálních ohranicujících obdélníku
A <-> B …  vzdálenost centroidu
```

### 5. Exporty (Výstupy)

Funkce umožňující převod geometrie do jiné reprezentace.

```
ST_AsGML()  
ST_AsSVG() 
ST_AsGeoJSON()
```

### 6. Prostorové predikáty

Funkce pro určení vzájemné polohy dvou geometrií. Vrací booleaovskou hodnotu (prostorový JOIN). 

```
boolean ST_Intersects( geometry geomA , geometry geomB );
boolean ST_Contains(geometry geomA, geometry geomB); 
...
ST_Touches(), ST_Equals(), ST_Disjoint() … 
...
ST_Relate() … -> devítiprvková matice topologického modelu DE-9IM (Dimensionally Extended Nine-Intersection Model)
``` 

### 7. Rozměr geometrie
Funkce pro výpočet geometrických měr.

```
float ST_Area(geometry);
float ST_Length(geometry a_2dlinestring);
float ST_Distance(geometry A, geometry B);
``` 

### 8. Geometrické operace

Geometrické operace 

```
ST_Buffer()        … obalová zóna
ST_Union()         … sjednocení 
ST_Difference()    … rozdíl 
ST_SymDifference() … symetricky rozdíl 
ST_Intersection()  … průnik
ST_ExteriorRing()  … obvodová hranice
ST_Dump()          … rozdelí multipart geometrii
ST_Polygonize()    … zaplochování 
ST_ConvexHull()    … konvexní obal

``` 

### 9. Linearní referencovaní

Funkce pro dopočet hodnot mezi uloženými body geometrií. 

```
float8 ST_InterpolatePoint(geometry line, geometry point);

```

### 10. Ostatní nezařazení funkce 

Funkce managementu prostorové databáze

```
ST_IsValid(geom)
ST_SetSRID()
ST_SRID() 
``` 

### 11. SFCGAL funkce

Knihovna pro 3D analýzu

```
ST_Orientation()
ST_3DIntersection() 
ST_3DDifference()
ST_Volume()
``` 



