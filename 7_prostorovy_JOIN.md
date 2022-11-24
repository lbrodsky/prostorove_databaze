# Prostorovy JOIN

### DE-9IM 
DE-9IM (Dimensionally Extended Nine-Intersection Model), který kombinuje možnosti průniků 
- vnitřků (Interior), 
- hranice (Boundary)
- a vnějšku (Exterior) 

dvou geometrických objektů. 

0 => bod
1 => linie
2 => plocha

T => {0,1,2}
F => prázdná množina

```
SELECT ST_Relate(
         'LINESTRING(0 0, 2 0)',
         'POLYGON((1 -1, 1 1, 3 1, 3 -1, 1 -1))'
       );


```

1   0   1
0   F   0
2   1   2


### Prstorove predikaty

výsledkem je hodnota Boolean (True / False)

```
T / F ST_Equals(A, B)     ... totožné
T / F ST_Disjoint(A , B)  ...   žádný totožný bod
 = NOT ST_Intersects(A, B) 
T/F ST_Intersects(A, B)   ...  alespoň jeden společný      
T/F  ST_Crosses(A, B)     ... společné vnitřní body
T/F  ST_Overlaps(A, B)    ... ne všechny, porovnává     geometrie stejné dimenze!
T/F ST_Touches(A, B)      ...  alespoň jeden společný  
T/F ST_Contains(A, B)     ...  ~ T/F ST_Within(B,A)
T/F ST_DWithin(A, B)      ...  ve vzdálenosti do B 
``` 

### Prostorovy JOIN 

```
SELECT [sloupce_leva_tab], [sloupce_prava_tab]
FROM   leva_tab AS l
JOIN   prava_tab AS p
ON 
-- pravidlo propojeni tabulek
ST_Intersets(l.geom, p.geom); 
[WHERE podmínka] 
[ORDER BY sloupce];
``` 

```
SELECT    t1.nazev, Sum(tb2.pocet) AS sumar
FROM      tabulka1 AS t1
JOIN      tabulka2 AS t2 
ON ST_Contains(t1.geom, t2.geom)
WHERE     t2.att = 'neco'
GROUP BY  t1.nazev
ORDER BY  sumar DESC;
``` 

### Prostorovy multi-JOIN 

```
SELECT výraz 
FROM t1 
JOIN t2 ON predikát1 
JOIN t3 ON predikát2 
JOIN t4 ON predikát3 
``` 

