# Pulsar manager backend

Pulsar manager backend is a supplement and improvement to Pulsar broker.

* Handle complex query requests
* Route requests (add, delete, update) to brokers
* Support multi broker, dynamic change environment

### Supported configurations of backend 

| Name | Default |Description
| ------- | ------- | ------- |
| `server.port` | 7750 | Port of backend service |
| `pulsar-manager.account` | pulsar | Login account |
| `pulsar-manager.password` | pulsar | Login password |
| `redirect.host` | localhost | IP address of front-end service |
| `redirect.port` | 9527 | Port of front-end service |
| `insert.stats.interval` | 30000ms | Time interval for collecting statistical information |
| `clear.stats.interval` | 300000ms | Time interval for cleaning statistics |

### How to set parameters when starting back-end services

```
java -jar ./build/libs/pulsar-manager.jar --redirect.host=http://localhost --redirect.port=9527 insert.stats.interval=600000
```

### Use custom databases

If you have a large amount of data, you can use a custom database. The following is an example of PostgreSQL.   

1. Initialize database and table structures using [file](https://github.com/streamnative/pulsar-manager/tree/master/src/main/resources/META-INF/sql/postgresql-schema.sql).

2. Modify the [configuration file](https://github.com/streamnative/pulsar-manager/blob/master/src/main/resources/application.properties) and add PostgreSQL configuration

```
spring.datasource.driver-class-name=org.postgresql.Driver
spring.datasource.url=jdbc:postgresql://127.0.0.1:5432/pulsar_manager
spring.datasource.username=postgres
spring.datasource.password=postgres
```

3. Compile to generate a new executable jar package

```
./gradlew -x build -x test
```
