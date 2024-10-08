# Úvod do SQL
Příklady z tohoto úvodu do SQL lze aplikovat na databázi `naturalearth`, implementovanou na PostgreSQL/PostGIS serveru, který sídlí na doméně `osgeo.natur.cuni.cz`. Před spuštěním SQL dotazu vždy zkontrolujte název databáze, název tabulky a název atributu. 

## Příkaz SELECT
Čtení dat z DB

-- Nejsnazší forma SELECTu je: <br> SELECT "co" FROM "odkud"

Příklad z DB Naturalearth: <br>

**SELECT name_long** <br>
**FROM countries;** <br>


Úkol:
Přidejte atributy postal a pop2020 do výpisu. <br> Název sloupce name_long přepište na Zeme pomocí aliasu AS.

## COUNT
Spočítejte, kolik je zemí v DB Naturalearth. <br> 
SELECT COUNT(*) FROM "odkud"

## Podminka WHERE
SELECT "co" FROM "odkud" WHERE "podminka" <br>

Priklad: <br/> 
**SELECT name_long** <br>
**FROM countries** <br>
**WHERE region_un = 'Europe';** <br>


Pro test na nerovnost se používá zápis <> nebo také někdy != <br>

Úkol:

Vyberte všechny neevropské země a vypište je.

Často potřebujeme testovat, zda nějaká hodnota přesahuje nebo nepřesahuje jinou. <br> 
SELECT "co" FROM "odkud" WHERE atribut <= 10000; <br/>

Test na text nemusí být vždy přesný, může záměrně obsahovat určitou volnost. <br> 
Pro volnější test textu se použije příkaz LIKE, a v hledaném vzoru se používají zástupné znaky %, _ a [].

SELECT "co" FROM "odkud" WHERE atribut LIKE 'Čern%'; <br> 
'Čern_' <br> 
'Čern[ýá]' <br>

## Negace NOT
Vyberte vše kromě ..., s operátorem negace. <br> 
SELECT "co" FROM "odkud" WHERE NOT "podmínka" <br>

Příklad: Všichni kromě "..." <br>

**SELECT name_long** <br>
**FROM countries** <br>
**WHERE region_un NOT LIKE 'Eu%';** <br>

## A současně AND
Pro výběr uplatňujeme více kritérií současně. <br> 
SELECT "co" FROM "odkud" WHERE "podmínka1" AND "podmínka2" <br>

Příklad: <br> 
**SELECT name_long** <br>
**FROM countries** <br>
**WHERE region_un = 'Europe' AND** <br>
**name_long LIKE 'C%';** <br>

## Alespoň jedno OR
Splnění alespoň jednoho z kritérií. <br> 
SELECT "co" FROM "odkud" WHERE "podmínka1" OR "podmínka2" <br>

**SELECT name_long** <br>
**FROM countries** <br>
**WHERE name_long LIKE 'A%' OR** <br>
**name_long LIKE 'C%';** <br>

## Operátor IN ~ patří do výčtu
SELECT "co" FROM "odkud" WHERE atribut IN (1, 2); <br>

**SELECT name_long** <br>
**FROM countries** <br>
**WHERE name_len IN (20, 24);** <br>

## Test rozmezí BETWEEN
Často potřebujeme testovat, zda nějaká hodnota patří do zadaného rozmezí od-do. <br> 
SELECT "co" FROM "odkud" WHERE atribut BETWEEN 1 AND 2; <br>

**SELECT name_long** <br>
**FROM countries** <br>
**WHERE label_y BETWEEN 40 and 60;** <br>

Přepište test rozmezí pomocí <>. <br> 

## Kombinace AND a OR 
SELECT "co" FROM "odkud" WHERE atribut = hodnota AND <br>
                               atribut2 = 1 OR atribut3 > 13; 

Příklad: <br>
**SELECT name_long** <br>
**FROM countries** <br>
**WHERE region_un = 'Europe' AND** <br>
**label_y BETWEEN 40 and 60;** <br>

## Priorita operátorů

Operátory mají různou prioritu při vyhodnocování. Například porovnání = je silnější než NOT, které je silnější než AND, jež je zase silnější než OR. <br> 
Ověřte na webu "operator precedence t-sql". <br>

## Řazení ORDER BY
Výsledek SQL dotazu chceme uspořádat podle nějakého kritéria, například abecedy. <br>

Příklad: Vypište všechny země pomocí řadícího kritéria ORDER BY: <br>

**SELECT name_long** <br>
**FROM countries** <br>
**ORDER BY name_long;** <br>

## Dvě řadící kritéria
**SELECT name_long, continent** <br>
**FROM countries** <br>
**ORDER BY** <br>
  **region_un, -- primarni radici kriterium** <br>
  **name_long; -- sekundarni radici kritereium** <br>

