# Description

This repo hosts the compose file code to host different docker services and expose them as services.

There will be single nginx service running on entire docker swarm cluster and each service has its won nginx config mounted on the nginx service


# Usage

Create network name `frontend` on the swarm cluster using below command

```
docker network create   --driver overlay  frontend

```


For service to deploy create a nginx conf that will be mounted in `/etc/nginx/conf.d/`


Create config file with name of the service and run the below command

Create the A record for each domain in conf to all nodes in the docker swarm

```

docker config create  addressbook_nginx_conf configs/addresbook.conf

```

Update docker compose to mount the conf under the below section:

```
    configs:
      - source: addressbook_nginx_conf
        target: /etc/nginx/conf.d/default.conf

```

# Run

``` 

docker stack deploy --compose-file docker-compose.yaml nginx

```

# For each new service create the config map with nginx configuration and add under `configs`


# The compose file refers to sample application in `https://github.com/santhu3064/addressbook-tomcat8`


