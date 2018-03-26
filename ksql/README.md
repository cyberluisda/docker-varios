# Description #

Simple pipeline with `Kafka SQL` stand-alone instance with kafka, zookeeper,
**without** _Schema registry_

## Starts pipline ##

```bash
docker-compose up target
```

## Execute commands with `ksql-cli` ##

```bash
docker-compose run --rm ksql-cli
```

This starts in interacive mode, and now we can exec _KSQL_ commands:

```sql
ksql> CREATE STREAM source_json_view (name varchar, value double, time varchar) WITH ( kafka_topic='source_json', value_format='JSON');

ksql> DESCRIBE source_json_view;

ksql> select STRINGTOTIMESTAMP(time, 'yyyy-MM-dd HH:mm:ssZZZZZ') as timestamp, name, value  from source_json_view;
```

**In adition** set `STRINGTOTIMESTAMP` with new _stream_. This will create new
topic `SOURCE_JSON_TIMESTAMP_VIEW` with data transformed.

```sql
ksql> CREATE STREAM source_json_timestamp_view \
  WITH (value_format='JSON') AS \
  SELECT \
    name, \
    value, \
    STRINGTOTIMESTAMP(time, 'yyyy-MM-dd HH:mm:ssZZZZZ') as timestamp \
  FROM source_json_view ;

ksql> DESCRIBE source_json_timestamp_view;

ksql> select * from source_json_timestamp_view;
```

Using `TABLE`

**TODO**

Now you can run _Ingest data_ commands in order to see select value in other
terminal instance.

## Ingest data ##

```bash
echo "{ \
\"time\": \"$(date +'%Y-%m-%d %H:%M:%S%z')\", \
\"name\": \"name1\", \
\"value\": 1234 \
}" | docker-compose run --rm kafka-ctl produce source_json
```
