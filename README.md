# spin-up the debezium connector using the debezium.json

curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors/ -d "@debezium.json"

# consume messages from the topic using kafka cat command using interactive shell

docker run --tty \
 --network postgres_debezium_cdc_default \
 confluentinc/cp-kafkacat \
 kafkacat -b kafka:9092 -C \
 -s key=s -s value=avro \
 -r http://schema-registry:8081 \
 -t postgres.public.student
