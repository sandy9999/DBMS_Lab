```
1.

DELIMITER //

set @insert_count=0;
    -> create trigger 
    -> 1st
    -> after insert on students
    -> for each row
    -> begin
    -> set @insert_count=@insert_count+1;
    -> end//

insert into students values(1,'slims','homer','homer@gmail.com',1,'cse',2487651);
insert into students values(2,'stinson','barney','barney@orkut.com',1,'cse',2487651);
insert into students values(3,'wilson','andrew','andrew@gmail.com',2,'eee',2667651);

select @insert_count;

2.

DELIMITER //

create trigger 2nd
    -> before insert on students
    -> for each row
    -> begin
    -> set @msg='Going to insert';
    -> end//

select @msg;

3.

DELIMITER //

create trigger 3rd
    -> before insert (or update) on students
    -> for each row
    -> begin
    -> set new.phoneno=concat('+91',new.phoneno);
    -> end//

select * from students;

4.

DELIMITER //

CREATE TRIGGER before_students_insert
	BEFORE INSERT
    ON Students
FOR EACH ROW
BEGIN
	IF(LOCATE(' ', new.firstName) <> 0) THEN
	SET NEW.lastName = SUBSTR(new.firstName, locate(' ', new.firstName) + 1);
	SET NEW.firstName = SUBSTR(new.firstName, 1, locate(' ', new.firstName) - 1);
	END IF;
END //


INSERT INTO Students values (4, "Rishab Rahiman", "", "123@abc.com", 3, "CSE", "9876543210") //

SELECT * FROM Students //

5.

DELIMITER //

create trigger 5ins
    -> after insert on students
    -> for each row
    -> begin
    -> insert into studentlog values(Now(),Current_User(),'insert');
    -> end//

create trigger 5ins
    -> after delete on students
    -> for each row
    -> begin
    -> insert into studentlog values(Now(),Current_User(),'delete');
    -> end//

create trigger 5ins
    -> after update on students
    -> for each row
    -> begin
    -> insert into studentlog values(Now(),Current_User(),'update');
    -> end//

DELIMITER ;

insert into students values(4,'johnson','alice','alice@gmail.com',3,'ice',9487651);
select * from studentlog;

6.

DELIMITER //

create trigger 6thh 
before insert on students 
for each row 
begin 
declare msg varchar(255); 
if(new.classyear>=2015) 
then update `ERROR: classyear>=2015` set x=1; 
end if; 
end//

DELIMITER ;

insert into students values(5,'holden','ed','ed@gmail.com',3,'ece',2667651);

7.

DELIMITER //

create trigger 7th
before insert on students 
for each row 
begin 
declare msg varchar(255); 
if(new.firstname='john') 
then update `ERROR: firstname='john'` set x=1; 
end if; 
end//

DELIMITER ;

insert into students values(6,'holden','john','john@gmail.com',1,'ece',2667651);

8.

DELIMITER //

create trigger 8th
before insert on students 
for each row 
begin 
declare msg varchar(255); 
if(old.rollno<>new.rollno) 
then update `ERROR: old.rollno<>new.rollno` set x=1; 
end if; 
end//

9.
DELIMITER //

CREATE VIEW temp_view AS
SELECT RollNo, FirstName FROM Students //

CREATE TRIGGER 9th
	BEFORE INSERT ON Students
FOR EACH ROW
BEGIN
	INSERT INTO temp_view VALUES (new.RollNo, new.FirstName);
END //
```