# Lab 5 Zadania

### Zadanie 1

1.
```sql
select * from postac
where rodzaj = 'wiking'
and nazwa <> 'Bjorn' # <>, != - rozny od
order by data_ur asc limit 2;

delete from postac where nazwa = 'Ragnar';
delete from postac where nazwa = 'Floki';
```
2.
```sql
alter table postac change id_postaci id_postaci int;
alter table postac modify id_postaci int;
# krok 2 - najpierw jednak usunecie kluczy obcych
alter table walizka drop foreign key walizka_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_1;
alter table przetwory drop foreign key przetwory_ibfk_2;
#....a
# wracamy do usuniecia auto_increment
# krok 3 - ostatecznie usuniecie klucza glownego
alter table postac drop primary key;
show create table postac;
```

### Zadanie 2

1.
```sql
# varchar vs varchar - varchar do max znakow, char -> dokladna ilosc znakow 
alter table postac add column pesel char(11) first;
# po uzupelnieniu danych mozemy dodac klucz glowny 
alter table postac add primary key(pesel);
update postac set pesel = '76453625431' + id_postaci;
select * from postac;
```
2.
```sql
alter table postac modify rodzaj enum('wiking', 'ptak', 'kobieta', 'syrena');
```
3.
```sql
insert into postac values('1234567890', default, 'Gertruda Nieszczera', 'syrena', '1060-05-02', '35', 1);
```

### Zadanie 3

1.
```sql
# % dowonly ciag znakow, _ - dokladnie jeden znak
update postac set statek = 1  where nazwa like '%a%';
```

2.
```sql
select * from statek where data_wodowania >= '1901-01-01' and data_wodowania <= '2000-12-31';
# lub
select * from statek where data_wodowania between '1901-01-01' and '2000-12-31';
# dla wykorzystania mniej szczegółowefgo przy samym użyciu roku
select * from statek where year(data_wodowania) between 1901 and 2000;

update statek
set max_ladownosc=max_ladownosc * 0.7 where year (data_wodowania) between 1901 and 2000;
```

3.
```sql
#instrukcja check
alter table postac add check (wiek < = 1000);
# test instrukcji check
update postac set wiek = 2000 where nazwa='Bjorn';
```

### Zadanie 4

1.
```sql
# krok 1 - dodanie weza do pola rodzaj
alter table postac modify rodzaj enum('wiking', 'ptak', 'kobieta', 'syrena', 'waz');
# krok 2 - dodanie rekordu z wężem Lokko
insert into postac values('09876543211', default, 'Lokko', 'waz', '1960-06-03', '10', NULL);
```

2.
```sql
# 1 opcja - nie musimy robic klucza glownego, nie przenosi od razu danych 
create table marynarz like postac;
insert into marynarz select * from postac where statek is not null;
# 2 opcja - wtedy mozemy wybrac konkretne rekordy z tabeli postac
create table marynarz as select * from postac where statek is not null;
```

3.
```sql
alter table marnarz add foreign key(statek) references(statek) 
```

### Zadanie 5

1.
```sql
update postac set statek=null;
```

2.
```sql
delete from postac where nazwa='Ragnar';
```

3.
```sql
delete from statek where nazwa_statku = 1
```

4.
```sql
show create table postac;
alter table postac drop foreign key postac_ibfk_;
drop table statek;
```

5.
```sql
CREATE TABLE zwierz (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nazwa VARCHAR(100),
    wiek INT
);
```

6.
```sql
insert into zwierz (nazwa, wiek)
select Drozd, wiek from postac;
```
