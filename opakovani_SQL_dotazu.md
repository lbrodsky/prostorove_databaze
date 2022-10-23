# Opakovani SQL dotazu do PostgreSQL databaze

1. Napiste dotaz pro zobrazeni jmena zeme (name_long), zkratky (postal) a populatce 2020 (pop2020) 
z databaze NaturalEarth2 tabulky ne_10m_admin_0_countries (DB soucasti OSGeo nebo z https://www.naturalearthdata.com/). Kolik je v tabulce zaznamu? 


2. Napiste dotaz pro vypis unikatnich hodnot pro atribut continent z tabulky ne_10m_admin_0_countries. 


3. Napiste dotaz pro vypis 10 nejlidnatejsich zemi. Vyuzij atributy name_full a pop_est.


4. Napiste dotaz pro vypocet "per capita GDP". Vzuyij  atributy name_full, gdp_md_est a pop_est. Vysledny sloupec vypoctu aliasuje jako per_capita_GDP. 


5. Napiste dotaz pro ziskani ID zeme (gid), jeji cely nazev a "per capita GDP" indikator serazeny vzestupne.


6. Napiste dotaz pro ziskani celkoveho poctu obyvatel v Evrope. 


7. Napiste dotaz pro vypis Zeme s nejmensim a nejvetsim poctem obyvatel. 


8. Napiste dotaz pro vypocet prumernaho GDP v Evrope. 


9. Napiste dotay pro vypis poctu obzvatel v jednotlivch kontinentech. 


10. Napiste dotaz, kterym ziskate jedinecny pocet roylisenych ekonomik (atribut economy) zemi sveta v tabulce ne_10m_admin_0_countries. 


12. Napiste dotaz, ktery ziska prvni dva znaky atributu iso_a3, a cely atribut iso_a2. 


13. Napiste dotaz pro vypocet vyrazu  171 * 214 + 625.


14. Napiste dotaz, kterym ziskate  jmeno zeme (name_long) a zkratku (postal) spojenou podtrzitkem v jedinaem sloupci 


15. Napiste dotaz, kterym ziskate jmena zemi po odstraneni vsech pocatecnich a koncovych mezer z tabulky ne_10m_admin_0_countries. 


16. Napiste dotaz, kterym ziskate jmeno zeme, zkratku zeme (postal) a delku jmena a zkratky (pocet znaku). 


17. Napiste dotaz, ktery zkontroluje zda sloupec jmeno zeme (name_long) a typ administrativni jednotky (featurecla) obsahuje nejake cislo.

```
-- pouzijte 
SIMILAR TO   '%0|1|2|3|4|5|6|7|8|9%'
``` 

18. Napiste dotaz pro vyber prvnich deseti zaznamu z tabulky ne_10m_admin_0_countries. 


19. Napiste dotaz pro vypocet zmeny populace mezi roky 1950 a 2020. 


20. Napiste dotaz pro vypocet procentickeho narustu populace mezi roky 1950 a 2020 vzhedem k roku 1950. 
