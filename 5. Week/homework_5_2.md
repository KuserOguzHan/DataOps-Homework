 # 1 Veri İndirme
 ```
 ! wget -P /home/train/datasets/  https://github.com/erkansirin78/datasets/raw/master/IOT-temp.csv.zip
 ```
 
 # 2. Aktif Etme
 ```
 [train@localhost ~]$ cd data-generator/
 
 [train@localhost data-generator]$ source datagen/bin/activate
 ```
 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
# 3. Dosya Oluştıurma Schema İçin
```
[train@localhost data-generator]$ mkdir /tmp/iot_telemetry-schema
```
 
```
python dataframe_to_log.py -i https://github.com/erkansirin78/datasets/raw/master/iot_telemetry_data.csv.zip -o /tmp/iot_telemetry-schema -oh True
```



-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# 4. Dosya Oluştıurma Input için 

``` 
(datagen) [train@trainvm data-generator]$ mkdir /tmp/iot_telemetry-input 
``` 
``` 
python dataframe_to_log.py -i https://github.com/erkansirin78/datasets/raw/master/iot_telemetry_data.csv.zip -o /tmp/iot_telemetry-input -shf True
``` 
 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 5. Temizlik komutları

``` 
(datagen) [train@trainvm data-generator]$ rm -rf /tmp/streaming/week5_2_check/*
``` 
 
``` 
(datagen) [train@trainvm data-generator]$ rm -rf /tmp/iot_telemetry-input/*
``` 
 
``` 
(datagen) [train@trainvm data-generator]$ rm -rf /tmp/iot_telemetry-output/*
```


```
from pyspark.sql import SparkSession, functions as F
from pyspark.sql.functions import window, avg, count, col, to_timestamp

spark = SparkSession.builder.appName("homework5_2").getOrCreate()

# prevent to error
spark.sparkContext.setLogLevel('ERROR')


# We must give schema to read
df = spark.read.format("csv") \
    .option("header", True) \
    .option("sep", ",") \
    .option("inferSchema", True) \
    .load("file:///tmp/iot_telemetry-schema") \
    .withColumn("event_time", F.to_timestamp(F.col("event_time"), "y-M-d h:m:s. SSSSSS"))

stream_schema = df.schema
df.printSchema()



# Read from source
line = spark.readStream.format("csv") \
            .schema(stream_schema) \
            .load("file:///tmp/iot_telemetry-input")



line2 = line\
    .groupBy(window(col("event_time"), "10 minutes", "5 minutes"), "device")\
    .agg(count("*").alias("signal_count"), avg("co").alias("avg_co"), avg("humidity").alias("avg.humidity"))\
    .orderBy("device")






checkpointDir = "file:///tmp/streaming/week5_2_check"


streamingQuery = (line2.writeStream
                  .format("console")
                  .outputMode("complete")
                  .trigger(processingTime="1 second")
                  .option("numRows", 10)
                  .option("truncate", False)
                  .option("checkpointLocation", checkpointDir)
                  .start())


streamingQuery.awaitTermination()
```












```
-------------------------------------------
Batch: 6
-------------------------------------------
+------------------------------------------+-----------------+------------+---------------------+-----------------+
|window                                    |device           |signal_count|avg_co               |avg.humidity     |
+------------------------------------------+-----------------+------------+---------------------+-----------------+
|{2023-04-10 11:50:00, 2023-04-10 12:00:00}|00:0f:00:70:91:0a|44          |0.0035794761033698867|75.24090940302068|
|{2023-04-10 11:50:00, 2023-04-10 12:00:00}|1c:bf:ce:15:ec:4d|57          |0.0042269459313427305|61.24561390123869|
|{2023-04-10 11:50:00, 2023-04-10 12:00:00}|b8:27:eb:bf:9d:51|69          |0.005625910672311013 |50.55507246376812|
+------------------------------------------+-----------------+------------+---------------------+-----------------+
```






