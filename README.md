# Online bus ticket booking system
### *https://onlinebusticketbooking.in

## features
   ### *user can be able to view and booking all type of bus.
## feature 1:list of all buses
```sql
create table bus_list( 
bus_no number, 
bus_name varchar2(50) not null, 
bus_source varchar2(50), 
bus_destination varchar2(50), 
class varchar2(50) not null, 
constraint bus_no_pk primary key (bus_no), 
constraint bus_class_ck check(class in ('sleeper','seater','sleeperAc','seaterAc')), 
constraint source_destination_ck check(bus_source<>bus_destination));
create sequence bus_no_seq start with 10
increment by 1;

insert into bus_list (bus_no,bus_name,bus_source,bus_destination,class) 
values (1,'dulexe','CMBT','MADURAI','sleeper');

```
| s.no | bus_no | bus_name     | bus_source | bus_destination  | class       |
|------|--------|--------------|------------|------------------|-------------|
| 1    | 1      | dulexe       | CMBT       | MADURAI          | sleeper     |


## feature-2 passanger information

```sql
create table passenger (
pas_id number not null,
pas_name varchar2(50) not null,
pas_age number not null,
pas_gender varchar2(20) not null,
pas_contact number(10) unique not null,
constraint pas_id_pk primary key(pas_id),
constraint pas_age_ck check(pas_age>=1),
constraint pas_gender_ck check(pas_gender in('Male','Female')),
constraint pas_contact_ck check(pas_contact>999999999));

create sequence pas_id
start with 1000
increment by 1;

insert into passenger (pas_id,pas_name,pas_age,pas_gender,pas_contact) 
values (pas_id.nextval,'vikki',24,'M',8989123456);
select * from passenger;
```
| s.no |  pas_id    | pas_name | pas_age | pas_gender | pas-contact |
|------| ---------  |----------|---------|------------|-------------|
| 1    |     1000   | vikki    | 24      | M          | 8989123456  |

## feature-3 bus_timing
```sql
create table bus_time(
bus_no number not null,
amount number not null,
departure_time timestamp not null,
arrival_time timestamp not null,
constraint bus_no_pk1 primary key(bus_no),
constraint bus_no_fk2 foreign key(bus_no) references bus_list(bus_no)
);

insert into bus_time values (10,100,to_date('10-02-2020 07:00:00PM','dd-mm-yyyy hh:mi:ssPM'),
to_date('11-02-2020 05:00:00AM','dd-mm-yyyy hh:mi:ssAM'));

select * from bus_time;
```
| s.no | bus_no | amount | departure_time        | arrival_time          |
|------|--------|--------|-----------------------|-----------------------|
| 1    | 10     | 100    | 10-02-2020 07:00:00PM | 11-02-2020 05:00:00AM |


## feature-4 Reservation information
```sql
create table reserve(
ticket_no number not null,
bus_no number not null,
pas_id number not null,
no_of_ticket number not null,
journey_date timestamp not null,
total_amount number,
status varchar2(20),
constraint ticket_no_pk primary key(ticket_no),
constraint no_of_ticket_ck check(no_of_ticket>0),
constraint status_ck check(status in('Booked')),
constraint pas_id_pk3 foreign key(pas_id) references passenger(pas_id),
constraint bus_no_pk2 foreign key(bus_no) references bus_list(bus_no)
);
alter table reserve add user_id number;
create sequence ticket_no
start with 100
increment by 1;

select * from reserve;
```
| s.no |ticket_no|  bus_no | pas_id | no_of_tick |
|------|---------|-------- |--------|------------|
| 1    | 100     |   11    | 1000   | 5          |
| 2    | 101     |   12    | 1012   | 3          |
| 3    | 102     |   10    | 1002   | 2          |
| 4    | 103     |   12    | 1003   | 10         |

### feature-5 seats Availability
```sql
create table seat_availability(
bus_no number unique not null,
available_seats number not null,
total_seats number not null,
constraint foreign_key_bus_no foreign key(bus_no) references bus_list(bus_no),
constraint check_no_of_seats check(available_seats>=0)
);

insert into seat_availablity values (10,50,50);
insert into seat_availablity values (11,25);
insert into seat_availablity values (10,20);
insert into seat_availablity values (13,10);
select * from seat_availablity;
```
| s.no | bus_no | available_seats | total_seats |
|------|--------|-----------------|-------------|
| 1    | 12     | 50              | 50          |

