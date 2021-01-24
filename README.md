# Active Passive RabbitMQ

Starts two instnaces of rabbitmq containers which will work in active-passive mode

## Prerequisites
Create a certificate(haproxy.pem) and keep it inside certificate folder

## Install

```
> git clone https://github.com/NandeeshBijoor/active-passive-rabbitmq.git
> cd active-passive-rabbitmq
> docker-compose up OR docker-compose up -d (detached mode)
```

## Enable clustering
docker exec -it active-passive-rabbitmq_rabbitmq2_1 sh -c "rabbitmqctl stop_app && rabbitmqctl join_cluster rabbit@rabbitmq1 && rabbitmqctl start_app"

## Check cluster status
docker exec -it active-passive-rabbitmq_rabbitmq1_1 rabbitmqctl cluster_status

## Access Rabbitmq

* The default username and password are `guest`/`guest`(Can be overriden through .env file)
* The broker accepts connections on `localhost:5672`
* The Management interface is found at `localhost:15672`

## Test active passive

* Access Rabbitmq Management Interface https://localhost:15672
* You see rabbit@rabbitmq1 in nodes list
* Remove rabbitmq1 container
* You see node changed to rabbit@rabbitmq2
