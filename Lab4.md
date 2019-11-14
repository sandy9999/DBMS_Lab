```
create database EmpDept;
use EmpDept;

create table Department(
	DeptNo int,
	DeptName varchar(255),
	Location varchar(255),
	primary key (DeptNo)
);

create table Employee (
	EmpNo int,
	EmpName varchar(255),
	Sex varchar(255),
	Salary int,
	Address varchar(255),
	DeptNo int references Department(DeptNo),
	primary key (EmpNo)
	
);

insert into Department values(1, "CSE", "Hyd");
insert into Department values(2, "ECE", "Trichy");
insert into Department values(3, "Chem", "Gujarat");

insert into Employee values(1, "Sandhya", "F", 10000, "2nd street", 1);
insert into Employee values(2, "Daniel", "M", 20000, "3rd street", 2);
insert into Employee values(3, "Kamalesh", "M", 15000, "4th street", 1);
```

```
1.

DELIMITER //
create procedure ShowDetail(in eno int )
begin
select * from Employee where EmpNo = eno;
end
//


DELIMITER ;
call ShowDetail(1);

2.

DELIMITER //

create procedure addDetail(in EmpNo int, in EmpName varchar(22), in Sex varchar(22), in Salary int, in Address varchar(22), in DeptNo int)
begin
insert into Employee values (EmpNo, EmpName, Sex, Salary, Address, DeptNo);
end
//

DELIMITER ;
call addDetail(4, "Sneha", "F", 40000, "5th street", 3);

3.

DELIMITER //

create procedure raiseSal(in EmpNo int, in inc int)
begin
update Employee set Salary = Salary + inc where EmpNo = EmpNo;
end
//

DELIMITER ;
call raiseSal(4, 5000);

4.

DELIMITER //

create procedure deleteDetail(in ename varchar(255) )
begin
delete from Employee where EmpName = ename;
end	
//

DELIMITER ;
call deleteDetail("Sandhya");

5.

DELIMITER //

create function showwMaxx() returns int
begin
declare sal int;
select max(Salary) into sal from Employee;
return sal;
end
//

DELIMITER ;
select * from Employee where Salary = showwMaxx();

6.

DELIMITER //

create function getTotal() returns int
begin
declare total int;
select count(*) into total from Employee;
return total;
end
//

DELIMITER ;
select getTotal();

7.

DELIMITER //

create function display_salary(id int) returns int
begin
declare total int;
select salary into total from Employee where EmpNo = id;
return total;
end; //

delimiter ;
select display_salary(2);

8.

DELIMITER //

create function avgsal(dept int) returns int
begin
declare total int;
select avg(salary) into total from Employee where DeptNo = 1 group by DeptNo;
return total;
end;
//

delimiter ;
select avgsal(1);

9.

DELIMITER //

create procedure listNames(in dno int)
begin
select EmpName from Employee where DeptNo = dno;
end	
//

DELIMITER ;
call listNames(1);

10.

DELIMITER //

create procedure raiseSal(in EmpNo int, in inc int)
begin
update Employee set Salary = Salary + inc where EmpNo = EmpNo;
end
//

create procedure dept_highest(in dno int)
begin
select max(Salary) from Employee where DeptNo = dno;
end	
//

create procedure dept_highest_all()
begin
declare n int default 0;
declare i int default 0;
select count(*) from Department into n;
set i = 0;
while i < n do
	call dept_highest(i+1);
	set i = i+1;
end while;
end
//

mysql> DELIMITER ;
mysql> call dept_highest_all();

11.

DELIMITER //

create function more_sal() returns int
begin
declare ct int;
select count(*) into ct from Employee where Salary > 50000;
return ct;
end
//

delimiter ;
select more_sal();

12.

DELIMITER //

create function locn() returns int
begin
declare ct int;
select count(*) into ct from Employee inner join Department where Employee.DeptNo = Department.DeptNo and Location = "Chennai";
return ct;
end //

delimiter ;
select locn();
```