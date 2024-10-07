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



