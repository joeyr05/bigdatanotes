# Database employee and department:

Status: Completed
Date: December 12, 2024

### **How to run Hadoop**

- open cmd as administrator and enter the following commands
    - `start-all`
    - `jps`
    - `StartNetworkServer -h 0.0.0.0`
- open another cmd as administrator
    - go to the hive/bin directory type `hive` to open the hive interpreter.

CTRL+L to clear screen

### Create tables under database company:

**dept:**

| dno | dname |
| --- | --- |
| 101 | sales |
| 102 | computer |
| 103 | accounts |
| 104 | hr |
| 105 | research_manager |

**emp:**

| eno | ename | esal | dno |
| --- | --- | --- | --- |
| 11 | Neha | 67899 | 101 |
| 12 | Puja | 98675 | 101 |
| 13 | Varun | 76787 | 102 |
| 14 | Harsh | 78653 | 102 |
| 15 | Leena | 89989 | 102 |
| 16 | Geeta | 76787 | 103 |
| 17 | Nita | 20000 | 103 |

`show databases;`

`create database company;`
`use company;`

`create table dept(dno int, name varchar(15)) row format delimited fields terminated by ‘,’;`

`load data local inpath ‘c:/hive/dept.csv’ into table dept;`

`create database emp;
use emp;`

`create table emp(eno int,ename varchar(15),salary int, dno int) row format delimited fields terminated by ‘,’;`

`load data local inpath ‘c:/hive/emp.csv’ into table emp;`

### Queries

- Display employee in descending order of salaries:
`select * from emp order by salary desc;`
- Display all employees who are earning between 60k-80k:
`select * from emp where salary between 60000 and 80000;`
- Display the highest and lowest salary values:
`select max(salary), min(salary) from emp;`
- Display average salary from emp table:
`select avg(salary) from emp;`
- Display ename and dname from dept and emp:
`select ename,dname from dept,emp`
`where dept.dn[o](http://dept.no) = emp.dno`
- Display dept wise total salary paid:
`select dname, sum(esal) from dept, emp where`
`dept.dno=emp.dno group by dname;`
- Display all employees from computer department:
`select ename from dept, emp where dept.dno=emp.dno and dname=’computer’;`
- Display dept wise total number of employees:
`select count(dno) from dept, emp where dept.dno=emp.dno group by dept.no;`
- Display the name of the department which are having more than 2 employees:
`select dname,count(*) as cnt from dept,emp
where dept.en[o](http://dept.no) = emp.no
group by dname
having cnt>2;`