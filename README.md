# Online bus ticket booking system
### *https://onlinebusticketbooking.in

## features
   ### *user can be able to view all type of bus.
## feature 1:lisr of all buses
```sql
create table bus_list(
bus_no number,
bus_name varchar2(50) not null unique,
bus_source varchar2(50) unique,
bus_destination varchar2(50) unique,
class varchar2(50) not null,
constraint bus_no_pk primary key (bus_no),
constraint bus_class_ck check(class in ('sleeper','seater','sleeper-ac','seater-ac')),
constraint source_destination_ck check(bus_source<>bus_destination));

```

