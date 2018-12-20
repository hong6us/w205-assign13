

## 1. Copy the docker-compose file and the python files into the directory ~/w205/full-stack2
```
mkdir ~/w205/full-stack2/
cd ~/w205/full-stack2
cp ~/w205/course-content/13-Understanding-Data/docker-compose.yml .
```

## 2. Spin up the docker container
```
docker-compose up -d
```

## 3. Rnning flask
```
docker-compose exec mids env FLASK_APP=/w205/full-stack/game_api.py flask run --host 0.0.0.0
```

## 4. Open another SSH session to make the call to the API.   This calls the api and register the api hits, generate the data.
```
science@w205s4-martin-14:~/w205/full-stack2$ docker-compose exec mids \
>   ab \
>     -n 10 \
>     -H "Host: user1.comcast.com" \
>     http://localhost:5000/
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient).....done


Server Software:        Werkzeug/0.14.1
Server Hostname:        localhost
Server Port:            5000

Document Path:          /
Document Length:        30 bytes

Concurrency Level:      1
Time taken for tests:   0.053 seconds
Complete requests:      10
Failed requests:        0
Total transferred:      1850 bytes
HTML transferred:       300 bytes
Requests per second:    188.43 [#/sec] (mean)
Time per request:       5.307 [ms] (mean)
Time per request:       5.307 [ms] (mean, across all concurrent requests)
Transfer rate:          34.04 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.2      0       1
Processing:     2    5   3.3      4      10
Waiting:        1    4   3.0      2       9
Total:          2    5   3.4      4      10

Percentage of the requests served within a certain time (ms)
  50%      4
  66%      8
  75%      9
  80%     10
  90%     10
  95%     10
  98%     10
  99%     10
 100%     10 (longest request)
``` 
 
```

science@w205s4-martin-14:~/w205/full-stack2$ docker-compose exec mids \
>   env FLASK_APP=/w205/full-stack2/game_api.py \
>   flask run --host 0.0.0.0
 * Serving Flask app "game_api"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)

127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:33:02] "GET / HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 19:34:42] "GET /purchase_a_sword HTTP/1.0" 200 -

```
```
science@w205s4-martin-14:~/w205/full-stack2$ docker-compose exec mids \
>   ab \
>     -n 10 \
>     -H "Host: user1.comcast.com" \
>     http://localhost:5000/purchase_a_sword
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient).....done


Server Software:        Werkzeug/0.14.1
Server Hostname:        localhost
Server Port:            5000

Document Path:          /purchase_a_sword
Document Length:        17 bytes

Concurrency Level:      1
Time taken for tests:   0.042 seconds
Complete requests:      10
Failed requests:        0
Total transferred:      1720 bytes
HTML transferred:       170 bytes
Requests per second:    235.87 [#/sec] (mean)
Time per request:       4.240 [ms] (mean)
Time per request:       4.240 [ms] (mean, across all concurrent requests)
Transfer rate:          39.62 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       0
Processing:     2    4   1.6      4       7
Waiting:        0    2   1.8      2       6
Total:          2    4   1.6      4       7

Percentage of the requests served within a certain time (ms)
  50%      4
  66%      5
  75%      6
  80%      6
  90%      7
  95%      7
  98%      7
  99%      7
 100%      7 (longest request)
```
## 5. Run filtered_writes.py.  Run through kafka config.  Create the table.
```
docker-compose exec spark spark-submit /w205/full-stack2/filtered_writes.py
```

