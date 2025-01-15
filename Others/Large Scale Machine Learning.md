---
Subject: "[[Indice - Machine Learning|ML]]"
tags:
  - ML
  - IR
Creation: 2024-12-19
---
## Data stream injection
---
-  Clickstream
- Change data capture
- Live video

## Click stream
---
***Click streams*** are data from the user during the experience with the interface.
Data are in the form 
```json
{DataTime}, {UserAngent}, {ID}, {Request}, {SessionID}, {IPAgent}
```

There are tools such as *Kafka* and *Kinesis* to manege these types of data.
- Kafka uses Brokers which riceve data from the producer and store data to the consumer. 
- Kinesis use Shards instead of brokers but they works in the same way.

Either brokers and shards scale-up with the number of clickstream logs, or any stream data type logs. For Brokers there is one which is the leader of each broker.

## Data storage
---
To have better performances we can use [[parallel]] storage that help to reduce time access and increase fault tollerance for the presence of copies of data.

It use a ***Hadoop Distributed File system***,