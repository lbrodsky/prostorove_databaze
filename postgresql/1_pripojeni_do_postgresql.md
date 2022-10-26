# Pripojeni do PostgreSQL

### PSQL 

$ psql -h 10.30.6.170 -d pdb -U k01 

(heslo zadame po dotazu terminalu)

Nebo pod standardnim uzivatelem 'postgres'

$sudo -u postgres psql 
$psql mydb
 
SELECT version();

SELECT postgis_full_version;

\conninfo;

### PgAdmin 

Otevrete PgAdmin III nebo PgAdmin IV v prohlizeci 
