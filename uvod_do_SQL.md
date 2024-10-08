# Uvod do SQL 

## Prikaz SELECT
Cteni dat z DB 

--Nejednodussi forma SELECTu je <br>
SELECT "co" FROM "odkud"

Priklad z DB Naturalearth: <br>

**SELECT name_long** <br>
**FROM countries;** <br>


Ukol: Pridejte atributy postal a pop2020 do vypisu <br>
Jmeno sloupce 'name_long' prepiste na 'Zeme' pomoci aliasu `AS`

## COUNT
Spocitejte kolik je zemi v DB Naturalearth <br>
SELECT COUNT(*) FROM "odkud" <br>

## Podminka WHERE
SELECT "co" FROM "odkud" WHERE "podminka" <br>

Priklad: <br/> 
**SELECT name_long** <br>
**FROM countries** <br>
**WHERE region_un = 'Europe';** <br>


Pro test na nerovnost se pouziva zapis < > nebo take nekdy != <br>

Ukol: vyberte vsechnz ne-Evropske zeme a vzpiste je. <br>

Casto potrebujeme testovat jestli nejaka hodnota presahuje ci nepresahuje nejakou jinou. <br>
SELECT "co" FROM "odkud" WHERE atribut <= 10000; <br/> 

Test na text nemusi byt vzdy presny, muze zamerne obsahovat urcitou volnost. <br>
Pro volnejsi test textu se pouzije prikaz `LIKE`a v hledanem vzoru se pouzivaji zastupne znaky %, _ a [] <br>

SELECT "co" FROM "odkud" WHERE atribut LIKE 'Čern%'; <br>
'Čern_' <br>
'Čern[ýá]' <br>

## Negace NOT
Vyber vsech krome ..., s operatorem negace. <br>
SELECT "co" FROM "odkud" WHERE NOT "podminka" <br>

Priklad vsichni krome "..." <br>

**SELECT name_long** <br>
**FROM countries** <br>
**WHERE region_un NOT LIKE 'Eu%';** <br>

## A soucasne AND
Pro vyber uplatnujem vice kriterii soucasne <br>
SELECT "co" FROM "odkud" WHERE "podminka1 " AND "podminak2" <br>

Priklad: <br> 
**SELECT name_long** <br>
**FROM countries** <br>
**WHERE region_un = 'Europe' AND** <br>
**name_long LIKE 'C%';** <br>

## Alespon jedno OR 
Splneni alespon jednoho z kriterii <br>
SELECT "co" FROM "odkud" WHERE "podminka1 " or "podminak2" <br>

**SELECT name_long** <br>
**FROM countries** <br>
**WHERE name_long LIKE 'A%' OR** <br>
**name_long LIKE 'C%';** <br>

## Operator IN ~ patri do vyctu 
SELECT "co" FROM "odkud" WHERE atribut IN (1, 2); <br>

**SELECT name_long** <br>
**FROM countries** <br>
**WHERE name_len IN (20, 24);** <br>

## Test rozmezi BETWEEN 
Casto potrebujem testovat, zda nejaka hodnota patri do zadaneho rozmezi od do <br>
SELECT "co" FROM "odkud" WHERE atribut BETWEEN 1 AND 2; <br>

**SELECT name_long** <br>
**FROM countries** <br>
**WHERE label_y BETWEEN 40 and 60;** <br>

Prepiste test rozmnezi pomoci < > <br>

## Kombinace AND a OR 
SELECT "co" FROM "odkud" WHERE atribut = hodnota AND <br>
                               atribut2 = 1 OR atribut3 > 13; 

Priklad: <br>
**SELECT name_long** <br>
**FROM countries** <br>
**WHERE region_un = 'Europe' AND** <br>
**label_y BETWEEN 40 and 60;** <br>

## Priorita operatoru 
Operatory maji ruznou prioritu pri vyhodnocovani. Napr. porovnani = je silnejsi nez NOT, ktere je sitlnejsi nez AND, jez je zase silnejsi nez OR. <br>
Over na webu "operator precedence t-sql". <br>

## Razeni ORDER BY 
Vysledek SQL dotazu chceme usporadat podle nejakeho kriteria, napriklad abecedy. <br>

Priklad: vypiste vsechny zeme pomoci radiciho kriteria ORDER BY: <br>

**SELECT name_long** <br>
**FROM countries** <br>
**ORDER BY name_long;** <br>

## Dve radici kriteria 
**SELECT name_long, continent** <br>
**FROM countries** <br>
**ORDER BY** <br>
  **region_un, -- primarni radici kriterium** <br>
  **name_long; -- sekundarni radici kritereium** <br>

## Vypis od nejmensiho 
Jako hlavni radixi kriterium vyuzijem HDP hodnotu <br>

**SELECT name_long, continent, HDP** <br>
**FROM countries** <br>
**ORDER BY** <br>
  **label_y DESC, -- primarni radici kriterium** <br>
  **continent,** <br>
  **name_long;** <br>

## Razeni a vyber v jednom 
**SELECT name_long, continent, HDP** <br>
**FROM countries** <br>
**WHERE region_un = 'Europe'** <br>
**ORDER BY** <br>
  **label_y DESC, -- primarni radici kriterium** <br>
  **region_un,** <br>
  **name_long;** <br>

## Zmena vystupu 

## Spojeni sloupcu 
SELECT prijmeni + N' ' + jmeno AS Cele jmeno FROM "odkud" <br>

## Primy vypocet 
**SELECT 1 + 1 AS "1+1"; <br>** <br>

## CASE na hodnoty 
Nekdy chceme vystup upravovat pro kazdou hodnotu zvlast. <br>

**SEELCT name_long, ...** <br>
  **CASE att** <br>
    **WHEN 1 THEN 'Prvni'** <br>
    **WHEN 2 THEN 'Druhy'** <br>
    **WHEN 3 THEN 'Treti'** <br>
    **ELSE 'Neznamy'** <br>
  **END AS Atribut** <br>
**FROM countries;** <br>

## CASE na podminky 
Nekdy chceme vystup upravovat pro kazdou hodnotu zvlast. <br>

**SEELCT name_long, ...** <br>
  **CASE** <br>
    **WHEN HDP < 1000 THEN 'Pposledni'** <br>
    **WHEN HDP > 5000 THEN 'Treti'** <br>
    **ELSE 'Prostredni'** <br>
  **END AS hdp** <br>
**FROM countries;** <br>

## Hodnota NULL 
Vypiste vsechny zaznamy uk terych chybi hodnata atributu ... <br>
SELECT atribut FROM db WHERE atribut = NULL; <br>

Nebo 
SELECT atribut FROM db WHERE atribut <> NULL;  <br>

## Spravy test na NULL 
SELECT atribut FROM db WHERE atribut IS NULL;  !!! <br>

Nebo <br>

SELECT atribut FROM db WHERE atribut IS NOT NULL;  !!! <br>

## Funkce ISNULL 
Funkce ISNULL prebira dva parametry. Jejim vysledkem je hodnota prvniho parametru, pokud tento neni NULL. V opacnem pripade je vysledkem funkce hodnota druheho parametru. <br>
**SELECT** <br>
  **ISNULL(N'Test', N'Nahradni hodnota'),** <br>
  **ISNULL(NULL, N'Nahradni hodnota');** <br>



