1.

```
create table department (
	Dno int,
	Dname varchar(255),
	Managername varchar(255),
	primary key (Dno)
);

create table emp (
	Empno int,
	Ename varchar(255),
	Address varchar(255),
	Sex varchar(255),
	DOB varchar(255),
	Dateofjoining varchar(255),
	Deptno int,
	Division varchar(255),
	Desig varchar(255),
	Salary int,
	primary key (Empno)
);

insert into department (Dno, Dname, Managername) values (1, "CSE", "Sandhya");
insert into department (Dno, Dname, Managername) values (2, "ECE", "Hrishi");
insert into department (Dno, Dname, Managername) values (3, "Civil", "Tanvi");
insert into department (Dno, Dname, Managername) values (4, "Chem", "Subash");


insert into emp (Empno, Ename, Address, Sex, DOB, Dateofjoining, Deptno, Division, Desig, Salary) values (1, "Sanju", "Second street, Trichy", "Male", "19-01-1999", "19-01-2019", 1, "A", "Employee", 1000);
insert into emp (Empno, Ename, Address, Sex, DOB, Dateofjoining, Deptno, Division, Desig, Salary) values (2, "Sneha", "Third street, Trichy", "Female", "17-08-1999", "19-01-2010", 2, "B", "Employee", 2000);
insert into emp (Empno, Ename, Address, Sex, DOB, Dateofjoining, Deptno, Division, Desig, Salary) values (3, "Daniel", "Fourth street, Trichy", "Male", "06-06-1999", "15-03-2012", 3, "C", "Junior Manager", 4000);
insert into emp (Empno, Ename, Address, Sex, DOB, Dateofjoining, Deptno, Division, Desig, Salary) values (4, "Ram", "Fifth street, Trichy", "Male", "22-08-1999", "19-06-2013", 1, "A", "System Administrator", 6000);
insert into emp (Empno, Ename, Address, Sex, DOB, Dateofjoining, Deptno, Division, Desig, Salary) values (5, "Sandhya", "Sixth street, Trichy", "Female", "22-08-1999", "19-06-2013", 1, "A", "Manager", 3000);
insert into emp (Empno, Ename, Address, Sex, DOB, Dateofjoining, Deptno, Division, Desig, Salary) values (6, "Hrishi", "Fifth street, Trichy", "Male", "22-08-1999", "19-06-2013", 2, "A", "Manager", 3000);
```

```
1. select Ename from emp where Salary < 3000 or Salary > 5000;
2. select emp.Ename, emp.Salary from emp inner join department on emp.Deptno = department.Dno where department.Dname = 'admin' or department.Dname = 'finance' or department.Dname = 'sales';
3. select emp.Ename, department.Dname from emp inner join department on emp.Deptno = department.Dno where department.Dname = 'marketing' union select emp.Ename, department.Dname from emp inner join department on emp.Deptno = department.Dno where department.Dname = 'sales';
4.  select Ename from emp where Division = "ne" or Division = "se";
5. select Ename from emp where Salary = (select max(Salary) from emp);
6. select Desig, avg(Salary) from emp group by Desig;
7. select Ename from emp var1 where var1.Salary = (select min(Salary) from emp var2 group by Deptno having var1.Deptno = var2.Deptno);
8. select * from emp var1 where var1.Salary > (select avg(Salary) from emp var2 group by Deptno having var1.Deptno = var2.Deptno);
9. select Ename from emp left outer join department on emp.Ename = department.Managername where department.Managername is NULL;
10. select Ename from emp where Desig!="Manager" & Salary > (select min(Salary) from emp where Desig="Manager");
11. select Dname from department var1 where (select count(*) from emp var2 group by Deptno having var1.Dno = var2.Deptno) = 0;
12. select Ename from emp where Desig!="Manager" & Salary > (select max(Salary) from emp where Desig="Manager");
13. select Ename, (YEAR(curdate())-YEAR(DOB)) as age from emp;
14) select Ename age from emp where (YEAR(curdate())-YEAR(Dateofjoining)) >= 10;
15. create VIEW v as select * from emp where Deptno=1;
select * from v;

```