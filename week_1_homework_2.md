## 0. Start Hadoop services

[train@localhost play]$ start-all.sh


## 1. Beeline connection  
`[train@localhost play]$ beeline -u jdbc:hive2://127.0.0.1:10000`

You should see `0: jdbc:hive2://127.0.0.1:10000>` means beeline shell is ready to use.  

Close logs  
`  0: jdbc:hive2://127.0.0.1:10000> set hive.server2.logging.operation.level=NONE;  `  


## 2. Create database named "hive_odev"
```
show databases;
```

```
create database hive_odev;
```

```
show databases;
```

```
use hive_odev;
```

### create table
```
create table if not exists wine
(Alcohol float, Malic_Acid float, Ash float, Ash_Alcanity float, Magnesium float, Total_Phenols float, Flavanoids float, Nonflavanoid_Phenols float, Proanthocyanins float, Color_Intensity float, Hue float, OD280 float, Proline float, Customer_Segment int)
row format delimited
fields terminated by ','
lines terminated by '\n'
tblproperties('skip.header.line.count'='1');
```
### Show table
```
show tables;
```

### Describe table
```
describe wine;
```

## 3. Load data to hive table
```
[train@trainvm ~]$ hdfs dfs -put ~/datasets/Wine.csv /user/train/hdfs_odev
```
```
jdbc:hive2://127.0.0.1:10000> load data inpath '/user/train/hdfs_odev/Wine.csv' into table wine;
```

## Show
```
select * from wine limit 10;
```

## 4. Create a table with a query
```
jdbc:hive2://127.0.0.1:10000> create table wine_alc_gt_13 as select * from wine where wine.alcohol > 13.00;
```

```
jdbc:hive2://127.0.0.1:10000> select count(1) from wine_alc_gt_13;
```

## 5. Drop table and dataset only one specail query
```
jdbc:hive2://127.0.0.1:10000> drop database hive_odev cascade;
```
```
jdbc:hive2://127.0.0.1:10000> show databases;
```

## 6. Dowlond DataSets
```
wget https://raw.githubusercontent.com/erkansirin78/datasets/master/hive/employee.txt -O ~/datasets/employe.csv
```

## 7. Create database
```
jdbc:hive2://127.0.0.1:10000>create database company;
```
```
show databases;
```

```
use company;
```
## 8. Create table
```
create table employee (name string,work_place array<string>,gender_age struct <gender:string,age:int>,skills_score map<string,int>)
row format delimited
fields terminated by '|'
collection items terminated by ','
map keys terminated by ':'
stored as textfile
tblproperties('skip.header.line.count'='1');
```
##Show table
```
show tables;
```
## 9. Dowland datasets
```
[train@trainvm ~]$ wget https://raw.githubusercontent.com/erkansirin78/datasets/master/hive/employee.txt -O ~/datasets/employee.txt
```
## Check DataSets
```
ls -l ~/datasets/
```

## 10. Send with put

```
[train@trainvm ~]$ hdfs dfs -put ~/datasets/employee.txt /user/train/hdfs_odev
```

```
jdbc:hive2://127.0.0.1:10000> load data inpath '/user/train/hdfs_odev/employee.txt' into table employee;
```

