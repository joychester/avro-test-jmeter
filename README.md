# Test Avro kafka message:

### Checkout project: https://github.com/corunet/kloadgen

### Topic management:
./kafka-topics --list --bootstrap-server localhost:9092
./kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic avro-test
./kafka-topics --delete --bootstrap-server localhost:9092 --topic avro-test

### Register a schema for a new topic:
curl -X POST -H "Content-Type: application/vnd.schemaregistry.v1+json" --data '{"schema": "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"my.examples\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"}]}"}' http://localhost:8081/subjects/avro-test-value/versions

### List Subject and Config:
curl -X GET http://localhost:8081/config/avro-test-value

curl -X GET http://localhost:8081/subjects

curl -X GET http://localhost:8081/subjects/avro-test-value/versions

curl -X GET http://localhost:8081/subjects/avro-test-value/versions/1
