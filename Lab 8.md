# Zadanie 1

1.
```sql
drop teable kreatura;
create table kreatura as select * from wikingowie.kreatura;
create table uczestnicy as select * from wikingowie. uczestnicy;
create table etapy_wyprawy as select * from wikingowie.etapy_wyprawy;
create table sektor as select * from wikingowie.sektor;
create table wyprawa as select * from wikingowie.wyprawa;
```


2.
```sql
select k.nazwa, u.id_uczestnika from kreatura k
left join uczestnicy u on k.idKreatury = u.id_uczestnika
where u.id_uczestnika is null; 
```

3.
```sql
select max(w.nazwa), sum(e.ilosc)
from wyprawa w
inner join uczestnicy u on w.id_wyprawy = u.id_wyprawy
inner join ekwipunek e on u.id_uczestnika = e.idKreatury
group by w.id_wyprawy;
```

# Zadanie 2

1.
```sql
select rodzaj, count(*), group_concat(nazwa SEPARATOR ' ') from kreatura
group by rodzaj;
```

2.
```sql
select w.nazwa, w.data_rozpoczecia,
e.kolejnosc, s.nazwa, k.nazwa
from etapy e
inner join wyprawa w on e.id_wyprawy = w.id_wyprawy
inner join sektor s on e.idSektora = s.id_sektora
inner join kreatura k on w.kierownik = k.idKreatury
order by data_rozpoczecia, kolejnosc;
```












