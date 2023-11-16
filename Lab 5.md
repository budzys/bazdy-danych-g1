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
alter table postac change id_postaci id_postaci int; # pozbywamy sie auto_incrementa
alter table postac drop primary key;
```
