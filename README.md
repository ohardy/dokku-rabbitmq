# RabbitMQ plugin for Dokku

Project: https://github.com/progrium/dokku

## Installation

```
cd /var/lib/dokku/plugins
git clone https://github.com/ohardy/dokku-rabbitmq rabbitmq
dokku plugins-install
```


## Commands
```
$ dokku help
    rabbitmq:console     <app>               Launch a RabbitMQ console for a given app
    rabbitmq:env         <app>               Get generated environment variables for <app>
    rabbitmq:url         <app>               Get DATABASE_URL for <app>
    rabbitmq:create      <app>               Create a RabbitMQ database
    rabbitmq:delete      <app>               Delete specified RabbitMQ database
    rabbitmq:link        <app> <another_app> Give environment variable of database of <app> to <another_app>
    rabbitmq:unlink      <another_app>       Unlink <another_app> to a database
    rabbitmq:restart                         Restart the RabbitMQ docker container and linked app
    rabbitmq:start                           Start the RabbitMQ docker container if it isn't running
    rabbitmq:stop                            Stop the RabbitMQ docker container
    rabbitmq:status                          Shows status of RabbitMQ
    rabbitmq:list                            List all databases
    rabbitmq:update                          Update this plugin
    rabbitmq:migrate                         Migrate
```

## Updating this plugin
Dokku doesn't handle plugin update. I made a pull request to dokku for that (https://github.com/progrium/dokku/pull/669)

So, each time you update this plugin with `git pull`, you need to call:
```
$ dokku rabbitmq:migrate
```

## Info
This plugin adds following environment variables to your app automatically:

* RABBITMQ_URL
* RABBITMQ_HOST
* RABBITMQ_PORT
* RABBITMQ_VHOST
* RABBITMQ_USER
* RABBITMQ_PASS

## Usage

### Start RabbitMQ:
```
$ dokku rabbitmq:start                 # Server side
..or..
$ ssh dokku@server rabbitmq:start      # Client side

```

### Stop RabbitMQ:
```
$ dokku rabbitmq:stop                 # Server side
..or..
$ ssh dokku@server rabbitmq:stop      # Client side

```

### Restart RabbitMQ:
```
$ dokku rabbitmq:restart                 # Server side
..or..
$ ssh dokku@server rabbitmq:restart      # Client side

```

### Create a new vhost/user:
```
$ dokku rabbitmq:create foo            # Server side
..or..
$ ssh dokku@server rabbitmq:create foo # Client side
```


## Link
You can link a database to an application :

- Create vhost/user:
```
$ dokku rabbitmq:create foo
```
- Push another_app to dokku and link it to foo with:
```
$ dokku rabbitmq:link foo another_app
```
- Environment variables for vhost/user foo will be available in another_app

## Unlink
```
$ dokku rabbitmq:unlink another_app # Server side
```
