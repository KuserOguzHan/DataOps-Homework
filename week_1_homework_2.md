## 1. Create a table that suits data in hdfs. To learn what to create, better to see data first
```
hdfs dfs -head  /user/train/hdfs_odev/Wine.csv
```
## 2. Create table.
```
[train@localhost ~]$ beeline -u jdbc:hive2://localhost:10000
```

# create table
```
create table if not exists wine
(Alcohol float, Malic_Acid float, Ash float, Ash_Alcanity float, Magnesium float, Total_Phenols float, Flavanoids float, Nonflavanoid_Phenols float, Proanthocyanins float, Color_Intensity float, Hue float, OD280 float, Proline float, Customer_Segment int)
row format delimited
fields terminated by ','
lines terminated by '\n'
tblproperties('skip.header.line.count'='1');
```
# Show table
```
show tables;
```

# Describe table
```
describe wine;
```

## 2. Load data to hive table
```
load data inpath '/user/train/hdfs_odev/Wine.csv' into table wine;
```
# Show
```
select * from wine limit 10;
```