## Výpis od nejmenšího
Jako hlavní řadící kritérium využijeme HDP hodnotu. <br>

**SELECT name_long, continent, HDP** <br>
**FROM countries** <br>
**ORDER BY** <br>
  **label_y DESC, -- primarni radici kriterium** <br>
  **continent,** <br>
  **name_long;** <br>

## Řazení a výběr v jednom
**SELECT name_long, continent, HDP** <br>
**FROM countries** <br>
**WHERE region_un = 'Europe'** <br>
**ORDER BY** <br>
  **label_y DESC, -- primarni radici kriterium** <br>
  **region_un,** <br>
  **name_long;** <br>

## Přímý výpočet
**SELECT 1 + 1 AS "1+1"; <br>** <br>

## CASE na hodnoty 
Někdy chceme výstup upravovat pro každou hodnotu zvlášť. <br> 
Vytvoř příklad nad daty NaturalEarth. 

**SEELCT name_long, ...** <br>
  **CASE att** <br>
    **WHEN 1 THEN 'Prvni'** <br>
    **WHEN 2 THEN 'Druhy'** <br>
    **WHEN 3 THEN 'Treti'** <br>
    **ELSE 'Neznamy'** <br>
  **END AS Atribut** <br>
**FROM countries;** <br>

## CASE na podminky 
Někdy chceme výstup upravovat pro každou podmínku zvlášť. <br>

**SEELCT name_long** <br>
  **CASE** <br>
    **WHEN GDP < 1000 THEN 'Posledni'** <br>
    **WHEN GDP > 5000 THEN 'Treti'** <br>
    **ELSE 'Prostredni'** <br>
  **END AS GDP** <br>
**FROM countries;** <br>

## Hodnota NULL 
Vypište všechny záznamy, u kterých chybí hodnota atributu ... <br> 
SELECT atribut FROM db WHERE atribut = NULL; <br>

Nebo 
SELECT atribut FROM db WHERE atribut <> NULL;  <br>

## Správný test na NULL
SELECT atribut FROM db WHERE atribut **IS NULL**;  !!! <br>

Nebo <br>

SELECT atribut FROM db WHERE atribut IS NOT NULL;  !!! <br>

## Funkce ISNULL 
Funkce ISNULL přebírá dva parametry. Jejím výsledkem je hodnota prvního parametru, pokud tento není NULL. 
V opačném případě je výsledkem funkce hodnota druhého parametru. <br>

**SELECT** <br>
  **ISNULL(att, 'Nahradni hodnota'),** <br>
  **ISNULL(NULL, 'Nahradni hodnota');** <br>

## Vypis unikátních hodnot z určitého sloupce v tabulce: DISTINCT 
**SELECT DISTINCT region_un** <br/> 
**FROM countries;** <br/>

## Seskupování GROUP BY
Agregační funkce umožňují spočítat počty, součty a podobně. <br> 
Nejprve je potřeba určit, který atribut použijeme k seskupování. Pak tento atribut uvedeme za SELECTem a za klíčovým slovem GROUP BY.

SELECT atribut FROM tabulka GROUP BY atribut; 

**SELECT region_un** <br/> 
**FROM countries** <br/>
**GROUP BY region_un;** <br/> 

Zaroven nekdy potrebujem vedet kolik zaznamu se seskupilo pro danou unikatni hodnotu atrinutu. 

**SELECT region_un, COUNT(*) AS pocet** <br/> 
**FROM countries** <br/>
**GROUP BY region_un;** <br/> 

Pripadne vypis jeste seradime podle atributu pocet. 

**SELECT region_un, COUNT(*) AS pocet** <br/> 
**FROM countries** <br/>
**GROUP BY region_un** <br/> 
**ORDER BY pocet;** <br/> 

Klicove slovo **COUNT** je mozne nahradit jinou agregacni funkci, napriklad SUM, apod. 

## Klauzule HAVING 
HAVING klauzule je speciálním druhem SQL příkazu, který se chová podobně jako jako WHERE. 
To znamená, že pomocí ní definujeme omezující podmínku při vyhledávání nebo manipulaci s tabulkami.

SELECT atribut
FROM tabulka
WHERE podminka1 
GROUP BY atribut
HAVING podminka2
ORDER BY atribut;

Priklad: 
**SELECT COUNT(CustomerID), Country** <br/>
**FROM Customers** <br/> 
**GROUP BY Country** <br/> 
**HAVING COUNT(CustomerID) > 5;** <br/> 

Pozdeji: vnorene dotazy, JOIN, tvorba tabulek 
