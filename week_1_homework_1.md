## 0. Check to files

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

## 1. Create new file

[train@localhost play]$
```
hdfs dfs -mkdir /user/train/hdfs_odev
```

### Check the file
```
hdfs dfs -ls /user/train/
```

## 2. Download DataSets in local

[train@localhost play]$
```
wget https://raw.githubusercontent.com/erkansirin78/datasets/master/Wine.csv -O ~/datasets/Wine.csv
```

### Check DataSets
```
ls -l ~/datasets/
```

## 3. Put DataSets from local to hdfs
[train@localhost play]$
```
hdfs dfs -put ~/datasets/Wine.csv /user/train/hdfs_odev
```

### Check the dataset

```
hdfs dfs -ls  /user/train/hdfs_odev/Wine.csv
```

## 4. Look at the datasets

[train@localhost play]$
```
hdfs dfs -head  /user/train/hdfs_odev/Wine.csv
```

## 5. Create new file in temp

```
hdfs dfs -mkdir /tmp/hdfs_odev
```

## 6. Copies /user/train/hdfs_odev/Wine.csv` to `/tmp/hdfs_odev

[train@localhost play]$
```
hdfs dfs -cp /user/train/hdfs_odev/Wine.csv /tmp/hdfs_odev/Wine.csv
```


### Check the datasets
```
hdfs dfs -ls /tmp/hdfs_odev/
```


## 7. Delete the datasets

[train@localhost play]$
```
hdfs dfs -rm /tmp/hdfs_odev
hdfs dfs -ls /tmp/
```

## 8. We have to change the chmod of the tmp to Explore `/user/train/hdfs_odev/Wine.csv` file from web hdfs.

[train@localhost play]$
```
hdfs dfs -chmod 777 /tmp
```
http://127.0.0.1:9870/explorer.html#/ in Linux
