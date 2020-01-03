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
select *from bus_list where bus_source='cmbt' and bus_source='cmbt';

```
| s.no | bus_no | bus_name     | bus_source | bus_destination | class       |
|------|--------|--------------|------------|-----------------|-------------|
| 1    | 11     | dulexe       | cmbt       | maduai          | sleeper     |
| 2    | 12     | express      | cmbt       | ramnad          | sleeper_ac  |
| 3    | 13     | super dulexe | tmb        | vellore         | seater      |
| 4    | 10     | parveen      | tmb        | tirpur          | seater_ac   |


## feature-2 passanger information

```sql
create table passenger (
bus_no number,
pas_id number not null,
pas_name varchar2(50) not null,
pas_age number not null,
pas_gender char(1) not null,
pas_contact number(10) not null,
constraint bus_no_fk foreign key (bus_no) references bus_list(bus_no),
constraint pas_id_pk primary key(pas_id),
constraint pas_age_ck check(pas_age>=1),
constraint pas_gender_ck check(pas_gender in('M','F')),
constraint pas_contat_ck check(pas_contact>999999999));
create sequence pas_id
start with 1000
increment by 1
insert into passenger (bus_no,pas_id,pas_name,pas_age,pas_gender,pas_contact) 
values (11,pas_id.nextval,'vikki',24,'M',8989123456);
insert into passenger (bus_no,pas_id,pas_name,pas_age,pas_gender,pas_contact) 
values (12,pas_id.nextval,'aravind',23,'M',9999654321);
insert into passenger (bus_no,pas_id,pas_name,pas_age,pas_gender,pas_contact) 
values (10,pas_id.nextval,'priya',22,'F',8887776661);
insert into passenger (bus_no,pas_id,pas_name,pas_age,pas_gender,pas_contact) 
values (13,pas_id.nextval,'manoj',21,'M',8800770066);
select * from passenger;
```
| s.no | bus_no  |bus_id     | pas_name | pas_age | pas_gender | pas-contact |
|------|-------- | --------  |----------|---------|------------|-------------|
| 1    | 11      |  1000     | vikki    | 24      | M          | 8989123456  |
| 2    | 12      |  1001     | aravind  | 23      | M          | 9999654321  |
| 3    | 10      |  1002     | priya    | 22      | F          | 8887776661  |
| 4    | 13      |  1003     | manoj    | 21      | M          | 8800770066  |

## feature-3 bus_timing
```sql
create table bus_time(
bus_no number not null,
amount number not null,
depart_time timestamp not null,
arr_time timestamp not null,
constraint bus_no_fk2 foreign key(bus_no) references bus_list(bus_no)
);
insert into bus_time values (11,100,to_date('20-01-2020 10:00:00PM','dd-mm-yyyy hh:mi:ssPM'),
to_date('21-01-2020 05:00:00AM','dd-mm-yyyy hh:mi:ssAM'));
insert into bus_time values (10,200,to_date('21-01-2020 07:00:00PM','dd-mm-yyyy hh:mi:ssPM'),
to_date('22-01-2020 05:00:00AM','dd-mm-yyyy hh:mi:ssAM'));
insert into bus_time values (13,300,to_date('20-01-2020 09:00:00PM','dd-mm-yyyy hh:mi:ssPM'),
to_date('24-01-2020 06:00:00AM','dd-mm-yyyy hh:mi:ssAM'));
insert into bus_time values (12,500,to_date('18-01-2020 08:00:00PM','dd-mm-yyyy hh:mi:ssPM'),
to_date('19-01-2020 07:00:00AM','dd-mm-yyyy hh:mi:ssAM'));
select * from bus_time;
```
| s.no | bus_no | amount | dpart_time                     | arr_time                       |
|------|--------|--------|--------------------------------|--------------------------------|
| 1    | 11     | 100    | 20-01-20 10:00:00.000000000 PM | 21-01-20 05:00:00.000000000 AM |
| 2    | 10     | 200    | 21-01-20 07:00:00.000000000 PM | 22-01-20 05:00:00.000000000 AM |
| 3    | 13     | 300    | 20-01-20 09:00:00.000000000 PM | 24-01-20 06:00:00.000000000 AM |
| 4    | 12     | 500    | 18-01-20 08:00:00.000000000 PM | 19-01-20 07:00:00.000000000 AM |

## feature-4 Reservation information
```sql
create table reserve(ticket_no number not null,
bus_no number not null,
pas_id number not null,
no_of_tick number not null,
constraint no_of_tick_ck check(no_of_tick>0),
constraint pas_id_pk3 foreign key(pas_id) references passenger(pas_id),
constraint bus_no_pk2 foreign key(bus_no) references bus_list(bus_no)
);
insert into reserve values (11111,11,1020,5);
insert into reserve values (22222,12,1021,3);
insert into reserve values (33333,10,1022,2);
insert into reserve values (44444,12,1023,10);
select * from reserve;
```
| s.no | ticket_no |  bus_no | pas_id | no_of_tick |
|------|-----------|-------- |--------|------------|
| 1    | 11111     |   11    | 1000   | 5          |
| 2    | 22222     |   12    | 1001   | 3          |
| 3    | 33333     |   10    | 1002   | 2          |
| 4    | 44444     |   13    | 1003   | 10         |

### feature-5 seats Availability
```sql
create table seat_availablity(bus_no number not null,
available_seats number not null,
constraint foreign_key_bus_no foreign key(bus_no) references bus_list(bus_no),
constraint check_no_of_seats check(available_seats>=0)
);
insert into seat_availablity values (12,15);
insert into seat_availablity values (11,25);
insert into seat_availablity values (10,20);
insert into seat_availablity values (13,10);
select * from seat_availablity;
```
| s.no | bus_no | available_seats |
|------|--------|-----------------|
| 1    | 12     | 15              |
| 2    | 11     | 25              |
| 3    | 10     | 20              |
| 4    | 13     | 10              |

###  freature-6 senario :To check bus source and destination details
```sql
select *from bus_list where bus_source='cmbt' and bus_source='cmbt';
```
| s.no | bus_no | bus_name     | bus_source | bus_destination | class       |
|------|--------|--------------|------------|-----------------|-------------|
| 1    | 11     | dulexe       | cmbt       | maduai          | sleeper     |
| 2    | 12     | express      | cmbt       | ramnad          | sleeper_ac  |
```sql
select * from passenger where bus_no=11;
```
| s.no | bus_no  |bus_id     | pas_name | pas_age | pas_gender | pas-contact |
|------|-------- | --------  |----------|---------|------------|-------------|
| 1    | 11      |  1000     | vikki    | 24      | M          | 8989123456  |

