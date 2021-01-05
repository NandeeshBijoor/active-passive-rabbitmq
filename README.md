# Cluster RabbitMQ

Starts two instnaces of rabbitmq containers which will work in active-passive mode

## Install

```
> git clone https://github.com/NandeeshBijoor/active-passive-rabbitmq.git
> cd active-passive-rabbitmq
> docker-compose up OR docker-compose up -d (detached mode)
```

Most things will be how you expect:

* The default username and password are `admin`/`Admin@123`
* The broker accepts connections on `localhost:5672`
* The Management interface is found at `localhost:15672`