```
ause of KAFKA-1894
18/12/18 19:36:28 INFO PythonRunner: Times: total = 44, boot = -394, init = 438, finish = 0
18/12/18 19:36:28 INFO CodeGenerator: Code generated in 12.905997 ms
18/12/18 19:36:28 INFO PythonRunner: Times: total = 12, boot = 4, init = 7, finish = 1
18/12/18 19:36:28 INFO Executor: Finished task 0.0 in stage 1.0 (TID 1). 2083 bytes result sent to driver
18/12/18 19:36:28 INFO TaskSetManager: Finished task 0.0 in stage 1.0 (TID 1) in 214 ms on localhost (executor driver) (1/1)
18/12/18 19:36:28 INFO TaskSchedulerImpl: Removed TaskSet 1.0, whose tasks have all completed, from pool
18/12/18 19:36:28 INFO DAGScheduler: ResultStage 1 (showString at NativeMethodAccessorImpl.java:0) finished in 0.216 s
18/12/18 19:36:28 INFO DAGScheduler: Job 1 finished: showString at NativeMethodAccessorImpl.java:0, took 0.239030 s
18/12/18 19:36:28 INFO CodeGenerator: Code generated in 35.498394 ms
+------+-----------------+---------------+--------------+--------------------+
|Accept|             Host|     User-Agent|    event_type|           timestamp|
+------+-----------------+---------------+--------------+--------------------+
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
+------+-----------------+---------------+--------------+--------------------+

```
## 6. See purchase file in HDFS
```
docker-compose exec cloudera hadoop fs -ls /tmp/purchases/
```
```
science@w205s4-martin-14:~/w205/full-stack2$ docker-compose exec cloudera hadoop fs -ls /tmp/purchases/
Found 2 items
-rw-r--r--   1 root supergroup          0 2018-12-18 19:36 /tmp/purchases/_SUCCESS
-rw-r--r--   1 root supergroup       1567 2018-12-18 19:36 /tmp/purchases/part-00000-c8a58a43-1ae9-4426-a3a1-f38e96a93b68-c000.snappy.parquet

```

## 7. Run write_hive_table.py.  Create the table.
```
docker-compose exec spark spark-submit /w205/full-stack2/write_hive_table.py
```
```
18/12/18 20:05:06 INFO CodeGenerator: Code generated in 16.980688 ms
+------+-----------------+---------------+--------------+--------------------+
|Accept|             Host|     User-Agent|    event_type|           timestamp|
+------+-----------------+---------------+--------------+--------------------+
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
|   */*|user1.comcast.com|ApacheBench/2.3|purchase_sword|2018-12-18 19:34:...|
+------+-----------------+---------------+--------------+--------------------+
```

## 8. Write to HDFS and validate the files
```
docker-compose exec cloudera hadoop fs -ls /tmp/
```
```

science@w205s4-martin-14:~/w205/full-stack2$ docker-compose exec cloudera hadoop fs -ls /tmp/
Found 4 items
drwxrwxrwt   - mapred mapred              0 2016-04-06 02:26 /tmp/hadoop-yarn
drwx-wx-wx   - hive   supergroup          0 2018-12-18 20:02 /tmp/hive
drwxrwxrwt   - mapred hadoop              0 2016-04-06 02:28 /tmp/logs
drwxr-xr-x   - root   supergroup          0 2018-12-18 20:05 /tmp/purchases

```

## 9. Query the tables in Presto
```
docker-compose exec presto presto --server presto:8080 --catalog hive --schema default
```
```
science@w205s4-martin-14:~/w205/full-stack2$ docker-compose exec presto presto --server presto:8080 --catalog hive --schema default
presto:default> show tables;
   Table
------------
 purchases
 purchases2
(2 rows)

Query 20181218_201200_00002_f3db8, FINISHED, 1 node
Splits: 2 total, 0 done (0.00%)
0:00 [0 rows, 0B] [0 rows/s, 0B/s]

presto:default> describe purchases;
   Column   |  Type   | Comment
------------+---------+---------
 accept     | varchar |
 host       | varchar |
 user-agent | varchar |
 event_type | varchar |
 timestamp  | varchar |
(5 rows)

Query 20181218_201226_00003_f3db8, FINISHED, 1 node
Splits: 2 total, 0 done (0.00%)
0:01 [0 rows, 0B] [0 rows/s, 0B/s]

presto:default> select * from purchases;
 accept |       host        |   user-agent    |   event_type   |        timestamp
--------+-------------------+-----------------+----------------+-------------------------
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.334
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.341
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.347
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.354
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.357
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.361
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.364
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.367
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.371
 */*    | user1.comcast.com | ApacheBench/2.3 | purchase_sword | 2018-12-18 19:34:42.374
(10 rows)

Query 20181218_201246_00004_f3db8, FINISHED, 1 node
Splits: 2 total, 1 done (50.00%)
0:02 [0 rows, 0B] [0 rows/s, 0B/s]

```
## 10. Run streaming
```
docker-compose exec spark spark-submit /w205/full-stack2/filter_swords_stream.py
```
```
science@w205s4-martin-14:~/w205/full-stack2$ docker-compose exec spark spark-submit /w205/full-stack2/write_swords_stream.py
Using Spark's default log4j profile: org/apache/spark/log4j-defaults.properties
18/12/18 20:22:46 INFO SparkContext: Running Spark version 2.2.0
18/12/18 20:22:46 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
18/12/18 20:22:47 INFO SparkContext: Submitted application: ExtractEventsJob
18/12/18 20:22:47 INFO SecurityManager: Changing view acls to: root
18/12/18 20:22:47 INFO SecurityManager: Changing modify acls to: root
18/12/18 20:22:47 INFO SecurityManager: Changing view acls groups to:
18/12/18 20:22:47 INFO SecurityManager: Changing modify acls groups to:

```

