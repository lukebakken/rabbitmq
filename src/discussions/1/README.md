<!-- vim:tw=80
-->

## Setup

```
git clone https://github.com/lukebakken/rabbitmq.git rabbitmq-github.git
```

## Reproduction

https://github.com/lukebakken/rabbitmq/discussions/1

The root cause of this issue is that, when started via docker, RabbitMQ does not
seem to mind that `auth_ldap` settings are in a configuration file, even though
`rabbitmq_auth_backend_ldap` is not enabled.

```
make start
```

However, if you start RabbitMQ from source, it will fail to start:

```
cd development/rabbitmq/rabbitmq-server
make RABBITMQ_CONFIG_FILES="/home/lbakken/development/lukebakken/rabbitmq-github/src/discussions/1/conf.d" PLUGINS='rabbitmq_management rabbitmq_top' run-broker
```

The above results in the following errors, as expected:

```
2025-04-23 15:45:50.308350-07:00 [debug] <0.162.0> Applying Datatypes
2025-04-23 15:45:50.314024-07:00 [error] <0.162.0> You've tried to set auth_ldap.servers.1, but there is no setting with that name.
2025-04-23 15:45:50.314076-07:00 [error] <0.162.0>   Did you mean one of these?
2025-04-23 15:45:50.338608-07:00 [error] <0.162.0>     auth_backends.$num
2025-04-23 15:45:50.338667-07:00 [error] <0.162.0>     auth_mechanisms.$name
2025-04-23 15:45:50.338716-07:00 [error] <0.162.0>     log.ra.level
2025-04-23 15:45:50.338867-07:00 [error] <0.162.0> You've tried to set auth_ldap.use_ssl, but there is no setting with that name.
```
