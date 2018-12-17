--------
|PL-SQL|
--------

1) --print hello
begin
dbms_output.put_line('hello');
end;
/
ans) hello

2) --to display a single value of a single row
declare

v_staff_name staff_master.staff_name%TYPE;

BEGIN

SELECT staff_name INTO v_staff_name FROM staff_master where staff_code='100001';

dbms_output.put_line(v_staff_name);

end;

/

ans) Arvind

3) --to display multiple values of a single row
declare

v_staff_name staff_master.staff_name%TYPE;

v_staff_sal staff_master.staff_sal%TYPE;

BEGIN

SELECT staff_name,staff_sal INTO v_staff_name,v_staff_sal FROM staff_master where staff_code='100001';

dbms_output.put_line(v_staff_name||' '||v_staff_sal);


end;

/
ans) Arvind 17000

4) --to display multiple values from a single column
declare

v_staff_name staff_master.staff_name%TYPE;

cursor c_staffdetails is select staff_name from staff_master where dept_code=20;

BEGIN

open c_staffdetails;

loop

fetch c_staffdetails into v_staff_name;

exit when c_staffdetails%notfound;

dbms_output.put_line(v_staff_name);

end loop;

close c_staffdetails;

end;

/
ans)	Shyam


	Anil


	Smith


	Rahul

5) --to display all records from a table
declare

v_student_details student_master%ROWTYPE;

cursor c_studentdetails is select * from student_master where dept_code=30;

BEGIN

open c_studentdetails;

loop

fetch c_studentdetails into v_student_details;

exit when c_studentdetails%notfound;

dbms_output.put_line(v_student_details.student_code||' '||v_student_details.student_name||' '||v_student_details.student_dob||' '||v_student_details.student_address);

end loop;

close c_studentdetails;

end;

/
ans)	1004 Raj 14-JAN-79 Mumbai


	1009 Vijay 19-JAN-80 Bangalore

	
	1012 Rajesh 22-JAN-80


	1017 Ramesh 27-DEC-80

6)
declare

type rec is RECORD

(staff_name varchar(20),dept_code number,staff_sal number);

var_rec rec;

begin

var_rec.staff_name:='sai';

var_rec.dept_code:=20;

var_rec.staff_sal:=10000;

dbms_output.put_line(var_rec.staff_name||' '||var_rec.dept_code||' '||var_rec.staff_sal);

end;
/
ans) sai 20 10000

7)
declare

type rec is RECORD

(v_staff_code staff_master.staff_code%TYPE,
v_staff_name staff_master.staff_name%TYPE,

v_dept_name department_master.dept_name%TYPE);

var_rec rec;

begin

select staff.staff_code,staff.staff_name,dept.dept_name into var_rec 

from staff_master staff,department_master dept 

where staff.staff_code='100001' and staff.dept_code=dept.dept_code;

dbms_output.put_line(var_rec.v_staff_name||' '||var_rec.v_staff_code||' '||var_rec.v_dept_name);

end;

/
ans)
Arvind 100001 Electronics

8)
declare
v_dept_code department_master.dept_code%type;
cursor c_staff_detail is select staff_name,dept_name from staff_master,department_master
where staff_master.dept_code=department_master.dept_code
and staff_master.dept_code=&v_dept_code;
begin
for var in c_staff_detail
loop
dbms_output.put_line(var.staff_name||', '||var.dept_name);
end loop;
end;declare
v_dept_code department_master.dept_code%type;
cursor c_staff_detail is select staff_name,dept_name from staff_master,department_master
where staff_master.dept_code=department_master.dept_code
and staff_master.dept_code=&v_dept_code;
begin
for var in c_staff_detail
loop
dbms_output.put_line(var.staff_name||', '||var.dept_name);
end loop;
end;
