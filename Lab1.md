1.

'''create database Company;
use Company;
create table Employee (
	Empid int,
	Empname varchar(255),
	Address varchar(255),
	Doj varchar(255),
	Salary decimal(5,2),
	primary key (Empid)

);

create table Project (
	Projectno int,
	Duration int,
	Projectname varchar(255),
	primary key Projectno
);

create table Workson (
	Empid int references Employee (Empid),
	Projno int references Project (Projectno)
);'''

** Please make PR to add insert commands here, too lazy to add **

1. '''select * from Employee order by Empname desc;'''

2. '''select * from Project where Projectno = 2;'''

3. '''select * from Employee where Empname like "B%";'''

4. '''select EmpId from Workson where Projno = 2;'''

2.

'''
create table Student (
	Rollno int,
	Name varchar(255),
	Marks1 int,
	Marks2 int,
	Marks3 int,
	Marks4 int,
	Marks5 int,
	Marks6 int,
	primary key (Rollno)

);

create table Department (
	Deptid int,
	Deptname varchar(255),
	HODname varchar(255),
	primary key (Deptid)
);

create table StudDep (
	Rollno int references Student(Rollno),
	Deptid int references Department(Deptid)	
);
'''

1. 

'''
insert into Student (Rollno, Name, Marks1, Marks2, Marks3, Marks4, Marks5, Marks6 ) values (1, 'Sandhya', 100, 100, 100, 100, 100, 100);
insert into Student (Rollno, Name, Marks1, Marks2, Marks3, Marks4, Marks5, Marks6 ) values (2, 'Sneha', 99, 100, 100, 100, 99, 100); 
insert into Student (Rollno, Name, Marks1, Marks2, Marks3, Marks4, Marks5, Marks6 ) values (3, 'Neha', 50, 50, 40, 50, 50, 50); 
insert into Student (Rollno, Name, Marks1, Marks2, Marks3, Marks4, Marks5, Marks6 ) values (4, 'Reshma', 60, 100, 60, 10, 90, 100); 

insert into Department (Deptid, Deptname, HODname) values (1, 'CSE', 'Rajeshwari');
insert into Department (Deptid, Deptname, HODname) values (2, 'ICE', 'Someone');

insert into StudDep (Rollno, Deptid) values (1, 1);
insert into StudDep (Rollno, Deptid) values (2, 1);
insert into StudDep (Rollno, Deptid) values (3, 2);
insert into StudDep (Rollno, Deptid) values (3, 2);
'''

2. '''select Name, Marks1, Marks2, Marks3, Marks4, Marks5, Marks6 from Student s inner join StudDep w on s.Rollno = w.Rollno inner join Department d on d.Deptid = w.Deptid where d.Deptid = 1;'''

3. '''select Deptname, HODname  from Student s inner join StudDep w on s.Rollno = w.Rollno inner join Department d on d.Deptid = w.Deptid where s.Rollno = 1;'''

4. '''select Name from Student where (Marks1 + Marks2 + Marks3 + Marks4 + Marks5 + Marks6) >= 500;'''

5. '''select HODname from Department where Deptname = 'CSE';'''

6. '''select s.Rollno from Student s inner join StudDep sd on s.Rollno = sd.Rollno inner join Department d on sd.Deptid = d.Deptid where Deptname = 'CSE';'''

3.

