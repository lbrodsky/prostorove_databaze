# Uvod do SQL 

## Prikaz SELECT
Cteni dat z DB 

--Nejednodussi forma SELECTu je <br>
SELECT "co" FROM "odkud"

Priklad z DB Naturalearth: <br>
`
SELECT name_long 

FROM countries;
`

Ukol: Pridejte atributy postal a pop2020 do vypisu <br>
Jmeno sloupce 'name_long' prepiste na 'Zeme' pomoci aliasu `AS`

## COUNT
Spocitejte kolik je zemi v DB Naturalearth 
SELECT COUNT(*) FROM "odkud"

## Podminka WHERE
SELECT "co" FROM "odkud" WHERE "podminka"

Priklad: 
`
SELECT name_long 
FROM countries 
WHERE continent = 'Europe'; 
`

Pro test na nerovnost se pouziva zapis < > nebo take nekdy != 

Ukol: vyberte vsechnz ne-Evropske zeme a vzpiste je. 

Casto potrebujeme testovat jestli nejaka hodnota presahuje ci nepresahuje nejakou jinou. 
SELECT "co" FROM "odkud" WHERE atribut <= 10000; 

Test na text nemusi byt vzdy presny, muze zamerne obsahovat urcitou volnost. 
Pro volnejsi test textu se pouzije prikaz `LIKE`a v hledanem vzoru se pouzivaji zastupne znaky %, _ a [] 
SELECT "co" FROM "odkud" WHERE atribut LIKE 'Cern%';
'Cern_'
Cern[ýá] 

## Negace NOT
Vyber vsech krome ..., s operatorem negace. 
SELECT "co" FROM "odkud" WHERE NOT "podminka" 

Priklad vsichni krome "..."
`
SELECT name_long 
FROM countries 
WHERE NOT LIKE 'Eu%'; 
`

## A soucasne AND
Pro vyber uplatnujem vice kriterii soucasne 
SELECT "co" FROM "odkud" WHERE "podminka1 " AND "podminak2"

Priklda: 
`
SELECT name_long 
FROM countries 
WHERE continent = 'Europe' AND 
country LIKE 'C%';  
`

## Alespon jedno OR 
Splneni alespon jednoho z kriterii 
SELECT "co" FROM "odkud" WHERE "podminka1 " or "podminak2"

`
SELECT name_long 
FROM countries 
WHERE country LIKE 'A%' OR 
country LIKE 'C%';  
`

## Operator IN ~ patri do vyctu 
SELECT "co" FROM "odkud" WHERE atribut IN (1, 2); 

`
SELECT name_long 
FROM countries 
WHERE att IN (1, 2);  
`

## Test rozmezi BETWEEN 
Casto potrebujem testovat, zda nejaka hodnota patri do zadaneho rozmezi od do
SELECT "co" FROM "odkud" WHERE atribut BETWEEN 1 AND 2; 

`
SELECT name_long 
FROM countries 
WHERE GDP BETWEEN 1000 and 2000;  
`

Prepiste test rozmnezi pomoci < >

## Kombinace AND a OR 
SELECT "co" FROM "odkud" WHERE atribut = hodnota AND 
                               atribut2 = 1 OR atribut3 > 13; 

Priklad: 
`
SELECT name_long 
FROM countries 
WHERE att = 'Europe' AND 
att2 LIKE 'A%' or att3 > 1000; 
`

## Priorita operatoru 
Operatory maji ruznou prioritu pri vyhodnocovani. Napr. porovnani = je silnejsi nez NOT, ktere je sitlnejsi nez AND, jez je zase silnejsi nez OR. 
Over na webu "operator precedence t-sql". 

## Razeni ORDER BY 
Vysledek SQL dotazu chceme usporadat podle nejakeho kriteria, napriklad abecedy. 

Priklad: vypiste vsechny zeme pomoci radiciho kriteria ORDER BY: 

`
SELECT name_long 
FROM countries
ORDER BY name_long; 
`

## Dve radici kriteria 
`
SELECT name_long, continent 
FROM countries
ORDER BY 
  continent, -- primarni radici kriterium
  name_long; -- sekundarni radici kritereium  
`

## Vypis od nejmensiho 
Jako hlavni radixi kriterium vyuzijem HDP hodnotu 
`
SELECT name_long, continent, HDP
FROM countries
ORDER BY 
  HDP DESC, -- primarni radici kriterium
  continent, 
  name_long;  
`

## Razeni a vyber v jednom 
`
SELECT name_long, continent, HDP
FROM countries
WHERE continent = 'Europe'
ORDER BY 
  HDP DESC, -- primarni radici kriterium
  continent, 
  name_long;  
`
## Zmena vystupu 

## Spojeni sloupcu 
SELECT prijmeni + N' ' + jmeno AS Cele jmeno FROM "odkud"

## Primy vypocet 
SELECT 1 + 1 AS [1+1], 
       N'1' + N'1' AS [N'1'+ N'1'] 
       1 + 2 * 3 AS [1 + 2 * 3]; 

## CASE na hodnoty 
Nekdy chceme vystup upravovat pro kazdou hodnotu zvlast. 
`
SEELCT name_long, ... 
  CASE att 
    WHEN 1 THEN 'Prvni'
    WHEN 2 THEN 'Druhy'
    WHEN 3 THEN 'Treti'
    ELSE 'Neznamy'
  END AS Atribut 
FROM countries; 
`

## CASE na podminky 
Nekdy chceme vystup upravovat pro kazdou hodnotu zvlast. 
`
SEELCT name_long, ... 
  CASE 
    WHEN HDP < 1000 THEN 'Pposledni'
    WHEN HDP > 5000 THEN 'Treti'
    ELSE 'Prostredni'
  END AS hdp 
FROM countries; 
`

## Hodnota NULL 
Vypiste vsechny zaznamy uk terych chybi hodnata atributu ... 
SELECT atribut FROM db WHERE atribut = NULL; 

Nebo 
SELECT atribut FROM db WHERE atribut <> NULL; 

## Spravy test na NULL 
SELECT atribut FROM db WHERE atribut IS NULL;  !!! 

Nebo 

SELECT atribut FROM db WHERE atribut IS NOT NULL;  !!! 

## Funkce ISNULL 
Funkce ISNULL prebira dva parametry. Jejim vysledkem je hodnota prvniho parametru, pokud tento neni NULL. V opacnem pripade je vysledkem funkce hodnota druheho parametru. 
SELECT 
  ISNULL(N'Test', N'Nahradni hodnota'), 
  ISNULL(NULL, N'Nahradni hodnota'); 



