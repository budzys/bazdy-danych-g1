# Zadanie 1

Przydatne:
show triggers;
show create trigger nazwa;
drop trigger nazwa;


delimiter // deklaracja zmieniająca na określony czas, specjalnego znaku, 
który powoduje wykonanie określonych instrukcji w ramach interpretera mySQL

new -> insert.update
old -> update, delete 

1.
```sql
delimiter //  
create trigger kreatura_before_insert
before insert on kreatura
for each row
begin 
 if new.waga <= 0
 then
  set new.waga = 1;
 end if;
end //
```

# Zadanie 2

1.
```sql
create table archiwum_wypraw(
id_wyprawy int primary key auto_increment,
nazwa varchar(55),
data_rozpoczecia date,
data_zakonczenia date,
kierownik varchar(55));

delimiter //
create trigger wyprawa_before_delete 
before delete on wyprawa
  for each row
  begin
    insert into archiwum_wypraw
    select w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa
    from wyprawa w join kreatura k on k.idKreatury=w.kierownik
    where id_wyprawy=old.id_wyprawy;
  end//
delimiter ;
```

# Zadanie 3

1.
```sql
delimiter //
create procedure eliksir_sily (in id int)
  begin
    update kreatura set udzwig = udzwig * 1.2 where idKreatury = id;
  end//
delimiter ;
```

2.
```sql


```
# Zadanie 4

1.
```sql

```

2.
```sql

```

# Zadanie 5

1.
```sql

```

2.
```sql

```

















