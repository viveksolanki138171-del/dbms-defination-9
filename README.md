# dbms-defination-9
--Write a PL/SQL block to calculate the total, percentage and grade of student based on his/her Rollno from RESULT table. (Create RESULT table with Rollno, Name, Sub1, Sub2, Sub3, Sub4, Sub5, Total, Per, Grade attributes with appropriate data type).

set serveroutput on; declare
v_rollno result.rollno%type; v_name	result.name%type; v_s1 result.sub1%type;
v_s2 result.sub2%type; v_s3 result.sub3%type; v_s4 result.sub4%type; v_s5 result.sub5%type; v_total number;
v_per number; v_grade varchar2(2);

begin

v_rollno := &enter_rollno;

select name, sub1, sub2, sub3, sub4, sub5 into v_name, v_s1, v_s2, v_s3, v_s4, v_s5 from result
where rollno = v_rollno;

v_total := v_s1 + v_s2 + v_s3 + v_s4 + v_s5; v_per := v_total / 5;

if v_per >= 70 then v_grade := 'a';
elsif v_per >= 60 then v_grade := 'b';
elsif v_per >= 50 then v_grade := 'c';
elsif v_per >= 40 then v_grade := 'd';
else
v_grade := 'f'; end if;

update result
set total = v_total, per	= v_per,
grade = v_grade where rollno = v_rollno;

dbms_output.put_line('roll no : ' || v_rollno); dbms_output.put_line('name			: ' || v_name); dbms_output.put_line('total	: ' || v_total); dbms_output.put_line('percent : ' || v_per); dbms_output.put_line('grade		: ' || v_grade);

commit; end;
/
