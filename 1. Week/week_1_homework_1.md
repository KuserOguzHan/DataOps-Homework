## Questions

- Download and put `https://raw.githubusercontent.com/erkansirin78/datasets/master/Wine.csv` dataset in hdfs `/user/train/hdfs_odev` directory.

- Copy this hdfs file `/user/train/hdfs_odev/Wine.csv` to `/tmp/hdfs_odev` hdfs directory.

- Delete `/tmp/hdfs_odev` directory with skipping the trash. 

- Explore `/user/train/hdfs_odev/Wine.csv` file from web hdfs.  
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Answers

### 0. Start Hadoop services

[train@localhost play]$ 
```
start-all.sh
```

### 1. Check to files

[train@localhost play]$
```
hdfs dfs -ls /
```
```
hdfs dfs -ls /user
```
```
hdfs dfs -ls /user/train
```

### 2. Create new file

[train@localhost play]$
```
hdfs dfs -mkdir /user/train/hdfs_odev
```

#### Check the file
```
hdfs dfs -ls /user/train/
```

### 3. Download DataSets in local

[train@localhost play]$
```
wget https://raw.githubusercontent.com/erkansirin78/datasets/master/Wine.csv -O ~/datasets/Wine.csv
```

#### Check DataSets
```
ls -l ~/datasets/
```

### 4. Put DataSets from local to hdfs
[train@localhost play]$
```
hdfs dfs -put ~/datasets/Wine.csv /user/train/hdfs_odev
```

#### Check the dataset
```
hdfs dfs -ls  /user/train/hdfs_odev/Wine.csv
```

### 5. Look at the datasets

[train@localhost play]$
```
hdfs dfs -head  /user/train/hdfs_odev/Wine.csv
```

### 6. Create new file in temp

```
hdfs dfs -mkdir /tmp/hdfs_odev
```

### 7. Copies /user/train/hdfs_odev/Wine.csv` to `/tmp/hdfs_odev

[train@localhost play]$
```
hdfs dfs -cp /user/train/hdfs_odev/Wine.csv /tmp/hdfs_odev/Wine.csv
```


#### Check the datasets
```
hdfs dfs -ls /tmp/hdfs_odev/
```


### 8. Delete the datasets

[train@localhost play]$
```
hdfs dfs -rm /tmp/hdfs_odev/Wine.csv
hdfs dfs -ls /tmp/
```

### 9. We have to change the chmod of the tmp to Explore `/user/train/hdfs_odev/Wine.csv` file from web hdfs.

[train@localhost play]$
```
hdfs dfs -chmod 777 /tmp
```
http://127.0.0.1:9870/explorer.html#/ in Linux
