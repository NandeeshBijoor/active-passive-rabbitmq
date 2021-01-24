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
`docker exec -it active-passive-rabbitmq_rabbitmq2_1 sh -c "rabbitmqctl stop_app && rabbitmqctl join_cluster rabbit@rabbitmq1 && rabbitmqctl start_app"`

## Check cluster status
`docker exec -it active-passive-rabbitmq_rabbitmq1_1 rabbitmqctl cluster_status`

## Access Rabbitmq
* Rabbitmq Management Interface https://localhost:15672 #SSL enabled
* The default username and password are `guest`/`guest`(Can be overriden through .env file)
* The broker accepts connections on `localhost:5672`

## Manual Testing Completed
```
...
rabbitmq1_1  | 2021-01-24 18:56:19.573 [warning] <0.1055.0> HTTP access denied: user 'test' - invalid credentials #Accessed the UI with invalid credentials
rabbitmq1_1  | 2021-01-24 18:57:03.116 [info] <0.60.0> SIGTERM received - shutting down #Stopped rabbitmq1 container
rabbitmq1_1  | 2021-01-24 18:57:03.119 [warning] <0.627.0> HTTP listener registry could not find context rabbitmq_prometheus_tls
rabbitmq1_1  | 2021-01-24 18:57:03.446 [warning] <0.627.0> HTTP listener registry could not find context rabbitmq_management_tls
rabbitmq1_1  | 2021-01-24 18:57:03.458 [info] <0.272.0> Peer discovery backend rabbit_peer_discovery_classic_config does not support registration, skipping unregistration.
rabbitmq1_1  | 2021-01-24 18:57:03.458 [info] <0.876.0> stopped TCP listener on [::]:5672
rabbitmq1_1  | 2021-01-24 18:57:03.461 [info] <0.515.0> Closing all connections in vhost '/' on node 'rabbit@rabbitmq1' because the vhost is stopping
rabbitmq1_1  | 2021-01-24 18:57:03.467 [info] <0.532.0> Stopping message store for directory '/var/lib/rabbitmq/mnesia/rabbit@rabbitmq1/msg_stores/vhosts/628WB79CIFDYO9LJI6DKMI09L/msg_store_persistent'
rabbitmq1_1  | 2021-01-24 18:57:03.471 [info] <0.532.0> Message store for directory '/var/lib/rabbitmq/mnesia/rabbit@rabbitmq1/msg_stores/vhosts/628WB79CIFDYO9LJI6DKMI09L/msg_store_persistent' is stopped
rabbitmq1_1  | 2021-01-24 18:57:03.471 [info] <0.527.0> Stopping message store for directory '/var/lib/rabbitmq/mnesia/rabbit@rabbitmq1/msg_stores/vhosts/628WB79CIFDYO9LJI6DKMI09L/msg_store_transient'
rabbitmq1_1  | 2021-01-24 18:57:03.475 [info] <0.527.0> Message store for directory '/var/lib/rabbitmq/mnesia/rabbit@rabbitmq1/msg_stores/vhosts/628WB79CIFDYO9LJI6DKMI09L/msg_store_transient' is stopped
rabbitmq2_1  | 2021-01-24 18:57:03.482 [info] <0.507.0> rabbit on node rabbit@rabbitmq1 down
rabbitmq2_1  | 2021-01-24 18:57:03.495 [info] <0.507.0> Keeping rabbit@rabbitmq1 listeners: the node is already back
rabbitmq2_1  | 2021-01-24 18:57:03.516 [info] <0.507.0> node rabbit@rabbitmq1 down: connection_closed
active-passive-rabbitmq_rabbitmq1_1 exited with code 0
rabbitmq2_1  | 2021-01-24 18:57:59.315 [warning] <0.1139.0> HTTP access denied: user 'test' - invalid credentials #Accessed the UI again with invalid credentials, this time request got to rabbitmq2
```
