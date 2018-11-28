# kibana

[Running Kibana on Docker](https://www.elastic.co/guide/en/kibana/current/docker.html)

## Docker Image

[Docker @ Elastic](https://www.docker.elastic.co)

```bash
docker pull docker.elastic.co/kibana/kibana:6.5.1
```

## docker-compose.yml

| Environment Variable | Kibana Setting |
|---|---|
| SERVER_NAME | server.name |
| KIBANA_DEFAULTAPPID | kibana.defaultAppId |
| XPACK_MONITORING_ENABLED | xpack.monitoring.enabled |

```yml
version: '2'
services:
  kibana:
    hostname: kibana
    container_name: kibana
    image: docker.elastic.co/kibana/kibana:6.5.1
    volumes:
      - ./kibana.yml:/usr/share/kibana/config/kibana.yml
```

## kibana.yml

| Environment Variable | Docker Default |
|---|---|
| server.name | kibana |
| server.host | "0" |
| elasticsearch.url | http://elasticsearch:9200 |
| xpack.monitoring.ui.container.elasticsearch.enabled | true |

```yml
server.name: kibana
server.host: "0"
elasticsearch.url: http://elasticsearch:9200
elasticsearch.username: elastic
elasticsearch.password: changeme
xpack.monitoring.ui.container.elasticsearch.enabled: true
```
