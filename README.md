# DataEngineService

To run this app, you'll be needing Kafka & Spark, Jdk 8. You can install all of that.
Or you can pull the docker image and run it directly.

instructions:
docker pull 23051999/dataengineservice

run the docker-compose.yaml file in the project, here it is:
This assumes ports 2181, 9092 and 8083 are free. If they are not, choose ports that suit you.

```
version: '3'
services:
  data-engine-service:
    build: .
    ports:
      - "8083:8083"
    links:
      - kafka
  zookeeper:
    image: zookeeper:3.7.0
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka
    ports:
      - "9092:9092"
    links:
      - zookeeper
    environment:
      KAFKA_ADVERTISED_HOST_NAME: kafka
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_CREATE_TOPICS: "GeoNodes:1:1,rawPlaces:1:1"
```

paste that script into a new file: docker-compose.yml and then run "docker-compose up"

