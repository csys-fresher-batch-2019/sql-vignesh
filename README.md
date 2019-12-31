# Online bus ticket booking system
### *https://onlinebusticketbooking.in

## features
   ### *user can be able to view all type of bus.
## feature 1:list of all buses
```sql
create table bus_list(
bus_no number,
bus_name varchar2(50) not null unique,
bus_source varchar2(50),
bus_destination varchar2(50),
class varchar2(50) not null,
constraint bus_no_pk primary key (bus_no),
constraint bus_class_ck check(class in ('sleeper','seater','sleeper-ac','seater-ac')),
constraint source_destination_ck check(bus_source<>bus_destination));

insert into bus_list (bus_no,bus_name,bus_source,bus_destination,class) 
values (11,'dulexe','cmbt','madurai','sleeper');
insert into bus_list (bus_no,bus_name,bus_source,bus_destination,class)
values (12,'express','cmbt','ramnad','sleeper-ac');
insert into bus_list (bus_no,bus_name,bus_source,bus_destination,class)
values (13,'superdulexe','tmb','vellore','seater');
insert into bus_list (bus_no,bus_name,bus_source,bus_destination,class)
values (10,'parveen','tmb','tirpur','seater-ac');
select *from bus_list where bus_source='cmbt' and bus_destination='madurai';

```

