# DEBEZIUM
### Proof Of Concept of Using debezium with a postgresql database and sending the data to multiple outputs

``` 
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors/ -d '
{
"name": "elastic-sink4",
"config": {
"connector.class":
"io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
"tasks.max": "1",
"topics": "dbserver3.public.customers",
"connection.url": "http://elasticsearch:9200",
"transforms": "key",
"transforms.key.type": "org.apache.kafka.connect.transforms.ExtractField$Key",
"transforms.key.field": "id",
"key.ignore": "false",
"type.name": "customer",
"behavior.on.null.values": "ignore"
}
}'
```

### Adding data in the database

```
create database inventory
\c inventory
CREATE TABLE customers (
	id serial PRIMARY KEY,
	first_name VARCHAR ( 50 )  NOT NULL,
	last_name VARCHAR ( 50 ) NOT NULL,
	email VARCHAR ( 255 ) UNIQUE NOT NULL
);

insert into customers (id, first_name, last_name, email) values ( 1, c, p, cp@test.ro);
```
