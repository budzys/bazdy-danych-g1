# Nagłówek 1
## Nagłówek 2
###### Nagłówek 6

**Pogrubiony** tekst...  
**_Pogrubiony i kursywa_** tekst...

**Listing 1**

```sql
SELECT * FROM osoba;
```

Kod możemy umieścic liniowo czyli `SELECT * FROM osoba;` tak.

Lista uporządkowana (numerowana).
1. Pozycja 1.
2. Pozycja 2.   
2.1 Pozycja 2.1

Lista wypunktowana:
* punkt 1
* punkt 2
  * punkt 2.1
 
  [etykieta].(url). -> link  
  ![etykieta].(url). -> obraz

**1 zadanie**
1.    create table postac
    -> (id_postaci int primary key auto_increment,
    -> nazwa varchar(40),
    -> rodzaj enum('wiking','ptak','kobieta'),
    -> data_ur date,
    -> wiek int unsigned);

2.   insert into postac values(default, 'Bjorn', 'wiking', '1700-11-09', 45);
   insert into postac values(default, 'Drozd', 'ptak', '2010-04-05', 13);
   insert into postac values(default, 'Tesciowa', 'kobieta', '1680-03-22', 65 );
   select * from postac; -> zeby sprawdzic dane tabeli

3.  update postac set wiek=88 where id_postaci=3;
    delete from postac where id=3; -> jakbym chcial usunac(uwaga usuwa caly wiersz a nie pojedynczy rekord)

**2 zadanie**
1.  create table walizka
    -> (id_walizki int primary key auto_increment,
    -> pojemnosc int unsigned,
    -> kolor enum('rozowy','czerwony','teczowy','zolty'),
    -> id_wlasciciela int,
    -> foreign key(id_wlasciciela) references postac(id_postaci) on delete cascade);

2.  alter table walizka alter kolor set default 'rozowy'; -> **bedzie na kolokwium!!!**

3.  insert into walizka values(default,50,default,1);
   insert into walizka(pojemnosc, id_wlasciciela) values(70,3); -> bez podawania default

**3 zadanie**
1.  create table izba(
    -> adres_budynku varchar(100),
    -> nazwa_izby varchar(100),
    -> metraz int unsigned,
    -> wlasciciel int,
    -> primary key(adres_budynku, nazwa_izby),
    -> foreign key(wlasciciel) references postac(id_postaci) on delete set null);

2.  alter table izba add column kolor varchar(20) default 'czarny' after metraz;

3.   insert into izba values('marcowa 8','stocznia',102,default,1);


    




