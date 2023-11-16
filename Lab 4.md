# Lab 4 Zadania

### Zadanie 1 

1.
'''sql
CREATE TABLE postac(
id_postaci INT primary key AUTO_INCREMENT,
nazwa VARCHAR(40),
rodzaj ENUM('wiking', 'ptak', 'kobieta'),
data_ur DATE,
wiek INT UNSIGNED);
'''

1.
'''sql
INSERT INTO postac values(default, 'Bjorn', 'wiking', 1700-02-02, 45);
INSERT INTO postac VALUES(DEFAULT, 'Drozd', 'ptak', 2010-10-05, 13);
insert into postac values(default, 'Tesciowa', 'kobieta', 1650-02-12, 70);
'''
1. 
update postac set wiek = 88 where id = 3; 

### Zadanie 2

1.
CREATE TABLE walizka(
id_walizki INT PRIMARY KEY AUTO_INCREMENT,
pojemnosc INT UNSIGNED,
kolor ENUM('rozowy', 'czerwony', 'teczowy', 'zolty'),
id_wlasciela int,
foreign key(id_wlasciciela) references postac(id_postaci) on delete CASCADE);

2. 
alter table walizka kolor set default 'rozowy';

3. 
INSERT into walizka values(default, 40, default);
insert into walizka values(70, 3);

### Zadanie 3

1.
create table izba (
adres_budynku VARCHAR(100) PRIMARY KEY,
nazwa_izby VARCHAR(100) PRIMARY KEY,
metraz INT UNSIGNED,
wlascieciel INT,
FOREIGN KEY (wlasciciel) REFERENCES postac(id_postaci) on delete set NULL);

2.
alter table izba add column kolor VARCHAR(20) default 'czarny' after metraz;

3.
update table izba values('marcowa 8', 'spizarnia', 40, 1,); 


 
 
 
 
 