'''
create database Sales;
use Sales;
create table salesperson (
	ssn int,
	name varchar(255),
	start_year int,
	dept_no int,
	primary key (ssn)
);

create table trip(
	ssn int references salesperson (ssn),
	from_city varchar(255),
	to_city varchar(255),
	departure_date varchar(255),
	return_date varchar(255),
	trip_id int,
	primary key (trip_id)
);

create table salerep_expense (
	expense_type varchar(255),
	amount decimal(5,2),
	trip_id int references trip(trip_id)
);

insert into salesperson (ssn, name, start_year, dept_no) values (1, 'Ashish', 2004, 100);
insert into salesperson (ssn, name, start_year, dept_no) values (2, 'Bestin', 2008, 200);
insert into salesperson (ssn, name, start_year, dept_no) values (3, 'Daniel', 2012, 200);
insert into salesperson (ssn, name, start_year, dept_no) values (4, 'Effy', 2014, 300);

insert into trip (ssn, from_city, to_city, departure_date, return_date, trip_id) values (1, 'Chennai', 'Bangalore', '11.02.2004', '12.04.2004', 1);
insert into trip (ssn, from_city, to_city, departure_date, return_date, trip_id) values (2, 'Mumbai', 'Bangalore', '11.02.2008', '12.04.2008', 2);
insert into trip (ssn, from_city, to_city, departure_date, return_date, trip_id) values (3, 'Chennai', 'Mumbai', '11.02.2012', '12.04.2012', 3);
insert into trip (ssn, from_city, to_city, departure_date, return_date, trip_id) values (4, 'Chennai', 'Mumbai', '11.02.2014', '12.04.2014', 4);
insert into trip (ssn, from_city, to_city, departure_date, return_date, trip_id) values (3, 'Bangalore', 'Mumbai', '11.02.2018', '12.04.2018', 5);

insert into salerep_expense(expense_type, amount, trip_id) values ('TRAVEL', 5000.00, 1);
insert into salerep_expense(expense_type, amount, trip_id) values ('FOOD', 100.00, 2);
insert into salerep_expense(expense_type, amount, trip_id) values ('TRAVEL', 1000.00, 2);
insert into salerep_expense(expense_type, amount, trip_id) values ('TRAVEL', 2000.00, 3);
insert into salerep_expense(expense_type, amount, trip_id) values ('FOOD', 1000.00, 3);
'''

1. '''select trip.ssn, trip.from_city, trip.to_city, trip.departure_date, trip.return_date from trip inner join salerep_expense on trip.trip_id = salerep_expense.trip_id where (select sum(amount)) >=2000;'''

2. '''select ssn from trip where to_city = 'Chennai'  group by ssn having count(to_city) >=2;'''

3. '''select sum(salerep_expense.amount) from trip inner join salerep_expense on trip.trip_id = salerep_expense.trip_id where ssn = 1000;'''

4. '''select name from salesperson order by name asc;'''

4.

'''
create table car (
	serial_no int,
	model varchar(255),
	manufacturer varchar(255),
	price decimal(15,2),
	primary key (serial_no)
);

create table options (
	serial_no int references car(serial_no),
	option_name varchar(255),
	price decimal(15,2)
);

create table sales (
	salesperson_id int references salesperson(salesperson_id),
	serial_no int references car(serial_no),
	date varchar(255),
	sale_price decimal(15,2),
	primary key (salesperson_id)
);

create table salesperson (
	salesperson_id int,
	name varchar(255),
	phone varchar(255),
	primary key (salesperson_id)
);

insert into car values(1000, "B5", "BMW", "10000000");
insert into car values(2,"B6", "BMW", 20000000);
insert into car values(4,"B7", "BMW", 30000000);
insert into car values(3,"A3", "AUDI", 10000000);
insert into car values(5,"A5", "AUDI", 20000000);
insert into car values(9,"A7", "AUDI", 41000000);
insert into car values(8,"A6", "AUDI", 35000000);

insert into  options values(1000, "Air bag", 10000);
insert into  options values(1000,"Rear cam", 20000);
insert into  options values(1000,"Extra leg room", 12000);
insert into  options values(9,"Air bag", 8000);
insert into  options values(9,"Extra leg room", 5000);
insert into  options values(9,"Rear cam", 12000);
insert into  options values(9,"Diesel", 3000);


insert into salesperson values(1, "John", 9999999999);
insert into salesperson values(2, "Ram", 9156728463);
insert into salesperson values(3, "Sreevats", 913547861);
insert into salesperson values(4, "RSRS", 993692581);
insert into salesperson values(5, "Subash", 914725855);
insert into salesperson values(6, "Trishi", 9994288654);

insert into sales values(1, 1000, "2018-05-08", 10050000);
insert into sales values(2, 3, "2018-05-08", 20050000);
insert into sales values(3, 5, "2018-05-08", 40050000);
insert into sales values(4, 9, "2018-05-08", 25050000);
insert into sales values(5, 2, "2018-05-08", 31050000);
insert into sales values(6, 8, "2018-05-08", 29050000);
'''

1. '''select name, sa.serial_no, sales_price, price from salesperson s inner join sales sa on s.salesperson_id = sa.salesperson_id inner join car c on sa.serial_no = c.serial_no where name = "John";'''

2. '''select car.serial_no, car.model from car LEFT JOIN options on car.serial_no = options.serial_no where options.option_name is NULL;'''

3. '''select distinct(c.serial_no), c.model, sales_price from car c inner join sales s on c.serial_no = s.serial_no inner join options o on c.serial_no = o.serial_no;'''

4. '''update salesperson set phone_no = 9998999799 where name = "Ram";'''
