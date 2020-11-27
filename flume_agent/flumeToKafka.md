```
flume to kafka
```
```
[hadoop@hadoop001 bin]$ cat /home/hadoop/app/apache-flume-1.6.0-cdh5.7.0-bin/conf/kafka.conf 
# Name the components on this agent
a1.sources = r1
a1.sinks = k1
a1.channels = c1

# Describe/configure the source
a1.sources.r1.type = TAILDIR
a1.sources.r1.filegroups = f1
a1.sources.r1.filegroups.f1 = /home/hadoop/data/flume/.*txt
a1.sources.r1.positionFile = /home/hadoop/app/apache-flume-1.6.0-cdh5.7.0-bin/bin/tail_dir.json

# Describe the sink
a1.sinks.k1.type = org.apache.flume.sink.kafka.KafkaSink
a1.sinks.k1.topic = flume_data
a1.sinks.k1.brokerList = hadoop001:9092,hadoop002:9092,hadoop003:9092
a1.sinks.k1.batchSize = 20

# Use a channel which buffers events in memory
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

# Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sinks.k1.channel = c1

```