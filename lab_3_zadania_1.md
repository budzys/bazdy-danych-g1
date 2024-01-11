### Zadanie 1
```sql
select imie, nazwisko, data_urodzenia from pracownik;
```

### Zadanie 2
```sql
select imie, nazwisko, year(curdate()) - year(data_urodzenia) as wiek from pracownik;
#lub
select imie, nazwisko, 2024 - year(data_urodzenia) as wiek from pracownik;
```

### Zadanie 3
```sql
select count(distinct(p.id_pracownika)), d.nazwa from pracownik p
inner join dzial d on p.dzial = d.id_dzialu group by d.id_dzial;
```

### Zadanie 4
```sql
select k.nazwa_kategori, count(distinct(t.id_towaru)) as liczba_produktow from towar t
inner join kategoria k on t.kategoria = k.id_kategori group by k.id_kategori;
```
### Zadanie 5
```sql
select k.nazwa_kategori, group_concat(t.nazwa_towaru) as lista_produktow from kategoria k
inner join towar t on t.kategoria = k.id_kategori group by k.id_kategori;
```

### Zadanie 6
```sql
select round(avg(pensja),2) from pracownik;
```

### Zadanie 7
```sql
select round(avg(pensja),2) from pracownik where year(curdate()) - year(data_zatrudnienia) >= 5;
```

### Zadanie 8
```sql
select t.nazwa_towaru from towar t 
inner join pozycja_zamowienia pz on t.id_towaru = pz.towar 
group by t.nazwa_towaru order by sum(pz.ilosc) desc limit 10;
```

### Zadania 9
```sql
select z.id_zamowienia, z.numer_zamowienia, sum(pz.ilosc*pz.cena) as zsumowana_wartosc_zamowienia from zamowienie z 
inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie
where quarter(z.data_zamowienia)=1
and year(z.data_zamowienia)=2017
group by z.id_zamowienia;
```

### Zadanie 10
```sql
select p.imie, p.nazwisko, sum(pz.ilosc*pz.cena) as zsumowana_wartosc_zamowienia from zamowienie z 
inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie
inner join pracownik p on p.id_pracownika=z.pracownik_id_pracownika
group by p.id_pracownika order by zsumowana_wartosc_zamowienia desc;
```















