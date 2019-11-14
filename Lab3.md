1.

```
create table hostel (
	hno int,
	hname varchar(255),
	type varchar(255),
	primary key (hno)
);

create table menu (
	hno int references hostel(hno),
	day varchar(255),
	breakfast varchar(255),
	lunch varchar(255),
	dinner varchar(255)
	
);

create table warden (
	wname varchar(255),
	qual varchar(255),
	hno int references hostel(hno)
);

create table student (
	sid int,
	sname varchar(255),
	gender varchar(255),
	year int,
	primary key (sid),
	hno int references hostel(hno)
);	

insert into hostel values (1, "Opal", "girls");
insert into hostel values (2, "Jade", "boys");
insert into hostel values (3, "Diamond", "boys");
insert into hostel values (4, "Coral", "boys");

insert into menu values (1, "Sunday", "Aloo Paratha", "Rice", "Chapathi Dhal");
insert into menu values (1, "Monday", "Dosa", "Rotis", "Fried Rice");
insert into menu values (2, "Sunday", "Idli", "Channa", "Dosa");
insert into menu values (3, "Sunday", "Ghee Dosa", "Paneer", "Pulao");

insert into warden values ("Sridevi", "Dr", 1);
insert into warden values ("Ram", "Dr", 2);
insert into warden values ("Jerome", "Dr", 3);

insert into student values (1, "Sandhya", "female", 3, 1);
insert into student values (2, "Daniel", "male", 1, 2);
insert into student values (3, "Rahul", "male", 2, 3);

```

```
2. select count(*) from hostel where type="girls"; select count(*) from hostel where type="boys";
3. select breakfast, lunch, dinner from menu inner join hostel on menu.hno = hostel.hno where day = "Tuesday" and hname  = "x";
4. select count(*), hname from warden inner join hostel on warden.hno = hostel.hno group by hostel.hno;
5. select count(*), hname from student inner join hostel on student.hno = hostel.hno group by hostel.hno;
6. update menu set breakfast = "Noodles" where day = "Thursday" and hno = 5;
7. select * from warden where qual = "Bcom" group by hno;
8. select count(*) from student where sname like "A%" and hno = 1;
9. select count(*), year from student where gender = "male" group by year;
10. select wname, hname from warden inner join hostel on warden.hno = hostel.hno where type = "girls";
11. select wname, hname from (student, warden) inner join hostel on warden.hno = hostel.hno and student.hno = hostel.hno where year = 3;
12. select wname, count(*) from (warden, student) inner join hostel on warden.hno = hostel.hno and student.hno = hostel.hno group by hname;
13. create VIEW v as select sname, gender, student.hno, wname from student inner join warden on student.hno = warden.hno;
select * from v;

```

2.

```
create table department (
	deptid int,
	deptname varchar(255),
	primary key (deptid)
);

create table student (
	rollno int,
	name varchar(255),
	gender varchar(255),
	mark1 int,
	mark2 int,
	mark3 int,
	total int,
	average int,
	deptid int references department(deptid),
	primary key (rollno)
);

create table staff (
	staffid int,
	name varchar(255),
	designation varchar(255),
	qualification varchar(255),
	deptid int references department(deptid),
	primary key (staffid)
);

create table tutor (
	rollno int references student(rollno),
	staffid int references staff(staffid)
);

insert into department values(1, "CSE");
insert into department values(2, "ECE");
insert into department values(3, "ICE");

insert into student values (1, "Sandhya", "F", 100, 100, 1000, 300, 100, 1);
insert into student values (2, "Ram", "M", 98, 99, 100, 297, 99, 1);
insert into student values (3, "Rahul", "M", 60, 60, 60, 180, 60, 2);

insert into staff values (1, "Raju", "professor", "Dr", 1);
insert into staff values (2, "Rajeswari", "hod", "Dr", 1);
insert into staff values (3, "Raghavan", "professor", "Dr", 2);

insert into tutor values (1, 1);
insert into tutor values (2, 1);
insert into tutor values (3, 3);
```

```
1. update student set total = mark1 + mark2 + mark3; update student set average = total/3;
2. select count(*) from student inner join department on student.deptid = department.deptid where deptname = "CSE";
3. select * from student where average > 85;
4. select count(*) from staff st inner join tutor t on st.staffid = t.staffid inner join student s on s.rollno = t.rollno where st.name = "Raju";
5. select staffid, name, designation, qualification, deptname from staff inner join department on staff.deptid = department.deptid where deptname = "CSE";
6. select count(distinct(designation)), count(distinct(deptname)) from staff, department;
7. select * from student where name like "R%";
8. select name, deptname from (tutor inner join (student, staff) on tutor.rollno = student.rollno and tutor.staffid = staff.staffid) x inner join department where x.deptid = department.deptid;
9. select count(*) from student where gender="F" group by deptid; select count(*) from student where gender="M" group by deptid;
10. select name, rollno from student inner join department on student.deptid = department.deptid where total = (select max(total) from student s2 where s2.deptid = department.deptid);
11. select tutor.rollno, name from tutor inner join (select name, rollno from student inner join department on student.deptid = department.deptid where total = (select max(total) from student s2 where s2.deptid = department.deptid)) as x  on tutor.rollno = x.rollno;
12. select staffid, staff.name, designation, qualification, staff.deptid from student  inner join staff on (staff.staffid = (select staffid from tutor where rollno = student.rollno) and  student.rollno = (select distinct(rollno) from tutor where rollno = student.rollno)) where gender = "F";
13. create VIEW v as select staffid, name, designation, qualification, deptname from staff inner join department on staff.deptid = department.deptid where designation = "professor";
select * from v;
```
