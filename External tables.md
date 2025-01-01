# External tables

Status: Completed
Date: December 21, 2024

- Note: Queries written in Hive are known as HQL(Hive Query language)
- Create the table in another hdfs location and not in warehouse directory.
- `hadoop fs -mkdir /tmp/ext_table`
- create data for eitems.txt inside hive directory
101,sofa,56000.0
102,TV,45000.50
103,Table,5000
104,Chair,3500
- `hadoop fs -put c:/hive2/eitems.txt /tmp/ext_table`
- type the query in hive: create external table eitems(itno int, itemname string, price float) row format delimited fields terminated by ‘,’ location ‘tmp/ext_table/’

### Partitioning in hive:

- It means dividing the table into parts based on the values of a particular column, such as date,course, etc.
- Static partitioning: required to pass the values of partitioned columns manually while loading data into the table.

**Importing CSV files:**

- `hive> create table countrydata(country string, continent string,year int, life_ex float,population float,gdppercapita float) row format delimited fields  terminated by ',';`

**Creating Static Partition table:**

- `hive> create table countrydt(country string, year int, lifeexpectancy float, population float, gdppercapita float) partitioned by (continent string) row format delimited fields terminated by ',';`
- `insert into table countrydt partition (continent=’Asia’) select country,year,life_ex,population,gdppercapita from countrydata where continent=’Asia’;`
- `hive> show partitions countrydt;`

```
#Output
OK
continent=Asia
Time taken: 0.236 seconds, Fetched: 1 row(s)
```

- `insert into table countrydt partition (continent=’Africa’) select country,year,life_ex,population,gdppercapita from countrydata where continent=’Africa’;`

```
#OUTPUT
OK
continent=Africa
continent=Asia
Time taken: 0.142 seconds, Fetched: 2 row(s)
```

To check the partition: 

- go to web and type `localhost:9870`
- go to `utilities` and under the dropdown menu click on `browse the file system`.

**Dynamic partition:**

- To enable dynamic partitioning:
`hive> set hive.exec.dynamic.partition.mode=nonstrict;`
- `hive> create table countrydetails(country string, year int, life_ex float,population float,gdppercapita float)partitioned by(continent string);`
- `hive> insert into table countrydetails partition (continent) select country,year,life_ex,population,gdppercapita from countrydata where continent='Asia';`
- `hive> select * from countrydetails;`