## 11. Generate more data
```
science@w205s4-martin-14:~/w205/full-stack2$ while true; do
>   docker-compose exec mids \
>     ab -n 10 -H "Host: user1.comcast.com" \
>       http://localhost:5000/purchase_a_sword
>   sleep 10
> done
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient).....done


Server Software:        Werkzeug/0.14.1
Server Hostname:        localhost
Server Port:            5000

Document Path:          /purchase_a_sword
Document Length:        17 bytes

Concurrency Level:      1
Time taken for tests:   0.047 seconds
Complete requests:      10
Failed requests:        0
Total transferred:      1720 bytes
HTML transferred:       170 bytes
Requests per second:    211.66 [#/sec] (mean)
Time per request:       4.725 [ms] (mean)
Time per request:       4.725 [ms] (mean, across all concurrent requests)
Transfer rate:          35.55 [Kbytes/sec] received

```
```
127.0.0.1 - - [18/Dec/2018 20:20:45] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:20:45] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:20:45] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:20:45] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:20:45] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:20:45] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:20:45] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:20:45] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:20:45] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:44] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:24:55] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:25:05] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:25:05] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:25:05] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:25:05] "GET /purchase_a_sword HTTP/1.0" 200 -
127.0.0.1 - - [18/Dec/2018 20:25:05] "GET /purchase_a_sword HTTP/1.0" 200
```
## 12. Feed
```
18/12/18 20:24:38 INFO ShutdownHookManager: Deleting directory /tmp/spark-1b995c0b-8acc-40e4-b828-dd2e565a9b30/pyspark-fdd9b482-6d72-4137-bc4c-581c8e5e4327
science@w205s4-martin-14:~/w205/full-stack2$ while true; do
>   docker-compose exec mids \
>     ab -n 10 -H "Host: user1.comcast.com" \
>       http://localhost:5000/purchase_a_sword
>   sleep 10
> done
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient).....done


Server Software:        Werkzeug/0.14.1
Server Hostname:        localhost
Server Port:            5000

Document Path:          /purchase_a_sword
Document Length:        17 bytes

Concurrency Level:      1
Time taken for tests:   0.047 seconds
Complete requests:      10
Failed requests:        0
Total transferred:      1720 bytes
HTML transferred:       170 bytes
Requests per second:    211.66 [#/sec] (mean)
Time per request:       4.725 [ms] (mean)
Time per request:       4.725 [ms] (mean, across all concurrent requests)
Transfer rate:          35.55 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.6      0       2
Processing:     1    4   5.6      3      20
Waiting:        1    3   5.5      1      19
Total:          1    5   5.7      3      20

Percentage of the requests served within a certain time (ms)
  50%      3
  66%      3
  75%      5
  80%      5
  90%     20
  95%     20

```
## 13. Check the files in Hadoop
```
science@w205s4-martin-14:~/w205/full-stack2$ docker-compose exec cloudera hadoop fs -ls /tmp/sword_purchases
Found 2 items
drwxr-xr-x   - root supergroup          0 2018-12-18 20:22 /tmp/sword_purchases/_spark_metadata
-rw-r--r--   1 root supergroup        688 2018-12-18 20:22 /tmp/sword_purchases/part-00000-48f37b4c-1f53-40da-8f6d-beb4fec23476-c000.snappy.parquet

```
## 14. Spin down
```
docker-compose down
```
