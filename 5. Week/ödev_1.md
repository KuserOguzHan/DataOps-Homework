 # 1 Veri İndirme
 ```
 ! wget -P /home/train/datasets/  https://github.com/erkansirin78/datasets/raw/master/IOT-temp.csv.zip
 ```
 
 # 2. Aktif Etme
 ```
 [train@localhost ~]$ cd data-generator/
 
 [train@localhost data-generator]$ source datagen/bin/activate
 ```
 
 -------------------------------------------------------------------------------------------------------------------------------
 
 # 3. Dosya Oluştıurma Schema İçin
 ```
 [train@localhost data-generator]$ mkdir /tmp/iot-temp-input
 ```
 
```
python dataframe_to_log.py -i https://github.com/erkansirin78/datasets/raw/master/IOT-temp.csv.zip -o /tmp/iot-temp-input -shf True
```
 
 
 -------------------------------------------------------------------------------------------------------------------------------

# 4. Dosya Oluştıurma Input için 

``` 
(datagen) [train@trainvm data-generator]$ mkdir /tmp/iot-temp-input_schema
``` 
``` 
python dataframe_to_log.py -i https://github.com/erkansirin78/datasets/raw/master/IOT-temp.csv.zip -o /tmp/iot-temp-input_schema -oh True
``` 
 
 
-------------------------------------------------------------------------------------------------------------------------------

# 5. Temizlik komutları

``` 
(datagen) [train@trainvm data-generator]$ rm -rf /tmp/streaming/week5_1_check/*
``` 
 
``` 
(datagen) [train@trainvm data-generator]$ rm -rf tmp/iot-temp-input/*
``` 
 
``` 
(datagen) [train@trainvm data-generator]$ rm -rf tmp/iot-temp-output/*
```


 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
