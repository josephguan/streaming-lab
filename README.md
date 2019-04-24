# Streaming Lab

This is my experiment lab for studying streaming frameworks, such as flink, spark-streaming, etc.
It includes some examples currently. In the near future, I will introduce more experiments...


## How To Compile

Run ```sbt assembly``` to compile, run tests and package all sub-projects.

If you want to operate specific sub-project, use ```project``` command in sbt shell to switch sub-project:
```shell
> projects          // list all sub-projects
> project examples  // switch to 'examples' sub-project
> project all       // switch to 'all' project which including all sub-projects
```


## Subprojects Overview

| subproject                          | description                                                 |
|-------------------------------------|-------------------------------------------------------------|
| [flink](./flink/README.md)          | Some examples for using flink in different ways.            |
| [kafka](./kafka/README.md)          | Some kafka producers used in flink and spark examples.      |
| [spark](./spark/README.md)          | Some examples for spark streaming and structured streaming. |


## License
This project is licensed under the terms of the Apache 2.0 license.

# SubProject: flink

This is a collection of flink example codes.

## How to use
executing the jar:
```shell
> ./flink run --class gx.flink.examples.table.Kafka09CsvTableExample flink-snippet-examples_0.0.1.jar --bootstrap.servers zdh16en:9092 --input-topic gxtest --output-topic gxtestout --zookeeper.connect zdh16en:2181/kafka --group.id gxhello --interval 5
```

monitoring print output:
```shell
> tail -f log/flink-*-taskexecutor-*.out
```

monitoring kafka output(topic):
```shell
> kafka-console-consumer --bootstrap-server zdh16en:9092 --topic gxtestout  --zookeeper zdh16en:2181/kafka
```


## Streaming Examples

#### [Kafka09StreamWordCountExample](src/main/scala/gx/flink/demo/examples/streaming/Kafka09StreamWordCountExample.scala)
A word count example for kafka(version 0.9) source.
Use SimpleWordProducer in [kafka](../kafka/README.md) subproject to generate test data.


#### [SocketStreamWordCountExample](src/main/scala/gx/flink/demo/examples/streaming/SocketStreamWordCountExample.scala)
A word count example for socket source.


## SQL Examples

#### [Kafka09JsonTableExample](src/main/scala/gx/flink/demo/examples/sql/Kafka09JsonTableExample.scala)
Process kafka source in json format using sql.
Use SimpleJsonProducer in [kafka](../kafka/README.md) subproject to generate test data.


#### [Kafka09CsvTableExample](src/main/scala/gx/flink/demo/examples/sql/Kafka09CsvTableExample.scala)
Process kafka source in csv format using sql.
Use SimpleCsvProducer in [kafka](../kafka/README.md) subproject to generate test data.
In this case, we used self-defined TableSource, Kafka09CsvTableSource, since flink do not have out-of-box supporting for csv format from kafka source.


#### [TwoStreamsWindowJoinExample](src/main/scala/gx/flink/demo/examples/sql/TwoStreamsWindowJoinExample.scala)
Demonstrates joining two streams using sql.


#### DimensionTableJoinExample
**TBD**: demonstrates stream table join with dimension table using table api.


#### GBaseSinkExample
**TBD**: sink query result to GBase table.

