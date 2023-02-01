## 1. Create a table that suits data in hdfs. To learn what to create, better to see data first
```
hdfs dfs -head  /user/train/hdfs_odev/Wine.csv
```
## 2. Create table.
```
[train@localhost ~]$ beeline -u jdbc:hive2://localhost:10000
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
load data inpath '/user/train/hdfs_odev/Wine.csv' into table wine;
```
### Show
```
select * from wine limit 10;
```

### Check

```
hdfs dfs -head /user/train/hdfs_odev/Wine.csv

hdfs dfs -ls /user/hive

hdfs dfs -ls /user/hive/warehouse

hdfs dfs -ls /user/hive/warehouse/wine
```


## 4. Create a table with a query
```
create table wine_alc_gt_13 as select * from wine where wine.alcohol > 13.00;
```

```
select count(1) from wine_alc_gt_13;
```







