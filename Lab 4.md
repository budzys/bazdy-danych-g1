# Lab 4 Zadania

### Zadanie 1 

1.
```sql
CREATE TABLE postac(
id_postaci INT primary key AUTO_INCREMENT,
nazwa VARCHAR(40),
rodzaj ENUM('wiking', 'ptak', 'kobieta'),
data_ur DATE,
wiek INT UNSIGNED);
```
2.
```sql
INSERT INTO postac VALUES(default, 'Bjorn', 'wiking', 1700-02-02, 45);
INSERT INTO postac VALUES(DEFAULT, 'Drozd', 'ptak', 2010-10-05, 13);
INSERT INTO postac VALUES(default, 'Tesciowa', 'kobieta', 1650-02-12, 70);
```
3.
```sql
UPDATE postac SET wiek = 88 WHERE ID = 3; 
```

### Zadanie 2

1.
```sql
CREATE TABLE walizka(
id_walizki INT PRIMARY KEY AUTO_INCREMENT,
pojemnosc INT UNSIGNED,
kolor ENUM('rozowy', 'czerwony', 'teczowy', 'zolty'),
id_wlasciela int,
foreign key(id_wlasciciela) references postac(id_postaci) on delete CASCADE);
```

2. 
```sql
alter table walizka kolor set default 'rozowy';
```

3.
```sql
INSERT into walizka values(default, 40, default, 1);
insert into walizka values(70, 3);
```

### Zadanie 3

1.
```sql
create table izba(
adres_budynku VARCHAR(100) PRIMARY KEY,
nazwa_izby VARCHAR(100) PRIMARY KEY,
metraz INT UNSIGNED,
wlascieciel INT,
FOREIGN KEY (wlasciciel) REFERENCES postac(id_postaci) on delete set NULL);
```

2.
```sql
alter table izba add column kolor VARCHAR(20) default 'czarny' after metraz;
```

3.
```sql
insert into izba values('marcowa 8', 'spizarnia', 40, 1,); 
```

### Zadanie 4

1.
```sql
create table przetwory(
id_przetworu int primary key auto_increment,
rok_produkcji int default 1654,
id_wykonawcy int,
foreign key (id_wykonawcy) references postac(id_postaci),
zawartosc varchar(50),
dodatek varchar(60) default 'papryczka chilli',
id_konsumenta int,
foreign key (id_konsumenta) references postac(id_postaci)
);
```
UWAGA! Operowanie tabelą może być na kolokwium. Przydatna komenda show create table nazwa_tabeli

2.
```sql
insert into przetwory values(default,default,3,'bigos z papryczką chilli', default, 1);
```

### Zadanie 5

1.
```sql
insert into postac values(default, 'Ragnar', 'wiking', '1700-01-11', 50);
insert into postac values(default, 'Ubbe', 'wiking', '1800-01-13', 35);
insert into postac values(default, 'Ivar', 'wiking', '1810-04-12', 30);
insert into postac values(default, 'Sigurd', 'wiking', '1840-10-15', 31);
insert into postac values(default, 'Floki', 'wiking', '1650-09-04', 40);
```
2. 
```sql
create table statek(
nazwa_statku int primary key auto_increment,
rodzaj_statku enum('drakar', 'transportowiec','rybacka'),
data_wodowania date,
max_ladownosc int unsigned
);
```
3.
```sql
insert into statek values(default, 'drakar', '1600-05-20', 50);
insert into statek values(default, 'rybacka', '1600-05-20', 50);
```
4.
```sql
alter table postac add column pola enum('laka', 'gory') after wiek;
```

5.
```sql
update postac set rodzaj = 'kapitan' where id_postaci = 1;
```
6.
```sql
alter table postac add column statek int;
alter table postac add foreign key(statek) references statek(nazwa_statku);
```
7.
```sql
update postac set statek = 1 where nazwa = 'Bjorn';
update postac set statek = 2 where nazwa = 'Floki';
```

8.
```sql
delete from izba where nazwa_izby = 'spizarnia';
```
9.
```sql
drop table izba;
```
