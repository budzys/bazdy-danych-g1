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
select w.data_rozpoczecia, ew.sektor
,ew.kolejnosc, s.nazwa, k.nazwa, w.id_wyprawy
from etapy_wyprawy ew
inner join wyprawa w on w.id_wyprawy = ew.idWyprawy
inner join sektor s on ew.sektor = s.id_sektora
inner join kreatura k on w.kierownik = k.idKreatury
order by w.data_rozpoczecia, ew.kolejnosc;
```

# Zadanie 3

1.
```sql
select s.nazwa, count(ew.sektor) from sektor s
left join etapy_wyprawy ew on s.id_sektora=ew.sektor
group by s.nazwa;
```

2.
```sql
select k.nazwa, 
if (count(u.id_uczestnika)>0, 'brał udział', 'nie brał udziału') 
from uczestnicy u 
right join kreatura k on k.idKreatury=u.id_uczestnika
group by k.nazwa;
```

# Zadanie 4

1.
```sql
select nazwa, length(nazwa) from kreatura;
```

2. 
```sql
select w.nazwa, u.id_uczestnika, e.ilosc, z.waga, 
sum(e.ilosc * z.waga) / count(distinct u.id_uczestnika)
from uczestnicy u
inner join wyprawa w on u.id_wyprawy=w.id_wyprawy
inner join ekwipunek e on u.id_uczestnika=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu
group by w.id_wyprawy;
```

# Zadanie 5
```sql
select k.nazwa, datediff (w.data_rozpoczecia, k.dataUr) as wiek_w_dniach
from kreatura k 
inner join uczestnicy u on u.id_uczestnika=k.idKreatury
inner join wyprawa w on u.id_wyprawy=w.id_wyprawy
inner join etapy_wyprawy ew on ew.idWyprawy=w.id_wyprawy
where ew.sektor=7 group by w.id_wyprawy, k.idKreatury;
```
















