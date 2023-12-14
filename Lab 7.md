# Zadanie 1

1.
```sql
select avg(waga) from kreatura where rodzaj = 'wiking';
```

2.
```sql
select rodzaj,
avg(waga),
count(*) 
from kreatura group by rodzaj; 
```

3.
```sql
select rodzaj,
avg(2023 - year(dataUr)) as sredniWiek
from kreatura group by rodzaj;
```


# Zadanie 2

1.
```sql
select rodzaj,
sum(waga*ilosc) 
from zasob group by rodzaj;
```

2.
```sql
select avg(waga) from zasob
where ilosc >= 4
group by rodzaj having sum(waga) > 10;
```

3.
```sql
select count(distinct nazwa) from zasob group by rodzaj;
```

Zadanie 3

1.
```sql
select nazwa, idZasobu, ilosc from kreatura, ekwipunek where kreatura.idKreatury=ekwipunek.idKreatury;
#lub
select k.nazwa, e.idZasobu, e.ilosc from kreatura k
inner join ekwipunek e on k.idKreatury=e.idKreatury;
```

2.
```sql
select k.nazwa, e.idZasobu, e.ilosc, z.nazwa from kreatura k
inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu;
```

3.
```sql
# left join + warunek z bull
select k.nazwa, e.idZasobu, e.ilosc from kreatura k
left join ekwipunek e on k.idKreatury=e.idKreatury
where e.idZasobu is null;
# podzapytanie
select nazwa, idKreatury from kreatura
where idKreatury not in 
(select distinct idKreatury from ekwipunek
where idKreatury is not null);
```


# Zadanie 4

1.
```sql
# select * from kreatura natural join ekwipunek; - nie najlepsze opcja
select k.nazwa z.nazwa from kreatura k
join ekwipunek e on k.idKreatury=e.idKreatury
join zasob z on e.idZasobu=z.idZasobu
where year(dataUr) between 1600 and 1699;
```

2.
```sql
select k.nazwa, k.dataUr z.rodzaj from kreatura k
inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu
where z.rodzaj = 'jedzenie'
order by k.dataUr desc limit 5;
```

3.
```sql
select concat(k1.nazwa, ' - ', k2.nazwa)
FROM kreatura k1
inner join kreatura k2 on k1.idKreatury - k2.idKreatury = 5;
```


# Zadanie 5

1.
```sql
select k.rodzaj, avg (e.ilosc * z.waga)
from kreatura k
inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu
where k.rodzaj not in ('malpa', 'waz') and 
e.ilosc < 30 group by k.rodzaj;
```

2.
```sql
select n.najstarsza, n.najmlodsza from
(select rodzaj, min(dataUr) najstarsza, 
max(dataUr) najmlodsza from kreatura
group by rodzaj) n,  kreatura k 
where n.najstarsza=k.dataUr 
or n.najmlodsza=k.dataUr;
# jest jeszcze druga opcja (przy uzyciu union), ktora bedzie wrzucona na repozytorium 
```
