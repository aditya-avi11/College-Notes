
Fetchin data from Weather API.
## COMMANDS TO TYPE IN TERMINALS :

1st :
./bin/zookeeper-server-start.sh config/zookeeper.properties

2nd:
./bin/kafka-server-start.sh config/server.properties

3rd :
./bin/kafka-topics.sh --create --topic input --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
./bin/kafka-topics.sh --create --topic output --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1

4th :
gedit ***api_to_kafka.py*** (type the below code in it)
then, python3 api_to_kafka.py

```python
import requests
from kafka import KafkaProducer
import json
import time

API_KEY = "7E807B56CA1F4C08999100307243112"
BASE_URL = 'http://api.weatherapi.com/v1/current.json'
LOCATION = 'Bangalore'

def fetch_weather():
	params = {'key' : API_KEY, 'q': LOCATION}
	response = requests.get(BASE_URL, params=params)
	if response.status_code == 200:
		return response.json()
	else:
		print(f'Failed to fetch weather data : {respinse.status_code}')
		return None
		
producer = KafkaProducer(bootstrap_servers = 'localhost:9092', value_serializer=lambda v : json.dumps(v).encode('utf-8'))

while True:
	weather_data = fetch_weather()
	if weather_data:
		print(f'Producing weather data : {weather_data}')
		producer.send('input', value=weather_data)
	time.sleep(5)
```

5th :
gedit ***flink-job.py*** (type the below code in it)
python3 flink-job.py 

```python
from pyflink.datastream import StreamExecutionEnvironment as SEE
from pyflink.datastream.connectors.kafka import FlinkKafkaConsumer, FlinkKafkaProducer
from pyflink.common.serialization import SimpleStringSchema
import json

env = SEE.get_execution_environment()
env.add_jars('file:///home/hadoop/kafka-3.9.0-src/jars/flink-sql-connector-kafka-1.15.0.jar')

consumer = FlinkKafkaConsumer(topics="input", deserialization_schema=SimpleStringSchema(), properties={'bootstrap.servers':'localhost:9092', 'group.id':'flink-consumer-group'})

data_stream = env.add_source(consumer)
processed_stream = data_stream  #.map(process)
processed_stream.print('Processed')
producer = FlinkKafkaProducer(topic='output', serialization_schema=SimpleStringSchema(), producer_config={'bootstrap.servers':'localhost:9092'})

processed_stream.add_sink(producer)
env.execute()
```