###  freature-6 senario :To check bus source and destination details
```sql
select *from bus_list where bus_source='cmbt';
```
| s.no | bus_no | bus_name     | bus_source | bus_destination  | class       |
|------|--------|--------------|------------|------------------|-------------|
| 1    | 10     | dulexe       | CMBT       | MADURAI          | sleeper     |

```sql
select * from passenger where pas_id=1000;
```
| s.no |   pas_id  | pas_name | pas_age | pas_gender | pas-contact |
|------| --------  |----------|---------|------------|-------------|
| 1    |  1000     | vikki    | 24      | M          | 8989123456  |

### senario- update bus_list
```sql
insert into bus_list (bus_no,bus_name,bus_source,bus_destination,class) 
values (10,'dulexe','cmbt','madurai','sleeper');
```
| s.no | bus_no | bus_name     | bus_source | bus_destination | class       |
|------|--------|--------------|------------|-----------------|-------------|
| 1    | 11     | dulexe       | cmbt       | maduai          | sleeper     |
### senario- If passenger age greater then 22---
```sql
select * from passenger where pas_age>23;
```
| s.no | bus_no  |bus_id     | pas_name | pas_age | pas_gender | pas-contact |
|------|-------- | --------  |----------|---------|------------|-------------|
| 1    | 11      |  1000     | vikki    | 24      | M          | 8989123456  |


### number of buses--
```sql
select count(*) bus_no from bus_list;
```
| bus_no  |
|---------|
|  1      |
### number of passengers--
```sql
select count(*) pas_id from passenger;
```
| pas_id  |
|---------|
|  1      |
### AdminLogin
```sql
create table AdminRegister
(
Admin_id number ,
Admin_name varchar(20) not null,
Email_id varchar(30) ,
pass_word varchar(30) not null,
constraint admin_id_uk unique (admin_id),
constraint Email_id_uh unique (Email_id));
```
### UserLogin
```sql
create table User_register(
name varchar(30) not null,
Email_id varchar(30) unique,
password varchar(30) not null,
contact number not null,
user_id number unique,
constraint user_id_ck check (user_id>=100)
);

create sequence user_id
start with 100 increment by 1;
```
### senario:using view
```sql
create or replace view bus_list_view as 
select bl.bus_no,bl.bus_name,bl.bus_source,bl.bus_destination,bl.class,bt.amount,bt.departure_time,bt.arrival_time,bs.total_seats, bs.total_seats as available_seats
from bus_list bl,bus_time bt,seat_availability bs where bl.bus_no = bt.bus_no and bt.bus_no = bs.bus_no;
select * from bus_list_view;
```
### senario:Remaining tickets
```sql
CREATE OR REPLACE FUNCTION SEATS_AVALABILITY (i_bus_no IN number)
RETURN NUMBER AS 
remaining_seats number;
booked_seats number;
maximum_seats number;
BEGIN
select available_seats into maximum_seats from seat_availablity where bus_no=i_bus_no;
select sum(no_of_tick) into booked_seats from reserve where bus_no=i_bus_no;
remaining_seats := maximum_seats - booked_seats;
  RETURN remaining_seats;
END SEATS_AVALABILITY;
select SEATS_AVALABILITY(11)from dual;
```
### senario:Using procedure
```sql
create or replace procedure ticket_booking(
bus_id in number,
passenger_id in number,
no_of_tickets in number,
journey_date in timestamp,
i_user_id in number,
o_ticket_id out number
)as 
seat_count number;
bus_fare number;
amt number;

begin
select ticket_no.nextval into o_ticket_id from dual;
  select amount into amt from bus_time where bus_no=bus_id;
  bus_fare:=no_of_tickets * amt;
  select available_seats into seat_count from seat_availability where bus_no=bus_id;
  if(seat_count>=no_of_tickets) then
    insert into reserve(ticket_no,bus_no,pas_id,no_of_ticket,total_amount,journey_date,status,user_id) values (o_ticket_id,bus_id,passenger_id,no_of_tickets,bus_fare,journey_date,'Booked',i_user_id);
    update seat_availability set available_seats=available_seats-no_of_tickets where bus_no=bus_id;
    update reserve set total_amount  = bus_fare where ticket_no = bus_id;
    o_ticket_id:=o_ticket_id;
    --ticket_status:='Ticket booked';
 -- else
     --   ticket_status:='Booking failed';
   
end if;
end ticket_booking;
```
