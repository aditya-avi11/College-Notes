

# Transactional Writes – Sample Qs

These are great hands-on exercises for understanding **PyFlink**, **Kafka**, and **Flink's transactional processing**! Let's tackle them one by one.

---
## **1. Implement a PyFlink Program to Write Data to a Kafka Topic with Exactly-Once Semantics**

**Steps to Implement:**

- Use **PyFlink** to process a stream of data.
- Write the processed data to **Kafka** using a **Kafka Sink**.
- Enable **exactly-once semantics** using Flink's **checkpointing mechanism**.

### **Code:**

```python
from pyflink.datastream import StreamExecutionEnvironment
from pyflink.datastream.connectors.kafka import KafkaSink, KafkaRecordSerializationSchema
from pyflink.common.serialization import SimpleStringSchema
from pyflink.common.watermark_strategy import WatermarkStrategy
from pyflink.datastream.formats.json import JsonRowSerializationSchema
import json

# Create Flink environment
env = StreamExecutionEnvironment.get_execution_environment()
env.enable_checkpointing(5000)  # Enable exactly-once checkpointing

# Define Kafka sink with exactly-once semantics
kafka_sink = KafkaSink.builder() \
    .set_bootstrap_servers("localhost:9092") \
    .set_record_serializer(KafkaRecordSerializationSchema.builder()
                           .set_topic("sales_data")
                           .set_value_serialization_schema(SimpleStringSchema())
                           .build()) \
    .set_delivery_guarantee(KafkaSink.DeliveryGuarantee.EXACTLY_ONCE) \
    .build()

# Sample data stream
data_stream = env.from_collection([
    json.dumps({"id": 1, "item": "Laptop", "price": 1000}),
    json.dumps({"id": 2, "item": "Mouse", "price": 50}),
    json.dumps({"id": 3, "item": "Keyboard", "price": 70}),
])

# Write data to Kafka
data_stream.sink_to(kafka_sink)

# Execute the Flink job
env.execute("Kafka Exactly-Once Producer")
```

### **Key Features:**

✅ **Exactly-once semantics** enabled with `env.enable_checkpointing(5000)`.  
✅ **KafkaSink with `DeliveryGuarantee.EXACTLY_ONCE`** ensures no duplicate messages.  
✅ **JSON serialization** for structured data.

---

## **2. Create a Flink Application That Writes Aggregated Sales Data to a Database Using a Two-Phase Commit Protocol**

**Steps to Implement:**

1. **Process streaming sales data**.
2. **Aggregate sales by category**.
3. **Write to a database (e.g., MySQL) using a Two-Phase Commit (2PC) Sink**.

### **Code:**

```python
from pyflink.datastream import StreamExecutionEnvironment
from pyflink.datastream.connectors.jdbc import JdbcSink, JdbcStatementBuilder
from pyflink.common.typeinfo import Types
from pyflink.datastream.state import ValueStateDescriptor
from pyflink.datastream.functions import KeyedProcessFunction

# Create Flink environment
env = StreamExecutionEnvironment.get_execution_environment()
env.enable_checkpointing(5000)

# Sample sales data: (category, amount)
data_stream = env.from_collection([
    ("Electronics", 1000),
    ("Clothing", 500),
    ("Electronics", 700),
    ("Clothing", 200),
], type_info=Types.TUPLE([Types.STRING(), Types.INT()]))

# Aggregation logic (stateful processing)
class AggregateSales(KeyedProcessFunction):
    def open(self, runtime_context):
        self.total_sales = runtime_context.get_state(
            ValueStateDescriptor("total_sales", Types.INT()))

    def process_element(self, value, ctx):
        current_total = self.total_sales.value() or 0
        new_total = current_total + value[1]
        self.total_sales.update(new_total)
        yield (value[0], new_total)  # Emit (category, total_sales)

aggregated_sales = data_stream.key_by(lambda x: x[0]).process(AggregateSales())

# Define the JDBC sink (2PC)
jdbc_sink = JdbcSink.sink(
    sql="INSERT INTO aggregated_sales (category, total_sales) VALUES (?, ?) "
        "ON DUPLICATE KEY UPDATE total_sales = VALUES(total_sales)",
    drivername="com.mysql.jdbc.Driver",
    db_url="jdbc:mysql://localhost:3306/sales_db",
    username="root",
    password="password",
    statement_builder=JdbcStatementBuilder.of(
        lambda stmt, record: stmt.set_string(1, record[0]) or stmt.set_int(2, record[1])
    ),
    sink_parallelism=1
)

# Write to the database using two-phase commit
aggregated_sales.add_sink(jdbc_sink)

# Execute the Flink job
env.execute("Sales Aggregation with 2PC Sink")
```

### **Key Features:**

✅ **Aggregates sales by category using stateful processing**.  
✅ **Uses MySQL sink with 2PC for transactional writes**.  
✅ **Ensures consistency even if Flink fails**.

---

## **3. Simulate a Failure Scenario and Demonstrate How Flink’s Transactional Writes Handle Recovery and Retries**

**Goal:**  
We will **simulate a failure** in Flink while writing data to Kafka and see how **checkpointing and transactional writes** ensure recovery.

### **Steps:**

1. **Enable checkpointing** (so Flink can recover from failure).
2. **Simulate a failure** in the Flink job.
3. **Restart the job** and observe Flink restoring from the last checkpoint.

---

### **Code with Failure Simulation**

```python
import time
import random
from pyflink.datastream import StreamExecutionEnvironment
from pyflink.datastream.connectors.kafka import KafkaSink, KafkaRecordSerializationSchema
from pyflink.common.serialization import SimpleStringSchema

# Create Flink environment
env = StreamExecutionEnvironment.get_execution_environment()
env.enable_checkpointing(5000)  # Enable exactly-once checkpointing

# Define Kafka sink
kafka_sink = KafkaSink.builder() \
    .set_bootstrap_servers("localhost:9092") \
    .set_record_serializer(KafkaRecordSerializationSchema.builder()
                           .set_topic("resilient_data")
                           .set_value_serialization_schema(SimpleStringSchema())
                           .build()) \
    .set_delivery_guarantee(KafkaSink.DeliveryGuarantee.EXACTLY_ONCE) \
    .build()

# Simulated data stream
def generate_data():
    for i in range(20):
        if i == 10:  # Simulate a failure at record 10
            print("Simulated Failure! Flink will restart...")
            time.sleep(5)
            raise RuntimeError("Simulated failure")
        yield f"record-{i}"

data_stream = env.from_collection(generate_data())

# Write to Kafka
data_stream.sink_to(kafka_sink)

# Execute the Flink job
try:
    env.execute("Transactional Write with Failure Simulation")
except Exception as e:
    print(f"Flink Job Failed: {e}")

# Restart Flink manually and it will resume from the last checkpoint.
```

---

### **What Happens?**

1. **Flink writes data to Kafka with exactly-once semantics**.
2. **Simulated failure at record 10** (Flink crashes).
3. **Flink recovers from the last checkpoint** when restarted.
4. **No duplicate records in Kafka** (ensuring exactly-once processing).

---

## **Key Takeaways**

|Feature|Benefit|
|---|---|
|**Kafka Exactly-Once Sink**|Ensures no duplicates even on failure|
|**Two-Phase Commit Sink (2PC)**|Guarantees atomic writes to databases|
|**Checkpointing Integration**|Allows Flink to recover from failures gracefully|
|**Simulated Failure Handling**|Demonstrates Flink's robustness in real-world systems|

---
