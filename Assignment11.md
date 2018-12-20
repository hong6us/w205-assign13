## 1. Copy the docker-compose file and the python files into the directory ~/w205/spark-from-files/.  
####   mkdir ~/w205/spark-from-files/
####   cd ~/w205/spark-from-files
####   cp ~/w205/course-content/11-Storing-Data-III/docker-compose.yml .
####   cp ~/w205/course-content/11-Storing-Data-III/*.py .

## 2. Spin up the docker container
#### docker-compose up -d

## 3. Verify the log Cloudera log file
#### docker-compose logs -f cloudera

## 4. Verify the files in Hadoop
#### docker-compose exec cloudera hadoop fs -ls /tmp/

## 5. Create the event using kafka 
#### docker-compose exec kafka kafka-topics --create --topic events --partitions 1 --replication-factor 1 --if-not-exists --zookeeper zookeeper:32181

## 6. Run flask.  Not adding thing at this point, this is the same as last week.
#### docker-compose exec mids env FLASK_APP=/w205/spark-from-files/game_api.py flask run --host 0.0.0.0

## 7. Open another SSH session to make the call to the API.   This calls the api and register the api hits, and return the string "This is the default response!" and "sword purchased"
#### localhost:5000/
#### localhost:5000/purchase_a_sword

## 8. Read the data from kafka
#### docker-compose exec mids kafkacat -C -b kafka:29092 -t events -o beginning -e
#### Geting the event in Kafka, each event is the json dictionary, which has the event type.  The request line in python file returns the additional fields such as User-Agent is the kind of device to use for connect to web service, which is the cul command.
```
{"Host": "localhost:5000", "event_type": "default", "Accept": "*/*", "User-Agent": "curl/7.47.0"}
{"Host": "localhost:5000", "event_type": "default", "Accept": "*/*", "User-Agent": "curl/7.47.0"}
{"Host": "localhost:5000", "event_type": "default", "Accept": "*/*", "User-Agent": "curl/7.47.0"}
{"Host": "localhost:5000", "event_type": "purchase_sword", "Accept": "*/*", "User-Agent": "curl/7.47.0"}
{"Host": "localhost:5000", "event_type": "purchase_sword", "Accept": "*/*", "User-Agent": "curl/7.47.0"}
{"Host": "localhost:5000", "event_type": "purchase_sword", "Accept": "*/*", "User-Agent": "curl/7.47.0"}
{"Host": "localhost:5000", "event_type": "purchase_sword", "Accept": "*/*", "User-Agent": "curl/7.47.0"}
...
```
## 9. Run pyspark, add printSchema() and show() to show data
#### docker-compose exec spark spark-submit /w205/spark-from-files/extract_events.py

## 10. Check results in Hadoop
#### docker-compose exec cloudera hadoop fs -ls /tmp/

## 11. Deploy Spark file to the cluster
#### docker-compose exec spark spark-submit /w205/spark-from-files/extract_events.py

## 12. Exit spark, spin down the container
#### docker-compose down
