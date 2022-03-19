##CDC debezium source DB2 to sink DB2
### Installation steps
- Install docker and docker compose 
- Run `docker-compose up -d`
- Run `docker-compose ps` command to make sure all conteiners are up on running
- Run   `docker logs -f db2-cdc_db2server2_1` command to see db2 entire setup is complete , it will take 5 to 10 min 
- For kafka UI use this link [control center](http://localhost:9021)
- Check both source and sink db2 connection using any IDE
- Follow below setup integrate connectors  
 
 ## Register connector 
 > curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @source.json
 > curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @jdbc-sink.json
## Delete connector
> curl -X DELETE http://localhost:8083/connectors/<connecto name>


### List all consumers
> docker-compose -f docker-compose.yaml exec kafka /kafka/bin/kafka-consumer-groups.sh     --bootstrap-server kafka:9092      --list
### Describe consumer
> docker-compose -f docker-compose.yaml exec kafka /kafka/bin/kafka-consumer-groups.sh     --bootstrap-server kafka:9092      --describe --group  connect-jdbc-sink
### console Consumer  
> docker-compose -f docker-compose.yaml exec kafka /kafka/bin/kafka-console-consumer.sh     --bootstrap-server kafka:9092     --from-beginning     --property print.key=true     --topic db2server.DB2INST1.CUSTOMERS


