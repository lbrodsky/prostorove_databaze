# Uvod do SQL 

## Prikaz SELECT
Cteni dat z DB 

--Nejednodussi forma SELECTu
SELECT "co" FROM "odkud"

Priklad z DB Naturalearth: 
`
SELECT name_long 
FROM countries;
`

Ukol: Pridejte atributy postal a pop2020 do vypisu
Jmeno sloupce 'name_long' prepiste na 'Zeme' pomoci aliasu `AS`

## COUNT
Spocitejte kolik je zemi v DB Naturalearth 
SELECT COUNT(*) FROM "odkud"

## Podminka WHERE
SELECT "co" FROM "odkud" WHERE "podminka"

Priklad: 
`
SELECT name_long 
FROM countries;
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
FROM countries;
WHERE NOT LIKE 'Eu%'; 
`

## A soucasne AND
Pro vyber uplatnujem vice kriterii soucasne 
SELECT "co" FROM "odkud" WHERE "podminka1 " AND "podminak2"

Priklda: 
`
SELECT name_long 
FROM countries;
WHERE continent = 'Europe' AND 
country LIKE 'C%';  
`

## Alespon jedno OR 
Splneni alespon jednoho z kriterii 
SELECT "co" FROM "odkud" WHERE "podminka1 " or "podminak2"

`
SELECT name_long 
FROM countries;
WHERE country LIKE 'A%' OR 
country LIKE 'C%';  
`

## Operator IN ~ patri do vyctu 
SELECT "co" FROM "odkud" WHERE atribut IN (1, 2); 

`
SELECT name_long 
FROM countries;
WHERE att IN (1, 2);  
`

## Test rozmezi BETWEEN 
Casto potrebujem testovat, zda nejaka hodnota patri do zadaneho rozmezi od do
SELECT "co" FROM "odkud" WHERE atribut BETWEEN 1 AND 2; 

`
SELECT name_long 
FROM countries;
WHERE GDP BETWEEN 1000 and 2000;  
`



