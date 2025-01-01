# Database author and book

Status: Completed
Date: December 19, 2024

### **How to run Hadoop**

- open cmd as administrator and enter the following commands
    - `start-all`
    - `jps`
    - `StartNetworkServer -h 0.0.0.0`
- open another cmd as administrator
    - go to the hive/bin directory type `hive` to open the hive interpreter.

CTRL+L to clear screen

**Author:**

11,Ivan Bayross
12,Kanitkar
13,David Thomas
14,Robert
15,James
16,Soumya

**Book:**

1001,Programming in C,240,12
1002,Mastering in C++,400,11
1003,Basics of Java,200,11
1004,Java Complete Reference,500,13
1005,Whole DBMS,600,11
1006,Mastering in PHP,450,12
1007,Basics of Big Data,400,
1008,Learning Web Technologies,340,

- create the db

`hive> set hive.auto.convert.join=false;`: fire this statement before using join function.

`select aname,bname from author left join book on author.ano=book.ano;`

```
#Output
Ivan Bayross    Whole DBMS
Ivan Bayross    Basics of Java
Ivan Bayross    Mastering in C++
Kanitkar        Mastering in PHP
Kanitkar        Programming in C
David Thomas    Java Complete Reference
Robert  NULL
James   NULL
Soumya  NULL
```

**Display author-wise total sum of the books:**

**Union:** 

`hive> select aname,bname from author left join book on author.ano=book.ano union
> select aname,bname from author right join book on author.ano=book.ano;`

```
#output
NULL    Basics of Big Data
NULL    Learning Web Technologies
David Thomas    Java Complete Reference
Ivan Bayross    Basics of Java
Ivan Bayross    Mastering in C++
Ivan Bayross    Whole DBMS
James   NULL
Kanitkar        Mastering in PHP
Kanitkar        Programming in C
Robert  NULL
Soumya  NULL
```