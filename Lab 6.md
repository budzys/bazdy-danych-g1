# Zadanie 1

1.
```sql
# jezeli wybrana baza to baza imienna
create table kreatura as select * from wikingowie.kreatura;
# jezeli wybrana baza to wikingowie
create table infs_buderm.kreatura select * from kreatura;

create table zasob as select * from wikingowie.zasob;
create table ekwipunek as select * from wikingowie.ekwipunek;
```

2.
```sql
select * from zasob;
```

3.
```sql
select * from zasob where rodzaj = 'jedzenie'
```

4.
```sql
select idZasobu, ilosc from zasob, kreatura where idKreatury in (1,3,5);
```

# Zadanie 2

1.
```sql
select * from kreatura where rodzaj !='wiedzma' and udzwig >= 50;
```

2.
```sql
select * from zasob where waga between 2 and 5;
```

3.
```sql
select * from kreatura where nazwa like '%or%' and udzwig between 30 and 70;
```

# Zadanie 3

1.
```sql
SELECT * FROM zasob WHERE MONTH(dataPozyskania) IN (7, 8);
```

2.
```sql
SELECT * FROM zasob WHERE rodzaj IS NOT NULL ORDER BY waga ASC;
```

3.
```sql
SELECT * FROM kreatura ORDER BY dataUr DESC LIMIT 5;
```

# Zadanie 4

1.
```sql 
select distinct rodzaj from zasob;
#lub
select distinct (rodzaj) from zasob;
```

2.
```sql
select concat(nazwa, ' to id=', idKreatury) from kreatura where rodzaj like 'wi%;
```

3.
```sql
SELECT nazwa, (ilosc*waga) as calkowitaWaga
from zasob where year (dataPozyskania) between 2000 and 2007;
```

# Zadanie 5

1.
```sql
SELECT nazwa, waga * 0.7 AS masa_netto, waga * 0.3 AS masa_odpadkow
FROM zasob
WHERE rodzaj = 'jedzenie';
```

2.
```sql
select * from zasob where rodzaj is null;
```

3. 
```sql
SELECT DISTINCT rodzaj FROM zasob WHERE (nazwa LIKE 'Ba%' OR nazwa LIKE '%os') AND rodzaj IS NOT NULL
ORDER BY rodzaj;
```
